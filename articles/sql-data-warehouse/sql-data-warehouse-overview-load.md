---
title: "aaaLoad danych do usługi Azure SQL Data Warehouse | Dokumentacja firmy Microsoft"
description: "Dowiedz się hello typowe scenariusze dotyczące danych ładowania do usługi SQL Data Warehouse. Obejmują one przy użyciu programu PolyBase, magazynu obiektów blob platformy Azure, plików prostych i wysyłania dysku. Można także użyć narzędzi innych firm."
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
ms.openlocfilehash: d1a5063f484e9bd95f854e27a4baed512148aad0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-into-azure-sql-data-warehouse"></a><span data-ttu-id="d8d81-105">Ładowanie danych do usługi Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="d8d81-105">Load data into Azure SQL Data Warehouse</span></span>
<span data-ttu-id="d8d81-106">Podsumowanie opcji scenariusz hello i zalecenia dotyczące ładowania danych do usługi SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="d8d81-106">A summary of hello scenario options and recommendations for loading data into SQL Data Warehouse.</span></span>

<span data-ttu-id="d8d81-107">Najtrudniejsze części Hello podczas ładowania danych jest zwykle przygotowywania danych hello hello obciążenia.</span><span class="sxs-lookup"><span data-stu-id="d8d81-107">hello hardest part of loading data is usually preparing hello data for hello load.</span></span> <span data-ttu-id="d8d81-108">Azure upraszcza ładowania przy użyciu magazynu obiektów blob platformy Azure jako magazynu danych wspólne dla wielu usług hello i przy użyciu fabryki danych Azure hello tooorchestrate przepływu danych i komunikacji między usługami Azure.</span><span class="sxs-lookup"><span data-stu-id="d8d81-108">Azure simplifies loading by using Azure blob storage as a common data store for many of hello services, and using Azure Data Factory tooorchestrate communication and data movement between hello Azure services.</span></span> <span data-ttu-id="d8d81-109">Te procesy są zintegrowane z technologii PolyBase, która korzysta z ogromną skalę równoległe przetwarzanie danych tooload (MPP) równolegle z magazynu obiektów blob platformy Azure do usługi SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="d8d81-109">These processes are integrated with PolyBase technology which uses massively parallel processing (MPP) tooload data in parallel from Azure blob storage into SQL Data Warehouse.</span></span> 

<span data-ttu-id="d8d81-110">Samouczki, które ładują przykładowe bazy danych, zobacz [załadować przykładowe bazy danych][Load sample databases].</span><span class="sxs-lookup"><span data-stu-id="d8d81-110">For tutorials that load sample databases, see [Load sample databases][Load sample databases].</span></span>

## <a name="load-from-azure-blob-storage"></a><span data-ttu-id="d8d81-111">Ładowanie z magazynu obiektów blob platformy Azure</span><span class="sxs-lookup"><span data-stu-id="d8d81-111">Load from Azure blob storage</span></span>
<span data-ttu-id="d8d81-112">Witaj najszybszy sposób tooimport danych do usługi SQL Data Warehouse jest toouse PolyBase tooload danych z magazynu obiektów blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d8d81-112">hello fastest way tooimport data into SQL Data Warehouse is toouse PolyBase tooload data from Azure blob storage.</span></span> <span data-ttu-id="d8d81-113">PolyBase używa usługi SQL Data Warehouse na ogromną skalę równoległe przetwarzania (MPP) projektu tooload danych równolegle z magazynu obiektów blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d8d81-113">PolyBase uses SQL Data Warehouse's massively parallel processing (MPP) design tooload data in parallel from Azure blob storage.</span></span> <span data-ttu-id="d8d81-114">toouse PolyBase, można użyć polecenia T-SQL lub potoku fabryki danych Azure.</span><span class="sxs-lookup"><span data-stu-id="d8d81-114">toouse PolyBase, you can use T-SQL commands or an Azure Data Factory pipeline.</span></span>

### <a name="1-use-polybase-and-t-sql"></a><span data-ttu-id="d8d81-115">1. Użyj programu PolyBase i T-SQL</span><span class="sxs-lookup"><span data-stu-id="d8d81-115">1. Use PolyBase and T-SQL</span></span>
<span data-ttu-id="d8d81-116">Podsumowanie procesu ładowania:</span><span class="sxs-lookup"><span data-stu-id="d8d81-116">Summary of loading process:</span></span>

1. <span data-ttu-id="d8d81-117">Przeniesienie magazynu obiektów blob tooAzure danych lub w usłudze Azure Data Lake Store i zapisze go w plikach tekstowych.</span><span class="sxs-lookup"><span data-stu-id="d8d81-117">Move your data tooAzure blob storage or Azure Data Lake Store and store it in text files.</span></span>
2. <span data-ttu-id="d8d81-118">Skonfiguruj obiekty zewnętrznego w lokalizacji hello toodefine SQL Data Warehouse i format danych hello</span><span class="sxs-lookup"><span data-stu-id="d8d81-118">Configure external objects in SQL Data Warehouse toodefine hello location and format of hello data</span></span>
3. <span data-ttu-id="d8d81-119">Równolegle danych hello tooload polecenia T-SQL do nowej tabeli bazy danych.</span><span class="sxs-lookup"><span data-stu-id="d8d81-119">Run a T-SQL command tooload hello data in parallel into a new database table.</span></span>

<!-- 5. Schedule and run a loading job. --> 

<span data-ttu-id="d8d81-120">Samouczek, zobacz [ładowanie danych z magazynu obiektów blob platformy Azure — tooSQL Data Warehouse (PolyBase)][Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)].</span><span class="sxs-lookup"><span data-stu-id="d8d81-120">For a tutorial, see [Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)][Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)].</span></span>

### <a name="2-use-azure-data-factory"></a><span data-ttu-id="d8d81-121">2. Używanie usługi Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="d8d81-121">2. Use Azure Data Factory</span></span>
<span data-ttu-id="d8d81-122">Dla prostszy sposób toouse PolyBase można utworzyć potok fabryki danych Azure, który używa danych tooload PolyBase z magazynu obiektów blob platformy Azure do usługi SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="d8d81-122">For a simpler way toouse PolyBase, you can create an Azure Data Factory pipeline that uses PolyBase tooload data from Azure blob storage into SQL Data Warehouse.</span></span> <span data-ttu-id="d8d81-123">Jest to szybkie tooconfigure, ponieważ nie ma potrzeby toodefine hello T-SQL obiektów.</span><span class="sxs-lookup"><span data-stu-id="d8d81-123">This is fast tooconfigure since you don't need toodefine hello T-SQL objects.</span></span> <span data-ttu-id="d8d81-124">Jeśli potrzebujesz danych zewnętrznych hello tooquery nie jest importowany, użyj T-SQL.</span><span class="sxs-lookup"><span data-stu-id="d8d81-124">If you need tooquery hello external data without importing it, use T-SQL.</span></span> 

<span data-ttu-id="d8d81-125">Podsumowanie procesu ładowania:</span><span class="sxs-lookup"><span data-stu-id="d8d81-125">Summary of loading process:</span></span>

1. <span data-ttu-id="d8d81-126">Przenieś usługi magazynu obiektów blob tooAzure danych i zapisze go w plikach tekstowych.</span><span class="sxs-lookup"><span data-stu-id="d8d81-126">Move your data tooAzure blob storage and store it in text files.</span></span> <span data-ttu-id="d8d81-127">Fabryka danych Azure nie obsługuje obecnie łączności ADLS przy użyciu programu PolyBase).</span><span class="sxs-lookup"><span data-stu-id="d8d81-127">Azure Data Factory does not currently support ADLS connectivity with PolyBase).</span></span>
2. <span data-ttu-id="d8d81-128">Tworzenie fabryki danych Azure potoku tooingest hello danych.</span><span class="sxs-lookup"><span data-stu-id="d8d81-128">Create an Azure Data Factory pipeline tooingest hello data.</span></span> <span data-ttu-id="d8d81-129">Opcja hello PolyBase.</span><span class="sxs-lookup"><span data-stu-id="d8d81-129">Use hello PolyBase option.</span></span>
4. <span data-ttu-id="d8d81-130">Planowanie i uruchamianie potoku hello.</span><span class="sxs-lookup"><span data-stu-id="d8d81-130">Schedule and run hello pipeline.</span></span>

<span data-ttu-id="d8d81-131">Samouczek, zobacz [ładowanie danych z magazynu obiektów blob platformy Azure — tooSQL Data Warehouse (fabryka danych Azure)][Load data from Azure blob storage tooSQL Data Warehouse (Azure Data Factory)].</span><span class="sxs-lookup"><span data-stu-id="d8d81-131">For a tutorial, see [Load data from Azure blob storage tooSQL Data Warehouse (Azure Data Factory)][Load data from Azure blob storage tooSQL Data Warehouse (Azure Data Factory)].</span></span>

## <a name="load-from-sql-server"></a><span data-ttu-id="d8d81-132">Ładowanie z programu SQL Server</span><span class="sxs-lookup"><span data-stu-id="d8d81-132">Load from SQL Server</span></span>
<span data-ttu-id="d8d81-133">dane tooload z tooSQL programu SQL Server Integration Services (SSIS), można użyć magazynu danych transferu plików prostych lub wysłać tooMicrosoft dysków.</span><span class="sxs-lookup"><span data-stu-id="d8d81-133">tooload data from SQL Server tooSQL Data Warehouse you can use Integration Services (SSIS), transfer flat files, or ship disks tooMicrosoft.</span></span> <span data-ttu-id="d8d81-134">Poniżej toosee podsumowanie hello różnych ładowania tootutorials procesy i łącza.</span><span class="sxs-lookup"><span data-stu-id="d8d81-134">Read on toosee a summary of hello different loading processes and links tootutorials.</span></span>

<span data-ttu-id="d8d81-135">tooplan migracji danych z programu SQL Server tooSQL hurtowni danych, zobacz hello [Omówienie migracji][Migration overview].</span><span class="sxs-lookup"><span data-stu-id="d8d81-135">tooplan a full data migration from SQL Server tooSQL Data Warehouse, see hello [Migration overview][Migration overview].</span></span> 

### <a name="use-integration-services-ssis"></a><span data-ttu-id="d8d81-136">Użyj usług Integration Services (SSIS)</span><span class="sxs-lookup"><span data-stu-id="d8d81-136">Use Integration Services (SSIS)</span></span>
<span data-ttu-id="d8d81-137">Jeśli korzystasz już z tooload pakietów Integration Services (SSIS) do programu SQL Server, należy zaktualizować toouse Twojego pakiety programu SQL Server jako hello źródła i magazynu danych SQL jako miejsce docelowe hello.</span><span class="sxs-lookup"><span data-stu-id="d8d81-137">If you are already using Integration Services (SSIS) packages tooload into SQL Server, you can update your packages toouse SQL Server as hello source and SQL Data Warehouse as hello destination.</span></span> <span data-ttu-id="d8d81-138">Jest to szybki i łatwy toodo i jest dobrym rozwiązaniem, jeśli nie chcesz toomigrate Twojego ładowania przetwarzania danych toouse już w chmurze hello.</span><span class="sxs-lookup"><span data-stu-id="d8d81-138">This is quick and easy toodo, and is a good choice if you are not trying toomigrate your loading process toouse data already in hello cloud.</span></span> <span data-ttu-id="d8d81-139">zależnościami Hello jest obciążenia hello będzie przebiegać wolniej niż przy użyciu programu PolyBase, ponieważ ta SSIS nie przeprowadza obciążenia hello równolegle.</span><span class="sxs-lookup"><span data-stu-id="d8d81-139">hello tradeoff is hello load will be slower than using PolyBase because this SSIS does not perform hello load in parallel.</span></span>

<span data-ttu-id="d8d81-140">Podsumowanie procesu ładowania:</span><span class="sxs-lookup"><span data-stu-id="d8d81-140">Summary of loading process:</span></span>

1. <span data-ttu-id="d8d81-141">Popraw wystąpienia programu SQL Server Integration Services pakietu toopoint toohello hello źródła i bazy danych magazynu danych SQL hello hello docelowym.</span><span class="sxs-lookup"><span data-stu-id="d8d81-141">Revise your Integration Services package toopoint toohello SQL Server instance for hello source and hello SQL Data Warehouse database for hello destination.</span></span>
2. <span data-ttu-id="d8d81-142">Migrowanie tooSQL Twojego schematu magazynu danych, jeśli nie jest już.</span><span class="sxs-lookup"><span data-stu-id="d8d81-142">Migrate your schema tooSQL Data Warehouse, if it is not there already.</span></span>
3. <span data-ttu-id="d8d81-143">Zmień mapowanie hello w pakietach Użyj tylko typy danych hello, które są obsługiwane przez usługi SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="d8d81-143">Change hello mapping in your packages use only hello data types that are supported by SQL Data Warehouse.</span></span>
4. <span data-ttu-id="d8d81-144">Planowanie i uruchamianie hello pakietu.</span><span class="sxs-lookup"><span data-stu-id="d8d81-144">Schedule and run hello package.</span></span>

<span data-ttu-id="d8d81-145">Samouczek, zobacz [ładowanie danych z programu SQL Server tooAzure magazynu danych SQL (SSIS)][Load data from SQL Server tooAzure SQL Data Warehouse (SSIS)].</span><span class="sxs-lookup"><span data-stu-id="d8d81-145">For a tutorial, see [Load data from SQL Server tooAzure SQL Data Warehouse (SSIS)][Load data from SQL Server tooAzure SQL Data Warehouse (SSIS)].</span></span>

### <a name="use-azcopy-recommended-for--10-tb-data"></a><span data-ttu-id="d8d81-146">Przy użyciu programu AZCopy (zalecane dla < 10 TB danych)</span><span class="sxs-lookup"><span data-stu-id="d8d81-146">Use AZCopy (recommended for < 10 TB data)</span></span>
<span data-ttu-id="d8d81-147">Jeśli rozmiar danych jest < 10 TB, można eksportować dane hello z pliki tooflat programu SQL Server, kopiowanie magazynu obiektów blob tooAzure pliki hello i następnie użyj programu PolyBase tooload hello danych do usługi SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="d8d81-147">If your data size is < 10 TB, you can export hello data from SQL Server tooflat files, copy hello files tooAzure blob storage, and then use PolyBase tooload hello data into SQL Data Warehouse</span></span>

<span data-ttu-id="d8d81-148">Podsumowanie procesu ładowania:</span><span class="sxs-lookup"><span data-stu-id="d8d81-148">Summary of loading process:</span></span>

1. <span data-ttu-id="d8d81-149">Za pomocą danych tooexport narzędzia wiersza polecenia bcp hello plików tooflat programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="d8d81-149">Use hello bcp command-line utility tooexport data from SQL Server tooflat files.</span></span>
2. <span data-ttu-id="d8d81-150">Użyj hello AZCopy narzędzia wiersza polecenia toocopy danych z magazynu obiektów blob tooAzure plików prostych.</span><span class="sxs-lookup"><span data-stu-id="d8d81-150">Use hello AZCopy command-line utility toocopy data from flat files tooAzure blob storage.</span></span>
3. <span data-ttu-id="d8d81-151">Użyj programu PolyBase tooload do usługi SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="d8d81-151">Use PolyBase tooload into SQL Data Warehouse.</span></span>

<span data-ttu-id="d8d81-152">Samouczek, zobacz [ładowanie danych z magazynu obiektów blob platformy Azure — tooSQL Data Warehouse (PolyBase)][Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)].</span><span class="sxs-lookup"><span data-stu-id="d8d81-152">For a tutorial, see [Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)][Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)].</span></span>

### <a name="use-bcp"></a><span data-ttu-id="d8d81-153">Użyj narzędzia bcp</span><span class="sxs-lookup"><span data-stu-id="d8d81-153">Use bcp</span></span>
<span data-ttu-id="d8d81-154">Jeśli masz niewielką ilość danych można użyć narzędzia bcp tooload bezpośrednio do usługi Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="d8d81-154">If you have a small amount of data you can use bcp tooload directly into Azure SQL Data Warehouse.</span></span>

<span data-ttu-id="d8d81-155">Podsumowanie procesu ładowania:</span><span class="sxs-lookup"><span data-stu-id="d8d81-155">Summary of loading process:</span></span>

1. <span data-ttu-id="d8d81-156">Za pomocą danych tooexport narzędzia wiersza polecenia bcp hello plików tooflat programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="d8d81-156">Use hello bcp command-line utility tooexport data from SQL Server tooflat files.</span></span>
2. <span data-ttu-id="d8d81-157">Użyj narzędzia bcp tooload danych z płaski plików bezpośrednio tooSQL hurtowni danych.</span><span class="sxs-lookup"><span data-stu-id="d8d81-157">Use bcp tooload data from flat files directly tooSQL Data Warehouse.</span></span>

<span data-ttu-id="d8d81-158">Samouczek, zobacz [ładowanie danych z programu SQL Server tooAzure SQL Data Warehouse (bcp)][Load data from SQL Server tooAzure SQL Data Warehouse (bcp)].</span><span class="sxs-lookup"><span data-stu-id="d8d81-158">For a tutorial, see [Load data from SQL Server tooAzure SQL Data Warehouse (bcp)][Load data from SQL Server tooAzure SQL Data Warehouse (bcp)].</span></span>

### <a name="use-importexport-recommended-for--10-tb-data"></a><span data-ttu-id="d8d81-159">Użyj importu/eksportu (zalecane dla > 10 TB danych)</span><span class="sxs-lookup"><span data-stu-id="d8d81-159">Use Import/Export (recommended for > 10 TB data)</span></span>
<span data-ttu-id="d8d81-160">Jeśli rozmiar danych jest > 10 TB, toomove go tooAzure, firma Microsoft zaleca użycie naszych dysku wysyłania usługi [importu/eksportu][Import/Export].</span><span class="sxs-lookup"><span data-stu-id="d8d81-160">If your data size is > 10 TB and you want toomove it tooAzure, we recommend that you use our disk shipping service [Import/Export][Import/Export].</span></span> 

<span data-ttu-id="d8d81-161">Podsumowanie procesu ładowania</span><span class="sxs-lookup"><span data-stu-id="d8d81-161">Summary of loading process</span></span>

1. <span data-ttu-id="d8d81-162">Za pomocą danych tooexport narzędzia wiersza polecenia bcp hello plików tooflat programu SQL Server na dyskach możliwej.</span><span class="sxs-lookup"><span data-stu-id="d8d81-162">Use hello bcp command-line utility tooexport data from SQL Server tooflat files on transferrable disks.</span></span>
2. <span data-ttu-id="d8d81-163">Należy najpierw wydać hello tooMicrosoft dysków.</span><span class="sxs-lookup"><span data-stu-id="d8d81-163">Ship hello disks tooMicrosoft.</span></span>
3. <span data-ttu-id="d8d81-164">Microsoft ładuje hello dane do magazynu danych SQL</span><span class="sxs-lookup"><span data-stu-id="d8d81-164">Microsoft loads hello data into SQL Data Warehouse</span></span>

## <a name="load-from-hdinsight"></a><span data-ttu-id="d8d81-165">Ładowanie z usługi HDInsight</span><span class="sxs-lookup"><span data-stu-id="d8d81-165">Load from HDInsight</span></span>
<span data-ttu-id="d8d81-166">Magazyn danych SQL obsługuje ładowanie danych z usługi HDInsight przy użyciu programu PolyBase.</span><span class="sxs-lookup"><span data-stu-id="d8d81-166">SQL Data Warehouse supports loading data from HDInsight via PolyBase.</span></span> <span data-ttu-id="d8d81-167">proces Hello jest hello taki sam jak podczas ładowania danych z magazynu obiektów Blob Azure - przy użyciu programu PolyBase tooconnect tooHDInsight tooload danych.</span><span class="sxs-lookup"><span data-stu-id="d8d81-167">hello process is hello same as loading data from Azure Blob Storage - using PolyBase tooconnect tooHDInsight tooload data.</span></span> 

### <a name="1-use-polybase-and-t-sql"></a><span data-ttu-id="d8d81-168">1. Użyj programu PolyBase i T-SQL</span><span class="sxs-lookup"><span data-stu-id="d8d81-168">1. Use PolyBase and T-SQL</span></span>
<span data-ttu-id="d8d81-169">Podsumowanie procesu ładowania:</span><span class="sxs-lookup"><span data-stu-id="d8d81-169">Summary of loading process:</span></span>

1. <span data-ttu-id="d8d81-170">Przenieś tooHDInsight Twoje dane i zapisze go w plikach tekstowych ORC lub Parquet format.</span><span class="sxs-lookup"><span data-stu-id="d8d81-170">Move your data tooHDInsight and store it in text files, ORC or Parquet format.</span></span>
2. <span data-ttu-id="d8d81-171">Skonfiguruj obiekty zewnętrznego w lokalizacji hello toodefine SQL Data Warehouse i format danych hello.</span><span class="sxs-lookup"><span data-stu-id="d8d81-171">Configure external objects in SQL Data Warehouse toodefine hello location and format of hello data.</span></span>
3. <span data-ttu-id="d8d81-172">Równolegle danych hello tooload polecenia T-SQL do nowej tabeli bazy danych.</span><span class="sxs-lookup"><span data-stu-id="d8d81-172">Run a T-SQL command tooload hello data in parallel into a new database table.</span></span>

<span data-ttu-id="d8d81-173">Samouczek, zobacz [ładowanie danych z magazynu obiektów blob platformy Azure — tooSQL Data Warehouse (PolyBase)][Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)].</span><span class="sxs-lookup"><span data-stu-id="d8d81-173">For a tutorial, see [Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)][Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)].</span></span>

## <a name="recommendations"></a><span data-ttu-id="d8d81-174">Zalecenia</span><span class="sxs-lookup"><span data-stu-id="d8d81-174">Recommendations</span></span>
<span data-ttu-id="d8d81-175">Wiele naszych partnerów ma ładowania rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="d8d81-175">Many of our partners have loading solutions.</span></span> <span data-ttu-id="d8d81-176">toofind się więcej, zobacz listę naszych [rozwiązania partnerów][solution partners].</span><span class="sxs-lookup"><span data-stu-id="d8d81-176">toofind out more, see a list of our [solution partners][solution partners].</span></span> 

<span data-ttu-id="d8d81-177">Jeśli dane pochodzące ze źródłem danych nierelacyjnych i tooload go do danych SQL można magazynu należy tootransform go do wierszy i kolumn przed rozpoczęciem ładowania.</span><span class="sxs-lookup"><span data-stu-id="d8d81-177">If your data is coming from a non-relational source and you want tooload it into SQL Data Warehouse you will need tootransform it into rows and columns before you load it.</span></span> <span data-ttu-id="d8d81-178">Witaj przekształcone dane nie wymaga toobe przechowywane w bazie danych, mogą być przechowywane w plikach tekstowych.</span><span class="sxs-lookup"><span data-stu-id="d8d81-178">hello transformed data doesn't need toobe stored in a database, it can be stored in text files.</span></span>

<span data-ttu-id="d8d81-179">Tworzenie statystyk na nowo załadowanych danych.</span><span class="sxs-lookup"><span data-stu-id="d8d81-179">Create statistics on newly loaded data.</span></span> <span data-ttu-id="d8d81-180">Usługa Azure SQL Data Warehouse nie obsługuje jeszcze automatycznego tworzenia ani aktualizowania statystyk.</span><span class="sxs-lookup"><span data-stu-id="d8d81-180">Azure SQL Data Warehouse does not yet support auto create or auto update statistics.</span></span>  <span data-ttu-id="d8d81-181">W kolejności tooget hello najlepszą wydajność zapytań należy najpierw załadować toocreate statystyki dla wszystkich kolumn wszystkich tabel po hello lub każdej istotnej zmianie występują w danych hello.</span><span class="sxs-lookup"><span data-stu-id="d8d81-181">In order tooget hello best performance from your queries, it's important toocreate statistics on all columns of all tables after hello first load or any substantial changes occur in hello data.</span></span>  <span data-ttu-id="d8d81-182">Aby uzyskać więcej informacji, zobacz [statystyki][Statistics].</span><span class="sxs-lookup"><span data-stu-id="d8d81-182">For details, see [Statistics][Statistics].</span></span>

## <a name="next-steps"></a><span data-ttu-id="d8d81-183">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d8d81-183">Next steps</span></span>
<span data-ttu-id="d8d81-184">Aby uzyskać więcej porad programistycznych, zobacz hello [omówienie tworzenia][development overview].</span><span class="sxs-lookup"><span data-stu-id="d8d81-184">For more development tips, see hello [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)]: ./sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md
[Load data from Azure blob storage tooSQL Data Warehouse (Azure Data Factory)]: ./sql-data-warehouse-load-from-azure-blob-storage-with-data-factory.md
[Load data from SQL Server tooAzure SQL Data Warehouse (SSIS)]: ./sql-data-warehouse-load-from-sql-server-with-integration-services.md
[Load data from SQL Server tooAzure SQL Data Warehouse (bcp)]: ./sql-data-warehouse-load-from-sql-server-with-bcp.md
[Load data from SQL Server tooAzure SQL Data Warehouse (AZCopy)]: ./sql-data-warehouse-load-from-sql-server-with-azcopy.md

[Load sample databases]: ./sql-data-warehouse-load-sample-databases.md
[Migration overview]: ./sql-data-warehouse-overview-migrate.md
[solution partners]: ./sql-data-warehouse-partner-business-intelligence.md
[development overview]: ./sql-data-warehouse-overview-develop.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md

<!--MSDN references-->

<!--Other Web references-->
[Import/Export]: https://azure.microsoft.com/documentation/articles/storage-import-export-service/
