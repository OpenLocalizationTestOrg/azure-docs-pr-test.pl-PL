---
title: "Azure Toolkit for IntelliJ: tworzenie aplikacji Spark dla klastra usługi HDInsight | Dokumentacja firmy Microsoft"
description: "Zestaw narzędzi platformy Azure dla IntelliJ umożliwia tworzenie aplikacji Spark napisanych w języku Scala i przesyłanie ich do klastra Spark w usłudze HDInsight."
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
ms.openlocfilehash: 19cb8f436fa4d86f323013a5d4b3b50bf6c80a1a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="use-azure-toolkit-for-intellij-to-create-spark-applications-for-an-hdinsight-cluster"></a>Zestaw narzędzi platformy Azure dla IntelliJ umożliwia tworzenie aplikacji Spark dla klastra usługi HDInsight

Użyj narzędzi Azure for IntelliJ wtyczki do tworzenia aplikacji Spark napisanych w języku Scala i przesyłanie ich do klastra Spark w usłudze HDInsight bezpośrednio z IntelliJ zintegrowane środowisko programistyczne (IDE). Można użyć wtyczki na kilka sposobów:

* Tworzenie i przesyłanie aplikacji Scala Spark w klastrze Spark w usłudze HDInsight.
* Dostęp do zasobów klastra Azure HDInsight Spark.
* Tworzenie i uruchamianie aplikacji Scala Spark lokalnie.

Aby utworzyć projekt, Wyświetl [tworzenie aplikacji Spark narzędzi Azure dla IntelliJ](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ) wideo.

> [!IMPORTANT]
> Ten dodatek można użyć, aby utworzyć i przesłać aplikacji tylko w przypadku klastra Spark w usłudze HDInsight w systemie Linux.
> 

## <a name="prerequisites"></a>Wymagania wstępne

- Klaster Apache Spark w usłudze HDInsight w systemie Linux. Aby uzyskać instrukcje, zobacz [klastrów utworzyć Apache Spark w usłudze Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).
- Oracle Java Development Kit. Możesz zainstalować ją z [witryny sieci Web programu Oracle](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).
- IntelliJ IDEA. W tym artykule używa wersji 2017.1. Możesz zainstalować ją z [JetBrains witryny sieci Web](https://www.jetbrains.com/idea/download/).

## <a name="install-azure-toolkit-for-intellij"></a>Zainstaluj zestaw narzędzi platformy Azure dla IntelliJ
Aby uzyskać instrukcje instalacji, zobacz [zainstalować zestaw narzędzi platformy Azure dla IntelliJ](../azure-toolkit-for-intellij-installation.md).

## <a name="sign-in-to-your-azure-subscription"></a>Zaloguj się do Twojej subskrypcji platformy Azure.

1. Uruchom IntelliJ IDE, a następnie otwórz Eksploratora Azure. Na **widoku** menu, wybierz opcję **okna narzędzi**, a następnie wybierz **Eksploratora Azure**.
       
   ![Łącze Eksploratora Azure](./media/hdinsight-apache-spark-intellij-tool-plugin/show-azure-explorer.png)

2. Kliknij prawym przyciskiem myszy **Azure** węzeł, a następnie wybierz **logowania**.

3. W **Azure logowania** wybierz pozycję **Zaloguj się**, a następnie wprowadź poświadczenia platformy Azure.

    ![Okno dialogowe Azure logowania](./media/hdinsight-apache-spark-intellij-tool-plugin/view-explorer-2.png)

4. Po zalogowaniu, **Wybierz subskrypcje** okno dialogowe wyświetla wszystkie subskrypcje platformy Azure, które są skojarzone z poświadczeniami. Wybierz **wybierz** przycisku.

    ![Okno dialogowe Wybieranie subskrypcji](./media/hdinsight-apache-spark-intellij-tool-plugin/Select-Subscriptions.png)

5. Na **Eksploratora Azure** karcie, rozwiń **HDInsight** do wyświetlania klastrów HDInsight Spark, które znajdują się w Twojej subskrypcji.
   
    ![Klastry HDInsight Spark w Eksploratorze Azure](./media/hdinsight-apache-spark-intellij-tool-plugin/view-explorer-3.png)

6. Aby wyświetlić zasoby, które są skojarzone z klastrem (na przykład konta magazynu), można rozwinąć węzła nazwy klastra.
   
    ![Nazwa klastra węzłów](./media/hdinsight-apache-spark-intellij-tool-plugin/view-explorer-4.png)

## <a name="run-a-spark-scala-application-on-an-hdinsight-spark-cluster"></a>Uruchamianie aplikacji Spark Scala w klastrze Spark w usłudze HDInsight

1. Uruchom IntelliJ IDEA, a następnie utworzyć projekt. W **nowy projekt** okno dialogowe, wykonaj następujące czynności: 

   a. Wybierz **HDInsight** > **Spark w usłudze HDInsight (Scala)**.

   b. W **narzędzia kompilacji** listy, wybierz jedną z następujących czynności, w zależności od potrzeb:

      * **Maven**, obsługę języka Scala Kreator tworzenia projektu
      * **SBT**, do zarządzania zależności i budowania projektu języka Scala

    ![Okno dialogowe nowego projektu](./media/hdinsight-apache-spark-intellij-tool-plugin/create-hdi-scala-app.png)

2. Wybierz **dalej**.

3. Kreator tworzenia projektu Scala automatycznie wykrywa, czy po zainstalowaniu Scala wtyczki. Wybierz **zainstalować**.

   ![Scala wtyczki wyboru](./media/hdinsight-apache-spark-intellij-tool-plugin/Scala-Plugin-check-Reminder.PNG) 

4. Aby pobrać dodatek plug-in Scala, wybierz **OK**. Postępuj zgodnie z instrukcjami, aby ponownie uruchomić środowisko IntelliJ. 

   ![Okno dialogowe Scala wtyczki instalacji](./media/hdinsight-apache-spark-intellij-tool-plugin/Choose-Scala-Plugin.PNG)

5. W **nowy projekt** okna, wykonaj następujące czynności:  

    ![Wybieranie Spark zestawu SDK](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-new-project.png)

   a. Wprowadź nazwę projektu i lokalizację.

   b. W **SDK projektu** listy rozwijanej wybierz **Java 1.8** dla klastra Spark 2.x lub wybierz **Java 1.7** 1.x klastra Spark.

   c. W **wersji Spark** listy rozwijanej, Kreator tworzenia projektu Scala integruje poprawnej wersji dla platformy Spark zestawy SDK i Scala. Jeśli wersja klastra Spark jest starsza niż 2.0, wybierz **Spark 1.x**. W przeciwnym razie wybierz **Spark2.x**. W tym przykładzie użyto **Spark pkt 2.0.2 (Scala 2.11.8)**.

6. Wybierz pozycję **Finish** (Zakończ).

7. Projekt Spark automatycznie utworzy artefaktu. Aby wyświetlić artefakt, wykonaj następujące czynności:

   a. Na **pliku** menu, wybierz opcję **struktury projektu**.

   b. W **struktury projektu** okno dialogowe, wybierz opcję **artefakty** Aby wyświetlić artefaktu domyślny, który jest tworzony. Można również tworzyć własne artefaktu, wybierając znak plus (**+**).

      ![W oknie dialogowym, informacje o artefaktów](./media/hdinsight-apache-spark-intellij-tool-plugin/default-artifact.png)
      
8. Dodaj kod źródłowy aplikacji, wykonując następujące czynności:

   a. W obszarze Eksplorator projektów kliknij prawym przyciskiem myszy **src**, wskaż polecenie **nowy**, a następnie wybierz **klasy Scala**.
      
      ![Polecenia służące do tworzenia klasy Scala w Eksploratorze projektu](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-scala-code.png)

   b. W **Utwórz nową klasę Scala** okna dialogowego polu, podaj nazwę, wybierz **obiektu** w **rodzaj** , a następnie wybierz **OK**.
      
      ![Tworzenie nowej klasy Scala, okno dialogowe](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-scala-code-object.png)

   c. W **MyClusterApp.scala** plików, wklej następujący kod. Ten kod odczytuje dane z HVAC.csv (dostępne na wszystkich klastrach HDInsight Spark), pobiera wierszy, które zawierają tylko jedna cyfra siódmego kolumny w pliku CSV i zapisuje dane wyjściowe do **/HVACOut** w obszarze domyślnego kontenera magazynu dla klastra.

        import org.apache.spark.SparkConf
        import org.apache.spark.SparkContext
    
        object MyClusterApp{
            def main (arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("MyClusterApp")
            val sc = new SparkContext(conf)
    
            val rdd = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")
    
            //find the rows that have only one digit in the seventh column in the CSV file
            val rdd1 =  rdd.filter(s => s.split(",")(6).length() == 1)
    
            rdd1.saveAsTextFile("wasb:///HVACOut")
            }
    
        }

9. Uruchom aplikację w klastrze Spark w usłudze HDInsight, wykonując następujące czynności:

   a. W obszarze Eksplorator projektów kliknij prawym przyciskiem myszy nazwę projektu, a następnie wybierz **przesyłanie aplikacji Spark HDInsight**.
      
      ![Aplikacji Spark przesłać do polecenia HDInsight](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-submit-spark-app-1.png)

   b. Monit o podanie poświadczeń subskrypcji platformy Azure. W **przesyłanie Spark** okno dialogowe, podaj następujące wartości, a następnie wybierz **przesyłania**.
      
      * Aby uzyskać **Spark klastrów (tylko w systemie Linux)**, wybierz klaster Spark w usłudze HDInsight, na którym chcesz uruchomić aplikację.

      * Wybierz artefakt z projektu IntelliJ lub wybierz jeden z dysku twardego.

      * W **Nazwa klasy głównym** wybierz wielokropek (**...** ), wybierz klasy głównym w kodzie źródłowym aplikacji, a następnie wybierz **OK**.

        ![Okno dialogowe Wybieranie klasy głównym](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-submit-spark-app-3.png)

      * Kod aplikacji, w tym przykładzie wymaga argumentów wiersza polecenia lub odwołać słoików lub pliki, pozostałe pola można pozostawić pusty. Po podaniu wszystkich informacji okno dialogowe powinno przypominać następujące obrazu.
        
        ![Okno dialogowe przesyłanie Spark](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-submit-spark-app-2.png)

   c. **Przesyłanie Spark** u dołu okna powinna zaczynać się wyświetlanie postępu. Można również Zatrzymaj aplikację, wybierając czerwony przycisk w **przesyłanie Spark** okna.
      
      ![Przesłanie Spark okna](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-app-result.png)
      
      Aby dowiedzieć się, jak uzyskać dostępu do danych wyjściowych zadania, zobacz "dostępu i zarządzania klastrami Spark w usłudze HDInsight przy użyciu zestawu narzędzi platformy Azure dla IntelliJ" sekcji w dalszej części tego artykułu.

## <a name="run-or-debug-a-spark-scala-application-on-an-hdinsight-spark-cluster"></a>Uruchom lub debugowanie aplikacji Spark Scala w klastrze Spark w usłudze HDInsight
Zalecamy również innym sposobem przesyłanie aplikacji Spark dla klastra. Możesz to zrobić przez ustawienie parametrów **konfiguracji uruchomienia/debugowania** IDE. Aby uzyskać więcej informacji, zobacz [zdalne debugowanie aplikacji Spark w klastrze usługi HDInsight narzędzi Azure for IntelliJ za pośrednictwem protokołu SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh).

## <a name="access-and-manage-hdinsight-spark-clusters-by-using-azure-toolkit-for-intellij"></a>Dostęp i zarządzania klastrami Spark w usłudze HDInsight przy użyciu zestawu narzędzi platformy Azure dla IntelliJ
Różne operacje można wykonywać za pomocą narzędzi Azure for IntelliJ.

### <a name="access-the-job-view"></a>Dostęp do widoku zadania
1. W Eksploratorze Azure rozwiń **HDInsight**, rozwiń nazwę klastra Spark, a następnie wybierz **zadania**.  

    ![Zadania widoku węzła](./media/hdinsight-apache-spark-intellij-tool-plugin/job-view-node.png)

2. W okienku po prawej stronie **widoku zadania Spark** karcie są wyświetlane wszystkie aplikacje, które zostały uruchomione w klastrze. Wybierz nazwę aplikacji, dla którego chcesz zobaczyć więcej szczegółów.

    ![Szczegóły aplikacji](./media/hdinsight-apache-spark-intellij-tool-plugin/view-job-logs.png)

3. Aby wyświetlić podstawowe informacje o zadaniu uruchomione, umieść kursor nad wykresu zadania. Aby wyświetlić wykres etapów i informacje, które generuje każde zadanie, wybierz węzeł na wykresie zadania.

    ![Szczegóły etap zadania](./media/hdinsight-apache-spark-intellij-tool-plugin/Job-graph-stage-info.png)

4. Często używane dzienniki, taką jak *Stderr sterownika*, *Stdout sterownika*, i *informacji o katalogu*, wybierz pozycję **dziennika** kartę.

    ![Szczegóły dziennika](./media/hdinsight-apache-spark-intellij-tool-plugin/Job-log-info.png)

5. Można również wyświetlić historię Spark interfejsu użytkownika i interfejsie użytkownika YARN (na poziomie aplikacji), klikając łącze w górnej części okna.

### <a name="access-the-spark-history-server"></a>Dostęp do serwera historii Spark
1. W Eksploratorze Azure rozwiń **HDInsight**, kliknij prawym przyciskiem myszy nazwę klastra Spark, a następnie wybierz **Otwórz użytkownika usługi Historia Spark**. 

2. Po wyświetleniu monitu wprowadź poświadczenia administratora klastra, które zostało określone podczas konfigurowania klastra.

3. Na pulpicie nawigacyjnym serwera Spark historii nazwę aplikacji służy do wyszukania aplikacji właśnie zakończono uruchomiona. W powyższym kodzie, należy określić nazwę aplikacji przy użyciu `val conf = new SparkConf().setAppName("MyClusterApp")`. W związku z tym jest nazwa aplikacji Spark **MyClusterApp**.

### <a name="start-the-ambari-portal"></a>Uruchom portalu Ambari
1. W Eksploratorze Azure rozwiń **HDInsight**, kliknij prawym przyciskiem myszy nazwę klastra Spark, a następnie wybierz **Otwórz Portal zarządzania klastra (Ambari)**. 

2. Po wyświetleniu monitu wprowadź poświadczenia administratora klastra. Te poświadczenia zostały określone podczas procesu konfigurowania klastra.

### <a name="manage-azure-subscriptions"></a>Zarządzać subskrypcjami platformy Azure
Domyślnie zestaw narzędzi platformy Azure dla IntelliJ wymieniono klastry Spark wszystkie subskrypcje platformy Azure. Jeśli to konieczne, można określić subskrypcje, które chcesz uzyskać dostęp. 

1. W Eksploratorze Azure, kliknij prawym przyciskiem myszy **Azure** węzła głównego, a następnie wybierz **Zarządzaj subskrypcjami**. 

2. W oknie dialogowym, wyczyść pola wyboru obok subskrypcje, które nie mają dostępu, a następnie wybierz **Zamknij**. Możesz też wybrać **Wyloguj** Aby wylogować się z subskrypcją platformy Azure.

## <a name="run-a-spark-scala-application-locally"></a>Uruchamianie aplikacji Spark Scala lokalnie
Zestaw narzędzi platformy Azure dla IntelliJ umożliwia uruchamianie aplikacji Spark Scala lokalnie na stacji roboczej. Aplikacje zazwyczaj nie potrzebują dostępu do zasobów klastra, takich jak kontenery magazynu i można uruchomić i przetestować je lokalnie.

### <a name="prerequisite"></a>Wymagania wstępne
Gdy używasz lokalnych aplikacji Spark Scala na komputerze z systemem Windows, można uzyskać wyjątku, zgodnie z objaśnieniem w [SPARK 2356](https://issues.apache.org/jira/browse/SPARK-2356). Wyjątek występuje, ponieważ brakuje WinUtils.exe w systemie Windows. 

Aby rozwiązać ten problem, [Pobierz plik wykonywalny](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) do lokalizacji, takie jak **C:\WinUtils\bin**. Następnie należy dodać zmienną środowiskową **HADOOP_HOME**, a następnie ustaw wartość zmiennej **C\WinUtils**.

### <a name="run-a-local-spark-scala-application"></a>Uruchamianie aplikacji Spark Scala lokalnej
1. Uruchom IntelliJ IDEA i tworzenia projektu. 

2. W **nowy projekt** okno dialogowe, wykonaj następujące czynności:
   
    a. Wybierz **HDInsight** > **Spark dla próbki uruchamiania lokalnego HDInsight (Scala)**.

    b. W **narzędzia kompilacji** listy, wybierz jedną z następujących czynności, w zależności od potrzeb:

      * **Maven**, obsługę języka Scala Kreator tworzenia projektu
      * **SBT**, do zarządzania zależności i budowania projektu języka Scala

    ![Okno dialogowe nowego projektu](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-app-local-run.png)

3. Wybierz **dalej**.
 
4. W następnym oknie wykonaj następujące czynności:
   
    a. Wprowadź nazwę projektu i lokalizację.

    b. W **SDK projektu** listy rozwijanej wybierz wersję Java, która jest nowsza niż wersja 1.7.

    c. W **wersji Spark** listy rozwijanej wybierz wersję języka Scala, którego chcesz używać: Scala 2.11.x dla platformy Spark w wersji 2.0 lub Scala 2.10.x dla wersji 1.6 Spark.

    ![Okno dialogowe nowego projektu](./media/hdinsight-apache-spark-intellij-tool-plugin/Create-local-project.PNG)

5. Wybierz pozycję **Finish** (Zakończ).

6. Przykładowy kod dodaje szablonu (**LogQuery**) w obszarze **src** folderu, który można uruchomić lokalnie na komputerze.
   
    ![Lokalizacja LogQuery](./media/hdinsight-apache-spark-intellij-tool-plugin/local-app.png)

7. Kliknij prawym przyciskiem myszy **LogQuery** aplikacji, a następnie wybierz **Uruchom "LogQuery"**. Na **Uruchom** kartę na dole pojawić się dane wyjściowe, takie jak następujące:
   
   ![Aplikacji Spark lokalnego wynik uruchomienia](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-app-local-run-result.png)

## <a name="convert-existing-intellij-idea-applications-to-use-azure-toolkit-for-intellij"></a>Konwertowanie istniejących aplikacji IntelliJ IDEA do użycia narzędzi Azure for IntelliJ
Możesz przekształcić istniejącą Spark Scala aplikacji utworzonej w IntelliJ IDEA, aby był zgodny z narzędzi Azure dla IntelliJ. Następnie można wtyczki przesyłania aplikacji do klastra Spark w usłudze HDInsight.

1. Dla istniejącej aplikacji Spark Scala, który został utworzony za pomocą IntelliJ IDEA Otwórz plik .iml skojarzone.

2. W katalogu głównym poziom jest **modułu** element podobnie do następującej:
   
        <module org.jetbrains.idea.maven.project.MavenProjectsManager.isMavenModule="true" type="JAVA_MODULE" version="4">

   Zmodyfikuj element, aby dodać `UniqueKey="HDInsightTool"` , aby **modułu** element wygląda podobnie do następującej:
   
        <module org.jetbrains.idea.maven.project.MavenProjectsManager.isMavenModule="true" type="JAVA_MODULE" version="4" UniqueKey="HDInsightTool">

3. Zapisz zmiany. Aplikacja teraz powinno być zgodne z narzędzi Azure dla IntelliJ. Można przetestować go, klikając prawym przyciskiem myszy nazwę projektu w Eksploratorze projektu. Menu podręczne ma teraz opcję **przesyłanie aplikacji Spark HDInsight**.

## <a name="troubleshooting"></a>Rozwiązywanie problemów

### <a name="error-in-local-run-please-use-a-larger-heap-size"></a>Błąd podczas uruchamiania lokalnego: *Użyj większego rozmiaru sterty*
W wersji 1.6 Spark Jeśli używasz SDK Java 32-bitowych podczas przebiegu lokalnego, mogą wystąpić następujące błędy:

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

Te błędy się tak zdarzyć, ponieważ rozmiar stosu nie jest wystarczająco duży dla Spark do uruchomienia. Platforma Spark wymaga co najmniej 471 MB. (Aby uzyskać więcej informacji, zobacz [SPARK 12081](https://issues.apache.org/jira/browse/SPARK-12081).) Jeden prostym rozwiązaniem jest korzystanie z zestawu SDK Java 64-bitowych. Możesz również zmienić ustawienia maszyny JVM w IntelliJ, dodając następujące opcje:

    -Xms128m -Xmx512m -XX:MaxPermSize=300m -ea

![Dodanie opcji do pola "Opcje maszyny Wirtualnej" IntelliJ](./media/hdinsight-apache-spark-intellij-tool-plugin/change-heap-size.png)

## <a name="faq"></a>Często zadawane pytania
Aby przesłać aplikacji do usługi Azure Data Lake Store, wybierz **Interactive** tryb podczas Azure procesu logowania. W przypadku wybrania **automatycznego** tryb, możesz uzyskać wystąpił błąd.

![interakcyjny rejestrowanie](./media/hdinsight-apache-spark-intellij-tool-plugin/interative-signin.png)

Teraz możemy go rozwiązał. Można wybrać Azure Data Lake klastra do przesyłania aplikacji przy użyciu dowolnej metody logowania.

## <a name="feedback-and-known-issues"></a>Opinie i znane problemy
Przeglądanie wyjść Spark bezpośrednio nie jest obecnie obsługiwana.

Jeśli masz jakiekolwiek sugestie lub opinii lub jeśli wystąpią problemy, korzystając z tego dodatku, wiadomość e-mail na adres hdivstool@microsoft.com.

## <a name="seealso"></a>Następne kroki
* [Przegląd: platforma Apache Spark w usłudze Azure HDInsight](hdinsight-apache-spark-overview.md)

### <a name="demo"></a>Demonstracja
* Tworzenie projektu Scala (klip wideo): [tworzenie Spark Scala aplikacji](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)
* Debugowanie zdalne (klip wideo): [użyj narzędzi Azure dla IntelliJ debugowanie aplikacji Spark zdalnie w klastrze usługi HDInsight](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)

### <a name="scenarios"></a>Scenariusze
* [Platforma Spark w usłudze BI: wykonaj interakcyjna analiza danych przy użyciu platformy Spark w usłudze HDInsight z narzędzi do analizy Biznesowej](hdinsight-apache-spark-use-bi-tools.md)
* [Platforma Spark przy użyciu Machine Learning: Korzystanie z platformy Spark w usłudze HDInsight do analizy temperatury w budynku z użyciem danych HVAC](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Platforma Spark i usługa Machine Learning: korzystanie z platformy Spark w usłudze HDInsight do przewidywania wyników kontroli żywności](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Przesyłanie strumieniowe Spark: Korzystanie z platformy Spark w usłudze HDInsight do tworzenia aplikacji przesyłania strumieniowego w czasie rzeczywistym](hdinsight-apache-spark-eventhub-streaming.md)
* [Analiza dzienników witryny sieci Web na platformie Spark w usłudze HDInsight](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="creating-and-running-applications"></a>Tworzenie i uruchamianie aplikacji
* [Tworzenie autonomicznych aplikacji przy użyciu języka Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Zdalne uruchamianie zadań w klastrze Spark przy użyciu programu Livy](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a>Narzędzia i rozszerzenia
* [Debugowanie aplikacji Spark zdalnie za pośrednictwem sieci VPN przy użyciu zestawu narzędzi Azure for IntelliJ](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Debugowanie aplikacji Spark zdalnie za pośrednictwem usługi SSH przy użyciu zestawu narzędzi Azure for IntelliJ](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md)
* [Użyj narzędzia HDInsight Tools for IntelliJ z Hortonworks piaskownicy](hdinsight-tools-for-intellij-with-hortonworks-sandbox.md)
* [Użyj narzędzia HDInsight Tools w zestawie narzędzi Azure dla programu Eclipse tworzenie aplikacji Spark](hdinsight-apache-spark-eclipse-tool-plugin.md)
* [Korzystanie z notesów Zeppelin w klastrze Spark w usłudze HDInsight](hdinsight-apache-spark-zeppelin-notebook.md)
* [Jądra dostępne dla notesu Jupyter w klastrze Spark w usłudze HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Korzystanie z zewnętrznych pakietów z notesami Jupyter](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Instalacja oprogramowania Jupyter na komputerze i nawiązywanie połączenia z klastrem Spark w usłudze HDInsight](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="managing-resources"></a>Zarządzanie zasobami
* [Zarządzanie zasobami klastra Apache Spark w usłudze Azure HDInsight](hdinsight-apache-spark-resource-manager.md)
* [Śledzenie i debugowanie zadań uruchamianych w klastrze Apache Spark w usłudze HDInsight](hdinsight-apache-spark-job-debugging.md)

