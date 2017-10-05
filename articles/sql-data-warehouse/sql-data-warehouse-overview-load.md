---
title: "Ładowanie danych do usługi Azure SQL Data Warehouse | Dokumentacja firmy Microsoft"
description: "Dowiedz się typowe scenariusze dotyczące danych ładowania do usługi SQL Data Warehouse. Obejmują one przy użyciu programu PolyBase, magazynu obiektów blob platformy Azure, plików prostych i wysyłania dysku. Można także użyć narzędzi innych firm."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
ms.assetid: 2253bf46-cf72-4de7-85ce-f267494d55fa
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: c4199a387f5cdbd477a5e348e48ba8e8b5900075
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="load-data-into-azure-sql-data-warehouse"></a><span data-ttu-id="731e4-105">Ładowanie danych do usługi Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="731e4-105">Load data into Azure SQL Data Warehouse</span></span>
<span data-ttu-id="731e4-106">Podsumowanie opcji scenariusza i zalecenia dotyczące ładowania danych do usługi SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="731e4-106">A summary of the scenario options and recommendations for loading data into SQL Data Warehouse.</span></span>

<span data-ttu-id="731e4-107">Najtrudniejsze część podczas ładowania danych jest zwykle Przygotowanie danych obciążenia.</span><span class="sxs-lookup"><span data-stu-id="731e4-107">The hardest part of loading data is usually preparing the data for the load.</span></span> <span data-ttu-id="731e4-108">Ładowanie upraszcza Azure przy użyciu magazynu obiektów blob platformy Azure jako magazynu danych wspólne dla wielu usług i fabryki danych Azure do organizowania przepływu danych i komunikacji między usługami Azure.</span><span class="sxs-lookup"><span data-stu-id="731e4-108">Azure simplifies loading by using Azure blob storage as a common data store for many of the services, and using Azure Data Factory to orchestrate communication and data movement between the Azure services.</span></span> <span data-ttu-id="731e4-109">Te procesy są zintegrowane z technologii PolyBase, który używa masowego przetwarzania równoległego (MPP) do ładowania danych równolegle z magazynu obiektów blob platformy Azure do usługi SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="731e4-109">These processes are integrated with PolyBase technology which uses massively parallel processing (MPP) to load data in parallel from Azure blob storage into SQL Data Warehouse.</span></span> 

<span data-ttu-id="731e4-110">Samouczki, które ładują przykładowe bazy danych, zobacz [załadować przykładowe bazy danych][Load sample databases].</span><span class="sxs-lookup"><span data-stu-id="731e4-110">For tutorials that load sample databases, see [Load sample databases][Load sample databases].</span></span>

## <a name="load-from-azure-blob-storage"></a><span data-ttu-id="731e4-111">Ładowanie z magazynu obiektów blob platformy Azure</span><span class="sxs-lookup"><span data-stu-id="731e4-111">Load from Azure blob storage</span></span>
<span data-ttu-id="731e4-112">Jest to najszybszy sposób importowania danych do usługi SQL Data Warehouse ładowanie danych z magazynu obiektów blob platformy Azure przy użyciu programu PolyBase.</span><span class="sxs-lookup"><span data-stu-id="731e4-112">The fastest way to import data into SQL Data Warehouse is to use PolyBase to load data from Azure blob storage.</span></span> <span data-ttu-id="731e4-113">Program PolyBase używa projektu masowego przetwarzania równoległego (MPP) magazynu danych SQL do ładowania danych równolegle z magazynu obiektów blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="731e4-113">PolyBase uses SQL Data Warehouse's massively parallel processing (MPP) design to load data in parallel from Azure blob storage.</span></span> <span data-ttu-id="731e4-114">Aby użyć programu PolyBase, można użyć polecenia T-SQL lub potoku fabryki danych Azure.</span><span class="sxs-lookup"><span data-stu-id="731e4-114">To use PolyBase, you can use T-SQL commands or an Azure Data Factory pipeline.</span></span>

### <a name="1-use-polybase-and-t-sql"></a><span data-ttu-id="731e4-115">1. Użyj programu PolyBase i T-SQL</span><span class="sxs-lookup"><span data-stu-id="731e4-115">1. Use PolyBase and T-SQL</span></span>
<span data-ttu-id="731e4-116">Podsumowanie procesu ładowania:</span><span class="sxs-lookup"><span data-stu-id="731e4-116">Summary of loading process:</span></span>

1. <span data-ttu-id="731e4-117">Przenoszenie danych do magazynu obiektów blob platformy Azure lub usługi Azure Data Lake Store i zapisze go w plikach tekstowych.</span><span class="sxs-lookup"><span data-stu-id="731e4-117">Move your data to Azure blob storage or Azure Data Lake Store and store it in text files.</span></span>
2. <span data-ttu-id="731e4-118">Skonfiguruj obiekty zewnętrzne w magazynie danych SQL, aby określić lokalizację i format danych</span><span class="sxs-lookup"><span data-stu-id="731e4-118">Configure external objects in SQL Data Warehouse to define the location and format of the data</span></span>
3. <span data-ttu-id="731e4-119">Uruchom polecenie T-SQL, aby załadować dane jednocześnie do nowej tabeli bazy danych.</span><span class="sxs-lookup"><span data-stu-id="731e4-119">Run a T-SQL command to load the data in parallel into a new database table.</span></span>

<!-- 5. Schedule and run a loading job. --> 

<span data-ttu-id="731e4-120">Samouczek, zobacz [ładowanie danych z magazynu obiektów blob platformy Azure SQL Data Warehouse (PolyBase)][Load data from Azure blob storage to SQL Data Warehouse (PolyBase)].</span><span class="sxs-lookup"><span data-stu-id="731e4-120">For a tutorial, see [Load data from Azure blob storage to SQL Data Warehouse (PolyBase)][Load data from Azure blob storage to SQL Data Warehouse (PolyBase)].</span></span>

### <a name="2-use-azure-data-factory"></a><span data-ttu-id="731e4-121">2. Używanie usługi Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="731e4-121">2. Use Azure Data Factory</span></span>
<span data-ttu-id="731e4-122">W prostszy sposób Użyj programu PolyBase można utworzyć potok fabryki danych Azure, który używa programu PolyBase do ładowania danych z magazynu obiektów blob platformy Azure do usługi SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="731e4-122">For a simpler way to use PolyBase, you can create an Azure Data Factory pipeline that uses PolyBase to load data from Azure blob storage into SQL Data Warehouse.</span></span> <span data-ttu-id="731e4-123">Jest to szybkie do skonfigurowania, ponieważ nie ma potrzeby definiowania obiektów T-SQL.</span><span class="sxs-lookup"><span data-stu-id="731e4-123">This is fast to configure since you don't need to define the T-SQL objects.</span></span> <span data-ttu-id="731e4-124">Jeśli potrzebujesz kwerendy danych zewnętrznych nie jest importowany, użyj T-SQL.</span><span class="sxs-lookup"><span data-stu-id="731e4-124">If you need to query the external data without importing it, use T-SQL.</span></span> 

<span data-ttu-id="731e4-125">Podsumowanie procesu ładowania:</span><span class="sxs-lookup"><span data-stu-id="731e4-125">Summary of loading process:</span></span>

1. <span data-ttu-id="731e4-126">Przenoszenie danych do magazynu obiektów blob platformy Azure i zapisze go w plikach tekstowych.</span><span class="sxs-lookup"><span data-stu-id="731e4-126">Move your data to Azure blob storage and store it in text files.</span></span> <span data-ttu-id="731e4-127">Fabryka danych Azure nie obsługuje obecnie łączności ADLS przy użyciu programu PolyBase).</span><span class="sxs-lookup"><span data-stu-id="731e4-127">Azure Data Factory does not currently support ADLS connectivity with PolyBase).</span></span>
2. <span data-ttu-id="731e4-128">Utworzyć potok fabryki danych Azure pozyskiwanie danych.</span><span class="sxs-lookup"><span data-stu-id="731e4-128">Create an Azure Data Factory pipeline to ingest the data.</span></span> <span data-ttu-id="731e4-129">Opcja PolyBase.</span><span class="sxs-lookup"><span data-stu-id="731e4-129">Use the PolyBase option.</span></span>
4. <span data-ttu-id="731e4-130">Planowanie i uruchamianie potoku.</span><span class="sxs-lookup"><span data-stu-id="731e4-130">Schedule and run the pipeline.</span></span>

<span data-ttu-id="731e4-131">Samouczek, zobacz [ładowanie danych z magazynu obiektów blob platformy Azure SQL Data Warehouse (fabryka danych Azure)][Load data from Azure blob storage to SQL Data Warehouse (Azure Data Factory)].</span><span class="sxs-lookup"><span data-stu-id="731e4-131">For a tutorial, see [Load data from Azure blob storage to SQL Data Warehouse (Azure Data Factory)][Load data from Azure blob storage to SQL Data Warehouse (Azure Data Factory)].</span></span>

## <a name="load-from-sql-server"></a><span data-ttu-id="731e4-132">Ładowanie z programu SQL Server</span><span class="sxs-lookup"><span data-stu-id="731e4-132">Load from SQL Server</span></span>
<span data-ttu-id="731e4-133">Aby załadować dane z programu SQL Server do usługi SQL Data Warehouse można użyć Integration Services (SSIS), transfer plików prostych lub dysków dostawy do firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="731e4-133">To load data from SQL Server to SQL Data Warehouse you can use Integration Services (SSIS), transfer flat files, or ship disks to Microsoft.</span></span> <span data-ttu-id="731e4-134">Odczyt do zawiera podsumowanie różnic ładowania procesy i łącza do samouczki.</span><span class="sxs-lookup"><span data-stu-id="731e4-134">Read on to see a summary of the different loading processes and links to tutorials.</span></span>

<span data-ttu-id="731e4-135">Aby zaplanować migracji danych z programu SQL Server do usługi SQL Data Warehouse, zobacz [Omówienie migracji][Migration overview].</span><span class="sxs-lookup"><span data-stu-id="731e4-135">To plan a full data migration from SQL Server to SQL Data Warehouse, see the [Migration overview][Migration overview].</span></span> 

### <a name="use-integration-services-ssis"></a><span data-ttu-id="731e4-136">Użyj usług Integration Services (SSIS)</span><span class="sxs-lookup"><span data-stu-id="731e4-136">Use Integration Services (SSIS)</span></span>
<span data-ttu-id="731e4-137">Jeśli korzystasz już z pakietów Integration Services (SSIS) do załadowania do serwera SQL Server, należy zaktualizować pakiety używać programu SQL Server jako źródła i magazynu danych SQL jako miejsca docelowego.</span><span class="sxs-lookup"><span data-stu-id="731e4-137">If you are already using Integration Services (SSIS) packages to load into SQL Server, you can update your packages to use SQL Server as the source and SQL Data Warehouse as the destination.</span></span> <span data-ttu-id="731e4-138">Jest to szybki i łatwy w celu i jest dobrym rozwiązaniem, jeśli nie chcesz migrować procesu ładowania, aby użyć danych już w chmurze.</span><span class="sxs-lookup"><span data-stu-id="731e4-138">This is quick and easy to do, and is a good choice if you are not trying to migrate your loading process to use data already in the cloud.</span></span> <span data-ttu-id="731e4-139">Zależności to obciążenie będzie przebiegać wolniej niż przy użyciu programu PolyBase, ponieważ ta SSIS nie przeprowadza obciążenia równolegle.</span><span class="sxs-lookup"><span data-stu-id="731e4-139">The tradeoff is the load will be slower than using PolyBase because this SSIS does not perform the load in parallel.</span></span>

<span data-ttu-id="731e4-140">Podsumowanie procesu ładowania:</span><span class="sxs-lookup"><span data-stu-id="731e4-140">Summary of loading process:</span></span>

1. <span data-ttu-id="731e4-141">Sprawdź, czy pakietu usług Integration Services, aby wskazywała wystąpienie serwera SQL dla źródła i bazy danych magazynu danych SQL dla miejsca docelowego.</span><span class="sxs-lookup"><span data-stu-id="731e4-141">Revise your Integration Services package to point to the SQL Server instance for the source and the SQL Data Warehouse database for the destination.</span></span>
2. <span data-ttu-id="731e4-142">Migrację schematu SQL Data Warehouse, jeśli nie jest już.</span><span class="sxs-lookup"><span data-stu-id="731e4-142">Migrate your schema to SQL Data Warehouse, if it is not there already.</span></span>
3. <span data-ttu-id="731e4-143">Zmień mapowanie w pakietach Użyj tylko typy danych, które są obsługiwane przez usługi SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="731e4-143">Change the mapping in your packages use only the data types that are supported by SQL Data Warehouse.</span></span>
4. <span data-ttu-id="731e4-144">Planowanie i uruchamianie pakietu.</span><span class="sxs-lookup"><span data-stu-id="731e4-144">Schedule and run the package.</span></span>

<span data-ttu-id="731e4-145">Samouczek, zobacz [ładowanie danych z programu SQL Server do magazynu danych SQL Azure (SSIS)][Load data from SQL Server to Azure SQL Data Warehouse (SSIS)].</span><span class="sxs-lookup"><span data-stu-id="731e4-145">For a tutorial, see [Load data from SQL Server to Azure SQL Data Warehouse (SSIS)][Load data from SQL Server to Azure SQL Data Warehouse (SSIS)].</span></span>

### <a name="use-azcopy-recommended-for--10-tb-data"></a><span data-ttu-id="731e4-146">Przy użyciu programu AZCopy (zalecane dla < 10 TB danych)</span><span class="sxs-lookup"><span data-stu-id="731e4-146">Use AZCopy (recommended for < 10 TB data)</span></span>
<span data-ttu-id="731e4-147">Jeśli rozmiar danych jest < 10 TB, można wyeksportować dane z programu SQL Server do plików prostych, skopiuj pliki do magazynu obiektów blob platformy Azure i następnie użyj programu PolyBase, aby załadować dane do magazynu danych SQL</span><span class="sxs-lookup"><span data-stu-id="731e4-147">If your data size is < 10 TB, you can export the data from SQL Server to flat files, copy the files to Azure blob storage, and then use PolyBase to load the data into SQL Data Warehouse</span></span>

<span data-ttu-id="731e4-148">Podsumowanie procesu ładowania:</span><span class="sxs-lookup"><span data-stu-id="731e4-148">Summary of loading process:</span></span>

1. <span data-ttu-id="731e4-149">Użyj narzędzia wiersza polecenia bcp do eksportowania danych z programu SQL Server do plików prostych.</span><span class="sxs-lookup"><span data-stu-id="731e4-149">Use the bcp command-line utility to export data from SQL Server to flat files.</span></span>
2. <span data-ttu-id="731e4-150">Użyj narzędzia wiersza polecenia AZCopy do kopiowania danych z plików prostych do magazynu obiektów blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="731e4-150">Use the AZCopy command-line utility to copy data from flat files to Azure blob storage.</span></span>
3. <span data-ttu-id="731e4-151">Użyj programu PolyBase, aby załadować do usługi SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="731e4-151">Use PolyBase to load into SQL Data Warehouse.</span></span>

<span data-ttu-id="731e4-152">Samouczek, zobacz [ładowanie danych z magazynu obiektów blob platformy Azure SQL Data Warehouse (PolyBase)][Load data from Azure blob storage to SQL Data Warehouse (PolyBase)].</span><span class="sxs-lookup"><span data-stu-id="731e4-152">For a tutorial, see [Load data from Azure blob storage to SQL Data Warehouse (PolyBase)][Load data from Azure blob storage to SQL Data Warehouse (PolyBase)].</span></span>

### <a name="use-bcp"></a><span data-ttu-id="731e4-153">Użyj narzędzia bcp</span><span class="sxs-lookup"><span data-stu-id="731e4-153">Use bcp</span></span>
<span data-ttu-id="731e4-154">Jeśli masz niewielką ilość danych można użyć bcp, aby załadować bezpośrednio do usługi Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="731e4-154">If you have a small amount of data you can use bcp to load directly into Azure SQL Data Warehouse.</span></span>

<span data-ttu-id="731e4-155">Podsumowanie procesu ładowania:</span><span class="sxs-lookup"><span data-stu-id="731e4-155">Summary of loading process:</span></span>

1. <span data-ttu-id="731e4-156">Użyj narzędzia wiersza polecenia bcp do eksportowania danych z programu SQL Server do plików prostych.</span><span class="sxs-lookup"><span data-stu-id="731e4-156">Use the bcp command-line utility to export data from SQL Server to flat files.</span></span>
2. <span data-ttu-id="731e4-157">Użyj narzędzia bcp do ładowania danych z plików prostych bezpośrednio do usługi SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="731e4-157">Use bcp to load data from flat files directly to SQL Data Warehouse.</span></span>

<span data-ttu-id="731e4-158">Samouczek, zobacz [ładowania danych z programu SQL Server do usługi Azure SQL Data Warehouse (bcp)][Load data from SQL Server to Azure SQL Data Warehouse (bcp)].</span><span class="sxs-lookup"><span data-stu-id="731e4-158">For a tutorial, see [Load data from SQL Server to Azure SQL Data Warehouse (bcp)][Load data from SQL Server to Azure SQL Data Warehouse (bcp)].</span></span>

### <a name="use-importexport-recommended-for--10-tb-data"></a><span data-ttu-id="731e4-159">Użyj importu/eksportu (zalecane dla > 10 TB danych)</span><span class="sxs-lookup"><span data-stu-id="731e4-159">Use Import/Export (recommended for > 10 TB data)</span></span>
<span data-ttu-id="731e4-160">Jeśli rozmiar danych jest > 10 TB i chcesz przenieść ją do platformy Azure, zalecane jest użycie naszych dysku wysyłania usługi [importu/eksportu][Import/Export].</span><span class="sxs-lookup"><span data-stu-id="731e4-160">If your data size is > 10 TB and you want to move it to Azure, we recommend that you use our disk shipping service [Import/Export][Import/Export].</span></span> 

<span data-ttu-id="731e4-161">Podsumowanie procesu ładowania</span><span class="sxs-lookup"><span data-stu-id="731e4-161">Summary of loading process</span></span>

1. <span data-ttu-id="731e4-162">Użyj narzędzia wiersza polecenia bcp do eksportowania danych z programu SQL Server do plików prostych możliwej dysków.</span><span class="sxs-lookup"><span data-stu-id="731e4-162">Use the bcp command-line utility to export data from SQL Server to flat files on transferrable disks.</span></span>
2. <span data-ttu-id="731e4-163">Należy najpierw wydać dysków do firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="731e4-163">Ship the disks to Microsoft.</span></span>
3. <span data-ttu-id="731e4-164">Microsoft ładuje dane do magazynu danych SQL</span><span class="sxs-lookup"><span data-stu-id="731e4-164">Microsoft loads the data into SQL Data Warehouse</span></span>

## <a name="load-from-hdinsight"></a><span data-ttu-id="731e4-165">Ładowanie z usługi HDInsight</span><span class="sxs-lookup"><span data-stu-id="731e4-165">Load from HDInsight</span></span>
<span data-ttu-id="731e4-166">Magazyn danych SQL obsługuje ładowanie danych z usługi HDInsight przy użyciu programu PolyBase.</span><span class="sxs-lookup"><span data-stu-id="731e4-166">SQL Data Warehouse supports loading data from HDInsight via PolyBase.</span></span> <span data-ttu-id="731e4-167">Proces jest taki sam, jak podczas ładowania danych z magazynu obiektów Blob platformy Azure — przy użyciu programu PolyBase do nawiązania połączenia usługi HDInsight można załadować danych.</span><span class="sxs-lookup"><span data-stu-id="731e4-167">The process is the same as loading data from Azure Blob Storage - using PolyBase to connect to HDInsight to load data.</span></span> 

### <a name="1-use-polybase-and-t-sql"></a><span data-ttu-id="731e4-168">1. Użyj programu PolyBase i T-SQL</span><span class="sxs-lookup"><span data-stu-id="731e4-168">1. Use PolyBase and T-SQL</span></span>
<span data-ttu-id="731e4-169">Podsumowanie procesu ładowania:</span><span class="sxs-lookup"><span data-stu-id="731e4-169">Summary of loading process:</span></span>

1. <span data-ttu-id="731e4-170">Przenoszenie danych do usługi HDInsight i zapisze go w plikach tekstowych ORC lub Parquet format.</span><span class="sxs-lookup"><span data-stu-id="731e4-170">Move your data to HDInsight and store it in text files, ORC or Parquet format.</span></span>
2. <span data-ttu-id="731e4-171">Skonfiguruj obiekty zewnętrzne w magazynie danych SQL, aby określić lokalizację i format danych.</span><span class="sxs-lookup"><span data-stu-id="731e4-171">Configure external objects in SQL Data Warehouse to define the location and format of the data.</span></span>
3. <span data-ttu-id="731e4-172">Uruchom polecenie T-SQL, aby załadować dane jednocześnie do nowej tabeli bazy danych.</span><span class="sxs-lookup"><span data-stu-id="731e4-172">Run a T-SQL command to load the data in parallel into a new database table.</span></span>

<span data-ttu-id="731e4-173">Samouczek, zobacz [ładowanie danych z magazynu obiektów blob platformy Azure SQL Data Warehouse (PolyBase)][Load data from Azure blob storage to SQL Data Warehouse (PolyBase)].</span><span class="sxs-lookup"><span data-stu-id="731e4-173">For a tutorial, see [Load data from Azure blob storage to SQL Data Warehouse (PolyBase)][Load data from Azure blob storage to SQL Data Warehouse (PolyBase)].</span></span>

## <a name="recommendations"></a><span data-ttu-id="731e4-174">Zalecenia</span><span class="sxs-lookup"><span data-stu-id="731e4-174">Recommendations</span></span>
<span data-ttu-id="731e4-175">Wiele naszych partnerów ma ładowania rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="731e4-175">Many of our partners have loading solutions.</span></span> <span data-ttu-id="731e4-176">Aby dowiedzieć się więcej, zobacz listę naszych [rozwiązania partnerów][solution partners].</span><span class="sxs-lookup"><span data-stu-id="731e4-176">To find out more, see a list of our [solution partners][solution partners].</span></span> 

<span data-ttu-id="731e4-177">Dane pochodzące ze źródłem danych nierelacyjnych i chcesz załadować go do magazynu danych SQL należy przekształcić w wiersze i kolumny, przed rozpoczęciem ładowania.</span><span class="sxs-lookup"><span data-stu-id="731e4-177">If your data is coming from a non-relational source and you want to load it into SQL Data Warehouse you will need to transform it into rows and columns before you load it.</span></span> <span data-ttu-id="731e4-178">Przekształcone dane nie mają być przechowywane w bazie danych, mogą być przechowywane w plikach tekstowych.</span><span class="sxs-lookup"><span data-stu-id="731e4-178">The transformed data doesn't need to be stored in a database, it can be stored in text files.</span></span>

<span data-ttu-id="731e4-179">Tworzenie statystyk na nowo załadowanych danych.</span><span class="sxs-lookup"><span data-stu-id="731e4-179">Create statistics on newly loaded data.</span></span> <span data-ttu-id="731e4-180">Usługa Azure SQL Data Warehouse nie obsługuje jeszcze automatycznego tworzenia ani aktualizowania statystyk.</span><span class="sxs-lookup"><span data-stu-id="731e4-180">Azure SQL Data Warehouse does not yet support auto create or auto update statistics.</span></span>  <span data-ttu-id="731e4-181">Aby uzyskać najlepszą wydajność zapytań, ważne jest, aby utworzyć statystyki dla wszystkich kolumn wszystkich tabel po pierwszym załadowaniu lub występują znaczne zmiany w danych.</span><span class="sxs-lookup"><span data-stu-id="731e4-181">In order to get the best performance from your queries, it's important to create statistics on all columns of all tables after the first load or any substantial changes occur in the data.</span></span>  <span data-ttu-id="731e4-182">Aby uzyskać więcej informacji, zobacz [statystyki][Statistics].</span><span class="sxs-lookup"><span data-stu-id="731e4-182">For details, see [Statistics][Statistics].</span></span>

## <a name="next-steps"></a><span data-ttu-id="731e4-183">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="731e4-183">Next steps</span></span>
<span data-ttu-id="731e4-184">Aby uzyskać więcej porad programistycznych, zobacz [omówienie tworzenia][development overview].</span><span class="sxs-lookup"><span data-stu-id="731e4-184">For more development tips, see the [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[Load data from Azure blob storage to SQL Data Warehouse (PolyBase)]: ./sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md
[Load data from Azure blob storage to SQL Data Warehouse (Azure Data Factory)]: ./sql-data-warehouse-load-from-azure-blob-storage-with-data-factory.md
[Load data from SQL Server to Azure SQL Data Warehouse (SSIS)]: ./sql-data-warehouse-load-from-sql-server-with-integration-services.md
[Load data from SQL Server to Azure SQL Data Warehouse (bcp)]: ./sql-data-warehouse-load-from-sql-server-with-bcp.md
[Load data from SQL Server to Azure SQL Data Warehouse (AZCopy)]: ./sql-data-warehouse-load-from-sql-server-with-azcopy.md

[Load sample databases]: ./sql-data-warehouse-load-sample-databases.md
[Migration overview]: ./sql-data-warehouse-overview-migrate.md
[solution partners]: ./sql-data-warehouse-partner-business-intelligence.md
[development overview]: ./sql-data-warehouse-overview-develop.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md

<!--MSDN references-->

<!--Other Web references-->
[Import/Export]: https://azure.microsoft.com/documentation/articles/storage-import-export-service/
