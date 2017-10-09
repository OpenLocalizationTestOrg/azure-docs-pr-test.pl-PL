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
# <a name="use-hello-beeline-client-with-apache-hive"></a><span data-ttu-id="bd912-105">Apache Hive za pomocą klienta Beeline hello</span><span class="sxs-lookup"><span data-stu-id="bd912-105">Use hello Beeline client with Apache Hive</span></span>

<span data-ttu-id="bd912-106">Dowiedz się, jak toouse [Beeline](https://cwiki.apache.org/confluence/display/Hive/HiveServer2+Clients#HiveServer2Clients-Beeline–NewCommandLineShell) toorun Hive zapytania w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="bd912-106">Learn how toouse [Beeline](https://cwiki.apache.org/confluence/display/Hive/HiveServer2+Clients#HiveServer2Clients-Beeline–NewCommandLineShell) toorun Hive queries on HDInsight.</span></span>

<span data-ttu-id="bd912-107">Beeline jest klientem Hive, który znajduje się na powitania głównymi węzłami klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="bd912-107">Beeline is a Hive client that is included on hello head nodes of your HDInsight cluster.</span></span> <span data-ttu-id="bd912-108">Beeline używa tooHiveServer2 tooconnect JDBC, z usługą hostowaną w klastrze usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="bd912-108">Beeline uses JDBC tooconnect tooHiveServer2, a service hosted on your HDInsight cluster.</span></span> <span data-ttu-id="bd912-109">Umożliwia także Beeline tooaccess Hive w usłudze HDInsight zdalnie ponad hello internet.</span><span class="sxs-lookup"><span data-stu-id="bd912-109">You can also use Beeline tooaccess Hive on HDInsight remotely over hello internet.</span></span> <span data-ttu-id="bd912-110">Witaj w poniższej tabeli zawiera parametry połączenia do użycia z Beeline:</span><span class="sxs-lookup"><span data-stu-id="bd912-110">hello following table provides connection strings for use with Beeline:</span></span>

| <span data-ttu-id="bd912-111">Gdzie uruchomić Beeline z</span><span class="sxs-lookup"><span data-stu-id="bd912-111">Where you run Beeline from</span></span> | <span data-ttu-id="bd912-112">Parametry</span><span class="sxs-lookup"><span data-stu-id="bd912-112">Parameters</span></span> |
| --- | --- | --- |
| <span data-ttu-id="bd912-113">SSH tooa headnode lub krawędzi węzeł połączenia</span><span class="sxs-lookup"><span data-stu-id="bd912-113">An SSH connection tooa headnode or edge node</span></span> | `-u 'jdbc:hive2://headnodehost:10001/;transportMode=http'` |
| <span data-ttu-id="bd912-114">Poza hello klastra</span><span class="sxs-lookup"><span data-stu-id="bd912-114">Outside hello cluster</span></span> | `-u 'jdbc:hive2://clustername.azurehdinsight.net:443/;ssl=true;transportMode=http;httpPath=/hive2' -n admin -p password` |

> [!NOTE]
> <span data-ttu-id="bd912-115">Zastąp `admin` z hello konto logowania klastra dla klastra.</span><span class="sxs-lookup"><span data-stu-id="bd912-115">Replace `admin` with hello cluster login account for your cluster.</span></span>
>
> <span data-ttu-id="bd912-116">Zastąp `password` hello hasła konta logowania hello klastra.</span><span class="sxs-lookup"><span data-stu-id="bd912-116">Replace `password` with hello password for hello cluster login account.</span></span>
>
> <span data-ttu-id="bd912-117">Zastąp `clustername` o nazwie hello klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="bd912-117">Replace `clustername` with hello name of your HDInsight cluster.</span></span>

## <span data-ttu-id="bd912-118"><a id="prereq"></a>Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="bd912-118"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="bd912-119">Opartych na systemie Linux platformą Hadoop w klastrze usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="bd912-119">A Linux-based Hadoop on HDInsight cluster.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="bd912-120">Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="bd912-120">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="bd912-121">Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).</span><span class="sxs-lookup"><span data-stu-id="bd912-121">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="bd912-122">Klient SSH lub lokalnego klienta Beeline.</span><span class="sxs-lookup"><span data-stu-id="bd912-122">An SSH client or a local Beeline client.</span></span> <span data-ttu-id="bd912-123">Większość hello kroków w tym dokumencie przyjęto założenie, że używasz Beeline z klastra toohello sesji SSH.</span><span class="sxs-lookup"><span data-stu-id="bd912-123">Most of hello steps in this document assume that you are using Beeline from an SSH session toohello cluster.</span></span> <span data-ttu-id="bd912-124">Uzyskać informacji o działaniu Beeline z zewnątrz hello klastra, zobacz hello [zdalnie użyć Beeline](#remote) sekcji.</span><span class="sxs-lookup"><span data-stu-id="bd912-124">For information on running Beeline from outside hello cluster, see hello [use Beeline remotely](#remote) section.</span></span>

    <span data-ttu-id="bd912-125">Aby uzyskać więcej informacji o korzystaniu z protokołu SSH, zobacz [używanie SSH z usługą HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="bd912-125">For more information on using SSH, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <span data-ttu-id="bd912-126"><a id="beeline"></a>Użyj Beeline</span><span class="sxs-lookup"><span data-stu-id="bd912-126"><a id="beeline"></a>Use Beeline</span></span>

1. <span data-ttu-id="bd912-127">Podczas uruchamiania Beeline, musisz podać parametry połączenia dla serwera HiveServer2 w klastrze usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="bd912-127">When starting Beeline, you must provide a connection string for HiveServer2 on your HDInsight cluster.</span></span> <span data-ttu-id="bd912-128">polecenie hello toorun z zewnątrz hello klastra, musisz także podać nazwę konta logowania klastra hello (domyślna `admin`) i hasło.</span><span class="sxs-lookup"><span data-stu-id="bd912-128">toorun hello command from outside hello cluster, you must also provide hello cluster login account name (default `admin`) and password.</span></span> <span data-ttu-id="bd912-129">Należy użyć następującej tabeli toofind hello połączenia ciągu formatu i parametry toouse hello:</span><span class="sxs-lookup"><span data-stu-id="bd912-129">Use hello following table toofind hello connection string format and parameters toouse:</span></span>

    | <span data-ttu-id="bd912-130">Gdzie uruchomić Beeline z</span><span class="sxs-lookup"><span data-stu-id="bd912-130">Where you run Beeline from</span></span> | <span data-ttu-id="bd912-131">Parametry</span><span class="sxs-lookup"><span data-stu-id="bd912-131">Parameters</span></span> |
    | --- | --- | --- |
    | <span data-ttu-id="bd912-132">SSH tooa headnode lub krawędzi węzeł połączenia</span><span class="sxs-lookup"><span data-stu-id="bd912-132">An SSH connection tooa headnode or edge node</span></span> | `-u 'jdbc:hive2://headnodehost:10001/;transportMode=http'` |
    | <span data-ttu-id="bd912-133">Poza hello klastra</span><span class="sxs-lookup"><span data-stu-id="bd912-133">Outside hello cluster</span></span> | `-u 'jdbc:hive2://clustername.azurehdinsight.net:443/;ssl=true;transportMode=http;httpPath=/hive2' -n admin -p password` |

    <span data-ttu-id="bd912-134">Na przykład hello następujące polecenia mogą być używane toostart Beeline z klastra toohello sesji SSH:</span><span class="sxs-lookup"><span data-stu-id="bd912-134">For example, hello following command can be used toostart Beeline from an SSH session toohello cluster:</span></span>

    ```bash
    beeline -u 'jdbc:hive2://headnodehost:10001/;transportMode=http'
    ```

    <span data-ttu-id="bd912-135">To polecenie uruchamia powitania klienta Beeline i łączy tooHiveServer2 na powitania węzła głównego klastra.</span><span class="sxs-lookup"><span data-stu-id="bd912-135">This command starts hello Beeline client, and connects tooHiveServer2 on hello cluster head node.</span></span> <span data-ttu-id="bd912-136">Po zakończeniu wykonywania polecenia hello przyjeździe `jdbc:hive2://headnodehost:10001/>` wiersza.</span><span class="sxs-lookup"><span data-stu-id="bd912-136">Once hello command completes, you arrive at a `jdbc:hive2://headnodehost:10001/>` prompt.</span></span>

2. <span data-ttu-id="bd912-137">Polecenia beeline rozpoczynać się od `!` znaków, na przykład `!help` Wyświetla Pomoc.</span><span class="sxs-lookup"><span data-stu-id="bd912-137">Beeline commands begin with a `!` character, for example `!help` displays help.</span></span> <span data-ttu-id="bd912-138">Jednak hello `!` można pominąć w przypadku niektórych poleceń.</span><span class="sxs-lookup"><span data-stu-id="bd912-138">However hello `!` can be omitted for some commands.</span></span> <span data-ttu-id="bd912-139">Na przykład `help` działa.</span><span class="sxs-lookup"><span data-stu-id="bd912-139">For example, `help` also works.</span></span>

    <span data-ttu-id="bd912-140">Brak `!sql`, która jest używana tooexecute instrukcje HiveQL.</span><span class="sxs-lookup"><span data-stu-id="bd912-140">There is a `!sql`, which is used tooexecute HiveQL statements.</span></span> <span data-ttu-id="bd912-141">Jednak HiveQL używa się tak najczęściej pominąć hello poprzedniego `!sql`.</span><span class="sxs-lookup"><span data-stu-id="bd912-141">However, HiveQL is so commonly used that you can omit hello preceding `!sql`.</span></span> <span data-ttu-id="bd912-142">następujące dwie instrukcje Hello są równoważne:</span><span class="sxs-lookup"><span data-stu-id="bd912-142">hello following two statements are equivalent:</span></span>

    ```hiveql
    !sql show tables;
    show tables;
    ```

    <span data-ttu-id="bd912-143">W nowym klastrze, znajduje się tylko jedną tabelę: **hivesampletable**.</span><span class="sxs-lookup"><span data-stu-id="bd912-143">On a new cluster, only one table is listed: **hivesampletable**.</span></span>

3. <span data-ttu-id="bd912-144">Użyj następującego polecenia toodisplay hello schematu dla hello hivesampletable hello:</span><span class="sxs-lookup"><span data-stu-id="bd912-144">Use hello following command toodisplay hello schema for hello hivesampletable:</span></span>

    ```hiveql
    describe hivesampletable;
    ```

    <span data-ttu-id="bd912-145">To polecenie zwraca hello następujących informacji:</span><span class="sxs-lookup"><span data-stu-id="bd912-145">This command returns hello following information:</span></span>

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

    <span data-ttu-id="bd912-146">Te informacje w tym artykule opisano hello kolumn w tabeli hello.</span><span class="sxs-lookup"><span data-stu-id="bd912-146">This information describes hello columns in hello table.</span></span> <span data-ttu-id="bd912-147">Gdy można wykonać niektóre zapytań dotyczących tych danych, zamiast tego utwórz nowy toodemonstrate tabeli jak tooload danych do gałęzi i zastosowanie schematu.</span><span class="sxs-lookup"><span data-stu-id="bd912-147">While we could perform some queries against this data, let's instead create a brand new table toodemonstrate how tooload data into Hive and apply a schema.</span></span>

4. <span data-ttu-id="bd912-148">Wprowadź następujące instrukcje toocreate tabela o nazwie hello **log4jLogs** przy użyciu dostarczonych z klastrem usługi HDInsight hello przykładowych danych:</span><span class="sxs-lookup"><span data-stu-id="bd912-148">Enter hello following statements toocreate a table named **log4jLogs** by using sample data provided with hello HDInsight cluster:</span></span>

    ```hiveql
    DROP TABLE log4jLogs;
    CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
    STORED AS TEXTFILE LOCATION 'wasb:///example/data/';
    SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;
    ```

    <span data-ttu-id="bd912-149">Instrukcje te należy wykonać hello następujące akcje:</span><span class="sxs-lookup"><span data-stu-id="bd912-149">These statements perform hello following actions:</span></span>

    * <span data-ttu-id="bd912-150">`DROP TABLE`— W przypadku hello tabela istnieje, zostaną usunięte.</span><span class="sxs-lookup"><span data-stu-id="bd912-150">`DROP TABLE` - If hello table exists, it is deleted.</span></span>

    * <span data-ttu-id="bd912-151">`CREATE EXTERNAL TABLE`-Tworzy **zewnętrznych** tabeli w gałęzi rejestru.</span><span class="sxs-lookup"><span data-stu-id="bd912-151">`CREATE EXTERNAL TABLE` - Creates an **external** table in Hive.</span></span> <span data-ttu-id="bd912-152">Tabele zewnętrzne przechowywać tylko hello definicji tabeli w gałęzi.</span><span class="sxs-lookup"><span data-stu-id="bd912-152">External tables only store hello table definition in Hive.</span></span> <span data-ttu-id="bd912-153">Hello danych pozostaje w hello oryginalnej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="bd912-153">hello data is left in hello original location.</span></span>

    * <span data-ttu-id="bd912-154">`ROW FORMAT`— Sposób formatowania danych hello.</span><span class="sxs-lookup"><span data-stu-id="bd912-154">`ROW FORMAT` - How hello data is formatted.</span></span> <span data-ttu-id="bd912-155">W takim przypadku hello pól w każdym dzienniku są oddzielone spacją.</span><span class="sxs-lookup"><span data-stu-id="bd912-155">In this case, hello fields in each log are separated by a space.</span></span>

    * <span data-ttu-id="bd912-156">`STORED AS TEXTFILE LOCATION`— W przypadku gdy hello dane są przechowywane i w jaki format pliku.</span><span class="sxs-lookup"><span data-stu-id="bd912-156">`STORED AS TEXTFILE LOCATION` - Where hello data is stored and in what file format.</span></span>

    * <span data-ttu-id="bd912-157">`SELECT`-Wybiera liczbę wszystkich wierszy gdzie kolumna **t4** zawiera wartość hello **[Błąd]**.</span><span class="sxs-lookup"><span data-stu-id="bd912-157">`SELECT` - Selects a count of all rows where column **t4** contains hello value **[ERROR]**.</span></span> <span data-ttu-id="bd912-158">To zapytanie zwraca wartość **3** są trzy wiersze, które zawierają tę wartość.</span><span class="sxs-lookup"><span data-stu-id="bd912-158">This query returns a value of **3** as there are three rows that contain this value.</span></span>

    * <span data-ttu-id="bd912-159">`INPUT__FILE__NAME LIKE '%.log'`-Hive prób tooapply hello schematu tooall pliki w katalogu hello.</span><span class="sxs-lookup"><span data-stu-id="bd912-159">`INPUT__FILE__NAME LIKE '%.log'` - Hive attempts tooapply hello schema tooall files in hello directory.</span></span> <span data-ttu-id="bd912-160">W takim przypadku hello katalog zawiera pliki, które nie są zgodne hello schematu.</span><span class="sxs-lookup"><span data-stu-id="bd912-160">In this case, hello directory contains files that do not match hello schema.</span></span> <span data-ttu-id="bd912-161">tooprevent odzyskiwanie danych w wynikach hello, niniejszych informuje Hive czy firma Microsoft powinno zwrócić dane tylko z plików w. dziennika.</span><span class="sxs-lookup"><span data-stu-id="bd912-161">tooprevent garbage data in hello results, this statement tells Hive that we should only return data from files ending in .log.</span></span>

  > [!NOTE]
  > <span data-ttu-id="bd912-162">Jeśli oczekujesz hello zaktualizowane przez źródło zewnętrzne podstawowej toobe danych należy użyć tabel zewnętrznych.</span><span class="sxs-lookup"><span data-stu-id="bd912-162">External tables should be used when you expect hello underlying data toobe updated by an external source.</span></span> <span data-ttu-id="bd912-163">Na przykład procesu przekazywania danych lub operacja MapReduce.</span><span class="sxs-lookup"><span data-stu-id="bd912-163">For example, an automated data upload process or a MapReduce operation.</span></span>
  >
  > <span data-ttu-id="bd912-164">Usunięcie tabeli zewnętrznej jest **nie** usunąć dane hello, tylko hello definicji tabeli.</span><span class="sxs-lookup"><span data-stu-id="bd912-164">Dropping an external table does **not** delete hello data, only hello table definition.</span></span>

    <span data-ttu-id="bd912-165">Witaj danych wyjściowych tego polecenia jest podobne toohello następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="bd912-165">hello output of this command is similar toohello following text:</span></span>

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

5. <span data-ttu-id="bd912-166">Użyj tooexit Beeline, `!exit`.</span><span class="sxs-lookup"><span data-stu-id="bd912-166">tooexit Beeline, use `!exit`.</span></span>

## <span data-ttu-id="bd912-167"><a id="file"></a>Użyj toorun Beeline pliku HiveQL</span><span class="sxs-lookup"><span data-stu-id="bd912-167"><a id="file"></a>Use Beeline toorun a HiveQL file</span></span>

<span data-ttu-id="bd912-168">Użyj hello następujące kroki toocreate pliku, i uruchom go za pomocą Beeline.</span><span class="sxs-lookup"><span data-stu-id="bd912-168">Use hello following steps toocreate a file, then run it using Beeline.</span></span>

1. <span data-ttu-id="bd912-169">Użyj hello następujące polecenie toocreate plik o nazwie **query.hql**:</span><span class="sxs-lookup"><span data-stu-id="bd912-169">Use hello following command toocreate a file named **query.hql**:</span></span>

    ```bash
    nano query.hql
    ```

2. <span data-ttu-id="bd912-170">Użyj następującego tekstu jako hello zawartość pliku hello hello.</span><span class="sxs-lookup"><span data-stu-id="bd912-170">Use hello following text as hello contents of hello file.</span></span> <span data-ttu-id="bd912-171">To zapytanie tworzy nową tabelę "internal" o nazwie **errorLogs**:</span><span class="sxs-lookup"><span data-stu-id="bd912-171">This query creates a new 'internal' table named **errorLogs**:</span></span>

    ```hiveql
    CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) STORED AS ORC;
    INSERT OVERWRITE TABLE errorLogs SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log';
    ```

    <span data-ttu-id="bd912-172">Instrukcje te należy wykonać hello następujące akcje:</span><span class="sxs-lookup"><span data-stu-id="bd912-172">These statements perform hello following actions:</span></span>

    * <span data-ttu-id="bd912-173">**Utwórz Tabela Jeśli nie ISTNIEJE** — Jeśli tabeli hello jeszcze nie istnieje, jest tworzony.</span><span class="sxs-lookup"><span data-stu-id="bd912-173">**CREATE TABLE IF NOT EXISTS** - If hello table does not already exist, it is created.</span></span> <span data-ttu-id="bd912-174">Ponieważ hello **zewnętrznych** — słowo kluczowe nie jest używany, ta instrukcja tworzy wewnętrznej tabeli.</span><span class="sxs-lookup"><span data-stu-id="bd912-174">Since hello **EXTERNAL** keyword is not used, this statement creates an internal table.</span></span> <span data-ttu-id="bd912-175">Wewnętrzny tabele są przechowywane w magazynie danych hello Hive i całkowicie zarządza Hive.</span><span class="sxs-lookup"><span data-stu-id="bd912-175">Internal tables are stored in hello Hive data warehouse and are managed completely by Hive.</span></span>
    * <span data-ttu-id="bd912-176">**ORC AS PRZECHOWYWANE** -przechowuje dane hello w formacie zoptymalizowanych pod kątem wiersza kolumnowy (ORC).</span><span class="sxs-lookup"><span data-stu-id="bd912-176">**STORED AS ORC** - Stores hello data in Optimized Row Columnar (ORC) format.</span></span> <span data-ttu-id="bd912-177">ORC format jest wysoce zoptymalizowane i wydajne formatu do przechowywania danych Hive.</span><span class="sxs-lookup"><span data-stu-id="bd912-177">ORC format is a highly optimized and efficient format for storing Hive data.</span></span>
    * <span data-ttu-id="bd912-178">**ZASTĄP INSERT... Wybierz** -wybiera wiersze z hello **log4jLogs** tabeli, która zawiera **[Błąd]**, a następnie wstawia hello danych do hello **errorLogs** tabeli.</span><span class="sxs-lookup"><span data-stu-id="bd912-178">**INSERT OVERWRITE ... SELECT** - Selects rows from hello **log4jLogs** table that contain **[ERROR]**, then inserts hello data into hello **errorLogs** table.</span></span>

    > [!NOTE]
    > <span data-ttu-id="bd912-179">W przeciwieństwie do tabel zewnętrznych porzucenie wewnętrznej tabeli usuwa hello również danych źródłowych.</span><span class="sxs-lookup"><span data-stu-id="bd912-179">Unlike external tables, dropping an internal table deletes hello underlying data as well.</span></span>

3. <span data-ttu-id="bd912-180">toosave hello pliku, użyj **Ctrl**+**_X**, wprowadź **Y**, a na końcu **Enter**.</span><span class="sxs-lookup"><span data-stu-id="bd912-180">toosave hello file, use **Ctrl**+**_X**, then enter **Y**, and finally **Enter**.</span></span>

4. <span data-ttu-id="bd912-181">Użyj następującego pliku hello toorun przy użyciu Beeline hello:</span><span class="sxs-lookup"><span data-stu-id="bd912-181">Use hello following toorun hello file using Beeline:</span></span>

    ```bash
    beeline -u 'jdbc:hive2://headnodehost:10001/;transportMode=http' -i query.hql
    ```

    > [!NOTE]
    > <span data-ttu-id="bd912-182">Witaj `-i` parametru rozpoczyna Beeline, uruchamia hello instrukcje w pliku query.hql hello.</span><span class="sxs-lookup"><span data-stu-id="bd912-182">hello `-i` parameter starts Beeline, runs hello statements in hello query.hql file.</span></span> <span data-ttu-id="bd912-183">Po wykonaniu kwerendy hello przyjeździe hello `jdbc:hive2://headnodehost:10001/>` wiersza.</span><span class="sxs-lookup"><span data-stu-id="bd912-183">Once hello query completes, you arrive at hello `jdbc:hive2://headnodehost:10001/>` prompt.</span></span> <span data-ttu-id="bd912-184">Można również uruchomić plik za pomocą hello `-f` parametr, który zamyka Beeline po zakończeniu hello zapytania.</span><span class="sxs-lookup"><span data-stu-id="bd912-184">You can also run a file using hello `-f` parameter, which exits Beeline after hello query completes.</span></span>

5. <span data-ttu-id="bd912-185">tooverify, który hello **errorLogs** tabela została utworzona, użyj powitania po instrukcji tooreturn hello wszystkie wiersze z **errorLogs**:</span><span class="sxs-lookup"><span data-stu-id="bd912-185">tooverify that hello **errorLogs** table was created, use hello following statement tooreturn all hello rows from **errorLogs**:</span></span>

    ```hiveql
    SELECT * from errorLogs;
    ```

    <span data-ttu-id="bd912-186">Trzy wiersze danych ma zostać zwrócony, zawierający wszystkie **[Błąd]** w kolumnie t4:</span><span class="sxs-lookup"><span data-stu-id="bd912-186">Three rows of data should be returned, all containing **[ERROR]** in column t4:</span></span>

        +---------------+---------------+---------------+---------------+---------------+---------------+---------------+--+
        | errorlogs.t1  | errorlogs.t2  | errorlogs.t3  | errorlogs.t4  | errorlogs.t5  | errorlogs.t6  | errorlogs.t7  |
        +---------------+---------------+---------------+---------------+---------------+---------------+---------------+--+
        | 2012-02-03    | 18:35:34      | SampleClass0  | [ERROR]       | incorrect     | id            |               |
        | 2012-02-03    | 18:55:54      | SampleClass1  | [ERROR]       | incorrect     | id            |               |
        | 2012-02-03    | 19:25:27      | SampleClass4  | [ERROR]       | incorrect     | id            |               |
        +---------------+---------------+---------------+---------------+---------------+---------------+---------------+--+
        3 rows selected (1.538 seconds)

## <span data-ttu-id="bd912-187"><a id="remote"></a>Użyj Beeline zdalnie</span><span class="sxs-lookup"><span data-stu-id="bd912-187"><a id="remote"></a>Use Beeline remotely</span></span>

<span data-ttu-id="bd912-188">Jeśli masz Beeline zainstalowane lokalnie lub jest ona używana przez obraz Docker takich jak [sutoiku/beeline](https://hub.docker.com/r/sutoiku/beeline/), należy użyć hello następujące parametry:</span><span class="sxs-lookup"><span data-stu-id="bd912-188">If you have Beeline installed locally, or are using it through a Docker image such as [sutoiku/beeline](https://hub.docker.com/r/sutoiku/beeline/), you must use hello following parameters:</span></span>

* <span data-ttu-id="bd912-189">__Parametry połączenia__:`-u 'jdbc:hive2://clustername.azurehdinsight.net:443/;ssl=true;transportMode=http;httpPath=/hive2'`</span><span class="sxs-lookup"><span data-stu-id="bd912-189">__Connection string__: `-u 'jdbc:hive2://clustername.azurehdinsight.net:443/;ssl=true;transportMode=http;httpPath=/hive2'`</span></span>

* <span data-ttu-id="bd912-190">__Nazwa logowania klastra__:`-n admin`</span><span class="sxs-lookup"><span data-stu-id="bd912-190">__Cluster login name__: `-n admin`</span></span>

* <span data-ttu-id="bd912-191">__Hasło logowania klastra__`-p 'password'`</span><span class="sxs-lookup"><span data-stu-id="bd912-191">__Cluster login password__ `-p 'password'`</span></span>

<span data-ttu-id="bd912-192">Zastąp hello `clustername` w parametrach połączenia hello o nazwie hello klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="bd912-192">Replace hello `clustername` in hello connection string with hello name of your HDInsight cluster.</span></span>

<span data-ttu-id="bd912-193">Zastąp `admin` o nazwie hello logowania do klastra i Zastąp `password` z hello hasło do logowania do klastra.</span><span class="sxs-lookup"><span data-stu-id="bd912-193">Replace `admin` with hello name of your cluster login, and replace `password` with hello password for your cluster login.</span></span>

## <span data-ttu-id="bd912-194"><a id="sparksql"></a>Beeline za pomocą Spark</span><span class="sxs-lookup"><span data-stu-id="bd912-194"><a id="sparksql"></a>Use Beeline with Spark</span></span>

<span data-ttu-id="bd912-195">Platforma Spark zawiera własną implementację serwera HiveServer2, które są często serwera Spark Thrift hello tooas określonej.</span><span class="sxs-lookup"><span data-stu-id="bd912-195">Spark provides its own implementation of HiveServer2, which is often refered tooas hello Spark Thrift server.</span></span> <span data-ttu-id="bd912-196">Ta usługa korzysta z zapytań Spark SQL tooresolve zamiast Hive i może zapewnić lepszą wydajność, w zależności od tego zapytania.</span><span class="sxs-lookup"><span data-stu-id="bd912-196">This service uses Spark SQL tooresolve queries instead of Hive, and may provide better performance depending on your query.</span></span>

<span data-ttu-id="bd912-197">serwera Spark Thrift toohello tooconnect platformy Spark w klastrze usługi HDInsight, używać portów `10002` zamiast `10001`.</span><span class="sxs-lookup"><span data-stu-id="bd912-197">tooconnect toohello Spark Thrift server of a Spark on HDInsight cluster, use port `10002` instead of `10001`.</span></span> <span data-ttu-id="bd912-198">Na przykład `beeline -u 'jdbc:hive2://headnodehost:10002/;transportMode=http'`.</span><span class="sxs-lookup"><span data-stu-id="bd912-198">For example, `beeline -u 'jdbc:hive2://headnodehost:10002/;transportMode=http'`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bd912-199">serwera Spark Thrift Hello jest nie bezpośrednio dostępny przez hello internet.</span><span class="sxs-lookup"><span data-stu-id="bd912-199">hello Spark Thrift server is not directly accessible over hello internet.</span></span> <span data-ttu-id="bd912-200">Można połączyć tooit w sesji SSH lub tylko wewnątrz hello tej samej sieci wirtualnej Azure, jak hello klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="bd912-200">You can only connect tooit from an SSH session or inside hello same Azure Virtual Network as hello HDInsight cluster.</span></span>

## <span data-ttu-id="bd912-201"><a id="summary"></a><a id="nextsteps"></a>Następne kroki</span><span class="sxs-lookup"><span data-stu-id="bd912-201"><a id="summary"></a><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="bd912-202">Bardziej ogólne informacje na temat Hive w usłudze HDInsight zobacz następujące dokumentu hello:</span><span class="sxs-lookup"><span data-stu-id="bd912-202">For more general information on Hive in HDInsight, see hello following document:</span></span>

* [<span data-ttu-id="bd912-203">Korzystanie z programu Hive z usługą Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="bd912-203">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="bd912-204">Aby uzyskać więcej informacji na temat innych sposobów może pracować z platformą Hadoop w usłudze HDInsight, zobacz powitania po dokumentów:</span><span class="sxs-lookup"><span data-stu-id="bd912-204">For more information on other ways you can work with Hadoop on HDInsight, see hello following documents:</span></span>

* [<span data-ttu-id="bd912-205">Korzystanie z języka Pig z usługą Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="bd912-205">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="bd912-206">Używanie MapReduce z usługą Hadoop w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="bd912-206">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="bd912-207">Jeśli używasz aplikacji Tez przy użyciu Hive, zobacz powitania po dokumentów:</span><span class="sxs-lookup"><span data-stu-id="bd912-207">If you are using Tez with Hive, see hello following documents:</span></span>

* [<span data-ttu-id="bd912-208">Użyj hello Tez interfejsu użytkownika w usłudze HDInsight z systemu Windows</span><span class="sxs-lookup"><span data-stu-id="bd912-208">Use hello Tez UI on Windows-based HDInsight</span></span>](hdinsight-debug-tez-ui.md)
* [<span data-ttu-id="bd912-209">Użyj hello widoku Ambari Tez w HDInsight opartych na systemie Linux</span><span class="sxs-lookup"><span data-stu-id="bd912-209">Use hello Ambari Tez view on Linux-based HDInsight</span></span>](hdinsight-debug-ambari-tez-view.md)

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
