---
title: "aaaHive przy użyciu narzędzi Data Lake (Hadoop) dla programu Visual Studio - Azure HDInsight | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak narzędzia hello toouse usługi Data Lake w dla programu Visual Studio toorun Apache Hive zapytania z platformy Apache Hadoop w usłudze Azure HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 2b3e672a-1195-4fa5-afb7-b7b73937bfbe
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/07/2017
ms.author: larryfr
ms.openlocfilehash: dc76974c02cf68bcf701b2b155842c9e9c5cb988
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="run-hive-queries-using-hello-data-lake-tools-for-visual-studio"></a>Uruchamianie zapytań Hive przy użyciu narzędzi Data Lake hello for Visual Studio

Dowiedz się, jak toouse hello Data Lake tools dla Visual Studio tooquery Apache Hive. narzędzia Data Lake Hello pozwalają tooeasily tworzenia, przesyłania i monitorowania tooHadoop zapytań Hive w usłudze Azure HDInsight.

## <a id="prereq"></a>Wymagania wstępne

* Klaster usługi Azure HDInsight (Hadoop w usłudze HDInsight)

  > [!IMPORTANT]
  > Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej. Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).

* Visual Studio (jedna hello następujące wersje):

    * Visual Studio 2013 Community/Professional/Premium/Ultimate z aktualizacją 4

    * Visual Studio 2015 (dowolna wersja)

    * Visual Studio 2017 (dowolna wersja)

* Narzędzia HDInsight tools for Visual Studio lub usługi Azure Data Lake tools dla programu Visual Studio. Zobacz [rozpocząć korzystanie z narzędzi Visual Studio Hadoop dla usługi HDInsight](hdinsight-hadoop-visual-studio-tools-get-started.md) informacji o instalowaniu i konfigurowaniu hello narzędzia.

## <a id="run"></a>Uruchamianie zapytań Hive przy użyciu hello Visual Studio

1. Otwórz **programu Visual Studio** i wybierz **nowy** > **projektu** > **usługi Azure Data Lake** > **HIVE** > **aplikacji Hive**. Podaj nazwę dla tego projektu.

2. Otwórz hello **Script.hql** pliku, który jest tworzony z tego projektu, a następnie wklej w hello następujące instrukcje HiveQL:

   ```hiveql
   set hive.execution.engine=tez;
   DROP TABLE log4jLogs;
   CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
   ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
   STORED AS TEXTFILE LOCATION '/example/data/';
   SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND  INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;
   ```

    Instrukcje te należy wykonać hello następujące akcje:

   * `DROP TABLE`: Jeśli hello tabela istnieje, ta instrukcja usunięcia go.

   * `CREATE EXTERNAL TABLE`: Tworzy nową tabelę "zewnętrzne" w gałęzi. Tabele zewnętrzne przechowywać tylko hello definicji tabeli w gałęzi (powitalne pozostanie danych w oryginalnej lokalizacji hello).

     > [!NOTE]
     > Jeśli oczekujesz hello zaktualizowane przez źródło zewnętrzne podstawowej toobe danych należy użyć tabel zewnętrznych. Na przykład zadania MapReduce lub usługi Azure.
     >
     > Usunięcie tabeli zewnętrznej jest **nie** usunąć dane hello, tylko hello definicji tabeli.

   * `ROW FORMAT`: Określa, że sposób formatowania danych hello Hive. W takim przypadku hello pól w każdym dzienniku są oddzielone spacją.

   * `STORED AS TEXTFILE LOCATION`: Nakazuje Hive gdzie hello są przechowywane dane (katalog hello przykład/danych) i które są przechowywane jako tekst.

   * `SELECT`: Wybierz liczbę wszystkich wierszy gdzie kolumna `t4` zawiera wartość hello `[ERROR]`. Ta instrukcja zwraca wartość `3` ponieważ istnieją trzy wiersze, które zawierają tę wartość.

   * `INPUT__FILE__NAME LIKE '%.log'`-Informuje Hive czy firma Microsoft powinno zwrócić dane tylko z plików w. dziennika. Klauzulę ogranicza hello wyszukiwania toohello sample.log pliku, który zawiera dane hello.

3. Wybierz hello z narzędzi hello **klastra usługi HDInsight** mają toouse dla tego zapytania. Wybierz **przesyłania** instrukcje hello toorun jako zadania Hive.

   ![Przedstawia paska](./media/hdinsight-hadoop-use-hive-visual-studio/toolbar.png)

4. Witaj **Podsumowanie zadania Hive** pojawia się i wyświetla informacje o hello uruchomienia zadania. Użyj hello **Odśwież** połączyć toorefresh hello zadania informacje do momentu hello **stan zadania** zmiany zbyt**Ukończono**.

   ![Podsumowanie zadania wyświetlania zadanie zostało ukończone](./media/hdinsight-hadoop-use-hive-visual-studio/jobsummary.png)

5. Użyj hello **dane wyjściowe zadania** link tooview hello dane wyjściowe tego zadania. Wyświetla `[ERROR] 3`, która jest wartością hello zwracanych przez to zapytanie.

6. Można również uruchomić zapytań programu Hive, bez tworzenia projektu. Przy użyciu **Eksploratora serwera**, rozwiń węzeł **Azure** > **HDInsight**, kliknij prawym przyciskiem myszy serwera usługi HDInsight, a następnie wybierz **Napisz zapytanie Hive**.

7. W hello **temp.hql** dokumentu, która jest wyświetlana, Dodaj następujące instrukcje HiveQL hello:

   ```hiveql
   set hive.execution.engine=tez;
   CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) STORED AS ORC;
   INSERT OVERWRITE TABLE errorLogs SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log';
   ```

    Instrukcje te należy wykonać hello następujące akcje:

   * `CREATE TABLE IF NOT EXISTS`: Tworzy tabelę, jeśli jeszcze nie istnieje. Ponieważ hello `EXTERNAL` — słowo kluczowe nie jest używany, ta instrukcja tworzy wewnętrznej tabeli. Wewnętrzny tabele są przechowywane w magazynie danych hello Hive i są zarządzane przez Hive.

     > [!NOTE]
     > W odróżnieniu od `EXTERNAL` tabel, również porzucenie wewnętrznej tabeli usuwa hello podstawowych danych.

   * `STORED AS ORC`: Magazyny hello dane w formacie (ORC) kolumnowym zoptymalizowane wiersza. ORC jest wysoce zoptymalizowane i wydajne formatu do przechowywania danych gałęzi.

   * `INSERT OVERWRITE ... SELECT`: Wybiera wiersze z hello `log4jLogs` tabeli, która zawiera `[ERROR]`, a następnie wstawia hello danych do hello `errorLogs` tabeli.

8. Z narzędzi hello wybierz **przesyłania** toorun hello zadania. Użyj hello **stan zadania** toodetermine zadania hello została pomyślnie ukończona.

9. tooverify, który hello zadania utworzone hello tabeli, użyj **Eksploratora serwera** i rozwiń **Azure** > **HDInsight** > z klastrem usługi HDInsight > **Bazy danych programu hive** > **domyślne**. Witaj **errorLogs** tabeli i hello **log4jLogs** tabeli są wymienione.

## <a id="nextsteps"></a>Następne kroki

Jak widać, hello narzędzia HDInsight tools for Visual Studio zapewniają prosty sposób toowork z zapytań programu Hive w usłudze HDInsight.

Aby uzyskać ogólne informacje na temat programu Hive w usłudze HDInsight:

* [Korzystanie z programu Hive z usługą Hadoop w usłudze HDInsight](hdinsight-use-hive.md)

Aby uzyskać informacje o innych metodach pracy z platformą Hadoop w usłudze HDInsight:

* [Korzystanie z języka Pig z usługą Hadoop w usłudze HDInsight](hdinsight-use-pig.md)

* [Używanie MapReduce z usługą Hadoop w usłudze HDInsight](hdinsight-use-mapreduce.md)

Aby uzyskać więcej informacji na temat hello HDInsight tools for Visual Studio:

* [Wprowadzenie do narzędzi HDInsight tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md)

[hdinsight-sdk-documentation]: http://msdnstage.redmond.corp.microsoft.com/library/dn479185.aspx

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[apache-tez]: http://tez.apache.org
[apache-hive]: http://hive.apache.org/
[apache-log4j]: http://en.wikipedia.org/wiki/Log4j
[hive-on-tez-wiki]: https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez
[import-to-excel]: http://azure.microsoft.com/documentation/articles/hdinsight-connect-excel-power-query/


[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md



[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md

[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx

[image-hdi-hive-powershell]: ./media/hdinsight-use-hive/HDI.HIVE.PowerShell.png
[img-hdi-hive-powershell-output]: ./media/hdinsight-use-hive/HDI.Hive.PowerShell.Output.png
[image-hdi-hive-architecture]: ./media/hdinsight-use-hive/HDI.Hive.Architecture.png
