---
title: "Analizowanie danych opóźnienie transmitowane przy użyciu Hive w usłudze HDInsight - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak korzystanie z programu Hive można analizować dane transmitowane w HDInsight opartych na systemie Linux, a następnie wyeksportować dane do bazy danych SQL przy użyciu Sqoop."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 0c23a079-981a-4079-b3f7-ad147b4609e5
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: 8cdc19ac8a517b6d8eefabb5476a686aa252a332
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="analyze-flight-delay-data-by-using-hive-on-linux-based-hdinsight"></a>Analizowanie danych opóźnienie transmitowane przy użyciu usługi Hive w usłudze HDInsight z systemem Linux

Dowiedz się, jak i analizować dane opóźnienie transmitowane przy użyciu Hive w usłudze HDInsight z systemem Linux, a następnie wyeksportować dane do bazy danych SQL Azure przy użyciu Sqoop.

> [!IMPORTANT]
> Kroki opisane w tym dokumencie wymagają klastra usługi HDInsight, który używa systemu Linux. Linux jest jedynym systemem operacyjnym używanym w połączeniu z usługą HDInsight w wersji 3.4 lub nowszą. Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).

### <a name="prerequisites"></a>Wymagania wstępne

* **Klaster usługi HDInsight**. Zobacz [rozpocząć korzystanie z usługi Hadoop przy użyciu Hive w usłudze HDInsight w systemie Linux](hdinsight-hadoop-linux-tutorial-get-started.md) instrukcje dotyczące tworzenia nowego klastra usługi HDInsight opartej na systemie Linux.

* **Baza danych Azure SQL**. Korzystasz z bazy danych Azure SQL jako miejsce docelowe magazynu danych. Jeśli nie masz już bazę danych SQL, zobacz [samouczek usługi SQL Database: tworzenie bazy danych SQL w minutach](../sql-database/sql-database-get-started.md).

* **Interfejs wiersza polecenia platformy Azure**. Jeśli nie zainstalowano wiersza polecenia platformy Azure, zobacz [Instalowanie i Konfigurowanie interfejsu wiersza polecenia Azure](../cli-install-nodejs.md) dla większej liczby kroków.

## <a name="download-the-flight-data"></a>Pobierz dane transmitowane

1. Przejdź do [badań i Nowatorska technologia administracji, biura statystyk transportu][rita-website].

2. Na stronie wybierz następujące wartości:

   | Nazwa | Wartość |
   | --- | --- |
   | Filtr roku |2013 |
   | Filtruj okres |Stycznia |
   | Pola |Rok, FlightDate, UniqueCarrier, operatora, FlightNum, OriginAirportID, pochodzenia, OriginCityName, OriginState, DestAirportID, Dest, DestCityName, DestState, DepDelayMinutes, ArrDelay, ArrDelayMinutes, CarrierDelay, WeatherDelay, NASDelay, SecurityDelay, LateAircraftDelay. Usuń zaznaczenie wszystkich innych pól |

3. Kliknij pozycję **Pobierz**.

## <a name="upload-the-data"></a>Przekazywanie danych

1. Użyj następującego polecenia, aby przekazać plik zip do węzła głównego klastra usługi HDInsight:

    ```
    scp FILENAME.zip USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:
    ```

    Zastąp **FILENAME** z nazwą pliku zip. Zastąp **USERNAME** z logowaniem SSH dla klastra usługi HDInsight. Zamień NAZWAKLASTRA nazwę klastra usługi HDInsight.

   > [!NOTE]
   > Jeśli używasz hasła uwierzytelniania nazwy logowania SSH, zostanie wyświetlony monit o hasło. Jeśli używasz klucza publicznego, może być konieczne użycie `-i` parametru i określ ścieżkę do odpowiedniego klucza prywatnego. Na przykład `scp -i ~/.ssh/id_rsa FILENAME.zip USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:`.

2. Po zakończeniu przekazywania nawiązać połączenia z klastrem przy użyciu protokołu SSH:

    ```ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net```

    Aby uzyskać więcej informacji, zobacz [Używanie protokołu SSH w usłudze HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

3. Po nawiązaniu połączenia, Rozpakuj plik zip należy wykonać następujące kroki:

    ```
    unzip FILENAME.zip
    ```

    To polecenie wyodrębnia plik CSV, który jest około 60 MB.

4. Użyj następującego polecenia, aby utworzyć katalog w magazynie usługi HDInsight, a następnie skopiuj plik do katalogu:

    ```
    hdfs dfs -mkdir -p /tutorials/flightdelays/data
    hdfs dfs -put FILENAME.csv /tutorials/flightdelays/data/
    ```

## <a name="create-and-run-the-hiveql"></a>Tworzenie i uruchamianie HiveQL

Wykonaj następujące kroki, aby zaimportować dane z pliku CSV do tabeli programu Hive o nazwie **opóźnienia**.

1. Użyj następującego polecenia można tworzyć i edytować nowy plik o nazwie **flightdelays.hql**:

    ```
    nano flightdelays.hql
    ```

    Zawartość tego pliku, należy użyć następującego tekstu:

    ```hiveql
    DROP TABLE delays_raw;
    -- Creates an external table over the csv file
    CREATE EXTERNAL TABLE delays_raw (
        YEAR string,
        FL_DATE string,
        UNIQUE_CARRIER string,
        CARRIER string,
        FL_NUM string,
        ORIGIN_AIRPORT_ID string,
        ORIGIN string,
        ORIGIN_CITY_NAME string,
        ORIGIN_CITY_NAME_TEMP string,
        ORIGIN_STATE_ABR string,
        DEST_AIRPORT_ID string,
        DEST string,
        DEST_CITY_NAME string,
        DEST_CITY_NAME_TEMP string,
        DEST_STATE_ABR string,
        DEP_DELAY_NEW float,
        ARR_DELAY_NEW float,
        CARRIER_DELAY float,
        WEATHER_DELAY float,
        NAS_DELAY float,
        SECURITY_DELAY float,
        LATE_AIRCRAFT_DELAY float)
    -- The following lines describe the format and location of the file
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ','
    LINES TERMINATED BY '\n'
    STORED AS TEXTFILE
    LOCATION '/tutorials/flightdelays/data';

    -- Drop the delays table if it exists
    DROP TABLE delays;
    -- Create the delays table and populate it with data
    -- pulled in from the CSV file (via the external table defined previously)
    CREATE TABLE delays AS
    SELECT YEAR AS year,
        FL_DATE AS flight_date,
        substring(UNIQUE_CARRIER, 2, length(UNIQUE_CARRIER) -1) AS unique_carrier,
        substring(CARRIER, 2, length(CARRIER) -1) AS carrier,
        substring(FL_NUM, 2, length(FL_NUM) -1) AS flight_num,
        ORIGIN_AIRPORT_ID AS origin_airport_id,
        substring(ORIGIN, 2, length(ORIGIN) -1) AS origin_airport_code,
        substring(ORIGIN_CITY_NAME, 2) AS origin_city_name,
        substring(ORIGIN_STATE_ABR, 2, length(ORIGIN_STATE_ABR) -1)  AS origin_state_abr,
        DEST_AIRPORT_ID AS dest_airport_id,
        substring(DEST, 2, length(DEST) -1) AS dest_airport_code,
        substring(DEST_CITY_NAME,2) AS dest_city_name,
        substring(DEST_STATE_ABR, 2, length(DEST_STATE_ABR) -1) AS dest_state_abr,
        DEP_DELAY_NEW AS dep_delay_new,
        ARR_DELAY_NEW AS arr_delay_new,
        CARRIER_DELAY AS carrier_delay,
        WEATHER_DELAY AS weather_delay,
        NAS_DELAY AS nas_delay,
        SECURITY_DELAY AS security_delay,
        LATE_AIRCRAFT_DELAY AS late_aircraft_delay
    FROM delays_raw;
    ```

2. Aby zapisać plik, użyj **Ctrl + X**, następnie **Y** .

3. Aby uruchomić Hive i przeprowadzić **flightdelays.hql** plików, użyj następującego polecenia:

    ```
    beeline -u 'jdbc:hive2://localhost:10001/;transportMode=http' -f flightdelays.hql
    ```

   > [!NOTE]
   > W tym przykładzie `localhost` służy Skoro masz połączenie z węzłem głównym klastra usługi HDInsight, czyli gdzie działa serwera HiveServer2.

4. Raz __flightdelays.hql__ zakończeniu uruchamiania skryptu, użyj następującego polecenia, aby otworzyć sesji interaktywnej Beeline:

    ```
    beeline -u 'jdbc:hive2://localhost:10001/;transportMode=http'
    ```

5. Po otrzymaniu `jdbc:hive2://localhost:10001/>` monit, użyj następującego zapytania do pobierania danych z transmitowane importowanych danych opóźnienia.

    ```hiveql
    INSERT OVERWRITE DIRECTORY '/tutorials/flightdelays/output'
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    SELECT regexp_replace(origin_city_name, '''', ''),
        avg(weather_delay)
    FROM delays
    WHERE weather_delay IS NOT NULL
    GROUP BY origin_city_name;
    ```

    To zapytanie pobiera listę miast, w których wystąpił pogody opóźnienia, oraz średnie opóźnienie czasu i zapisać go do `/tutorials/flightdelays/output`. Później Sqoop odczytuje dane z tej lokalizacji i eksportowania ich do bazy danych SQL Azure.

6. Aby zakończyć Beeline, wprowadź `!quit` w wierszu.

## <a name="create-a-sql-database"></a>Tworzenie bazy danych SQL

Jeśli masz już bazę danych SQL, należy uzyskać nazwę serwera. Można znaleźć nazwę serwera w [portalu Azure](https://portal.azure.com) wybierając **baz danych**i filtrowanie Nazwa bazy danych chcesz użyć. Nazwa serwera ma na liście **serwera** kolumny.

Jeśli nie masz już bazę danych SQL, skorzystaj z informacji w [samouczek usługi SQL Database: tworzenie bazy danych SQL w minutach](../sql-database/sql-database-get-started.md) go utworzyć. Zapisz nazwę serwera, do bazy danych.

## <a name="create-a-sql-database-table"></a>Tworzenie tabeli bazy danych SQL

> [!NOTE]
> Istnieje wiele sposobów łączenia z bazą danych SQL i tworzenie tabeli. Następujące kroki użyj [protokół FreeTDS](http://www.freetds.org/) z klastrem usługi HDInsight.


1. Połącz się z klastrem usługi HDInsight opartej na systemie Linux przy użyciu protokołu SSH, a wykonanie następujących kroków w sesji SSH.

2. Aby zainstalować protokół FreeTDS, użyj następującego polecenia:

    ```
    sudo apt-get --assume-yes install freetds-dev freetds-bin
    ```

3. Po zakończeniu instalacji, użyj następującego polecenia, aby połączyć się z serwerem bazy danych SQL. Zastąp **serverName** z nazwą serwera bazy danych SQL. Zastąp **adminLogin** i **adminPassword** z nazwy logowania bazy danych SQL. Zastąp **databaseName** o nazwie bazy danych.

    ```
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P <adminPassword> -p 1433 -D <databaseName>
    ```

    Pojawi się dane wyjściowe podobne do następującego tekstu:

    ```
    locale is "en_US.UTF-8"
    locale charset is "UTF-8"
    using default charset "UTF-8"
    Default database being set to sqooptest
    1>
    ```

4. W `1>` monit, wprowadź następujące wiersze:

    ```
    CREATE TABLE [dbo].[delays](
    [origin_city_name] [nvarchar](50) NOT NULL,
    [weather_delay] float,
    CONSTRAINT [PK_delays] PRIMARY KEY CLUSTERED   
    ([origin_city_name] ASC))
    GO
    ```

    Gdy `GO` instrukcja została wprowadzona, poprzednie instrukcje są oceniane. To zapytanie tworzy tabelę o nazwie **opóźnienia**, z indeksem klastrowanym.

    Użyj następującego zapytania, aby sprawdzić, czy tabela została utworzona:

    ```
    SELECT * FROM information_schema.tables
    GO
    ```

    Dane wyjściowe będą podobne do następującego tekstu:

    ```
    TABLE_CATALOG   TABLE_SCHEMA    TABLE_NAME      TABLE_TYPE
    databaseName       dbo     delays      BASE TABLE
    ```

5. Wprowadź `exit` na `1>` prompt wyjść z narzędzia tsql.

## <a name="export-data-with-sqoop"></a>Eksportowanie danych z Sqoop

1. Aby sprawdzić, czy Sqoop widzą bazy danych SQL, użyj następującego polecenia:

    ```
    sqoop list-databases --connect jdbc:sqlserver://<serverName>.database.windows.net:1433 --username <adminLogin> --password <adminPassword>
    ```

    To polecenie zwraca listę baz danych, łącznie z bazy danych utworzone wcześniej tabeli opóźnienia.

2. Eksportowanie danych z hivesampletable do tabeli mobiledata, użyj następującego polecenia:

    ```
    sqoop export --connect 'jdbc:sqlserver://<serverName>.database.windows.net:1433;database=<databaseName>' --username <adminLogin> --password <adminPassword> --table 'delays' --export-dir '/tutorials/flightdelays/output' --fields-terminated-by '\t' -m 1
    ```

    Sqoop nawiązuje połączenie z bazą danych zawierającą tabeli opóźnienia i eksportowanie danych `/tutorials/flightdelays/output` katalogu do tabeli opóźnienia.

3. Po zakończeniu wykonywania polecenia, użyj następujących funkcji do łączenia z bazą danych przy użyciu języka TSQL:

    ```
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P <adminPassword> -p 1433 -D <databaseName>
    ```

    Po nawiązaniu połączenia, należy zastosować następujące instrukcje, aby sprawdzić, czy dane zostały wyeksportowane do tabeli mobiledata:

    ```
    SELECT * FROM delays
    GO
    ```

    Powinna zostać wyświetlona lista danych w tabeli. Typ `exit` aby wyjść z narzędzia tsql.

## <a id="nextsteps"></a> Następne kroki

Aby dowiedzieć się więcej sposobów pracować z danymi w usłudze HDInsight, można znaleźć w następujących dokumentach:

* [Korzystanie z programu Hive z usługą HDInsight][hdinsight-use-hive]
* [Korzystanie z Oozie z usługą HDInsight][hdinsight-use-oozie]
* [Korzystanie z usługą HDInsight Sqoop][hdinsight-use-sqoop]
* [Korzystanie z języka Pig z usługą HDInsight][hdinsight-use-pig]
* [Tworzenie programów Java MapReduce dla usługi HDInsight][hdinsight-develop-mapreduce]
* [Opracowywanie przesyłanie strumieniowe programów dla usługi HDInsight Hadoop języka Python][hdinsight-develop-streaming]

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/


[rita-website]: http://www.transtats.bts.gov/DL_SelectFields.asp?Table_ID=236&DB_Short_Name=On-Time
[cindygross-hive-tables]: http://blogs.msdn.com/b/cindygross/archive/2013/02/06/hdinsight-hive-internal-and-external-tables-intro.aspx

[hdinsight-use-oozie]: hdinsight-use-oozie-linux-mac.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-use-sqoop]: hdinsight-use-sqoop-mac-linux.md
[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-develop-streaming]: hdinsight-hadoop-streaming-python.md
[hdinsight-develop-mapreduce]: hdinsight-develop-deploy-java-mapreduce-linux.md

[hadoop-hiveql]: https://cwiki.apache.org/confluence/display/Hive/LanguageManual+DDL

[technetwiki-hive-error]: http://social.technet.microsoft.com/wiki/contents/articles/23047.hdinsight-hive-error-unable-to-rename.aspx
