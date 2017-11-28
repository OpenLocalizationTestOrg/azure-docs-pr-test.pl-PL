---
title: "Działanie procedury przechowywane programu SQL Server"
description: "Dowiedz się, jak SQL Server działania dotyczącego procedury składowanej umożliwia wywołanie procedury przechowywanej w bazie danych SQL Azure lub usługi Azure SQL Data Warehouse z potoku fabryki danych."
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
ms.openlocfilehash: 6505d9aa2c7ae003bd928e2fa82cd923a9615394
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="sql-server-stored-procedure-activity"></a><span data-ttu-id="a7b65-103">Działanie procedury przechowywane programu SQL Server</span><span class="sxs-lookup"><span data-stu-id="a7b65-103">SQL Server Stored Procedure Activity</span></span>
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="a7b65-104">Działanie gałęzi</span><span class="sxs-lookup"><span data-stu-id="a7b65-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="a7b65-105">Działanie pig</span><span class="sxs-lookup"><span data-stu-id="a7b65-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="a7b65-106">Działania MapReduce</span><span class="sxs-lookup"><span data-stu-id="a7b65-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="a7b65-107">Działaniu przesyłania strumieniowego usługi Hadoop</span><span class="sxs-lookup"><span data-stu-id="a7b65-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="a7b65-108">Działanie Spark</span><span class="sxs-lookup"><span data-stu-id="a7b65-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="a7b65-109">Działanie wykonywania wsadowego w usłudze Machine Learning</span><span class="sxs-lookup"><span data-stu-id="a7b65-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="a7b65-110">Działania aktualizowania zasobów w usłudze Machine Learning</span><span class="sxs-lookup"><span data-stu-id="a7b65-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="a7b65-111">Działania procedur składowanych</span><span class="sxs-lookup"><span data-stu-id="a7b65-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="a7b65-112">Działania języka U-SQL usługi Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="a7b65-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="a7b65-113">Działania niestandardowe .NET</span><span class="sxs-lookup"><span data-stu-id="a7b65-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

## <a name="overview"></a><span data-ttu-id="a7b65-114">Omówienie</span><span class="sxs-lookup"><span data-stu-id="a7b65-114">Overview</span></span>
<span data-ttu-id="a7b65-115">Użyj działania przekształcania danych w fabryce danych [potoku](data-factory-create-pipelines.md) do transformacji i przetwarzać dane pierwotne służące do przewidywania i szczegółowych informacji.</span><span class="sxs-lookup"><span data-stu-id="a7b65-115">You use data transformation activities in a Data Factory [pipeline](data-factory-create-pipelines.md) to transform and process raw data into predictions and insights.</span></span> <span data-ttu-id="a7b65-116">Działania dotyczącego procedury składowanej jest jednym z działania przekształcania, które obsługuje fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="a7b65-116">The Stored Procedure Activity is one of the transformation activities that Data Factory supports.</span></span> <span data-ttu-id="a7b65-117">W tym artykule opiera się na [działań przekształcania danych](data-factory-data-transformation-activities.md) artykułu, który przedstawia ogólny przegląd transformacji danych i działań przekształcania obsługiwanych w fabryce danych.</span><span class="sxs-lookup"><span data-stu-id="a7b65-117">This article builds on the [data transformation activities](data-factory-data-transformation-activities.md) article, which presents a general overview of data transformation and the supported transformation activities in Data Factory.</span></span>

<span data-ttu-id="a7b65-118">Działania dotyczącego procedury składowanej umożliwia wywołanie procedury składowanej w jednym z następujących magazynów danych w przedsiębiorstwie lub na maszynie wirtualnej platformy Azure (VM):</span><span class="sxs-lookup"><span data-stu-id="a7b65-118">You can use the Stored Procedure Activity to invoke a stored procedure in one of the following data stores in your enterprise or on an Azure virtual machine (VM):</span></span> 

- <span data-ttu-id="a7b65-119">Usługa Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="a7b65-119">Azure SQL Database</span></span>
- <span data-ttu-id="a7b65-120">Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="a7b65-120">Azure SQL Data Warehouse</span></span>
- <span data-ttu-id="a7b65-121">Baza danych programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="a7b65-121">SQL Server Database.</span></span>  <span data-ttu-id="a7b65-122">Jeśli używasz programu SQL Server, należy zainstalować bramę zarządzania danymi na tym samym komputerze, który jest hostem bazy danych lub na osobnym komputerze, który ma dostęp do bazy danych.</span><span class="sxs-lookup"><span data-stu-id="a7b65-122">If you are using SQL Server, install Data Management Gateway on the same machine that hosts the database or on a separate machine that has access to the database.</span></span> <span data-ttu-id="a7b65-123">Brama zarządzania danymi jest składnik, który nawiązuje połączenie danych źródeł na lokalnym/na maszynie Wirtualnej platformy Azure z usługami w chmurze w sposób bezpieczny i zarządzanie nimi.</span><span class="sxs-lookup"><span data-stu-id="a7b65-123">Data Management Gateway is a component that connects data sources on-premises/on Azure VM with cloud services in a secure and managed way.</span></span> <span data-ttu-id="a7b65-124">Zobacz [brama zarządzania danymi](data-factory-data-management-gateway.md) artykułu, aby uzyskać szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="a7b65-124">See [Data Management Gateway](data-factory-data-management-gateway.md) article for details.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a7b65-125">Podczas kopiowania danych do usługi Azure SQL Database lub SQL Server, można skonfigurować **SqlSink** w przypadku działania kopiowania, aby wywołać procedurę składowaną przy użyciu **sqlWriterStoredProcedureName** właściwości.</span><span class="sxs-lookup"><span data-stu-id="a7b65-125">When copying data into Azure SQL Database or SQL Server, you can configure the **SqlSink** in copy activity to invoke a stored procedure by using the **sqlWriterStoredProcedureName** property.</span></span> <span data-ttu-id="a7b65-126">Aby uzyskać więcej informacji, zobacz [wywołaj procedurę składowaną z działania kopiowania](data-factory-invoke-stored-procedure-from-copy-activity.md).</span><span class="sxs-lookup"><span data-stu-id="a7b65-126">For more information, see [Invoke stored procedure from copy activity](data-factory-invoke-stored-procedure-from-copy-activity.md).</span></span> <span data-ttu-id="a7b65-127">Aby uzyskać więcej informacji dotyczących właściwości, zobacz następujące artykuły łącznika: [bazy danych SQL Azure](data-factory-azure-sql-connector.md#copy-activity-properties), [programu SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="a7b65-127">For details about the property, see following connector articles: [Azure SQL Database](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties).</span></span> <span data-ttu-id="a7b65-128">Wywoływanie procedury składowanej podczas kopiowania danych do usługi Azure SQL Data Warehouse przy użyciu aktywność kopiowania nie jest obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="a7b65-128">Invoking a stored procedure while copying data into an Azure SQL Data Warehouse by using a copy activity is not supported.</span></span> <span data-ttu-id="a7b65-129">Jednak działania procedury składowanej służy do wywołania procedury przechowywanej w usłudze SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="a7b65-129">But, you can use the stored procedure activity to invoke a stored procedure in a SQL Data Warehouse.</span></span> 
>  
> <span data-ttu-id="a7b65-130">Podczas kopiowania danych z bazy danych SQL Azure lub programu SQL Server lub magazyn danych SQL Azure, możesz skonfigurować **SqlSource** w przypadku działania kopiowania, aby wywołać procedurę składowaną można odczytać danych ze źródłowej bazy danych przy użyciu  **sqlReaderStoredProcedureName** właściwości.</span><span class="sxs-lookup"><span data-stu-id="a7b65-130">When copying data from Azure SQL Database or SQL Server or Azure SQL Data Warehouse, you can configure **SqlSource** in copy activity to invoke a stored procedure to read data from the source database by using the **sqlReaderStoredProcedureName** property.</span></span> <span data-ttu-id="a7b65-131">Aby uzyskać więcej informacji, zobacz następujące artykuły łącznika: [bazy danych SQL Azure](data-factory-azure-sql-connector.md#copy-activity-properties), [programu SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties), [magazyn danych SQL Azure](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties)</span><span class="sxs-lookup"><span data-stu-id="a7b65-131">For more information, see the following connector articles: [Azure SQL Database](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties), [Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties)</span></span>          


<span data-ttu-id="a7b65-132">Poniższe wskazówki używa działania dotyczącego procedury składowanej w potoku do wywołania procedury przechowywanej w bazie danych Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="a7b65-132">The following walkthrough uses the Stored Procedure Activity in a pipeline to invoke a stored procedure in an Azure SQL database.</span></span> 

## <a name="walkthrough"></a><span data-ttu-id="a7b65-133">Przewodnik</span><span class="sxs-lookup"><span data-stu-id="a7b65-133">Walkthrough</span></span>
### <a name="sample-table-and-stored-procedure"></a><span data-ttu-id="a7b65-134">Przykładowa tabela i procedury składowanej</span><span class="sxs-lookup"><span data-stu-id="a7b65-134">Sample table and stored procedure</span></span>
1. <span data-ttu-id="a7b65-135">Utwórz następującą **tabeli** w bazie danych SQL Azure przy użyciu programu SQL Server Management Studio lub innych narzędzi potrafisz.</span><span class="sxs-lookup"><span data-stu-id="a7b65-135">Create the following **table** in your Azure SQL Database using SQL Server Management Studio or any other tool you are comfortable with.</span></span> <span data-ttu-id="a7b65-136">Kolumna datetimestamp jest data i godzina wygenerowania odpowiedni identyfikator.</span><span class="sxs-lookup"><span data-stu-id="a7b65-136">The datetimestamp column is the date and time when the corresponding ID is generated.</span></span>

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
    <span data-ttu-id="a7b65-137">Identyfikator jest unikatowy zidentyfikować i kolumna datetimestamp jest data i godzina wygenerowania odpowiedni identyfikator.</span><span class="sxs-lookup"><span data-stu-id="a7b65-137">Id is the unique identified and the datetimestamp column is the date and time when the corresponding ID is generated.</span></span>
    
    ![Dane przykładowe](./media/data-factory-stored-proc-activity/sample-data.png)

    <span data-ttu-id="a7b65-139">W tym przykładzie procedura składowana jest w bazie danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="a7b65-139">In this sample, the stored procedure is in an Azure SQL Database.</span></span> <span data-ttu-id="a7b65-140">Jeśli procedura składowana jest magazyn danych SQL Azure i bazy danych programu SQL Server, to rozwiązanie jest podobne.</span><span class="sxs-lookup"><span data-stu-id="a7b65-140">If the stored procedure is in an Azure SQL Data Warehouse and SQL Server Database, the approach is similar.</span></span> <span data-ttu-id="a7b65-141">Dla bazy danych programu SQL Server, należy zainstalować [brama zarządzania danymi](data-factory-data-management-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="a7b65-141">For a SQL Server database, you must install a [Data Management Gateway](data-factory-data-management-gateway.md).</span></span>
2. <span data-ttu-id="a7b65-142">Utwórz następującą **procedury składowanej** która wstawia dane w celu **sampletable**.</span><span class="sxs-lookup"><span data-stu-id="a7b65-142">Create the following **stored procedure** that inserts data in to the **sampletable**.</span></span>

    ```SQL
    CREATE PROCEDURE sp_sample @DateTime nvarchar(127)
    AS

    BEGIN
        INSERT INTO [sampletable]
        VALUES (newid(), @DateTime)
    END
    ```

   > [!IMPORTANT]
   > <span data-ttu-id="a7b65-143">**Nazwa** i **wielkości liter** parametru (DateTime w tym przykładzie) musi być zgodna z parametr określony w potoku/aktywność JSON.</span><span class="sxs-lookup"><span data-stu-id="a7b65-143">**Name** and **casing** of the parameter (DateTime in this example) must match that of parameter specified in the pipeline/activity JSON.</span></span> <span data-ttu-id="a7b65-144">W definicji procedury składowanej, upewnij się, że  **@**  służy jako prefiksu w parametrze.</span><span class="sxs-lookup"><span data-stu-id="a7b65-144">In the stored procedure definition, ensure that **@** is used as a prefix for the parameter.</span></span>

### <a name="create-a-data-factory"></a><span data-ttu-id="a7b65-145">Tworzenie fabryki danych</span><span class="sxs-lookup"><span data-stu-id="a7b65-145">Create a data factory</span></span>
1. <span data-ttu-id="a7b65-146">Zaloguj się do witryny [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="a7b65-146">Log in to [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="a7b65-147">Kliknij przycisk **nowy** w menu po lewej stronie kliknij **analizy i analiza**i kliknij przycisk **fabryki danych**.</span><span class="sxs-lookup"><span data-stu-id="a7b65-147">Click **NEW** on the left menu, click **Intelligence + Analytics**, and click **Data Factory**.</span></span>

    ![Nowa fabryka danych](media/data-factory-stored-proc-activity/new-data-factory.png)    
3. <span data-ttu-id="a7b65-149">W **nowa fabryka danych** bloku, wprowadź **SProcDF** dla nazwy.</span><span class="sxs-lookup"><span data-stu-id="a7b65-149">In the **New data factory** blade, enter **SProcDF** for the Name.</span></span> <span data-ttu-id="a7b65-150">Nazwy fabryki danych Azure są **unikatowych**.</span><span class="sxs-lookup"><span data-stu-id="a7b65-150">Azure Data Factory names are **globally unique**.</span></span> <span data-ttu-id="a7b65-151">Musisz prefiksu nazwy fabryki danych z nazwą, aby umożliwić pomyślne utworzenie fabryki.</span><span class="sxs-lookup"><span data-stu-id="a7b65-151">You need to prefix the name of the data factory with your name, to enable the successful creation of the factory.</span></span>

   ![Nowa fabryka danych](media/data-factory-stored-proc-activity/new-data-factory-blade.png)         
4. <span data-ttu-id="a7b65-153">Wybierz użytkownika **subskrypcji platformy Azure**.</span><span class="sxs-lookup"><span data-stu-id="a7b65-153">Select your **Azure subscription**.</span></span>
5. <span data-ttu-id="a7b65-154">Aby uzyskać **grupy zasobów**, wykonaj jedną z następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="a7b65-154">For **Resource Group**, do one of the following steps:</span></span>
   1. <span data-ttu-id="a7b65-155">Kliknij przycisk **Utwórz nowy** , a następnie wprowadź nazwę grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="a7b65-155">Click **Create new** and enter a name for the resource group.</span></span>
   2. <span data-ttu-id="a7b65-156">Kliknij przycisk **Użyj istniejącego** i wybierz istniejącą grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="a7b65-156">Click **Use existing** and select an existing resource group.</span></span>  
6. <span data-ttu-id="a7b65-157">Na liście **lokalizacja** wybierz lokalizację fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="a7b65-157">Select the **location** for the data factory.</span></span>
7. <span data-ttu-id="a7b65-158">Wybierz **Przypnij do pulpitu nawigacyjnego** , dzięki czemu można wyświetlić fabryki danych na pulpicie nawigacyjnym następnym zalogowaniu.</span><span class="sxs-lookup"><span data-stu-id="a7b65-158">Select **Pin to dashboard** so that you can see the data factory on the dashboard next time you log in.</span></span>
8. <span data-ttu-id="a7b65-159">Kliknij przycisk **Utwórz** w bloku **Nowa fabryka danych**.</span><span class="sxs-lookup"><span data-stu-id="a7b65-159">Click **Create** on the **New data factory** blade.</span></span>
9. <span data-ttu-id="a7b65-160">Zobacz tworzony w fabryce danych **pulpitu nawigacyjnego** portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="a7b65-160">You see the data factory being created in the **dashboard** of the Azure portal.</span></span> <span data-ttu-id="a7b65-161">Po pomyślnym utworzeniu fabryki danych zostanie wyświetlona strona fabryki danych z zawartością fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="a7b65-161">After the data factory has been created successfully, you see the data factory page, which shows you the contents of the data factory.</span></span>

   ![Strona główna fabryki danych](media/data-factory-stored-proc-activity/data-factory-home-page.png)

### <a name="create-an-azure-sql-linked-service"></a><span data-ttu-id="a7b65-163">Tworzenie usługi SQL Azure połączone</span><span class="sxs-lookup"><span data-stu-id="a7b65-163">Create an Azure SQL linked service</span></span>
<span data-ttu-id="a7b65-164">Po utworzeniu fabryki danych, możesz utworzyć Azure SQL połączonej usługi, która łączy bazy danych Azure SQL, który zawiera tabelę sampletable i sp_sample przechowywane procedury z fabryką danych.</span><span class="sxs-lookup"><span data-stu-id="a7b65-164">After creating the data factory, you create an Azure SQL linked service that links your Azure SQL database, which contains the sampletable table and sp_sample stored procedure, to your data factory.</span></span>

1. <span data-ttu-id="a7b65-165">Kliknij przycisk **tworzenie i wdrażanie** na **fabryki danych** bloku **SProcDF** można uruchomić Edytor fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="a7b65-165">Click **Author and deploy** on the **Data Factory** blade for **SProcDF** to launch the Data Factory Editor.</span></span>
2. <span data-ttu-id="a7b65-166">Kliknij przycisk **nowy magazyn danych** polecenie Pasek i wybierz polecenie **bazy danych SQL Azure**.</span><span class="sxs-lookup"><span data-stu-id="a7b65-166">Click **New data store** on the command bar and choose **Azure SQL Database**.</span></span> <span data-ttu-id="a7b65-167">Powinna zostać wyświetlona skryptu JSON do tworzenia usług SQL Azure połączone w edytorze.</span><span class="sxs-lookup"><span data-stu-id="a7b65-167">You should see the JSON script for creating an Azure SQL linked service in the editor.</span></span>

   ![Nowy magazyn danych](media/data-factory-stored-proc-activity/new-data-store.png)
3. <span data-ttu-id="a7b65-169">W skrypcie JSON wprowadź następujące zmiany:</span><span class="sxs-lookup"><span data-stu-id="a7b65-169">In the JSON script, make the following changes:</span></span>

   1. <span data-ttu-id="a7b65-170">Zastąp `<servername>` z nazwy serwera bazy danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="a7b65-170">Replace `<servername>` with the name of your Azure SQL Database server.</span></span>
   2. <span data-ttu-id="a7b65-171">Zastąp `<databasename>` z bazą danych, w którym został utworzony w tabeli i procedury składowanej.</span><span class="sxs-lookup"><span data-stu-id="a7b65-171">Replace `<databasename>` with the database in which you created the table and the stored procedure.</span></span>
   3. <span data-ttu-id="a7b65-172">Zastąp `<username@servername>` przy użyciu konta użytkownika, który ma dostęp do bazy danych.</span><span class="sxs-lookup"><span data-stu-id="a7b65-172">Replace `<username@servername>` with the user account that has access to the database.</span></span>
   4. <span data-ttu-id="a7b65-173">Zastąp `<password>` hasłem do konta użytkownika.</span><span class="sxs-lookup"><span data-stu-id="a7b65-173">Replace `<password>` with the password for the user account.</span></span>

      ![Nowy magazyn danych](media/data-factory-stored-proc-activity/azure-sql-linked-service.png)
4. <span data-ttu-id="a7b65-175">Aby wdrożyć połączonej usługi, kliknij przycisk **Wdróż** na pasku poleceń.</span><span class="sxs-lookup"><span data-stu-id="a7b65-175">To deploy the linked service, click **Deploy** on the command bar.</span></span> <span data-ttu-id="a7b65-176">Upewnij się, że widoczny AzureSqlLinkedService w widoku drzewa po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="a7b65-176">Confirm that you see the AzureSqlLinkedService in the tree view on the left.</span></span>

    ![Widok drzewa połączonej usługi](media/data-factory-stored-proc-activity/tree-view.png)

### <a name="create-an-output-dataset"></a><span data-ttu-id="a7b65-178">Tworzenie wyjściowego zestawu danych</span><span class="sxs-lookup"><span data-stu-id="a7b65-178">Create an output dataset</span></span>
<span data-ttu-id="a7b65-179">Należy określić wyjściowy zestaw danych działania procedura składowana nawet wtedy, gdy procedura składowana nie zwraca żadnych danych.</span><span class="sxs-lookup"><span data-stu-id="a7b65-179">You must specify an output dataset for a stored procedure activity even if the stored procedure does not produce any data.</span></span> <span data-ttu-id="a7b65-180">To, ponieważ jest on wyjściowy zestaw danych, które dyski harmonogram działania (częstotliwość działanie jest uruchamiane — co godzinę, codziennie, itp.).</span><span class="sxs-lookup"><span data-stu-id="a7b65-180">That's because it's the output dataset that drives the schedule of the activity (how often the activity is run - hourly, daily, etc.).</span></span> <span data-ttu-id="a7b65-181">Wyjściowy zestaw danych musi używać **połączona usługa** odwołujący się do bazy danych SQL Azure lub usługi Azure SQL Data Warehouse lub bazy danych programu SQL Server w której ma zostać procedurę składowaną, aby uruchomić.</span><span class="sxs-lookup"><span data-stu-id="a7b65-181">The output dataset must use a **linked service** that refers to an Azure SQL Database or an Azure SQL Data Warehouse or a SQL Server Database in which you want the stored procedure to run.</span></span> <span data-ttu-id="a7b65-182">Wyjściowy zestaw danych może stanowić sposób przekazać wyników procedury składowanej dla kolejnych przetwarzania przez inne działanie ([łańcucha działania](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) w potoku.</span><span class="sxs-lookup"><span data-stu-id="a7b65-182">The output dataset can serve as a way to pass the result of the stored procedure for subsequent processing by another activity ([chaining activities](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) in the pipeline.</span></span> <span data-ttu-id="a7b65-183">Jednak fabryki danych nie automatycznie zapisuje dane wyjściowe procedury składowanej do tego elementu dataset.</span><span class="sxs-lookup"><span data-stu-id="a7b65-183">However, Data Factory does not automatically write the output of a stored procedure to this dataset.</span></span> <span data-ttu-id="a7b65-184">Jest procedury przechowywanej, która zapisuje do tabeli SQL, która wskazuje wyjściowego zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="a7b65-184">It is the stored procedure that writes to a SQL table that the output dataset points to.</span></span> <span data-ttu-id="a7b65-185">W niektórych przypadkach może być wyjściowy zestaw danych **fikcyjny dataset** (zestawu danych, który wskazuje tabelę, która naprawdę nie przechowuje dane wyjściowe procedury składowanej).</span><span class="sxs-lookup"><span data-stu-id="a7b65-185">In some cases, the output dataset can be a **dummy dataset** (a dataset that points to a table that does not really hold output of the stored procedure).</span></span> <span data-ttu-id="a7b65-186">Tego fikcyjny zestawu danych jest używany tylko w celu określenia harmonogram uruchamiania działania procedury składowanej.</span><span class="sxs-lookup"><span data-stu-id="a7b65-186">This dummy dataset is used only to specify the schedule for running the stored procedure activity.</span></span> 

1. <span data-ttu-id="a7b65-187">Kliknij przycisk **... Więcej** na pasku narzędzi kliknij **nowy zestaw danych**i kliknij przycisk **Azure SQL**.</span><span class="sxs-lookup"><span data-stu-id="a7b65-187">Click **... More** on the toolbar, click **New dataset**, and click **Azure SQL**.</span></span> <span data-ttu-id="a7b65-188">**Nowy zestaw danych** na pasku poleceń i wybierz **Azure SQL**.</span><span class="sxs-lookup"><span data-stu-id="a7b65-188">**New dataset** on the command bar and select **Azure SQL**.</span></span>

    ![Widok drzewa połączonej usługi](media/data-factory-stored-proc-activity/new-dataset.png)
2. <span data-ttu-id="a7b65-190">Skopiuj/Wklej poniższy skrypt JSON w celu edytora JSON.</span><span class="sxs-lookup"><span data-stu-id="a7b65-190">Copy/paste the following JSON script in to the JSON editor.</span></span>

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
3. <span data-ttu-id="a7b65-191">Aby wdrożyć zestawu danych, kliknij przycisk **Wdróż** na pasku poleceń.</span><span class="sxs-lookup"><span data-stu-id="a7b65-191">To deploy the dataset, click **Deploy** on the command bar.</span></span> <span data-ttu-id="a7b65-192">Upewnij się, że jest wyświetlany element dataset w widoku drzewa.</span><span class="sxs-lookup"><span data-stu-id="a7b65-192">Confirm that you see the dataset in the tree view.</span></span>

    ![Widok drzewa z połączonych usług](media/data-factory-stored-proc-activity/tree-view-2.png)

### <a name="create-a-pipeline-with-sqlserverstoredprocedure-activity"></a><span data-ttu-id="a7b65-194">Utworzyć potok z działaniem SqlServerStoredProcedure</span><span class="sxs-lookup"><span data-stu-id="a7b65-194">Create a pipeline with SqlServerStoredProcedure activity</span></span>
<span data-ttu-id="a7b65-195">Teraz Utwórzmy potoku z działania procedury składowanej.</span><span class="sxs-lookup"><span data-stu-id="a7b65-195">Now, let's create a pipeline with a stored procedure activity.</span></span> 

<span data-ttu-id="a7b65-196">Zwróć uwagę następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="a7b65-196">Notice the following properties:</span></span> 

- <span data-ttu-id="a7b65-197">**Typu** właściwość jest ustawiona na **SqlServerStoredProcedure**.</span><span class="sxs-lookup"><span data-stu-id="a7b65-197">The **type** property is set to **SqlServerStoredProcedure**.</span></span> 
- <span data-ttu-id="a7b65-198">**StoredProcedureName** w typ właściwości jest równa **sp_sample** (Nazwa procedury składowanej).</span><span class="sxs-lookup"><span data-stu-id="a7b65-198">The **storedProcedureName** in type properties is set to **sp_sample** (name of the stored procedure).</span></span>
- <span data-ttu-id="a7b65-199">**StoredProcedureParameters** sekcja zawiera jeden parametr o nazwie **wartości daty i godziny**.</span><span class="sxs-lookup"><span data-stu-id="a7b65-199">The **storedProcedureParameters** section contains one parameter named **DataTime**.</span></span> <span data-ttu-id="a7b65-200">Nazwa i wielkość liter w wyrazie parametru w formacie JSON muszą być zgodne, nazwa i wielkość liter w wyrazie parametru w definicji procedury składowanej.</span><span class="sxs-lookup"><span data-stu-id="a7b65-200">Name and casing of the parameter in JSON must match the name and casing of the parameter in the stored procedure definition.</span></span> <span data-ttu-id="a7b65-201">Jeśli należy przekazać wartość null dla parametru, należy użyć składni: `"param1": null` (tylko małe litery).</span><span class="sxs-lookup"><span data-stu-id="a7b65-201">If you need pass null for a parameter, use the syntax: `"param1": null` (all lowercase).</span></span>
 
1. <span data-ttu-id="a7b65-202">Kliknij przycisk **... Więcej** na pasku poleceń i kliknij przycisk **nowy potok**.</span><span class="sxs-lookup"><span data-stu-id="a7b65-202">Click **... More** on the command bar and click **New pipeline**.</span></span>
2. <span data-ttu-id="a7b65-203">Skopiuj/Wklej poniższy fragment kodu JSON:</span><span class="sxs-lookup"><span data-stu-id="a7b65-203">Copy/paste the following JSON snippet:</span></span>   

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
3. <span data-ttu-id="a7b65-204">Aby wdrożyć potok, kliknij przycisk **Wdróż** na pasku narzędzi.</span><span class="sxs-lookup"><span data-stu-id="a7b65-204">To deploy the pipeline, click **Deploy** on the toolbar.</span></span>  

### <a name="monitor-the-pipeline"></a><span data-ttu-id="a7b65-205">Monitorowanie potoku</span><span class="sxs-lookup"><span data-stu-id="a7b65-205">Monitor the pipeline</span></span>
1. <span data-ttu-id="a7b65-206">Kliknij przycisk **X**, aby zamknąć bloki Edytora fabryki danych i przejść z powrotem do bloku Fabryka danych, a następnie kliknij przycisk **Diagram**.</span><span class="sxs-lookup"><span data-stu-id="a7b65-206">Click **X** to close Data Factory Editor blades and to navigate back to the Data Factory blade, and click **Diagram**.</span></span>

    ![Diagram kafelka](media/data-factory-stored-proc-activity/data-factory-diagram-tile.png)
2. <span data-ttu-id="a7b65-208">Na stronie **Widok diagramu** zostanie wyświetlony przegląd potoków i zestawów danych używanych w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="a7b65-208">In the **Diagram View**, you see an overview of the pipelines, and datasets used in this tutorial.</span></span>

    ![Diagram kafelka](media/data-factory-stored-proc-activity/data-factory-diagram-view.png)
3. <span data-ttu-id="a7b65-210">W widoku diagramu, kliknij dwukrotnie element dataset `sprocsampleout`.</span><span class="sxs-lookup"><span data-stu-id="a7b65-210">In the Diagram View, double-click the dataset `sprocsampleout`.</span></span> <span data-ttu-id="a7b65-211">Zostanie wyświetlony wycinków w stanie gotowe.</span><span class="sxs-lookup"><span data-stu-id="a7b65-211">You see the slices in Ready state.</span></span> <span data-ttu-id="a7b65-212">Powinien istnieć pięć wycinków, ponieważ wycinek jest tworzone dla każdej godziny od czasu rozpoczęcia i godzina zakończenia w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="a7b65-212">There should be five slices because a slice is produced for each hour between the start time and end time from the JSON.</span></span>

    ![Diagram kafelka](media/data-factory-stored-proc-activity/data-factory-slices.png)
4. <span data-ttu-id="a7b65-214">Gdy wycinek jest **gotowe** stanu, uruchom `select * from sampletable` zapytanie w bazie danych Azure SQL, aby sprawdzić, czy dane dodano do tabeli przez procedurę składowaną.</span><span class="sxs-lookup"><span data-stu-id="a7b65-214">When a slice is in **Ready** state, run a `select * from sampletable` query against the Azure SQL database to verify that the data was inserted in to the table by the stored procedure.</span></span>

   ![dane wyjściowe](./media/data-factory-stored-proc-activity/output.png)

   <span data-ttu-id="a7b65-216">Zobacz [monitorować potoku](data-factory-monitor-manage-pipelines.md) szczegółowe informacje o monitorowaniu potoki fabryki danych Azure.</span><span class="sxs-lookup"><span data-stu-id="a7b65-216">See [Monitor the pipeline](data-factory-monitor-manage-pipelines.md) for detailed information about monitoring Azure Data Factory pipelines.</span></span>  


## <a name="specify-an-input-dataset"></a><span data-ttu-id="a7b65-217">Określ zestaw danych wejściowych</span><span class="sxs-lookup"><span data-stu-id="a7b65-217">Specify an input dataset</span></span>
<span data-ttu-id="a7b65-218">W tym przewodnikiem działania procedury składowanej nie ma żadnych wejściowe zestawy danych.</span><span class="sxs-lookup"><span data-stu-id="a7b65-218">In the walkthrough, stored procedure activity does not have any input datasets.</span></span> <span data-ttu-id="a7b65-219">Jeśli określisz zestaw danych wejściowych działania procedury składowanej nie działa do momentu wycinka wejściowy zestaw danych jest dostępna (w stanie innym niż Ready).</span><span class="sxs-lookup"><span data-stu-id="a7b65-219">If you specify an input dataset, the stored procedure activity does not run until the slice of input dataset is available (in Ready state).</span></span> <span data-ttu-id="a7b65-220">Zestaw danych może być zewnętrzny zestaw danych, (tj. nie jest generowany przez innego działania w tym samym potoku) lub wewnętrzny zestawu danych, który jest generowany przez działanie w strumieniu przychodzącym (działania wykonywane przed tego działania).</span><span class="sxs-lookup"><span data-stu-id="a7b65-220">The dataset can be an external dataset (that is not produced by another activity in the same pipeline) or an internal dataset that is produced by an upstream activity (the activity that runs before this activity).</span></span> <span data-ttu-id="a7b65-221">Można określić wiele zestawów wejściowych danych działania procedury składowanej.</span><span class="sxs-lookup"><span data-stu-id="a7b65-221">You can specify multiple input datasets for the stored procedure activity.</span></span> <span data-ttu-id="a7b65-222">Jeśli tak zrobisz, działania procedury składowanej działa tylko wtedy, gdy wszystkie fragmenty wejściowy zestaw danych są dostępne (w stanie gotowe).</span><span class="sxs-lookup"><span data-stu-id="a7b65-222">If you do so, the stored procedure activity runs only when all the input dataset slices are available (in Ready state).</span></span> <span data-ttu-id="a7b65-223">Wejściowy zestaw danych nie mogą być używane w procedurze składowanej jako parametr.</span><span class="sxs-lookup"><span data-stu-id="a7b65-223">The input dataset cannot be consumed in the stored procedure as a parameter.</span></span> <span data-ttu-id="a7b65-224">Tylko służy do sprawdzania zależności przed rozpoczęciem działania procedury składowanej.</span><span class="sxs-lookup"><span data-stu-id="a7b65-224">It is only used to check the dependency before starting the stored procedure activity.</span></span>

## <a name="chaining-with-other-activities"></a><span data-ttu-id="a7b65-225">Łańcuch serwerów z innymi działaniami</span><span class="sxs-lookup"><span data-stu-id="a7b65-225">Chaining with other activities</span></span>
<span data-ttu-id="a7b65-226">Jeśli chcesz tworzyć łańcuchy działania nadrzędnego tego działania, określ dane wyjściowe działania nadrzędnego jako dane wejściowe tego działania.</span><span class="sxs-lookup"><span data-stu-id="a7b65-226">If you want to chain an upstream activity with this activity, specify the output of the upstream activity as an input of this activity.</span></span> <span data-ttu-id="a7b65-227">Po wykonaniu tego działania procedury składowanej nie działa, dopiero po ukończeniu działania nadrzędnego i wyjściowy zestaw danych działania nadrzędnego jest dostępna (w stanie gotowe).</span><span class="sxs-lookup"><span data-stu-id="a7b65-227">When you do so, the stored procedure activity does not run until the upstream activity completes and the output dataset of the upstream activity is available (in Ready status).</span></span> <span data-ttu-id="a7b65-228">Wyjściowe zestawy danych z wielu działań nadrzędnego może służyć jako wejściowe zestawy danych działania procedury składowanej.</span><span class="sxs-lookup"><span data-stu-id="a7b65-228">You can specify output datasets of multiple upstream activities as input datasets of the stored procedure activity.</span></span> <span data-ttu-id="a7b65-229">Po wykonaniu tego działania procedury składowanej działa tylko wtedy, gdy są dostępne wszystkie fragmenty wejściowy zestaw danych.</span><span class="sxs-lookup"><span data-stu-id="a7b65-229">When you do so, the stored procedure activity runs only when all the input dataset slices are available.</span></span>  

<span data-ttu-id="a7b65-230">W poniższym przykładzie jest dane wyjściowe działania kopiowania: OutputDataset, która jest wartością wejściową działania procedury składowanej.</span><span class="sxs-lookup"><span data-stu-id="a7b65-230">In the following example, the output of the copy activity is: OutputDataset, which is an input of the stored procedure activity.</span></span> <span data-ttu-id="a7b65-231">W związku z tym działania procedury składowanej nie działa, dopiero po ukończeniu działania kopiowania i wycinek OutputDataset jest dostępna (w stanie gotowe).</span><span class="sxs-lookup"><span data-stu-id="a7b65-231">Therefore, the stored procedure activity does not run until the copy activity completes and the OutputDataset slice is available (in Ready state).</span></span> <span data-ttu-id="a7b65-232">Jeśli określisz wiele zestawów danych wejściowych działania procedury składowanej nie działa, dopóki wszystkie fragmenty wejściowy zestaw danych są dostępne (w stanie gotowe).</span><span class="sxs-lookup"><span data-stu-id="a7b65-232">If you specify multiple input datasets, the stored procedure activity does not run until all the input dataset slices are available (in Ready state).</span></span> <span data-ttu-id="a7b65-233">Wejściowe zestawy danych nie można użyć bezpośrednio jako parametry działania procedury składowanej.</span><span class="sxs-lookup"><span data-stu-id="a7b65-233">The input datasets cannot be used directly as parameters to the stored procedure activity.</span></span> 

<span data-ttu-id="a7b65-234">Aby uzyskać więcej informacji na tworzenie łańcucha działań, zobacz [wielu działań w potoku](data-factory-create-pipelines.md#multiple-activities-in-a-pipeline)</span><span class="sxs-lookup"><span data-stu-id="a7b65-234">For more information on chaining activities, see [multiple activities in a pipeline](data-factory-create-pipelines.md#multiple-activities-in-a-pipeline)</span></span>

```json
{

    "name": "ADFTutorialPipeline",
    "properties": {
        "description": "Copy data from a blob to blob",
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

<span data-ttu-id="a7b65-235">Podobnie Aby połączyć działania procedury magazynu o **działania podrzędne** (działań uruchamianych po ukończeniu działania procedury składowanej), określ wyjściowy zestaw danych działania procedura składowana jako danych wejściowych działanie podrzędne w potoku.</span><span class="sxs-lookup"><span data-stu-id="a7b65-235">Similarly, to link the store procedure activity with **downstream activities** (the activities that run after the stored procedure activity completes), specify the output dataset of the stored procedure activity as an input of the downstream activity in the pipeline.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a7b65-236">Podczas kopiowania danych do usługi Azure SQL Database lub SQL Server, można skonfigurować **SqlSink** w przypadku działania kopiowania, aby wywołać procedurę składowaną przy użyciu **sqlWriterStoredProcedureName** właściwości.</span><span class="sxs-lookup"><span data-stu-id="a7b65-236">When copying data into Azure SQL Database or SQL Server, you can configure the **SqlSink** in copy activity to invoke a stored procedure by using the **sqlWriterStoredProcedureName** property.</span></span> <span data-ttu-id="a7b65-237">Aby uzyskać więcej informacji, zobacz [wywołaj procedurę składowaną z działania kopiowania](data-factory-invoke-stored-procedure-from-copy-activity.md).</span><span class="sxs-lookup"><span data-stu-id="a7b65-237">For more information, see [Invoke stored procedure from copy activity](data-factory-invoke-stored-procedure-from-copy-activity.md).</span></span> <span data-ttu-id="a7b65-238">Aby uzyskać więcej informacji dotyczących właściwości, zobacz następujące artykuły łącznika: [bazy danych SQL Azure](data-factory-azure-sql-connector.md#copy-activity-properties), [programu SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="a7b65-238">For details about the property, see the following connector articles: [Azure SQL Database](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties).</span></span>
>  
> <span data-ttu-id="a7b65-239">Podczas kopiowania danych z bazy danych SQL Azure lub programu SQL Server lub magazyn danych SQL Azure, możesz skonfigurować **SqlSource** w przypadku działania kopiowania, aby wywołać procedurę składowaną można odczytać danych ze źródłowej bazy danych przy użyciu  **sqlReaderStoredProcedureName** właściwości.</span><span class="sxs-lookup"><span data-stu-id="a7b65-239">When copying data from Azure SQL Database or SQL Server or Azure SQL Data Warehouse, you can configure **SqlSource** in copy activity to invoke a stored procedure to read data from the source database by using the **sqlReaderStoredProcedureName** property.</span></span> <span data-ttu-id="a7b65-240">Aby uzyskać więcej informacji, zobacz następujące artykuły łącznika: [bazy danych SQL Azure](data-factory-azure-sql-connector.md#copy-activity-properties), [programu SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties), [magazyn danych SQL Azure](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties)</span><span class="sxs-lookup"><span data-stu-id="a7b65-240">For more information, see the following connector articles: [Azure SQL Database](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties), [Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties)</span></span>          

## <a name="json-format"></a><span data-ttu-id="a7b65-241">JSON format</span><span class="sxs-lookup"><span data-stu-id="a7b65-241">JSON format</span></span>
<span data-ttu-id="a7b65-242">Oto formatu JSON określających działania dotyczącego procedury składowanej:</span><span class="sxs-lookup"><span data-stu-id="a7b65-242">Here is the JSON format for defining a Stored Procedure Activity:</span></span>

```JSON
{
    "name": "SQLSPROCActivity",
    "description": "description",
    "type": "SqlServerStoredProcedure",
    "inputs":  [ { "name": "inputtable"  } ],
    "outputs":  [ { "name": "outputtable" } ],
    "typeProperties":
    {
        "storedProcedureName": "<name of the stored procedure>",
        "storedProcedureParameters":  
        {
            "param1": "param1Value"
            …
        }
    }
}
```

<span data-ttu-id="a7b65-243">W poniższej tabeli opisano te właściwości JSON:</span><span class="sxs-lookup"><span data-stu-id="a7b65-243">The following table describes these JSON properties:</span></span>

| <span data-ttu-id="a7b65-244">Właściwość</span><span class="sxs-lookup"><span data-stu-id="a7b65-244">Property</span></span> | <span data-ttu-id="a7b65-245">Opis</span><span class="sxs-lookup"><span data-stu-id="a7b65-245">Description</span></span> | <span data-ttu-id="a7b65-246">Wymagane</span><span class="sxs-lookup"><span data-stu-id="a7b65-246">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a7b65-247">name</span><span class="sxs-lookup"><span data-stu-id="a7b65-247">name</span></span> | <span data-ttu-id="a7b65-248">Nazwa działania</span><span class="sxs-lookup"><span data-stu-id="a7b65-248">Name of the activity</span></span> |<span data-ttu-id="a7b65-249">Tak</span><span class="sxs-lookup"><span data-stu-id="a7b65-249">Yes</span></span> |
| <span data-ttu-id="a7b65-250">Opis elementu</span><span class="sxs-lookup"><span data-stu-id="a7b65-250">description</span></span> |<span data-ttu-id="a7b65-251">Tekst opisujący działanie służy do</span><span class="sxs-lookup"><span data-stu-id="a7b65-251">Text describing what the activity is used for</span></span> |<span data-ttu-id="a7b65-252">Nie</span><span class="sxs-lookup"><span data-stu-id="a7b65-252">No</span></span> |
| <span data-ttu-id="a7b65-253">type</span><span class="sxs-lookup"><span data-stu-id="a7b65-253">type</span></span> | <span data-ttu-id="a7b65-254">Musi mieć wartość: **SqlServerStoredProcedure**</span><span class="sxs-lookup"><span data-stu-id="a7b65-254">Must be set to: **SqlServerStoredProcedure**</span></span> | <span data-ttu-id="a7b65-255">Tak</span><span class="sxs-lookup"><span data-stu-id="a7b65-255">Yes</span></span> |
| <span data-ttu-id="a7b65-256">Dane wejściowe</span><span class="sxs-lookup"><span data-stu-id="a7b65-256">inputs</span></span> | <span data-ttu-id="a7b65-257">Opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="a7b65-257">Optional.</span></span> <span data-ttu-id="a7b65-258">Jeśli określisz wejściowy zestaw danych, musi być dostępny (w stanie "Gotowe") dla działania procedury składowanej do uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="a7b65-258">If you do specify an input dataset, it must be available (in ‘Ready’ status) for the stored procedure activity to run.</span></span> <span data-ttu-id="a7b65-259">Wejściowy zestaw danych nie mogą być używane w procedurze składowanej jako parametr.</span><span class="sxs-lookup"><span data-stu-id="a7b65-259">The input dataset cannot be consumed in the stored procedure as a parameter.</span></span> <span data-ttu-id="a7b65-260">Tylko służy do sprawdzania zależności przed rozpoczęciem działania procedury składowanej.</span><span class="sxs-lookup"><span data-stu-id="a7b65-260">It is only used to check the dependency before starting the stored procedure activity.</span></span> |<span data-ttu-id="a7b65-261">Nie</span><span class="sxs-lookup"><span data-stu-id="a7b65-261">No</span></span> |
| <span data-ttu-id="a7b65-262">dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="a7b65-262">outputs</span></span> | <span data-ttu-id="a7b65-263">Należy określić zestaw danych wyjściowych dla działania procedury składowanej.</span><span class="sxs-lookup"><span data-stu-id="a7b65-263">You must specify an output dataset for a stored procedure activity.</span></span> <span data-ttu-id="a7b65-264">Określa wyjściowy zestaw danych **harmonogram** działania procedury składowanej (co godzinę, co tydzień, co miesiąc, itp.).</span><span class="sxs-lookup"><span data-stu-id="a7b65-264">Output dataset specifies the **schedule** for the stored procedure activity (hourly, weekly, monthly, etc.).</span></span> <br/><br/><span data-ttu-id="a7b65-265">Wyjściowy zestaw danych musi używać **połączona usługa** odwołujący się do bazy danych SQL Azure lub usługi Azure SQL Data Warehouse lub bazy danych programu SQL Server w której ma zostać procedurę składowaną, aby uruchomić.</span><span class="sxs-lookup"><span data-stu-id="a7b65-265">The output dataset must use a **linked service** that refers to an Azure SQL Database or an Azure SQL Data Warehouse or a SQL Server Database in which you want the stored procedure to run.</span></span> <br/><br/><span data-ttu-id="a7b65-266">Wyjściowy zestaw danych może stanowić sposób przekazać wyników procedury składowanej dla kolejnych przetwarzania przez inne działanie ([łańcucha działania](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) w potoku.</span><span class="sxs-lookup"><span data-stu-id="a7b65-266">The output dataset can serve as a way to pass the result of the stored procedure for subsequent processing by another activity ([chaining activities](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) in the pipeline.</span></span> <span data-ttu-id="a7b65-267">Jednak fabryki danych nie automatycznie zapisuje dane wyjściowe procedury składowanej do tego elementu dataset.</span><span class="sxs-lookup"><span data-stu-id="a7b65-267">However, Data Factory does not automatically write the output of a stored procedure to this dataset.</span></span> <span data-ttu-id="a7b65-268">Jest procedury przechowywanej, która zapisuje do tabeli SQL, która wskazuje wyjściowego zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="a7b65-268">It is the stored procedure that writes to a SQL table that the output dataset points to.</span></span> <br/><br/><span data-ttu-id="a7b65-269">W niektórych przypadkach może być wyjściowy zestaw danych **fikcyjny zestawu danych**, które służą tylko do określ harmonogram uruchamiania działania procedury składowanej.</span><span class="sxs-lookup"><span data-stu-id="a7b65-269">In some cases, the output dataset can be a **dummy dataset**, which is used only to specify the schedule for running the stored procedure activity.</span></span> |<span data-ttu-id="a7b65-270">Tak</span><span class="sxs-lookup"><span data-stu-id="a7b65-270">Yes</span></span> |
| <span data-ttu-id="a7b65-271">storedProcedureName</span><span class="sxs-lookup"><span data-stu-id="a7b65-271">storedProcedureName</span></span> |<span data-ttu-id="a7b65-272">Określ nazwę procedury składowanej bazy danych Azure SQL lub w bazie danych magazynu danych SQL Azure lub programu SQL Server, reprezentowanego przez połączonej usługi, która używa tabeli wyników.</span><span class="sxs-lookup"><span data-stu-id="a7b65-272">Specify the name of the stored procedure in the Azure SQL database or Azure SQL Data Warehouse or SQL Server database that is represented by the linked service that the output table uses.</span></span> |<span data-ttu-id="a7b65-273">Tak</span><span class="sxs-lookup"><span data-stu-id="a7b65-273">Yes</span></span> |
| <span data-ttu-id="a7b65-274">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="a7b65-274">storedProcedureParameters</span></span> |<span data-ttu-id="a7b65-275">Określ wartości dla parametrów procedury składowanej.</span><span class="sxs-lookup"><span data-stu-id="a7b65-275">Specify values for stored procedure parameters.</span></span> <span data-ttu-id="a7b65-276">Jeśli chcesz przekazać wartości null dla parametru należy użyć składni: "param1": wartość null (małe litery).</span><span class="sxs-lookup"><span data-stu-id="a7b65-276">If you need to pass null for a parameter, use the syntax: "param1": null (all lower case).</span></span> <span data-ttu-id="a7b65-277">Zobacz poniższy przykład, aby dowiedzieć się więcej o korzystaniu z tej właściwości.</span><span class="sxs-lookup"><span data-stu-id="a7b65-277">See the following sample to learn about using this property.</span></span> |<span data-ttu-id="a7b65-278">Nie</span><span class="sxs-lookup"><span data-stu-id="a7b65-278">No</span></span> |

## <a name="passing-a-static-value"></a><span data-ttu-id="a7b65-279">Przekazywanie wartości statycznej</span><span class="sxs-lookup"><span data-stu-id="a7b65-279">Passing a static value</span></span>
<span data-ttu-id="a7b65-280">Teraz załóżmy należy rozważyć dodanie inną kolumnę o nazwie "Scenariusza" w tabeli zawierającej wartości statycznej o nazwie "Próbki dokumentu".</span><span class="sxs-lookup"><span data-stu-id="a7b65-280">Now, let’s consider adding another column named ‘Scenario’ in the table containing a static value called ‘Document sample’.</span></span>

![Przykładowe dane 2](./media/data-factory-stored-proc-activity/sample-data-2.png)

<span data-ttu-id="a7b65-282">**Tabela:**</span><span class="sxs-lookup"><span data-stu-id="a7b65-282">**Table:**</span></span>

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

<span data-ttu-id="a7b65-283">**Procedura składowana:**</span><span class="sxs-lookup"><span data-stu-id="a7b65-283">**Stored procedure:**</span></span>

```SQL
CREATE PROCEDURE sp_sample2 @DateTime nvarchar(127) , @Scenario nvarchar(127)

AS

BEGIN
    INSERT INTO [sampletable2]
    VALUES (newid(), @DateTime, @Scenario)
END
```

<span data-ttu-id="a7b65-284">Teraz, Przekaż **scenariusza** parametr i wartość z działania procedury składowanej.</span><span class="sxs-lookup"><span data-stu-id="a7b65-284">Now, pass the **Scenario** parameter and the value from the stored procedure activity.</span></span> <span data-ttu-id="a7b65-285">**TypeProperties** sekcji w poprzednim przykładzie wygląda następująco: następujący fragment kodu:</span><span class="sxs-lookup"><span data-stu-id="a7b65-285">The **typeProperties** section in the preceding sample looks like the following snippet:</span></span>

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

<span data-ttu-id="a7b65-286">**Zestaw danych z fabryki danych:**</span><span class="sxs-lookup"><span data-stu-id="a7b65-286">**Data Factory dataset:**</span></span>

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

<span data-ttu-id="a7b65-287">**Potok fabryki danych**</span><span class="sxs-lookup"><span data-stu-id="a7b65-287">**Data Factory pipeline**</span></span>

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