---
title: "aaaAzure narzędzi dla programu Eclipse — Scala tworzenie aplikacji Spark w usłudze HDInsight | Dokumentacja firmy Microsoft"
description: "Narzędzia HDInsight Tools w zestawie narzędzi Azure dla aplikacji Spark toodevelop Eclipse napisanych w języku Scala i przesłać je tooan klastra Spark w usłudze HDInsight, bezpośrednio z hello Eclipse IDE."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: f6c79550-5803-4e13-b541-e86c4abb420b
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/24/2017
ms.author: nitinme
ms.openlocfilehash: 3ab70857c1e81f591a1c7e29bc1706ec4899ff58
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-toolkit-for-eclipse-toocreate-spark-applications-for-an-hdinsight-cluster"></a>Użyj narzędzi Azure dla programu Eclipse aplikacji Spark toocreate dla klastra usługi HDInsight

Użyj narzędzia HDInsight Tools w zestawie narzędzi Azure dla aplikacji Spark toodevelop Eclipse napisanych w języku Scala i przesyłanie ich tooan Azure HDInsight Spark klastra bezpośrednio z hello Eclipse IDE. Można użyć narzędzia HDInsight hello wtyczki na kilka różnych sposobów:

* toodevelop i przesyłanie aplikacji Scala Spark w klastrze Spark w usłudze HDInsight
* tooaccess zasobów klastra Spark w usłudze HDInsight Azure
* toodevelop i uruchamianie aplikacji Scala Spark lokalnie

> [!IMPORTANT]
> To narzędzie może być używane toocreate i przesyłanie aplikacji tylko dla klastra Spark w usłudze HDInsight w systemie Linux.
> 
> 

## <a name="prerequisites"></a>Wymagania wstępne

* Klaster Apache Spark w usłudze HDInsight. Aby uzyskać instrukcje, zobacz [klastrów utworzyć Apache Spark w usłudze Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).
* Oracle Java Development Kit w wersji 8, który służy do środowiska wykonawczego Eclipse IDE hello. Można go pobrać ze hello [witryny sieci Web programu Oracle](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).
* Środowisko Eclipse IDE. W tym artykule wykorzystano Eclipse Neon. Można ją zainstalować, korzystając z hello [witryny sieci Web w środowisku Eclipse](https://www.eclipse.org/downloads/).   
* Zestaw SDK platformy Spark. Możesz pobrać go z [GitHub](http://go.microsoft.com/fwlink/?LinkID=723585&clcid=0x409).


## <a name="install-hdinsight-tools-in-azure-toolkit-for-eclipse-and-scala-plugin"></a>Instalowanie narzędzi HDInsight Tools w zestawie narzędzi platformy Azure dla programu Eclipse i Scala wtyczki
### <a name="install-hdinsight-tools"></a>Instalowanie narzędzi HDInsight Tools
Narzędzia HDInsight Tools dla programu Eclipse jest dostępny jako część zestawu narzędzi platformy Azure dla programu Eclipse. Aby uzyskać instrukcje instalacji, zobacz [Instalowanie zestawu narzędzi platformy Azure dla programu Eclipse](../azure-toolkit-for-eclipse-installation.md).
### <a name="install-scala-plugin"></a>Instalowanie wtyczki Scala
Po otwarciu hello Intellij hello narzędzi HDInsight Tools automatycznie wykrywa, czy zainstalowano Scala wtyczki. Kliknij przycisk **OK** toocontinue i wykonaj tooinstall instrukcje hello przez hello Eclipse Marketplace.

 ![Automatyczne instalowanie Scala wtyczki](./media/hdinsight-apache-spark-eclipse-tool-plugin/auto-install-scala.png)

## <a name="sign-in-tooyour-azure-subscription"></a>Zaloguj się tooyour subskrypcji platformy Azure
1. Uruchom hello Eclipse IDE i Otwórz Eksploratora Azure. Na powitania **okna** menu, kliknij przycisk **Pokaż widok**, a następnie kliknij przycisk **innych**. Okno dialogowe hello otwiera, rozwiń węzeł **Azure**, kliknij przycisk **Eksploratora Azure**, a następnie kliknij przycisk **OK**.

    ![Pokaż okno dialogowe widoku](./media/hdinsight-apache-spark-eclipse-tool-plugin/view-explorer-1.png)
2. Kliknij prawym przyciskiem myszy hello **Azure** węzeł, a następnie kliknij przycisk **Zaloguj**.
3. W hello **Azure logowania** okno dialogowe, wybierz metodę uwierzytelniania powitania kliknij pozycję **Zaloguj**i wprowadź swoje poświadczenia usługi Azure.
   
    ![Azure logowania — okno dialogowe](./media/hdinsight-apache-spark-eclipse-tool-plugin/view-explorer-2.png)
4. Po zalogowaniu hello **Wybierz subskrypcje** okna dialogowego pole listy hello wszystkie subskrypcje platformy Azure skojarzone z poświadczeniami hello. Kliknij przycisk **wybierz** hello tooclose — okno dialogowe.

    ![Wybierz subskrypcje — okno dialogowe](./media/hdinsight-apache-spark-eclipse-tool-plugin/Select-Subscriptions.png)
5. Na powitania **Eksploratora Azure** karcie, rozwiń **HDInsight** hello toosee klastry Spark w usłudze HDInsight w ramach Twojej subskrypcji.
   
    ![Klastry HDInsight Spark w Eksploratorze Azure](./media/hdinsight-apache-spark-eclipse-tool-plugin/view-explorer-3.png)
6. Nazwa węzła toosee hello zasobów klastra (na przykład konta magazynu) skojarzony z klastrem hello można rozwinąć.
   
    ![Rozszerzanie zasobów toosee nazwa klastra](./media/hdinsight-apache-spark-eclipse-tool-plugin/view-explorer-4.png)



## <a name="set-up-a-spark-scala-project-for-an-hdinsight-spark-cluster"></a>Konfigurowanie projektu Spark Scala dla klastra Spark w usłudze HDInsight

1. W obszarze roboczym Eclipse IDE hello, kliknij przycisk **pliku**, kliknij przycisk **nowy**, a następnie kliknij przycisk **projektu**. 
2. W Kreatorze nowego projektu hello, rozwiń węzeł **HDInsight**, wybierz pozycję **Spark w usłudze HDInsight (Scala)**, a następnie kliknij przycisk **dalej**.

    ![Wybieranie hello Spark w usłudze HDInsight (Scala) projektu](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-hdi-scala-app-2.png)
3. Hello Scala projektu tworzenia Kreator automatycznie wykrywa, czy zainstalowano Scala wtyczki. Kliknij przycisk **OK** toocontinue pobieranie hello Scala dodatek, a następnie wykonaj hello instrukcje toorestart Eclipse.

    ![Scala wyboru](./media/hdinsight-apache-spark-eclipse-tool-plugin/auto-install-scala-2.png)
4. W hello **nowy projekt języka Scala HDInsight** okno dialogowe, podaj hello następujące wartości, a następnie kliknij **dalej**:
   * Wprowadź nazwę dla projektu hello.
   * W hello **środowiska JRE** obszaru, upewnij się, że **Użyj środowiska wykonawczego środowiska JRE** ustawiono zbyt**JavaSE 1.7** lub nowszym.
   * Upewnij się, że zestaw SDK platformy Spark jest zestaw toohello której pobrano hello zestawu SDK. Witaj lokalizacji pobierania toohello łącze znajduje się w hello [wymagania wstępne](#prerequisites) we wcześniejszej części tego artykułu. Możesz również pobrać hello zestawu SDK z hello łącze w oknie dialogowym hello.

    ![Okno dialogowe Nowy projekt języka Scala HDInsight](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-hdi-scala-app-3.png)
5.  W hello następnym oknie dialogowym kliknij hello **biblioteki** i Zachowaj hello wartości domyślne, a następnie kliknij **Zakończ**. 
   
    ![Karta biblioteki](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-hdi-scala-app-4.png)
  
## <a name="create-a-scala-application-for-an-hdinsight-spark-cluster"></a>Tworzenie aplikacji dla klastra usługi HDInsight Spark Scala

1. W hello Eclipse IDE, korzystając z Eksploratora pakietu, rozwiń węzeł projektu hello, który został utworzony wcześniej, kliknij prawym przyciskiem myszy **src**, punktu zbyt**nowy**, a następnie kliknij przycisk **innych**.
2. W hello **kreatora wybierz** okna dialogowego rozwiń **kreatorów języka Scala**, kliknij przycisk **obiektu Scala**, a następnie kliknij przycisk **dalej**.
   
    ![Wybierz okno dialogowe Kreator](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-scala-proj-1.png)
3. W hello **Utwórz nowy plik** okno dialogowe, wprowadź nazwę dla obiekt hello, a następnie kliknij przycisk **Zakończ**.
   
    ![Utwórz nowy plik — okno dialogowe](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-scala-proj-2.png)
4. Wklej hello następującego kodu w edytorze tekstu hello:
   
        import org.apache.spark.SparkConf
        import org.apache.spark.SparkContext
   
        object MyClusterApp{
          def main (arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("MyClusterApp")
            val sc = new SparkContext(conf)
   
            val rdd = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")
   
            //find hello rows that have only one digit in hello seventh column in hello CSV
            val rdd1 =  rdd.filter(s => s.split(",")(6).length() == 1)
   
            rdd1.saveAsTextFile("wasb:///HVACOut")
          }        
        }
5. Uruchom aplikację hello w klastrze Spark w usłudze HDInsight:
   
   1. W Eksploratorze pakietu, kliknij prawym przyciskiem myszy nazwę projektu hello, a następnie wybierz **tooHDInsight przesyłanie aplikacji Spark**.        
   2. W hello **przesyłanie Spark** okno dialogowe, podaj hello następujące wartości, a następnie kliknij **przesyłania**:
      
      * Aby uzyskać **nazwy klastra**, wybierz hello klaster Spark w usłudze HDInsight, na którym ma zostać toorun aplikacji.
      * Wybierz artefakt z projektu Eclipse hello, lub wybierz jedną z dysku twardego. Wartość domyślna Hello zależy od elementu hello prawym przyciskiem myszy w Eksploratorze pakietu.
      * W hello **Nazwa klasy głównym** dropdownlist, przesłanie Kreator wyświetla wszystkie nazwy obiektów z wybranego projektu. Wybierz lub wprowadź jedną, które mają toorun. W przypadku wybrania artefaktów z dysku twardego, należy wprowadzić nazwę klasy głównym samodzielnie. 
      * Kod aplikacji hello w tym przykładzie wymagają żadnych argumentów wiersza polecenia lub odwołać słoików lub pliki, można pozostawić hello pozostała pusta pól tekstowych.
        
       ![Przesłanie Spark — okno dialogowe](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-scala-proj-3.png)
   3. Witaj **przesyłanie Spark** kartę powinien rozpocząć hello postęp wyświetlania. Po kliknięciu przycisku hello red w hello można zatrzymać aplikacji hello **przesyłanie Spark** okna. Można również wyświetlić hello dzienników dla tej aplikacji określonych uruchomić, klikając ikona globu hello (wskazywane przez hello niebieskie pole w obrazie hello).
      
       ![Przesłanie Spark okna](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-scala-proj-4.png)

## <a name="access-and-manage-hdinsight-spark-clusters-by-using-hdinsight-tools-in-azure-toolkit-for-eclipse"></a>Dostęp i zarządzania klastrami Spark w usłudze HDInsight przy użyciu narzędzia HDInsight Tools w zestawie narzędzi Azure dla programu Eclipse
Za pomocą narzędzi HDInsight, takich jak uzyskiwanie dostępu do danych wyjściowych zadania hello można wykonywać różne operacje.

### <a name="access-hello-job-view"></a>Wyświetl zadania hello dostępu
1. W Eksploratorze Azure rozwiń **HDInsight**, rozwiń nazwę klastra Spark hello, a następnie kliknij przycisk **zadania**. 

    ![Zadania widoku węzła](./media/hdinsight-apache-spark-intellij-tool-plugin/job-view-node.png)

2. Polecenie hello **zadania** węzła. Narzędzia HDInsight Hello automatycznie — wykrywa, czy zainstalowano dodatek clipse E (fx) hello. Kliknij przycisk **OK** toocontinue i wykonaj instrukcje hello tooinstall hello Eclipse Marketplace i ponownego uruchomienia aplikacji Eclipse.

    ![Zainstaluj clipse E (fx)](./media/hdinsight-apache-spark-eclipse-tool-plugin/auto-install-efxclipse.png)

3. Otwórz hello widoku zadania z hello **zadania** węzła. W okienku po prawej stronie powitania, hello **widoku zadania Spark** karcie są wyświetlane wszystkie aplikacje hello, które zostały uruchomione w klastrze hello. Kliknij nazwę hello aplikacji hello, dla której ma zostać toosee więcej szczegółów.

    ![Szczegóły aplikacji](./media/hdinsight-apache-spark-intellij-tool-plugin/view-job-logs.png)
4. Po umieszczeniu wskaźnika myszy na wykresie zadania hello Wyświetla podstawowych informacji o uruchomionych zadań. Kliknięcie wykresu zadań hello przedstawia wykres etapy hello i informacje, które generuje każde zadanie.

    ![Szczegóły etap zadania](./media/hdinsight-apache-spark-intellij-tool-plugin/Job-graph-stage-info.png)

5. Często używanych dzienników, w tym Stderr sterownika, Stdout sterowników i informacje katalogu są wymienione w hello **dziennika** kartę.

    ![Szczegóły dziennika](./media/hdinsight-apache-spark-intellij-tool-plugin/Job-log-info.png)
6. Hello historii Spark interfejsu użytkownika i hello interfejsie użytkownika YARN (na poziomie aplikacji hello) można także otworzyć, klikając hello hyperlink odpowiednich u góry hello hello okna.

### <a name="access-hello-storage-container-for-hello-cluster"></a>Dostęp do kontenera magazynu hello hello klastra
1. W Eksploratorze Azure rozwiń hello **HDInsight** toosee węzła głównego listę klastry HDInsight Spark, które są dostępne.
2. Rozwiń węzeł konta magazynu hello toosee hello nazwy klastra i hello domyślnego kontenera magazynu dla klastra hello.
   
    ![Magazyn konta i domyślnego kontenera magazynu](./media/hdinsight-apache-spark-eclipse-tool-plugin/view-explorer-5.png)
3. Kliknij nazwę kontenera magazynu hello skojarzony z klastrem hello. W okienku po prawej stronie powitania, kliknij dwukrotnie hello **HVACOut** folderu. Otwórz jeden hello **części -** pliki toosee hello dane wyjściowe aplikacji hello.

### <a name="access-hello-spark-history-server"></a>Dostęp do serwera historii Spark hello
1. W Eksploratorze Azure, kliknij prawym przyciskiem myszy nazwę klastra Spark, a następnie wybierz **Otwórz użytkownika usługi Historia Spark**. Po wyświetleniu monitu wprowadź poświadczenia administratora hello hello klastra. Należy wcześniej określić te podczas inicjowania obsługi administracyjnej hello klastra.
2. W hello Spark historii serwera pulpitu nawigacyjnego toolook Nazwa aplikacji hello jest używany dla aplikacji hello właśnie zakończono uruchomiona. W hello poprzedzających kodu, należy określić nazwę aplikacji hello przy użyciu `val conf = new SparkConf().setAppName("MyClusterApp")`. W związku z tym nazwa aplikacji Spark został **MyClusterApp**.

### <a name="start-hello-ambari-portal"></a>Uruchom hello Ambari portalu
1. W Eksploratorze Azure, kliknij prawym przyciskiem myszy nazwę klastra Spark, a następnie wybierz **Otwórz Portal zarządzania klastra (Ambari)**. 
2. Po wyświetleniu monitu wprowadź poświadczenia administratora hello hello klastra. Należy wcześniej określić te podczas inicjowania obsługi administracyjnej hello klastra.

### <a name="manage-azure-subscriptions"></a>Zarządzać subskrypcjami platformy Azure
Domyślnie narzędzia HDInsight w zestawie narzędzi Azure dla programu Eclipse Wyświetla klastry Spark hello wszystkie subskrypcje platformy Azure. Jeśli to konieczne, można określić hello subskrypcji, dla których chcesz tooaccess hello klastra. 

1. W Eksploratorze Azure, kliknij prawym przyciskiem myszy hello **Azure** węzła głównego, a następnie kliknij przycisk **Zarządzaj subskrypcjami**. 
2. Okno dialogowe hello, wyczyść pola wyboru hello hello subskrypcji, że nie ma tooaccess, a następnie kliknij przycisk **Zamknij**. Możesz również kliknąć **Wyloguj** Jeśli chcesz toosign poza subskrypcją platformy Azure.

## <a name="run-a-spark-scala-application-locally"></a>Uruchamianie aplikacji Spark Scala lokalnie
Używając narzędzia HDInsight Tools w zestawie narzędzi Azure dla aplikacji Spark Scala toorun Eclipse lokalnie na stacji roboczej. Zazwyczaj te aplikacje nie wymagają dostępu toocluster zasoby, takie jak kontenera magazynu, a program można uruchomić i przetestować je lokalnie.

### <a name="prerequisite"></a>Wymagania wstępne
Gdy używasz lokalnych aplikacji Spark Scala hello na komputerze z systemem Windows, można uzyskać wyjątku zgodnie z objaśnieniem w [SPARK 2356](https://issues.apache.org/jira/browse/SPARK-2356). Ten wyjątek spowodowany **WinUtils.exe** nie ma w systemie Windows. 

tooresolve tego błędu, należy najpierw [Pobierz hello wykonywalnego](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) tooa lokalizacji, takich jak **C:\WinUtils\bin**. Następnie należy dodać zmienną środowiskową hello **HADOOP_HOME** i ustaw wartość hello zmiennej hello zbyt**C\WinUtils**.

### <a name="run-a-local-spark-scala-application"></a>Uruchamianie aplikacji Spark Scala lokalnej
1. Uruchom środowisko Eclipse i tworzenia projektu. W hello **nowy projekt** okno dialogowe upewnij hello następujące opcje, a następnie kliknij przycisk **dalej**.
   
   * Wybierz w okienku po lewej stronie powitania **HDInsight**.
   * W okienku po prawej stronie powitania, wybierz **Spark dla usługi HDInsight lokalnego uruchamiania próbki (Scala)**.

    ![Okno dialogowe Nowy projekt](./media/hdinsight-apache-spark-eclipse-tool-plugin/hdi-spark-app-local-run.png)
2. Szczegóły projektu hello tooprovide, wykonaj kroki od 3 do 6 z hello wcześniejszej sekcji [Konfigurowanie projektu dla klastra Spark w usłudze HDInsight Spark Scala](#set-up-a-spark-scala-project-for-an-hdinsight-spark cluster).
3. Przykładowy kod dodaje Hello szablonu (**LogQuery**) w obszarze hello **src** folderu, który można uruchomić lokalnie na komputerze.
   
    ![Lokalizacja LogQuery](./media/hdinsight-apache-spark-eclipse-tool-plugin/local-app.png)
4. Powitania kliknij prawym przyciskiem myszy **LogQuery** aplikacji, punkt zbyt**Uruchom jako**, a następnie kliknij przycisk **1 aplikacja Scala**. Zostaną wyświetlone informacje takie w hello **konsoli** u dołu hello:
   
   ![Aplikacji Spark lokalnego wynik uruchomienia](./media/hdinsight-apache-spark-eclipse-tool-plugin/hdi-spark-app-local-run-result.png)

## <a name="faq"></a>Często zadawane pytania
Wybierz toosubmit aplikacji tooAzure Data Lake Store, **Interactive** tryb podczas procesu hello Azure logowania. W przypadku wybrania **automatycznego** tryb, możesz uzyskać wystąpił błąd.

![interakcyjny rejestrowanie](./media/hdinsight-apache-spark-eclipse-tool-plugin/interactive-authentication.png)

Teraz możemy go rozwiązał. Możesz wybrać toosubmit Azure Data Lake klastra aplikacji przy użyciu dowolnej metody logowania.

## <a name="feedback-and-known-issues"></a>Opinie i znane problemy
Przeglądanie wyjść Spark bezpośrednio nie jest obecnie obsługiwana.

Jeśli masz jakiekolwiek sugestie lub opinii lub napotykasz problemy podczas korzystania z tego narzędzia, możesz wolnego toosend nas wiadomość e-mail na hdivstool@microsoft.com.

## <a name="seealso"></a>Zobacz też
* [Przegląd: platforma Apache Spark w usłudze Azure HDInsight](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a>Scenariusze
* [Platforma Spark i analiza biznesowa: interakcyjna analiza danych na platformie Spark w usłudze HDInsight z użyciem narzędzi do analizy biznesowej](hdinsight-apache-spark-use-bi-tools.md)
* [Platforma Spark i usługa Machine Learning: korzystanie z platformy Spark w usłudze HDInsight do analizy temperatury w budynku z użyciem danych HVAC](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Platforma Spark przy użyciu Machine Learning: Korzystanie z platformy Spark w wyników inspekcji żywności toopredict HDInsight](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Przesyłanie strumieniowe Spark: korzystanie z platformy Spark w usłudze HDInsight do tworzenia aplikacji do przesyłania strumieniowego w czasie rzeczywistym](hdinsight-apache-spark-eventhub-streaming.md)
* [Analiza dzienników witryny sieci Web na platformie Spark w usłudze HDInsight](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="creating-and-running-applications"></a>Tworzenie i uruchamianie aplikacji
* [Tworzenie autonomicznych aplikacji przy użyciu języka Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Zdalne uruchamianie zadań w klastrze Spark przy użyciu programu Livy](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a>Narzędzia i rozszerzenia
* [Zestaw narzędzi platformy Azure na użytek IntelliJ toocreate i przesyłanie aplikacji Spark Scala](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Użyj narzędzi Azure dla aplikacji Spark toodebug IntelliJ zdalnie za pośrednictwem sieci VPN](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Użyj narzędzi Azure dla aplikacji Spark toodebug IntelliJ zdalnie za pośrednictwem SSH](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md)
* [Użyj narzędzia HDInsight Tools for IntelliJ z Hortonworks piaskownicy](hdinsight-tools-for-intellij-with-hortonworks-sandbox.md)
* [Korzystanie z notesów Zeppelin w klastrze Spark w usłudze HDInsight](hdinsight-apache-spark-zeppelin-notebook.md)
* [Jądra dostępne dla notesu Jupyter w klastrze Spark w usłudze HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Korzystanie z zewnętrznych pakietów z notesami Jupyter](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Instalacja oprogramowania Jupyter na komputerze i połącz tooan klastra Spark w usłudze HDInsight](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="managing-resources"></a>Zarządzanie zasobami
* [Zarządzanie zasobami hello klastra Apache Spark w usłudze Azure HDInsight](hdinsight-apache-spark-resource-manager.md)
* [Śledzenie i debugowanie zadań uruchamianych w klastrze Apache Spark w usłudze HDInsight](hdinsight-apache-spark-job-debugging.md)

