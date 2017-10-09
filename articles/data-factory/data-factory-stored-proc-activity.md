---
title: "aaaSQL działania dotyczącego procedury składowanej serwera"
description: "Dowiedz się, jak używasz tooinvoke programu SQL Server działania dotyczącego procedury składowanej hello procedurę przechowywaną w bazie danych SQL Azure lub usługi Azure SQL Data Warehouse z potoku fabryki danych."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 1c46ed69-4049-44ec-9b46-e90e964a4a8e
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: spelluru
ms.openlocfilehash: 9116f80eefc59d95e866b2ba1de2feb1bdc4b1d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="sql-server-stored-procedure-activity"></a><span data-ttu-id="75ff6-103">Działanie procedury przechowywane programu SQL Server</span><span class="sxs-lookup"><span data-stu-id="75ff6-103">SQL Server Stored Procedure Activity</span></span>
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="75ff6-104">Działanie gałęzi</span><span class="sxs-lookup"><span data-stu-id="75ff6-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="75ff6-105">Działanie pig</span><span class="sxs-lookup"><span data-stu-id="75ff6-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="75ff6-106">Działania MapReduce</span><span class="sxs-lookup"><span data-stu-id="75ff6-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="75ff6-107">Działaniu przesyłania strumieniowego usługi Hadoop</span><span class="sxs-lookup"><span data-stu-id="75ff6-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="75ff6-108">Działanie Spark</span><span class="sxs-lookup"><span data-stu-id="75ff6-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="75ff6-109">Działanie wykonywania wsadowego w usłudze Machine Learning</span><span class="sxs-lookup"><span data-stu-id="75ff6-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="75ff6-110">Działania aktualizowania zasobów w usłudze Machine Learning</span><span class="sxs-lookup"><span data-stu-id="75ff6-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="75ff6-111">Działania procedur składowanych</span><span class="sxs-lookup"><span data-stu-id="75ff6-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="75ff6-112">Działania języka U-SQL usługi Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="75ff6-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="75ff6-113">Działania niestandardowe .NET</span><span class="sxs-lookup"><span data-stu-id="75ff6-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

## <a name="overview"></a><span data-ttu-id="75ff6-114">Omówienie</span><span class="sxs-lookup"><span data-stu-id="75ff6-114">Overview</span></span>
<span data-ttu-id="75ff6-115">Użyj działania przekształcania danych w fabryce danych [potoku](data-factory-create-pipelines.md) tootransform i przetwarzanie danych pierwotnych do przewidywania i szczegółowych informacji.</span><span class="sxs-lookup"><span data-stu-id="75ff6-115">You use data transformation activities in a Data Factory [pipeline](data-factory-create-pipelines.md) tootransform and process raw data into predictions and insights.</span></span> <span data-ttu-id="75ff6-116">Witaj działania dotyczącego procedury składowanej jest jednym z hello transformacji działania, które obsługuje fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="75ff6-116">hello Stored Procedure Activity is one of hello transformation activities that Data Factory supports.</span></span> <span data-ttu-id="75ff6-117">W tym artykule opiera się na powitania [działań przekształcania danych](data-factory-data-transformation-activities.md) artykułu, który przedstawia ogólny przegląd transformacji danych i działań przekształcania hello obsługiwany w fabryce danych.</span><span class="sxs-lookup"><span data-stu-id="75ff6-117">This article builds on hello [data transformation activities](data-factory-data-transformation-activities.md) article, which presents a general overview of data transformation and hello supported transformation activities in Data Factory.</span></span>

<span data-ttu-id="75ff6-118">Program hello tooinvoke działania dotyczącego procedury składowanej procedury składowanej w jednym z hello następujące dane są przechowywane w przedsiębiorstwie lub na maszynie wirtualnej platformy Azure (VM):</span><span class="sxs-lookup"><span data-stu-id="75ff6-118">You can use hello Stored Procedure Activity tooinvoke a stored procedure in one of hello following data stores in your enterprise or on an Azure virtual machine (VM):</span></span> 

- <span data-ttu-id="75ff6-119">Usługa Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="75ff6-119">Azure SQL Database</span></span>
- <span data-ttu-id="75ff6-120">Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="75ff6-120">Azure SQL Data Warehouse</span></span>
- <span data-ttu-id="75ff6-121">Baza danych programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="75ff6-121">SQL Server Database.</span></span>  <span data-ttu-id="75ff6-122">Jeśli używasz programu SQL Server, należy zainstalować brama zarządzania danymi na powitania, które same komputera, czy hosty hello bazy danych lub na osobnym komputerze, który ma toohello dostępu do bazy danych.</span><span class="sxs-lookup"><span data-stu-id="75ff6-122">If you are using SQL Server, install Data Management Gateway on hello same machine that hosts hello database or on a separate machine that has access toohello database.</span></span> <span data-ttu-id="75ff6-123">Brama zarządzania danymi jest składnik, który nawiązuje połączenie danych źródeł na lokalnym/na maszynie Wirtualnej platformy Azure z usługami w chmurze w sposób bezpieczny i zarządzanie nimi.</span><span class="sxs-lookup"><span data-stu-id="75ff6-123">Data Management Gateway is a component that connects data sources on-premises/on Azure VM with cloud services in a secure and managed way.</span></span> <span data-ttu-id="75ff6-124">Zobacz [brama zarządzania danymi](data-factory-data-management-gateway.md) artykułu, aby uzyskać szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="75ff6-124">See [Data Management Gateway](data-factory-data-management-gateway.md) article for details.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="75ff6-125">Podczas kopiowania danych do usługi Azure SQL Database lub SQL Server, można skonfigurować hello **SqlSink** w tooinvoke działania kopiowania procedury składowanej przy użyciu hello **sqlWriterStoredProcedureName** właściwości.</span><span class="sxs-lookup"><span data-stu-id="75ff6-125">When copying data into Azure SQL Database or SQL Server, you can configure hello **SqlSink** in copy activity tooinvoke a stored procedure by using hello **sqlWriterStoredProcedureName** property.</span></span> <span data-ttu-id="75ff6-126">Aby uzyskać więcej informacji, zobacz [wywołaj procedurę składowaną z działania kopiowania](data-factory-invoke-stored-procedure-from-copy-activity.md).</span><span class="sxs-lookup"><span data-stu-id="75ff6-126">For more information, see [Invoke stored procedure from copy activity](data-factory-invoke-stored-procedure-from-copy-activity.md).</span></span> <span data-ttu-id="75ff6-127">Aby uzyskać szczegółowe informacje dotyczące właściwości hello, zobacz następujące artykuły łącznika: [bazy danych SQL Azure](data-factory-azure-sql-connector.md#copy-activity-properties), [programu SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="75ff6-127">For details about hello property, see following connector articles: [Azure SQL Database](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties).</span></span> <span data-ttu-id="75ff6-128">Wywoływanie procedury składowanej podczas kopiowania danych do usługi Azure SQL Data Warehouse przy użyciu aktywność kopiowania nie jest obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="75ff6-128">Invoking a stored procedure while copying data into an Azure SQL Data Warehouse by using a copy activity is not supported.</span></span> <span data-ttu-id="75ff6-129">Jednak hello przechowywane procedury działania tooinvoke procedury składowanej można użyć w usłudze SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="75ff6-129">But, you can use hello stored procedure activity tooinvoke a stored procedure in a SQL Data Warehouse.</span></span> 
>  
> <span data-ttu-id="75ff6-130">Podczas kopiowania danych z bazy danych SQL Azure lub programu SQL Server lub magazyn danych SQL Azure, możesz skonfigurować **SqlSource** w tooinvoke działania kopiowania danych tooread procedurę składowaną z hello źródłowej bazy danych przy użyciu hello  **sqlReaderStoredProcedureName** właściwości.</span><span class="sxs-lookup"><span data-stu-id="75ff6-130">When copying data from Azure SQL Database or SQL Server or Azure SQL Data Warehouse, you can configure **SqlSource** in copy activity tooinvoke a stored procedure tooread data from hello source database by using hello **sqlReaderStoredProcedureName** property.</span></span> <span data-ttu-id="75ff6-131">Aby uzyskać więcej informacji, zobacz następujące artykuły łącznika hello: [bazy danych SQL Azure](data-factory-azure-sql-connector.md#copy-activity-properties), [programu SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties), [magazyn danych SQL Azure](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties)</span><span class="sxs-lookup"><span data-stu-id="75ff6-131">For more information, see hello following connector articles: [Azure SQL Database](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties), [Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties)</span></span>          


<span data-ttu-id="75ff6-132">następujące wskazówki używa Hello hello działania dotyczącego procedury składowanej w potoku tooinvoke procedurę przechowywaną w bazie danych Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="75ff6-132">hello following walkthrough uses hello Stored Procedure Activity in a pipeline tooinvoke a stored procedure in an Azure SQL database.</span></span> 

## <a name="walkthrough"></a><span data-ttu-id="75ff6-133">Przewodnik</span><span class="sxs-lookup"><span data-stu-id="75ff6-133">Walkthrough</span></span>
### <a name="sample-table-and-stored-procedure"></a><span data-ttu-id="75ff6-134">Przykładowa tabela i procedury składowanej</span><span class="sxs-lookup"><span data-stu-id="75ff6-134">Sample table and stored procedure</span></span>
1. <span data-ttu-id="75ff6-135">Utwórz następujące hello **tabeli** w bazie danych SQL Azure przy użyciu programu SQL Server Management Studio lub innych narzędzi potrafisz.</span><span class="sxs-lookup"><span data-stu-id="75ff6-135">Create hello following **table** in your Azure SQL Database using SQL Server Management Studio or any other tool you are comfortable with.</span></span> <span data-ttu-id="75ff6-136">Kolumna datetimestamp Hello jest hello Data i godzina, o których wygenerowano hello odpowiedni identyfikator.</span><span class="sxs-lookup"><span data-stu-id="75ff6-136">hello datetimestamp column is hello date and time when hello corresponding ID is generated.</span></span>

    ```SQL
    CREATE TABLE dbo.sampletable
    (
        Id uniqueidentifier,
        datetimestamp nvarchar(127)
    )
    GO

    CREATE CLUSTERED INDEX ClusteredID ON dbo.sampletable(Id);
    GO
    ```
    <span data-ttu-id="75ff6-137">Identyfikator jest unikatowy hello zidentyfikowane i kolumny datetimestamp hello jest hello Data i godzina, o których wygenerowano hello odpowiedni identyfikator.</span><span class="sxs-lookup"><span data-stu-id="75ff6-137">Id is hello unique identified and hello datetimestamp column is hello date and time when hello corresponding ID is generated.</span></span>
    
    ![Dane przykładowe](./media/data-factory-stored-proc-activity/sample-data.png)

    <span data-ttu-id="75ff6-139">W tym przykładzie procedury przechowywane hello jest baza danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="75ff6-139">In this sample, hello stored procedure is in an Azure SQL Database.</span></span> <span data-ttu-id="75ff6-140">Jeśli hello procedury składowanej magazyn danych SQL Azure i bazy danych serwera SQL, podejście hello jest podobne.</span><span class="sxs-lookup"><span data-stu-id="75ff6-140">If hello stored procedure is in an Azure SQL Data Warehouse and SQL Server Database, hello approach is similar.</span></span> <span data-ttu-id="75ff6-141">Dla bazy danych programu SQL Server, należy zainstalować [brama zarządzania danymi](data-factory-data-management-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="75ff6-141">For a SQL Server database, you must install a [Data Management Gateway](data-factory-data-management-gateway.md).</span></span>
2. <span data-ttu-id="75ff6-142">Utwórz następujące hello **procedury składowanej** która wstawia dane do toohello **sampletable**.</span><span class="sxs-lookup"><span data-stu-id="75ff6-142">Create hello following **stored procedure** that inserts data in toohello **sampletable**.</span></span>

    ```SQL
    CREATE PROCEDURE sp_sample @DateTime nvarchar(127)
    AS

    BEGIN
        INSERT INTO [sampletable]
        VALUES (newid(), @DateTime)
    END
    ```

   > [!IMPORTANT]
   > <span data-ttu-id="75ff6-143">**Nazwa** i **wielkości liter** z hello parametr (DateTime w tym przykładzie) musi być zgodna z parametr określony w potoku hello/aktywność JSON.</span><span class="sxs-lookup"><span data-stu-id="75ff6-143">**Name** and **casing** of hello parameter (DateTime in this example) must match that of parameter specified in hello pipeline/activity JSON.</span></span> <span data-ttu-id="75ff6-144">W definicji procedury składowanej hello, upewnij się, że  **@**  służy jako prefiksu dla parametru hello.</span><span class="sxs-lookup"><span data-stu-id="75ff6-144">In hello stored procedure definition, ensure that **@** is used as a prefix for hello parameter.</span></span>

### <a name="create-a-data-factory"></a><span data-ttu-id="75ff6-145">Tworzenie fabryki danych</span><span class="sxs-lookup"><span data-stu-id="75ff6-145">Create a data factory</span></span>
1. <span data-ttu-id="75ff6-146">Zaloguj się za[portalu Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="75ff6-146">Log in too[Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="75ff6-147">Kliknij przycisk **nowy** w menu po lewej stronie powitania kliknij **analizy i analiza**i kliknij przycisk **fabryki danych**.</span><span class="sxs-lookup"><span data-stu-id="75ff6-147">Click **NEW** on hello left menu, click **Intelligence + Analytics**, and click **Data Factory**.</span></span>

    ![Nowa fabryka danych](media/data-factory-stored-proc-activity/new-data-factory.png)    
3. <span data-ttu-id="75ff6-149">W hello **nowa fabryka danych** bloku, wprowadź **SProcDF** dla hello nazwy.</span><span class="sxs-lookup"><span data-stu-id="75ff6-149">In hello **New data factory** blade, enter **SProcDF** for hello Name.</span></span> <span data-ttu-id="75ff6-150">Nazwy fabryki danych Azure są **unikatowych**.</span><span class="sxs-lookup"><span data-stu-id="75ff6-150">Azure Data Factory names are **globally unique**.</span></span> <span data-ttu-id="75ff6-151">Należy tooprefix hello nazwa fabryki danych hello nazwą użytkownika, po pomyślnym utworzeniu hello tooenable hello fabryki.</span><span class="sxs-lookup"><span data-stu-id="75ff6-151">You need tooprefix hello name of hello data factory with your name, tooenable hello successful creation of hello factory.</span></span>

   ![Nowa fabryka danych](media/data-factory-stored-proc-activity/new-data-factory-blade.png)         
4. <span data-ttu-id="75ff6-153">Wybierz użytkownika **subskrypcji platformy Azure**.</span><span class="sxs-lookup"><span data-stu-id="75ff6-153">Select your **Azure subscription**.</span></span>
5. <span data-ttu-id="75ff6-154">Aby uzyskać **grupy zasobów**, wykonaj jedną z hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="75ff6-154">For **Resource Group**, do one of hello following steps:</span></span>
   1. <span data-ttu-id="75ff6-155">Kliknij przycisk **Utwórz nowy** , a następnie wprowadź nazwę grupy zasobów hello.</span><span class="sxs-lookup"><span data-stu-id="75ff6-155">Click **Create new** and enter a name for hello resource group.</span></span>
   2. <span data-ttu-id="75ff6-156">Kliknij przycisk **Użyj istniejącego** i wybierz istniejącą grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="75ff6-156">Click **Use existing** and select an existing resource group.</span></span>  
6. <span data-ttu-id="75ff6-157">Wybierz hello **lokalizacji** hello fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="75ff6-157">Select hello **location** for hello data factory.</span></span>
7. <span data-ttu-id="75ff6-158">Wybierz **toodashboard numeru Pin** dzięki czemu można zobaczyć fabryki danych hello na pulpicie nawigacyjnym hello następnym zalogowaniu.</span><span class="sxs-lookup"><span data-stu-id="75ff6-158">Select **Pin toodashboard** so that you can see hello data factory on hello dashboard next time you log in.</span></span>
8. <span data-ttu-id="75ff6-159">Kliknij przycisk **Utwórz** na powitania **nowa fabryka danych** bloku.</span><span class="sxs-lookup"><span data-stu-id="75ff6-159">Click **Create** on hello **New data factory** blade.</span></span>
9. <span data-ttu-id="75ff6-160">Zobacz hello fabryki danych tworzona w hello **pulpitu nawigacyjnego** z hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="75ff6-160">You see hello data factory being created in hello **dashboard** of hello Azure portal.</span></span> <span data-ttu-id="75ff6-161">Po hello fabryki danych został utworzony pomyślnie, zobacz strony fabryki danych hello, który umożliwia hello zawartość hello fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="75ff6-161">After hello data factory has been created successfully, you see hello data factory page, which shows you hello contents of hello data factory.</span></span>

   ![Strona główna fabryki danych](media/data-factory-stored-proc-activity/data-factory-home-page.png)

### <a name="create-an-azure-sql-linked-service"></a><span data-ttu-id="75ff6-163">Tworzenie usługi SQL Azure połączone</span><span class="sxs-lookup"><span data-stu-id="75ff6-163">Create an Azure SQL linked service</span></span>
<span data-ttu-id="75ff6-164">Po utworzeniu hello fabryki danych, możesz utworzyć Azure połączoną usługą SQL łączącą bazy danych Azure SQL, zawierającą hello sampletable tabeli i sp_sample przechowywane procedury, tooyour fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="75ff6-164">After creating hello data factory, you create an Azure SQL linked service that links your Azure SQL database, which contains hello sampletable table and sp_sample stored procedure, tooyour data factory.</span></span>

1. <span data-ttu-id="75ff6-165">Kliknij przycisk **tworzenie i wdrażanie** na powitania **fabryki danych** bloku **SProcDF** toolaunch hello Edytor fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="75ff6-165">Click **Author and deploy** on hello **Data Factory** blade for **SProcDF** toolaunch hello Data Factory Editor.</span></span>
2. <span data-ttu-id="75ff6-166">Kliknij przycisk **nowy magazyn danych** hello pasek poleceń i wybierz **bazy danych SQL Azure**.</span><span class="sxs-lookup"><span data-stu-id="75ff6-166">Click **New data store** on hello command bar and choose **Azure SQL Database**.</span></span> <span data-ttu-id="75ff6-167">Powinny pojawić się, że hello skryptu JSON do tworzenia usługi Azure SQL połączonej usługi w edytorze hello.</span><span class="sxs-lookup"><span data-stu-id="75ff6-167">You should see hello JSON script for creating an Azure SQL linked service in hello editor.</span></span>

   ![Nowy magazyn danych](media/data-factory-stored-proc-activity/new-data-store.png)
3. <span data-ttu-id="75ff6-169">W hello skryptu JSON wprowadź następujące zmiany hello:</span><span class="sxs-lookup"><span data-stu-id="75ff6-169">In hello JSON script, make hello following changes:</span></span>

   1. <span data-ttu-id="75ff6-170">Zastąp `<servername>` o nazwie powitania serwera bazy danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="75ff6-170">Replace `<servername>` with hello name of your Azure SQL Database server.</span></span>
   2. <span data-ttu-id="75ff6-171">Zastąp `<databasename>` z hello bazy danych, w której utworzono tabelę hello i hello procedury składowanej.</span><span class="sxs-lookup"><span data-stu-id="75ff6-171">Replace `<databasename>` with hello database in which you created hello table and hello stored procedure.</span></span>
   3. <span data-ttu-id="75ff6-172">Zastąp `<username@servername>` z hello konta użytkownika, które ma toohello dostępu do bazy danych.</span><span class="sxs-lookup"><span data-stu-id="75ff6-172">Replace `<username@servername>` with hello user account that has access toohello database.</span></span>
   4. <span data-ttu-id="75ff6-173">Zastąp `<password>` hello hasła dla konta użytkownika hello.</span><span class="sxs-lookup"><span data-stu-id="75ff6-173">Replace `<password>` with hello password for hello user account.</span></span>

      ![Nowy magazyn danych](media/data-factory-stored-proc-activity/azure-sql-linked-service.png)
4. <span data-ttu-id="75ff6-175">toodeploy hello połączonej usługi, kliknij przycisk **Wdróż** na powitania paska poleceń.</span><span class="sxs-lookup"><span data-stu-id="75ff6-175">toodeploy hello linked service, click **Deploy** on hello command bar.</span></span> <span data-ttu-id="75ff6-176">Upewnij się, że widoczne hello AzureSqlLinkedService w drzewie hello wyświetlić powitania po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="75ff6-176">Confirm that you see hello AzureSqlLinkedService in hello tree view on hello left.</span></span>

    ![Widok drzewa połączonej usługi](media/data-factory-stored-proc-activity/tree-view.png)

### <a name="create-an-output-dataset"></a><span data-ttu-id="75ff6-178">Tworzenie wyjściowego zestawu danych</span><span class="sxs-lookup"><span data-stu-id="75ff6-178">Create an output dataset</span></span>
<span data-ttu-id="75ff6-179">Należy określić wyjściowy zestaw danych działania procedura składowana nawet, jeśli procedury składowanej hello nie zwraca żadnych danych.</span><span class="sxs-lookup"><span data-stu-id="75ff6-179">You must specify an output dataset for a stored procedure activity even if hello stored procedure does not produce any data.</span></span> <span data-ttu-id="75ff6-180">Wynika to z jego hello wyjściowy zestaw danych, które dyski hello harmonogram działania hello (częstotliwość hello działanie jest uruchamiane — co godzinę, codziennie, itp.).</span><span class="sxs-lookup"><span data-stu-id="75ff6-180">That's because it's hello output dataset that drives hello schedule of hello activity (how often hello activity is run - hourly, daily, etc.).</span></span> <span data-ttu-id="75ff6-181">Witaj wyjściowego zestawu danych musi używać **połączona usługa** przywołujący tooan bazy danych SQL Azure lub usługi Azure SQL Data Warehouse lub baza danych SQL Server w której ma zostać hello toorun procedury składowanej.</span><span class="sxs-lookup"><span data-stu-id="75ff6-181">hello output dataset must use a **linked service** that refers tooan Azure SQL Database or an Azure SQL Data Warehouse or a SQL Server Database in which you want hello stored procedure toorun.</span></span> <span data-ttu-id="75ff6-182">Witaj wyjściowego zestawu danych może służyć jako wynik hello toopass sposób hello przechowywane procedury dla dalszego przetwarzania przez inne działanie ([łańcucha działania](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) w potoku hello.</span><span class="sxs-lookup"><span data-stu-id="75ff6-182">hello output dataset can serve as a way toopass hello result of hello stored procedure for subsequent processing by another activity ([chaining activities](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) in hello pipeline.</span></span> <span data-ttu-id="75ff6-183">Jednak automatycznie fabryki danych nie zapisuje dane wyjściowe hello toothis procedury przechowywanej zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="75ff6-183">However, Data Factory does not automatically write hello output of a stored procedure toothis dataset.</span></span> <span data-ttu-id="75ff6-184">Jest to hello tej tabeli SQL tooa zapisy hello punktów zestawu danych wyjściowych do procedury składowanej.</span><span class="sxs-lookup"><span data-stu-id="75ff6-184">It is hello stored procedure that writes tooa SQL table that hello output dataset points to.</span></span> <span data-ttu-id="75ff6-185">W niektórych przypadkach może być hello wyjściowy zestaw danych **fikcyjny dataset** (procedury przechowywanej zestawu danych, który wskazuje tooa tabeli, która naprawdę nie przechowuje dane wyjściowe hello).</span><span class="sxs-lookup"><span data-stu-id="75ff6-185">In some cases, hello output dataset can be a **dummy dataset** (a dataset that points tooa table that does not really hold output of hello stored procedure).</span></span> <span data-ttu-id="75ff6-186">Ten fikcyjny zestaw danych jest używany tylko toospecify hello harmonogramu uruchamiania hello przechowywane procedury działania.</span><span class="sxs-lookup"><span data-stu-id="75ff6-186">This dummy dataset is used only toospecify hello schedule for running hello stored procedure activity.</span></span> 

1. <span data-ttu-id="75ff6-187">Kliknij przycisk **... Więcej** na powitania narzędzi, kliknij przycisk **nowy zestaw danych**i kliknij przycisk **Azure SQL**.</span><span class="sxs-lookup"><span data-stu-id="75ff6-187">Click **... More** on hello toolbar, click **New dataset**, and click **Azure SQL**.</span></span> <span data-ttu-id="75ff6-188">**Nowy zestaw danych** w poleceniu hello paska i wybierz pozycję **Azure SQL**.</span><span class="sxs-lookup"><span data-stu-id="75ff6-188">**New dataset** on hello command bar and select **Azure SQL**.</span></span>

    ![Widok drzewa połączonej usługi](media/data-factory-stored-proc-activity/new-dataset.png)
2. <span data-ttu-id="75ff6-190">Skopiuj/Wklej hello następującego skryptu JSON w edytorze JSON toohello.</span><span class="sxs-lookup"><span data-stu-id="75ff6-190">Copy/paste hello following JSON script in toohello JSON editor.</span></span>

    ```JSON
    {                
        "name": "sprocsampleout",
        "properties": {
            "type": "AzureSqlTable",
            "linkedServiceName": "AzureSqlLinkedService",
            "typeProperties": {
                "tableName": "sampletable"
            },
            "availability": {
                "frequency": "Hour",
                "interval": 1
            }
        }
    }
    ```
3. <span data-ttu-id="75ff6-191">toodeploy hello zestawu danych, kliknij przycisk **Wdróż** na powitania paska poleceń.</span><span class="sxs-lookup"><span data-stu-id="75ff6-191">toodeploy hello dataset, click **Deploy** on hello command bar.</span></span> <span data-ttu-id="75ff6-192">Upewnij się, że hello dataset w widoku drzewa hello jest wyświetlany.</span><span class="sxs-lookup"><span data-stu-id="75ff6-192">Confirm that you see hello dataset in hello tree view.</span></span>

    ![Widok drzewa z połączonych usług](media/data-factory-stored-proc-activity/tree-view-2.png)

### <a name="create-a-pipeline-with-sqlserverstoredprocedure-activity"></a><span data-ttu-id="75ff6-194">Utworzyć potok z działaniem SqlServerStoredProcedure</span><span class="sxs-lookup"><span data-stu-id="75ff6-194">Create a pipeline with SqlServerStoredProcedure activity</span></span>
<span data-ttu-id="75ff6-195">Teraz Utwórzmy potoku z działania procedury składowanej.</span><span class="sxs-lookup"><span data-stu-id="75ff6-195">Now, let's create a pipeline with a stored procedure activity.</span></span> 

<span data-ttu-id="75ff6-196">Zwróć uwagę hello następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="75ff6-196">Notice hello following properties:</span></span> 

- <span data-ttu-id="75ff6-197">Witaj **typu** właściwość jest ustawiona zbyt**SqlServerStoredProcedure**.</span><span class="sxs-lookup"><span data-stu-id="75ff6-197">hello **type** property is set too**SqlServerStoredProcedure**.</span></span> 
- <span data-ttu-id="75ff6-198">Witaj **storedProcedureName** w typie właściwości ustawiono zbyt**sp_sample** (procedury składowanej nazwy hello).</span><span class="sxs-lookup"><span data-stu-id="75ff6-198">hello **storedProcedureName** in type properties is set too**sp_sample** (name of hello stored procedure).</span></span>
- <span data-ttu-id="75ff6-199">Witaj **storedProcedureParameters** sekcja zawiera jeden parametr o nazwie **wartości daty i godziny**.</span><span class="sxs-lookup"><span data-stu-id="75ff6-199">hello **storedProcedureParameters** section contains one parameter named **DataTime**.</span></span> <span data-ttu-id="75ff6-200">Nazwa i wielkość liter w wyrazie parametru hello w formacie JSON muszą być zgodne, nazwa hello i wielkość liter w wyrazie hello parametru w definicji procedury hello przechowywane.</span><span class="sxs-lookup"><span data-stu-id="75ff6-200">Name and casing of hello parameter in JSON must match hello name and casing of hello parameter in hello stored procedure definition.</span></span> <span data-ttu-id="75ff6-201">Jeśli należy przekazać wartość null dla parametru, należy użyć składni hello: `"param1": null` (tylko małe litery).</span><span class="sxs-lookup"><span data-stu-id="75ff6-201">If you need pass null for a parameter, use hello syntax: `"param1": null` (all lowercase).</span></span>
 
1. <span data-ttu-id="75ff6-202">Kliknij przycisk **... Więcej** hello pasek poleceń i kliknij przycisk **nowy potok**.</span><span class="sxs-lookup"><span data-stu-id="75ff6-202">Click **... More** on hello command bar and click **New pipeline**.</span></span>
2. <span data-ttu-id="75ff6-203">Skopiuj i Wklej powitania po fragment kodu JSON:</span><span class="sxs-lookup"><span data-stu-id="75ff6-203">Copy/paste hello following JSON snippet:</span></span>   

    ```JSON
    {
        "name": "SprocActivitySamplePipeline",
        "properties": {
            "activities": [
                {
                    "type": "SqlServerStoredProcedure",
                    "typeProperties": {
                        "storedProcedureName": "sp_sample",
                        "storedProcedureParameters": {
                            "DateTime": "$$Text.Format('{0:yyyy-MM-dd HH:mm:ss}', SliceStart)"
                        }
                    },
                    "outputs": [
                        {
                            "name": "sprocsampleout"
                        }
                    ],
                    "scheduler": {
                        "frequency": "Hour",
                        "interval": 1
                    },
                    "name": "SprocActivitySample"
                }
            ],
             "start": "2017-04-02T00:00:00Z",
             "end": "2017-04-02T05:00:00Z",
            "isPaused": false
        }
    }
    ```
3. <span data-ttu-id="75ff6-204">toodeploy hello potoku, kliknij przycisk **Wdróż** na powitania narzędzi.</span><span class="sxs-lookup"><span data-stu-id="75ff6-204">toodeploy hello pipeline, click **Deploy** on hello toolbar.</span></span>  

### <a name="monitor-hello-pipeline"></a><span data-ttu-id="75ff6-205">Monitor hello potoku</span><span class="sxs-lookup"><span data-stu-id="75ff6-205">Monitor hello pipeline</span></span>
1. <span data-ttu-id="75ff6-206">Kliknij przycisk **X** tooclose Edytor fabryki danych bloków toonavigate kopii toohello bloku fabryki danych i kliknij przycisk **Diagram**.</span><span class="sxs-lookup"><span data-stu-id="75ff6-206">Click **X** tooclose Data Factory Editor blades and toonavigate back toohello Data Factory blade, and click **Diagram**.</span></span>

    ![Diagram kafelka](media/data-factory-stored-proc-activity/data-factory-diagram-tile.png)
2. <span data-ttu-id="75ff6-208">W hello **widoku diagramu**, zobacz Omówienie potoki hello i używać zestawów danych w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="75ff6-208">In hello **Diagram View**, you see an overview of hello pipelines, and datasets used in this tutorial.</span></span>

    ![Diagram kafelka](media/data-factory-stored-proc-activity/data-factory-diagram-view.png)
3. <span data-ttu-id="75ff6-210">Hello widoku diagramu, kliknij dwukrotnie hello dataset `sprocsampleout`.</span><span class="sxs-lookup"><span data-stu-id="75ff6-210">In hello Diagram View, double-click hello dataset `sprocsampleout`.</span></span> <span data-ttu-id="75ff6-211">Zostanie wyświetlony wycinków hello w stanie gotowe.</span><span class="sxs-lookup"><span data-stu-id="75ff6-211">You see hello slices in Ready state.</span></span> <span data-ttu-id="75ff6-212">Powinien istnieć pięć wycinków, ponieważ wycinek jest tworzone dla każdej godziny między hello godzinę rozpoczęcia i zakończenia z hello JSON.</span><span class="sxs-lookup"><span data-stu-id="75ff6-212">There should be five slices because a slice is produced for each hour between hello start time and end time from hello JSON.</span></span>

    ![Diagram kafelka](media/data-factory-stored-proc-activity/data-factory-slices.png)
4. <span data-ttu-id="75ff6-214">Gdy wycinek jest **gotowe** stanu, uruchom `select * from sampletable` zapytania dotyczącego hello tooverify bazy danych Azure SQL, która hello danych została umieszczona w tabeli toohello hello przechowywane procedury.</span><span class="sxs-lookup"><span data-stu-id="75ff6-214">When a slice is in **Ready** state, run a `select * from sampletable` query against hello Azure SQL database tooverify that hello data was inserted in toohello table by hello stored procedure.</span></span>

   ![dane wyjściowe](./media/data-factory-stored-proc-activity/output.png)

   <span data-ttu-id="75ff6-216">Zobacz [potoku hello Monitor](data-factory-monitor-manage-pipelines.md) szczegółowe informacje o monitorowaniu potoki fabryki danych Azure.</span><span class="sxs-lookup"><span data-stu-id="75ff6-216">See [Monitor hello pipeline](data-factory-monitor-manage-pipelines.md) for detailed information about monitoring Azure Data Factory pipelines.</span></span>  


## <a name="specify-an-input-dataset"></a><span data-ttu-id="75ff6-217">Określ zestaw danych wejściowych</span><span class="sxs-lookup"><span data-stu-id="75ff6-217">Specify an input dataset</span></span>
<span data-ttu-id="75ff6-218">W przewodniku hello działania procedury składowanej nie ma żadnych wejściowe zestawy danych.</span><span class="sxs-lookup"><span data-stu-id="75ff6-218">In hello walkthrough, stored procedure activity does not have any input datasets.</span></span> <span data-ttu-id="75ff6-219">Jeśli określisz zestaw danych wejściowych, hello działania procedury składowanej nie działa do momentu hello wejściowego zestawu danych jest dostępny (w stanie gotowe).</span><span class="sxs-lookup"><span data-stu-id="75ff6-219">If you specify an input dataset, hello stored procedure activity does not run until hello slice of input dataset is available (in Ready state).</span></span> <span data-ttu-id="75ff6-220">Hello zestawu danych może być zewnętrzny zestaw danych (który nie jest generowany przez innego działania w hello tego samego potoku) lub wewnętrzny zestawu danych, który jest generowany przez działanie w strumieniu przychodzącym (hello działania wykonywane przed tego działania).</span><span class="sxs-lookup"><span data-stu-id="75ff6-220">hello dataset can be an external dataset (that is not produced by another activity in hello same pipeline) or an internal dataset that is produced by an upstream activity (hello activity that runs before this activity).</span></span> <span data-ttu-id="75ff6-221">Można określić wiele zestawów wejściowych danych hello przechowywane procedury działania.</span><span class="sxs-lookup"><span data-stu-id="75ff6-221">You can specify multiple input datasets for hello stored procedure activity.</span></span> <span data-ttu-id="75ff6-222">Jeśli tak zrobisz hello działania procedury składowanej działa tylko wtedy, gdy wszystkie fragmenty wejściowy zestaw danych hello są dostępne (w stanie gotowe).</span><span class="sxs-lookup"><span data-stu-id="75ff6-222">If you do so, hello stored procedure activity runs only when all hello input dataset slices are available (in Ready state).</span></span> <span data-ttu-id="75ff6-223">Witaj wejściowy zestaw danych nie mogą być używane w procedurze hello przechowywane jako parametr.</span><span class="sxs-lookup"><span data-stu-id="75ff6-223">hello input dataset cannot be consumed in hello stored procedure as a parameter.</span></span> <span data-ttu-id="75ff6-224">Jest tylko zależności hello toocheck używane przed początkowy hello przechowywane procedury działania.</span><span class="sxs-lookup"><span data-stu-id="75ff6-224">It is only used toocheck hello dependency before starting hello stored procedure activity.</span></span>

## <a name="chaining-with-other-activities"></a><span data-ttu-id="75ff6-225">Łańcuch serwerów z innymi działaniami</span><span class="sxs-lookup"><span data-stu-id="75ff6-225">Chaining with other activities</span></span>
<span data-ttu-id="75ff6-226">Jeśli toochain działania nadrzędnego tego działania, należy określić hello dane wyjściowe działania nadrzędnego hello jako dane wejściowe tego działania.</span><span class="sxs-lookup"><span data-stu-id="75ff6-226">If you want toochain an upstream activity with this activity, specify hello output of hello upstream activity as an input of this activity.</span></span> <span data-ttu-id="75ff6-227">Po wykonaniu tej hello działania procedury składowanej nie jest możliwe dopiero po zakończeniu działania nadrzędnego hello i hello wyjściowy zestaw danych działania nadrzędnego hello jest dostępna (w stanie gotowe).</span><span class="sxs-lookup"><span data-stu-id="75ff6-227">When you do so, hello stored procedure activity does not run until hello upstream activity completes and hello output dataset of hello upstream activity is available (in Ready status).</span></span> <span data-ttu-id="75ff6-228">Wyjściowe zestawy danych z wielu działań nadrzędnego może służyć jako wejściowe zestawy danych hello przechowywane procedury działania.</span><span class="sxs-lookup"><span data-stu-id="75ff6-228">You can specify output datasets of multiple upstream activities as input datasets of hello stored procedure activity.</span></span> <span data-ttu-id="75ff6-229">Po wykonaniu tej czynności hello przechowywane działania procedura działa tylko wtedy, gdy wszystkie fragmenty wejściowy zestaw danych hello są dostępne.</span><span class="sxs-lookup"><span data-stu-id="75ff6-229">When you do so, hello stored procedure activity runs only when all hello input dataset slices are available.</span></span>  

<span data-ttu-id="75ff6-230">Poniższy przykład hello, hello dane wyjściowe działania kopiowania hello jest: OutputDataset, która jest wartością wejściową hello przechowywane procedury działania.</span><span class="sxs-lookup"><span data-stu-id="75ff6-230">In hello following example, hello output of hello copy activity is: OutputDataset, which is an input of hello stored procedure activity.</span></span> <span data-ttu-id="75ff6-231">W związku z tym hello działania procedury składowanej nie uruchamia dopiero po zakończeniu działania kopiowania hello i hello OutputDataset jest dostępny (w stanie gotowe).</span><span class="sxs-lookup"><span data-stu-id="75ff6-231">Therefore, hello stored procedure activity does not run until hello copy activity completes and hello OutputDataset slice is available (in Ready state).</span></span> <span data-ttu-id="75ff6-232">Jeśli określisz wiele zestawów danych wejściowych hello działania procedury składowanej nie działa, dopóki wszystkie fragmenty wejściowy zestaw danych hello są dostępne (w stanie gotowe).</span><span class="sxs-lookup"><span data-stu-id="75ff6-232">If you specify multiple input datasets, hello stored procedure activity does not run until all hello input dataset slices are available (in Ready state).</span></span> <span data-ttu-id="75ff6-233">Witaj wejściowe zestawy danych nie można użyć bezpośrednio jako parametry toohello przechowywane procedury działania.</span><span class="sxs-lookup"><span data-stu-id="75ff6-233">hello input datasets cannot be used directly as parameters toohello stored procedure activity.</span></span> 

<span data-ttu-id="75ff6-234">Aby uzyskać więcej informacji na tworzenie łańcucha działań, zobacz [wielu działań w potoku](data-factory-create-pipelines.md#multiple-activities-in-a-pipeline)</span><span class="sxs-lookup"><span data-stu-id="75ff6-234">For more information on chaining activities, see [multiple activities in a pipeline](data-factory-create-pipelines.md#multiple-activities-in-a-pipeline)</span></span>

```json
{

    "name": "ADFTutorialPipeline",
    "properties": {
        "description": "Copy data from a blob tooblob",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [ { "name": "InputDataset" } ],
                "outputs": [ { "name": "OutputDataset" } ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst"
                },
                "name": "CopyFromBlobToSQL"
            },
            {
                "type": "SqlServerStoredProcedure",
                "typeProperties": {
                    "storedProcedureName": "SPSproc"
                },
                "inputs": [ { "name": "OutputDataset" } ],
                "outputs": [ { "name": "SQLOutputDataset" } ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "retry": 3
                },
                "name": "RunStoredProcedure"
            }

        ],
        "start": "2017-04-12T00:00:00Z",
        "end": "2017-04-13T00:00:00Z",
        "isPaused": false,
    }
}
```

<span data-ttu-id="75ff6-235">Podobnie, toolink hello magazynu procedury działania o **działania podrzędne** (działania hello, uruchamiane po hello procedury składowanej zakończeniu działania), określ hello wyjściowy zestaw danych działania procedura hello przechowywane jako dane wejściowe działania podrzędne hello w potoku hello.</span><span class="sxs-lookup"><span data-stu-id="75ff6-235">Similarly, toolink hello store procedure activity with **downstream activities** (hello activities that run after hello stored procedure activity completes), specify hello output dataset of hello stored procedure activity as an input of hello downstream activity in hello pipeline.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="75ff6-236">Podczas kopiowania danych do usługi Azure SQL Database lub SQL Server, można skonfigurować hello **SqlSink** w tooinvoke działania kopiowania procedury składowanej przy użyciu hello **sqlWriterStoredProcedureName** właściwości.</span><span class="sxs-lookup"><span data-stu-id="75ff6-236">When copying data into Azure SQL Database or SQL Server, you can configure hello **SqlSink** in copy activity tooinvoke a stored procedure by using hello **sqlWriterStoredProcedureName** property.</span></span> <span data-ttu-id="75ff6-237">Aby uzyskać więcej informacji, zobacz [wywołaj procedurę składowaną z działania kopiowania](data-factory-invoke-stored-procedure-from-copy-activity.md).</span><span class="sxs-lookup"><span data-stu-id="75ff6-237">For more information, see [Invoke stored procedure from copy activity](data-factory-invoke-stored-procedure-from-copy-activity.md).</span></span> <span data-ttu-id="75ff6-238">Szczegółowe informacje o właściwości hello, zobacz następujące artykuły łącznika hello: [bazy danych SQL Azure](data-factory-azure-sql-connector.md#copy-activity-properties), [programu SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="75ff6-238">For details about hello property, see hello following connector articles: [Azure SQL Database](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties).</span></span>
>  
> <span data-ttu-id="75ff6-239">Podczas kopiowania danych z bazy danych SQL Azure lub programu SQL Server lub magazyn danych SQL Azure, możesz skonfigurować **SqlSource** w tooinvoke działania kopiowania danych tooread procedurę składowaną z hello źródłowej bazy danych przy użyciu hello  **sqlReaderStoredProcedureName** właściwości.</span><span class="sxs-lookup"><span data-stu-id="75ff6-239">When copying data from Azure SQL Database or SQL Server or Azure SQL Data Warehouse, you can configure **SqlSource** in copy activity tooinvoke a stored procedure tooread data from hello source database by using hello **sqlReaderStoredProcedureName** property.</span></span> <span data-ttu-id="75ff6-240">Aby uzyskać więcej informacji, zobacz następujące artykuły łącznika hello: [bazy danych SQL Azure](data-factory-azure-sql-connector.md#copy-activity-properties), [programu SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties), [magazyn danych SQL Azure](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties)</span><span class="sxs-lookup"><span data-stu-id="75ff6-240">For more information, see hello following connector articles: [Azure SQL Database](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties), [Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties)</span></span>          

## <a name="json-format"></a><span data-ttu-id="75ff6-241">JSON format</span><span class="sxs-lookup"><span data-stu-id="75ff6-241">JSON format</span></span>
<span data-ttu-id="75ff6-242">Oto formatu JSON hello określających działania dotyczącego procedury składowanej:</span><span class="sxs-lookup"><span data-stu-id="75ff6-242">Here is hello JSON format for defining a Stored Procedure Activity:</span></span>

```JSON
{
    "name": "SQLSPROCActivity",
    "description": "description",
    "type": "SqlServerStoredProcedure",
    "inputs":  [ { "name": "inputtable"  } ],
    "outputs":  [ { "name": "outputtable" } ],
    "typeProperties":
    {
        "storedProcedureName": "<name of hello stored procedure>",
        "storedProcedureParameters":  
        {
            "param1": "param1Value"
            …
        }
    }
}
```

<span data-ttu-id="75ff6-243">Witaj w poniższej tabeli opisano te właściwości JSON:</span><span class="sxs-lookup"><span data-stu-id="75ff6-243">hello following table describes these JSON properties:</span></span>

| <span data-ttu-id="75ff6-244">Właściwość</span><span class="sxs-lookup"><span data-stu-id="75ff6-244">Property</span></span> | <span data-ttu-id="75ff6-245">Opis</span><span class="sxs-lookup"><span data-stu-id="75ff6-245">Description</span></span> | <span data-ttu-id="75ff6-246">Wymagane</span><span class="sxs-lookup"><span data-stu-id="75ff6-246">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="75ff6-247">name</span><span class="sxs-lookup"><span data-stu-id="75ff6-247">name</span></span> | <span data-ttu-id="75ff6-248">Nazwa działania hello</span><span class="sxs-lookup"><span data-stu-id="75ff6-248">Name of hello activity</span></span> |<span data-ttu-id="75ff6-249">Tak</span><span class="sxs-lookup"><span data-stu-id="75ff6-249">Yes</span></span> |
| <span data-ttu-id="75ff6-250">description</span><span class="sxs-lookup"><span data-stu-id="75ff6-250">description</span></span> |<span data-ttu-id="75ff6-251">Tekst opisujący, jakie działanie hello jest używany dla</span><span class="sxs-lookup"><span data-stu-id="75ff6-251">Text describing what hello activity is used for</span></span> |<span data-ttu-id="75ff6-252">Nie</span><span class="sxs-lookup"><span data-stu-id="75ff6-252">No</span></span> |
| <span data-ttu-id="75ff6-253">type</span><span class="sxs-lookup"><span data-stu-id="75ff6-253">type</span></span> | <span data-ttu-id="75ff6-254">Musi mieć wartość: **SqlServerStoredProcedure**</span><span class="sxs-lookup"><span data-stu-id="75ff6-254">Must be set to: **SqlServerStoredProcedure**</span></span> | <span data-ttu-id="75ff6-255">Tak</span><span class="sxs-lookup"><span data-stu-id="75ff6-255">Yes</span></span> |
| <span data-ttu-id="75ff6-256">Dane wejściowe</span><span class="sxs-lookup"><span data-stu-id="75ff6-256">inputs</span></span> | <span data-ttu-id="75ff6-257">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="75ff6-257">Optional.</span></span> <span data-ttu-id="75ff6-258">Jeśli określisz wejściowy zestaw danych, musi być dostępny (w stanie "Gotowe") dla hello przechowywane procedury toorun działania.</span><span class="sxs-lookup"><span data-stu-id="75ff6-258">If you do specify an input dataset, it must be available (in ‘Ready’ status) for hello stored procedure activity toorun.</span></span> <span data-ttu-id="75ff6-259">Witaj wejściowy zestaw danych nie mogą być używane w procedurze hello przechowywane jako parametr.</span><span class="sxs-lookup"><span data-stu-id="75ff6-259">hello input dataset cannot be consumed in hello stored procedure as a parameter.</span></span> <span data-ttu-id="75ff6-260">Jest tylko zależności hello toocheck używane przed początkowy hello przechowywane procedury działania.</span><span class="sxs-lookup"><span data-stu-id="75ff6-260">It is only used toocheck hello dependency before starting hello stored procedure activity.</span></span> |<span data-ttu-id="75ff6-261">Nie</span><span class="sxs-lookup"><span data-stu-id="75ff6-261">No</span></span> |
| <span data-ttu-id="75ff6-262">dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="75ff6-262">outputs</span></span> | <span data-ttu-id="75ff6-263">Należy określić zestaw danych wyjściowych dla działania procedury składowanej.</span><span class="sxs-lookup"><span data-stu-id="75ff6-263">You must specify an output dataset for a stored procedure activity.</span></span> <span data-ttu-id="75ff6-264">Wyjściowy zestaw danych określa hello **harmonogram** hello przechowywane procedury działania (co godzinę, co tydzień, co miesiąc, itp.).</span><span class="sxs-lookup"><span data-stu-id="75ff6-264">Output dataset specifies hello **schedule** for hello stored procedure activity (hourly, weekly, monthly, etc.).</span></span> <br/><br/><span data-ttu-id="75ff6-265">Witaj wyjściowego zestawu danych musi używać **połączona usługa** przywołujący tooan bazy danych SQL Azure lub usługi Azure SQL Data Warehouse lub baza danych SQL Server w której ma zostać hello toorun procedury składowanej.</span><span class="sxs-lookup"><span data-stu-id="75ff6-265">hello output dataset must use a **linked service** that refers tooan Azure SQL Database or an Azure SQL Data Warehouse or a SQL Server Database in which you want hello stored procedure toorun.</span></span> <br/><br/><span data-ttu-id="75ff6-266">Witaj wyjściowego zestawu danych może służyć jako wynik hello toopass sposób hello przechowywane procedury dla dalszego przetwarzania przez inne działanie ([łańcucha działania](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) w potoku hello.</span><span class="sxs-lookup"><span data-stu-id="75ff6-266">hello output dataset can serve as a way toopass hello result of hello stored procedure for subsequent processing by another activity ([chaining activities](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) in hello pipeline.</span></span> <span data-ttu-id="75ff6-267">Jednak automatycznie fabryki danych nie zapisuje dane wyjściowe hello toothis procedury przechowywanej zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="75ff6-267">However, Data Factory does not automatically write hello output of a stored procedure toothis dataset.</span></span> <span data-ttu-id="75ff6-268">Jest to hello tej tabeli SQL tooa zapisy hello punktów zestawu danych wyjściowych do procedury składowanej.</span><span class="sxs-lookup"><span data-stu-id="75ff6-268">It is hello stored procedure that writes tooa SQL table that hello output dataset points to.</span></span> <br/><br/><span data-ttu-id="75ff6-269">W niektórych przypadkach może być hello wyjściowy zestaw danych **fikcyjny dataset**, który jest używany tylko toospecify hello harmonogramu uruchamiania hello przechowywane procedury działania.</span><span class="sxs-lookup"><span data-stu-id="75ff6-269">In some cases, hello output dataset can be a **dummy dataset**, which is used only toospecify hello schedule for running hello stored procedure activity.</span></span> |<span data-ttu-id="75ff6-270">Tak</span><span class="sxs-lookup"><span data-stu-id="75ff6-270">Yes</span></span> |
| <span data-ttu-id="75ff6-271">storedProcedureName</span><span class="sxs-lookup"><span data-stu-id="75ff6-271">storedProcedureName</span></span> |<span data-ttu-id="75ff6-272">Określ nazwę hello hello przechowywane procedury hello bazy danych Azure SQL lub w bazie danych magazynu danych SQL Azure lub programu SQL Server, reprezentowanego przez hello połączone usługi, która hello używa tabeli danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="75ff6-272">Specify hello name of hello stored procedure in hello Azure SQL database or Azure SQL Data Warehouse or SQL Server database that is represented by hello linked service that hello output table uses.</span></span> |<span data-ttu-id="75ff6-273">Tak</span><span class="sxs-lookup"><span data-stu-id="75ff6-273">Yes</span></span> |
| <span data-ttu-id="75ff6-274">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="75ff6-274">storedProcedureParameters</span></span> |<span data-ttu-id="75ff6-275">Określ wartości dla parametrów procedury składowanej.</span><span class="sxs-lookup"><span data-stu-id="75ff6-275">Specify values for stored procedure parameters.</span></span> <span data-ttu-id="75ff6-276">Jeśli potrzebujesz toopass wartości null dla parametru, należy użyć składni hello: "param1": wartość null (małe litery).</span><span class="sxs-lookup"><span data-stu-id="75ff6-276">If you need toopass null for a parameter, use hello syntax: "param1": null (all lower case).</span></span> <span data-ttu-id="75ff6-277">Zobacz powitania po toolearn próbki o korzystaniu z tej właściwości.</span><span class="sxs-lookup"><span data-stu-id="75ff6-277">See hello following sample toolearn about using this property.</span></span> |<span data-ttu-id="75ff6-278">Nie</span><span class="sxs-lookup"><span data-stu-id="75ff6-278">No</span></span> |

## <a name="passing-a-static-value"></a><span data-ttu-id="75ff6-279">Przekazywanie wartości statycznej</span><span class="sxs-lookup"><span data-stu-id="75ff6-279">Passing a static value</span></span>
<span data-ttu-id="75ff6-280">Teraz załóżmy należy rozważyć dodanie inną kolumnę o nazwie "Scenariusza" w tabeli hello zawierające wartości statycznej o nazwie "Próbki dokumentu".</span><span class="sxs-lookup"><span data-stu-id="75ff6-280">Now, let’s consider adding another column named ‘Scenario’ in hello table containing a static value called ‘Document sample’.</span></span>

![Przykładowe dane 2](./media/data-factory-stored-proc-activity/sample-data-2.png)

<span data-ttu-id="75ff6-282">**Tabela:**</span><span class="sxs-lookup"><span data-stu-id="75ff6-282">**Table:**</span></span>

```SQL
CREATE TABLE dbo.sampletable2
(
    Id uniqueidentifier,
    datetimestamp nvarchar(127),
    scenario nvarchar(127)
)
GO

CREATE CLUSTERED INDEX ClusteredID ON dbo.sampletable2(Id);
```

<span data-ttu-id="75ff6-283">**Procedura składowana:**</span><span class="sxs-lookup"><span data-stu-id="75ff6-283">**Stored procedure:**</span></span>

```SQL
CREATE PROCEDURE sp_sample2 @DateTime nvarchar(127) , @Scenario nvarchar(127)

AS

BEGIN
    INSERT INTO [sampletable2]
    VALUES (newid(), @DateTime, @Scenario)
END
```

<span data-ttu-id="75ff6-284">Teraz, Przekaż hello **scenariusza** wartość parametru i hello z hello przechowywane procedury działania.</span><span class="sxs-lookup"><span data-stu-id="75ff6-284">Now, pass hello **Scenario** parameter and hello value from hello stored procedure activity.</span></span> <span data-ttu-id="75ff6-285">Witaj **typeProperties** części hello poprzedzających próbki prawdopodobnie powitania po fragment kodu:</span><span class="sxs-lookup"><span data-stu-id="75ff6-285">hello **typeProperties** section in hello preceding sample looks like hello following snippet:</span></span>

```JSON
"typeProperties":
{
    "storedProcedureName": "sp_sample",
    "storedProcedureParameters":
    {
        "DateTime": "$$Text.Format('{0:yyyy-MM-dd HH:mm:ss}', SliceStart)",
        "Scenario": "Document sample"
    }
}
```

<span data-ttu-id="75ff6-286">**Zestaw danych z fabryki danych:**</span><span class="sxs-lookup"><span data-stu-id="75ff6-286">**Data Factory dataset:**</span></span>

```JSON
{
    "name": "sprocsampleout2",
    "properties": {
        "published": false,
        "type": "AzureSqlTable",
        "linkedServiceName": "AzureSqlLinkedService",
        "typeProperties": {
            "tableName": "sampletable2"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="75ff6-287">**Potok fabryki danych**</span><span class="sxs-lookup"><span data-stu-id="75ff6-287">**Data Factory pipeline**</span></span>

```JSON
{
    "name": "SprocActivitySamplePipeline2",
    "properties": {
        "activities": [
            {
                "type": "SqlServerStoredProcedure",
                "typeProperties": {
                    "storedProcedureName": "sp_sample2",
                    "storedProcedureParameters": {
                        "DateTime": "$$Text.Format('{0:yyyy-MM-dd HH:mm:ss}', SliceStart)",
                        "Scenario": "Document sample"
                    }
                },
                "outputs": [
                    {
                        "name": "sprocsampleout2"
                    }
                ],
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "SprocActivitySample"
            }
        ],
        "start": "2016-10-02T00:00:00Z",
        "end": "2016-10-02T05:00:00Z"
    }
}
```