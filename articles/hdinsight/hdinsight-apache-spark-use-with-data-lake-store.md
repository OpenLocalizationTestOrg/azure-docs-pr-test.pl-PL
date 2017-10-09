---
title: "aaaUse danych tooanalyze Apache Spark w usłudze Azure Data Lake Store | Dokumentacja firmy Microsoft"
description: "Uruchamianie zadań Spark tooanalyze danych przechowywanych w usłudze Azure Data Lake Store"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 1f174323-c17b-428c-903d-04f0e272784c
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 3b7f628f7a8114d2ca6f3f9219ce107905f1c818
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hdinsight-spark-cluster-tooanalyze-data-in-data-lake-store"></a>Użyj danych tooanalyze klastra Spark w usłudze HDInsight w usłudze Data Lake Store

W tym samouczku użyjesz notesu Jupyter dostępne z toorun klastry HDInsight Spark zadanie, które odczytuje dane z konta usługi Data Lake Store.

## <a name="prerequisites"></a>Wymagania wstępne

* Konto usługi Azure Data Lake Store. Postępuj zgodnie z instrukcjami hello w [wprowadzenie do usługi Azure Data Lake Store za pomocą portalu Azure hello](../data-lake-store/data-lake-store-get-started-portal.md).

* Azure klastra Spark w usłudze HDInsight z usługą Data Lake Store jako magazyn. Postępuj zgodnie z instrukcjami hello w [tworzenia klastra usługi HDInsight z Data Lake Store przy użyciu portalu Azure](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).

    
## <a name="prepare-hello-data"></a>Przygotowanie danych hello

> [!NOTE]
> Nie trzeba tooperform ten krok po utworzeniu klastra usługi HDInsight hello z usługi Data Lake Store jako domyślnego magazynu. procesy tworzenia klastra Hello dodaje konto usługi Data Lake Store hello określone podczas tworzenia klastra hello przykładowych danych. Pomiń sekcję toohello [klastra Spark w usłudze HDInsight użycia z usługą Data Lake Store](#use-an-hdinsight-spark-cluster-with-data-lake-store).
>
>

Jeśli utworzono klaster usługi HDInsight z usługą Data Lake Store jako dodatkowego miejsca do magazynowania i obiektu Blob magazynu Azure jako domyślny magazyn, należy najpierw skopiować przez niektóre przykładowe dane toohello konta usługi Data Lake Store. Można użyć hello przykładowych danych z obiektu Blob magazynu Azure skojarzony z klastrem usługi HDInsight hello powitalne. Można użyć hello [narzędzie ADLCopy](http://aka.ms/downloadadlcopy) toodo tak. Pobierz i zainstaluj narzędzie hello z hello łącza.

1. Otwórz wiersz polecenia i przejdź do katalogu toohello AdlCopy zainstalowanym, zwykle `%HOMEPATH%\Documents\adlcopy`.

2. Uruchom następujące polecenie toocopy hello konkretnego obiektu blob hello źródła kontenera tooa usługi Data Lake Store:

        AdlCopy /source https://<source_account>.blob.core.windows.net/<source_container>/<blob name> /dest swebhdfs://<dest_adls_account>.azuredatalakestore.net/<dest_folder>/ /sourcekey <storage_account_key_for_storage_container>

    Kopiuj hello **HVAC.csv** o plików przykładowych danych **/HdiSamples/HdiSamples/SensorSampleData/hvac/** toohello konta usługi Azure Data Lake Store. fragment kodu Hello powinna wyglądać:

        AdlCopy /Source https://mydatastore.blob.core.windows.net/mysparkcluster/HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv /dest swebhdfs://mydatalakestore.azuredatalakestore.net/hvac/ /sourcekey uJUfvD6cEvhfLoBae2yyQf8t9/BpbWZ4XoYj4kAS5Jf40pZaMNf0q6a8yqTxktwVgRED4vPHeh/50iS9atS5LQ==

   > [!WARNING]
   > Upewnij się, hello pliku i nazwy ścieżki są w przypadku prawidłowego hello.
   >
   >
3. Można tooenter zostanie wyświetlony monit o poświadczenia hello hello subskrypcji platformy Azure, w którym masz konto usługi Data Lake Store. Zostaną wyświetlone następujące dane wyjściowe podobne toohello:

        Initializing Copy.
        Copy Started.
        100% data copied.
        Copy Completed. 1 file copied.

    plik danych Hello (**HVAC.csv**) zostaną skopiowane w folderze **/hvac** w hello konta usługi Data Lake Store.

## <a name="use-an-hdinsight-spark-cluster-with-data-lake-store"></a>Używanie klastra Spark w usłudze HDInsight z usługą Data Lake Store

1. Z hello [Azure Portal](https://portal.azure.com/), hello tablicy startowej, kliknij Kafelek hello klastra Spark (jeśli został przypięty toohello tablicy startowej). Można także przechodzić tooyour klastra w obszarze **Przeglądaj wszystko** > **klastrów usługi HDInsight**.

2. W bloku klastra Spark hello, kliknij **szybkie linki**, a następnie z hello **pulpit nawigacyjny klastra** bloku, kliknij przycisk **notesu Jupyter**. Jeśli zostanie wyświetlony monit, wprowadź poświadczenia administratora hello hello klastra.

   > [!NOTE]
   > Można również przejść hello Jupyter Notebook dla klastra przez hello otwarcia następującego adresu URL w przeglądarce. Zastąp **CLUSTERNAME** o nazwie hello klastra:
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >

3. Utwórz nowy notes. Kliknij opcję **New** (Nowy), a następnie kliknij pozycję **PySpark**.

    ![Tworzenie nowego notesu Jupyter](./media/hdinsight-apache-spark-use-with-data-lake-store/hdinsight-create-jupyter-notebook.png "Tworzenie nowego notesu Jupyter")

4. Ponieważ Notes jądro PySpark hello został utworzony, nie trzeba toocreate kontekstów jawnie. konteksty Spark i Hive Hello zostanie automatycznie utworzone automatycznie po uruchomieniu pierwszej komórki kodu hello. Możesz zacząć od importowania typów hello wymaganych dla tego scenariusza. toodo tak, Wklej hello następującego fragmentu kodu w komórce i naciśnij klawisz **SHIFT + ENTER**.

        from pyspark.sql.types import *

    Za każdym razem, gdy zostanie uruchomione zadanie w oprogramowaniu Jupyter tytuł okna przeglądarki sieci web zostaną wyświetlone **(zajęty)** stan wraz z tytułem notesu hello. Widoczne będzie także pełne kółko toohello dalej **PySpark** tekst w hello prawym górnym rogu. Po zakończeniu zadania hello zmieni to tooa okrąg.

     ![Stan zadania notesu Jupyter](./media/hdinsight-apache-spark-use-with-data-lake-store/hdinsight-jupyter-job-status.png "Stan zadania notesu Jupyter")

5. Ładowanie przykładowych danych do tabeli tymczasowej przy użyciu hello **HVAC.csv** plik skopiowany toohello konta usługi Data Lake Store. Można uzyskać dostępu do hello danych na koncie usługi Data Lake Store hello przy użyciu hello następującego wzorca adresu URL.

    * Jeśli masz usługi Data Lake Store jako domyślny magazyn HVAC.csv będzie na toohello podobne ścieżki hello następującego adresu URL:

            adl://<data_lake_store_name>.azuredatalakestore.net/<cluster_root>/HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv

        Lub, można także użyć skróconą format hello poniżej:

            adl:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv

    * Jeśli masz usługi Data Lake Store jako dodatkowego magazynu HVAC.csv będzie w lokalizacji hello jest kopiowany, takich jak:

            adl://<data_lake_store_name>.azuredatalakestore.net/<path_to_file>

     W pustej komórce Wklej hello poniższy przykład kodu, Zastąp **MYDATALAKESTORE** z nazwy konta usługi Data Lake Store i naciśnij klawisz **SHIFT + ENTER**. Ten przykład kodu rejestruje hello danych do tabeli tymczasowej o nazwie **hvac**.

            # Load hello data. hello path below assumes Data Lake Store is default storage for hello Spark cluster
            hvacText = sc.textFile("adl://MYDATALAKESTORE.azuredatalakestore.net/cluster/mysparkcluster/HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

            # Create hello schema
            hvacSchema = StructType([StructField("date", StringType(), False),StructField("time", StringType(), False),StructField("targettemp", IntegerType(), False),StructField("actualtemp", IntegerType(), False),StructField("buildingID", StringType(), False)])

            # Parse hello data in hvacText
            hvac = hvacText.map(lambda s: s.split(",")).filter(lambda s: s[0] != "Date").map(lambda s:(str(s[0]), str(s[1]), int(s[2]), int(s[3]), str(s[6]) ))

            # Create a data frame
            hvacdf = sqlContext.createDataFrame(hvac,hvacSchema)

            # Register hello data fram as a table toorun queries against
            hvacdf.registerTempTable("hvac")

6. Ponieważ używasz jądra PySpark, można teraz bezpośrednio uruchomić zapytanie SQL na tabeli tymczasowej hello **hvac** właśnie utworzony przy użyciu hello `%%sql` magic. Aby uzyskać więcej informacji na temat hello `%%sql` magic, a także innych poleceń magicznych dostępnych z użyciem jądra PySpark hello, zobacz [jądra dostępne dla notesu Jupyter w klastrze z klastrami Spark w usłudze HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).

        %%sql
        SELECT buildingID, (targettemp - actualtemp) AS temp_diff, date FROM hvac WHERE date = \"6/1/13\"

7. Po pomyślnym ukończeniu zadania hello hello następujące tabelaryczne dane wyjściowe jest wyświetlane domyślnie.

      ![Wyniki zapytania w tabeli danych wyjściowych](./media/hdinsight-apache-spark-use-with-data-lake-store/jupyter-tabular-output.png "Wyniki zapytania w tabeli danych wyjściowych")

     Można również sprawdzić hello wyniki w postaci innych wizualizacji. Na przykład wykres warstwowy powitalne samych danych wyjściowych będzie wyglądać hello poniżej.

     ![Wykres warstwowy wyników zapytania](./media/hdinsight-apache-spark-use-with-data-lake-store/jupyter-area-output.png "Wykres warstwowy wyników zapytania")

8. Po zakończeniu uruchamiania aplikacji hello należy zamknięcia hello notesu toorelease hello zasobów. toodo tak, z hello **pliku** kliknij menu notesu hello **zamknąć i zatrzymuje**. To spowoduje zamknięcie i zamknij hello notesu.


## <a name="next-steps"></a>Następne kroki

* [Tworzenie autonomicznych Scala aplikacji toorun w klastrze Apache Spark](hdinsight-apache-spark-create-standalone-application.md)
* [Użyj narzędzia HDInsight Tools w zestawie narzędzi Azure dla aplikacji Spark toocreate IntelliJ dla klastra usługi HDInsight Spark Linux](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Użyj narzędzia HDInsight Tools w zestawie narzędzi Azure dla programu Eclipse toocreate Spark aplikacji dla klastra usługi HDInsight Spark Linux](hdinsight-apache-spark-eclipse-tool-plugin.md)
