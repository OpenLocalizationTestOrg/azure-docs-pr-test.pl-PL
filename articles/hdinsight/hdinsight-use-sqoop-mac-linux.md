---
title: "Apache Sqoop z platformą Hadoop — usługa Azure HDInsight | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak używać narzędzia Apache Sqoop do importowania i eksportowania między Hadoop w usłudze HDInsight i bazy danych SQL Azure."
editor: cgronlun
manager: jhubbard
services: hdinsight
documentationcenter: 
author: Blackmist
tags: azure-portal
keywords: hadoop sqoop, sqoop
ms.assetid: 303649a5-4be5-4933-bf1d-4b232083c354
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: larryfr
ms.openlocfilehash: 35dcbb91e6af1480685c9fd5b829c54277c1c605
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="use-apache-sqoop-to-import-and-export-data-between-hadoop-on-hdinsight-and-sql-database"></a><span data-ttu-id="2475e-104">Apache Sqoop umożliwia importowanie i eksportowanie danych między Hadoop w usłudze HDInsight i bazy danych SQL</span><span class="sxs-lookup"><span data-stu-id="2475e-104">Use Apache Sqoop to import and export data between Hadoop on HDInsight and SQL Database</span></span>

[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

<span data-ttu-id="2475e-105">Dowiedz się, jak używać narzędzia Apache Sqoop importowania i eksportowania między klastrem usługi Hadoop w usłudze Azure HDInsight i bazy danych Azure SQL Database lub programu Microsoft SQL Server.</span><span class="sxs-lookup"><span data-stu-id="2475e-105">Learn how to use Apache Sqoop to import and export between a Hadoop cluster in Azure HDInsight and Azure SQL Database or Microsoft SQL Server database.</span></span> <span data-ttu-id="2475e-106">Użyj dokumentów z krokami w tym `sqoop` polecenia bezpośrednio z headnode klastra usługi Hadoop.</span><span class="sxs-lookup"><span data-stu-id="2475e-106">The steps in this document use the `sqoop` command directly from the headnode of the Hadoop cluster.</span></span> <span data-ttu-id="2475e-107">SSH umożliwia łączenie z węzłem głównym, a następnie uruchom polecenia w tym dokumencie.</span><span class="sxs-lookup"><span data-stu-id="2475e-107">You use SSH to connect to the head node and run the commands in this document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2475e-108">Kroki opisane w tym dokumencie pracować tylko z klastrami usługi HDInsight, które używają systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="2475e-108">The steps in this document only work with HDInsight clusters that use Linux.</span></span> <span data-ttu-id="2475e-109">Linux jest jedynym systemem operacyjnym używanym w połączeniu z usługą HDInsight w wersji 3.4 lub nowszą.</span><span class="sxs-lookup"><span data-stu-id="2475e-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="2475e-110">Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).</span><span class="sxs-lookup"><span data-stu-id="2475e-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="install-freetds"></a><span data-ttu-id="2475e-111">Zainstaluj protokół FreeTDS</span><span class="sxs-lookup"><span data-stu-id="2475e-111">Install FreeTDS</span></span>

1. <span data-ttu-id="2475e-112">Używanie protokołu SSH, aby połączyć się z klastrem usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2475e-112">Use SSH to connect to the HDInsight cluster.</span></span> <span data-ttu-id="2475e-113">Na przykład następujące polecenie nawiązuje połączenie z podstawowym headnode klastra o nazwie `mycluster`:</span><span class="sxs-lookup"><span data-stu-id="2475e-113">For example, the following command connects to the primary headnode of a cluster named `mycluster`:</span></span>

    ```bash
    ssh CLUSTERNAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="2475e-114">Aby uzyskać więcej informacji, zobacz [Używanie protokołu SSH w usłudze HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="2475e-114">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="2475e-115">Aby zainstalować protokół FreeTDS, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="2475e-115">Use the following command to install FreeTDS:</span></span>

    ```bash
    sudo apt --assume-yes install freetds-dev freetds-bin
    ```

    <span data-ttu-id="2475e-116">Protokół FreeTDS jest używany w kilku etapach nawiązać połączenia z bazą danych SQL.</span><span class="sxs-lookup"><span data-stu-id="2475e-116">FreeTDS is used in several steps to connect to SQL Database.</span></span>

## <a name="create-the-table-in-sql-database"></a><span data-ttu-id="2475e-117">Tworzenie tabeli w bazie danych SQL</span><span class="sxs-lookup"><span data-stu-id="2475e-117">Create the table in SQL Database</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2475e-118">Jeśli korzystasz z klastrem usługi HDInsight i tworzenie bazy danych SQL w [Tworzenie klastra i bazy danych SQL](hdinsight-use-sqoop.md), pomiń kroki opisane w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="2475e-118">If you are using the HDInsight cluster and SQL Database created in [Create cluster and SQL database](hdinsight-use-sqoop.md), skip the steps in this section.</span></span> <span data-ttu-id="2475e-119">Bazy danych i tabeli zostały utworzone jako część kroki [Tworzenie klastra i bazy danych SQL](hdinsight-use-sqoop.md) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="2475e-119">The database and table were created as part of the steps in the [Create cluster and SQL database](hdinsight-use-sqoop.md) document.</span></span>

1. <span data-ttu-id="2475e-120">W sesji SSH wpisz następujące polecenie, aby połączyć się z serwerem bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="2475e-120">From the SSH session, use the following command to connect to the SQL Database server.</span></span>

        TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P <adminPassword> -p 1433 -D sqooptest

    <span data-ttu-id="2475e-121">Pojawi się dane wyjściowe podobne do następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="2475e-121">You receive output similar to the following text:</span></span>

        locale is "en_US.UTF-8"
        locale charset is "UTF-8"
        using default charset "UTF-8"
        Default database being set to sqooptest
        1>

2. <span data-ttu-id="2475e-122">W `1>` monit, wprowadź następujące zapytanie:</span><span class="sxs-lookup"><span data-stu-id="2475e-122">At the `1>` prompt, enter the following query:</span></span>

    ```sql
    CREATE TABLE [dbo].[mobiledata](
    [clientid] [nvarchar](50),
    [querytime] [nvarchar](50),
    [market] [nvarchar](50),
    [deviceplatform] [nvarchar](50),
    [devicemake] [nvarchar](50),
    [devicemodel] [nvarchar](50),
    [state] [nvarchar](50),
    [country] [nvarchar](50),
    [querydwelltime] [float],
    [sessionid] [bigint],
    [sessionpagevieworder] [bigint])
    GO
    CREATE CLUSTERED INDEX mobiledata_clustered_index on mobiledata(clientid)
    GO
    ```

    <span data-ttu-id="2475e-123">Gdy `GO` instrukcja została wprowadzona, poprzednie instrukcje są oceniane.</span><span class="sxs-lookup"><span data-stu-id="2475e-123">When the `GO` statement is entered, the previous statements are evaluated.</span></span> <span data-ttu-id="2475e-124">Najpierw **mobiledata** tabela została utworzona, a następnie indeks klastrowany zostaną dodane do niego (wymagane przez usługę SQL Database).</span><span class="sxs-lookup"><span data-stu-id="2475e-124">First, the **mobiledata** table is created, then a clustered index is added to it (required by SQL Database.)</span></span>

    <span data-ttu-id="2475e-125">Użyj następującego zapytania, aby sprawdzić, czy tabela została utworzona:</span><span class="sxs-lookup"><span data-stu-id="2475e-125">Use the following query to verify that the table has been created:</span></span>

    ```sql
    SELECT * FROM information_schema.tables
    GO
    ```

    <span data-ttu-id="2475e-126">Zostaną wyświetlone dane wyjściowe podobne do następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="2475e-126">You see output similar to the following text:</span></span>

        TABLE_CATALOG   TABLE_SCHEMA    TABLE_NAME      TABLE_TYPE
        sqooptest       dbo     mobiledata      BASE TABLE

3. <span data-ttu-id="2475e-127">Wprowadź `exit` na `1>` prompt wyjść z narzędzia tsql.</span><span class="sxs-lookup"><span data-stu-id="2475e-127">Enter `exit` at the `1>` prompt to exit the tsql utility.</span></span>

## <a name="sqoop-export"></a><span data-ttu-id="2475e-128">Sqoop eksportu</span><span class="sxs-lookup"><span data-stu-id="2475e-128">Sqoop export</span></span>

1. <span data-ttu-id="2475e-129">Połączenie SSH do klastra użyj następującego polecenia, aby sprawdzić, czy Sqoop widzą bazy danych SQL:</span><span class="sxs-lookup"><span data-stu-id="2475e-129">From the SSH connection to the cluster, use the following command to verify that Sqoop can see your SQL Database:</span></span>

    ```bash
    sqoop list-databases --connect jdbc:sqlserver://<serverName>.database.windows.net:1433 --username <adminLogin> -P
    ```
    <span data-ttu-id="2475e-130">Po wyświetleniu monitu wprowadź hasło dla nazwy logowania bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="2475e-130">When prompted, enter the password for the SQL Database login.</span></span>

    <span data-ttu-id="2475e-131">To polecenie zwraca listę baz danych, w tym **sqooptest** bazy danych, który został utworzony wcześniej.</span><span class="sxs-lookup"><span data-stu-id="2475e-131">This command returns a list of databases, including the **sqooptest** database that you created earlier.</span></span>

2. <span data-ttu-id="2475e-132">Aby wyeksportować dane z **hivesampletable** do **mobiledata** tabeli, należy użyć następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="2475e-132">To export data from **hivesampletable** to the **mobiledata** table, use the following command:</span></span>

    ```bash
    sqoop export --connect 'jdbc:sqlserver://<serverName>.database.windows.net:1433;database=sqooptest' --username <adminLogin> -P --table 'mobiledata' --export-dir 'wasb:///hive/warehouse/hivesampletable' --fields-terminated-by '\t' -m 1
    ```

    <span data-ttu-id="2475e-133">To polecenie powoduje, że Sqoop nawiązać **sqooptest** bazy danych.</span><span class="sxs-lookup"><span data-stu-id="2475e-133">This command instructs Sqoop to connect to the **sqooptest** database.</span></span> <span data-ttu-id="2475e-134">Sqoop następnie eksportuje dane z **wasb: / / / gałęzi/magazynu/hivesampletable** do **mobiledata** tabeli.</span><span class="sxs-lookup"><span data-stu-id="2475e-134">Sqoop then exports data from **wasb:///hive/warehouse/hivesampletable** to the **mobiledata** table.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="2475e-135">Użyj `wasb:///` Jeśli konta usługi Azure Storage jest domyślny magazyn dla klastra.</span><span class="sxs-lookup"><span data-stu-id="2475e-135">Use `wasb:///` if the default storage for your cluster is an Azure Storage account.</span></span> <span data-ttu-id="2475e-136">Użyj `adl:///` przypadku usługi Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="2475e-136">Use `adl:///` if it is an Azure Data Lake Store.</span></span>

3. <span data-ttu-id="2475e-137">Po zakończeniu wykonywania polecenia, użyj następującego polecenia do łączenia z bazą danych przy użyciu języka TSQL:</span><span class="sxs-lookup"><span data-stu-id="2475e-137">After the command completes, use the following command to connect to the database using TSQL:</span></span>

    ```bash
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P -p 1433 -D sqooptest
    ```

    <span data-ttu-id="2475e-138">Po nawiązaniu połączenia użyj następujące instrukcje, aby sprawdzić, czy dane został wyeksportowany do **mobiledata** tabeli:</span><span class="sxs-lookup"><span data-stu-id="2475e-138">Once connected, use the following statements to verify that the data was exported to the **mobiledata** table:</span></span>

    ```sql
    SET ROWCOUNT 50;
    SELECT * FROM mobiledata
    GO
    ```

    <span data-ttu-id="2475e-139">Powinna zostać wyświetlona lista danych w tabeli.</span><span class="sxs-lookup"><span data-stu-id="2475e-139">You should see a listing of data in the table.</span></span> <span data-ttu-id="2475e-140">Typ `exit` aby wyjść z narzędzia tsql.</span><span class="sxs-lookup"><span data-stu-id="2475e-140">Type `exit` to exit the tsql utility.</span></span>

## <a name="sqoop-import"></a><span data-ttu-id="2475e-141">Importuj Sqoop</span><span class="sxs-lookup"><span data-stu-id="2475e-141">Sqoop import</span></span>

1. <span data-ttu-id="2475e-142">Użyj następującego polecenia do importowania danych z **mobiledata** do tabeli w bazie danych SQL, **wasb: / / / samouczki/usesqoop/importeddata** katalogu w usłudze HDInsight:</span><span class="sxs-lookup"><span data-stu-id="2475e-142">Use the following command to import data from the **mobiledata** table in SQL Database, to the **wasb:///tutorials/usesqoop/importeddata** directory on HDInsight:</span></span>

    ```bash
    sqoop import --connect 'jdbc:sqlserver://<serverName>.database.windows.net:1433;database=sqooptest' --username <adminLogin> --password <adminPassword> --table 'mobiledata' --target-dir 'wasb:///tutorials/usesqoop/importeddata' --fields-terminated-by '\t' --lines-terminated-by '\n' -m 1
    ```

    <span data-ttu-id="2475e-143">Pola są oddzielone znak tabulacji, a wiersze kończą się znakiem nowego wiersza.</span><span class="sxs-lookup"><span data-stu-id="2475e-143">The fields in the data are separated by a tab character, and the lines are terminated by a new-line character.</span></span>

2. <span data-ttu-id="2475e-144">Po zakończeniu importowania, użyj następującego polecenia do listy limit danych w nowym katalogu:</span><span class="sxs-lookup"><span data-stu-id="2475e-144">Once the import has completed, use the following command to list out the data in the new directory:</span></span>

    ```bash
    hdfs dfs -text /tutorials/usesqoop/importeddata/part-m-00000
    ```

## <a name="using-sql-server"></a><span data-ttu-id="2475e-145">Za pomocą programu SQL Server</span><span class="sxs-lookup"><span data-stu-id="2475e-145">Using SQL Server</span></span>

<span data-ttu-id="2475e-146">Umożliwia także Sqoop umożliwia importowanie i eksportowanie danych z programu SQL Server w centrum danych lub na maszynie wirtualnej hostowanej na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="2475e-146">You can also use Sqoop to import and export data from SQL Server, either in your data center or on a Virtual Machine hosted in Azure.</span></span> <span data-ttu-id="2475e-147">Różnice między przy użyciu bazy danych SQL i programu SQL Server są następujące:</span><span class="sxs-lookup"><span data-stu-id="2475e-147">The differences between using SQL Database and SQL Server are:</span></span>

* <span data-ttu-id="2475e-148">Zarówno HDInsight, jak i SQL Server musi być w tej samej sieci wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="2475e-148">Both HDInsight and SQL Server must be on the same Azure Virtual Network.</span></span>

    <span data-ttu-id="2475e-149">Na przykład zobacz [HDInsight połączyć się z siecią lokalną](./connect-on-premises-network.md) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="2475e-149">For an example, see the [Connect HDInsight to your on-premises network](./connect-on-premises-network.md) document.</span></span>

    <span data-ttu-id="2475e-150">Aby uzyskać więcej informacji o korzystaniu z sieci wirtualnej platformy Azure HDInsight, zobacz [rozszerzenie usługi HDInsight za pomocą usługi Azure Virtual Network](hdinsight-extend-hadoop-virtual-network.md) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="2475e-150">For more information on using HDInsight with an Azure Virtual Network, see the [Extend HDInsight with Azure Virtual Network](hdinsight-extend-hadoop-virtual-network.md) document.</span></span> <span data-ttu-id="2475e-151">Aby uzyskać więcej informacji w sieci wirtualnej Azure, zobacz [omówienie sieci wirtualnych](../virtual-network/virtual-networks-overview.md) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="2475e-151">For more information on Azure Virtual Network, see the [Virtual Network Overview](../virtual-network/virtual-networks-overview.md) document.</span></span>

* <span data-ttu-id="2475e-152">Program SQL Server musi być skonfigurowane i umożliwiają uwierzytelnianie SQL.</span><span class="sxs-lookup"><span data-stu-id="2475e-152">SQL Server must be configured to allow SQL authentication.</span></span> <span data-ttu-id="2475e-153">Aby uzyskać więcej informacji, zobacz [wybierz tryb uwierzytelniania](https://msdn.microsoft.com/ms144284.aspx) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="2475e-153">For more information, see the [Choose an Authentication Mode](https://msdn.microsoft.com/ms144284.aspx) document.</span></span>

* <span data-ttu-id="2475e-154">Może być konieczne skonfigurowanie serwera SQL na akceptowanie połączeń zdalnych.</span><span class="sxs-lookup"><span data-stu-id="2475e-154">You may have to configure SQL Server to accept remote connections.</span></span> <span data-ttu-id="2475e-155">Aby uzyskać więcej informacji, zobacz [jak rozwiązywać problemy z nawiązywania połączenia z aparatem bazy danych programu SQL Server](http://social.technet.microsoft.com/wiki/contents/articles/2102.how-to-troubleshoot-connecting-to-the-sql-server-database-engine.aspx) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="2475e-155">For more information, see the [How to troubleshoot connecting to the SQL Server database engine](http://social.technet.microsoft.com/wiki/contents/articles/2102.how-to-troubleshoot-connecting-to-the-sql-server-database-engine.aspx) document.</span></span>

* <span data-ttu-id="2475e-156">Utwórz **sqooptest** bazy danych w programie SQL Server przy użyciu narzędzia, takie jak **programu SQL Server Management Studio** lub **tsql**.</span><span class="sxs-lookup"><span data-stu-id="2475e-156">Create the **sqooptest** database in SQL Server using a utility such as **SQL Server Management Studio** or **tsql**.</span></span> <span data-ttu-id="2475e-157">Kroki do używania interfejsu wiersza polecenia Azure działa tylko w bazie danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="2475e-157">The steps for using the Azure CLI only work for Azure SQL Database.</span></span>

    <span data-ttu-id="2475e-158">Użyj następujących instrukcji języka Transact-SQL, aby utworzyć **mobiledata** tabeli:</span><span class="sxs-lookup"><span data-stu-id="2475e-158">Use the following Transact-SQL statements to create the **mobiledata** table:</span></span>

    ```sql
    CREATE TABLE [dbo].[mobiledata](
    [clientid] [nvarchar](50),
    [querytime] [nvarchar](50),
    [market] [nvarchar](50),
    [deviceplatform] [nvarchar](50),
    [devicemake] [nvarchar](50),
    [devicemodel] [nvarchar](50),
    [state] [nvarchar](50),
    [country] [nvarchar](50),
    [querydwelltime] [float],
    [sessionid] [bigint],
    [sessionpagevieworder] [bigint])
    ```

* <span data-ttu-id="2475e-159">Podczas nawiązywania połączenia z programem SQL Server z usługi HDInsight, należy użyć adresu IP programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="2475e-159">When connecting to the SQL Server from HDInsight, you may have to use the IP address of the SQL Server.</span></span> <span data-ttu-id="2475e-160">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="2475e-160">For example:</span></span>

    ```bash
    sqoop import --connect 'jdbc:sqlserver://10.0.1.1:1433;database=sqooptest' --username <adminLogin> --password <adminPassword> --table 'mobiledata' --target-dir 'wasb:///tutorials/usesqoop/importeddata' --fields-terminated-by '\t' --lines-terminated-by '\n' -m 1
    ```

## <a name="limitations"></a><span data-ttu-id="2475e-161">Ograniczenia</span><span class="sxs-lookup"><span data-stu-id="2475e-161">Limitations</span></span>

* <span data-ttu-id="2475e-162">Zbiorcze export - opartych na systemie Linux z usługi HDInsight, łącznik Sqoop, używany do eksportowania danych do programu Microsoft SQL Server lub bazy danych SQL Azure nie obsługuje obecnie zbiorcze operacje wstawiania.</span><span class="sxs-lookup"><span data-stu-id="2475e-162">Bulk export - With Linux-based HDInsight, the Sqoop connector used to export data to Microsoft SQL Server or Azure SQL Database does not currently support bulk inserts.</span></span>

* <span data-ttu-id="2475e-163">Przetwarzanie wsadowe — z opartą na systemie Linux usługą HDInsight przy użyciu `-batch` przełączyć podczas wykonywania operacji wstawienia, Sqoop sprawia, że wiele operacji wstawienia zamiast przetwarzanie wsadowe operacji insert.</span><span class="sxs-lookup"><span data-stu-id="2475e-163">Batching - With Linux-based HDInsight, When using the `-batch` switch when performing inserts, Sqoop makes multiple inserts instead of batching the insert operations.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2475e-164">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="2475e-164">Next steps</span></span>

<span data-ttu-id="2475e-165">Teraz ma przedstawiono sposób używania Sqoop.</span><span class="sxs-lookup"><span data-stu-id="2475e-165">Now you have learned how to use Sqoop.</span></span> <span data-ttu-id="2475e-166">Aby dowiedzieć się więcej, zobacz:</span><span class="sxs-lookup"><span data-stu-id="2475e-166">To learn more, see:</span></span>

* <span data-ttu-id="2475e-167">[Korzystanie z usługą HDInsight Oozie][hdinsight-use-oozie]: Użyj Sqoop działań w przepływie pracy Oozie.</span><span class="sxs-lookup"><span data-stu-id="2475e-167">[Use Oozie with HDInsight][hdinsight-use-oozie]: Use Sqoop action in an Oozie workflow.</span></span>
* <span data-ttu-id="2475e-168">[Analizowanie danych opóźnienie transmitowane przy użyciu usługi HDInsight][hdinsight-analyze-flight-data]: Użyj gałąź rejestru, aby transmitowane analizować opóźnienie danych, a następnie użyj Sqoop eksportować dane do bazy danych Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="2475e-168">[Analyze flight delay data using HDInsight][hdinsight-analyze-flight-data]: Use Hive to analyze flight delay data, and then use Sqoop to export data to an Azure SQL database.</span></span>
* <span data-ttu-id="2475e-169">[Przekazywanie danych do usługi HDInsight][hdinsight-upload-data]: znajdowanie innych metod do przekazywania danych do magazynu obiektów Blob HDInsight/Azure.</span><span class="sxs-lookup"><span data-stu-id="2475e-169">[Upload data to HDInsight][hdinsight-upload-data]: Find other methods for uploading data to HDInsight/Azure Blob storage.</span></span>

[hdinsight-versions]:  hdinsight-component-versioning.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-storage]: ../hdinsight-hadoop-use-blob-storage.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md

[sqldatabase-get-started]: ../sql-database-get-started.md
[sqldatabase-create-configue]: ../sql-database-create-configure.md

[powershell-start]: http://technet.microsoft.com/library/hh847889.aspx
[powershell-install]: /powershell/azureps-cmdlets-docs
[powershell-script]: http://technet.microsoft.com/library/ee176949.aspx

[sqoop-user-guide-1.4.4]: https://sqoop.apache.org/docs/1.4.4/SqoopUserGuide.html
