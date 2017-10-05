---
title: "Ładowanie terabajtów danych do usługi SQL Data Warehouse | Dokumentacja firmy Microsoft"
description: "Pokazuje, jak 1 TB danych mogą być ładowane do usługi Azure SQL Data Warehouse z fabryką danych Azure w obszarze 15 minut"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: a6c133c0-ced2-463c-86f0-a07b00c9e37f
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jingwang
ms.openlocfilehash: c29f1f01b660c4eb780e178a68036327fafa9ba6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="load-1-tb-into-azure-sql-data-warehouse-under-15-minutes-with-data-factory"></a><span data-ttu-id="17629-103">Ładowanie 1 TB do usługi Azure SQL Data Warehouse w obszarze 15 minut przy użyciu fabryki danych</span><span class="sxs-lookup"><span data-stu-id="17629-103">Load 1 TB into Azure SQL Data Warehouse under 15 minutes with Data Factory</span></span>
<span data-ttu-id="17629-104">[Usługa Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md) oparte na chmurze, skalowalnych w poziomie bazy danych jest w stanie przetwarzanie bardzo dużych woluminów danych relacyjnych i nierelacyjnych.</span><span class="sxs-lookup"><span data-stu-id="17629-104">[Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md) is a cloud-based, scale-out database capable of processing massive volumes of data, both relational and non-relational.</span></span>  <span data-ttu-id="17629-105">Zbudowany w oparciu o architekturę masowego przetwarzania równoległego (MPP), usługa SQL Data Warehouse jest zoptymalizowana pod kątem obciążeń magazynu danych przedsiębiorstwa.</span><span class="sxs-lookup"><span data-stu-id="17629-105">Built on massively parallel processing (MPP) architecture, SQL Data Warehouse is optimized for enterprise data warehouse workloads.</span></span>  <span data-ttu-id="17629-106">Zapewnia elastyczność chmury elastycznie skalować magazyn i zasobów obliczeniowych niezależnie.</span><span class="sxs-lookup"><span data-stu-id="17629-106">It offers cloud elasticity with the flexibility to scale storage and compute independently.</span></span>

<span data-ttu-id="17629-107">Wprowadzenie do korzystania z usługi Azure SQL Data Warehouse jest teraz łatwiejsze niż kiedykolwiek przy użyciu **fabryki danych Azure**.</span><span class="sxs-lookup"><span data-stu-id="17629-107">Getting started with Azure SQL Data Warehouse is now easier than ever using **Azure Data Factory**.</span></span>  <span data-ttu-id="17629-108">Fabryka danych Azure to usługa integracji pełni zarządzanych danych oparte na chmurze, używany do wypełniania SQL Data Warehouse przy użyciu danych z istniejącego systemu i zapisywanie cenny czas podczas oceny usługi SQL Data Warehouse i tworzenia rozwiązań analizy.</span><span class="sxs-lookup"><span data-stu-id="17629-108">Azure Data Factory is a fully managed cloud-based data integration service, which can be used to populate a SQL Data Warehouse with the data from your existing system, and saving you valuable time while evaluating SQL Data Warehouse and building your analytics solutions.</span></span> <span data-ttu-id="17629-109">Poniżej przedstawiono najważniejsze zalety ładowania danych do usługi Azure SQL Data Warehouse przy użyciu fabryki danych Azure:</span><span class="sxs-lookup"><span data-stu-id="17629-109">Here are the key benefits of loading data into Azure SQL Data Warehouse using Azure Data Factory:</span></span>

* <span data-ttu-id="17629-110">**Można skonfigurować**: Kreator intuicyjne krok 5 z bez skryptu wymagane.</span><span class="sxs-lookup"><span data-stu-id="17629-110">**Easy to set up**: 5-step intuitive wizard with no scripting required.</span></span>
* <span data-ttu-id="17629-111">**Obsługa magazynu danych sformatowanego**: wbudowaną obsługę bogaty zestaw lokalnymi i magazyny danych oparte na chmurze.</span><span class="sxs-lookup"><span data-stu-id="17629-111">**Rich data store support**: built-in support for a rich set of on-premises and cloud-based data stores.</span></span>
* <span data-ttu-id="17629-112">**Bezpieczne i zgodne**: dane są przesyłane za pośrednictwem protokołu HTTPS lub ExpressRoute i zapewnia obecności usługi globalne dane nigdy nie przekracza granic geograficznych</span><span class="sxs-lookup"><span data-stu-id="17629-112">**Secure and compliant**: data is transferred over HTTPS or ExpressRoute, and global service presence ensures your data never leaves the geographical boundary</span></span>
* <span data-ttu-id="17629-113">**Bezkonkurencyjne wydajności przy użyciu programu PolyBase** — przy użyciu programu Polybase jest najbardziej wydajnym sposobem przenoszenia danych do usługi Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="17629-113">**Unparalleled performance by using PolyBase** – Using Polybase is the most efficient way to move data into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="17629-114">Funkcja tymczasowych obiektów blob, można osiągnąć szybkości wysokie obciążenie ze wszystkich typów magazynów danych oprócz magazynu obiektów Blob platformy Azure, który aparat Polybase obsługuje domyślnie.</span><span class="sxs-lookup"><span data-stu-id="17629-114">Using the staging blob feature, you can achieve high load speeds from all types of data stores besides Azure Blob storage, which the Polybase supports by default.</span></span>

<span data-ttu-id="17629-115">W tym artykule przedstawiono sposób korzystania z Kreatora kopiowania fabryki danych ładowanie 1 TB danych z magazynu obiektów Blob Azure do usługi Azure SQL Data Warehouse w obszarze 15 minut na ponad 1,2 GB/s przepustowości.</span><span class="sxs-lookup"><span data-stu-id="17629-115">This article shows you how to use Data Factory Copy Wizard to load 1-TB data from Azure Blob Storage into Azure SQL Data Warehouse in under 15 minutes, at over 1.2 GBps throughput.</span></span>

<span data-ttu-id="17629-116">Ten artykuł zawiera instrukcje krok po kroku przenoszenie danych do usługi Azure SQL Data Warehouse przy użyciu Kreatora kopiowania.</span><span class="sxs-lookup"><span data-stu-id="17629-116">This article provides step-by-step instructions for moving data into Azure SQL Data Warehouse by using the Copy Wizard.</span></span>

> [!NOTE]
>  <span data-ttu-id="17629-117">Aby uzyskać ogólne informacje o możliwościach fabryki danych podczas przenoszenia danych do/z usługi Azure SQL Data Warehouse, zobacz [przenoszenie danych do i z usługi Azure SQL Data Warehouse przy użyciu fabryki danych Azure](data-factory-azure-sql-data-warehouse-connector.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="17629-117">For general information about capabilities of Data Factory in moving data to/from Azure SQL Data Warehouse, see [Move data to and from Azure SQL Data Warehouse using Azure Data Factory](data-factory-azure-sql-data-warehouse-connector.md) article.</span></span>
>
> <span data-ttu-id="17629-118">Można również tworzyć przy użyciu portalu Azure, programu Visual Studio, programu PowerShell, potoki itp. Zobacz [samouczek: kopiowanie danych z obiektu Blob Azure do usługi Azure SQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) szybkie przewodnik krok po kroku instrukcje dotyczące używania działania kopiowania w fabryce danych Azure.</span><span class="sxs-lookup"><span data-stu-id="17629-118">You can also build pipelines using Azure portal, Visual Studio, PowerShell, etc. See [Tutorial: Copy data from Azure Blob to Azure SQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for a quick walkthrough with step-by-step instructions for using the Copy Activity in Azure Data Factory.</span></span>  
>
>

## <a name="prerequisites"></a><span data-ttu-id="17629-119">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="17629-119">Prerequisites</span></span>
* <span data-ttu-id="17629-120">Azure Blob Storage: tego eksperymentu używa magazynu obiektów Blob Azure (GRS) do przechowywania TPC-H testowych w zestawie danych.</span><span class="sxs-lookup"><span data-stu-id="17629-120">Azure Blob Storage: this experiment uses Azure Blob Storage (GRS) for storing TPC-H testing dataset.</span></span>  <span data-ttu-id="17629-121">Dowiedz się, jeśli nie masz konta magazynu platformy Azure, [jak utworzyć konto magazynu](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span><span class="sxs-lookup"><span data-stu-id="17629-121">If you do not have an Azure storage account, learn [how to create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span></span>
* <span data-ttu-id="17629-122">[TPC-H](http://www.tpc.org/tpch/) danych: Firma Microsoft będzie używany TPC-H jako testowego zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="17629-122">[TPC-H](http://www.tpc.org/tpch/) data: we are going to use TPC-H as the testing dataset.</span></span>  <span data-ttu-id="17629-123">W tym celu należy użyć `dbgen` z zestawu narzędzi TPC-H, który pomaga wygenerowania zestawu dataset.</span><span class="sxs-lookup"><span data-stu-id="17629-123">To do that, you need to use `dbgen` from TPC-H toolkit, which helps you generate the dataset.</span></span>  <span data-ttu-id="17629-124">Albo można pobrać kodu źródłowego dla `dbgen` z [narzędzia TPC](http://www.tpc.org/tpc_documents_current_versions/current_specifications.asp) i skompiluj go samodzielnie lub pobrać skompilowanym plikiem binarnym z [GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/TPCHTools).</span><span class="sxs-lookup"><span data-stu-id="17629-124">You can either download source code for `dbgen` from [TPC Tools](http://www.tpc.org/tpc_documents_current_versions/current_specifications.asp) and compile it yourself, or download the compiled binary from [GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/TPCHTools).</span></span>  <span data-ttu-id="17629-125">Uruchom dbgen.exe za pomocą następujących poleceń, aby wygenerować plik prosty 1 TB dla `lineitem` tabeli rozpowszechniania przez 10 plików:</span><span class="sxs-lookup"><span data-stu-id="17629-125">Run dbgen.exe with the following commands to generate 1 TB flat file for `lineitem` table spread across 10 files:</span></span>

  * `Dbgen -s 1000 -S **1** -C 10 -T L -v`
  * `Dbgen -s 1000 -S **2** -C 10 -T L -v`
  * <span data-ttu-id="17629-126">…</span><span class="sxs-lookup"><span data-stu-id="17629-126">…</span></span>
  * `Dbgen -s 1000 -S **10** -C 10 -T L -v`

    <span data-ttu-id="17629-127">Teraz skopiuj wygenerowany pliki do obiektów Blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="17629-127">Now copy the generated files to Azure Blob.</span></span>  <span data-ttu-id="17629-128">Zapoznaj się [przenoszenie danych do i z lokalnego systemu plików przy użyciu fabryki danych Azure](data-factory-onprem-file-system-connector.md) dla, jak to zrobić przy użyciu kopii ADF.</span><span class="sxs-lookup"><span data-stu-id="17629-128">Refer to [Move data to and from an on-premises file system by using Azure Data Factory](data-factory-onprem-file-system-connector.md) for how to do that using ADF Copy.</span></span>    
* <span data-ttu-id="17629-129">Usługa Azure SQL Data Warehouse: tego eksperymentu ładuje dane do magazynu danych SQL Azure utworzonych za pomocą dwu 6000</span><span class="sxs-lookup"><span data-stu-id="17629-129">Azure SQL Data Warehouse: this experiment loads data into Azure SQL Data Warehouse created with 6,000 DWUs</span></span>

    <span data-ttu-id="17629-130">Zapoznaj się [Utwórz magazyn danych SQL Azure](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md) szczegółowe informacje dotyczące sposobu tworzenia bazy danych SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="17629-130">Refer to [Create an Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md) for detailed instructions on how to create a SQL Data Warehouse database.</span></span>  <span data-ttu-id="17629-131">Aby uzyskać najlepszą wydajność obciążenia możliwych do usługi SQL Data Warehouse przy użyciu programu Polybase, możemy wybierz maksymalną liczbę jednostek magazynu danych (dwu) dozwolone w ustawieniu wydajności jest 6000 jednostek dwu.</span><span class="sxs-lookup"><span data-stu-id="17629-131">To get the best possible load performance into SQL Data Warehouse using Polybase, we choose maximum number of Data Warehouse Units (DWUs) allowed in the Performance setting, which is 6,000 DWUs.</span></span>

  > [!NOTE]
  > <span data-ttu-id="17629-132">Podczas ładowania z obiektów Blob platformy Azure, ładowanie wydajności danych jest wprost proporcjonalny do liczby jednostek dwu Skonfiguruj na magazyn danych SQL:</span><span class="sxs-lookup"><span data-stu-id="17629-132">When loading from Azure Blob, the data loading performance is directly proportional to the number of DWUs you configure on the SQL Data Warehouse:</span></span>
  >
  > <span data-ttu-id="17629-133">Ładowanie 1 TB do 1000 DWU usługa SQL Data Warehouse uwzględnia 87 minut (przepływność ~ 200 MB/s) podczas ładowania 1 TB 2000 DWU usługa SQL Data Warehouse przyjmuje 46 minut (przepływność ~ 380 MB/s) podczas ładowania 1 TB w 6000 DWU usługa SQL Data Warehouse trwa 14 minut (przepływność ~1.2 GB/s)</span><span class="sxs-lookup"><span data-stu-id="17629-133">Loading 1 TB into 1,000 DWU SQL Data Warehouse takes 87 minutes (~200 MBps throughput) Loading 1 TB into 2,000 DWU SQL Data Warehouse takes 46 minutes (~380 MBps throughput) Loading 1 TB into 6,000 DWU SQL Data Warehouse takes 14 minutes (~1.2 GBps throughput)</span></span>
  >
  >

    <span data-ttu-id="17629-134">Aby utworzyć magazyn danych SQL z dwu 6000, przesuń suwak wydajności do prawej:</span><span class="sxs-lookup"><span data-stu-id="17629-134">To create a SQL Data Warehouse with 6,000 DWUs, move the Performance slider all the way to the right:</span></span>

    ![Suwak wydajności](media/data-factory-load-sql-data-warehouse/performance-slider.png)

    <span data-ttu-id="17629-136">Dla istniejącej bazy danych nie jest skonfigurowany z dwu 6000 można go skalować przy użyciu portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="17629-136">For an existing database that is not configured with 6,000 DWUs, you can scale it up using Azure portal.</span></span>  <span data-ttu-id="17629-137">Przejdź do bazy danych w portalu Azure, a nie **skali** przycisk **omówienie** panelu pokazano na poniższej ilustracji:</span><span class="sxs-lookup"><span data-stu-id="17629-137">Navigate to the database in Azure portal, and there is a **Scale** button in the **Overview** panel shown in the following image:</span></span>

    ![Przycisk skali](media/data-factory-load-sql-data-warehouse/scale-button.png)    

    <span data-ttu-id="17629-139">Kliknij przycisk **skali** przycisk Otwórz panel następujące, przesuń suwak na wartość maksymalna, a następnie kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="17629-139">Click the **Scale** button to open the following panel, move the slider to the maximum value, and click **Save** button.</span></span>

    ![Okno dialogowe skalowania](media/data-factory-load-sql-data-warehouse/scale-dialog.png)

    <span data-ttu-id="17629-141">Tego eksperymentu ładuje dane do usługi Azure SQL Data Warehouse przy użyciu `xlargerc` klasy zasobów.</span><span class="sxs-lookup"><span data-stu-id="17629-141">This experiment loads data into Azure SQL Data Warehouse using `xlargerc` resource class.</span></span>

    <span data-ttu-id="17629-142">Aby uzyskać najlepsze możliwe przepływności, kopii musi zostać wykonana przy użyciu usługi SQL Data Warehouse użytkownik należący do `xlargerc` klasy zasobów.</span><span class="sxs-lookup"><span data-stu-id="17629-142">To achieve best possible throughput, copy needs to be performed using a SQL Data Warehouse user belonging to `xlargerc` resource class.</span></span>  <span data-ttu-id="17629-143">Dowiedz się, jak to zrobić, postępując [zmienić przykład klasy zasobów użytkownika](../sql-data-warehouse/sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).</span><span class="sxs-lookup"><span data-stu-id="17629-143">Learn how to do that by following [Change a user resource class example](../sql-data-warehouse/sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).</span></span>  
* <span data-ttu-id="17629-144">Tworzenie schematu tabeli docelowej bazy danych Azure SQL Data Warehouse, uruchamiając następującą instrukcję DDL:</span><span class="sxs-lookup"><span data-stu-id="17629-144">Create destination table schema in Azure SQL Data Warehouse database, by running the following DDL statement:</span></span>

    ```SQL  
    CREATE TABLE [dbo].[lineitem]
    (
        [L_ORDERKEY] [bigint] NOT NULL,
        [L_PARTKEY] [bigint] NOT NULL,
        [L_SUPPKEY] [bigint] NOT NULL,
        [L_LINENUMBER] [int] NOT NULL,
        [L_QUANTITY] [decimal](15, 2) NULL,
        [L_EXTENDEDPRICE] [decimal](15, 2) NULL,
        [L_DISCOUNT] [decimal](15, 2) NULL,
        [L_TAX] [decimal](15, 2) NULL,
        [L_RETURNFLAG] [char](1) NULL,
        [L_LINESTATUS] [char](1) NULL,
        [L_SHIPDATE] [date] NULL,
        [L_COMMITDATE] [date] NULL,
        [L_RECEIPTDATE] [date] NULL,
        [L_SHIPINSTRUCT] [char](25) NULL,
        [L_SHIPMODE] [char](10) NULL,
        [L_COMMENT] [varchar](44) NULL
    )
    WITH
    (
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    ```
<span data-ttu-id="17629-145">Kroki wymagań wstępnych zakończone firma Microsoft teraz przystąpić do konfigurowania działanie kopiowania za pomocą Kreatora kopiowania.</span><span class="sxs-lookup"><span data-stu-id="17629-145">With the prerequisite steps completed, we are now ready to configure the copy activity using the Copy Wizard.</span></span>

## <a name="launch-copy-wizard"></a><span data-ttu-id="17629-146">Uruchamianie Kreatora kopiowania</span><span class="sxs-lookup"><span data-stu-id="17629-146">Launch Copy Wizard</span></span>
1. <span data-ttu-id="17629-147">Zaloguj się do witryny [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="17629-147">Log in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="17629-148">Kliknij przycisk **+ nowy** z lewego górnego rogu, kliknij przycisk **analizy i analiza**i kliknij przycisk **fabryki danych**.</span><span class="sxs-lookup"><span data-stu-id="17629-148">Click **+ NEW** from the top-left corner, click **Intelligence + analytics**, and click **Data Factory**.</span></span>
3. <span data-ttu-id="17629-149">W bloku **Nowa fabryka danych**:</span><span class="sxs-lookup"><span data-stu-id="17629-149">In the **New data factory** blade:</span></span>

   1. <span data-ttu-id="17629-150">Wprowadź **LoadIntoSQLDWDataFactory** dla **nazwa**.</span><span class="sxs-lookup"><span data-stu-id="17629-150">Enter **LoadIntoSQLDWDataFactory** for the **name**.</span></span>
       <span data-ttu-id="17629-151">Nazwa fabryki danych Azure musi być globalnie unikatowa.</span><span class="sxs-lookup"><span data-stu-id="17629-151">The name of the Azure data factory must be globally unique.</span></span> <span data-ttu-id="17629-152">Jeśli zostanie wyświetlony błąd: **nazwa fabryki danych "LoadIntoSQLDWDataFactory" nie jest dostępna**, Zmień nazwę fabryki danych (na przykład yournameLoadIntoSQLDWDataFactory) i spróbuj ponownie utworzyć.</span><span class="sxs-lookup"><span data-stu-id="17629-152">If you receive the error: **Data factory name “LoadIntoSQLDWDataFactory” is not available**, change the name of the data factory (for example, yournameLoadIntoSQLDWDataFactory) and try creating again.</span></span> <span data-ttu-id="17629-153">Artykuł [Data Factory — Naming Rules](data-factory-naming-rules.md) (Fabryka danych — zasady nazewnictwa) zawiera zasady nazewnictwa artefaktów usługi Fabryka danych.</span><span class="sxs-lookup"><span data-stu-id="17629-153">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>  
   2. <span data-ttu-id="17629-154">Wybierz swoją **subskrypcję** platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="17629-154">Select your Azure **subscription**.</span></span>
   3. <span data-ttu-id="17629-155">Wykonaj jedną z następujących czynności dotyczącą grupy zasobów:</span><span class="sxs-lookup"><span data-stu-id="17629-155">For Resource Group, do one of the following steps:</span></span>
      1. <span data-ttu-id="17629-156">Wybierz pozycję **Użyj istniejącej**, aby wybrać istniejącą grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="17629-156">Select **Use existing** to select an existing resource group.</span></span>
      2. <span data-ttu-id="17629-157">Wybierz pozycję **Utwórz nowy**, aby wprowadzić nazwę grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="17629-157">Select **Create new** to enter a name for a resource group.</span></span>
   4. <span data-ttu-id="17629-158">Wybierz **lokalizację** fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="17629-158">Select a **location** for the data factory.</span></span>
   5. <span data-ttu-id="17629-159">Zaznacz pole wyboru **Przypnij do pulpitu nawigacyjnego** u dołu bloku.</span><span class="sxs-lookup"><span data-stu-id="17629-159">Select **Pin to dashboard** check box at the bottom of the blade.</span></span>  
   6. <span data-ttu-id="17629-160">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="17629-160">Click **Create**.</span></span>
4. <span data-ttu-id="17629-161">Po zakończeniu tworzenia zostanie wyświetlony blok **Fabryka danych**, jak pokazano na poniższej ilustracji:</span><span class="sxs-lookup"><span data-stu-id="17629-161">After the creation is complete, you see the **Data Factory** blade as shown in the following image:</span></span>

   ![Strona główna fabryki danych](media/data-factory-load-sql-data-warehouse/data-factory-home-page-copy-data.png)
5. <span data-ttu-id="17629-163">Na stronie głównej usługi Fabryka danych kliknij kafelek **Kopiowanie danych**, aby uruchomić **Kreatora kopiowania**.</span><span class="sxs-lookup"><span data-stu-id="17629-163">On the Data Factory home page, click the **Copy data** tile to launch **Copy Wizard**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="17629-164">Jeśli widać, że przeglądarka sieci Web jest zablokowana podczas wyświetlania komunikatu „Autoryzowanie...”, wyłącz ustawienie **Blokuj pliki cookie i dane witryn innych firm** lub pozostaw je włączone i utwórz wyjątek dla witryny **login.microsoftonline.com**, a następnie spróbuj ponownie uruchomić kreatora.</span><span class="sxs-lookup"><span data-stu-id="17629-164">If you see that the web browser is stuck at "Authorizing...", disable/uncheck **Block third party cookies and site data** setting (or) keep it enabled and create an exception for **login.microsoftonline.com** and then try launching the wizard again.</span></span>
   >
   >

## <a name="step-1-configure-data-loading-schedule"></a><span data-ttu-id="17629-165">Krok 1: Skonfiguruj harmonogram ładowanie danych</span><span class="sxs-lookup"><span data-stu-id="17629-165">Step 1: Configure data loading schedule</span></span>
<span data-ttu-id="17629-166">Pierwszym krokiem jest aby skonfigurować harmonogram dla ładowania danych.</span><span class="sxs-lookup"><span data-stu-id="17629-166">The first step is to configure the data loading schedule.</span></span>  

<span data-ttu-id="17629-167">Na stronie **Właściwości**:</span><span class="sxs-lookup"><span data-stu-id="17629-167">In the **Properties** page:</span></span>

1. <span data-ttu-id="17629-168">Wprowadź **CopyFromBlobToAzureSqlDataWarehouse** dla **Nazwa zadania**</span><span class="sxs-lookup"><span data-stu-id="17629-168">Enter **CopyFromBlobToAzureSqlDataWarehouse** for **Task name**</span></span>
2. <span data-ttu-id="17629-169">Wybierz **uruchom raz teraz** opcji.</span><span class="sxs-lookup"><span data-stu-id="17629-169">Select **Run once now** option.</span></span>   
3. <span data-ttu-id="17629-170">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="17629-170">Click **Next**.</span></span>  

    ![Kreator kopiowania — strona właściwości](media/data-factory-load-sql-data-warehouse/copy-wizard-properties-page.png)

## <a name="step-2-configure-source"></a><span data-ttu-id="17629-172">Krok 2: Konfigurowanie źródła</span><span class="sxs-lookup"><span data-stu-id="17629-172">Step 2: Configure source</span></span>
<span data-ttu-id="17629-173">W tej sekcji przedstawiono kroki, aby skonfigurować źródło: obiektów Blob platformy Azure zawierającą TPC 1 TB-H pozycji plików.</span><span class="sxs-lookup"><span data-stu-id="17629-173">This section shows you the steps to configure the source: Azure Blob containing the 1-TB TPC-H line item files.</span></span>

1. <span data-ttu-id="17629-174">Wybierz **magazyn obiektów Blob Azure** przechowywania danych, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="17629-174">Select the **Azure Blob Storage** as the data store and click **Next**.</span></span>

    ![Kreator kopiowania — wybierz źródło strony](media/data-factory-load-sql-data-warehouse/select-source-connection.png)

2. <span data-ttu-id="17629-176">Podaj dane połączenia dla konta magazynu obiektów Blob platformy Azure, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="17629-176">Fill in the connection information for the Azure Blob storage account, and click **Next**.</span></span>

    ![Kreator kopiowania — informacje o źródle połączenia](media/data-factory-load-sql-data-warehouse/source-connection-info.png)

3. <span data-ttu-id="17629-178">Wybierz **folderu** zawierający TPC-H wiersz plików z elementami, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="17629-178">Choose the **folder** containing the TPC-H line item files and click **Next**.</span></span>

    ![Kreator kopiowania — wybierz folder wejściowy](media/data-factory-load-sql-data-warehouse/select-input-folder.png)

4. <span data-ttu-id="17629-180">Po kliknięciu **dalej**, ustawienia formatu pliku są wykrywane automatycznie.</span><span class="sxs-lookup"><span data-stu-id="17629-180">Upon clicking **Next**, the file format settings are detected automatically.</span></span>  <span data-ttu-id="17629-181">Sprawdź, upewnij się, że ogranicznik kolumny jest ' | 'zamiast przecinkami domyślne",".</span><span class="sxs-lookup"><span data-stu-id="17629-181">Check to make sure that column delimiter is ‘|’ instead of the default comma ‘,’.</span></span>  <span data-ttu-id="17629-182">Kliknij przycisk **dalej** po przejrzeniu danych.</span><span class="sxs-lookup"><span data-stu-id="17629-182">Click **Next** after you have previewed the data.</span></span>

    ![Kreator kopiowania — ustawienia format pliku](media/data-factory-load-sql-data-warehouse/file-format-settings.png)

## <a name="step-3-configure-destination"></a><span data-ttu-id="17629-184">Krok 3: Konfigurowanie docelowej</span><span class="sxs-lookup"><span data-stu-id="17629-184">Step 3: Configure destination</span></span>
<span data-ttu-id="17629-185">W tej sekcji przedstawiono sposób skonfigurowane miejsce docelowe: `lineitem` tabeli w bazie danych magazynu danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="17629-185">This section shows you how to configure the destination: `lineitem` table in the Azure SQL Data Warehouse database.</span></span>

1. <span data-ttu-id="17629-186">Wybierz **magazyn danych SQL Azure** jako miejsce docelowe przechowywania, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="17629-186">Choose **Azure SQL Data Warehouse** as the destination store and click **Next**.</span></span>

    ![Kreator kopiowania — wybierz miejsce docelowe magazynu danych](media/data-factory-load-sql-data-warehouse/select-destination-data-store.png)

2. <span data-ttu-id="17629-188">Wprowadź informacje o połączeniu dla usługi Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="17629-188">Fill in the connection information for Azure SQL Data Warehouse.</span></span>  <span data-ttu-id="17629-189">Upewnij się, że należy określić użytkownika należącego do roli `xlargerc` (zobacz **wymagania wstępne** sekcji, aby uzyskać szczegółowe instrukcje) i kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="17629-189">Make sure you specify the user that is a member of the role `xlargerc` (see the **prerequisites** section for detailed instructions), and click **Next**.</span></span>

    ![Kreator kopiowania — informacje o połączeniu docelowego](media/data-factory-load-sql-data-warehouse/destination-connection-info.png)

3. <span data-ttu-id="17629-191">Wybierz tabelę docelową, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="17629-191">Choose the destination table and click **Next**.</span></span>

    ![Kreator kopiowania — strona mapowania tabeli](media/data-factory-load-sql-data-warehouse/table-mapping-page.png)

4. <span data-ttu-id="17629-193">Na stronie mapowania schematu, nie zaznaczaj opcji "Zastosować mapowanie kolumn" wyboru i kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="17629-193">In Schema mapping page, leave "Apply column mapping" option unchecked and click **Next**.</span></span>

## <a name="step-4-performance-settings"></a><span data-ttu-id="17629-194">Krok 4: Ustawienia wydajności</span><span class="sxs-lookup"><span data-stu-id="17629-194">Step 4: Performance settings</span></span>

<span data-ttu-id="17629-195">**Zezwalaj na polybase** jest domyślnie zaznaczone.</span><span class="sxs-lookup"><span data-stu-id="17629-195">**Allow polybase** is checked by default.</span></span>  <span data-ttu-id="17629-196">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="17629-196">Click **Next**.</span></span>

![Kreator kopiowania — strona mapowanie schematu](media/data-factory-load-sql-data-warehouse/performance-settings-page.png)

## <a name="step-5-deploy-and-monitor-load-results"></a><span data-ttu-id="17629-198">Krok 5: Wdrażanie i monitorowanie wyników obciążenia</span><span class="sxs-lookup"><span data-stu-id="17629-198">Step 5: Deploy and monitor load results</span></span>
1. <span data-ttu-id="17629-199">Kliknij przycisk **Zakończ** przycisk, aby wdrożyć.</span><span class="sxs-lookup"><span data-stu-id="17629-199">Click **Finish** button to deploy.</span></span>

    ![Kreator kopiowania — strona podsumowania](media/data-factory-load-sql-data-warehouse/summary-page.png)

2. <span data-ttu-id="17629-201">Po zakończeniu wdrożenia, kliknij przycisk `Click here to monitor copy pipeline` monitorowanie kopii Uruchom postępu.</span><span class="sxs-lookup"><span data-stu-id="17629-201">After the deployment is complete, click `Click here to monitor copy pipeline` to monitor the copy run progress.</span></span> <span data-ttu-id="17629-202">Wybierz utworzony w potoku kopiowania **okien działania** listy.</span><span class="sxs-lookup"><span data-stu-id="17629-202">Select the copy pipeline you created in the **Activity Windows** list.</span></span>

    ![Kreator kopiowania — strona podsumowania](media/data-factory-load-sql-data-warehouse/select-pipeline-monitor-manage-app.png)

    <span data-ttu-id="17629-204">Możesz wyświetlić szczegóły uruchomienia kopii **działania okna Eksploratora** w prawym panelu, w tym ilość danych ze źródła do odczytu i zapisywane w docelowym, czas trwania i to średnia przepływność dla przebiegu.</span><span class="sxs-lookup"><span data-stu-id="17629-204">You can view the copy run details in the **Activity Window Explorer** in the right panel, including the data volume read from source and written into destination, duration, and the average throughput for the run.</span></span>

    <span data-ttu-id="17629-205">Jak widać na poniższym zrzucie ekranu, kopiowanie 1 TB danych z magazynu obiektów Blob Azure do usługi SQL Data Warehouse trwało 14 minut, efektywnie uzyskanie 1,22 przepływności GB/s!</span><span class="sxs-lookup"><span data-stu-id="17629-205">As you can see from the following screen shot, copying 1 TB from Azure Blob Storage into SQL Data Warehouse took 14 minutes, effectively achieving 1.22 GBps throughput!</span></span>

    ![Kreator kopiowania — okno dialogowe zakończyło się pomyślnie](media/data-factory-load-sql-data-warehouse/succeeded-info.png)

## <a name="best-practices"></a><span data-ttu-id="17629-207">Najlepsze praktyki</span><span class="sxs-lookup"><span data-stu-id="17629-207">Best practices</span></span>
<span data-ttu-id="17629-208">Poniżej przedstawiono kilka najlepszych rozwiązań dotyczących bazy danych Azure SQL Data Warehouse:</span><span class="sxs-lookup"><span data-stu-id="17629-208">Here are a few best practices for running your Azure SQL Data Warehouse database:</span></span>

* <span data-ttu-id="17629-209">Używanie większych klasy zasobu, podczas ładowania do KLASTROWANEGO INDEKSU magazynu kolumn.</span><span class="sxs-lookup"><span data-stu-id="17629-209">Use a larger resource class when loading into a CLUSTERED COLUMNSTORE INDEX.</span></span>
* <span data-ttu-id="17629-210">Dla bardziej wydajne sprzężeń należy wziąć pod uwagę przy użyciu skrótu dystrybucji przez wybierz kolumnę, zamiast domyślnej round dystrybucji działania okrężnego.</span><span class="sxs-lookup"><span data-stu-id="17629-210">For more efficient joins, consider using hash distribution by a select column instead of default round robin distribution.</span></span>
* <span data-ttu-id="17629-211">Szybsze szybkości obciążenia należy wziąć pod uwagę przy użyciu sterty przejściowej danych.</span><span class="sxs-lookup"><span data-stu-id="17629-211">For faster load speeds, consider using heap for transient data.</span></span>
* <span data-ttu-id="17629-212">Tworzenie statystyk po zakończeniu ładowania magazyn danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="17629-212">Create statistics after you finish loading Azure SQL Data Warehouse.</span></span>

<span data-ttu-id="17629-213">Zobacz [najlepsze rozwiązania dotyczące usługi Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-best-practices.md) szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="17629-213">See [Best practices for Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-best-practices.md) for details.</span></span>

## <a name="next-steps"></a><span data-ttu-id="17629-214">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="17629-214">Next steps</span></span>
* <span data-ttu-id="17629-215">[Kreator kopiowania fabryki danych](data-factory-copy-wizard.md) — ten artykuł zawiera szczegółowe informacje o kreatorze kopiowania.</span><span class="sxs-lookup"><span data-stu-id="17629-215">[Data Factory Copy Wizard](data-factory-copy-wizard.md) - This article provides details about the Copy Wizard.</span></span>
* <span data-ttu-id="17629-216">[Skopiuj wydajności działania i dostrajania przewodnik](data-factory-copy-activity-performance.md) — ten artykuł zawiera odwołanie do pomiaru wydajności i dostrajania przewodnik.</span><span class="sxs-lookup"><span data-stu-id="17629-216">[Copy Activity performance and tuning guide](data-factory-copy-activity-performance.md) - This article contains the reference performance measurements and tuning guide.</span></span>
