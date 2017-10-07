---
title: "niestandardowe pakiety Maven aaaUse z Jupyter w łączniku Spark on Azure HDInsight | Dokumentacja firmy Microsoft"
description: "Instrukcje krok po kroku na jak notesów Jupyter tooconfigure dostępne z Spark w usłudze HDInsight clusters toouse niestandardowe pakiety Maven."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 2a8bc545-064e-436f-8b5f-e67c26cfbf98
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: ba8ac13716bc94ab082a18fe02d4a40b2f1e09e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-external-packages-with-jupyter-notebooks-in-apache-spark-clusters-on-hdinsight"></a>Korzystanie z zewnętrznych pakietów z notesami Jupyter w klastrach Apache Spark w usłudze HDInsight
> [!div class="op_single_selector"]
> * [Przy użyciu magic komórki](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
> * [Za pomocą akcji skryptu](hdinsight-apache-spark-python-package-installation.md)
>
>

Dowiedz się, jak tooconfigure notesu Jupyter w klastrze Apache Spark w HDInsight toouse zewnętrzne społeczności-przyczyniły się **maven** pakiety, które nie są objęte poza pole hello klastra. 

Możesz przeszukać hello [repozytorium Maven](http://search.maven.org/) dla hello pełną listę pakietów, które są dostępne. Można również uzyskać listę dostępnych pakietów z innych źródeł. Na przykład pełną listę społeczności przyczyniły się do pakietów znajduje się w temacie [pakietów Spark](http://spark-packages.org/).

W tym artykule przedstawiono sposób toouse hello [udostępnionego woluminu klastra spark](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) pakietu z hello notesu Jupyter.



## <a name="prerequisites"></a>Wymagania wstępne
Musi mieć następujące hello:

* Klaster Apache Spark w usłudze HDInsight. Aby uzyskać instrukcje, zobacz [klastrów utworzyć Apache Spark w usłudze Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).

## <a name="use-external-packages-with-jupyter-notebooks"></a>Korzystanie z zewnętrznych pakietów z notesami Jupyter
1. Z hello [Azure Portal](https://portal.azure.com/), hello tablicy startowej, kliknij Kafelek hello klastra Spark (jeśli został przypięty toohello tablicy startowej). Można także przechodzić tooyour klastra w obszarze **Przeglądaj wszystko** > **klastrów usługi HDInsight**.   
2. W bloku klastra Spark hello, kliknij **szybkie linki**, a następnie z hello **pulpit nawigacyjny klastra** bloku, kliknij przycisk **notesu Jupyter**. Jeśli zostanie wyświetlony monit, wprowadź poświadczenia administratora hello hello klastra.

    > [!NOTE]
    > Można również przejść hello Jupyter Notebook dla klastra przez hello otwarcia następującego adresu URL w przeglądarce. Zastąp **CLUSTERNAME** o nazwie hello klastra:
    > 
    > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
    > 

   

3. Utwórz nowy notes. Kliknij przycisk **nowy**, a następnie kliknij przycisk **Spark**.
   
    ![Tworzenie nowego notesu Jupyter](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/hdinsight-spark-create-notebook.png "Tworzenie nowego notesu Jupyter")

4. Nowy notes jest utworzony i otwarty z hello nazwie Untitled.pynb. Kliknij nazwę notesu hello u góry hello, a następnie wprowadź przyjazną nazwę.
   
    ![Podaj nazwę notesu hello](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/hdinsight-spark-name-notebook.png "Podaj nazwę notesu hello")

5. Użyje hello `%%configure` magic tooconfigure hello notesu toouse pakietów zewnętrznych. W notesach, które używają pakiety zewnętrzne, upewnij się, należy wywołać hello `%%configure` magic w hello pierwszej komórki kodu. Dzięki temu, że jądra hello jest skonfigurowany toouse hello pakietu przed rozpoczęciem powitalne sesji.

    >[!IMPORTANT] 
    >Jeśli zapomnisz tooconfigure hello jądra w pierwszej komórki hello, możesz użyć hello `%%configure` z hello `-f` parametru, ale zostanie uruchomiona ponownie hello sesji i postępu wszystkich zostaną utracone.

    | Wersja usługi HDInsight | Polecenie |
    |-------------------|---------|
    |HDInsight 3.3 i HDInsight 3.4 | `%%configure` <br>`{ "packages":["com.databricks:spark-csv_2.10:1.4.0"] }`|
    | Dla usługi HDInsight 3.5 | `%%configure`<br>`{ "conf": {"spark.jars.packages": "com.databricks:spark-csv_2.10:1.4.0" }}`|

6. fragment Hello powyżej oczekuje współrzędne maven hello hello pakietów zewnętrznych w centralnym repozytorium Maven. W tym fragmencie `com.databricks:spark-csv_2.10:1.4.0` jest hello maven Współrzędna dla **udostępnionego woluminu klastra spark** pakietu. Oto konstrukcji hello współrzędnych dla pakietu.
   
    a. Zlokalizuj pakiet hello w hello repozytorium Maven. W tym samouczku używamy [udostępnionego woluminu klastra spark](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar).
   
    b. Z repozytorium hello Zbierz wartości hello **GroupId**, **ArtifactId**, i **wersji**. Upewnij się, że hello wartości, które należy zebrać są zgodne z klastrem. W tym przypadku użyto Scala 2.10 i Spark 1.4.0 pakietu, ale mogą być potrzebne różne wersje tooselect hello odpowiednią wersję języka Scala lub Spark w klastrze. Można sprawdzić wersji języka Scala hello w klastrze, uruchamiając `scala.util.Properties.versionString` na powitania Spark Jupyter jądra lub Prześlij Spark. Można sprawdzić wersji Spark hello w klastrze, uruchamiając `sc.version` na notesów Jupyter.
   
    ![Pakiety zewnętrzne za pomocą notesu Jupyter](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/use-external-packages-with-jupyter.png "pakiety zewnętrzne za pomocą notesu Jupyter")
   
    c. Łączenie hello trzech wartości oddzielonych dwukropkiem (**:**).
   
        com.databricks:spark-csv_2.10:1.4.0

7. Uruchom hello komórki kodu z hello `%%configure` magic. Spowoduje to skonfigurowanie hello podstawowej Livy sesji toouse hello pakietu podane. W kolejnych komórek hello w notesie hello można teraz używać pakietu hello, jak pokazano poniżej.
   
        val df = sqlContext.read.format("com.databricks.spark.csv").
        option("header", "true").
        option("inferSchema", "true").
        load("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

8. Następnie możesz uruchomić wstawki hello, jak pokazano poniżej, tooview hello danych z hello dataframe utworzony w poprzednim kroku hello.
   
        df.show()
   
        df.select("Time").count()

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

* [Użyj python zewnętrznych pakietów z notesami Jupyter w klastrach Apache Spark w usłudze HDInsight w systemie Linux](hdinsight-apache-spark-python-package-installation.md)
* [Użyj dodatku HDInsight Tools Plugin dla toocreate IntelliJ IDEA i przesyłanie aplikacji Spark Scala](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Użyj dodatku HDInsight Tools Plugin zdalnie dla aplikacji Spark toodebug IntelliJ IDEA](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Korzystanie z notesów Zeppelin w klastrze Spark w usłudze HDInsight](hdinsight-apache-spark-zeppelin-notebook.md)
* [Jądra dostępne dla notesu Jupyter w klastrze Spark w usłudze HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Instalacja oprogramowania Jupyter na komputerze i połącz tooan klastra Spark w usłudze HDInsight](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>Zarządzanie zasobami
* [Zarządzanie zasobami hello klastra Apache Spark w usłudze Azure HDInsight](hdinsight-apache-spark-resource-manager.md)
* [Śledzenie i debugowanie zadań uruchamianych w klastrze Apache Spark w usłudze HDInsight](hdinsight-apache-spark-job-debugging.md)

