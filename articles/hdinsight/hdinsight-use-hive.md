---
title: aaaWhat jest Apache Hive i HiveQL - Azure HDInsight | Dokumentacja firmy Microsoft
description: "Apache Hive jest platforma Hadoop w systemie magazynu danych. Można badać danych przechowywanych w gałęzi przy użyciu HiveQL, które podobne tooTransact-SQL. W tym dokumencie przedstawiono sposób toouse Hive i HiveQL z usługą Azure HDInsight."
keywords: "hiveql, co to jest hive i hadoop hiveql, jak toouse hive, Dowiedz się, hive, co to jest gałąź"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 2c10f989-7636-41bf-b7f7-c4b67ec0814f
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/03/2017
ms.author: larryfr
ms.openlocfilehash: a2772312263895ff99b499898264c2e6d5e816e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-apache-hive-and-hiveql-on-azure-hdinsight"></a>Co to jest Apache Hive i HiveQL w usłudze Azure HDInsight?

[Apache Hive](http://hive.apache.org/) jest systemem magazynu danych dla platformy Hadoop. Gałąź umożliwia podsumowania danych, wyszukiwanie i analizy danych. Zapytań programu hive są zapisywane w HiveQL, czyli tooSQL podobne języka zapytań.

Gałąź umożliwia tooproject struktury danych niestrukturalnych w dużej mierze. Po zdefiniowaniu struktury hello służy HiveQL tooquery hello danych bez znajomości języka Java lub MapReduce.

Usługa HDInsight zapewnia kilka typów klastra, które są dopasowane do konkretnych obciążeń. następujące typy klastrów Hello są najczęściej używane dla zapytań programu Hive:

* __Interakcyjne Hive__: klastra usługi Hadoop A, która zapewnia [niskim opóźnieniu analitycznego przetwarzania (LLAP)](https://cwiki.apache.org/confluence/display/Hive/LLAP) czas odpowiedzi tooimprove funkcje dla interakcyjnych zapytań. Aby uzyskać więcej informacji, zobacz hello [rozpoczynać interakcyjne Hive w usłudze HDInsight](hdinsight-hadoop-use-interactive-hive.md) dokumentu.

* __Hadoop__: klaster A Hadoop dostosowana pod kątem obciążeń przetwarzania wsadowego. Aby uzyskać więcej informacji, zobacz hello [Start z usługą Hadoop w usłudze HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md) dokumentu.

* __Platforma Spark__: platforma Apache Spark ma wbudowaną funkcję do pracy z gałęzi. Aby uzyskać więcej informacji, zobacz hello [rozpoczynać Spark w usłudze HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md) dokumentu.

* __HBase__: HiveQL mogą być używane tooquery danych przechowywanych w bazie danych HBase. Aby uzyskać więcej informacji, zobacz hello [rozpoczynać się od bazy danych HBase w usłudze HDInsight](hdinsight-hbase-tutorial-get-started-linux.md) dokumentu.

## <a name="how-toouse-hive"></a>Jak Hive toouse

Użyj poniższej hello tabeli toodiscover jak toouse Hive z usługą HDInsight:

| **Ta metoda** Jeśli chcesz... | .. .an **interakcyjne** powłoki | ... **partii** przetwarzania | .. zwykle to **systemu operacyjnego klastra** | .. .from to **system operacyjny klienta** |
|:--- |:---:|:---:|:--- |:--- |
| [Widok gałęzi](hdinsight-hadoop-use-hive-ambari-view.md) |✔ |✔ |Linux |Wszelkie (opartych na przeglądarce) |
| [Beeline klienta](hdinsight-hadoop-use-hive-beeline.md) |✔ |✔ |Linux |Linux, Unix, Mac OS X lub systemu Windows |
| [Interfejs API REST](hdinsight-hadoop-use-hive-curl.md) |&nbsp; |✔ |Linux lub Windows * |Linux, Unix, Mac OS X lub systemu Windows |
| [Narzędzia HDInsight tools for Visual Studio](hdinsight-hadoop-use-hive-visual-studio.md) |&nbsp; |✔ |Linux lub Windows * |Windows |
| [Środowisko Windows PowerShell](hdinsight-hadoop-use-hive-powershell.md) |&nbsp; |✔ |Linux lub Windows * |Windows |

> [!IMPORTANT]
> \*Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej. Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).
>
> Jeśli korzystasz z klastra usługi HDInsight opartej na systemie Windows, możesz użyć hello [konsoli zapytania](hdinsight-hadoop-use-hive-query-console.md) z przeglądarki lub [pulpitu zdalnego](hdinsight-hadoop-use-hive-remote-desktop.md) toorun zapytań programu Hive.

## <a name="hiveql-language-reference"></a>Dokumentacja języka HiveQL

Dokumentacja języka HiveQL jest dostępna w hello [ręcznego języka (https://cwiki.apache.org/confluence/display/Hive/LanguageManual)](https://cwiki.apache.org/confluence/display/Hive/LanguageManual).

## <a name="hive-and-data-structure"></a>Struktura danych i hive

Gałąź rozumie struktury toowork z i częściowo ustrukturyzowanych danych. Na przykład pliki tekstowe gdzie hello pola są rozdzielone określonych znaków. Po instrukcji HiveQL Hello tworzy tabelę danych rozdzielonych spacjami:

```hiveql
CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
STORED AS TEXTFILE LOCATION '/example/data/';
```

Hive obsługuje również niestandardowe **serializator/deserializers (SerDe)** złożonego lub nieregularnych strukturalnych danych. Aby uzyskać więcej informacji, zobacz hello [jak toouse niestandardowych SerDe JSON z usługą HDInsight](http://blogs.msdn.com/b/bigdatasupport/archive/2014/06/18/how-to-use-a-custom-json-serde-with-microsoft-azure-hdinsight.aspx) dokumentu.

Aby uzyskać więcej informacji na formaty plików obsługiwane przez Hive, zobacz hello [ręcznego języka (https://cwiki.apache.org/confluence/display/Hive/LanguageManual)](https://cwiki.apache.org/confluence/display/Hive/LanguageManual)

## <a name="hive-internal-tables-vs-external-tables"></a>Hive tabel zewnętrznych vs wewnętrzny tabel

Istnieją dwa typy tabel, które można utworzyć przy użyciu Hive:

* __Wewnętrzny__: dane są przechowywane w magazynie danych hello Hive. Witaj hurtowni danych znajduje się pod adresem `/hive/warehouse/` na powitania domyślny magazyn dla klastra hello.

    Użyj wewnętrznego tabel, gdy:

    * Dane są tymczasowe.
    * Mają cykl życia hello toomanage Hive hello tabeli i danych.

* __Zewnętrzne__: dane są przechowywane poza hello hurtowni danych. Witaj danych mogą być przechowywane na każdy Magazyn dostępny przez klaster hello.

    Użyj tabel zewnętrznych, gdy:

    * dane Hello jest również używany poza Hive. Na przykład pliki danych hello są aktualizowane przez inny proces (co oznacza, że nie blokuje pliki hello.)
    * Dane muszą tooremain w hello bazowy lokalizacji, nawet po porzucenie hello tabeli.
    * Należy lokalizacjach niestandardowych, takich jak konta magazynu z systemem innym niż domyślny.
    * Z programem innym niż hive zarządza hello format danych, lokalizacji itp.

Aby uzyskać więcej informacji, zobacz hello [Hive wewnętrznych i zewnętrznych wprowadzenie tabel] [ cindygross-hive-tables] wpis w blogu.

## <a name="user-defined-functions-udf"></a>Funkcje zdefiniowane przez użytkownika (UDF)

Można również rozszerzać hive za pośrednictwem **funkcje zdefiniowane przez użytkownika (UDF)**. UDF umożliwia funkcjonalności tooimplement lub logikę, która nie jest łatwo uformowana w HiveQL. Przykład przy użyciu Hive za pomocą funkcji UDF Zobacz hello w następujących dokumentach:

* [Użyj funkcji zdefiniowanej przez użytkownika języka Java przy użyciu Hive](hdinsight-hadoop-hive-java-udf.md)

* [Użyj funkcji zdefiniowanej przez użytkownika Python z Hive i Pig](hdinsight-python.md)

* [C# — funkcja zdefiniowana przez użytkownika za pomocą technologii Hive i Pig](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)

* [Jak tooadd gałąź niestandardowe zdefiniowane przez użytkownika funkcji tooHDInsight](http://blogs.msdn.com/b/bigdatasupport/archive/2014/01/14/how-to-add-custom-hive-udfs-to-hdinsight.aspx)

* [Przykład Hive funkcja zdefiniowana przez użytkownika tooconvert formaty daty i godziny tooHive sygnatury czasowej](https://github.com/Azure-Samples/hdinsight-java-hive-udf)

## <a id="data"></a>Przykładowe dane

Hive w usłudze HDInsight jest dostarczany wstępnie załadowane z wewnętrznej tabeli o nazwie `hivesampletable`. Usługa HDInsight zapewnia również przykład zestawów danych, które mogą być używane z gałęzi. Te zestawy danych są przechowywane w hello `/example/data` i `/HdiSamples` katalogów. Te katalogi istnieją w hello domyślny magazyn dla klastra.

## <a id="job"></a>Przykładowe zapytanie Hive

Witaj, następujące kolumny projektu instrukcje HiveQL na powitania `/example/data/sample.log` pliku:

    set hive.execution.engine=tez;
    DROP TABLE log4jLogs;
    CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
    STORED AS TEXTFILE LOCATION '/example/data/';
    SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;

W poprzednim przykładzie hello instrukcje HiveQL hello wykonaj hello następujące akcje:

* `set hive.execution.engine=tez;`: Ustawia hello wykonywania aparatu toouse Tez. Przy użyciu aplikacji Tez zamiast MapReduce zapewnić wzrost wydajności zapytań. Aby uzyskać więcej informacji o aplikacji Tez, zobacz hello [Użyj Apache Tez zwiększonej wydajności](#usetez) sekcji.

    > [!NOTE]
    > Ta instrukcja jest tylko wymagane w przypadku korzystania z klastra usługi HDInsight opartej na systemie Windows. Tez jest hello domyślnego wykonywania aparatu dla usługi HDInsight opartej na systemie Linux.

* `DROP TABLE`: Jeśli hello tabela już istnieje, usuń go.

* `CREATE EXTERNAL TABLE`: Tworzy nowy **zewnętrznych** tabeli w gałęzi rejestru. Tabele zewnętrzne przechowywać tylko hello definicji tabeli w gałęzi. Hello danych pozostaje w oryginalnej lokalizacji hello i hello oryginalnym formacie.

* `ROW FORMAT`: Określa, że sposób formatowania danych hello Hive. W takim przypadku hello pól w każdym dzienniku są oddzielone spacją.

* `STORED AS TEXTFILE LOCATION`: Nakazuje Hive gdzie hello są przechowywane dane (hello `example/data` katalogu) i które są przechowywane jako tekst. można w jednym pliku lub rozłożyć na wiele plików w katalogu hello Hello danych.

* `SELECT`: Wybiera liczbę wszystkich wierszy w przypadku gdy hello kolumny **t4** zawiera wartość hello **[Błąd]**. Ta instrukcja zwraca wartość **3** ponieważ istnieją trzy wiersze, które zawierają tę wartość.

* `INPUT__FILE__NAME LIKE '%.log'`-Hive prób tooapply hello schematu tooall pliki w katalogu hello. W takim przypadku hello katalog zawiera pliki, które nie są zgodne hello schematu. tooprevent odzyskiwanie danych w wynikach hello, niniejszych informuje Hive czy firma Microsoft powinno zwrócić dane tylko z plików w. dziennika.

> [!NOTE]
> Jeśli oczekujesz hello zaktualizowane przez źródło zewnętrzne podstawowej toobe danych należy użyć tabel zewnętrznych. Na przykład procesu przekazywania danych lub operacja MapReduce.
>
> Usunięcie tabeli zewnętrznej jest **nie** usuwania danych hello usuwa tylko hello definicji tabeli.

toocreate **wewnętrzny** tabeli zamiast zewnętrznego, użyj następującego HiveQL hello:

    set hive.execution.engine=tez;
    CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
    STORED AS ORC;
    INSERT OVERWRITE TABLE errorLogs
    SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]';

Instrukcje te należy wykonać hello następujące akcje:

* `CREATE TABLE IF NOT EXISTS`: Jeśli hello tabela nie istnieje, należy go utworzyć. Ponieważ hello **zewnętrznych** — słowo kluczowe nie jest używany, ta instrukcja tworzy wewnętrznej tabeli. Tabela Hello są przechowywane w magazynie danych Hive hello i zarządza całkowicie Hive.

* `STORED AS ORC`: Przechowuje dane hello w formacie zoptymalizowanych pod kątem wiersza kolumnowy (ORC). ORC jest wysoce zoptymalizowane i wydajne formatu do przechowywania danych gałęzi.

* `INSERT OVERWRITE ... SELECT`: Wybiera wiersze z hello **log4jLogs** tabeli, która zawiera **[Błąd]**, a następnie hello wstawia dane do hello **errorLogs** tabeli.

> [!NOTE]
> W przeciwieństwie do tabel zewnętrznych porzucenie wewnętrznej tabeli spowoduje również usunięcie hello danych.

## <a name="improve-hive-query-performance"></a>Poprawiać wydajność zapytań Hive

### <a id="usetez"></a>Apache Tez

[Apache Tez](http://tez.apache.org) to platforma, która umożliwia aplikacjom znacznym danych, takich jak Hive, toorun wydajniej na dużą skalę. Tez jest domyślnie włączona dla klastrów usługi HDInsight opartych na systemie Linux.

> [!NOTE]
> Tez jest obecnie domyślnie wyłączona w przypadku klastrów usługi HDInsight opartej na systemie Windows, a musi być włączona. dla zapytania programu Hive, musi być ustawiona tootake zaletą aplikacji Tez, hello następujące wartości:
>
> `set hive.execution.engine=tez;`
>
> Tez jest hello domyślny aparat dla klastrów usługi HDInsight opartych na systemie Linux.

Witaj [Hive w aplikacji Tez dokumentów projektowych](https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez) zawiera szczegółowe informacje dotyczące opcji wdrażania hello i dostrajania konfiguracji.

tooaid w debugowaniu zadań została uruchomiona przy użyciu aplikacji Tez, usługa HDInsight zapewnia powitania po web UI, umożliwiających tooview szczegóły Tez zadań:

* [Użyj hello widoku Ambari Tez w HDInsight opartych na systemie Linux](hdinsight-debug-ambari-tez-view.md)

* [Użyj hello Tez interfejsu użytkownika w usłudze HDInsight z systemu Windows](hdinsight-debug-tez-ui.md)

### <a name="low-latency-analytical-processing-llap"></a>Małe opóźnienia przetwarzania analitycznego (LLAP)

[LLAP](https://cwiki.apache.org/confluence/display/Hive/LLAP) (czasami znana jako funkcja Live długich i procesów) to nowa funkcja w gałęzi 2.0, umożliwiającą buforowanie w pamięci zapytań. LLAP sprawia, że zapytań programu Hive szybciej się zbyt[26 x szybciej niż Hive 1.x w niektórych przypadkach](https://hortonworks.com/blog/announcing-apache-hive-2-1-25x-faster-queries-much/).

Usługa HDInsight zapewnia LLAP w hello interakcyjne Hive typ klastra. Aby uzyskać więcej informacji, zobacz hello [rozpoczynać interakcyjne Hive](hdinsight-hadoop-use-interactive-hive.md) dokumentu.

## <a name="hive-jobs-and-sql-server-integration-services"></a>Zadania hive i SQL Server Integration Services

Możesz użyć programu SQL Server Integration Services (SSIS) toorun zadania Hive. Hello Azure Feature Pack do SSIS zapewnia hello następujące składniki, które współpracują z zadań Hive w usłudze HDInsight.

* [Zadania Azure HDInsight Hive][hivetask]

* [Menedżer połączeń subskrypcji platformy Azure][connectionmanager]

Dowiedz się więcej o hello Azure Feature Pack SSIS [tutaj][ssispack].

## <a id="nextsteps"></a>Następne kroki

Teraz, kiedy znasz już gałąź jest i jak toouse go z platformą Hadoop w usłudze HDInsight, hello Użyj następujących łączy tooexplore toowork inne sposoby z usługą Azure HDInsight.

* [Przekazywanie danych tooHDInsight][hdinsight-upload-data]
* [Korzystanie z języka Pig z usługą HDInsight][hdinsight-use-pig]
* [Korzystanie z zadań MapReduce z usługą HDInsight][hdinsight-use-mapreduce]

[hdinsight-sdk-documentation]: http://msdnstage.redmond.corp.microsoft.com/library/dn479185.aspx

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[apache-tez]: http://tez.apache.org
[apache-hive]: http://hive.apache.org/
[apache-log4j]: http://en.wikipedia.org/wiki/Log4j
[hive-on-tez-wiki]: https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez
[import-to-excel]: http://azure.microsoft.com/documentation/articles/hdinsight-connect-excel-power-query/
[hivetask]: http://msdn.microsoft.com/library/mt146771(v=sql.120).aspx
[connectionmanager]: http://msdn.microsoft.com/library/mt146773(v=sql.120).aspx
[ssispack]: http://msdn.microsoft.com/library/mt146770(v=sql.120).aspx

[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md


[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md

[Powershell-install-configure]: /powershell/azureps-cmdlets-docs
[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx


[cindygross-hive-tables]: http://blogs.msdn.com/b/cindygross/archive/2013/02/06/hdinsight-hive-internal-and-external-tables-intro.aspx
