---
title: "aaaAnalyze szczegółowe informacje o aplikacji dzienniki z Spark - Azure HDInsight | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooexport szczegółowe informacje o aplikacji dzienniki tooblob magazynu, a następnie analizować dzienniki hello z platformy Spark w usłudze HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 883beae6-9839-45b5-94f7-7eb0f4534ad5
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/15/2017
ms.author: larryfr
ms.openlocfilehash: 11ed8cf68dba8d5f9d6e4a65eba0d2b5a950cd00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-application-insights-telemetry-logs-with-spark-on-hdinsight"></a>Analizowanie dzienników telemetrii usługi Application Insights z platformy Spark w usłudze HDInsight

Dowiedz się, jak Spark toouse na tooanalyze HDInsight dane telemetryczne szczegółowe informacje o aplikacji.

[Visual Studio Application Insights](../application-insights/app-insights-overview.md) jest usługa analizy, który monitoruje aplikacje sieci web. Dane telemetryczne generowane przez usługę Application Insights może być eksportowany tooAzure magazynu. Po hello danych w magazynie Azure HDInsight mogą być używane tooanalyze go.

## <a name="prerequisites"></a>Wymagania wstępne

* Aplikacja, która jest skonfigurowana toouse Application Insights.

* Znajomość tworzenia klastra usługi HDInsight opartej na systemie Linux. Aby uzyskać więcej informacji, zobacz [utworzyć Spark w usłudze HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).

  > [!IMPORTANT]
  > kroki Hello w tym dokumencie wymagają klastra usługi HDInsight, który używa systemu Linux. Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej. Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).

* Przeglądarka sieci web.

Witaj następujące zasoby używane w programie tworzenia i testowania w tym dokumencie:

* Dane telemetrii usługi Application Insights został wygenerowany za pomocą [aplikacji sieci web Node.js skonfigurowane usługi Application Insights toouse](../application-insights/app-insights-nodejs.md).

* Platforma Spark opartych na systemie Linux w klastrze usługi HDInsight w wersji 3.5 było używane tooanalyze hello danych.

## <a name="architecture-and-planning"></a>Planowanie i architektura

powitania po diagram ilustruje hello architektury usługi, w tym przykładzie:

![Diagram przedstawiający dane przepływające z usługi Application Insights tooblob magazynu, a następnie przetwarzanych przez Spark w usłudze HDInsight](./media/hdinsight-spark-analyze-application-insight-logs/appinsightshdinsight.png)

### <a name="azure-storage"></a>Azure Storage

Usługi Application Insights może być skonfigurowany toocontinuously eksportowania telemetrii informacji tooblobs. HDInsight można następnie odczytywane dane przechowywane w obiektach blob hello. Istnieją jednak niektóre wymagania, które należy wykonać:

* **Lokalizacja**: hello konta magazynu i HDInsight znajdują się w różnych lokalizacjach, może zwiększyć czas oczekiwania. Zwiększa także kosztów, opłaty za wyjście są stosowane toodata przenoszenia między regionami.

    > [!WARNING]
    > Używanie konta magazynu w innej lokalizacji niż HDInsight nie jest obsługiwane.

* **Typ obiektu blob**: HDInsight obsługuje tylko blokowe obiekty BLOB. Usługa Application Insights domyślnie toousing blokowych obiektów blob, dlatego powinna działać domyślnie z usługą HDInsight.

Informacje dotyczące dodawania istniejącego klastra usługi HDInsight tooan dodatkowego miejsca do magazynowania, zobacz hello [dodać dodatkowe konta magazynu](hdinsight-hadoop-add-storage.md) dokumentu.

### <a name="data-schema"></a>Schemat danych

Usługa Application Insights udostępnia [wyeksportować modelu danych](../application-insights/app-insights-export-data-model.md) informacje o formacie danych telemetrycznych hello wyeksportowane tooblobs. Hello kroków w tym dokumencie za pomocą programu Spark SQL toowork hello danych. Spark SQL może automatycznie generować schematu dla struktury danych JSON hello zarejestrowane przez usługę Application Insights.

## <a name="export-telemetry-data"></a>Eksportowanie danych telemetrii

Wykonaj kroki hello w [skonfigurować eksportu ciągłego](../application-insights/app-insights-export-telemetry.md) tooconfigure Twojego usługi Application Insights tooexport telemetrii informacji tooan magazynu Azure blob.

## <a name="configure-hdinsight-tooaccess-hello-data"></a>Konfigurowanie usługi HDInsight tooaccess hello danych

W przypadku tworzenia klastra usługi HDInsight, należy dodać konto magazynu hello podczas tworzenia klastra.

tooadd hello konta magazynu Azure tooan istniejącego klastra, użyj informacji hello w hello [dodać dodatkowe konta magazynu](hdinsight-hadoop-add-storage.md) dokumentu.

## <a name="analyze-hello-data-pyspark"></a>Analizowanie danych hello: PySpark

1. Z hello [portalu Azure](https://portal.azure.com), wybierz użytkownika Spark w klastrze usługi HDInsight. Z hello **szybkie linki** zaznacz **pulpitów nawigacyjnych klastrów**, a następnie wybierz **notesu Jupyter** w bloku klastra Dashboard__ hello.

    ![Witaj pulpitów nawigacyjnych klastrów](./media/hdinsight-spark-analyze-application-insight-logs/clusterdashboards.png)

2. Witaj prawym górnym rogu strony Jupyter hello, wybierz **nowy**, a następnie **PySpark**. Otwiera nową kartę przeglądarki zawierające notesu Jupyter na podstawie języka Python.

3. W pierwszym polu hello (nazywane **komórki**) na stronie powitania wprowadź hello następującego tekstu:

   ```python
   sc._jsc.hadoopConfiguration().set('mapreduce.input.fileinputformat.input.dir.recursive', 'true')
   ```

    Ten kod konfiguruje strukturę katalogów Spark toorecursively dostępu hello hello danych wejściowych. Telemetrię usługi Application Insights jest rejestrowane tooa katalogu struktury podobne toohello `/{telemetry type}/YYYY-MM-DD/{##}/`.

4. Użyj **SHIFT + ENTER** toorun hello kodu. Na powitania po lewej stronie komórki Witaj "\*" pojawia się między tooindicate nawiasy hello jest wykonywana hello kodu w tej komórce. Po zakończeniu instalacji hello "\*" zmienia numer tooa i dane wyjściowe podobne toohello następującego tekstu jest wyświetlana poniżej komórki hello:

        Creating SparkContext as 'sc'

        ID    YARN Application ID    Kind    State    Spark UI    Driver log    Current session?
        3    application_1468969497124_0001    pyspark    idle    Link    Link    ✔

        Creating HiveContext as 'sqlContext'
        SparkContext and HiveContext created. Executing user code ...
5. Nowe komórki jest tworzony poniżej hello pierwszy z nich. Wprowadź powitania po tekst w komórce nowe hello. Zastąp `CONTAINER` i `STORAGEACCOUNT` z nazwą konta magazynu Azure hello i nazwa kontenera obiektów blob, który zawiera dane usługi Application Insights.

   ```python
   %%bash
   hdfs dfs -ls wasb://CONTAINER@STORAGEACCOUNT.blob.core.windows.net/
   ```

    Użyj **SHIFT + ENTER** tooexecute tej komórki. Zostanie wyświetlony wynik toohello podobne, następującego tekstu:

        Found 1 items
        drwxrwxrwx   -          0 1970-01-01 00:00 wasb://appinsights@contosostore.blob.core.windows.net/contosoappinsights_2bededa61bc741fbdee6b556571a4831

    Ścieżka wasb Hello zwrócona jest lokalizacja hello hello danych telemetrii usługi Application Insights. Zmień hello `hdfs dfs -ls` wiersz zwrócony hello komórki toouse hello wasb ścieżki, a następnie użyj **SHIFT + ENTER** toorun hello ponownie komórki. Teraz, wyniki hello powinien być wyświetlany hello katalogi, które zawierają dane telemetryczne.

   > [!NOTE]
   > Dla pozostałych hello hello kroki opisane w tej sekcji, hello `wasb://appinsights@contosostore.blob.core.windows.net/contosoappinsights_{ID}/Requests` użyto katalogu. Struktury katalogów mogą się różnić.

6. W następnej komórki hello, wprowadź hello następującego kodu: Zastąp `WASB_PATH` ze ścieżką hello hello w poprzednim kroku.

   ```python
   jsonFiles = sc.textFile('WASB_PATH')
   jsonData = sqlContext.read.json(jsonFiles)
   ```

    Ten kod tworzy dataframe z hello wyeksportowane przez hello Eksport ciągły proces pliki w formacie JSON. Użyj **SHIFT + ENTER** toorun tej komórki.
7. W następnej komórki hello wprowadź i uruchom powitania po tooview hello schematu, Spark utworzony hello JSON plików:

   ```python
   jsonData.printSchema()
   ```

    Witaj schematu dla każdego typu danych telemetrycznych różni się. Witaj poniższym przykładzie jest hello schematem generowany dla żądań sieci web (dane przechowywane w hello `Requests` podkatalogu):

        root
        |-- context: struct (nullable = true)
        |    |-- application: struct (nullable = true)
        |    |    |-- version: string (nullable = true)
        |    |-- custom: struct (nullable = true)
        |    |    |-- dimensions: array (nullable = true)
        |    |    |    |-- element: string (containsNull = true)
        |    |    |-- metrics: array (nullable = true)
        |    |    |    |-- element: string (containsNull = true)
        |    |-- data: struct (nullable = true)
        |    |    |-- eventTime: string (nullable = true)
        |    |    |-- isSynthetic: boolean (nullable = true)
        |    |    |-- samplingRate: double (nullable = true)
        |    |    |-- syntheticSource: string (nullable = true)
        |    |-- device: struct (nullable = true)
        |    |    |-- browser: string (nullable = true)
        |    |    |-- browserVersion: string (nullable = true)
        |    |    |-- deviceModel: string (nullable = true)
        |    |    |-- deviceName: string (nullable = true)
        |    |    |-- id: string (nullable = true)
        |    |    |-- osVersion: string (nullable = true)
        |    |    |-- type: string (nullable = true)
        |    |-- location: struct (nullable = true)
        |    |    |-- city: string (nullable = true)
        |    |    |-- clientip: string (nullable = true)
        |    |    |-- continent: string (nullable = true)
        |    |    |-- country: string (nullable = true)
        |    |    |-- province: string (nullable = true)
        |    |-- operation: struct (nullable = true)
        |    |    |-- name: string (nullable = true)
        |    |-- session: struct (nullable = true)
        |    |    |-- id: string (nullable = true)
        |    |    |-- isFirst: boolean (nullable = true)
        |    |-- user: struct (nullable = true)
        |    |    |-- anonId: string (nullable = true)
        |    |    |-- isAuthenticated: boolean (nullable = true)
        |-- internal: struct (nullable = true)
        |    |-- data: struct (nullable = true)
        |    |    |-- documentVersion: string (nullable = true)
        |    |    |-- id: string (nullable = true)
        |-- request: array (nullable = true)
        |    |-- element: struct (containsNull = true)
        |    |    |-- count: long (nullable = true)
        |    |    |-- durationMetric: struct (nullable = true)
        |    |    |    |-- count: double (nullable = true)
        |    |    |    |-- max: double (nullable = true)
        |    |    |    |-- min: double (nullable = true)
        |    |    |    |-- sampledValue: double (nullable = true)
        |    |    |    |-- stdDev: double (nullable = true)
        |    |    |    |-- value: double (nullable = true)
        |    |    |-- id: string (nullable = true)
        |    |    |-- name: string (nullable = true)
        |    |    |-- responseCode: long (nullable = true)
        |    |    |-- success: boolean (nullable = true)
        |    |    |-- url: string (nullable = true)
        |    |    |-- urlData: struct (nullable = true)
        |    |    |    |-- base: string (nullable = true)
        |    |    |    |-- hashTag: string (nullable = true)
        |    |    |    |-- host: string (nullable = true)
        |    |    |    |-- protocol: string (nullable = true)
8. Użyj powitania po dataframe hello tooregister jako tabeli tymczasowej i uruchomienie na powitania danych zapytania:

   ```python
   jsonData.registerTempTable("requests")
   df = sqlContext.sql("select context.location.city from requests where context.location.city is not null")
   df.show()
   ```

    To zapytanie zwraca informacje Miasto hello hello górny 20 rekordów, w którym context.location.city nie jest zerowa.

   > [!NOTE]
   > Struktura kontekstu Hello znajduje się w wszystkie dane telemetryczne zarejestrowane przez usługę Application Insights. element Miasto Hello może nie można wypełnić w dziennikach. Użyj tooidentify schematu hello inne elementy, które można wykonać zapytanie zawierające dane dla dzienników.

    Ta kwerenda zwraca informacje toohello podobne następującego tekstu:

        +---------+
        |     city|
        +---------+
        | Bellevue|
        |  Redmond|
        |  Seattle|
        |Charlotte|
        ...
        +---------+

## <a name="analyze-hello-data-scala"></a>Analizowanie danych hello: Scala

1. Z hello [portalu Azure](https://portal.azure.com), wybierz użytkownika Spark w klastrze usługi HDInsight. Z hello **szybkie linki** zaznacz **pulpitów nawigacyjnych klastrów**, a następnie wybierz **notesu Jupyter** w bloku klastra Dashboard__ hello.

    ![Witaj pulpitów nawigacyjnych klastrów](./media/hdinsight-spark-analyze-application-insight-logs/clusterdashboards.png)
2. Witaj prawym górnym rogu strony Jupyter hello, wybierz **nowy**, a następnie **Scala**. Pojawi się na nowej karcie przeglądarki zawierające notesu Jupyter opartych na języku Scala.
3. W pierwszym polu hello (nazywane **komórki**) na stronie powitania wprowadź hello następującego tekstu:

   ```scala
   sc.hadoopConfiguration.set("mapreduce.input.fileinputformat.input.dir.recursive", "true")
   ```

    Ten kod konfiguruje strukturę katalogów Spark toorecursively dostępu hello hello danych wejściowych. Telemetrii usługi Application Insights rejestrowane za podobną strukturę katalogów tooa`/{telemetry type}/YYYY-MM-DD/{##}/`.

4. Użyj **SHIFT + ENTER** toorun hello kodu. Na powitania po lewej stronie komórki Witaj "\*" pojawia się między tooindicate nawiasy hello jest wykonywana hello kodu w tej komórce. Po zakończeniu instalacji hello "\*" zmienia numer tooa i dane wyjściowe podobne toohello następującego tekstu jest wyświetlana poniżej komórki hello:

        Creating SparkContext as 'sc'

        ID    YARN Application ID    Kind    State    Spark UI    Driver log    Current session?
        3    application_1468969497124_0001    spark    idle    Link    Link    ✔

        Creating HiveContext as 'sqlContext'
        SparkContext and HiveContext created. Executing user code ...
5. Nowe komórki jest tworzony poniżej hello pierwszy z nich. Wprowadź powitania po tekst w komórce nowe hello. Zastąp `CONTAINER` i `STORAGEACCOUNT` z nazwą konta magazynu Azure hello i nazwa kontenera obiektów blob, który zawiera usługi Application Insights dzienniki.

   ```scala
   %%bash
   hdfs dfs -ls wasb://CONTAINER@STORAGEACCOUNT.blob.core.windows.net/
   ```

    Użyj **SHIFT + ENTER** tooexecute tej komórki. Zostanie wyświetlony wynik toohello podobne, następującego tekstu:

        Found 1 items
        drwxrwxrwx   -          0 1970-01-01 00:00 wasb://appinsights@contosostore.blob.core.windows.net/contosoappinsights_2bededa61bc741fbdee6b556571a4831

    Ścieżka wasb Hello zwrócona jest lokalizacja hello hello danych telemetrii usługi Application Insights. Zmień hello `hdfs dfs -ls` wiersz zwrócony hello komórki toouse hello wasb ścieżki, a następnie użyj **SHIFT + ENTER** toorun hello ponownie komórki. Teraz, wyniki hello powinien być wyświetlany hello katalogi, które zawierają dane telemetryczne.

   > [!NOTE]
   > Dla pozostałych hello hello kroki opisane w tej sekcji, hello `wasb://appinsights@contosostore.blob.core.windows.net/contosoappinsights_{ID}/Requests` użyto katalogu. Ten katalog nie istnieje, chyba że jest dane telemetryczne dla aplikacji sieci web.

6. W następnej komórki hello, wprowadź hello następującego kodu: Zastąp `WASB\_PATH` ze ścieżką hello hello w poprzednim kroku.

   ```scala
   var jsonFiles = sc.textFile('WASB_PATH')
   val sqlContext = new org.apache.spark.sql.SQLContext(sc)
   var jsonData = sqlContext.read.json(jsonFiles)
   ```

    Ten kod tworzy dataframe z hello wyeksportowane przez hello Eksport ciągły proces pliki w formacie JSON. Użyj **SHIFT + ENTER** toorun tej komórki.

7. W następnej komórki hello wprowadź i uruchom powitania po tooview hello schematu, Spark utworzony hello JSON plików:

   ```scala
   jsonData.printSchema
   ```

    Witaj schematu dla każdego typu danych telemetrycznych różni się. Witaj poniższym przykładzie jest hello schematem generowany dla żądań sieci web (dane przechowywane w hello `Requests` podkatalogu):

        root
        |-- context: struct (nullable = true)
        |    |-- application: struct (nullable = true)
        |    |    |-- version: string (nullable = true)
        |    |-- custom: struct (nullable = true)
        |    |    |-- dimensions: array (nullable = true)
        |    |    |    |-- element: string (containsNull = true)
        |    |    |-- metrics: array (nullable = true)
        |    |    |    |-- element: string (containsNull = true)
        |    |-- data: struct (nullable = true)
        |    |    |-- eventTime: string (nullable = true)
        |    |    |-- isSynthetic: boolean (nullable = true)
        |    |    |-- samplingRate: double (nullable = true)
        |    |    |-- syntheticSource: string (nullable = true)
        |    |-- device: struct (nullable = true)
        |    |    |-- browser: string (nullable = true)
        |    |    |-- browserVersion: string (nullable = true)
        |    |    |-- deviceModel: string (nullable = true)
        |    |    |-- deviceName: string (nullable = true)
        |    |    |-- id: string (nullable = true)
        |    |    |-- osVersion: string (nullable = true)
        |    |    |-- type: string (nullable = true)
        |    |-- location: struct (nullable = true)
        |    |    |-- city: string (nullable = true)
        |    |    |-- clientip: string (nullable = true)
        |    |    |-- continent: string (nullable = true)
        |    |    |-- country: string (nullable = true)
        |    |    |-- province: string (nullable = true)
        |    |-- operation: struct (nullable = true)
        |    |    |-- name: string (nullable = true)
        |    |-- session: struct (nullable = true)
        |    |    |-- id: string (nullable = true)
        |    |    |-- isFirst: boolean (nullable = true)
        |    |-- user: struct (nullable = true)
        |    |    |-- anonId: string (nullable = true)
        |    |    |-- isAuthenticated: boolean (nullable = true)
        |-- internal: struct (nullable = true)
        |    |-- data: struct (nullable = true)
        |    |    |-- documentVersion: string (nullable = true)
        |    |    |-- id: string (nullable = true)
        |-- request: array (nullable = true)
        |    |-- element: struct (containsNull = true)
        |    |    |-- count: long (nullable = true)
        |    |    |-- durationMetric: struct (nullable = true)
        |    |    |    |-- count: double (nullable = true)
        |    |    |    |-- max: double (nullable = true)
        |    |    |    |-- min: double (nullable = true)
        |    |    |    |-- sampledValue: double (nullable = true)
        |    |    |    |-- stdDev: double (nullable = true)
        |    |    |    |-- value: double (nullable = true)
        |    |    |-- id: string (nullable = true)
        |    |    |-- name: string (nullable = true)
        |    |    |-- responseCode: long (nullable = true)
        |    |    |-- success: boolean (nullable = true)
        |    |    |-- url: string (nullable = true)
        |    |    |-- urlData: struct (nullable = true)
        |    |    |    |-- base: string (nullable = true)
        |    |    |    |-- hashTag: string (nullable = true)
        |    |    |    |-- host: string (nullable = true)
        |    |    |    |-- protocol: string (nullable = true)

8. Użyj powitania po dataframe hello tooregister jako tabeli tymczasowej i uruchomienie na powitania danych zapytania:

   ```scala
   jsonData.registerTempTable("requests")
   var city = sqlContext.sql("select context.location.city from requests where context.location.city is not null limit 10").show()
   ```

    To zapytanie zwraca informacje Miasto hello hello górny 20 rekordów, w którym context.location.city nie jest zerowa.

   > [!NOTE]
   > Struktura kontekstu Hello znajduje się w wszystkie dane telemetryczne zarejestrowane przez usługę Application Insights. element Miasto Hello może nie można wypełnić w dziennikach. Użyj tooidentify schematu hello inne elementy, które można wykonać zapytanie zawierające dane dla dzienników.
   >
   >

    Ta kwerenda zwraca informacje toohello podobne następującego tekstu:

        +---------+
        |     city|
        +---------+
        | Bellevue|
        |  Redmond|
        |  Seattle|
        |Charlotte|
        ...
        +---------+

## <a name="next-steps"></a>Następne kroki

Więcej przykładów dotyczących przy użyciu Spark toowork przy użyciu danych i usług Azure Zobacz hello w następujących dokumentach:

* [Platforma Spark i analiza biznesowa: interakcyjna analiza danych na platformie Spark w usłudze HDInsight z użyciem narzędzi do analizy biznesowej](hdinsight-apache-spark-use-bi-tools.md)
* [Platforma Spark i usługa Machine Learning: korzystanie z platformy Spark w usłudze HDInsight do analizy temperatury w budynku z użyciem danych HVAC](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Platforma Spark przy użyciu Machine Learning: Korzystanie z platformy Spark w wyników inspekcji żywności toopredict HDInsight](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Przesyłanie strumieniowe Spark: Korzystanie z platformy Spark w usłudze HDInsight do tworzenia aplikacji przesyłania strumieniowego](hdinsight-apache-spark-eventhub-streaming.md)
* [Analiza dzienników witryny sieci Web na platformie Spark w usłudze HDInsight](hdinsight-apache-spark-custom-library-website-log-analysis.md)

Aby uzyskać informacje na temat tworzenia i uruchamiania aplikacji Spark Zobacz hello w następujących dokumentach:

* [Tworzenie autonomicznych aplikacji przy użyciu języka Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Zdalne uruchamianie zadań w klastrze Spark przy użyciu programu Livy](hdinsight-apache-spark-livy-rest-interface.md)
