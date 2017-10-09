---
title: "aaaApache Sqoop z platformą Hadoop - Azure HDInsight | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse tooimport Apache Sqoop i eksportowanie pomiędzy platformą Hadoop w usłudze HDInsight i bazy danych SQL Azure."
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
ms.openlocfilehash: b256285659bbcf18ff05e220ccdf51c21eb8fbf7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-apache-sqoop-tooimport-and-export-data-between-hadoop-on-hdinsight-and-sql-database"></a><span data-ttu-id="4bcd6-104">Użyj narzędzia Apache Sqoop tooimport i wyeksportuj dane między Hadoop w usłudze HDInsight i bazy danych SQL</span><span class="sxs-lookup"><span data-stu-id="4bcd6-104">Use Apache Sqoop tooimport and export data between Hadoop on HDInsight and SQL Database</span></span>

[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

<span data-ttu-id="4bcd6-105">Dowiedz się, jak klastra tooimport Apache Sqoop toouse i eksportowanie między usługi Hadoop w usłudze Azure HDInsight i bazy danych Azure SQL Database lub programu Microsoft SQL Server.</span><span class="sxs-lookup"><span data-stu-id="4bcd6-105">Learn how toouse Apache Sqoop tooimport and export between a Hadoop cluster in Azure HDInsight and Azure SQL Database or Microsoft SQL Server database.</span></span> <span data-ttu-id="4bcd6-106">Hello czynnościach w ramach tego dokumentu Użyj hello `sqoop` polecenia bezpośrednio z headnode hello hello klastra usługi Hadoop.</span><span class="sxs-lookup"><span data-stu-id="4bcd6-106">hello steps in this document use hello `sqoop` command directly from hello headnode of hello Hadoop cluster.</span></span> <span data-ttu-id="4bcd6-107">Użyj węzła głównego SSH tooconnect toohello i uruchamiania poleceń hello w tym dokumencie.</span><span class="sxs-lookup"><span data-stu-id="4bcd6-107">You use SSH tooconnect toohello head node and run hello commands in this document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4bcd6-108">Hello kroki opisane w tym dokumencie pracować tylko z klastrami usługi HDInsight, które używają systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="4bcd6-108">hello steps in this document only work with HDInsight clusters that use Linux.</span></span> <span data-ttu-id="4bcd6-109">Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="4bcd6-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="4bcd6-110">Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).</span><span class="sxs-lookup"><span data-stu-id="4bcd6-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="install-freetds"></a><span data-ttu-id="4bcd6-111">Zainstaluj protokół FreeTDS</span><span class="sxs-lookup"><span data-stu-id="4bcd6-111">Install FreeTDS</span></span>

1. <span data-ttu-id="4bcd6-112">Użyj klastra usługi HDInsight toohello tooconnect SSH.</span><span class="sxs-lookup"><span data-stu-id="4bcd6-112">Use SSH tooconnect toohello HDInsight cluster.</span></span> <span data-ttu-id="4bcd6-113">Na przykład hello następujące polecenie łączy toohello headnode podstawowego klastra o nazwie `mycluster`:</span><span class="sxs-lookup"><span data-stu-id="4bcd6-113">For example, hello following command connects toohello primary headnode of a cluster named `mycluster`:</span></span>

    ```bash
    ssh CLUSTERNAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="4bcd6-114">Aby uzyskać więcej informacji, zobacz [Używanie protokołu SSH w usłudze HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="4bcd6-114">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="4bcd6-115">Użyj następującego polecenia tooinstall protokół FreeTDS hello:</span><span class="sxs-lookup"><span data-stu-id="4bcd6-115">Use hello following command tooinstall FreeTDS:</span></span>

    ```bash
    sudo apt --assume-yes install freetds-dev freetds-bin
    ```

    <span data-ttu-id="4bcd6-116">Protokół FreeTDS jest używany w kilku kroków tooSQL tooconnect bazy danych.</span><span class="sxs-lookup"><span data-stu-id="4bcd6-116">FreeTDS is used in several steps tooconnect tooSQL Database.</span></span>

## <a name="create-hello-table-in-sql-database"></a><span data-ttu-id="4bcd6-117">Utwórz tabelę hello w bazie danych SQL</span><span class="sxs-lookup"><span data-stu-id="4bcd6-117">Create hello table in SQL Database</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4bcd6-118">Jeśli korzystasz z klastrem usługi HDInsight hello i tworzenie bazy danych SQL w [Tworzenie klastra i bazy danych SQL](hdinsight-use-sqoop.md), pomiń kroki hello w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="4bcd6-118">If you are using hello HDInsight cluster and SQL Database created in [Create cluster and SQL database](hdinsight-use-sqoop.md), skip hello steps in this section.</span></span> <span data-ttu-id="4bcd6-119">Witaj bazy danych i tabeli zostały utworzone jako część hello etapami hello [Tworzenie klastra i bazy danych SQL](hdinsight-use-sqoop.md) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="4bcd6-119">hello database and table were created as part of hello steps in hello [Create cluster and SQL database](hdinsight-use-sqoop.md) document.</span></span>

1. <span data-ttu-id="4bcd6-120">W sesji SSH hello Użyj hello następujące polecenia tooconnect toohello bazy danych programu SQL server.</span><span class="sxs-lookup"><span data-stu-id="4bcd6-120">From hello SSH session, use hello following command tooconnect toohello SQL Database server.</span></span>

        TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P <adminPassword> -p 1433 -D sqooptest

    <span data-ttu-id="4bcd6-121">Pojawi się toohello podobne dane wyjściowe następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="4bcd6-121">You receive output similar toohello following text:</span></span>

        locale is "en_US.UTF-8"
        locale charset is "UTF-8"
        using default charset "UTF-8"
        Default database being set toosqooptest
        1>

2. <span data-ttu-id="4bcd6-122">Na powitania `1>` monit, wprowadź hello następujące zapytania:</span><span class="sxs-lookup"><span data-stu-id="4bcd6-122">At hello `1>` prompt, enter hello following query:</span></span>

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

    <span data-ttu-id="4bcd6-123">Gdy hello `GO` instrukcja została wprowadzona, poprzednie instrukcje hello są oceniane.</span><span class="sxs-lookup"><span data-stu-id="4bcd6-123">When hello `GO` statement is entered, hello previous statements are evaluated.</span></span> <span data-ttu-id="4bcd6-124">Po pierwsze, hello **mobiledata** tabela została utworzona, a następnie indeks klastrowany jest dodawany tooit (wymagane przez usługę SQL Database).</span><span class="sxs-lookup"><span data-stu-id="4bcd6-124">First, hello **mobiledata** table is created, then a clustered index is added tooit (required by SQL Database.)</span></span>

    <span data-ttu-id="4bcd6-125">Utworzono hello Użyj następującego tooverify zapytania, który hello tabeli:</span><span class="sxs-lookup"><span data-stu-id="4bcd6-125">Use hello following query tooverify that hello table has been created:</span></span>

    ```sql
    SELECT * FROM information_schema.tables
    GO
    ```

    <span data-ttu-id="4bcd6-126">Zostaną wyświetlone dane wyjściowe toohello podobne następującego tekstu:</span><span class="sxs-lookup"><span data-stu-id="4bcd6-126">You see output similar toohello following text:</span></span>

        TABLE_CATALOG   TABLE_SCHEMA    TABLE_NAME      TABLE_TYPE
        sqooptest       dbo     mobiledata      BASE TABLE

3. <span data-ttu-id="4bcd6-127">Wprowadź `exit` na powitania `1>` Monituj tooexit hello tsql narzędzia.</span><span class="sxs-lookup"><span data-stu-id="4bcd6-127">Enter `exit` at hello `1>` prompt tooexit hello tsql utility.</span></span>

## <a name="sqoop-export"></a><span data-ttu-id="4bcd6-128">Sqoop eksportu</span><span class="sxs-lookup"><span data-stu-id="4bcd6-128">Sqoop export</span></span>

1. <span data-ttu-id="4bcd6-129">Użyj hello następujące polecenia z hello SSH połączenia toohello klastra tooverify czy Sqoop widzą bazy danych SQL:</span><span class="sxs-lookup"><span data-stu-id="4bcd6-129">From hello SSH connection toohello cluster, use hello following command tooverify that Sqoop can see your SQL Database:</span></span>

    ```bash
    sqoop list-databases --connect jdbc:sqlserver://<serverName>.database.windows.net:1433 --username <adminLogin> -P
    ```
    <span data-ttu-id="4bcd6-130">Po wyświetleniu monitu wprowadź hasło hello hello logowania bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="4bcd6-130">When prompted, enter hello password for hello SQL Database login.</span></span>

    <span data-ttu-id="4bcd6-131">To polecenie zwraca listę baz danych, w tym hello **sqooptest** bazy danych, który został utworzony wcześniej.</span><span class="sxs-lookup"><span data-stu-id="4bcd6-131">This command returns a list of databases, including hello **sqooptest** database that you created earlier.</span></span>

2. <span data-ttu-id="4bcd6-132">dane tooexport **hivesampletable** toohello **mobiledata** tabeli, należy użyć następującego polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="4bcd6-132">tooexport data from **hivesampletable** toohello **mobiledata** table, use hello following command:</span></span>

    ```bash
    sqoop export --connect 'jdbc:sqlserver://<serverName>.database.windows.net:1433;database=sqooptest' --username <adminLogin> -P --table 'mobiledata' --export-dir 'wasb:///hive/warehouse/hivesampletable' --fields-terminated-by '\t' -m 1
    ```

    <span data-ttu-id="4bcd6-133">To polecenie powoduje, że Sqoop tooconnect toohello **sqooptest** bazy danych.</span><span class="sxs-lookup"><span data-stu-id="4bcd6-133">This command instructs Sqoop tooconnect toohello **sqooptest** database.</span></span> <span data-ttu-id="4bcd6-134">Sqoop następnie eksportuje dane z **wasb: / / / gałęzi/magazynu/hivesampletable** toohello **mobiledata** tabeli.</span><span class="sxs-lookup"><span data-stu-id="4bcd6-134">Sqoop then exports data from **wasb:///hive/warehouse/hivesampletable** toohello **mobiledata** table.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="4bcd6-135">Użyj `wasb:///` Jeśli konta usługi Azure Storage jest hello domyślny magazyn dla klastra.</span><span class="sxs-lookup"><span data-stu-id="4bcd6-135">Use `wasb:///` if hello default storage for your cluster is an Azure Storage account.</span></span> <span data-ttu-id="4bcd6-136">Użyj `adl:///` przypadku usługi Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="4bcd6-136">Use `adl:///` if it is an Azure Data Lake Store.</span></span>

3. <span data-ttu-id="4bcd6-137">Po zakończeniu wykonywania polecenia hello, użyj następującego polecenia tooconnect toohello bazy danych przy użyciu języka TSQL hello:</span><span class="sxs-lookup"><span data-stu-id="4bcd6-137">After hello command completes, use hello following command tooconnect toohello database using TSQL:</span></span>

    ```bash
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P -p 1433 -D sqooptest
    ```

    <span data-ttu-id="4bcd6-138">Po nawiązaniu połączenia hello Użyj następującego tooverify instrukcji, która hello danych został wyeksportowany toohello **mobiledata** tabeli:</span><span class="sxs-lookup"><span data-stu-id="4bcd6-138">Once connected, use hello following statements tooverify that hello data was exported toohello **mobiledata** table:</span></span>

    ```sql
    SET ROWCOUNT 50;
    SELECT * FROM mobiledata
    GO
    ```

    <span data-ttu-id="4bcd6-139">Powinna zostać wyświetlona lista dane w tabeli hello.</span><span class="sxs-lookup"><span data-stu-id="4bcd6-139">You should see a listing of data in hello table.</span></span> <span data-ttu-id="4bcd6-140">Typ `exit` tooexit hello tsql narzędzia.</span><span class="sxs-lookup"><span data-stu-id="4bcd6-140">Type `exit` tooexit hello tsql utility.</span></span>

## <a name="sqoop-import"></a><span data-ttu-id="4bcd6-141">Importuj Sqoop</span><span class="sxs-lookup"><span data-stu-id="4bcd6-141">Sqoop import</span></span>

1. <span data-ttu-id="4bcd6-142">Użyj hello następujące polecenie tooimport danych z hello **mobiledata** tabeli w bazie danych SQL, toohello **wasb: / / / samouczki/usesqoop/importeddata** katalogu w usłudze HDInsight:</span><span class="sxs-lookup"><span data-stu-id="4bcd6-142">Use hello following command tooimport data from hello **mobiledata** table in SQL Database, toohello **wasb:///tutorials/usesqoop/importeddata** directory on HDInsight:</span></span>

    ```bash
    sqoop import --connect 'jdbc:sqlserver://<serverName>.database.windows.net:1433;database=sqooptest' --username <adminLogin> --password <adminPassword> --table 'mobiledata' --target-dir 'wasb:///tutorials/usesqoop/importeddata' --fields-terminated-by '\t' --lines-terminated-by '\n' -m 1
    ```

    <span data-ttu-id="4bcd6-143">Hello pól danych hello są rozdzielone przez znak tabulacji, a wiersze hello kończą się znakiem nowego wiersza.</span><span class="sxs-lookup"><span data-stu-id="4bcd6-143">hello fields in hello data are separated by a tab character, and hello lines are terminated by a new-line character.</span></span>

2. <span data-ttu-id="4bcd6-144">Po zakończeniu importowania hello Użyj hello następujące polecenia toolist hello dane w hello nowego katalogu:</span><span class="sxs-lookup"><span data-stu-id="4bcd6-144">Once hello import has completed, use hello following command toolist out hello data in hello new directory:</span></span>

    ```bash
    hdfs dfs -text /tutorials/usesqoop/importeddata/part-m-00000
    ```

## <a name="using-sql-server"></a><span data-ttu-id="4bcd6-145">Za pomocą programu SQL Server</span><span class="sxs-lookup"><span data-stu-id="4bcd6-145">Using SQL Server</span></span>

<span data-ttu-id="4bcd6-146">Można również użyć Sqoop tooimport i eksportowanie danych z programu SQL Server w centrum danych lub na maszynie wirtualnej hostowanej na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="4bcd6-146">You can also use Sqoop tooimport and export data from SQL Server, either in your data center or on a Virtual Machine hosted in Azure.</span></span> <span data-ttu-id="4bcd6-147">Hello różnice między przy użyciu bazy danych SQL i programu SQL Server są następujące:</span><span class="sxs-lookup"><span data-stu-id="4bcd6-147">hello differences between using SQL Database and SQL Server are:</span></span>

* <span data-ttu-id="4bcd6-148">Zarówno HDInsight, jak i SQL Server musi być na hello tej samej sieci wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="4bcd6-148">Both HDInsight and SQL Server must be on hello same Azure Virtual Network.</span></span>

    <span data-ttu-id="4bcd6-149">Na przykład zobacz hello [sieć lokalną tooyour połączyć HDInsight](./connect-on-premises-network.md) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="4bcd6-149">For an example, see hello [Connect HDInsight tooyour on-premises network](./connect-on-premises-network.md) document.</span></span>

    <span data-ttu-id="4bcd6-150">Aby uzyskać więcej informacji o korzystaniu z sieci wirtualnej platformy Azure HDInsight, zobacz hello [rozszerzenie usługi HDInsight za pomocą usługi Azure Virtual Network](hdinsight-extend-hadoop-virtual-network.md) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="4bcd6-150">For more information on using HDInsight with an Azure Virtual Network, see hello [Extend HDInsight with Azure Virtual Network](hdinsight-extend-hadoop-virtual-network.md) document.</span></span> <span data-ttu-id="4bcd6-151">Aby uzyskać więcej informacji w sieci wirtualnej Azure, zobacz hello [omówienie sieci wirtualnych](../virtual-network/virtual-networks-overview.md) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="4bcd6-151">For more information on Azure Virtual Network, see hello [Virtual Network Overview](../virtual-network/virtual-networks-overview.md) document.</span></span>

* <span data-ttu-id="4bcd6-152">Program SQL Server musi być skonfigurowany tooallow uwierzytelniania SQL.</span><span class="sxs-lookup"><span data-stu-id="4bcd6-152">SQL Server must be configured tooallow SQL authentication.</span></span> <span data-ttu-id="4bcd6-153">Aby uzyskać więcej informacji, zobacz hello [wybierz tryb uwierzytelniania](https://msdn.microsoft.com/ms144284.aspx) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="4bcd6-153">For more information, see hello [Choose an Authentication Mode](https://msdn.microsoft.com/ms144284.aspx) document.</span></span>

* <span data-ttu-id="4bcd6-154">Może być tooconfigure połączeń zdalnych tooaccept programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="4bcd6-154">You may have tooconfigure SQL Server tooaccept remote connections.</span></span> <span data-ttu-id="4bcd6-155">Aby uzyskać więcej informacji, zobacz hello [sposób łączenia toohello tootroubleshoot programu SQL Server bazy danych aparatu](http://social.technet.microsoft.com/wiki/contents/articles/2102.how-to-troubleshoot-connecting-to-the-sql-server-database-engine.aspx) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="4bcd6-155">For more information, see hello [How tootroubleshoot connecting toohello SQL Server database engine](http://social.technet.microsoft.com/wiki/contents/articles/2102.how-to-troubleshoot-connecting-to-the-sql-server-database-engine.aspx) document.</span></span>

* <span data-ttu-id="4bcd6-156">Utwórz hello **sqooptest** bazy danych w programie SQL Server przy użyciu narzędzia, takie jak **programu SQL Server Management Studio** lub **tsql**.</span><span class="sxs-lookup"><span data-stu-id="4bcd6-156">Create hello **sqooptest** database in SQL Server using a utility such as **SQL Server Management Studio** or **tsql**.</span></span> <span data-ttu-id="4bcd6-157">Hello kroki do używania hello Azure CLI są prawidłowe tylko dla bazy danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="4bcd6-157">hello steps for using hello Azure CLI only work for Azure SQL Database.</span></span>

    <span data-ttu-id="4bcd6-158">Użyj powitania po hello toocreate instrukcji języka Transact-SQL **mobiledata** tabeli:</span><span class="sxs-lookup"><span data-stu-id="4bcd6-158">Use hello following Transact-SQL statements toocreate hello **mobiledata** table:</span></span>

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

* <span data-ttu-id="4bcd6-159">Podczas łączenia toohello programu SQL Server z usługi HDInsight, może mieć adres IP hello toouse hello programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="4bcd6-159">When connecting toohello SQL Server from HDInsight, you may have toouse hello IP address of hello SQL Server.</span></span> <span data-ttu-id="4bcd6-160">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="4bcd6-160">For example:</span></span>

    ```bash
    sqoop import --connect 'jdbc:sqlserver://10.0.1.1:1433;database=sqooptest' --username <adminLogin> --password <adminPassword> --table 'mobiledata' --target-dir 'wasb:///tutorials/usesqoop/importeddata' --fields-terminated-by '\t' --lines-terminated-by '\n' -m 1
    ```

## <a name="limitations"></a><span data-ttu-id="4bcd6-161">Ograniczenia</span><span class="sxs-lookup"><span data-stu-id="4bcd6-161">Limitations</span></span>

* <span data-ttu-id="4bcd6-162">Masowo export - HDInsight opartych na systemie Linux z, hello Sqoop łącznik używany tooexport danych tooMicrosoft serwera SQL lub bazy danych SQL Azure nie obsługuje obecnie zbiorcze operacje wstawiania.</span><span class="sxs-lookup"><span data-stu-id="4bcd6-162">Bulk export - With Linux-based HDInsight, hello Sqoop connector used tooexport data tooMicrosoft SQL Server or Azure SQL Database does not currently support bulk inserts.</span></span>

* <span data-ttu-id="4bcd6-163">Przetwarzanie wsadowe — z opartą na systemie Linux usługą HDInsight przy użyciu hello `-batch` przełączyć podczas wykonywania operacji wstawienia, Sqoop sprawia, że wiele operacji wstawienia zamiast przetwarzanie wsadowe hello operacje wstawiania.</span><span class="sxs-lookup"><span data-stu-id="4bcd6-163">Batching - With Linux-based HDInsight, When using hello `-batch` switch when performing inserts, Sqoop makes multiple inserts instead of batching hello insert operations.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4bcd6-164">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="4bcd6-164">Next steps</span></span>

<span data-ttu-id="4bcd6-165">Teraz wiesz już, jak toouse Sqoop.</span><span class="sxs-lookup"><span data-stu-id="4bcd6-165">Now you have learned how toouse Sqoop.</span></span> <span data-ttu-id="4bcd6-166">toolearn więcej, zobacz:</span><span class="sxs-lookup"><span data-stu-id="4bcd6-166">toolearn more, see:</span></span>

* <span data-ttu-id="4bcd6-167">[Korzystanie z usługą HDInsight Oozie][hdinsight-use-oozie]: Użyj Sqoop działań w przepływie pracy Oozie.</span><span class="sxs-lookup"><span data-stu-id="4bcd6-167">[Use Oozie with HDInsight][hdinsight-use-oozie]: Use Sqoop action in an Oozie workflow.</span></span>
* <span data-ttu-id="4bcd6-168">[Analizowanie danych opóźnienie transmitowane przy użyciu usługi HDInsight][hdinsight-analyze-flight-data]: Użyj Hive transmitowane tooanalyze opóźnienie danych, a następnie użyj bazy danych Azure SQL tooan Sqoop tooexport danych.</span><span class="sxs-lookup"><span data-stu-id="4bcd6-168">[Analyze flight delay data using HDInsight][hdinsight-analyze-flight-data]: Use Hive tooanalyze flight delay data, and then use Sqoop tooexport data tooan Azure SQL database.</span></span>
* <span data-ttu-id="4bcd6-169">[Przekazywanie danych tooHDInsight][hdinsight-upload-data]: znajdowanie innych metod do przekazywania danych tooHDInsight/usługi Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="4bcd6-169">[Upload data tooHDInsight][hdinsight-upload-data]: Find other methods for uploading data tooHDInsight/Azure Blob storage.</span></span>

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
