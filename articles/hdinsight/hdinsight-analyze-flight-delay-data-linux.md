---
title: "aaaAnalyze transmitowane opóźnienie danych przy użyciu Hive w usłudze HDInsight - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse Hive dane transmitowane tooanalyze na HDInsight opartych na systemie Linux, a następnie wyeksportować hello tooSQL danych bazy danych przy użyciu Sqoop."
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
ms.openlocfilehash: 7830457a7100880dff1c647dde1b4d203bfea3c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-flight-delay-data-by-using-hive-on-linux-based-hdinsight"></a>Analizowanie danych opóźnienie transmitowane przy użyciu usługi Hive w usłudze HDInsight z systemem Linux

Dowiedz się, jak tooanalyze transmitowane opóźnienie danych przy użyciu Hive w usłudze HDInsight z systemem Linux następnie wyeksportować hello tooAzure danych bazy danych SQL przy użyciu Sqoop.

> [!IMPORTANT]
> kroki Hello w tym dokumencie wymagają klastra usługi HDInsight, który używa systemu Linux. Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej. Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).

### <a name="prerequisites"></a>Wymagania wstępne

* **Klaster usługi HDInsight**. Zobacz [rozpocząć korzystanie z usługi Hadoop przy użyciu Hive w usłudze HDInsight w systemie Linux](hdinsight-hadoop-linux-tutorial-get-started.md) instrukcje dotyczące tworzenia nowego klastra usługi HDInsight opartej na systemie Linux.

* **Usługa Azure SQL Database**. Korzystasz z bazy danych Azure SQL jako miejsce docelowe magazynu danych. Jeśli nie masz już bazę danych SQL, zobacz [samouczek usługi SQL Database: tworzenie bazy danych SQL w minutach](../sql-database/sql-database-get-started.md).

* **Interfejs wiersza polecenia platformy Azure**. Jeśli nie zainstalowano hello wiersza polecenia platformy Azure, zobacz [Instalowanie i Konfigurowanie interfejsu wiersza polecenia Azure hello](../cli-install-nodejs.md) dla większej liczby kroków.

## <a name="download-hello-flight-data"></a>Pobierz dane transmitowane hello

1. Przeglądaj zbyt[badań i innowacyjnych technologii administracji, biura statystyk transportu][rita-website].

2. Na stronie powitania wybierz hello następujące wartości:

   | Nazwa | Wartość |
   | --- | --- |
   | Filtr roku |2013 |
   | Filtruj okres |Stycznia |
   | Pola |Rok, FlightDate, UniqueCarrier, operatora, FlightNum, OriginAirportID, pochodzenia, OriginCityName, OriginState, DestAirportID, Dest, DestCityName, DestState, DepDelayMinutes, ArrDelay, ArrDelayMinutes, CarrierDelay, WeatherDelay, NASDelay, SecurityDelay, LateAircraftDelay. Usuń zaznaczenie wszystkich innych pól |

3. Kliknij pozycję **Pobierz**.

## <a name="upload-hello-data"></a>Przekazywanie danych hello

1. Użyj następującego polecenia tooupload hello zip pliku toohello HDInsight węzła głównego klastra hello:

    ```
    scp FILENAME.zip USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:
    ```

    Zastąp **FILENAME** o nazwie hello hello pliku zip. Zastąp **USERNAME** z logowaniem SSH hello hello klastra usługi HDInsight. Zamień NAZWAKLASTRA hello nazwę hello klastra usługi HDInsight.

   > [!NOTE]
   > Jeśli używasz tooauthenticate hasło logowanie SSH, zostanie wyświetlony monit o hasło hello. Jeśli używasz klucza publicznego, może być konieczne toouse hello `-i` parametru i określ toohello ścieżka hello pasujących do klucza prywatnego. Na przykład `scp -i ~/.ssh/id_rsa FILENAME.zip USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:`.

2. Po zakończeniu przekazywania hello połączenie toohello klastra przy użyciu protokołu SSH:

    ```ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net```

    Aby uzyskać więcej informacji, zobacz [Używanie protokołu SSH w usłudze HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

3. Po nawiązaniu połączenia użyj następującego pliku .zip hello toounzip hello:

    ```
    unzip FILENAME.zip
    ```

    To polecenie wyodrębnia plik CSV, który jest około 60 MB.

4. Użyj hello następujące polecenia toocreate katalogu w magazynie usługi HDInsight, a następnie skopiuj katalog toohello pliku hello:

    ```
    hdfs dfs -mkdir -p /tutorials/flightdelays/data
    hdfs dfs -put FILENAME.csv /tutorials/flightdelays/data/
    ```

## <a name="create-and-run-hello-hiveql"></a>Tworzenie i uruchamianie hello HiveQL

Użyj następujących hello kroki tooimport danych z pliku CSV hello w tabeli programu Hive o nazwie **opóźnienia**.

1. Użyj następujących hello polecenia toocreate i Edytuj plik o nazwie **flightdelays.hql**:

    ```
    nano flightdelays.hql
    ```

    Użyj hello następującego tekstu jako hello zawartość tego pliku:

    ```hiveql
    DROP TABLE delays_raw;
    -- Creates an external table over hello csv file
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
    -- hello following lines describe hello format and location of hello file
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ','
    LINES TERMINATED BY '\n'
    STORED AS TEXTFILE
    LOCATION '/tutorials/flightdelays/data';

    -- Drop hello delays table if it exists
    DROP TABLE delays;
    -- Create hello delays table and populate it with data
    -- pulled in from hello CSV file (via hello external table defined previously)
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

2. toosave hello pliku, użyj **Ctrl + X**, następnie **Y** .

3. toostart Hive i wykonywania hello **flightdelays.hql** plików, użyj następującego polecenia hello:

    ```
    beeline -u 'jdbc:hive2://localhost:10001/;transportMode=http' -f flightdelays.hql
    ```

   > [!NOTE]
   > W tym przykładzie `localhost` jest używany, ponieważ są połączone toohello węzła głównego klastra usługi HDInsight hello, czyli gdzie działa serwera HiveServer2.

4. Raz hello __flightdelays.hql__ skrypt uruchomiony zakończeniu Użyj hello następujące polecenie tooopen jako sesja interaktywna Beeline:

    ```
    beeline -u 'jdbc:hive2://localhost:10001/;transportMode=http'
    ```

5. Po otrzymaniu hello `jdbc:hive2://localhost:10001/>` monit, użyj hello poniższych zapytania tooretrieve danych z danych opóźnienie transmitowane hello zaimportowane.

    ```hiveql
    INSERT OVERWRITE DIRECTORY '/tutorials/flightdelays/output'
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    SELECT regexp_replace(origin_city_name, '''', ''),
        avg(weather_delay)
    FROM delays
    WHERE weather_delay IS NOT NULL
    GROUP BY origin_city_name;
    ```

    To zapytanie pobiera listę miejscowości opóźnienia doświadczonym pogodzie, wraz ze średnią hello opóźnienie czasu i zapisać go za`/tutorials/flightdelays/output`. Później Sqoop odczytuje hello danych z tej lokalizacji i wyeksportować go tooAzure bazy danych SQL.

6. Wprowadź tooexit Beeline, `!quit` hello w wierszu.

## <a name="create-a-sql-database"></a>Tworzenie bazy danych SQL

Jeśli masz już bazę danych SQL, należy uzyskać hello nazwy serwera. Hello nazwy serwera można znaleźć w hello [portalu Azure](https://portal.azure.com) wybierając **baz danych**, i filtrowanie hello hello nazwę bazy danych należy ma toouse. Nazwa serwera Hello ma na liście hello **serwera** kolumny.

Jeśli nie masz już bazę danych SQL, użyj informacji hello w [samouczek usługi SQL Database: tworzenie bazy danych SQL w minutach](../sql-database/sql-database-get-started.md) toocreate jeden. Zapisz nazwę serwera hello do hello bazy danych.

## <a name="create-a-sql-database-table"></a>Tworzenie tabeli bazy danych SQL

> [!NOTE]
> Istnieje wiele sposobów tooSQL tooconnect bazy danych i Utwórz tabelę. Witaj, użyj czynności po [protokół FreeTDS](http://www.freetds.org/) z klastrem usługi HDInsight hello.


1. Użyj SSH tooconnect toohello opartych na systemie Linux klaster usługi HDInsight i uruchamiania hello następujące kroki w sesji SSH hello.

2. Użyj następującego polecenia tooinstall protokół FreeTDS hello:

    ```
    sudo apt-get --assume-yes install freetds-dev freetds-bin
    ```

3. Po zakończeniu instalacji hello Użyj hello następujące polecenia tooconnect toohello bazy danych programu SQL server. Zastąp **serverName** z nazwą serwera bazy danych SQL hello. Zastąp **adminLogin** i **adminPassword** z logowaniem hello bazy danych SQL. Zastąp **databaseName** hello nazwą bazy danych.

    ```
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P <adminPassword> -p 1433 -D <databaseName>
    ```

    Pojawi się toohello podobne dane wyjściowe następującego tekstu:

    ```
    locale is "en_US.UTF-8"
    locale charset is "UTF-8"
    using default charset "UTF-8"
    Default database being set toosqooptest
    1>
    ```

4. Na powitania `1>` monit, wprowadź hello następujące wiersze:

    ```
    CREATE TABLE [dbo].[delays](
    [origin_city_name] [nvarchar](50) NOT NULL,
    [weather_delay] float,
    CONSTRAINT [PK_delays] PRIMARY KEY CLUSTERED   
    ([origin_city_name] ASC))
    GO
    ```

    Gdy hello `GO` instrukcja została wprowadzona, poprzednie instrukcje hello są oceniane. To zapytanie tworzy tabelę o nazwie **opóźnienia**, z indeksem klastrowanym.

    Utworzono hello Użyj następującego tooverify zapytania, który hello tabeli:

    ```
    SELECT * FROM information_schema.tables
    GO
    ```

    Witaj danych wyjściowych jest podobne toohello następującego tekstu:

    ```
    TABLE_CATALOG   TABLE_SCHEMA    TABLE_NAME      TABLE_TYPE
    databaseName       dbo     delays      BASE TABLE
    ```

5. Wprowadź `exit` na powitania `1>` Monituj tooexit hello tsql narzędzia.

## <a name="export-data-with-sqoop"></a>Eksportowanie danych z Sqoop

1. Użyj hello następujące polecenie tooverify czy Sqoop widzą bazy danych SQL:

    ```
    sqoop list-databases --connect jdbc:sqlserver://<serverName>.database.windows.net:1433 --username <adminLogin> --password <adminPassword>
    ```

    To polecenie zwraca listę baz danych, w tym hello bazy danych, utworzone wcześniej hello tabeli opóźnień w.

2. Użyj następującego polecenia tooexport danych z tabeli mobiledata toohello hivesampletable hello:

    ```
    sqoop export --connect 'jdbc:sqlserver://<serverName>.database.windows.net:1433;database=<databaseName>' --username <adminLogin> --password <adminPassword> --table 'delays' --export-dir '/tutorials/flightdelays/output' --fields-terminated-by '\t' -m 1
    ```

    Sqoop łączy toohello bazy danych zawierające hello opóźnienia tabeli i eksportuje dane z hello `/tutorials/flightdelays/output` tabeli opóźnienia toohello katalogów.

3. Po zakończeniu wykonywania polecenia hello Użyj hello następujące bazy danych toohello tooconnect przy użyciu języka TSQL:

    ```
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P <adminPassword> -p 1433 -D <databaseName>
    ```

    Po nawiązaniu połączenia użyj hello następujące instrukcje tooverify czy hello danych został wyeksportowany toohello mobiledata tabeli:

    ```
    SELECT * FROM delays
    GO
    ```

    Powinna zostać wyświetlona lista dane w tabeli hello. Typ `exit` tooexit hello tsql narzędzia.

## <a id="nextsteps"></a> Następne kroki

Zobacz więcej sposobów toowork z danymi w usłudze HDInsight, toolearn hello w następujących dokumentach:

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
