---
title: "klaster notesów Zeppelin aaaUse z platformy Apache Spark w usłudze Azure HDInsight | Dokumentacja firmy Microsoft"
description: "Instrukcje krok po kroku, w jaki klastrów notesów Zeppelin toouse z platformy Apache Spark w usłudze Azure HDInsight."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: df489d70-7788-4efa-a089-e5e5006421e2
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 3ab479cfccc7fd38a9bf6a9fb4f5928beec8ff7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-zeppelin-notebooks-with-apache-spark-cluster-on-azure-hdinsight"></a>Korzystanie z notesów Zeppelin z klastra Apache Spark w usłudze Azure HDInsight

Klastry HDInsight Spark obejmują notesów Zeppelin służy toorun zadań Spark. W tym artykule dowiesz się, jak toouse hello notesu Zeppelin w klastrze usługi HDInsight.

> [!NOTE]
> Notesów Zeppelin są dostępne tylko w przypadku 1.6.3 platformy Spark w usłudze HDInsight 3.5 i Spark 2.1.0 na 3,6 HDInsight.
>

**Wymagania wstępne:**

* Subskrypcja platformy Azure. Zobacz temat [Uzyskiwanie bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* Klaster Apache Spark w usłudze HDInsight. Aby uzyskać instrukcje, zobacz [klastrów utworzyć Apache Spark w usłudze Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).

## <a name="launch-a-zeppelin-notebook"></a>Uruchamianie notesu Zeppelin
1. W bloku klastra Spark hello, kliknij **pulpit nawigacyjny klastra**, a następnie kliknij przycisk **notesu Zeppelin**. Jeśli zostanie wyświetlony monit, wprowadź poświadczenia administratora hello hello klastra.
   
   > [!NOTE]
   > Można również przejść hello Zeppelin Notebook dla klastra przez hello otwarcia następującego adresu URL w przeglądarce. Zastąp **CLUSTERNAME** o nazwie hello klastra:
   > 
   > `https://CLUSTERNAME.azurehdinsight.net/zeppelin`
   > 
   > 
2. Utwórz nowy notes. Okienko nagłówka hello, kliknij **notesu**, a następnie kliknij przycisk **Tworzenie nowej notatki**.
   
    ![Tworzenie nowego notesu Zeppelin](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-create-zeppelin-notebook.png "Tworzenie nowego notesu Zeppelin")
   
    Wprowadź nazwę notesu hello, a następnie kliknij przycisk **utworzyć Uwaga**.
3. Ponadto upewnij się, że nagłówek notesu hello wyświetlany jest stan połączenia. Jest oznaczany zielonym kropką w hello prawym górnym rogu.
   
    ![Stan notesu Zeppelin](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-connected.png "Zeppelin notesu stanu")
4. Załaduj przykładowe dane do tabeli tymczasowej. Podczas tworzenia klastra Spark w usłudze HDInsight, hello przykładowy plik danych **hvac.csv**, jest skopiowany toohello skojarzone konto magazynu w obszarze **\HdiSamples\SensorSampleData\hvac**.
   
    W hello akapitu pusty jest domyślnie tworzona w hello nowy notes Wklej hello następującego fragmentu.
   
        %livy.spark
        //hello above magic instructs Zeppelin toouse hello Livy Scala interpreter
   
        // Create an RDD using hello default Spark context, sc
        val hvacText = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")
   
        // Define a schema
        case class Hvac(date: String, time: String, targettemp: Integer, actualtemp: Integer, buildingID: String)
   
        // Map hello values in hello .csv file toohello schema
        val hvac = hvacText.map(s => s.split(",")).filter(s => s(0) != "Date").map(
            s => Hvac(s(0), 
                    s(1),
                    s(2).toInt,
                    s(3).toInt,
                    s(6)
            )
        ).toDF()
   
        // Register as a temporary table called "hvac"
        hvac.registerTempTable("hvac")
   
    Naciśnij klawisz **SHIFT + ENTER** lub kliknij przycisk hello **odtwarzanie** przycisk dla hello akapitu toorun hello fragmentu. Stan Hello na powitania prawym dolnym rogu akapitu hello powinien postępu z GOTOWY do czasu tooFINISHED uruchomiona. dane wyjściowe Hello zostaną wyświetlone u dołu hello hello tym samym obiekcie paragraph. Zrzut ekranu Hello wygląda hello:
   
    ![Tworzenie tabeli tymczasowej od danych pierwotnych](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-load-data.png "Tworzenie tabeli tymczasowej od danych pierwotnych")
   
    Można też podać akapitu tooeach tytułu. W prawym górnym rogu powitania kliknij hello **ustawienia** ikonę, a następnie kliknij przycisk **Pokaż tytuł**.
5. Teraz możesz uruchomić instrukcje Spark SQL na powitania **hvac** tabeli. Wklej hello następujące zapytanie w nowy akapit. Witaj zapytanie pobiera identyfikator budynku hello i hello różnicy między hello docelowych i rzeczywistego temperatury dla każdego opierając się na dany dzień. Naciśnij klawisz **SHIFT + ENTER**.
   
        %sql
        select buildingID, (targettemp - actualtemp) as temp_diff, date from hvac where date = "6/1/13" 
   
    Witaj **% sql** instrukcji na początku hello informuje hello notesu toouse hello Livy Scala interpreter.
   
    Witaj Poniższy zrzut ekranu przedstawia hello dane wyjściowe.
   
    ![Uruchom instrukcję Spark SQL za pomocą notesu hello](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-spark-query-1.png "zestawienia Spark SQL za pomocą notesu hello")
   
     Kliknij przycisk hello wyświetlania opcje (wyróżniane na prostokąt) tooswitch między różne reprezentacje dla hello samych danych wyjściowych. Kliknij przycisk **ustawienia** toochoose jakie consitutes hello klucza i wartości w danych wyjściowych hello. Witaj Przechwytywanie ekranu powyżej używa **buildingID** jako klucz hello i średnią hello **temp_diff** jako wartość hello.
6. Można również uruchomić używania zmiennych w zapytaniu hello instrukcje Spark SQL. Witaj dalej fragment kodu przedstawia sposób toodefine zmiennej, **Temp**, w zapytaniu hello z hello możliwe wartości ma tooquery z. Przy pierwszym uruchomieniu zapytania hello, menu rozwijane jest automatycznie wypełniana określone dla zmiennej hello hello wartości.
   
        %sql
        select buildingID, date, targettemp, (targettemp - actualtemp) as temp_diff from hvac where targettemp > "${Temp = 65,65|75|85}" 
   
    Wklej następujący fragment kodu w nowy akapit i naciśnij klawisz **SHIFT + ENTER**. Witaj Poniższy zrzut ekranu przedstawia hello dane wyjściowe.
   
    ![Uruchom instrukcję Spark SQL za pomocą notesu hello](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-spark-query-2.png "zestawienia Spark SQL za pomocą notesu hello")
   
    Następnych kwerend można wybrać nową wartość z listy rozwijanej hello i ponownie uruchom zapytanie hello. Kliknij przycisk **ustawienia** toochoose jakie consitutes hello klucza i wartości w danych wyjściowych hello. Witaj Przechwytywanie ekranu powyżej używa **buildingID** jako klucz hello hello średnią **temp_diff** jako wartość hello i **targettemp** jako hello grupy.
7. Uruchom ponownie hello Livy interpreter tooexit hello aplikacji. toodo, Otwórz ustawienia interpreter klikając hello zalogowany nazwy użytkownika z hello prawym górnym rogu, a następnie kliknij przycisk **Interpreter**.
   
    ![Uruchamianie interpreter](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive danych wyjściowych")
8. Przewiń tooLivy interpreter ustawienia, a następnie kliknij przycisk **ponownego uruchomienia**.
   
    ![Uruchom ponownie hello Livy intepreter](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-restart-interpreter.png "ponowne uruchomienie hello Zeppelin intepreter")

## <a name="how-do-i-use-external-packages-with-hello-notebook"></a>Jak korzystanie z zewnętrznych pakietów z notesem hello?
W klastrze Apache Spark na HDInsight (Linux) toouse zewnętrznych, przyczyniły się społeczności pakiety, które nie są uwzględniane out-of box hello klastra można skonfigurować hello Zeppelin notesu. Możesz przeszukać hello [repozytorium Maven](http://search.maven.org/) dla hello pełną listę pakietów, które są dostępne. Można również uzyskać listę dostępnych pakietów z innych źródeł. Na przykład pełną listę społeczności przyczyniły się do pakietów znajduje się w temacie [pakietów Spark](http://spark-packages.org/).

W tym artykule, zobaczysz jak toouse hello [udostępnionego woluminu klastra spark](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) pakietu z hello notesu Jupyter.

1. Otwórz ustawienia interpreter. Z hello prawym górnym rogu, kliknij hello rejestrowane w nazwie użytkownika, a następnie kliknij **Interpreter**.
   
    ![Uruchamianie interpreter](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive danych wyjściowych")
2. Przewiń tooLivy interpreter ustawienia, a następnie kliknij przycisk **Edytuj**.
   
    ![Zmień ustawienia interpreter](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-use-external-package-1.png "zmiany ustawień interpretera")
3. Dodaj nowy klucz o nazwie **livy.spark.jars.packages** i ustaw jej wartość w formacie hello `group:id:version`. Tak, jeśli chcesz toouse hello [udostępnionego woluminu klastra spark](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) pakietu, należy ustawić wartość hello klucza hello zbyt`com.databricks:spark-csv_2.10:1.4.0`.
   
    ![Zmień ustawienia interpreter](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-use-external-package-2.png "zmiany ustawień interpretera")
   
    Kliknij przycisk **zapisać** i uruchom ponownie hello Livy interpreter.
4. **Porada**: Jeśli chcesz toounderstand wprowadzania tooarrive na powitania wartość klucza hello powyżej, w tym sposób.
   
    a. Zlokalizuj pakiet hello w hello repozytorium Maven. W tym samouczku użyliśmy [udostępnionego woluminu klastra spark](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar).
   
    b. Z repozytorium hello Zbierz wartości hello **GroupId**, **ArtifactId**, i **wersji**.
   
    ![Pakiety zewnętrzne za pomocą notesu Jupyter](./media/hdinsight-apache-spark-zeppelin-notebook/use-external-packages-with-jupyter.png "pakiety zewnętrzne za pomocą notesu Jupyter")
   
    c. Łączenie hello trzech wartości oddzielonych dwukropkiem (**:**).
   
        com.databricks:spark-csv_2.10:1.4.0

## <a name="where-are-hello-zeppelin-notebooks-saved"></a>Gdzie są hello notesów Zeppelin zapisać?
notesów Zeppelin Hello są zapisywane toohello headnodes klastra. Dlatego po usunięciu klastra hello notesów hello zostaną również usunięte. Jeśli chcesz toopreserve notesy do późniejszego użytku w innych klastrach, należy wyeksportować je po zakończeniu działania zadań hello. tooexport notesu, kliknij przycisk hello **wyeksportować** ikony, jak pokazano w poniższym obrazie hello.

![Pobierz notesu](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-download-notebook.png "notesu hello pobierania")

To notesu hello jest zapisywany w formacie JSON w lokalizacji pobierania.

## <a name="livy-session-management"></a>Zarządzanie sesjami programu Livy
Po uruchomieniu hello pierwszym akapicie kodu w notesie Zeppelin w nowej sesji programu Livy jest tworzony w klastrze Spark w usłudze HDInsight. Ta sesja jest współużytkowana przez wszystkie notesów Zeppelin, które następnie utworzysz. Jeśli dla niektórych hello Przyczyna Livy sesja jest skasowane (ponowne uruchomienie klastra, itp.), nie będą mogli toorun zadań hello Zeppelin notesu.

W takim przypadku należy wykonać następujące kroki, przed rozpoczęciem uruchomionych zadań z notesu Zeppelin hello. 

1. Uruchom ponownie hello interpreter Livy z hello Zeppelin notesu. toodo, Otwórz ustawienia interpreter klikając hello zalogowany nazwy użytkownika z hello prawym górnym rogu, a następnie kliknij przycisk **Interpreter**.
   
    ![Uruchamianie interpreter](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive danych wyjściowych")
2. Przewiń tooLivy interpreter ustawienia, a następnie kliknij przycisk **ponownego uruchomienia**.
   
    ![Uruchom ponownie hello Livy intepreter](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-restart-interpreter.png "ponowne uruchomienie hello Zeppelin intepreter")
3. Uruchom komórki kodu z istniejącego notesu Zeppelin. Spowoduje to utworzenie nowej sesji programu Livy hello klastra usługi HDInsight.

## <a name="seealso"></a>Zobacz też
* [Przegląd: platforma Apache Spark w usłudze Azure HDInsight](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a>Scenariusze
* [Platforma Spark i analiza biznesowa: interakcyjna analiza danych na platformie Spark w usłudze HDInsight z użyciem narzędzi do analizy biznesowej](hdinsight-apache-spark-use-bi-tools.md)
* [Platforma Spark i usługa Machine Learning: korzystanie z platformy Spark w usłudze HDInsight do analizy temperatury w budynku z użyciem danych HVAC](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Platforma Spark przy użyciu Machine Learning: Korzystanie z platformy Spark w wyników inspekcji żywności toopredict HDInsight](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Przesyłanie strumieniowe Spark: korzystanie z platformy Spark w usłudze HDInsight do tworzenia aplikacji do przesyłania strumieniowego w czasie rzeczywistym](hdinsight-apache-spark-eventhub-streaming.md)
* [Analiza dzienników witryny sieci Web na platformie Spark w usłudze HDInsight](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a>Tworzenie i uruchamianie aplikacji
* [Tworzenie autonomicznych aplikacji przy użyciu języka Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Zdalne uruchamianie zadań w klastrze Spark przy użyciu programu Livy](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a>Narzędzia i rozszerzenia
* [Użyj dodatku HDInsight Tools Plugin dla toocreate IntelliJ IDEA i przesyłanie aplikacji Spark Scala](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Użyj dodatku HDInsight Tools Plugin zdalnie dla aplikacji Spark toodebug IntelliJ IDEA](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Jądra dostępne dla notesu Jupyter w klastrze Spark w usłudze HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Korzystanie z zewnętrznych pakietów z notesami Jupyter](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Instalacja oprogramowania Jupyter na komputerze i połącz tooan klastra Spark w usłudze HDInsight](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>Zarządzanie zasobami
* [Zarządzanie zasobami hello klastra Apache Spark w usłudze Azure HDInsight](hdinsight-apache-spark-resource-manager.md)
* [Śledzenie i debugowanie zadań uruchamianych w klastrze Apache Spark w usłudze HDInsight](hdinsight-apache-spark-job-debugging.md)

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md 







