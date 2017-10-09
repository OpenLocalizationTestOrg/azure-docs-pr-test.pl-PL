---
title: "aaaRun interakcyjnych zapytań w klastrze Spark w usłudze HDInsight Azure | Dokumentacja firmy Microsoft"
description: "Szybki Start Spark w usłudze HDInsight w sposób klastra toocreate Apache Spark w usłudze HDInsight."
keywords: spark quickstart,interactive spark,interactive query,hdinsight spark,azure spark
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: nitinme
ms.openlocfilehash: 3864eba50eb3828a9ecb657ded88080e1974585f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="run-interactive-queries-on-an-hdinsight-spark-cluster"></a>Uruchamianie interakcyjnych zapytań w klastrze Spark w usłudze HDInsight

W tym artykule używamy Jupyter notebook toorun interakcyjne zapytań Spark SQL przed klastra Spark. Notesu Jupyter jest oparty na przeglądarce aplikacji, rozszerzający hello toohello interaktywna opartych na konsoli sieci Web. Aby uzyskać więcej informacji, zobacz [notesu Jupyter hello](http://jupyter-notebook.readthedocs.io/en/latest/notebook.html).

W tym samouczku, użyj hello **PySpark** jądra w toorun notesu Jupyter hello interakcyjne zapytań Spark SQL. Notesów Jupyter w klastrach HDInsight obsługuje również dwa inne jądra - **PySpark3** i **Spark**. Aby uzyskać więcej informacji o jądra hello i korzyści hello **PySpark**, zobacz [klastrów jądra notesu Jupyter do użycia z platformy Apache Spark w usłudze HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md).

## <a name="prerequisites"></a>Wymagania wstępne

* **Klaster usługi Azure HDInsight Spark**. Aby uzyskać instrukcje, zobacz [utworzyć klaster Apache Spark w usłudze Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).

## <a name="create-a-jupyter-notebook-toorun-interactive-queries"></a>Tworzenie notesu Jupyter toorun interakcyjnych zapytań

zapytania toorun używamy przykładowych danych, które jest domyślnie dostępna w magazynie hello skojarzony z klastrem hello. Jednak należy najpierw załadować dane do Spark jako dataframe. Po utworzeniu hello dataframe, można wykonać zapytania na nim za pomocą notesu Jupyter hello. W tej sekcji można przyjrzeć się jak:

* Rejestrowanie zestawu danych przykładowych jako Spark dataframe.
* Uruchamianie kwerend dotyczących hello dataframe.

1. Otwórz hello [portalu Azure](https://portal.azure.com/). Jeśli zgłoszono toopin hello klastra toohello z pulpitu nawigacyjnego, kliknij Kafelek klastra hello z bloku hello pulpitu nawigacyjnego toolaunch hello klastra.

    Jeśli nie przypiąć hello klastra toohello pulpitu nawigacyjnego, w okienku po lewej stronie powitania kliknij przycisk **klastrów usługi HDInsight**, a następnie kliknij przycisk hello klaster został utworzony.

3. W obszarze **Szybkie łącza** kliknij pozycję **Pulpity nawigacyjne klastra**, a następnie pozycję **Notes Jupyter**. Jeśli zostanie wyświetlony monit, wprowadź poświadczenia administratora hello hello klastra.

   ![Otwórz Jupyter notebook toorun interakcyjne Spark SQL zapytania](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-start-jupyter-interactive-spark-sql-query.png "Jupyter Otwórz notesu toorun interakcyjne Spark SQL zapytań")

   > [!NOTE]
   > Mogą również uzyskać dostęp hello Jupyter notebook dla klastra przez hello otwarcia następującego adresu URL w przeglądarce. Zastąp **CLUSTERNAME** o nazwie hello klastra:
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >
3. Utwórz notes. Kliknij opcję **New** (Nowy), a następnie kliknij pozycję **PySpark**.

   ![Utwórz Jupyter notebook toorun interakcyjne Spark SQL kwerendę](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-create-jupyter-interactive-Spark-SQL-query.png "tworzenie Jupyter notebook toorun interakcyjne Spark SQL kwerendy")

   Nowy notes jest utworzony i otwarty o nazwie hello Untitled(Untitled.pynb).

4. Kliknij nazwę notesu hello u góry hello, a następnie wprowadź przyjazną nazwę, jeśli chcesz.

    ![Podaj nazwę dla hello Jupter notesu toorun interakcyjne Spark zapytania z](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-jupyter-notebook-name.png "Podaj nazwę dla hello Jupter notesu toorun interakcyjne Spark zapytania z")

5. Wklej hello następujący kod w pustej komórki, a następnie naciśnij **SHIFT + ENTER** toorun hello kodu. Witaj kod importuje typy hello wymagane dla tego scenariusza:

        from pyspark.sql.types import *

    Ponieważ Notes jądro PySpark hello został utworzony, nie trzeba toocreate kontekstów jawnie. konteksty Spark i Hive Hello są utworzony automatycznie po uruchomieniu pierwszej komórki kodu hello.

    ![Stan interakcyjnego zapytania Spark SQL](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-interactive-spark-query-status.png "Stan interakcyjnego zapytania Spark SQL")

    Każdym uruchomieniu zapytania interakcyjne w oprogramowaniu Jupyter, tytuł okna przeglądarki sieci web zawiera **(zajęty)** stan wraz z tytułem notesu hello. Zobacz też toohello dalej pełne kółko **PySpark** tekst w hello prawym górnym rogu. Po zakończeniu zadania hello zmienia tooa okrąg.

6. Przed załadowaniem danych hello w klastrze Spark NAS Szukaj migawkę go. Witaj przykładowych danych używanych w tym samouczku jest dostępna jako plik CSV we wszystkich klastrach HDInsight Spark w **\HdiSamples\HdiSamples\SensorSampleData\hvac\hvac.csv**. Witaj danych przechwytuje hello zmiany temperatury w budynku. Oto hello kilka pierwszych wierszy hello danych.

    ![Migawki danych do interaktywnego zapytań Spark SQL](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-sample-data-interactive-spark-sql-query.png "migawki danych do interaktywnego zapytań Spark SQL")

6. Tworzenie dataframe i tabeli tymczasowej (**hvac**), uruchamiając hello następującego kodu. W tym samouczku firma Microsoft nie twórz wszystkie hello kolumn w tabeli tymczasowej hello jako kolumny w porównaniu toohello w hello dane pierwotne w formacie CSV. 

        # Create an RDD from sample data
        hvacText = sc.textFile("wasbs:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

        # Create a schema for our data
        Entry = Row('Date', 'Time', 'TargetTemp', 'ActualTemp', 'BuildingID')

        # Parse hello data and create a schema
        hvacParts = hvacText.map(lambda s: s.split(',')).filter(lambda s: s[0] != 'Date')
        hvac = hvacParts.map(lambda p: Entry(str(p[0]), str(p[1]), int(p[2]), int(p[3]), int(p[6])))
        
        # Infer hello schema and create a table       
        hvacTable = sqlContext.createDataFrame(hvac)
        hvacTable.registerTempTable('hvactemptable')
        dfw = DataFrameWriter(hvacTable)
        dfw.saveAsTable('hvac')

7. Po utworzeniu tabeli hello, uruchom zapytanie interakcyjne na powitania danych, użyj następującego kodu hello.

        %%sql
        SELECT buildingID, (targettemp - actualtemp) AS temp_diff, date FROM hvac WHERE date = \"6/1/13\"

   Ponieważ używasz jądra PySpark, można teraz bezpośrednio uruchomić interakcyjne zapytania SQL w tabeli tymczasowej hello **hvac** utworzony przy użyciu hello `%%sql` magic. Aby uzyskać więcej informacji na temat hello `%%sql` magic i innych poleceń magicznych dostępnych z użyciem jądra PySpark hello, zobacz [jądra dostępne dla notesu Jupyter w klastrze z klastrami Spark w usłudze HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).

   Domyślnie powoduje wyświetlenie Hello następujące tabelaryczne dane wyjściowe.

     ![Tabela wyjściowa wyników interakcyjnego zapytania Spark](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-interactive-spark-query-result.png "Tabela wyjściowa wyników interakcyjnego zapytania Spark")

    Można również sprawdzić hello wyniki w postaci innych wizualizacji. Na przykład wykres warstwowy powitalne samych danych wyjściowych będzie wyglądać hello poniżej.

    ![Wykres warstwowy wyników interakcyjnego zapytania Spark](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-interactive-spark-query-result-area-chart.png "Wykres warstwowy wyników interakcyjnego zapytania Spark")

9. Zamknij zasobów klastra hello toorelease notesu powitania po zakończeniu działania aplikacji hello. toodo tak, z hello **pliku** kliknij menu notesu hello **zamknąć i zatrzymuje**.

## <a name="next-step"></a>Następny krok

W niniejszym artykule możesz przedstawiono sposób toorun interakcyjnych zapytań w łączniku Spark przy użyciu notesu Jupyter. Przejdź dalej toosee artykułu toohello, jak można ściągnąć hello danych zarejestrowanych w łączniku Spark do narzędzia analytics analizy Biznesowej, takich jak Power BI i Tableau. 

> [!div class="nextstepaction"]
>[Platforma Spark BI z usługą Azure HDInsight przy użyciu narzędzi do wizualizacji danych](hdinsight-apache-spark-use-bi-tools.md)




