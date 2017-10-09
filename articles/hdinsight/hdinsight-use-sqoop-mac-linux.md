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
# <a name="use-apache-sqoop-tooimport-and-export-data-between-hadoop-on-hdinsight-and-sql-database"></a>Użyj narzędzia Apache Sqoop tooimport i wyeksportuj dane między Hadoop w usłudze HDInsight i bazy danych SQL

[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

Dowiedz się, jak klastra tooimport Apache Sqoop toouse i eksportowanie między usługi Hadoop w usłudze Azure HDInsight i bazy danych Azure SQL Database lub programu Microsoft SQL Server. Hello czynnościach w ramach tego dokumentu Użyj hello `sqoop` polecenia bezpośrednio z headnode hello hello klastra usługi Hadoop. Użyj węzła głównego SSH tooconnect toohello i uruchamiania poleceń hello w tym dokumencie.

> [!IMPORTANT]
> Hello kroki opisane w tym dokumencie pracować tylko z klastrami usługi HDInsight, które używają systemu Linux. Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej. Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).

## <a name="install-freetds"></a>Zainstaluj protokół FreeTDS

1. Użyj klastra usługi HDInsight toohello tooconnect SSH. Na przykład hello następujące polecenie łączy toohello headnode podstawowego klastra o nazwie `mycluster`:

    ```bash
    ssh CLUSTERNAME-ssh.azurehdinsight.net
    ```

    Aby uzyskać więcej informacji, zobacz [Używanie protokołu SSH w usłudze HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

2. Użyj następującego polecenia tooinstall protokół FreeTDS hello:

    ```bash
    sudo apt --assume-yes install freetds-dev freetds-bin
    ```

    Protokół FreeTDS jest używany w kilku kroków tooSQL tooconnect bazy danych.

## <a name="create-hello-table-in-sql-database"></a>Utwórz tabelę hello w bazie danych SQL

> [!IMPORTANT]
> Jeśli korzystasz z klastrem usługi HDInsight hello i tworzenie bazy danych SQL w [Tworzenie klastra i bazy danych SQL](hdinsight-use-sqoop.md), pomiń kroki hello w tej sekcji. Witaj bazy danych i tabeli zostały utworzone jako część hello etapami hello [Tworzenie klastra i bazy danych SQL](hdinsight-use-sqoop.md) dokumentu.

1. W sesji SSH hello Użyj hello następujące polecenia tooconnect toohello bazy danych programu SQL server.

        TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P <adminPassword> -p 1433 -D sqooptest

    Pojawi się toohello podobne dane wyjściowe następującego tekstu:

        locale is "en_US.UTF-8"
        locale charset is "UTF-8"
        using default charset "UTF-8"
        Default database being set toosqooptest
        1>

2. Na powitania `1>` monit, wprowadź hello następujące zapytania:

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

    Gdy hello `GO` instrukcja została wprowadzona, poprzednie instrukcje hello są oceniane. Po pierwsze, hello **mobiledata** tabela została utworzona, a następnie indeks klastrowany jest dodawany tooit (wymagane przez usługę SQL Database).

    Utworzono hello Użyj następującego tooverify zapytania, który hello tabeli:

    ```sql
    SELECT * FROM information_schema.tables
    GO
    ```

    Zostaną wyświetlone dane wyjściowe toohello podobne następującego tekstu:

        TABLE_CATALOG   TABLE_SCHEMA    TABLE_NAME      TABLE_TYPE
        sqooptest       dbo     mobiledata      BASE TABLE

3. Wprowadź `exit` na powitania `1>` Monituj tooexit hello tsql narzędzia.

## <a name="sqoop-export"></a>Sqoop eksportu

1. Użyj hello następujące polecenia z hello SSH połączenia toohello klastra tooverify czy Sqoop widzą bazy danych SQL:

    ```bash
    sqoop list-databases --connect jdbc:sqlserver://<serverName>.database.windows.net:1433 --username <adminLogin> -P
    ```
    Po wyświetleniu monitu wprowadź hasło hello hello logowania bazy danych SQL.

    To polecenie zwraca listę baz danych, w tym hello **sqooptest** bazy danych, który został utworzony wcześniej.

2. dane tooexport **hivesampletable** toohello **mobiledata** tabeli, należy użyć następującego polecenia hello:

    ```bash
    sqoop export --connect 'jdbc:sqlserver://<serverName>.database.windows.net:1433;database=sqooptest' --username <adminLogin> -P --table 'mobiledata' --export-dir 'wasb:///hive/warehouse/hivesampletable' --fields-terminated-by '\t' -m 1
    ```

    To polecenie powoduje, że Sqoop tooconnect toohello **sqooptest** bazy danych. Sqoop następnie eksportuje dane z **wasb: / / / gałęzi/magazynu/hivesampletable** toohello **mobiledata** tabeli.

    > [!IMPORTANT]
    > Użyj `wasb:///` Jeśli konta usługi Azure Storage jest hello domyślny magazyn dla klastra. Użyj `adl:///` przypadku usługi Azure Data Lake Store.

3. Po zakończeniu wykonywania polecenia hello, użyj następującego polecenia tooconnect toohello bazy danych przy użyciu języka TSQL hello:

    ```bash
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P -p 1433 -D sqooptest
    ```

    Po nawiązaniu połączenia hello Użyj następującego tooverify instrukcji, która hello danych został wyeksportowany toohello **mobiledata** tabeli:

    ```sql
    SET ROWCOUNT 50;
    SELECT * FROM mobiledata
    GO
    ```

    Powinna zostać wyświetlona lista dane w tabeli hello. Typ `exit` tooexit hello tsql narzędzia.

## <a name="sqoop-import"></a>Importuj Sqoop

1. Użyj hello następujące polecenie tooimport danych z hello **mobiledata** tabeli w bazie danych SQL, toohello **wasb: / / / samouczki/usesqoop/importeddata** katalogu w usłudze HDInsight:

    ```bash
    sqoop import --connect 'jdbc:sqlserver://<serverName>.database.windows.net:1433;database=sqooptest' --username <adminLogin> --password <adminPassword> --table 'mobiledata' --target-dir 'wasb:///tutorials/usesqoop/importeddata' --fields-terminated-by '\t' --lines-terminated-by '\n' -m 1
    ```

    Hello pól danych hello są rozdzielone przez znak tabulacji, a wiersze hello kończą się znakiem nowego wiersza.

2. Po zakończeniu importowania hello Użyj hello następujące polecenia toolist hello dane w hello nowego katalogu:

    ```bash
    hdfs dfs -text /tutorials/usesqoop/importeddata/part-m-00000
    ```

## <a name="using-sql-server"></a>Za pomocą programu SQL Server

Można również użyć Sqoop tooimport i eksportowanie danych z programu SQL Server w centrum danych lub na maszynie wirtualnej hostowanej na platformie Azure. Hello różnice między przy użyciu bazy danych SQL i programu SQL Server są następujące:

* Zarówno HDInsight, jak i SQL Server musi być na hello tej samej sieci wirtualnej platformy Azure.

    Na przykład zobacz hello [sieć lokalną tooyour połączyć HDInsight](./connect-on-premises-network.md) dokumentu.

    Aby uzyskać więcej informacji o korzystaniu z sieci wirtualnej platformy Azure HDInsight, zobacz hello [rozszerzenie usługi HDInsight za pomocą usługi Azure Virtual Network](hdinsight-extend-hadoop-virtual-network.md) dokumentu. Aby uzyskać więcej informacji w sieci wirtualnej Azure, zobacz hello [omówienie sieci wirtualnych](../virtual-network/virtual-networks-overview.md) dokumentu.

* Program SQL Server musi być skonfigurowany tooallow uwierzytelniania SQL. Aby uzyskać więcej informacji, zobacz hello [wybierz tryb uwierzytelniania](https://msdn.microsoft.com/ms144284.aspx) dokumentu.

* Może być tooconfigure połączeń zdalnych tooaccept programu SQL Server. Aby uzyskać więcej informacji, zobacz hello [sposób łączenia toohello tootroubleshoot programu SQL Server bazy danych aparatu](http://social.technet.microsoft.com/wiki/contents/articles/2102.how-to-troubleshoot-connecting-to-the-sql-server-database-engine.aspx) dokumentu.

* Utwórz hello **sqooptest** bazy danych w programie SQL Server przy użyciu narzędzia, takie jak **programu SQL Server Management Studio** lub **tsql**. Hello kroki do używania hello Azure CLI są prawidłowe tylko dla bazy danych SQL Azure.

    Użyj powitania po hello toocreate instrukcji języka Transact-SQL **mobiledata** tabeli:

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

* Podczas łączenia toohello programu SQL Server z usługi HDInsight, może mieć adres IP hello toouse hello programu SQL Server. Na przykład:

    ```bash
    sqoop import --connect 'jdbc:sqlserver://10.0.1.1:1433;database=sqooptest' --username <adminLogin> --password <adminPassword> --table 'mobiledata' --target-dir 'wasb:///tutorials/usesqoop/importeddata' --fields-terminated-by '\t' --lines-terminated-by '\n' -m 1
    ```

## <a name="limitations"></a>Ograniczenia

* Masowo export - HDInsight opartych na systemie Linux z, hello Sqoop łącznik używany tooexport danych tooMicrosoft serwera SQL lub bazy danych SQL Azure nie obsługuje obecnie zbiorcze operacje wstawiania.

* Przetwarzanie wsadowe — z opartą na systemie Linux usługą HDInsight przy użyciu hello `-batch` przełączyć podczas wykonywania operacji wstawienia, Sqoop sprawia, że wiele operacji wstawienia zamiast przetwarzanie wsadowe hello operacje wstawiania.

## <a name="next-steps"></a>Następne kroki

Teraz wiesz już, jak toouse Sqoop. toolearn więcej, zobacz:

* [Korzystanie z usługą HDInsight Oozie][hdinsight-use-oozie]: Użyj Sqoop działań w przepływie pracy Oozie.
* [Analizowanie danych opóźnienie transmitowane przy użyciu usługi HDInsight][hdinsight-analyze-flight-data]: Użyj Hive transmitowane tooanalyze opóźnienie danych, a następnie użyj bazy danych Azure SQL tooan Sqoop tooexport danych.
* [Przekazywanie danych tooHDInsight][hdinsight-upload-data]: znajdowanie innych metod do przekazywania danych tooHDInsight/usługi Azure Blob storage.

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
