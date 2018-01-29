---
title: "Uruchamianie interakcyjnych zapytań w klastrze Spark w usłudze HDInsight Azure | Dokumentacja firmy Microsoft"
description: "Przewodnik Szybki start platformy HDInsight Spark opisujący sposób tworzenia klastra platformy Apache Spark w usłudze HDInsight."
keywords: spark quickstart,interactive spark,interactive query,hdinsight spark,azure spark
services: hdinsight
documentationcenter: 
author: mumian
manager: cgronlun
editor: cgronlun
tags: azure-portal
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/29/2017
ms.author: jgao
ms.openlocfilehash: 78ab44a7afa6523e1e9e4082b3f45b1a28affe77
ms.sourcegitcommit: a48e503fce6d51c7915dd23b4de14a91dd0337d8
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/05/2017
---
# <a name="run-interactive-queries-on-spark-clusters-in-hdinsight"></a>Uruchamianie interakcyjnych zapytań w klastrze Spark w usłudze HDInsight

Dowiedz się, jak użyć notesu Jupyter do uruchamiania interakcyjnych zapytań Spark SQL w odniesieniu do klastra Spark. 

[Notesu Jupyter](http://jupyter-notebook.readthedocs.io/en/latest/notebook.html) jest oparty na przeglądarce aplikacji, rozszerzający interaktywna opartych na konsoli sieci Web. Platforma Spark w usłudze HDInsight obejmuje również [notesu Zeppelin](apache-spark-zeppelin-notebook.md). Notesu Jupyter jest używana w tym samouczku.

Notesów Jupyter w klastrach HDInsight obsługuje trzy jądra - **PySpark**, **PySpark3**, i **Spark**. **PySpark** jądra jest używana w tym samouczku. Aby uzyskać więcej informacji na temat jądra i korzyści wynikające ze stosowania **PySpark**, zobacz [klastrów jądra notesu Jupyter do użycia z platformy Apache Spark w usłudze HDInsight](apache-spark-jupyter-notebook-kernels.md). Aby użyć notesu Zeppelin, zobacz [klastra notesów Zeppelin korzystać z platformy Apache Spark w usłudze Azure HDInsight](./apache-spark-zeppelin-notebook.md).

W tym samouczku zapytaniu dotyczącym danych w pliku csv. Należy najpierw załadować dane do Spark jako dataframe. Następnie można uruchomić zapytania na dataframe za pomocą notesu Jupyter. 

## <a name="prerequisites"></a>Wymagania wstępne

* **Klaster usługi Azure HDInsight Spark**. Aby uzyskać instrukcje, zobacz [utworzyć klaster Apache Spark w usłudze Azure HDInsight](apache-spark-jupyter-spark-sql.md).
* **Notesu Jupyter przy użyciu PySpark**. Aby uzyskać instrukcje, zobacz [tworzenie notesu Jupyter](./apache-spark-jupyter-spark-sql.md#create-a-jupyter-notebook).

## <a name="create-a-dataframe-from-a-csv-file"></a>Utwórz dataframe z pliku csv

Element SQLContext aplikacji można utworzyć dataframes z istniejących RDD, z tabeli programu Hive lub ze źródeł danych. 

**Aby utworzyć dataframe z pliku csv**

1. Tworzenie notesu Jupyter przy użyciu PySpark, jeśli nie masz. Aby uzyskać instrukcje, zobacz [tworzenie notesu Jupyter](./apache-spark-jupyter-spark-sql.md#create-a-jupyter-notebook).

2. Wklej następujący kod w pustej komórce notesu, a następnie naciśnij klawisz **SHIFT + ENTER** do uruchomienia kodu. Kod importuje typy wymagane w tym scenariuszu:

    ```PySpark
    from pyspark.sql import *
    from pyspark.sql.types import *
    ```
    Przez jądro PySpark tworzenie notesu, Spark i Hive kontekstów są utworzony automatycznie po uruchomieniu pierwszej komórki kodu. Nie ma konieczności jawnego tworzenia kontekstów.

    Podczas uruchamiania interaktywnego zapytania w oprogramowaniu Jupyter, tytuł okna lub karty przeglądarki sieci web zawiera **(zajęty)** stan wraz z tytułem notesu. Widoczne jest także pełne kółko obok tekstu **PySpark** w prawym górnym rogu. Po zakończeniu zadania zmienia się ono w pusty okrąg.

    ![Stan interakcyjnego zapytania Spark SQL](./media/apache-spark-load-data-run-query/hdinsight-spark-interactive-spark-query-status.png "Stan interakcyjnego zapytania Spark SQL")

3. Uruchom następujący kod, aby utworzyć dataframe i tabeli tymczasowej (**hvac**), uruchamiając następujący kod: kod nie Wyodrębnij wszystkie kolumny dostępne w pliku CSV. 

    ```PySpark
    # Create an RDD from sample data
    hvacText = sc.textFile("wasbs:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")
    
    # Create a schema for our data
    Entry = Row('Date', 'Time', 'TargetTemp', 'ActualTemp', 'BuildingID')
    
    # Parse the data and create a schema
    hvacParts = hvacText.map(lambda s: s.split(',')).filter(lambda s: s[0] != 'Date')
    hvac = hvacParts.map(lambda p: Entry(str(p[0]), str(p[1]), int(p[2]), int(p[3]), int(p[6])))
    
    # Infer the schema and create a table       
    hvacTable = sqlContext.createDataFrame(hvac)
    hvacTable.registerTempTable('hvactemptable')
    dfw = DataFrameWriter(hvacTable)
    dfw.saveAsTable('hvac')
    ```
    Poniższy zrzut ekranu przedstawia migawki pliku HVAC.csv. Plik csv zawiera wszystkie klastry HDInsigt Spark. Przechwytywanie danych zmiany temperatury w budynku.

    ![Migawki danych do interaktywnego zapytań Spark SQL](./media/apache-spark-load-data-run-query/hdinsight-spark-sample-data-interactive-spark-sql-query.png "migawki danych do interaktywnego zapytań Spark SQL")

## <a name="run-queries-on-the-dataframe"></a>Uruchamianie kwerend dotyczących dataframe

Po utworzeniu tabeli, możesz uruchomić kwerendę interakcyjne na danych.

**Aby uruchomić kwerendę**

1. W pustej komórce notesu, uruchom następujący kod:

    ```PySpark
    %%sql
    SELECT buildingID, (targettemp - actualtemp) AS temp_diff, date FROM hvac WHERE date = \"6/1/13\"
    ```

   Ponieważ jądra PySpark są używane w notesie, można teraz bezpośrednio uruchomić interakcyjne zapytania SQL w tabeli tymczasowej **hvac** utworzonego przy użyciu `%%sql` magic. Aby uzyskać więcej informacji na temat polecenia magicznego `%%sql` oraz innych poleceń magicznych dostępnych za pośrednictwem jądra PySpark, zobacz [Jądra dostępne dla notesu Jupyter w klastrze Spark w usłudze HDInsight](apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).

   Domyślnie jest wyświetlana następująca tabela danych wyjściowych.

     ![Tabela wyjściowa wyników interakcyjnego zapytania Spark](./media/apache-spark-load-data-run-query/hdinsight-interactive-spark-query-result.png "Tabela wyjściowa wyników interakcyjnego zapytania Spark")

3. Wyniki można również przeglądać w postaci innych wizualizacji. Aby wyświetlić wykres warstwowy tych samych danych wyjściowych, wybierz **obszaru** następnie ustaw inne wartości, jak pokazano.

    ![Wykres warstwowy wyników interakcyjnego zapytania Spark](./media/apache-spark-load-data-run-query/hdinsight-interactive-spark-query-result-area-chart.png "Wykres warstwowy wyników interakcyjnego zapytania Spark")

10. Z **pliku** menu w notesie kliknij **zapisywanie i punktu kontrolnego**. 

11. Jeśli zaczynasz [następny samouczek](apache-spark-use-bi-tools.md) teraz, pozostaw otwarte notesu. Jeśli nie, należy wyłączyć aby zwolnić zasoby klastra: z **pliku** menu w notesie kliknij **zamknąć i zatrzymuje**.

## <a name="next-step"></a>Następny krok

W tym artykule przedstawiono sposób wykonywania interakcyjnych zapytań w łączniku Spark przy użyciu notesu Jupyter. Przejdź do następnego artykuł, aby zobaczyć, jak dane, które są zarejestrowane w Spark można ściągnąć do narzędzia analytics analizy Biznesowej, takich jak Power BI i Tableau. 

> [!div class="nextstepaction"]
>[Platforma Spark BI z usługą Azure HDInsight przy użyciu narzędzi do wizualizacji danych](apache-spark-use-bi-tools.md)




