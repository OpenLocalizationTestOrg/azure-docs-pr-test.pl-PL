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
# <a name="copy-data-between-data-lake-store-and-azure-sql-database-using-sqoop"></a><span data-ttu-id="84735-103">Kopiowanie danych między Data Lake Store i za pomocą Sqoop bazy danych Azure SQL</span><span class="sxs-lookup"><span data-stu-id="84735-103">Copy data between Data Lake Store and Azure SQL database using Sqoop</span></span>
<span data-ttu-id="84735-104">Dowiedz się, jak toouse Apache Sqoop tooimport i eksportowanie danych między bazą danych SQL Azure i usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="84735-104">Learn how toouse Apache Sqoop tooimport and export data between Azure SQL Database and Data Lake Store.</span></span>

## <a name="what-is-sqoop"></a><span data-ttu-id="84735-105">Co to jest Sqoop?</span><span class="sxs-lookup"><span data-stu-id="84735-105">What is Sqoop?</span></span>
<span data-ttu-id="84735-106">Aplikacje danych big data nadają się naturalnie do przetwarzania nieustrukturyzowanych i częściowo ustrukturyzowanych danych, takich jak dzienniki i pliki.</span><span class="sxs-lookup"><span data-stu-id="84735-106">Big data applications are a natural choice for processing unstructured and semi-structured data, such as logs and files.</span></span> <span data-ttu-id="84735-107">Jednak mogą również istnieć dane tooprocess strukturę potrzeby, które są przechowywane w relacyjnych baz danych.</span><span class="sxs-lookup"><span data-stu-id="84735-107">However, there may also be a need tooprocess structured data that is stored in relational databases.</span></span>

<span data-ttu-id="84735-108">[Apache Sqoop](https://sqoop.apache.org/docs/1.4.4/SqoopUserGuide.html) jest tootransfer narzędzie przeznaczone danych między relacyjnych baz danych i repozytorium danych big data, takich jak Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="84735-108">[Apache Sqoop](https://sqoop.apache.org/docs/1.4.4/SqoopUserGuide.html) is a tool designed tootransfer data between  relational databases and a big data repository, such as Data Lake Store.</span></span> <span data-ttu-id="84735-109">Służy on tooimport danych z systemu zarządzania relacyjnymi bazami danych (RDBMS) takie jak bazy danych SQL Azure do usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="84735-109">You can use it tooimport data from a relational database management system (RDBMS) such as Azure SQL Database into Data Lake Store.</span></span> <span data-ttu-id="84735-110">Można Przekształć i analizować dane hello przy użyciu danych big data obciążeń i następnie wyeksportować dane hello do RDBMS.</span><span class="sxs-lookup"><span data-stu-id="84735-110">You can then transform and analyze hello data using big data workloads and then export hello data back into an RDBMS.</span></span> <span data-ttu-id="84735-111">W tym samouczku należy użyć jako tooimport relacyjnej bazy danych/eksportu z bazy danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="84735-111">In this tutorial, you use an Azure SQL Database as your relational database tooimport/export from.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="84735-112">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="84735-112">Prerequisites</span></span>
<span data-ttu-id="84735-113">Przed rozpoczęciem tego artykułu, musi mieć następujące hello:</span><span class="sxs-lookup"><span data-stu-id="84735-113">Before you begin this article, you must have hello following:</span></span>

* <span data-ttu-id="84735-114">**Subskrypcja platformy Azure**.</span><span class="sxs-lookup"><span data-stu-id="84735-114">**An Azure subscription**.</span></span> <span data-ttu-id="84735-115">Zobacz temat [Uzyskiwanie bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="84735-115">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="84735-116">**Konto usługi Azure Data Lake Store**.</span><span class="sxs-lookup"><span data-stu-id="84735-116">**An Azure Data Lake Store account**.</span></span> <span data-ttu-id="84735-117">Aby uzyskać instrukcje dotyczące jednego, zobacz toocreate [wprowadzenie do usługi Azure Data Lake Store](data-lake-store-get-started-portal.md)</span><span class="sxs-lookup"><span data-stu-id="84735-117">For instructions on how toocreate one, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md)</span></span>
* <span data-ttu-id="84735-118">**Klaster HDInsight Azure** z tooa dostępu do konta usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="84735-118">**Azure HDInsight cluster** with access tooa Data Lake Store account.</span></span> <span data-ttu-id="84735-119">Zobacz [tworzenia klastra usługi HDInsight z usługą Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="84735-119">See [Create an HDInsight cluster with Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md).</span></span> <span data-ttu-id="84735-120">W tym artykule przyjęto założenie, że masz klaster usługi HDInsight Linux z dostępem do usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="84735-120">This article assumes you have an HDInsight Linux cluster with Data Lake Store access.</span></span>
* <span data-ttu-id="84735-121">**Usługa Azure SQL Database**.</span><span class="sxs-lookup"><span data-stu-id="84735-121">**Azure SQL Database**.</span></span> <span data-ttu-id="84735-122">Aby uzyskać instrukcje dotyczące toocreate jeden, zobacz [tworzenie bazy danych Azure SQL](../sql-database/sql-database-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="84735-122">For instructions on how toocreate one, see [Create an Azure SQL database](../sql-database/sql-database-get-started.md)</span></span>

## <a name="do-you-learn-fast-with-videos"></a><span data-ttu-id="84735-123">Czy dzięki filmom szybko się uczysz?</span><span class="sxs-lookup"><span data-stu-id="84735-123">Do you learn fast with videos?</span></span>
<span data-ttu-id="84735-124">[Obejrzyj ten film](https://mix.office.com/watch/1butcdjxmu114) na temat danych toocopy między obiektach blob magazynu Azure i usługi Data Lake Store za pomocą narzędzia DistCp.</span><span class="sxs-lookup"><span data-stu-id="84735-124">[Watch this video](https://mix.office.com/watch/1butcdjxmu114) on how toocopy data between Azure Storage Blobs and Data Lake Store using DistCp.</span></span>

## <a name="create-sample-tables-in-hello-azure-sql-database"></a><span data-ttu-id="84735-125">Tworzenie tabel próbki w hello bazy danych SQL Azure</span><span class="sxs-lookup"><span data-stu-id="84735-125">Create sample tables in hello Azure SQL Database</span></span>
1. <span data-ttu-id="84735-126">toostart, Utwórz dwie przykładowe tabele w hello bazy danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="84735-126">toostart with, create two sample tables in hello Azure SQL Database.</span></span> <span data-ttu-id="84735-127">Użyj [programu SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md) lub Visual Studio tooconnect toohello bazy danych SQL Azure, a następnie hello wykonywania następującego zapytania.</span><span class="sxs-lookup"><span data-stu-id="84735-127">Use [SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md) or Visual Studio tooconnect toohello Azure SQL Database and then run hello following queries.</span></span>

    <span data-ttu-id="84735-128">**Utwórz Tabela1**</span><span class="sxs-lookup"><span data-stu-id="84735-128">**Create Table1**</span></span>

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

    <span data-ttu-id="84735-129">**Utwórz Table2**</span><span class="sxs-lookup"><span data-stu-id="84735-129">**Create Table2**</span></span>

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
2. <span data-ttu-id="84735-130">W **Table1**, Dodawanie przykładowych danych.</span><span class="sxs-lookup"><span data-stu-id="84735-130">In **Table1**, add some sample data.</span></span> <span data-ttu-id="84735-131">Pozostaw **Table2** puste.</span><span class="sxs-lookup"><span data-stu-id="84735-131">Leave **Table2** empty.</span></span> <span data-ttu-id="84735-132">Firma Microsoft będzie importowania danych z **Tabela1** do usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="84735-132">We will import data from **Table1** into Data Lake Store.</span></span> <span data-ttu-id="84735-133">Następnie, firma Microsoft będzie eksportować dane z usługi Data Lake Store w **Table2**.</span><span class="sxs-lookup"><span data-stu-id="84735-133">Then, we will export data from Data Lake Store into **Table2**.</span></span> <span data-ttu-id="84735-134">Uruchom hello następującego fragmentu.</span><span class="sxs-lookup"><span data-stu-id="84735-134">Run hello following snippet.</span></span>

        INSERT INTO [dbo].[Table1] VALUES (1,'Neal','Kell'), (2,'Lila','Fulton'), (3, 'Erna','Myers'), (4,'Annette','Simpson');


## <a name="use-sqoop-from-an-hdinsight-cluster-with-access-toodata-lake-store"></a><span data-ttu-id="84735-135">Użyj Sqoop z klastra usługi HDInsight dostępu tooData Lake — Magazyn</span><span class="sxs-lookup"><span data-stu-id="84735-135">Use Sqoop from an HDInsight cluster with access tooData Lake Store</span></span>
<span data-ttu-id="84735-136">Klaster usługi HDInsight jest już dostępne pakiety Sqoop hello.</span><span class="sxs-lookup"><span data-stu-id="84735-136">An HDInsight cluster already has hello Sqoop packages available.</span></span> <span data-ttu-id="84735-137">Jeśli skonfigurowano hello HDInsight klastra toouse Data Lake Store jako dodatkowego magazynu, możesz użyć danych tooimport/export Sqoop (bez żadnych zmian konfiguracji) między relacyjnej bazy danych (w tym przykładzie baza danych SQL Azure) i usługi Data Lake Store konto.</span><span class="sxs-lookup"><span data-stu-id="84735-137">If you have configured hello HDInsight cluster toouse Data Lake Store as an additional storage, you can use Sqoop (without any configuration changes) tooimport/export data between a relational database (in this example, Azure SQL Database) and a Data Lake Store account.</span></span>

1. <span data-ttu-id="84735-138">W tym samouczku przyjęto założenie, że utworzono klaster systemu Linux, należy używać klastra toohello tooconnect SSH.</span><span class="sxs-lookup"><span data-stu-id="84735-138">For this tutorial, we assume you created a Linux cluster so you should use SSH tooconnect toohello cluster.</span></span> <span data-ttu-id="84735-139">Zobacz [Connect tooa opartych na systemie Linux klaster usługi HDInsight](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="84735-139">See [Connect tooa Linux-based HDInsight cluster](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>
2. <span data-ttu-id="84735-140">Sprawdź, czy mają dostęp do konta usługi Data Lake Store hello z hello klastra.</span><span class="sxs-lookup"><span data-stu-id="84735-140">Verify whether you can access hello Data Lake Store account from hello cluster.</span></span> <span data-ttu-id="84735-141">Uruchom następujące polecenie w wierszu SSH hello hello:</span><span class="sxs-lookup"><span data-stu-id="84735-141">Run hello following command from hello SSH prompt:</span></span>

        hdfs dfs -ls adl://<data_lake_store_account>.azuredatalakestore.net/

    <span data-ttu-id="84735-142">To powinien zawierać listę plików/folderów w hello konta usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="84735-142">This should provide a list of files/folders in hello Data Lake Store account.</span></span>

### <a name="import-data-from-azure-sql-database-into-data-lake-store"></a><span data-ttu-id="84735-143">Importowanie danych z bazy danych SQL Azure do usługi Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="84735-143">Import data from Azure SQL Database into Data Lake Store</span></span>
1. <span data-ttu-id="84735-144">Przejdź toohello katalogu, gdzie Sqoop pakiety są dostępne.</span><span class="sxs-lookup"><span data-stu-id="84735-144">Navigate toohello directory where Sqoop packages are available.</span></span> <span data-ttu-id="84735-145">Zazwyczaj są to w `/usr/hdp/<version>/sqoop/bin`.</span><span class="sxs-lookup"><span data-stu-id="84735-145">Typically, this will be at `/usr/hdp/<version>/sqoop/bin`.</span></span>
2. <span data-ttu-id="84735-146">Importuj dane hello z **Tabela1** do hello konta usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="84735-146">Import hello data from **Table1** into hello Data Lake Store account.</span></span> <span data-ttu-id="84735-147">Witaj użyj następującej składni:</span><span class="sxs-lookup"><span data-stu-id="84735-147">Use hello following syntax:</span></span>

        sqoop-import --connect "jdbc:sqlserver://<sql-database-server-name>.database.windows.net:1433;username=<username>@<sql-database-server-name>;password=<password>;database=<sql-database-name>" --table Table1 --target-dir adl://<data-lake-store-name>.azuredatalakestore.net/Sqoop/SqoopImportTable1

    <span data-ttu-id="84735-148">Należy pamiętać, że **— Nazwa bazy danych sql-server** symbol zastępczy reprezentuje nazwę powitania serwera hello, w którym jest uruchomiona hello bazy danych Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="84735-148">Note that **sql-database-server-name** placeholder represents hello name of hello server where hello Azure SQL database is running.</span></span> <span data-ttu-id="84735-149">**Nazwa bazy danych SQL** symbol zastępczy reprezentuje hello nazwę rzeczywistej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="84735-149">**sql-database-name** placeholder represents hello actual database name.</span></span>

    <span data-ttu-id="84735-150">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="84735-150">For example,</span></span>


        sqoop-import --connect "jdbc:sqlserver://mysqoopserver.database.windows.net:1433;username=nitinme@mysqoopserver;password=<password>;database=mysqoopdatabase" --table Table1 --target-dir adl://myadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1

1. <span data-ttu-id="84735-151">Sprawdź, czy ten powitalne dane zostały przeniesione toohello konta usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="84735-151">Verify that hello data has been transferred toohello Data Lake Store account.</span></span> <span data-ttu-id="84735-152">Uruchom następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="84735-152">Run hello following command:</span></span>

        hdfs dfs -ls adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/

    <span data-ttu-id="84735-153">Witaj następujące dane wyjściowe powinny być widoczne.</span><span class="sxs-lookup"><span data-stu-id="84735-153">You should see hello following output.</span></span>


        -rwxrwxrwx   0 sshuser hdfs          0 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/_SUCCESS
        -rwxrwxrwx   0 sshuser hdfs         12 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00000
        -rwxrwxrwx   0 sshuser hdfs         14 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00001
        -rwxrwxrwx   0 sshuser hdfs         13 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00002
        -rwxrwxrwx   0 sshuser hdfs         18 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00003

    <span data-ttu-id="84735-154">Każdy **części-m -*** pliku odpowiada tooa wiersza w tabeli źródłowej hello, **Table1**.</span><span class="sxs-lookup"><span data-stu-id="84735-154">Each **part-m-*** file corresponds tooa row in hello source table, **Table1**.</span></span> <span data-ttu-id="84735-155">Można wyświetlić zawartość hello części hello - m-* tooverify pliki.</span><span class="sxs-lookup"><span data-stu-id="84735-155">You can view hello contents of hello part-m-* files tooverify.</span></span>


### <a name="export-data-from-data-lake-store-into-azure-sql-database"></a><span data-ttu-id="84735-156">Eksportowanie danych z usługi Data Lake Store w bazie danych SQL Azure</span><span class="sxs-lookup"><span data-stu-id="84735-156">Export data from Data Lake Store into Azure SQL Database</span></span>
1. <span data-ttu-id="84735-157">Eksportowanie danych hello z konta usługi Data Lake Store toohello tabeli pusta, **Table2**, w hello bazy danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="84735-157">Export hello data from Data Lake Store account toohello empty table, **Table2**, in hello Azure SQL Database.</span></span> <span data-ttu-id="84735-158">Użyj następującej składni hello.</span><span class="sxs-lookup"><span data-stu-id="84735-158">Use hello following syntax.</span></span>

        sqoop-export --connect "jdbc:sqlserver://<sql-database-server-name>.database.windows.net:1433;username=<username>@<sql-database-server-name>;password=<password>;database=<sql-database-name>" --table Table2 --export-dir adl://<data-lake-store-name>.azuredatalakestore.net/Sqoop/SqoopImportTable1 --input-fields-terminated-by ","

    <span data-ttu-id="84735-159">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="84735-159">For example,</span></span>


        sqoop-export --connect "jdbc:sqlserver://mysqoopserver.database.windows.net:1433;username=nitinme@mysqoopserver;password=<password>;database=mysqoopdatabase" --table Table2 --export-dir adl://myadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1 --input-fields-terminated-by ","

1. <span data-ttu-id="84735-160">Sprawdź, czy tego powitalne dane zostały przekazane toohello tabela bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="84735-160">Verify that hello data was uploaded toohello SQL Database table.</span></span> <span data-ttu-id="84735-161">Użyj [programu SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md) lub Visual Studio tooconnect toohello bazy danych SQL Azure, a następnie hello uruchom następujące zapytanie.</span><span class="sxs-lookup"><span data-stu-id="84735-161">Use [SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md) or Visual Studio tooconnect toohello Azure SQL Database and then run hello following query.</span></span>

        SELECT * FROM TABLE2

    <span data-ttu-id="84735-162">Powinno to mieć hello następujące dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="84735-162">This should have hello following output.</span></span>

         ID  FName   LName
        ------------------
        1    Neal    Kell
        2    Lila    Fulton
        3    Erna    Myers
        4    Annette    Simpson

## <a name="performance-considerations-while-using-sqoop"></a><span data-ttu-id="84735-163">Zagadnienia dotyczące wydajności przy użyciu Sqoop</span><span class="sxs-lookup"><span data-stu-id="84735-163">Performance considerations while using Sqoop</span></span>

<span data-ttu-id="84735-164">Dla Twojego Sqoop dostrajania wydajności zadania toocopy danych tooData Lake Store, zobacz [Sqoop wydajności dokumentu](https://blogs.msdn.microsoft.com/bigdatasupport/2015/02/17/sqoop-job-performance-tuning-in-hdinsight-hadoop/).</span><span class="sxs-lookup"><span data-stu-id="84735-164">For performance tuning your Sqoop job toocopy data tooData Lake Store, see [Sqoop performance document](https://blogs.msdn.microsoft.com/bigdatasupport/2015/02/17/sqoop-job-performance-tuning-in-hdinsight-hadoop/).</span></span>

## <a name="see-also"></a><span data-ttu-id="84735-165">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="84735-165">See also</span></span>
* [<span data-ttu-id="84735-166">Kopiowanie danych z usługi Azure magazynu obiektów blob tooData Lake Store</span><span class="sxs-lookup"><span data-stu-id="84735-166">Copy data from Azure Storage Blobs tooData Lake Store</span></span>](data-lake-store-copy-data-azure-storage-blob.md)
* [<span data-ttu-id="84735-167">Zabezpieczanie danych w usłudze Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="84735-167">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="84735-168">Korzystanie z usługi Azure Data Lake Analytics z usługą Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="84735-168">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="84735-169">Korzystanie z usługi Azure HDInsight z usługą Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="84735-169">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
