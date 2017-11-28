---
title: "aaaLoad terabajtów danych do usługi SQL Data Warehouse | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: e63f60461b082b0e3979004cb631dbf4a6710de3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="load-1-tb-into-azure-sql-data-warehouse-under-15-minutes-with-data-factory"></a><span data-ttu-id="20ede-103">Ładowanie 1 TB do usługi Azure SQL Data Warehouse w obszarze 15 minut przy użyciu fabryki danych</span><span class="sxs-lookup"><span data-stu-id="20ede-103">Load 1 TB into Azure SQL Data Warehouse under 15 minutes with Data Factory</span></span>
<span data-ttu-id="20ede-104">[Usługa Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md) oparte na chmurze, skalowalnych w poziomie bazy danych jest w stanie przetwarzanie bardzo dużych woluminów danych relacyjnych i nierelacyjnych.</span><span class="sxs-lookup"><span data-stu-id="20ede-104">[Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md) is a cloud-based, scale-out database capable of processing massive volumes of data, both relational and non-relational.</span></span>  <span data-ttu-id="20ede-105">Zbudowany w oparciu o architekturę masowego przetwarzania równoległego (MPP), usługa SQL Data Warehouse jest zoptymalizowana pod kątem obciążeń magazynu danych przedsiębiorstwa.</span><span class="sxs-lookup"><span data-stu-id="20ede-105">Built on massively parallel processing (MPP) architecture, SQL Data Warehouse is optimized for enterprise data warehouse workloads.</span></span>  <span data-ttu-id="20ede-106">Zapewnia elastyczność hello elastyczność tooscale magazynu w chmurze i zasobów obliczeniowych niezależnie.</span><span class="sxs-lookup"><span data-stu-id="20ede-106">It offers cloud elasticity with hello flexibility tooscale storage and compute independently.</span></span>

<span data-ttu-id="20ede-107">Wprowadzenie do korzystania z usługi Azure SQL Data Warehouse jest teraz łatwiejsze niż kiedykolwiek przy użyciu **fabryki danych Azure**.</span><span class="sxs-lookup"><span data-stu-id="20ede-107">Getting started with Azure SQL Data Warehouse is now easier than ever using **Azure Data Factory**.</span></span>  <span data-ttu-id="20ede-108">Fabryka danych Azure to usługa integracji pełni zarządzanych danych oparte na chmurze, które mogą być używane toopopulate SQL Data Warehouse hello danych z istniejącego systemu i zapisywanie cenny czas podczas oceny usługi SQL Data Warehouse i budowania sieci analityka rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="20ede-108">Azure Data Factory is a fully managed cloud-based data integration service, which can be used toopopulate a SQL Data Warehouse with hello data from your existing system, and saving you valuable time while evaluating SQL Data Warehouse and building your analytics solutions.</span></span> <span data-ttu-id="20ede-109">Poniżej przedstawiono główne zalety hello ładowania danych do usługi Azure SQL Data Warehouse przy użyciu fabryki danych Azure:</span><span class="sxs-lookup"><span data-stu-id="20ede-109">Here are hello key benefits of loading data into Azure SQL Data Warehouse using Azure Data Factory:</span></span>

* <span data-ttu-id="20ede-110">**Łatwe tooset się**: Kreator intuicyjne krok 5 z bez skryptu wymagane.</span><span class="sxs-lookup"><span data-stu-id="20ede-110">**Easy tooset up**: 5-step intuitive wizard with no scripting required.</span></span>
* <span data-ttu-id="20ede-111">**Obsługa magazynu danych sformatowanego**: wbudowaną obsługę bogaty zestaw lokalnymi i magazyny danych oparte na chmurze.</span><span class="sxs-lookup"><span data-stu-id="20ede-111">**Rich data store support**: built-in support for a rich set of on-premises and cloud-based data stores.</span></span>
* <span data-ttu-id="20ede-112">**Bezpieczne i zgodne**: dane są przesyłane za pośrednictwem protokołu HTTPS lub ExpressRoute i zapewnia obecności usługi globalne dane nigdy nie przekracza granic geograficznych hello</span><span class="sxs-lookup"><span data-stu-id="20ede-112">**Secure and compliant**: data is transferred over HTTPS or ExpressRoute, and global service presence ensures your data never leaves hello geographical boundary</span></span>
* <span data-ttu-id="20ede-113">**Bezkonkurencyjne wydajności przy użyciu programu PolyBase** — przy użyciu programu Polybase jest hello najbardziej efektywny sposób toomove danych do usługi Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="20ede-113">**Unparalleled performance by using PolyBase** – Using Polybase is hello most efficient way toomove data into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="20ede-114">Hello przemieszczania funkcji obiektów blob można osiągnąć szybkości wysokie obciążenie ze wszystkich typów magazynów danych oprócz magazynu obiektów Blob platformy Azure, które hello aparat Polybase obsługuje domyślnie.</span><span class="sxs-lookup"><span data-stu-id="20ede-114">Using hello staging blob feature, you can achieve high load speeds from all types of data stores besides Azure Blob storage, which hello Polybase supports by default.</span></span>

<span data-ttu-id="20ede-115">W tym artykule opisano sposób toouse kreatora kopiowania fabryki danych tooload 1 TB danych z magazynu obiektów Blob Azure do usługi Azure SQL Data Warehouse w obszarze 15 minut, w ponad 1,2 GB/s przepustowości.</span><span class="sxs-lookup"><span data-stu-id="20ede-115">This article shows you how toouse Data Factory Copy Wizard tooload 1-TB data from Azure Blob Storage into Azure SQL Data Warehouse in under 15 minutes, at over 1.2 GBps throughput.</span></span>

<span data-ttu-id="20ede-116">Ten artykuł zawiera instrukcje krok po kroku przenoszenie danych do usługi Azure SQL Data Warehouse przy użyciu Kreatora kopiowania hello.</span><span class="sxs-lookup"><span data-stu-id="20ede-116">This article provides step-by-step instructions for moving data into Azure SQL Data Warehouse by using hello Copy Wizard.</span></span>

> [!NOTE]
>  <span data-ttu-id="20ede-117">Aby uzyskać ogólne informacje o możliwościach fabryki danych podczas przenoszenia danych do/z usługi Azure SQL Data Warehouse, zobacz [przenieść tooand danych z usługi Azure SQL Data Warehouse przy użyciu fabryki danych Azure](data-factory-azure-sql-data-warehouse-connector.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="20ede-117">For general information about capabilities of Data Factory in moving data to/from Azure SQL Data Warehouse, see [Move data tooand from Azure SQL Data Warehouse using Azure Data Factory](data-factory-azure-sql-data-warehouse-connector.md) article.</span></span>
>
> <span data-ttu-id="20ede-118">Można również tworzyć przy użyciu portalu Azure, programu Visual Studio, programu PowerShell, potoki itp. Zobacz [samouczek: kopiowanie danych z tooAzure obiektów Blob platformy Azure SQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) Przewodnik Szybki z instrukcje krok po kroku dotyczące korzystania z hello działanie kopiowania w fabryce danych Azure.</span><span class="sxs-lookup"><span data-stu-id="20ede-118">You can also build pipelines using Azure portal, Visual Studio, PowerShell, etc. See [Tutorial: Copy data from Azure Blob tooAzure SQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for a quick walkthrough with step-by-step instructions for using hello Copy Activity in Azure Data Factory.</span></span>  
>
>

## <a name="prerequisites"></a><span data-ttu-id="20ede-119">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="20ede-119">Prerequisites</span></span>
* <span data-ttu-id="20ede-120">Azure Blob Storage: tego eksperymentu używa magazynu obiektów Blob Azure (GRS) do przechowywania TPC-H testowych w zestawie danych.</span><span class="sxs-lookup"><span data-stu-id="20ede-120">Azure Blob Storage: this experiment uses Azure Blob Storage (GRS) for storing TPC-H testing dataset.</span></span>  <span data-ttu-id="20ede-121">Dowiedz się, jeśli nie masz konta magazynu platformy Azure, [jak toocreate konta magazynu](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span><span class="sxs-lookup"><span data-stu-id="20ede-121">If you do not have an Azure storage account, learn [how toocreate a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span></span>
* <span data-ttu-id="20ede-122">[TPC-H](http://www.tpc.org/tpch/) danych: zamierzamy toouse TPC-H, jak hello zestawu danych testowych.</span><span class="sxs-lookup"><span data-stu-id="20ede-122">[TPC-H](http://www.tpc.org/tpch/) data: we are going toouse TPC-H as hello testing dataset.</span></span>  <span data-ttu-id="20ede-123">toodo, że należy toouse `dbgen` z zestawu narzędzi TPC-H, który pomaga Generowanie hello zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="20ede-123">toodo that, you need toouse `dbgen` from TPC-H toolkit, which helps you generate hello dataset.</span></span>  <span data-ttu-id="20ede-124">Albo można pobrać kodu źródłowego dla `dbgen` z [narzędzia TPC](http://www.tpc.org/tpc_documents_current_versions/current_specifications.asp) i skompiluj go samodzielnie lub danych binarnych skompilowanych hello pobierania z [GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/TPCHTools).</span><span class="sxs-lookup"><span data-stu-id="20ede-124">You can either download source code for `dbgen` from [TPC Tools](http://www.tpc.org/tpc_documents_current_versions/current_specifications.asp) and compile it yourself, or download hello compiled binary from [GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/TPCHTools).</span></span>  <span data-ttu-id="20ede-125">Uruchom dbgen.exe hello następujące polecenia toogenerate pliku prostego 1 TB dla `lineitem` tabeli rozpowszechniania przez 10 plików:</span><span class="sxs-lookup"><span data-stu-id="20ede-125">Run dbgen.exe with hello following commands toogenerate 1 TB flat file for `lineitem` table spread across 10 files:</span></span>

  * `Dbgen -s 1000 -S **1** -C 10 -T L -v`
  * `Dbgen -s 1000 -S **2** -C 10 -T L -v`
  * <span data-ttu-id="20ede-126">…</span><span class="sxs-lookup"><span data-stu-id="20ede-126">…</span></span>
  * `Dbgen -s 1000 -S **10** -C 10 -T L -v`

    <span data-ttu-id="20ede-127">Teraz hello kopii wygenerowanych plików tooAzure obiektów Blob.</span><span class="sxs-lookup"><span data-stu-id="20ede-127">Now copy hello generated files tooAzure Blob.</span></span>  <span data-ttu-id="20ede-128">Odwołuje się zbyt[przenieść tooand danych z lokalnego systemu plików przy użyciu fabryki danych Azure](data-factory-onprem-file-system-connector.md) jak toodo który przy użyciu kopii ADF.</span><span class="sxs-lookup"><span data-stu-id="20ede-128">Refer too[Move data tooand from an on-premises file system by using Azure Data Factory](data-factory-onprem-file-system-connector.md) for how toodo that using ADF Copy.</span></span>    
* <span data-ttu-id="20ede-129">Usługa Azure SQL Data Warehouse: tego eksperymentu ładuje dane do magazynu danych SQL Azure utworzonych za pomocą dwu 6000</span><span class="sxs-lookup"><span data-stu-id="20ede-129">Azure SQL Data Warehouse: this experiment loads data into Azure SQL Data Warehouse created with 6,000 DWUs</span></span>

    <span data-ttu-id="20ede-130">Odwołuje się zbyt[Utwórz magazyn danych SQL Azure](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md) szczegółowe informacje dotyczące sposobu toocreate SQL Data Warehouse bazy danych.</span><span class="sxs-lookup"><span data-stu-id="20ede-130">Refer too[Create an Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md) for detailed instructions on how toocreate a SQL Data Warehouse database.</span></span>  <span data-ttu-id="20ede-131">tooget hello najlepsze możliwe obciążenie wydajności do usługi SQL Data Warehouse przy użyciu programu Polybase, możemy wybierz maksymalną liczbę jednostek magazynu danych (dwu) dozwolone w ustawieniu wydajności hello, czyli 6000 jednostek dwu.</span><span class="sxs-lookup"><span data-stu-id="20ede-131">tooget hello best possible load performance into SQL Data Warehouse using Polybase, we choose maximum number of Data Warehouse Units (DWUs) allowed in hello Performance setting, which is 6,000 DWUs.</span></span>

  > [!NOTE]
  > <span data-ttu-id="20ede-132">Podczas ładowania z obiektów Blob platformy Azure, ładowanie wydajności danych hello jest wprost proporcjonalny toohello liczby jednostek dwu Skonfiguruj na powitania SQL Data Warehouse:</span><span class="sxs-lookup"><span data-stu-id="20ede-132">When loading from Azure Blob, hello data loading performance is directly proportional toohello number of DWUs you configure on hello SQL Data Warehouse:</span></span>
  >
  > <span data-ttu-id="20ede-133">Ładowanie 1 TB do 1000 DWU usługa SQL Data Warehouse uwzględnia 87 minut (przepływność ~ 200 MB/s) podczas ładowania 1 TB 2000 DWU usługa SQL Data Warehouse przyjmuje 46 minut (przepływność ~ 380 MB/s) podczas ładowania 1 TB w 6000 DWU usługa SQL Data Warehouse trwa 14 minut (przepływność ~1.2 GB/s)</span><span class="sxs-lookup"><span data-stu-id="20ede-133">Loading 1 TB into 1,000 DWU SQL Data Warehouse takes 87 minutes (~200 MBps throughput) Loading 1 TB into 2,000 DWU SQL Data Warehouse takes 46 minutes (~380 MBps throughput) Loading 1 TB into 6,000 DWU SQL Data Warehouse takes 14 minutes (~1.2 GBps throughput)</span></span>
  >
  >

    <span data-ttu-id="20ede-134">toocreate SQL Data Warehouse z dwu 6000, przesuń suwak wydajności hello wszystkich toohello sposób powitania po prawej:</span><span class="sxs-lookup"><span data-stu-id="20ede-134">toocreate a SQL Data Warehouse with 6,000 DWUs, move hello Performance slider all hello way toohello right:</span></span>

    ![Suwak wydajności](media/data-factory-load-sql-data-warehouse/performance-slider.png)

    <span data-ttu-id="20ede-136">Dla istniejącej bazy danych nie jest skonfigurowany z dwu 6000 można go skalować przy użyciu portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="20ede-136">For an existing database that is not configured with 6,000 DWUs, you can scale it up using Azure portal.</span></span>  <span data-ttu-id="20ede-137">Przejdź toohello bazy danych, w portalu Azure, a nie **skali** przycisku na powitania **omówienie** panelu pokazano powitania po obrazu:</span><span class="sxs-lookup"><span data-stu-id="20ede-137">Navigate toohello database in Azure portal, and there is a **Scale** button in hello **Overview** panel shown in hello following image:</span></span>

    ![Przycisk skali](media/data-factory-load-sql-data-warehouse/scale-button.png)    

    <span data-ttu-id="20ede-139">Kliknij przycisk hello **skali** następujące hello tooopen przycisk panelu, przesuń suwak hello toohello maksymalną wartość i kliknij **Zapisz** przycisku.</span><span class="sxs-lookup"><span data-stu-id="20ede-139">Click hello **Scale** button tooopen hello following panel, move hello slider toohello maximum value, and click **Save** button.</span></span>

    ![Okno dialogowe skalowania](media/data-factory-load-sql-data-warehouse/scale-dialog.png)

    <span data-ttu-id="20ede-141">Tego eksperymentu ładuje dane do usługi Azure SQL Data Warehouse przy użyciu `xlargerc` klasy zasobów.</span><span class="sxs-lookup"><span data-stu-id="20ede-141">This experiment loads data into Azure SQL Data Warehouse using `xlargerc` resource class.</span></span>

    <span data-ttu-id="20ede-142">tooachieve najlepsze możliwe przepływności, kopii musi toobe wykonywane przy użyciu użytkownika usługi SQL Data Warehouse należącego zbyt`xlargerc` klasy zasobów.</span><span class="sxs-lookup"><span data-stu-id="20ede-142">tooachieve best possible throughput, copy needs toobe performed using a SQL Data Warehouse user belonging too`xlargerc` resource class.</span></span>  <span data-ttu-id="20ede-143">Dowiedz się, jak toodo który wykonując [zmienić przykład klasy zasobów użytkownika](../sql-data-warehouse/sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).</span><span class="sxs-lookup"><span data-stu-id="20ede-143">Learn how toodo that by following [Change a user resource class example](../sql-data-warehouse/sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).</span></span>  
* <span data-ttu-id="20ede-144">Tworzenie schematu tabeli docelowej w bazie danych Azure SQL Data Warehouse, uruchamiając powitania po instrukcji DDL:</span><span class="sxs-lookup"><span data-stu-id="20ede-144">Create destination table schema in Azure SQL Data Warehouse database, by running hello following DDL statement:</span></span>

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
<span data-ttu-id="20ede-145">Dzięki wstępnie wymagane kroki hello ukończone mamy teraz działanie kopiowania hello tooconfigure gotowe za pomocą Kreatora kopiowania hello.</span><span class="sxs-lookup"><span data-stu-id="20ede-145">With hello prerequisite steps completed, we are now ready tooconfigure hello copy activity using hello Copy Wizard.</span></span>

## <a name="launch-copy-wizard"></a><span data-ttu-id="20ede-146">Uruchamianie Kreatora kopiowania</span><span class="sxs-lookup"><span data-stu-id="20ede-146">Launch Copy Wizard</span></span>
1. <span data-ttu-id="20ede-147">Zaloguj się za toohello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="20ede-147">Log in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="20ede-148">Kliknij przycisk **+ nowy** hello lewym górnym rogu kliknij **analizy i analiza**i kliknij przycisk **fabryki danych**.</span><span class="sxs-lookup"><span data-stu-id="20ede-148">Click **+ NEW** from hello top-left corner, click **Intelligence + analytics**, and click **Data Factory**.</span></span>
3. <span data-ttu-id="20ede-149">W hello **nowa fabryka danych** bloku:</span><span class="sxs-lookup"><span data-stu-id="20ede-149">In hello **New data factory** blade:</span></span>

   1. <span data-ttu-id="20ede-150">Wprowadź **LoadIntoSQLDWDataFactory** dla hello **nazwa**.</span><span class="sxs-lookup"><span data-stu-id="20ede-150">Enter **LoadIntoSQLDWDataFactory** for hello **name**.</span></span>
       <span data-ttu-id="20ede-151">Nazwa fabryki danych Azure hello Hello musi być globalnie unikatowe.</span><span class="sxs-lookup"><span data-stu-id="20ede-151">hello name of hello Azure data factory must be globally unique.</span></span> <span data-ttu-id="20ede-152">Jeśli wystąpi błąd hello: **nazwa fabryki danych "LoadIntoSQLDWDataFactory" nie jest dostępna**, Zmień nazwę hello hello fabryki danych (na przykład yournameLoadIntoSQLDWDataFactory) i spróbuj ponownie utworzyć.</span><span class="sxs-lookup"><span data-stu-id="20ede-152">If you receive hello error: **Data factory name “LoadIntoSQLDWDataFactory” is not available**, change hello name of hello data factory (for example, yournameLoadIntoSQLDWDataFactory) and try creating again.</span></span> <span data-ttu-id="20ede-153">Artykuł [Data Factory — Naming Rules](data-factory-naming-rules.md) (Fabryka danych — zasady nazewnictwa) zawiera zasady nazewnictwa artefaktów usługi Fabryka danych.</span><span class="sxs-lookup"><span data-stu-id="20ede-153">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>  
   2. <span data-ttu-id="20ede-154">Wybierz swoją **subskrypcję** platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="20ede-154">Select your Azure **subscription**.</span></span>
   3. <span data-ttu-id="20ede-155">Dla grupy zasobów wykonaj jedną z hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="20ede-155">For Resource Group, do one of hello following steps:</span></span>
      1. <span data-ttu-id="20ede-156">Wybierz **Użyj istniejącego** tooselect istniejącą grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="20ede-156">Select **Use existing** tooselect an existing resource group.</span></span>
      2. <span data-ttu-id="20ede-157">Wybierz **Utwórz nowy** tooenter nazwę grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="20ede-157">Select **Create new** tooenter a name for a resource group.</span></span>
   4. <span data-ttu-id="20ede-158">Wybierz **lokalizacji** hello fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="20ede-158">Select a **location** for hello data factory.</span></span>
   5. <span data-ttu-id="20ede-159">Wybierz **toodashboard numeru Pin** pole wyboru u dołu hello hello bloku.</span><span class="sxs-lookup"><span data-stu-id="20ede-159">Select **Pin toodashboard** check box at hello bottom of hello blade.</span></span>  
   6. <span data-ttu-id="20ede-160">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="20ede-160">Click **Create**.</span></span>
4. <span data-ttu-id="20ede-161">Po zakończeniu tworzenia hello Zobacz hello **fabryki danych** bloku, jak pokazano w powitania po obrazu:</span><span class="sxs-lookup"><span data-stu-id="20ede-161">After hello creation is complete, you see hello **Data Factory** blade as shown in hello following image:</span></span>

   ![Strona główna fabryki danych](media/data-factory-load-sql-data-warehouse/data-factory-home-page-copy-data.png)
5. <span data-ttu-id="20ede-163">Na stronie głównej fabryki danych powitania kliknij hello **skopiować dane** Kafelek toolaunch **kreatora kopiowania**.</span><span class="sxs-lookup"><span data-stu-id="20ede-163">On hello Data Factory home page, click hello **Copy data** tile toolaunch **Copy Wizard**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="20ede-164">Jeśli widzisz tej przeglądarki sieci web hello jest zablokowany na "Autoryzowanie...", wyłącz/Usuń zaznaczenie pola wyboru **zablokować pliki cookie innych firm, a dane lokacji** ustawienie (lub) schowaj włączone i utworzyć wyjątek **login.microsoftonline.com**, a następnie spróbuj ponownie uruchomić Kreatora hello.</span><span class="sxs-lookup"><span data-stu-id="20ede-164">If you see that hello web browser is stuck at "Authorizing...", disable/uncheck **Block third party cookies and site data** setting (or) keep it enabled and create an exception for **login.microsoftonline.com** and then try launching hello wizard again.</span></span>
   >
   >

## <a name="step-1-configure-data-loading-schedule"></a><span data-ttu-id="20ede-165">Krok 1: Skonfiguruj harmonogram ładowanie danych</span><span class="sxs-lookup"><span data-stu-id="20ede-165">Step 1: Configure data loading schedule</span></span>
<span data-ttu-id="20ede-166">pierwszym krokiem Hello są dane hello tooconfigure ładowania harmonogramu.</span><span class="sxs-lookup"><span data-stu-id="20ede-166">hello first step is tooconfigure hello data loading schedule.</span></span>  

<span data-ttu-id="20ede-167">W hello **właściwości** strony:</span><span class="sxs-lookup"><span data-stu-id="20ede-167">In hello **Properties** page:</span></span>

1. <span data-ttu-id="20ede-168">Wprowadź **CopyFromBlobToAzureSqlDataWarehouse** dla **Nazwa zadania**</span><span class="sxs-lookup"><span data-stu-id="20ede-168">Enter **CopyFromBlobToAzureSqlDataWarehouse** for **Task name**</span></span>
2. <span data-ttu-id="20ede-169">Wybierz **uruchom raz teraz** opcji.</span><span class="sxs-lookup"><span data-stu-id="20ede-169">Select **Run once now** option.</span></span>   
3. <span data-ttu-id="20ede-170">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="20ede-170">Click **Next**.</span></span>  

    ![Kreator kopiowania — strona właściwości](media/data-factory-load-sql-data-warehouse/copy-wizard-properties-page.png)

## <a name="step-2-configure-source"></a><span data-ttu-id="20ede-172">Krok 2: Konfigurowanie źródła</span><span class="sxs-lookup"><span data-stu-id="20ede-172">Step 2: Configure source</span></span>
<span data-ttu-id="20ede-173">Ten przedstawia sekcji hello kroki tooconfigure hello źródła: obiektów Blob platformy Azure zawierającą hello TPC 1 TB-H pozycji plików.</span><span class="sxs-lookup"><span data-stu-id="20ede-173">This section shows you hello steps tooconfigure hello source: Azure Blob containing hello 1-TB TPC-H line item files.</span></span>

1. <span data-ttu-id="20ede-174">Wybierz hello **magazyn obiektów Blob Azure** danych hello przechowywania, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="20ede-174">Select hello **Azure Blob Storage** as hello data store and click **Next**.</span></span>

    ![Kreator kopiowania — wybierz źródło strony](media/data-factory-load-sql-data-warehouse/select-source-connection.png)

2. <span data-ttu-id="20ede-176">Wypełnij hello informacje o połączeniu dla hello konta magazynu obiektów Blob platformy Azure, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="20ede-176">Fill in hello connection information for hello Azure Blob storage account, and click **Next**.</span></span>

    ![Kreator kopiowania — informacje o źródle połączenia](media/data-factory-load-sql-data-warehouse/source-connection-info.png)

3. <span data-ttu-id="20ede-178">Wybierz hello **folderu** hello TPC-H wiersza zawierającego element plików, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="20ede-178">Choose hello **folder** containing hello TPC-H line item files and click **Next**.</span></span>

    ![Kreator kopiowania — wybierz folder wejściowy](media/data-factory-load-sql-data-warehouse/select-input-folder.png)

4. <span data-ttu-id="20ede-180">Po kliknięciu **dalej**, ustawienia formatu pliku hello są wykrywane automatycznie.</span><span class="sxs-lookup"><span data-stu-id="20ede-180">Upon clicking **Next**, hello file format settings are detected automatically.</span></span>  <span data-ttu-id="20ede-181">Sprawdź toomake się, że jest ogranicznik tej kolumny ' | 'zamiast przecinkami domyślne hello",".</span><span class="sxs-lookup"><span data-stu-id="20ede-181">Check toomake sure that column delimiter is ‘|’ instead of hello default comma ‘,’.</span></span>  <span data-ttu-id="20ede-182">Kliknij przycisk **dalej** po przejrzeniu hello danych.</span><span class="sxs-lookup"><span data-stu-id="20ede-182">Click **Next** after you have previewed hello data.</span></span>

    ![Kreator kopiowania — ustawienia format pliku](media/data-factory-load-sql-data-warehouse/file-format-settings.png)

## <a name="step-3-configure-destination"></a><span data-ttu-id="20ede-184">Krok 3: Konfigurowanie docelowej</span><span class="sxs-lookup"><span data-stu-id="20ede-184">Step 3: Configure destination</span></span>
<span data-ttu-id="20ede-185">W tej sekcji przedstawiono, jak tooconfigure hello docelowego: `lineitem` tabeli w bazie danych Azure SQL Data Warehouse hello.</span><span class="sxs-lookup"><span data-stu-id="20ede-185">This section shows you how tooconfigure hello destination: `lineitem` table in hello Azure SQL Data Warehouse database.</span></span>

1. <span data-ttu-id="20ede-186">Wybierz **magazyn danych SQL Azure** jako miejsce docelowe hello przechowywania, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="20ede-186">Choose **Azure SQL Data Warehouse** as hello destination store and click **Next**.</span></span>

    ![Kreator kopiowania — wybierz miejsce docelowe magazynu danych](media/data-factory-load-sql-data-warehouse/select-destination-data-store.png)

2. <span data-ttu-id="20ede-188">Wypełnij hello informacje o połączeniu dla usługi Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="20ede-188">Fill in hello connection information for Azure SQL Data Warehouse.</span></span>  <span data-ttu-id="20ede-189">Upewnij się, że Określ hello użytkownika, który jest członkiem roli hello `xlargerc` (zobacz hello **wymagania wstępne** sekcji, aby uzyskać szczegółowe instrukcje) i kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="20ede-189">Make sure you specify hello user that is a member of hello role `xlargerc` (see hello **prerequisites** section for detailed instructions), and click **Next**.</span></span>

    ![Kreator kopiowania — informacje o połączeniu docelowego](media/data-factory-load-sql-data-warehouse/destination-connection-info.png)

3. <span data-ttu-id="20ede-191">Wybierz tabelę docelową hello i kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="20ede-191">Choose hello destination table and click **Next**.</span></span>

    ![Kreator kopiowania — strona mapowania tabeli](media/data-factory-load-sql-data-warehouse/table-mapping-page.png)

4. <span data-ttu-id="20ede-193">Na stronie mapowania schematu, nie zaznaczaj opcji "Zastosować mapowanie kolumn" wyboru i kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="20ede-193">In Schema mapping page, leave "Apply column mapping" option unchecked and click **Next**.</span></span>

## <a name="step-4-performance-settings"></a><span data-ttu-id="20ede-194">Krok 4: Ustawienia wydajności</span><span class="sxs-lookup"><span data-stu-id="20ede-194">Step 4: Performance settings</span></span>

<span data-ttu-id="20ede-195">**Zezwalaj na polybase** jest domyślnie zaznaczone.</span><span class="sxs-lookup"><span data-stu-id="20ede-195">**Allow polybase** is checked by default.</span></span>  <span data-ttu-id="20ede-196">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="20ede-196">Click **Next**.</span></span>

![Kreator kopiowania — strona mapowanie schematu](media/data-factory-load-sql-data-warehouse/performance-settings-page.png)

## <a name="step-5-deploy-and-monitor-load-results"></a><span data-ttu-id="20ede-198">Krok 5: Wdrażanie i monitorowanie wyników obciążenia</span><span class="sxs-lookup"><span data-stu-id="20ede-198">Step 5: Deploy and monitor load results</span></span>
1. <span data-ttu-id="20ede-199">Kliknij przycisk **Zakończ** toodeploy przycisku.</span><span class="sxs-lookup"><span data-stu-id="20ede-199">Click **Finish** button toodeploy.</span></span>

    ![Kreator kopiowania — strona podsumowania](media/data-factory-load-sql-data-warehouse/summary-page.png)

2. <span data-ttu-id="20ede-201">Po zakończeniu wdrażania powitania kliknij `Click here toomonitor copy pipeline` kopiowania hello toomonitor Uruchom postępu.</span><span class="sxs-lookup"><span data-stu-id="20ede-201">After hello deployment is complete, click `Click here toomonitor copy pipeline` toomonitor hello copy run progress.</span></span> <span data-ttu-id="20ede-202">Potok kopiowania hello wybierz utworzony w hello **okien działania** listy.</span><span class="sxs-lookup"><span data-stu-id="20ede-202">Select hello copy pipeline you created in hello **Activity Windows** list.</span></span>

    ![Kreator kopiowania — strona podsumowania](media/data-factory-load-sql-data-warehouse/select-pipeline-monitor-manage-app.png)

    <span data-ttu-id="20ede-204">Możesz wyświetlić szczegóły uruchomienia w hello kopiowania hello **działania okna Eksploratora** hello prawym panelu, w tym ilość danych hello odczytywane źródła i zapisywane na docelowy, czas trwania i średniej przepływności hello hello Uruchom.</span><span class="sxs-lookup"><span data-stu-id="20ede-204">You can view hello copy run details in hello **Activity Window Explorer** in hello right panel, including hello data volume read from source and written into destination, duration, and hello average throughput for hello run.</span></span>

    <span data-ttu-id="20ede-205">Jak widać na powitania po zrzut ekranu, kopiowanie 1 TB danych z magazynu obiektów Blob Azure do usługi SQL Data Warehouse trwało 14 minut, efektywnie uzyskanie 1,22 przepływności GB/s!</span><span class="sxs-lookup"><span data-stu-id="20ede-205">As you can see from hello following screen shot, copying 1 TB from Azure Blob Storage into SQL Data Warehouse took 14 minutes, effectively achieving 1.22 GBps throughput!</span></span>

    ![Kreator kopiowania — okno dialogowe zakończyło się pomyślnie](media/data-factory-load-sql-data-warehouse/succeeded-info.png)

## <a name="best-practices"></a><span data-ttu-id="20ede-207">Najlepsze praktyki</span><span class="sxs-lookup"><span data-stu-id="20ede-207">Best practices</span></span>
<span data-ttu-id="20ede-208">Poniżej przedstawiono kilka najlepszych rozwiązań dotyczących bazy danych Azure SQL Data Warehouse:</span><span class="sxs-lookup"><span data-stu-id="20ede-208">Here are a few best practices for running your Azure SQL Data Warehouse database:</span></span>

* <span data-ttu-id="20ede-209">Używanie większych klasy zasobu, podczas ładowania do KLASTROWANEGO INDEKSU magazynu kolumn.</span><span class="sxs-lookup"><span data-stu-id="20ede-209">Use a larger resource class when loading into a CLUSTERED COLUMNSTORE INDEX.</span></span>
* <span data-ttu-id="20ede-210">Dla bardziej wydajne sprzężeń należy wziąć pod uwagę przy użyciu skrótu dystrybucji przez wybierz kolumnę, zamiast domyślnej round dystrybucji działania okrężnego.</span><span class="sxs-lookup"><span data-stu-id="20ede-210">For more efficient joins, consider using hash distribution by a select column instead of default round robin distribution.</span></span>
* <span data-ttu-id="20ede-211">Szybsze szybkości obciążenia należy wziąć pod uwagę przy użyciu sterty przejściowej danych.</span><span class="sxs-lookup"><span data-stu-id="20ede-211">For faster load speeds, consider using heap for transient data.</span></span>
* <span data-ttu-id="20ede-212">Tworzenie statystyk po zakończeniu ładowania magazyn danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="20ede-212">Create statistics after you finish loading Azure SQL Data Warehouse.</span></span>

<span data-ttu-id="20ede-213">Zobacz [najlepsze rozwiązania dotyczące usługi Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-best-practices.md) szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="20ede-213">See [Best practices for Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-best-practices.md) for details.</span></span>

## <a name="next-steps"></a><span data-ttu-id="20ede-214">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="20ede-214">Next steps</span></span>
* <span data-ttu-id="20ede-215">[Kreator kopiowania fabryki danych](data-factory-copy-wizard.md) — w tym artykule przedstawiono szczegóły hello kreatora kopiowania.</span><span class="sxs-lookup"><span data-stu-id="20ede-215">[Data Factory Copy Wizard](data-factory-copy-wizard.md) - This article provides details about hello Copy Wizard.</span></span>
* <span data-ttu-id="20ede-216">[Skopiuj wydajności działania i dostrajania przewodnik](data-factory-copy-activity-performance.md) — ten artykuł zawiera hello pomiarów wydajności i dostrajania przewodnik.</span><span class="sxs-lookup"><span data-stu-id="20ede-216">[Copy Activity performance and tuning guide](data-factory-copy-activity-performance.md) - This article contains hello reference performance measurements and tuning guide.</span></span>
