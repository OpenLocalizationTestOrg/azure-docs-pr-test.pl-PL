---
title: aaaUse Beeline z Apache Hive - Azure HDInsight | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toouse hello Beeline klienta toorun Hive zapytania z platformą Hadoop w usłudze HDInsight. Narzędzie do pracy z serwera HiveServer2 za pośrednictwem JDBC jest beeline."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
keywords: "gałąź beeline, beeline gałęzi"
ms.assetid: 3adfb1ba-8924-4a13-98db-10a67ab24fca
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/26/2017
ms.author: larryfr
ms.openlocfilehash: e788ff39f33d928808cfcb83a92f62ac9ae8ca09
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-beeline-client-with-apache-hive"></a>Apache Hive za pomocą klienta Beeline hello

Dowiedz się, jak toouse [Beeline](https://cwiki.apache.org/confluence/display/Hive/HiveServer2+Clients#HiveServer2Clients-Beeline–NewCommandLineShell) toorun Hive zapytania w usłudze HDInsight.

Beeline jest klientem Hive, który znajduje się na powitania głównymi węzłami klastra usługi HDInsight. Beeline używa tooHiveServer2 tooconnect JDBC, z usługą hostowaną w klastrze usługi HDInsight. Umożliwia także Beeline tooaccess Hive w usłudze HDInsight zdalnie ponad hello internet. Witaj w poniższej tabeli zawiera parametry połączenia do użycia z Beeline:

| Gdzie uruchomić Beeline z | Parametry |
| --- | --- | --- |
| SSH tooa headnode lub krawędzi węzeł połączenia | `-u 'jdbc:hive2://headnodehost:10001/;transportMode=http'` |
| Poza hello klastra | `-u 'jdbc:hive2://clustername.azurehdinsight.net:443/;ssl=true;transportMode=http;httpPath=/hive2' -n admin -p password` |

> [!NOTE]
> Zastąp `admin` z hello konto logowania klastra dla klastra.
>
> Zastąp `password` hello hasła konta logowania hello klastra.
>
> Zastąp `clustername` o nazwie hello klastra usługi HDInsight.

## <a id="prereq"></a>Wymagania wstępne

* Opartych na systemie Linux platformą Hadoop w klastrze usługi HDInsight.

  > [!IMPORTANT]
  > Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej. Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).

* Klient SSH lub lokalnego klienta Beeline. Większość hello kroków w tym dokumencie przyjęto założenie, że używasz Beeline z klastra toohello sesji SSH. Uzyskać informacji o działaniu Beeline z zewnątrz hello klastra, zobacz hello [zdalnie użyć Beeline](#remote) sekcji.

    Aby uzyskać więcej informacji o korzystaniu z protokołu SSH, zobacz [używanie SSH z usługą HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

## <a id="beeline"></a>Użyj Beeline

1. Podczas uruchamiania Beeline, musisz podać parametry połączenia dla serwera HiveServer2 w klastrze usługi HDInsight. polecenie hello toorun z zewnątrz hello klastra, musisz także podać nazwę konta logowania klastra hello (domyślna `admin`) i hasło. Należy użyć następującej tabeli toofind hello połączenia ciągu formatu i parametry toouse hello:

    | Gdzie uruchomić Beeline z | Parametry |
    | --- | --- | --- |
    | SSH tooa headnode lub krawędzi węzeł połączenia | `-u 'jdbc:hive2://headnodehost:10001/;transportMode=http'` |
    | Poza hello klastra | `-u 'jdbc:hive2://clustername.azurehdinsight.net:443/;ssl=true;transportMode=http;httpPath=/hive2' -n admin -p password` |

    Na przykład hello następujące polecenia mogą być używane toostart Beeline z klastra toohello sesji SSH:

    ```bash
    beeline -u 'jdbc:hive2://headnodehost:10001/;transportMode=http'
    ```

    To polecenie uruchamia powitania klienta Beeline i łączy tooHiveServer2 na powitania węzła głównego klastra. Po zakończeniu wykonywania polecenia hello przyjeździe `jdbc:hive2://headnodehost:10001/>` wiersza.

2. Polecenia beeline rozpoczynać się od `!` znaków, na przykład `!help` Wyświetla Pomoc. Jednak hello `!` można pominąć w przypadku niektórych poleceń. Na przykład `help` działa.

    Brak `!sql`, która jest używana tooexecute instrukcje HiveQL. Jednak HiveQL używa się tak najczęściej pominąć hello poprzedniego `!sql`. następujące dwie instrukcje Hello są równoważne:

    ```hiveql
    !sql show tables;
    show tables;
    ```

    W nowym klastrze, znajduje się tylko jedną tabelę: **hivesampletable**.

3. Użyj następującego polecenia toodisplay hello schematu dla hello hivesampletable hello:

    ```hiveql
    describe hivesampletable;
    ```

    To polecenie zwraca hello następujących informacji:

        +-----------------------+------------+----------+--+
        |       col_name        | data_type  | comment  |
        +-----------------------+------------+----------+--+
        | clientid              | string     |          |
        | querytime             | string     |          |
        | market                | string     |          |
        | deviceplatform        | string     |          |
        | devicemake            | string     |          |
        | devicemodel           | string     |          |
        | state                 | string     |          |
        | country               | string     |          |
        | querydwelltime        | double     |          |
        | sessionid             | bigint     |          |
        | sessionpagevieworder  | bigint     |          |
        +-----------------------+------------+----------+--+

    Te informacje w tym artykule opisano hello kolumn w tabeli hello. Gdy można wykonać niektóre zapytań dotyczących tych danych, zamiast tego utwórz nowy toodemonstrate tabeli jak tooload danych do gałęzi i zastosowanie schematu.

4. Wprowadź następujące instrukcje toocreate tabela o nazwie hello **log4jLogs** przy użyciu dostarczonych z klastrem usługi HDInsight hello przykładowych danych:

    ```hiveql
    DROP TABLE log4jLogs;
    CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
    STORED AS TEXTFILE LOCATION 'wasb:///example/data/';
    SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;
    ```

    Instrukcje te należy wykonać hello następujące akcje:

    * `DROP TABLE`— W przypadku hello tabela istnieje, zostaną usunięte.

    * `CREATE EXTERNAL TABLE`-Tworzy **zewnętrznych** tabeli w gałęzi rejestru. Tabele zewnętrzne przechowywać tylko hello definicji tabeli w gałęzi. Hello danych pozostaje w hello oryginalnej lokalizacji.

    * `ROW FORMAT`— Sposób formatowania danych hello. W takim przypadku hello pól w każdym dzienniku są oddzielone spacją.

    * `STORED AS TEXTFILE LOCATION`— W przypadku gdy hello dane są przechowywane i w jaki format pliku.

    * `SELECT`-Wybiera liczbę wszystkich wierszy gdzie kolumna **t4** zawiera wartość hello **[Błąd]**. To zapytanie zwraca wartość **3** są trzy wiersze, które zawierają tę wartość.

    * `INPUT__FILE__NAME LIKE '%.log'`-Hive prób tooapply hello schematu tooall pliki w katalogu hello. W takim przypadku hello katalog zawiera pliki, które nie są zgodne hello schematu. tooprevent odzyskiwanie danych w wynikach hello, niniejszych informuje Hive czy firma Microsoft powinno zwrócić dane tylko z plików w. dziennika.

  > [!NOTE]
  > Jeśli oczekujesz hello zaktualizowane przez źródło zewnętrzne podstawowej toobe danych należy użyć tabel zewnętrznych. Na przykład procesu przekazywania danych lub operacja MapReduce.
  >
  > Usunięcie tabeli zewnętrznej jest **nie** usunąć dane hello, tylko hello definicji tabeli.

    Witaj danych wyjściowych tego polecenia jest podobne toohello następującego tekstu:

        INFO  : Tez session hasn't been created yet. Opening session
        INFO  :

        INFO  : Status: Running (Executing on YARN cluster with App id application_1443698635933_0001)

        INFO  : Map 1: -/-      Reducer 2: 0/1
        INFO  : Map 1: 0/1      Reducer 2: 0/1
        INFO  : Map 1: 0/1      Reducer 2: 0/1
        INFO  : Map 1: 0/1      Reducer 2: 0/1
        INFO  : Map 1: 0/1      Reducer 2: 0/1
        INFO  : Map 1: 0(+1)/1  Reducer 2: 0/1
        INFO  : Map 1: 0(+1)/1  Reducer 2: 0/1
        INFO  : Map 1: 1/1      Reducer 2: 0/1
        INFO  : Map 1: 1/1      Reducer 2: 0(+1)/1
        INFO  : Map 1: 1/1      Reducer 2: 1/1
        +----------+--------+--+
        |   sev    | count  |
        +----------+--------+--+
        | [ERROR]  | 3      |
        +----------+--------+--+
        1 row selected (47.351 seconds)

5. Użyj tooexit Beeline, `!exit`.

## <a id="file"></a>Użyj toorun Beeline pliku HiveQL

Użyj hello następujące kroki toocreate pliku, i uruchom go za pomocą Beeline.

1. Użyj hello następujące polecenie toocreate plik o nazwie **query.hql**:

    ```bash
    nano query.hql
    ```

2. Użyj następującego tekstu jako hello zawartość pliku hello hello. To zapytanie tworzy nową tabelę "internal" o nazwie **errorLogs**:

    ```hiveql
    CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) STORED AS ORC;
    INSERT OVERWRITE TABLE errorLogs SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log';
    ```

    Instrukcje te należy wykonać hello następujące akcje:

    * **Utwórz Tabela Jeśli nie ISTNIEJE** — Jeśli tabeli hello jeszcze nie istnieje, jest tworzony. Ponieważ hello **zewnętrznych** — słowo kluczowe nie jest używany, ta instrukcja tworzy wewnętrznej tabeli. Wewnętrzny tabele są przechowywane w magazynie danych hello Hive i całkowicie zarządza Hive.
    * **ORC AS PRZECHOWYWANE** -przechowuje dane hello w formacie zoptymalizowanych pod kątem wiersza kolumnowy (ORC). ORC format jest wysoce zoptymalizowane i wydajne formatu do przechowywania danych Hive.
    * **ZASTĄP INSERT... Wybierz** -wybiera wiersze z hello **log4jLogs** tabeli, która zawiera **[Błąd]**, a następnie wstawia hello danych do hello **errorLogs** tabeli.

    > [!NOTE]
    > W przeciwieństwie do tabel zewnętrznych porzucenie wewnętrznej tabeli usuwa hello również danych źródłowych.

3. toosave hello pliku, użyj **Ctrl**+**_X**, wprowadź **Y**, a na końcu **Enter**.

4. Użyj następującego pliku hello toorun przy użyciu Beeline hello:

    ```bash
    beeline -u 'jdbc:hive2://headnodehost:10001/;transportMode=http' -i query.hql
    ```

    > [!NOTE]
    > Witaj `-i` parametru rozpoczyna Beeline, uruchamia hello instrukcje w pliku query.hql hello. Po wykonaniu kwerendy hello przyjeździe hello `jdbc:hive2://headnodehost:10001/>` wiersza. Można również uruchomić plik za pomocą hello `-f` parametr, który zamyka Beeline po zakończeniu hello zapytania.

5. tooverify, który hello **errorLogs** tabela została utworzona, użyj powitania po instrukcji tooreturn hello wszystkie wiersze z **errorLogs**:

    ```hiveql
    SELECT * from errorLogs;
    ```

    Trzy wiersze danych ma zostać zwrócony, zawierający wszystkie **[Błąd]** w kolumnie t4:

        +---------------+---------------+---------------+---------------+---------------+---------------+---------------+--+
        | errorlogs.t1  | errorlogs.t2  | errorlogs.t3  | errorlogs.t4  | errorlogs.t5  | errorlogs.t6  | errorlogs.t7  |
        +---------------+---------------+---------------+---------------+---------------+---------------+---------------+--+
        | 2012-02-03    | 18:35:34      | SampleClass0  | [ERROR]       | incorrect     | id            |               |
        | 2012-02-03    | 18:55:54      | SampleClass1  | [ERROR]       | incorrect     | id            |               |
        | 2012-02-03    | 19:25:27      | SampleClass4  | [ERROR]       | incorrect     | id            |               |
        +---------------+---------------+---------------+---------------+---------------+---------------+---------------+--+
        3 rows selected (1.538 seconds)

## <a id="remote"></a>Użyj Beeline zdalnie

Jeśli masz Beeline zainstalowane lokalnie lub jest ona używana przez obraz Docker takich jak [sutoiku/beeline](https://hub.docker.com/r/sutoiku/beeline/), należy użyć hello następujące parametry:

* __Parametry połączenia__:`-u 'jdbc:hive2://clustername.azurehdinsight.net:443/;ssl=true;transportMode=http;httpPath=/hive2'`

* __Nazwa logowania klastra__:`-n admin`

* __Hasło logowania klastra__`-p 'password'`

Zastąp hello `clustername` w parametrach połączenia hello o nazwie hello klastra usługi HDInsight.

Zastąp `admin` o nazwie hello logowania do klastra i Zastąp `password` z hello hasło do logowania do klastra.

## <a id="sparksql"></a>Beeline za pomocą Spark

Platforma Spark zawiera własną implementację serwera HiveServer2, które są często serwera Spark Thrift hello tooas określonej. Ta usługa korzysta z zapytań Spark SQL tooresolve zamiast Hive i może zapewnić lepszą wydajność, w zależności od tego zapytania.

serwera Spark Thrift toohello tooconnect platformy Spark w klastrze usługi HDInsight, używać portów `10002` zamiast `10001`. Na przykład `beeline -u 'jdbc:hive2://headnodehost:10002/;transportMode=http'`.

> [!IMPORTANT]
> serwera Spark Thrift Hello jest nie bezpośrednio dostępny przez hello internet. Można połączyć tooit w sesji SSH lub tylko wewnątrz hello tej samej sieci wirtualnej Azure, jak hello klastra usługi HDInsight.

## <a id="summary"></a><a id="nextsteps"></a>Następne kroki

Bardziej ogólne informacje na temat Hive w usłudze HDInsight zobacz następujące dokumentu hello:

* [Korzystanie z programu Hive z usługą Hadoop w usłudze HDInsight](hdinsight-use-hive.md)

Aby uzyskać więcej informacji na temat innych sposobów może pracować z platformą Hadoop w usłudze HDInsight, zobacz powitania po dokumentów:

* [Korzystanie z języka Pig z usługą Hadoop w usłudze HDInsight](hdinsight-use-pig.md)
* [Używanie MapReduce z usługą Hadoop w usłudze HDInsight](hdinsight-use-mapreduce.md)

Jeśli używasz aplikacji Tez przy użyciu Hive, zobacz powitania po dokumentów:

* [Użyj hello Tez interfejsu użytkownika w usłudze HDInsight z systemu Windows](hdinsight-debug-tez-ui.md)
* [Użyj hello widoku Ambari Tez w HDInsight opartych na systemie Linux](hdinsight-debug-ambari-tez-view.md)

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

[putty]: http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html


[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md


[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx
