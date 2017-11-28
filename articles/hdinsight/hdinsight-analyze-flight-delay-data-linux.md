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
# <a name="analyze-flight-delay-data-by-using-hive-on-linux-based-hdinsight"></a><span data-ttu-id="05d4b-103">Analizowanie danych opóźnienie transmitowane przy użyciu usługi Hive w usłudze HDInsight z systemem Linux</span><span class="sxs-lookup"><span data-stu-id="05d4b-103">Analyze flight delay data by using Hive on Linux-based HDInsight</span></span>

<span data-ttu-id="05d4b-104">Dowiedz się, jak tooanalyze transmitowane opóźnienie danych przy użyciu Hive w usłudze HDInsight z systemem Linux następnie wyeksportować hello tooAzure danych bazy danych SQL przy użyciu Sqoop.</span><span class="sxs-lookup"><span data-stu-id="05d4b-104">Learn how tooanalyze flight delay data using Hive on Linux-based HDInsight then export hello data tooAzure SQL Database using Sqoop.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="05d4b-105">kroki Hello w tym dokumencie wymagają klastra usługi HDInsight, który używa systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="05d4b-105">hello steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="05d4b-106">Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="05d4b-106">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="05d4b-107">Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).</span><span class="sxs-lookup"><span data-stu-id="05d4b-107">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

### <a name="prerequisites"></a><span data-ttu-id="05d4b-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="05d4b-108">Prerequisites</span></span>

* <span data-ttu-id="05d4b-109">**Klaster usługi HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="05d4b-109">**An HDInsight cluster**.</span></span> <span data-ttu-id="05d4b-110">Zobacz [rozpocząć korzystanie z usługi Hadoop przy użyciu Hive w usłudze HDInsight w systemie Linux](hdinsight-hadoop-linux-tutorial-get-started.md) instrukcje dotyczące tworzenia nowego klastra usługi HDInsight opartej na systemie Linux.</span><span class="sxs-lookup"><span data-stu-id="05d4b-110">See [Get started using Hadoop with Hive in HDInsight on Linux](hdinsight-hadoop-linux-tutorial-get-started.md) for steps on creating a new Linux-based HDInsight cluster.</span></span>

* <span data-ttu-id="05d4b-111">**Usługa Azure SQL Database**.</span><span class="sxs-lookup"><span data-stu-id="05d4b-111">**Azure SQL Database**.</span></span> <span data-ttu-id="05d4b-112">Korzystasz z bazy danych Azure SQL jako miejsce docelowe magazynu danych.</span><span class="sxs-lookup"><span data-stu-id="05d4b-112">You use an Azure SQL database as a destination data store.</span></span> <span data-ttu-id="05d4b-113">Jeśli nie masz już bazę danych SQL, zobacz [samouczek usługi SQL Database: tworzenie bazy danych SQL w minutach](../sql-database/sql-database-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="05d4b-113">If you do not have a SQL Database already, see [SQL Database tutorial: Create a SQL database in minutes](../sql-database/sql-database-get-started.md).</span></span>

* <span data-ttu-id="05d4b-114">**Interfejs wiersza polecenia platformy Azure**.</span><span class="sxs-lookup"><span data-stu-id="05d4b-114">**Azure CLI**.</span></span> <span data-ttu-id="05d4b-115">Jeśli nie zainstalowano hello wiersza polecenia platformy Azure, zobacz [Instalowanie i Konfigurowanie interfejsu wiersza polecenia Azure hello](../cli-install-nodejs.md) dla większej liczby kroków.</span><span class="sxs-lookup"><span data-stu-id="05d4b-115">If you have not installed hello Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) for more steps.</span></span>

## <a name="download-hello-flight-data"></a><span data-ttu-id="05d4b-116">Pobierz dane transmitowane hello</span><span class="sxs-lookup"><span data-stu-id="05d4b-116">Download hello flight data</span></span>

1. <span data-ttu-id="05d4b-117">Przeglądaj zbyt[badań i innowacyjnych technologii administracji, biura statystyk transportu][rita-website].</span><span class="sxs-lookup"><span data-stu-id="05d4b-117">Browse too[Research and Innovative Technology Administration, Bureau of Transportation Statistics][rita-website].</span></span>

2. <span data-ttu-id="05d4b-118">Na stronie powitania wybierz hello następujące wartości:</span><span class="sxs-lookup"><span data-stu-id="05d4b-118">On hello page, select hello following values:</span></span>

   | <span data-ttu-id="05d4b-119">Nazwa</span><span class="sxs-lookup"><span data-stu-id="05d4b-119">Name</span></span> | <span data-ttu-id="05d4b-120">Wartość</span><span class="sxs-lookup"><span data-stu-id="05d4b-120">Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="05d4b-121">Filtr roku</span><span class="sxs-lookup"><span data-stu-id="05d4b-121">Filter Year</span></span> |<span data-ttu-id="05d4b-122">2013</span><span class="sxs-lookup"><span data-stu-id="05d4b-122">2013</span></span> |
   | <span data-ttu-id="05d4b-123">Filtruj okres</span><span class="sxs-lookup"><span data-stu-id="05d4b-123">Filter Period</span></span> |<span data-ttu-id="05d4b-124">Stycznia</span><span class="sxs-lookup"><span data-stu-id="05d4b-124">January</span></span> |
   | <span data-ttu-id="05d4b-125">Pola</span><span class="sxs-lookup"><span data-stu-id="05d4b-125">Fields</span></span> |<span data-ttu-id="05d4b-126">Rok, FlightDate, UniqueCarrier, operatora, FlightNum, OriginAirportID, pochodzenia, OriginCityName, OriginState, DestAirportID, Dest, DestCityName, DestState, DepDelayMinutes, ArrDelay, ArrDelayMinutes, CarrierDelay, WeatherDelay, NASDelay, SecurityDelay, LateAircraftDelay.</span><span class="sxs-lookup"><span data-stu-id="05d4b-126">Year, FlightDate, UniqueCarrier, Carrier, FlightNum, OriginAirportID, Origin, OriginCityName, OriginState, DestAirportID, Dest, DestCityName, DestState, DepDelayMinutes, ArrDelay, ArrDelayMinutes, CarrierDelay, WeatherDelay, NASDelay, SecurityDelay, LateAircraftDelay.</span></span> <span data-ttu-id="05d4b-127">Usuń zaznaczenie wszystkich innych pól</span><span class="sxs-lookup"><span data-stu-id="05d4b-127">Clear all other fields</span></span> |

3. <span data-ttu-id="05d4b-128">Kliknij pozycję **Pobierz**.</span><span class="sxs-lookup"><span data-stu-id="05d4b-128">Click **Download**.</span></span>

## <a name="upload-hello-data"></a><span data-ttu-id="05d4b-129">Przekazywanie danych hello</span><span class="sxs-lookup"><span data-stu-id="05d4b-129">Upload hello data</span></span>

1. <span data-ttu-id="05d4b-130">Użyj następującego polecenia tooupload hello zip pliku toohello HDInsight węzła głównego klastra hello:</span><span class="sxs-lookup"><span data-stu-id="05d4b-130">Use hello following command tooupload hello zip file toohello HDInsight cluster head node:</span></span>

    ```
    scp FILENAME.zip USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:
    ```

    <span data-ttu-id="05d4b-131">Zastąp **FILENAME** o nazwie hello hello pliku zip.</span><span class="sxs-lookup"><span data-stu-id="05d4b-131">Replace **FILENAME** with hello name of hello zip file.</span></span> <span data-ttu-id="05d4b-132">Zastąp **USERNAME** z logowaniem SSH hello hello klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="05d4b-132">Replace **USERNAME** with hello SSH login for hello HDInsight cluster.</span></span> <span data-ttu-id="05d4b-133">Zamień NAZWAKLASTRA hello nazwę hello klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="05d4b-133">Replace CLUSTERNAME with hello name of hello HDInsight cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="05d4b-134">Jeśli używasz tooauthenticate hasło logowanie SSH, zostanie wyświetlony monit o hasło hello.</span><span class="sxs-lookup"><span data-stu-id="05d4b-134">If you use a password tooauthenticate your SSH login, you are prompted for hello password.</span></span> <span data-ttu-id="05d4b-135">Jeśli używasz klucza publicznego, może być konieczne toouse hello `-i` parametru i określ toohello ścieżka hello pasujących do klucza prywatnego.</span><span class="sxs-lookup"><span data-stu-id="05d4b-135">If you used a public key, you may need toouse hello `-i` parameter and specify hello path toohello matching private key.</span></span> <span data-ttu-id="05d4b-136">Na przykład `scp -i ~/.ssh/id_rsa FILENAME.zip USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:`.</span><span class="sxs-lookup"><span data-stu-id="05d4b-136">For example, `scp -i ~/.ssh/id_rsa FILENAME.zip USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:`.</span></span>

2. <span data-ttu-id="05d4b-137">Po zakończeniu przekazywania hello połączenie toohello klastra przy użyciu protokołu SSH:</span><span class="sxs-lookup"><span data-stu-id="05d4b-137">Once hello upload has completed, connect toohello cluster using SSH:</span></span>

    ```ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net```

    <span data-ttu-id="05d4b-138">Aby uzyskać więcej informacji, zobacz [Używanie protokołu SSH w usłudze HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="05d4b-138">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

3. <span data-ttu-id="05d4b-139">Po nawiązaniu połączenia użyj następującego pliku .zip hello toounzip hello:</span><span class="sxs-lookup"><span data-stu-id="05d4b-139">Once connected, use hello following toounzip hello .zip file:</span></span>

    ```
    unzip FILENAME.zip
    ```

    <span data-ttu-id="05d4b-140">To polecenie wyodrębnia plik CSV, który jest około 60 MB.</span><span class="sxs-lookup"><span data-stu-id="05d4b-140">This command extracts a .csv file that is roughly 60 MB.</span></span>

4. <span data-ttu-id="05d4b-141">Użyj hello następujące polecenia toocreate katalogu w magazynie usługi HDInsight, a następnie skopiuj katalog toohello pliku hello:</span><span class="sxs-lookup"><span data-stu-id="05d4b-141">Use hello following command toocreate a directory on HDInsight storage, and then copy hello file toohello directory:</span></span>

    ```
    hdfs dfs -mkdir -p /tutorials/flightdelays/data
    hdfs dfs -put FILENAME.csv /tutorials/flightdelays/data/
    ```

## <a name="create-and-run-hello-hiveql"></a><span data-ttu-id="05d4b-142">Tworzenie i uruchamianie hello HiveQL</span><span class="sxs-lookup"><span data-stu-id="05d4b-142">Create and run hello HiveQL</span></span>

<span data-ttu-id="05d4b-143">Użyj następujących hello kroki tooimport danych z pliku CSV hello w tabeli programu Hive o nazwie **opóźnienia**.</span><span class="sxs-lookup"><span data-stu-id="05d4b-143">Use hello following steps tooimport data from hello CSV file into a Hive table named **Delays**.</span></span>

1. <span data-ttu-id="05d4b-144">Użyj następujących hello polecenia toocreate i Edytuj plik o nazwie **flightdelays.hql**:</span><span class="sxs-lookup"><span data-stu-id="05d4b-144">Use hello following command toocreate and edit a new file named **flightdelays.hql**:</span></span>

    ```
    nano flightdelays.hql
    ```

    <span data-ttu-id="05d4b-145">Użyj hello następującego tekstu jako hello zawartość tego pliku:</span><span class="sxs-lookup"><span data-stu-id="05d4b-145">Use hello following text as hello contents of this file:</span></span>

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

2. <span data-ttu-id="05d4b-146">toosave hello pliku, użyj **Ctrl + X**, następnie **Y** .</span><span class="sxs-lookup"><span data-stu-id="05d4b-146">toosave hello file, use **Ctrl + X**, then **Y** .</span></span>

3. <span data-ttu-id="05d4b-147">toostart Hive i wykonywania hello **flightdelays.hql** plików, użyj następującego polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="05d4b-147">toostart Hive and run hello **flightdelays.hql** file, use hello following command:</span></span>

    ```
    beeline -u 'jdbc:hive2://localhost:10001/;transportMode=http' -f flightdelays.hql
    ```

   > [!NOTE]
   > <span data-ttu-id="05d4b-148">W tym przykładzie `localhost` jest używany, ponieważ są połączone toohello węzła głównego klastra usługi HDInsight hello, czyli gdzie działa serwera HiveServer2.</span><span class="sxs-lookup"><span data-stu-id="05d4b-148">In this example, `localhost` is used since you are connected toohello head node of hello HDInsight cluster, which is where HiveServer2 is running.</span></span>

4. <span data-ttu-id="05d4b-149">Raz hello __flightdelays.hql__ skrypt uruchomiony zakończeniu Użyj hello następujące polecenie tooopen jako sesja interaktywna Beeline:</span><span class="sxs-lookup"><span data-stu-id="05d4b-149">Once hello __flightdelays.hql__ script finishes running, use hello following command tooopen an interactive Beeline session:</span></span>

    ```
    beeline -u 'jdbc:hive2://localhost:10001/;transportMode=http'
    ```

5. <span data-ttu-id="05d4b-150">Po otrzymaniu hello `jdbc:hive2://localhost:10001/>` monit, użyj hello poniższych zapytania tooretrieve danych z danych opóźnienie transmitowane hello zaimportowane.</span><span class="sxs-lookup"><span data-stu-id="05d4b-150">When you receive hello `jdbc:hive2://localhost:10001/>` prompt, use hello following query tooretrieve data from hello imported flight delay data.</span></span>

    ```hiveql
    INSERT OVERWRITE DIRECTORY '/tutorials/flightdelays/output'
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    SELECT regexp_replace(origin_city_name, '''', ''),
        avg(weather_delay)
    FROM delays
    WHERE weather_delay IS NOT NULL
    GROUP BY origin_city_name;
    ```

    <span data-ttu-id="05d4b-151">To zapytanie pobiera listę miejscowości opóźnienia doświadczonym pogodzie, wraz ze średnią hello opóźnienie czasu i zapisać go za`/tutorials/flightdelays/output`.</span><span class="sxs-lookup"><span data-stu-id="05d4b-151">This query retrieves a list of cities that experienced weather delays, along with hello average delay time, and save it too`/tutorials/flightdelays/output`.</span></span> <span data-ttu-id="05d4b-152">Później Sqoop odczytuje hello danych z tej lokalizacji i wyeksportować go tooAzure bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="05d4b-152">Later, Sqoop reads hello data from this location and export it tooAzure SQL Database.</span></span>

6. <span data-ttu-id="05d4b-153">Wprowadź tooexit Beeline, `!quit` hello w wierszu.</span><span class="sxs-lookup"><span data-stu-id="05d4b-153">tooexit Beeline, enter `!quit` at hello prompt.</span></span>

## <a name="create-a-sql-database"></a><span data-ttu-id="05d4b-154">Tworzenie bazy danych SQL</span><span class="sxs-lookup"><span data-stu-id="05d4b-154">Create a SQL Database</span></span>

<span data-ttu-id="05d4b-155">Jeśli masz już bazę danych SQL, należy uzyskać hello nazwy serwera.</span><span class="sxs-lookup"><span data-stu-id="05d4b-155">If you already have a SQL Database, you must get hello server name.</span></span> <span data-ttu-id="05d4b-156">Hello nazwy serwera można znaleźć w hello [portalu Azure](https://portal.azure.com) wybierając **baz danych**, i filtrowanie hello hello nazwę bazy danych należy ma toouse.</span><span class="sxs-lookup"><span data-stu-id="05d4b-156">You can find hello server name in hello [Azure portal](https://portal.azure.com) by selecting **SQL Databases**, and then filtering on hello name of hello database you wish toouse.</span></span> <span data-ttu-id="05d4b-157">Nazwa serwera Hello ma na liście hello **serwera** kolumny.</span><span class="sxs-lookup"><span data-stu-id="05d4b-157">hello server name is listed in hello **SERVER** column.</span></span>

<span data-ttu-id="05d4b-158">Jeśli nie masz już bazę danych SQL, użyj informacji hello w [samouczek usługi SQL Database: tworzenie bazy danych SQL w minutach](../sql-database/sql-database-get-started.md) toocreate jeden.</span><span class="sxs-lookup"><span data-stu-id="05d4b-158">If you do not already have a SQL Database, use hello information in [SQL Database tutorial: Create a SQL database in minutes](../sql-database/sql-database-get-started.md) toocreate one.</span></span> <span data-ttu-id="05d4b-159">Zapisz nazwę serwera hello do hello bazy danych.</span><span class="sxs-lookup"><span data-stu-id="05d4b-159">Save hello server name used for hello database.</span></span>

## <a name="create-a-sql-database-table"></a><span data-ttu-id="05d4b-160">Tworzenie tabeli bazy danych SQL</span><span class="sxs-lookup"><span data-stu-id="05d4b-160">Create a SQL Database table</span></span>

> [!NOTE]
> <span data-ttu-id="05d4b-161">Istnieje wiele sposobów tooSQL tooconnect bazy danych i Utwórz tabelę.</span><span class="sxs-lookup"><span data-stu-id="05d4b-161">There are many ways tooconnect tooSQL Database and create a table.</span></span> <span data-ttu-id="05d4b-162">Witaj, użyj czynności po [protokół FreeTDS](http://www.freetds.org/) z klastrem usługi HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="05d4b-162">hello following steps use [FreeTDS](http://www.freetds.org/) from hello HDInsight cluster.</span></span>


1. <span data-ttu-id="05d4b-163">Użyj SSH tooconnect toohello opartych na systemie Linux klaster usługi HDInsight i uruchamiania hello następujące kroki w sesji SSH hello.</span><span class="sxs-lookup"><span data-stu-id="05d4b-163">Use SSH tooconnect toohello Linux-based HDInsight cluster, and run hello following steps from hello SSH session.</span></span>

2. <span data-ttu-id="05d4b-164">Użyj następującego polecenia tooinstall protokół FreeTDS hello:</span><span class="sxs-lookup"><span data-stu-id="05d4b-164">Use hello following command tooinstall FreeTDS:</span></span>

    ```
    sudo apt-get --assume-yes install freetds-dev freetds-bin
    ```

3. <span data-ttu-id="05d4b-165">Po zakończeniu instalacji hello Użyj hello następujące polecenia tooconnect toohello bazy danych programu SQL server.</span><span class="sxs-lookup"><span data-stu-id="05d4b-165">Once hello install completes, use hello following command tooconnect toohello SQL Database server.</span></span> <span data-ttu-id="05d4b-166">Zastąp **serverName** z nazwą serwera bazy danych SQL hello.</span><span class="sxs-lookup"><span data-stu-id="05d4b-166">Replace **serverName** with hello SQL Database server name.</span></span> <span data-ttu-id="05d4b-167">Zastąp **adminLogin** i **adminPassword** z logowaniem hello bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="05d4b-167">Replace **adminLogin** and **adminPassword** with hello login for SQL Database.</span></span> <span data-ttu-id="05d4b-168">Zastąp **databaseName** hello nazwą bazy danych.</span><span class="sxs-lookup"><span data-stu-id="05d4b-168">Replace **databaseName** with hello database name.</span></span>

    ```
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P <adminPassword> -p 1433 -D <databaseName>
    ```

    <span data-ttu-id="05d4b-169">Pojawi się toohello podobne dane wyjściowe następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="05d4b-169">You receive output similar toohello following text:</span></span>

    ```
    locale is "en_US.UTF-8"
    locale charset is "UTF-8"
    using default charset "UTF-8"
    Default database being set toosqooptest
    1>
    ```

4. <span data-ttu-id="05d4b-170">Na powitania `1>` monit, wprowadź hello następujące wiersze:</span><span class="sxs-lookup"><span data-stu-id="05d4b-170">At hello `1>` prompt, enter hello following lines:</span></span>

    ```
    CREATE TABLE [dbo].[delays](
    [origin_city_name] [nvarchar](50) NOT NULL,
    [weather_delay] float,
    CONSTRAINT [PK_delays] PRIMARY KEY CLUSTERED   
    ([origin_city_name] ASC))
    GO
    ```

    <span data-ttu-id="05d4b-171">Gdy hello `GO` instrukcja została wprowadzona, poprzednie instrukcje hello są oceniane.</span><span class="sxs-lookup"><span data-stu-id="05d4b-171">When hello `GO` statement is entered, hello previous statements are evaluated.</span></span> <span data-ttu-id="05d4b-172">To zapytanie tworzy tabelę o nazwie **opóźnienia**, z indeksem klastrowanym.</span><span class="sxs-lookup"><span data-stu-id="05d4b-172">This query creates a table named **delays**, with a clustered index.</span></span>

    <span data-ttu-id="05d4b-173">Utworzono hello Użyj następującego tooverify zapytania, który hello tabeli:</span><span class="sxs-lookup"><span data-stu-id="05d4b-173">Use hello following query tooverify that hello table has been created:</span></span>

    ```
    SELECT * FROM information_schema.tables
    GO
    ```

    <span data-ttu-id="05d4b-174">Witaj danych wyjściowych jest podobne toohello następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="05d4b-174">hello output is similar toohello following text:</span></span>

    ```
    TABLE_CATALOG   TABLE_SCHEMA    TABLE_NAME      TABLE_TYPE
    databaseName       dbo     delays      BASE TABLE
    ```

5. <span data-ttu-id="05d4b-175">Wprowadź `exit` na powitania `1>` Monituj tooexit hello tsql narzędzia.</span><span class="sxs-lookup"><span data-stu-id="05d4b-175">Enter `exit` at hello `1>` prompt tooexit hello tsql utility.</span></span>

## <a name="export-data-with-sqoop"></a><span data-ttu-id="05d4b-176">Eksportowanie danych z Sqoop</span><span class="sxs-lookup"><span data-stu-id="05d4b-176">Export data with Sqoop</span></span>

1. <span data-ttu-id="05d4b-177">Użyj hello następujące polecenie tooverify czy Sqoop widzą bazy danych SQL:</span><span class="sxs-lookup"><span data-stu-id="05d4b-177">Use hello following command tooverify that Sqoop can see your SQL Database:</span></span>

    ```
    sqoop list-databases --connect jdbc:sqlserver://<serverName>.database.windows.net:1433 --username <adminLogin> --password <adminPassword>
    ```

    <span data-ttu-id="05d4b-178">To polecenie zwraca listę baz danych, w tym hello bazy danych, utworzone wcześniej hello tabeli opóźnień w.</span><span class="sxs-lookup"><span data-stu-id="05d4b-178">This command returns a list of databases, including hello database that you created hello delays table in earlier.</span></span>

2. <span data-ttu-id="05d4b-179">Użyj następującego polecenia tooexport danych z tabeli mobiledata toohello hivesampletable hello:</span><span class="sxs-lookup"><span data-stu-id="05d4b-179">Use hello following command tooexport data from hivesampletable toohello mobiledata table:</span></span>

    ```
    sqoop export --connect 'jdbc:sqlserver://<serverName>.database.windows.net:1433;database=<databaseName>' --username <adminLogin> --password <adminPassword> --table 'delays' --export-dir '/tutorials/flightdelays/output' --fields-terminated-by '\t' -m 1
    ```

    <span data-ttu-id="05d4b-180">Sqoop łączy toohello bazy danych zawierające hello opóźnienia tabeli i eksportuje dane z hello `/tutorials/flightdelays/output` tabeli opóźnienia toohello katalogów.</span><span class="sxs-lookup"><span data-stu-id="05d4b-180">Sqoop connects toohello database containing hello delays table, and exports data from hello `/tutorials/flightdelays/output` directory toohello delays table.</span></span>

3. <span data-ttu-id="05d4b-181">Po zakończeniu wykonywania polecenia hello Użyj hello następujące bazy danych toohello tooconnect przy użyciu języka TSQL:</span><span class="sxs-lookup"><span data-stu-id="05d4b-181">After hello command completes, use hello following tooconnect toohello database using TSQL:</span></span>

    ```
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P <adminPassword> -p 1433 -D <databaseName>
    ```

    <span data-ttu-id="05d4b-182">Po nawiązaniu połączenia użyj hello następujące instrukcje tooverify czy hello danych został wyeksportowany toohello mobiledata tabeli:</span><span class="sxs-lookup"><span data-stu-id="05d4b-182">Once connected, use hello following statements tooverify that hello data was exported toohello mobiledata table:</span></span>

    ```
    SELECT * FROM delays
    GO
    ```

    <span data-ttu-id="05d4b-183">Powinna zostać wyświetlona lista dane w tabeli hello.</span><span class="sxs-lookup"><span data-stu-id="05d4b-183">You should see a listing of data in hello table.</span></span> <span data-ttu-id="05d4b-184">Typ `exit` tooexit hello tsql narzędzia.</span><span class="sxs-lookup"><span data-stu-id="05d4b-184">Type `exit` tooexit hello tsql utility.</span></span>

## <span data-ttu-id="05d4b-185"><a id="nextsteps"></a> Następne kroki</span><span class="sxs-lookup"><span data-stu-id="05d4b-185"><a id="nextsteps"></a> Next steps</span></span>

<span data-ttu-id="05d4b-186">Zobacz więcej sposobów toowork z danymi w usłudze HDInsight, toolearn hello w następujących dokumentach:</span><span class="sxs-lookup"><span data-stu-id="05d4b-186">toolearn more ways toowork with data in HDInsight, see hello following documents:</span></span>

* <span data-ttu-id="05d4b-187">[Korzystanie z programu Hive z usługą HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="05d4b-187">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="05d4b-188">[Korzystanie z Oozie z usługą HDInsight][hdinsight-use-oozie]</span><span class="sxs-lookup"><span data-stu-id="05d4b-188">[Use Oozie with HDInsight][hdinsight-use-oozie]</span></span>
* <span data-ttu-id="05d4b-189">[Korzystanie z usługą HDInsight Sqoop][hdinsight-use-sqoop]</span><span class="sxs-lookup"><span data-stu-id="05d4b-189">[Use Sqoop with HDInsight][hdinsight-use-sqoop]</span></span>
* <span data-ttu-id="05d4b-190">[Korzystanie z języka Pig z usługą HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="05d4b-190">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="05d4b-191">[Tworzenie programów Java MapReduce dla usługi HDInsight][hdinsight-develop-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="05d4b-191">[Develop Java MapReduce programs for HDInsight][hdinsight-develop-mapreduce]</span></span>
* <span data-ttu-id="05d4b-192">[Opracowywanie przesyłanie strumieniowe programów dla usługi HDInsight Hadoop języka Python][hdinsight-develop-streaming]</span><span class="sxs-lookup"><span data-stu-id="05d4b-192">[Develop Python Hadoop streaming programs for HDInsight][hdinsight-develop-streaming]</span></span>

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
