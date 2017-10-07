---
title: "aaaAnalyze dzienników witryn sieci Web z bibliotekami Python w łączniku Spark - Azure | Dokumentacja firmy Microsoft"
description: "Ten notes pokazano, jak tooanalyze dziennika danych przy użyciu niestandardowa biblioteka z łącznikiem Spark on Azure HDInsight."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 8c61c70f-fe7f-4f0f-a4ab-0cccee5668c9
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 29e4308b2a359aee6d69494a98307d4da07f7909
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-website-logs-using-a-custom-python-library-with-spark-cluster-on-hdinsight"></a>Analizowanie dzienników witryn sieci Web przy użyciu niestandardowa biblioteka języka Python z klastra Spark w usłudze HDInsight

Ten notes pokazano, jak tooanalyze dziennika danych przy użyciu niestandardowa biblioteka z platformy Spark w usłudze HDInsight. biblioteka języka Python, nazywany jest niestandardowa biblioteka Hello używamy **iislogparser.py**.

> [!TIP]
> W tym samouczku jest również dostępny jako notesu Jupyter w klastrze Spark (Linux), które są tworzone w usłudze HDInsight. środowisko notesu Hello umożliwia uruchamianie hello Python wstawki z notesu hello, sama. Samouczek hello tooperform z poziomu Notes, tworzenie klastra Spark, uruchom notesu Jupyter (`https://CLUSTERNAME.azurehdinsight.net/jupyter`), a następnie uruchom notesu hello **analizowanie dzienników z Spark przy użyciu niestandardowych library.ipynb** w obszarze hello  **PySpark** folderu.
>
>

**Wymagania wstępne:**

Musi mieć następujące hello:

* Subskrypcja platformy Azure. Zobacz temat [Uzyskiwanie bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).

* Klaster Apache Spark w usłudze HDInsight. Aby uzyskać instrukcje, zobacz [klastrów utworzyć Apache Spark w usłudze Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).

## <a name="save-raw-data-as-an-rdd"></a>Zapisz dane pierwotne jako RDD
W tej sekcji użyjesz hello [Jupyter](https://jupyter.org) notesu skojarzone z klastra Apache Spark w usłudze HDInsight toorun zadania, które przetwarzać dane pierwotne próbki i zapisz go jako tabeli programu Hive. Witaj przykładowych danych jest plik CSV (hvac.csv) dostępne na wszystkich klastrach domyślnie.

Gdy dane są zapisywane jako tabeli programu Hive, w następnej sekcji hello firma Microsoft będzie łączyć toohello tabeli Hive za pomocą narzędzi analizy Biznesowej, takich jak Power BI i Tableau.

1. Z hello [portalu Azure](https://portal.azure.com/), hello tablicy startowej, kliknij Kafelek hello klastra Spark (jeśli został przypięty toohello tablicy startowej). Można także przechodzić tooyour klastra w obszarze **Przeglądaj wszystko** > **klastrów usługi HDInsight**.   
2. W bloku klastra Spark powitania kliknij **pulpit nawigacyjny klastra**, a następnie kliknij przycisk **notesu Jupyter**. Jeśli zostanie wyświetlony monit, wprowadź poświadczenia administratora hello hello klastra.

   > [!NOTE]
   > Można również przejść hello Jupyter Notebook dla klastra przez hello otwarcia następującego adresu URL w przeglądarce. Zastąp **CLUSTERNAME** o nazwie hello klastra:
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >
3. Utwórz nowy notes. Kliknij opcję **New** (Nowy), a następnie kliknij pozycję **PySpark**.

    ![Tworzenie nowego notesu Jupyter](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-create-jupyter-notebook.png "Tworzenie nowego notesu Jupyter")
4. Nowy notes jest utworzony i otwarty z hello nazwie Untitled.pynb. Kliknij nazwę notesu hello u góry hello, a następnie wprowadź przyjazną nazwę.

    ![Podaj nazwę notesu hello](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-name-jupyter-notebook.png "Podaj nazwę notesu hello")
5. Ponieważ Notes jądro PySpark hello został utworzony, nie trzeba toocreate kontekstów jawnie. konteksty Spark i Hive Hello zostanie automatycznie utworzone automatycznie po uruchomieniu pierwszej komórki kodu hello. Możesz zacząć od importowania typów hello, które są wymagane dla tego scenariusza. Witaj następującego fragmentu kodu w pustej komórce Wklej, a następnie naciśnij klawisz **SHIFT + ENTER**.

        from pyspark.sql import Row
        from pyspark.sql.types import *


1. Utwórz RDD przy użyciu danych dziennika próbki hello już dostępne w klastrze hello. Są dostępne dane hello w hello domyślnego konta magazynu skojarzone z klastrem hello na **\HdiSamples\HdiSamples\WebsiteLogSampleData\SampleLog\909f2b.log**.

        logs = sc.textFile('wasb:///HdiSamples/HdiSamples/WebsiteLogSampleData/SampleLog/909f2b.log')


1. Pobierz przykładowy dziennik Ustaw tooverify tego hello poprzedniego kroku została ukończona pomyślnie.

        logs.take(5)

    Powinny być widoczne następujące dane wyjściowe podobne toohello:

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        [u'#Software: Microsoft Internet Information Services 8.0',
         u'#Fields: date time s-sitename cs-method cs-uri-stem cs-uri-query s-port cs-username c-ip cs(User-Agent) cs(Cookie) cs(Referer) cs-host sc-status sc-substatus sc-win32-status sc-bytes cs-bytes time-taken',
         u'2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step2.png X-ARR-LOG-ID=2ec4b8ad-3cf0-4442-93ab-837317ece6a1 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 53175 871 46',
         u'2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step3.png X-ARR-LOG-ID=9eace870-2f49-4efd-b204-0d170da46b4a 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 51237 871 32',
         u'2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step4.png X-ARR-LOG-ID=4bea5b3d-8ac9-46c9-9b8c-ec3e9500cbea 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 72177 871 47']

## <a name="analyze-log-data-using-a-custom-python-library"></a>Analizowanie danych dziennika przy użyciu niestandardowa biblioteka języka Python
1. W powyższych danych wyjściowych hello hello pierwszych kilku wierszy zawierają informacje o nagłówku hello i każdym wierszu pozostałych dopasowuje schematu hello opisane w tym nagłówka. Podczas analizowania dzienników takie może być skomplikowane. Tak, używamy niestandardowa biblioteka języka Python (**iislogparser.py**), które służą do analizowania tych dzienników znacznie łatwiejsze. Domyślnie ta biblioteka jest dołączana do klastra Spark w usłudze HDInsight w **/HdiSamples/HdiSamples/WebsiteLogSampleData/iislogparser.py**.

    Ta biblioteka nie działa jednak w hello `PYTHONPATH` , nie można użyć przy użyciu instrukcji importu, takich jak `import iislogparser`. toouse tej biblioteki, możemy przeprowadzić dystrybucję go węzłów procesu roboczego hello tooall. Uruchom hello następującego fragmentu.

        sc.addPyFile('wasb:///HdiSamples/HdiSamples/WebsiteLogSampleData/iislogparser.py')


1. `iislogparser`udostępnia funkcję `parse_log_line` zwracającą `None` Jeśli wiersz dziennika jest wiersz nagłówka i zwraca wystąpienie klasy hello `LogLine` klasy, jeśli wykryje wiersza dziennika. Użyj hello `LogLine` tooextract klasy hello tylko wiersze dziennika z hello RDD:

        def parse_line(l):
            import iislogparser
            return iislogparser.parse_log_line(l)
        logLines = logs.map(parse_line).filter(lambda p: p is not None).cache()
2. Pobrać kilka tooverify wyodrębnionego dziennika wiersze, które hello kroku została ukończona pomyślnie.

       logLines.take(2)

   Hello dane wyjściowe powinny być podobne toohello następujące czynności:

       # -----------------
       # THIS IS AN OUTPUT
       # -----------------

       [2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step2.png X-ARR-LOG-ID=2ec4b8ad-3cf0-4442-93ab-837317ece6a1 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 53175 871 46,
        2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step3.png X-ARR-LOG-ID=9eace870-2f49-4efd-b204-0d170da46b4a 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 51237 871 32]
3. Hello `LogLine` klasy, z kolei ma niektóre przydatne metody, takie jak `is_error()`, która zwraca czy wpis dziennika ma kod błędu. Użyj hello toocompute liczba błędów w wierszach dziennika hello wyodrębnione, a następnie zalogowanie wszystkich hello błędy tooa inny plik.

       errors = logLines.filter(lambda p: p.is_error())
       numLines = logLines.count()
       numErrors = errors.count()
       print 'There are', numErrors, 'errors and', numLines, 'log entries'
       errors.map(lambda p: str(p)).saveAsTextFile('wasb:///HdiSamples/HdiSamples/WebsiteLogSampleData/SampleLog/909f2b-2.log')

   Powinny pojawić się dane wyjściowe podobne do następujących hello:

       # -----------------
       # THIS IS AN OUTPUT
       # -----------------

       There are 30 errors and 646 log entries
4. Można również użyć **Matplotlib** tooconstruct wizualizacji danych hello. Na przykład jeśli chcesz tooisolate hello przyczynę żądania, które są uruchamiane przez długi czas, można toofind hello pliki, przyjmujących hello większość czasu tooserve średnio.
   Poniższy fragment Hello pobiera hello top 25 zasobów, których przez większość czasu tooserve żądanie.

       def avgTimeTakenByKey(rdd):
           return rdd.combineByKey(lambda line: (line.time_taken, 1),
                                   lambda x, line: (x[0] + line.time_taken, x[1] + 1),
                                   lambda x, y: (x[0] + y[0], x[1] + y[1]))\
                     .map(lambda x: (x[0], float(x[1][0]) / float(x[1][1])))

       avgTimeTakenByKey(logLines.map(lambda p: (p.cs_uri_stem, p))).top(25, lambda x: x[1])

   Powinny pojawić się dane wyjściowe podobne do następujących hello:

       # -----------------
       # THIS IS AN OUTPUT
       # -----------------

       [(u'/blogposts/mvc4/step13.png', 197.5),
        (u'/blogposts/mvc2/step10.jpg', 179.5),
        (u'/blogposts/extractusercontrol/step5.png', 170.0),
        (u'/blogposts/mvc4/step8.png', 159.0),
        (u'/blogposts/mvcrouting/step22.jpg', 155.0),
        (u'/blogposts/mvcrouting/step3.jpg', 152.0),
        (u'/blogposts/linqsproc1/step16.jpg', 138.75),
        (u'/blogposts/linqsproc1/step26.jpg', 137.33333333333334),
        (u'/blogposts/vs2008javascript/step10.jpg', 127.0),
        (u'/blogposts/nested/step2.jpg', 126.0),
        (u'/blogposts/adminpack/step1.png', 124.0),
        (u'/BlogPosts/datalistpaging/step2.png', 118.0),
        (u'/blogposts/mvc4/step35.png', 117.0),
        (u'/blogposts/mvcrouting/step2.jpg', 116.5),
        (u'/blogposts/aboutme/basketball.jpg', 109.0),
        (u'/blogposts/anonymoustypes/step11.jpg', 109.0),
        (u'/blogposts/mvc4/step12.png', 106.0),
        (u'/blogposts/linq8/step0.jpg', 105.5),
        (u'/blogposts/mvc2/step18.jpg', 104.0),
        (u'/blogposts/mvc2/step11.jpg', 104.0),
        (u'/blogposts/mvcrouting/step1.jpg', 104.0),
        (u'/blogposts/extractusercontrol/step1.png', 103.0),
        (u'/blogposts/sqlvideos/sqlvideos.jpg', 102.0),
        (u'/blogposts/mvcrouting/step21.jpg', 101.0),
        (u'/blogposts/mvc4/step1.png', 98.0)]
5. Można również prezentować te informacje w postaci hello wykresu. Jako pierwszy krok toocreate wykresu, poinformuj nas najpierw utworzyć tabeli tymczasowej **AverageTime**. Witaj tabeli grup Witaj rejestruje przez toosee czasu, jeśli było żadnych nietypowe opóźnienia rzędu w dowolnym momencie konkretnego.

       avgTimeTakenByMinute = avgTimeTakenByKey(logLines.map(lambda p: (p.datetime.minute, p))).sortByKey()
       schema = StructType([StructField('Minutes', IntegerType(), True),
                            StructField('Time', FloatType(), True)])

       avgTimeTakenByMinuteDF = sqlContext.createDataFrame(avgTimeTakenByMinute, schema)
       avgTimeTakenByMinuteDF.registerTempTable('AverageTime')
6. Następnie możesz uruchomić powitania po tooget zapytania SQL wszystkie rekordy hello w hello **AverageTime** tabeli.

       %%sql -o averagetime
       SELECT * FROM AverageTime

   Witaj `%%sql` magic następuje `-o averagetime` gwarantuje, że hello wyników kwerendy hello jest trwały lokalnie na serwerze Jupyter hello (zazwyczaj hello headnode hello klastra). dane wyjściowe Hello jest utrwalony jako [Pandas](http://pandas.pydata.org/) dataframe z hello określona nazwa **averagetime**.

   Powinny pojawić się dane wyjściowe podobne do następujących hello:

   ![Dane wyjściowe kwerendy SQL](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-jupyter-sql-qyery-output.png "wyników zapytania SQL")

   Aby uzyskać więcej informacji na temat hello `%%sql` magicznych, zobacz [obsługiwane parametry z hello %% sql magic](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).
7. Teraz możesz używać Matplotlib, tooconstruct wizualizację danych, toocreate wykresu użycie biblioteki. Ponieważ kreślenia hello musi być utworzony na podstawie hello lokalnie utrwalone **averagetime** dataframe, fragment kodu hello musi rozpoczynać się od hello `%%local` magic. Dzięki temu, że kod hello uruchamiane lokalnie na serwerze Jupyter hello.

       %%local
       %matplotlib inline
       import matplotlib.pyplot as plt

       plt.plot(averagetime['Minutes'], averagetime['Time'], marker='o', linestyle='--')
       plt.xlabel('Time (min)')
       plt.ylabel('Average time taken for request (ms)')

   Powinny pojawić się dane wyjściowe podobne do następujących hello:

   ![Dane wyjściowe Matplotlib](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-apache-spark-web-log-analysis-plot.png "Matplotlib danych wyjściowych")
8. Po zakończeniu uruchamiania aplikacji hello należy zamknięcia hello notesu toorelease hello zasobów. toodo tak, z hello **pliku** kliknij menu notesu hello **zamknąć i zatrzymuje**. To spowoduje zamknięcie i zamknij hello notesu.

## <a name="seealso"></a>Zobacz też
* [Przegląd: platforma Apache Spark w usłudze Azure HDInsight](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a>Scenariusze
* [Platforma Spark i analiza biznesowa: interakcyjna analiza danych na platformie Spark w usłudze HDInsight z użyciem narzędzi do analizy biznesowej](hdinsight-apache-spark-use-bi-tools.md)
* [Platforma Spark i usługa Machine Learning: korzystanie z platformy Spark w usłudze HDInsight do analizy temperatury w budynku z użyciem danych HVAC](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Platforma Spark przy użyciu Machine Learning: Korzystanie z platformy Spark w wyników inspekcji żywności toopredict HDInsight](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Przesyłanie strumieniowe Spark: korzystanie z platformy Spark w usłudze HDInsight do tworzenia aplikacji do przesyłania strumieniowego w czasie rzeczywistym](hdinsight-apache-spark-eventhub-streaming.md)

### <a name="create-and-run-applications"></a>Tworzenie i uruchamianie aplikacji
* [Tworzenie autonomicznych aplikacji przy użyciu języka Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Zdalne uruchamianie zadań w klastrze Spark przy użyciu programu Livy](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a>Narzędzia i rozszerzenia
* [Użyj dodatku HDInsight Tools Plugin dla toocreate IntelliJ IDEA i przesyłanie aplikacji Spark Scala](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Użyj dodatku HDInsight Tools Plugin zdalnie dla aplikacji Spark toodebug IntelliJ IDEA](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Korzystanie z notesów Zeppelin w klastrze Spark w usłudze HDInsight](hdinsight-apache-spark-zeppelin-notebook.md)
* [Jądra dostępne dla notesu Jupyter w klastrze Spark w usłudze HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Korzystanie z zewnętrznych pakietów z notesami Jupyter](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Instalacja oprogramowania Jupyter na komputerze i połącz tooan klastra Spark w usłudze HDInsight](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>Zarządzanie zasobami
* [Zarządzanie zasobami hello klastra Apache Spark w usłudze Azure HDInsight](hdinsight-apache-spark-resource-manager.md)
* [Śledzenie i debugowanie zadań uruchamianych w klastrze Apache Spark w usłudze HDInsight](hdinsight-apache-spark-job-debugging.md)
