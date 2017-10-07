---
title: "aaaCopy danych między Data Lake Store i bazy danych Azure SQL przy użyciu Sqoop | Dokumentacja firmy Microsoft"
description: "Użyj Sqoop toocopy danych między bazą danych SQL Azure i usługi Data Lake Store"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 3f914b2a-83cc-4950-b3f7-69c921851683
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: f58483455f0ebe9544673a1d5c5884f2721c800c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-between-data-lake-store-and-azure-sql-database-using-sqoop"></a>Kopiowanie danych między Data Lake Store i za pomocą Sqoop bazy danych Azure SQL
Dowiedz się, jak toouse Apache Sqoop tooimport i eksportowanie danych między bazą danych SQL Azure i usługi Data Lake Store.

## <a name="what-is-sqoop"></a>Co to jest Sqoop?
Aplikacje danych big data nadają się naturalnie do przetwarzania nieustrukturyzowanych i częściowo ustrukturyzowanych danych, takich jak dzienniki i pliki. Jednak mogą również istnieć dane tooprocess strukturę potrzeby, które są przechowywane w relacyjnych baz danych.

[Apache Sqoop](https://sqoop.apache.org/docs/1.4.4/SqoopUserGuide.html) jest tootransfer narzędzie przeznaczone danych między relacyjnych baz danych i repozytorium danych big data, takich jak Data Lake Store. Służy on tooimport danych z systemu zarządzania relacyjnymi bazami danych (RDBMS) takie jak bazy danych SQL Azure do usługi Data Lake Store. Można Przekształć i analizować dane hello przy użyciu danych big data obciążeń i następnie wyeksportować dane hello do RDBMS. W tym samouczku należy użyć jako tooimport relacyjnej bazy danych/eksportu z bazy danych SQL Azure.

## <a name="prerequisites"></a>Wymagania wstępne
Przed rozpoczęciem tego artykułu, musi mieć następujące hello:

* **Subskrypcja platformy Azure**. Zobacz temat [Uzyskiwanie bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Konto usługi Azure Data Lake Store**. Aby uzyskać instrukcje dotyczące jednego, zobacz toocreate [wprowadzenie do usługi Azure Data Lake Store](data-lake-store-get-started-portal.md)
* **Klaster HDInsight Azure** z tooa dostępu do konta usługi Data Lake Store. Zobacz [tworzenia klastra usługi HDInsight z usługą Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md). W tym artykule przyjęto założenie, że masz klaster usługi HDInsight Linux z dostępem do usługi Data Lake Store.
* **Usługa Azure SQL Database**. Aby uzyskać instrukcje dotyczące toocreate jeden, zobacz [tworzenie bazy danych Azure SQL](../sql-database/sql-database-get-started.md)

## <a name="do-you-learn-fast-with-videos"></a>Czy dzięki filmom szybko się uczysz?
[Obejrzyj ten film](https://mix.office.com/watch/1butcdjxmu114) na temat danych toocopy między obiektach blob magazynu Azure i usługi Data Lake Store za pomocą narzędzia DistCp.

## <a name="create-sample-tables-in-hello-azure-sql-database"></a>Tworzenie tabel próbki w hello bazy danych SQL Azure
1. toostart, Utwórz dwie przykładowe tabele w hello bazy danych SQL Azure. Użyj [programu SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md) lub Visual Studio tooconnect toohello bazy danych SQL Azure, a następnie hello wykonywania następującego zapytania.

    **Utwórz Tabela1**

        CREATE TABLE [dbo].[Table1](
        [ID] [int] NOT NULL,
        [FName] [nvarchar](50) NOT NULL,
        [LName] [nvarchar](50) NOT NULL,
         CONSTRAINT [PK_Table_4] PRIMARY KEY CLUSTERED
            (
                   [ID] ASC
            )
        ) ON [PRIMARY]
        GO

    **Utwórz Table2**

        CREATE TABLE [dbo].[Table2](
        [ID] [int] NOT NULL,
        [FName] [nvarchar](50) NOT NULL,
        [LName] [nvarchar](50) NOT NULL,
         CONSTRAINT [PK_Table_4] PRIMARY KEY CLUSTERED
            (
                   [ID] ASC
            )
        ) ON [PRIMARY]
        GO
2. W **Table1**, Dodawanie przykładowych danych. Pozostaw **Table2** puste. Firma Microsoft będzie importowania danych z **Tabela1** do usługi Data Lake Store. Następnie, firma Microsoft będzie eksportować dane z usługi Data Lake Store w **Table2**. Uruchom hello następującego fragmentu.

        INSERT INTO [dbo].[Table1] VALUES (1,'Neal','Kell'), (2,'Lila','Fulton'), (3, 'Erna','Myers'), (4,'Annette','Simpson');


## <a name="use-sqoop-from-an-hdinsight-cluster-with-access-toodata-lake-store"></a>Użyj Sqoop z klastra usługi HDInsight dostępu tooData Lake — Magazyn
Klaster usługi HDInsight jest już dostępne pakiety Sqoop hello. Jeśli skonfigurowano hello HDInsight klastra toouse Data Lake Store jako dodatkowego magazynu, możesz użyć danych tooimport/export Sqoop (bez żadnych zmian konfiguracji) między relacyjnej bazy danych (w tym przykładzie baza danych SQL Azure) i usługi Data Lake Store konto.

1. W tym samouczku przyjęto założenie, że utworzono klaster systemu Linux, należy używać klastra toohello tooconnect SSH. Zobacz [Connect tooa opartych na systemie Linux klaster usługi HDInsight](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).
2. Sprawdź, czy mają dostęp do konta usługi Data Lake Store hello z hello klastra. Uruchom następujące polecenie w wierszu SSH hello hello:

        hdfs dfs -ls adl://<data_lake_store_account>.azuredatalakestore.net/

    To powinien zawierać listę plików/folderów w hello konta usługi Data Lake Store.

### <a name="import-data-from-azure-sql-database-into-data-lake-store"></a>Importowanie danych z bazy danych SQL Azure do usługi Data Lake Store
1. Przejdź toohello katalogu, gdzie Sqoop pakiety są dostępne. Zazwyczaj są to w `/usr/hdp/<version>/sqoop/bin`.
2. Importuj dane hello z **Tabela1** do hello konta usługi Data Lake Store. Witaj użyj następującej składni:

        sqoop-import --connect "jdbc:sqlserver://<sql-database-server-name>.database.windows.net:1433;username=<username>@<sql-database-server-name>;password=<password>;database=<sql-database-name>" --table Table1 --target-dir adl://<data-lake-store-name>.azuredatalakestore.net/Sqoop/SqoopImportTable1

    Należy pamiętać, że **— Nazwa bazy danych sql-server** symbol zastępczy reprezentuje nazwę powitania serwera hello, w którym jest uruchomiona hello bazy danych Azure SQL. **Nazwa bazy danych SQL** symbol zastępczy reprezentuje hello nazwę rzeczywistej bazy danych.

    Na przykład:


        sqoop-import --connect "jdbc:sqlserver://mysqoopserver.database.windows.net:1433;username=nitinme@mysqoopserver;password=<password>;database=mysqoopdatabase" --table Table1 --target-dir adl://myadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1

1. Sprawdź, czy ten powitalne dane zostały przeniesione toohello konta usługi Data Lake Store. Uruchom następujące polecenie hello:

        hdfs dfs -ls adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/

    Witaj następujące dane wyjściowe powinny być widoczne.


        -rwxrwxrwx   0 sshuser hdfs          0 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/_SUCCESS
        -rwxrwxrwx   0 sshuser hdfs         12 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00000
        -rwxrwxrwx   0 sshuser hdfs         14 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00001
        -rwxrwxrwx   0 sshuser hdfs         13 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00002
        -rwxrwxrwx   0 sshuser hdfs         18 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00003

    Każdy **części-m -*** pliku odpowiada tooa wiersza w tabeli źródłowej hello, **Table1**. Można wyświetlić zawartość hello części hello - m-* tooverify pliki.


### <a name="export-data-from-data-lake-store-into-azure-sql-database"></a>Eksportowanie danych z usługi Data Lake Store w bazie danych SQL Azure
1. Eksportowanie danych hello z konta usługi Data Lake Store toohello tabeli pusta, **Table2**, w hello bazy danych SQL Azure. Użyj następującej składni hello.

        sqoop-export --connect "jdbc:sqlserver://<sql-database-server-name>.database.windows.net:1433;username=<username>@<sql-database-server-name>;password=<password>;database=<sql-database-name>" --table Table2 --export-dir adl://<data-lake-store-name>.azuredatalakestore.net/Sqoop/SqoopImportTable1 --input-fields-terminated-by ","

    Na przykład:


        sqoop-export --connect "jdbc:sqlserver://mysqoopserver.database.windows.net:1433;username=nitinme@mysqoopserver;password=<password>;database=mysqoopdatabase" --table Table2 --export-dir adl://myadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1 --input-fields-terminated-by ","

1. Sprawdź, czy tego powitalne dane zostały przekazane toohello tabela bazy danych SQL. Użyj [programu SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md) lub Visual Studio tooconnect toohello bazy danych SQL Azure, a następnie hello uruchom następujące zapytanie.

        SELECT * FROM TABLE2

    Powinno to mieć hello następujące dane wyjściowe.

         ID  FName   LName
        ------------------
        1    Neal    Kell
        2    Lila    Fulton
        3    Erna    Myers
        4    Annette    Simpson

## <a name="performance-considerations-while-using-sqoop"></a>Zagadnienia dotyczące wydajności przy użyciu Sqoop

Dla Twojego Sqoop dostrajania wydajności zadania toocopy danych tooData Lake Store, zobacz [Sqoop wydajności dokumentu](https://blogs.msdn.microsoft.com/bigdatasupport/2015/02/17/sqoop-job-performance-tuning-in-hdinsight-hadoop/).

## <a name="see-also"></a>Zobacz też
* [Kopiowanie danych z usługi Azure magazynu obiektów blob tooData Lake Store](data-lake-store-copy-data-azure-storage-blob.md)
* [Zabezpieczanie danych w usłudze Data Lake Store](data-lake-store-secure-data.md)
* [Korzystanie z usługi Azure Data Lake Analytics z usługą Data Lake Store](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [Korzystanie z usługi Azure HDInsight z usługą Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md)
