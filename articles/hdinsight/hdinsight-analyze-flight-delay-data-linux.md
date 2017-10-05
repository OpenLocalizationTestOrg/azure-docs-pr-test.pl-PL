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
# <a name="analyze-flight-delay-data-by-using-hive-on-linux-based-hdinsight"></a><span data-ttu-id="006d4-103">Analizowanie danych opóźnienie transmitowane przy użyciu usługi Hive w usłudze HDInsight z systemem Linux</span><span class="sxs-lookup"><span data-stu-id="006d4-103">Analyze flight delay data by using Hive on Linux-based HDInsight</span></span>

<span data-ttu-id="006d4-104">Dowiedz się, jak i analizować dane opóźnienie transmitowane przy użyciu Hive w usłudze HDInsight z systemem Linux, a następnie wyeksportować dane do bazy danych SQL Azure przy użyciu Sqoop.</span><span class="sxs-lookup"><span data-stu-id="006d4-104">Learn how to analyze flight delay data using Hive on Linux-based HDInsight then export the data to Azure SQL Database using Sqoop.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="006d4-105">Kroki opisane w tym dokumencie wymagają klastra usługi HDInsight, który używa systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="006d4-105">The steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="006d4-106">Linux jest jedynym systemem operacyjnym używanym w połączeniu z usługą HDInsight w wersji 3.4 lub nowszą.</span><span class="sxs-lookup"><span data-stu-id="006d4-106">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="006d4-107">Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).</span><span class="sxs-lookup"><span data-stu-id="006d4-107">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

### <a name="prerequisites"></a><span data-ttu-id="006d4-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="006d4-108">Prerequisites</span></span>

* <span data-ttu-id="006d4-109">**Klaster usługi HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="006d4-109">**An HDInsight cluster**.</span></span> <span data-ttu-id="006d4-110">Zobacz [rozpocząć korzystanie z usługi Hadoop przy użyciu Hive w usłudze HDInsight w systemie Linux](hdinsight-hadoop-linux-tutorial-get-started.md) instrukcje dotyczące tworzenia nowego klastra usługi HDInsight opartej na systemie Linux.</span><span class="sxs-lookup"><span data-stu-id="006d4-110">See [Get started using Hadoop with Hive in HDInsight on Linux](hdinsight-hadoop-linux-tutorial-get-started.md) for steps on creating a new Linux-based HDInsight cluster.</span></span>

* <span data-ttu-id="006d4-111">**Baza danych Azure SQL**.</span><span class="sxs-lookup"><span data-stu-id="006d4-111">**Azure SQL Database**.</span></span> <span data-ttu-id="006d4-112">Korzystasz z bazy danych Azure SQL jako miejsce docelowe magazynu danych.</span><span class="sxs-lookup"><span data-stu-id="006d4-112">You use an Azure SQL database as a destination data store.</span></span> <span data-ttu-id="006d4-113">Jeśli nie masz już bazę danych SQL, zobacz [samouczek usługi SQL Database: tworzenie bazy danych SQL w minutach](../sql-database/sql-database-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="006d4-113">If you do not have a SQL Database already, see [SQL Database tutorial: Create a SQL database in minutes](../sql-database/sql-database-get-started.md).</span></span>

* <span data-ttu-id="006d4-114">**Interfejs wiersza polecenia platformy Azure**.</span><span class="sxs-lookup"><span data-stu-id="006d4-114">**Azure CLI**.</span></span> <span data-ttu-id="006d4-115">Jeśli nie zainstalowano wiersza polecenia platformy Azure, zobacz [Instalowanie i Konfigurowanie interfejsu wiersza polecenia Azure](../cli-install-nodejs.md) dla większej liczby kroków.</span><span class="sxs-lookup"><span data-stu-id="006d4-115">If you have not installed the Azure CLI, see [Install and Configure the Azure CLI](../cli-install-nodejs.md) for more steps.</span></span>

## <a name="download-the-flight-data"></a><span data-ttu-id="006d4-116">Pobierz dane transmitowane</span><span class="sxs-lookup"><span data-stu-id="006d4-116">Download the flight data</span></span>

1. <span data-ttu-id="006d4-117">Przejdź do [badań i Nowatorska technologia administracji, biura statystyk transportu][rita-website].</span><span class="sxs-lookup"><span data-stu-id="006d4-117">Browse to [Research and Innovative Technology Administration, Bureau of Transportation Statistics][rita-website].</span></span>

2. <span data-ttu-id="006d4-118">Na stronie wybierz następujące wartości:</span><span class="sxs-lookup"><span data-stu-id="006d4-118">On the page, select the following values:</span></span>

   | <span data-ttu-id="006d4-119">Nazwa</span><span class="sxs-lookup"><span data-stu-id="006d4-119">Name</span></span> | <span data-ttu-id="006d4-120">Wartość</span><span class="sxs-lookup"><span data-stu-id="006d4-120">Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="006d4-121">Filtr roku</span><span class="sxs-lookup"><span data-stu-id="006d4-121">Filter Year</span></span> |<span data-ttu-id="006d4-122">2013</span><span class="sxs-lookup"><span data-stu-id="006d4-122">2013</span></span> |
   | <span data-ttu-id="006d4-123">Filtruj okres</span><span class="sxs-lookup"><span data-stu-id="006d4-123">Filter Period</span></span> |<span data-ttu-id="006d4-124">Stycznia</span><span class="sxs-lookup"><span data-stu-id="006d4-124">January</span></span> |
   | <span data-ttu-id="006d4-125">Pola</span><span class="sxs-lookup"><span data-stu-id="006d4-125">Fields</span></span> |<span data-ttu-id="006d4-126">Rok, FlightDate, UniqueCarrier, operatora, FlightNum, OriginAirportID, pochodzenia, OriginCityName, OriginState, DestAirportID, Dest, DestCityName, DestState, DepDelayMinutes, ArrDelay, ArrDelayMinutes, CarrierDelay, WeatherDelay, NASDelay, SecurityDelay, LateAircraftDelay.</span><span class="sxs-lookup"><span data-stu-id="006d4-126">Year, FlightDate, UniqueCarrier, Carrier, FlightNum, OriginAirportID, Origin, OriginCityName, OriginState, DestAirportID, Dest, DestCityName, DestState, DepDelayMinutes, ArrDelay, ArrDelayMinutes, CarrierDelay, WeatherDelay, NASDelay, SecurityDelay, LateAircraftDelay.</span></span> <span data-ttu-id="006d4-127">Usuń zaznaczenie wszystkich innych pól</span><span class="sxs-lookup"><span data-stu-id="006d4-127">Clear all other fields</span></span> |

3. <span data-ttu-id="006d4-128">Kliknij pozycję **Pobierz**.</span><span class="sxs-lookup"><span data-stu-id="006d4-128">Click **Download**.</span></span>

## <a name="upload-the-data"></a><span data-ttu-id="006d4-129">Przekazywanie danych</span><span class="sxs-lookup"><span data-stu-id="006d4-129">Upload the data</span></span>

1. <span data-ttu-id="006d4-130">Użyj następującego polecenia, aby przekazać plik zip do węzła głównego klastra usługi HDInsight:</span><span class="sxs-lookup"><span data-stu-id="006d4-130">Use the following command to upload the zip file to the HDInsight cluster head node:</span></span>

    ```
    scp FILENAME.zip USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:
    ```

    <span data-ttu-id="006d4-131">Zastąp **FILENAME** z nazwą pliku zip.</span><span class="sxs-lookup"><span data-stu-id="006d4-131">Replace **FILENAME** with the name of the zip file.</span></span> <span data-ttu-id="006d4-132">Zastąp **USERNAME** z logowaniem SSH dla klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="006d4-132">Replace **USERNAME** with the SSH login for the HDInsight cluster.</span></span> <span data-ttu-id="006d4-133">Zamień NAZWAKLASTRA nazwę klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="006d4-133">Replace CLUSTERNAME with the name of the HDInsight cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="006d4-134">Jeśli używasz hasła uwierzytelniania nazwy logowania SSH, zostanie wyświetlony monit o hasło.</span><span class="sxs-lookup"><span data-stu-id="006d4-134">If you use a password to authenticate your SSH login, you are prompted for the password.</span></span> <span data-ttu-id="006d4-135">Jeśli używasz klucza publicznego, może być konieczne użycie `-i` parametru i określ ścieżkę do odpowiedniego klucza prywatnego.</span><span class="sxs-lookup"><span data-stu-id="006d4-135">If you used a public key, you may need to use the `-i` parameter and specify the path to the matching private key.</span></span> <span data-ttu-id="006d4-136">Na przykład `scp -i ~/.ssh/id_rsa FILENAME.zip USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:`.</span><span class="sxs-lookup"><span data-stu-id="006d4-136">For example, `scp -i ~/.ssh/id_rsa FILENAME.zip USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:`.</span></span>

2. <span data-ttu-id="006d4-137">Po zakończeniu przekazywania nawiązać połączenia z klastrem przy użyciu protokołu SSH:</span><span class="sxs-lookup"><span data-stu-id="006d4-137">Once the upload has completed, connect to the cluster using SSH:</span></span>

    ```ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net```

    <span data-ttu-id="006d4-138">Aby uzyskać więcej informacji, zobacz [Używanie protokołu SSH w usłudze HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="006d4-138">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

3. <span data-ttu-id="006d4-139">Po nawiązaniu połączenia, Rozpakuj plik zip należy wykonać następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="006d4-139">Once connected, use the following to unzip the .zip file:</span></span>

    ```
    unzip FILENAME.zip
    ```

    <span data-ttu-id="006d4-140">To polecenie wyodrębnia plik CSV, który jest około 60 MB.</span><span class="sxs-lookup"><span data-stu-id="006d4-140">This command extracts a .csv file that is roughly 60 MB.</span></span>

4. <span data-ttu-id="006d4-141">Użyj następującego polecenia, aby utworzyć katalog w magazynie usługi HDInsight, a następnie skopiuj plik do katalogu:</span><span class="sxs-lookup"><span data-stu-id="006d4-141">Use the following command to create a directory on HDInsight storage, and then copy the file to the directory:</span></span>

    ```
    hdfs dfs -mkdir -p /tutorials/flightdelays/data
    hdfs dfs -put FILENAME.csv /tutorials/flightdelays/data/
    ```

## <a name="create-and-run-the-hiveql"></a><span data-ttu-id="006d4-142">Tworzenie i uruchamianie HiveQL</span><span class="sxs-lookup"><span data-stu-id="006d4-142">Create and run the HiveQL</span></span>

<span data-ttu-id="006d4-143">Wykonaj następujące kroki, aby zaimportować dane z pliku CSV do tabeli programu Hive o nazwie **opóźnienia**.</span><span class="sxs-lookup"><span data-stu-id="006d4-143">Use the following steps to import data from the CSV file into a Hive table named **Delays**.</span></span>

1. <span data-ttu-id="006d4-144">Użyj następującego polecenia można tworzyć i edytować nowy plik o nazwie **flightdelays.hql**:</span><span class="sxs-lookup"><span data-stu-id="006d4-144">Use the following command to create and edit a new file named **flightdelays.hql**:</span></span>

    ```
    nano flightdelays.hql
    ```

    <span data-ttu-id="006d4-145">Zawartość tego pliku, należy użyć następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="006d4-145">Use the following text as the contents of this file:</span></span>

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

2. <span data-ttu-id="006d4-146">Aby zapisać plik, użyj **Ctrl + X**, następnie **Y** .</span><span class="sxs-lookup"><span data-stu-id="006d4-146">To save the file, use **Ctrl + X**, then **Y** .</span></span>

3. <span data-ttu-id="006d4-147">Aby uruchomić Hive i przeprowadzić **flightdelays.hql** plików, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="006d4-147">To start Hive and run the **flightdelays.hql** file, use the following command:</span></span>

    ```
    beeline -u 'jdbc:hive2://localhost:10001/;transportMode=http' -f flightdelays.hql
    ```

   > [!NOTE]
   > <span data-ttu-id="006d4-148">W tym przykładzie `localhost` służy Skoro masz połączenie z węzłem głównym klastra usługi HDInsight, czyli gdzie działa serwera HiveServer2.</span><span class="sxs-lookup"><span data-stu-id="006d4-148">In this example, `localhost` is used since you are connected to the head node of the HDInsight cluster, which is where HiveServer2 is running.</span></span>

4. <span data-ttu-id="006d4-149">Raz __flightdelays.hql__ zakończeniu uruchamiania skryptu, użyj następującego polecenia, aby otworzyć sesji interaktywnej Beeline:</span><span class="sxs-lookup"><span data-stu-id="006d4-149">Once the __flightdelays.hql__ script finishes running, use the following command to open an interactive Beeline session:</span></span>

    ```
    beeline -u 'jdbc:hive2://localhost:10001/;transportMode=http'
    ```

5. <span data-ttu-id="006d4-150">Po otrzymaniu `jdbc:hive2://localhost:10001/>` monit, użyj następującego zapytania do pobierania danych z transmitowane importowanych danych opóźnienia.</span><span class="sxs-lookup"><span data-stu-id="006d4-150">When you receive the `jdbc:hive2://localhost:10001/>` prompt, use the following query to retrieve data from the imported flight delay data.</span></span>

    ```hiveql
    INSERT OVERWRITE DIRECTORY '/tutorials/flightdelays/output'
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    SELECT regexp_replace(origin_city_name, '''', ''),
        avg(weather_delay)
    FROM delays
    WHERE weather_delay IS NOT NULL
    GROUP BY origin_city_name;
    ```

    <span data-ttu-id="006d4-151">To zapytanie pobiera listę miast, w których wystąpił pogody opóźnienia, oraz średnie opóźnienie czasu i zapisać go do `/tutorials/flightdelays/output`.</span><span class="sxs-lookup"><span data-stu-id="006d4-151">This query retrieves a list of cities that experienced weather delays, along with the average delay time, and save it to `/tutorials/flightdelays/output`.</span></span> <span data-ttu-id="006d4-152">Później Sqoop odczytuje dane z tej lokalizacji i eksportowania ich do bazy danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="006d4-152">Later, Sqoop reads the data from this location and export it to Azure SQL Database.</span></span>

6. <span data-ttu-id="006d4-153">Aby zakończyć Beeline, wprowadź `!quit` w wierszu.</span><span class="sxs-lookup"><span data-stu-id="006d4-153">To exit Beeline, enter `!quit` at the prompt.</span></span>

## <a name="create-a-sql-database"></a><span data-ttu-id="006d4-154">Tworzenie bazy danych SQL</span><span class="sxs-lookup"><span data-stu-id="006d4-154">Create a SQL Database</span></span>

<span data-ttu-id="006d4-155">Jeśli masz już bazę danych SQL, należy uzyskać nazwę serwera.</span><span class="sxs-lookup"><span data-stu-id="006d4-155">If you already have a SQL Database, you must get the server name.</span></span> <span data-ttu-id="006d4-156">Można znaleźć nazwę serwera w [portalu Azure](https://portal.azure.com) wybierając **baz danych**i filtrowanie Nazwa bazy danych chcesz użyć.</span><span class="sxs-lookup"><span data-stu-id="006d4-156">You can find the server name in the [Azure portal](https://portal.azure.com) by selecting **SQL Databases**, and then filtering on the name of the database you wish to use.</span></span> <span data-ttu-id="006d4-157">Nazwa serwera ma na liście **serwera** kolumny.</span><span class="sxs-lookup"><span data-stu-id="006d4-157">The server name is listed in the **SERVER** column.</span></span>

<span data-ttu-id="006d4-158">Jeśli nie masz już bazę danych SQL, skorzystaj z informacji w [samouczek usługi SQL Database: tworzenie bazy danych SQL w minutach](../sql-database/sql-database-get-started.md) go utworzyć.</span><span class="sxs-lookup"><span data-stu-id="006d4-158">If you do not already have a SQL Database, use the information in [SQL Database tutorial: Create a SQL database in minutes](../sql-database/sql-database-get-started.md) to create one.</span></span> <span data-ttu-id="006d4-159">Zapisz nazwę serwera, do bazy danych.</span><span class="sxs-lookup"><span data-stu-id="006d4-159">Save the server name used for the database.</span></span>

## <a name="create-a-sql-database-table"></a><span data-ttu-id="006d4-160">Tworzenie tabeli bazy danych SQL</span><span class="sxs-lookup"><span data-stu-id="006d4-160">Create a SQL Database table</span></span>

> [!NOTE]
> <span data-ttu-id="006d4-161">Istnieje wiele sposobów łączenia z bazą danych SQL i tworzenie tabeli.</span><span class="sxs-lookup"><span data-stu-id="006d4-161">There are many ways to connect to SQL Database and create a table.</span></span> <span data-ttu-id="006d4-162">Następujące kroki użyj [protokół FreeTDS](http://www.freetds.org/) z klastrem usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="006d4-162">The following steps use [FreeTDS](http://www.freetds.org/) from the HDInsight cluster.</span></span>


1. <span data-ttu-id="006d4-163">Połącz się z klastrem usługi HDInsight opartej na systemie Linux przy użyciu protokołu SSH, a wykonanie następujących kroków w sesji SSH.</span><span class="sxs-lookup"><span data-stu-id="006d4-163">Use SSH to connect to the Linux-based HDInsight cluster, and run the following steps from the SSH session.</span></span>

2. <span data-ttu-id="006d4-164">Aby zainstalować protokół FreeTDS, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="006d4-164">Use the following command to install FreeTDS:</span></span>

    ```
    sudo apt-get --assume-yes install freetds-dev freetds-bin
    ```

3. <span data-ttu-id="006d4-165">Po zakończeniu instalacji, użyj następującego polecenia, aby połączyć się z serwerem bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="006d4-165">Once the install completes, use the following command to connect to the SQL Database server.</span></span> <span data-ttu-id="006d4-166">Zastąp **serverName** z nazwą serwera bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="006d4-166">Replace **serverName** with the SQL Database server name.</span></span> <span data-ttu-id="006d4-167">Zastąp **adminLogin** i **adminPassword** z nazwy logowania bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="006d4-167">Replace **adminLogin** and **adminPassword** with the login for SQL Database.</span></span> <span data-ttu-id="006d4-168">Zastąp **databaseName** o nazwie bazy danych.</span><span class="sxs-lookup"><span data-stu-id="006d4-168">Replace **databaseName** with the database name.</span></span>

    ```
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P <adminPassword> -p 1433 -D <databaseName>
    ```

    <span data-ttu-id="006d4-169">Pojawi się dane wyjściowe podobne do następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="006d4-169">You receive output similar to the following text:</span></span>

    ```
    locale is "en_US.UTF-8"
    locale charset is "UTF-8"
    using default charset "UTF-8"
    Default database being set to sqooptest
    1>
    ```

4. <span data-ttu-id="006d4-170">W `1>` monit, wprowadź następujące wiersze:</span><span class="sxs-lookup"><span data-stu-id="006d4-170">At the `1>` prompt, enter the following lines:</span></span>

    ```
    CREATE TABLE [dbo].[delays](
    [origin_city_name] [nvarchar](50) NOT NULL,
    [weather_delay] float,
    CONSTRAINT [PK_delays] PRIMARY KEY CLUSTERED   
    ([origin_city_name] ASC))
    GO
    ```

    <span data-ttu-id="006d4-171">Gdy `GO` instrukcja została wprowadzona, poprzednie instrukcje są oceniane.</span><span class="sxs-lookup"><span data-stu-id="006d4-171">When the `GO` statement is entered, the previous statements are evaluated.</span></span> <span data-ttu-id="006d4-172">To zapytanie tworzy tabelę o nazwie **opóźnienia**, z indeksem klastrowanym.</span><span class="sxs-lookup"><span data-stu-id="006d4-172">This query creates a table named **delays**, with a clustered index.</span></span>

    <span data-ttu-id="006d4-173">Użyj następującego zapytania, aby sprawdzić, czy tabela została utworzona:</span><span class="sxs-lookup"><span data-stu-id="006d4-173">Use the following query to verify that the table has been created:</span></span>

    ```
    SELECT * FROM information_schema.tables
    GO
    ```

    <span data-ttu-id="006d4-174">Dane wyjściowe będą podobne do następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="006d4-174">The output is similar to the following text:</span></span>

    ```
    TABLE_CATALOG   TABLE_SCHEMA    TABLE_NAME      TABLE_TYPE
    databaseName       dbo     delays      BASE TABLE
    ```

5. <span data-ttu-id="006d4-175">Wprowadź `exit` na `1>` prompt wyjść z narzędzia tsql.</span><span class="sxs-lookup"><span data-stu-id="006d4-175">Enter `exit` at the `1>` prompt to exit the tsql utility.</span></span>

## <a name="export-data-with-sqoop"></a><span data-ttu-id="006d4-176">Eksportowanie danych z Sqoop</span><span class="sxs-lookup"><span data-stu-id="006d4-176">Export data with Sqoop</span></span>

1. <span data-ttu-id="006d4-177">Aby sprawdzić, czy Sqoop widzą bazy danych SQL, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="006d4-177">Use the following command to verify that Sqoop can see your SQL Database:</span></span>

    ```
    sqoop list-databases --connect jdbc:sqlserver://<serverName>.database.windows.net:1433 --username <adminLogin> --password <adminPassword>
    ```

    <span data-ttu-id="006d4-178">To polecenie zwraca listę baz danych, łącznie z bazy danych utworzone wcześniej tabeli opóźnienia.</span><span class="sxs-lookup"><span data-stu-id="006d4-178">This command returns a list of databases, including the database that you created the delays table in earlier.</span></span>

2. <span data-ttu-id="006d4-179">Eksportowanie danych z hivesampletable do tabeli mobiledata, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="006d4-179">Use the following command to export data from hivesampletable to the mobiledata table:</span></span>

    ```
    sqoop export --connect 'jdbc:sqlserver://<serverName>.database.windows.net:1433;database=<databaseName>' --username <adminLogin> --password <adminPassword> --table 'delays' --export-dir '/tutorials/flightdelays/output' --fields-terminated-by '\t' -m 1
    ```

    <span data-ttu-id="006d4-180">Sqoop nawiązuje połączenie z bazą danych zawierającą tabeli opóźnienia i eksportowanie danych `/tutorials/flightdelays/output` katalogu do tabeli opóźnienia.</span><span class="sxs-lookup"><span data-stu-id="006d4-180">Sqoop connects to the database containing the delays table, and exports data from the `/tutorials/flightdelays/output` directory to the delays table.</span></span>

3. <span data-ttu-id="006d4-181">Po zakończeniu wykonywania polecenia, użyj następujących funkcji do łączenia z bazą danych przy użyciu języka TSQL:</span><span class="sxs-lookup"><span data-stu-id="006d4-181">After the command completes, use the following to connect to the database using TSQL:</span></span>

    ```
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P <adminPassword> -p 1433 -D <databaseName>
    ```

    <span data-ttu-id="006d4-182">Po nawiązaniu połączenia, należy zastosować następujące instrukcje, aby sprawdzić, czy dane zostały wyeksportowane do tabeli mobiledata:</span><span class="sxs-lookup"><span data-stu-id="006d4-182">Once connected, use the following statements to verify that the data was exported to the mobiledata table:</span></span>

    ```
    SELECT * FROM delays
    GO
    ```

    <span data-ttu-id="006d4-183">Powinna zostać wyświetlona lista danych w tabeli.</span><span class="sxs-lookup"><span data-stu-id="006d4-183">You should see a listing of data in the table.</span></span> <span data-ttu-id="006d4-184">Typ `exit` aby wyjść z narzędzia tsql.</span><span class="sxs-lookup"><span data-stu-id="006d4-184">Type `exit` to exit the tsql utility.</span></span>

## <span data-ttu-id="006d4-185"><a id="nextsteps"></a> Następne kroki</span><span class="sxs-lookup"><span data-stu-id="006d4-185"><a id="nextsteps"></a> Next steps</span></span>

<span data-ttu-id="006d4-186">Aby dowiedzieć się więcej sposobów pracować z danymi w usłudze HDInsight, można znaleźć w następujących dokumentach:</span><span class="sxs-lookup"><span data-stu-id="006d4-186">To learn more ways to work with data in HDInsight, see the following documents:</span></span>

* <span data-ttu-id="006d4-187">[Korzystanie z programu Hive z usługą HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="006d4-187">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="006d4-188">[Korzystanie z Oozie z usługą HDInsight][hdinsight-use-oozie]</span><span class="sxs-lookup"><span data-stu-id="006d4-188">[Use Oozie with HDInsight][hdinsight-use-oozie]</span></span>
* <span data-ttu-id="006d4-189">[Korzystanie z usługą HDInsight Sqoop][hdinsight-use-sqoop]</span><span class="sxs-lookup"><span data-stu-id="006d4-189">[Use Sqoop with HDInsight][hdinsight-use-sqoop]</span></span>
* <span data-ttu-id="006d4-190">[Korzystanie z języka Pig z usługą HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="006d4-190">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="006d4-191">[Tworzenie programów Java MapReduce dla usługi HDInsight][hdinsight-develop-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="006d4-191">[Develop Java MapReduce programs for HDInsight][hdinsight-develop-mapreduce]</span></span>
* <span data-ttu-id="006d4-192">[Opracowywanie przesyłanie strumieniowe programów dla usługi HDInsight Hadoop języka Python][hdinsight-develop-streaming]</span><span class="sxs-lookup"><span data-stu-id="006d4-192">[Develop Python Hadoop streaming programs for HDInsight][hdinsight-develop-streaming]</span></span>

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
