---
title: "aaaCopy danych do/z magazynu obiektów Blob Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocopy obiektu blob danych w fabryce danych Azure. Użyj naszej próbki: jak toocopy tooand danych z magazynu obiektów Blob Azure i bazy danych SQL Azure."
keywords: "dane obiektów blob, kopiowania obiektów blob platformy azure"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: bec8160f-5e07-47e4-8ee1-ebb14cfb805d
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jingwang
ms.openlocfilehash: 8428c64e8e8b1084b3f2f680c4e1819559e4ffa3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tooor-from-azure-blob-storage-using-azure-data-factory"></a><span data-ttu-id="6fceb-105">Skopiuj tooor danych z magazynu obiektów Blob platformy Azure przy użyciu fabryki danych Azure</span><span class="sxs-lookup"><span data-stu-id="6fceb-105">Copy data tooor from Azure Blob Storage using Azure Data Factory</span></span>
<span data-ttu-id="6fceb-106">W tym artykule opisano, jak toouse hello działanie kopiowania w fabryce danych Azure toocopy danych tooand z magazynu obiektów Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="6fceb-106">This article explains how toouse hello Copy Activity in Azure Data Factory toocopy data tooand from Azure Blob Storage.</span></span> <span data-ttu-id="6fceb-107">Opiera się na powitania [działań przepływu danych](data-factory-data-movement-activities.md) artykułu, który przedstawia ogólny przegląd przenoszenia danych z hello działanie kopiowania.</span><span class="sxs-lookup"><span data-stu-id="6fceb-107">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

## <a name="overview"></a><span data-ttu-id="6fceb-108">Omówienie</span><span class="sxs-lookup"><span data-stu-id="6fceb-108">Overview</span></span>
<span data-ttu-id="6fceb-109">Możesz skopiować dane z dowolnych obsługiwanych źródeł danych magazynu tooAzure magazynu obiektów Blob lub z magazynu obiektów Blob Azure tooany obsługiwane ujścia danych.</span><span class="sxs-lookup"><span data-stu-id="6fceb-109">You can copy data from any supported source data store tooAzure Blob Storage or from Azure Blob Storage tooany supported sink data store.</span></span> <span data-ttu-id="6fceb-110">Witaj Poniższa tabela zawiera listę magazynów danych są obsługiwane jako źródła lub wychwytywanie przez działanie kopiowania hello.</span><span class="sxs-lookup"><span data-stu-id="6fceb-110">hello following table provides a list of data stores supported as sources or sinks by hello copy activity.</span></span> <span data-ttu-id="6fceb-111">Na przykład można przenieść dane **z** bazy danych programu SQL Server lub bazy danych Azure SQL **do** magazynu obiektów blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6fceb-111">For example, you can move data **from** a SQL Server database or an Azure SQL database **to** an Azure blob storage.</span></span> <span data-ttu-id="6fceb-112">I dane należy skopiować **z** magazynu obiektów blob Azure **do** magazyn danych SQL Azure lub kolekcji usługi Azure DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="6fceb-112">And, you can copy data **from** Azure blob storage **to** an Azure SQL Data Warehouse or an Azure Cosmos DB collection.</span></span> 

## <a name="supported-scenarios"></a><span data-ttu-id="6fceb-113">Obsługiwane scenariusze</span><span class="sxs-lookup"><span data-stu-id="6fceb-113">Supported scenarios</span></span>
<span data-ttu-id="6fceb-114">Dane należy skopiować **z magazynu obiektów Blob Azure** toohello po magazynów danych:</span><span class="sxs-lookup"><span data-stu-id="6fceb-114">You can copy data **from Azure Blob Storage** toohello following data stores:</span></span>

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="6fceb-115">Można skopiować danych z powitania po magazyny danych **tooAzure magazynu obiektów Blob**:</span><span class="sxs-lookup"><span data-stu-id="6fceb-115">You can copy data from hello following data stores **tooAzure Blob Storage**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]
 
> [!IMPORTANT]
> <span data-ttu-id="6fceb-116">Działanie kopiowania obsługuje kopiowania danych z / tooboth kont magazynu ogólnego przeznaczenia Azure i Hot/Cool magazynu obiektów Blob.</span><span class="sxs-lookup"><span data-stu-id="6fceb-116">Copy Activity supports copying data from/tooboth general-purpose Azure Storage accounts and Hot/Cool Blob storage.</span></span> <span data-ttu-id="6fceb-117">działanie Hello obsługuje **czytania z bloku, Dołącz lub stronicowe**, ale obsługuje **zapisywania tooonly blokowych obiektów blob**.</span><span class="sxs-lookup"><span data-stu-id="6fceb-117">hello activity supports **reading from block, append, or page blobs**, but supports **writing tooonly block blobs**.</span></span> <span data-ttu-id="6fceb-118">Usługa Azure Premium Storage nie jest obsługiwany jako zbiorniku, ponieważ nie jest obsługiwana przez stronicowych obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="6fceb-118">Azure Premium Storage is not supported as a sink because it is backed by page blobs.</span></span>
> 
> <span data-ttu-id="6fceb-119">Aktywność kopiowania nie powoduje usunięcia danych ze źródła hello, po hello, którego dane są pomyślnie skopiowane toohello docelowego.</span><span class="sxs-lookup"><span data-stu-id="6fceb-119">Copy Activity does not delete data from hello source after hello data is successfully copied toohello destination.</span></span> <span data-ttu-id="6fceb-120">Jeśli potrzebujesz toodelete źródła danych po pomyślnym kopiowania utworzyć [działania niestandardowego](data-factory-use-custom-activities.md) toodelete hello danych i użyj hello działania w potoku hello.</span><span class="sxs-lookup"><span data-stu-id="6fceb-120">If you need toodelete source data after a successful copy, create a [custom activity](data-factory-use-custom-activities.md) toodelete hello data and use hello activity in hello pipeline.</span></span> <span data-ttu-id="6fceb-121">Na przykład zobacz hello [usuwania obiektów blob lub folderu przykładem w witrynie GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/DeleteBlobFileFolderCustomActivity).</span><span class="sxs-lookup"><span data-stu-id="6fceb-121">For an example, see hello [Delete blob or folder sample on GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/DeleteBlobFileFolderCustomActivity).</span></span> 

## <a name="get-started"></a><span data-ttu-id="6fceb-122">Rozpoczęcie pracy</span><span class="sxs-lookup"><span data-stu-id="6fceb-122">Get started</span></span>
<span data-ttu-id="6fceb-123">Można utworzyć potoku o działanie kopiowania, który przenosi dane z magazynu obiektów Blob Azure przy użyciu różnych narzędzi/interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="6fceb-123">You can create a pipeline with a copy activity that moves data to/from an Azure Blob Storage by using different tools/APIs.</span></span>

<span data-ttu-id="6fceb-124">Witaj Najprostszym sposobem toocreate potoku jest toouse hello **kreatora kopiowania**.</span><span class="sxs-lookup"><span data-stu-id="6fceb-124">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="6fceb-125">Ten artykuł zawiera [wskazówki](#walkthrough-use-copy-wizard-to-copy-data-tofrom-blob-storage) tworzenia danych toocopy potoku z tooanother lokalizacji magazynu obiektów Blob Azure lokalizacji magazynu obiektów Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="6fceb-125">This article has a [walkthrough](#walkthrough-use-copy-wizard-to-copy-data-tofrom-blob-storage) for creating a pipeline toocopy data from an Azure Blob Storage location  tooanother Azure Blob Storage location.</span></span> <span data-ttu-id="6fceb-126">Samouczek dotyczący tworzenia potoku toocopy danych z magazynu obiektów Blob Azure tooAzure bazy danych SQL, zobacz [samouczek: tworzenie potoku za pomocą Kreatora kopiowania](data-factory-copy-data-wizard-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="6fceb-126">For a tutorial on creating a pipeline toocopy data from an Azure Blob Storage tooAzure SQL Database, see [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md).</span></span>

<span data-ttu-id="6fceb-127">Można również użyć hello następujące narzędzia toocreate potoku: **portalu Azure**, **programu Visual Studio**, **programu Azure PowerShell**, **szablonu usługi Azure Resource Manager** , **Interfejs API .NET**, i **interfejsu API REST**.</span><span class="sxs-lookup"><span data-stu-id="6fceb-127">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="6fceb-128">Zobacz [samouczek działania kopiowania](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) dla toocreate instrukcje krok po kroku potoku z działaniem kopiowania.</span><span class="sxs-lookup"><span data-stu-id="6fceb-128">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span>

<span data-ttu-id="6fceb-129">Czy za pomocą narzędzia hello lub interfejsów API, należy wykonać następujące kroki toocreate potok, który przenosi się, że magazyn danych ze źródła danych magazynu danych zbiornika tooa hello:</span><span class="sxs-lookup"><span data-stu-id="6fceb-129">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="6fceb-130">Utwórz **fabryki danych**.</span><span class="sxs-lookup"><span data-stu-id="6fceb-130">Create a **data factory**.</span></span> <span data-ttu-id="6fceb-131">Fabryka danych może zawierać co najmniej jeden potoków.</span><span class="sxs-lookup"><span data-stu-id="6fceb-131">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="6fceb-132">Utwórz **połączone usługi** toolink usługi fabryka danych tooyour magazynów danych wejściowych i wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="6fceb-132">Create **linked services** toolink input and output data stores tooyour data factory.</span></span> <span data-ttu-id="6fceb-133">Na przykład jeśli dane są kopiowane z bazy danych Azure SQL tooan magazynu obiektów blob platformy Azure, utworzysz dwie toolink połączonych usług Twoje konto magazynu Azure i fabryki danych tooyour bazy danych Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="6fceb-133">For example, if you are copying data from an Azure blob storage tooan Azure SQL database, you create two linked services toolink your Azure storage account and Azure SQL database tooyour data factory.</span></span> <span data-ttu-id="6fceb-134">Dla właściwości połączonej usługi, które są określone tooAzure magazynu obiektów Blob, zobacz [połączona usługa właściwości](#linked-service-properties) sekcji.</span><span class="sxs-lookup"><span data-stu-id="6fceb-134">For linked service properties that are specific tooAzure Blob Storage, see [linked service properties](#linked-service-properties) section.</span></span> 
2. <span data-ttu-id="6fceb-135">Utwórz **zestawów danych** toorepresent wejściowe i wyjściowe dane hello operacji kopiowania.</span><span class="sxs-lookup"><span data-stu-id="6fceb-135">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> <span data-ttu-id="6fceb-136">Przykład Witaj wymienionych w ostatnim kroku hello służy do tworzenia kontenera obiektów blob hello toospecify zestawu danych i folderu zawierającego hello danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="6fceb-136">In hello example mentioned in hello last step, you create a dataset toospecify hello blob container and folder that contains hello input data.</span></span> <span data-ttu-id="6fceb-137">I utwórz inny zestaw danych toospecify hello tabeli SQL w bazie danych Azure SQL hello przechowujący dane hello skopiowane z magazynu obiektów blob hello.</span><span class="sxs-lookup"><span data-stu-id="6fceb-137">And, you create another dataset toospecify hello SQL table in hello Azure SQL database that holds hello data copied from hello blob storage.</span></span> <span data-ttu-id="6fceb-138">Dla właściwości zestawu danych, które są określone tooAzure magazynu obiektów Blob, zobacz [właściwości zestawu danych](#dataset-properties) sekcji.</span><span class="sxs-lookup"><span data-stu-id="6fceb-138">For dataset properties that are specific tooAzure Blob Storage, see [dataset properties](#dataset-properties) section.</span></span>
3. <span data-ttu-id="6fceb-139">Utwórz **potoku** aktywnością kopiowania zestawu danych jako dane wejściowe i zestawu danych jako dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="6fceb-139">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="6fceb-140">W przykładzie hello wspomniano wcześniej używa BlobSource jako źródło i SqlSink jako zbiorniku dla aktywności kopiowania hello.</span><span class="sxs-lookup"><span data-stu-id="6fceb-140">In hello example mentioned earlier, you use BlobSource as a source and SqlSink as a sink for hello copy activity.</span></span> <span data-ttu-id="6fceb-141">Podobnie są kopiowane z bazy danych SQL Azure tooAzure magazynu obiektów Blob, należy użyć SqlSource i BlobSink w przypadku działania kopiowania hello.</span><span class="sxs-lookup"><span data-stu-id="6fceb-141">Similarly, if you are copying from Azure SQL Database tooAzure Blob Storage, you use SqlSource and BlobSink in hello copy activity.</span></span> <span data-ttu-id="6fceb-142">Dla właściwości działania kopiowania, które są określone tooAzure magazynu obiektów Blob, zobacz [skopiować właściwości działania](#copy-activity-properties) sekcji.</span><span class="sxs-lookup"><span data-stu-id="6fceb-142">For copy activity properties that are specific tooAzure Blob Storage, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="6fceb-143">Szczegółowe informacje dotyczące sposobu toouse, Magazyn danych, jako źródło lub zbiorniku kliknij łącze hello w poprzedniej sekcji powitania dla magazynu danych.</span><span class="sxs-lookup"><span data-stu-id="6fceb-143">For details on how toouse a data store as a source or a sink, click hello link in hello previous section for your data store.</span></span>  

<span data-ttu-id="6fceb-144">Korzystając z Kreatora hello, definicje JSON do tych jednostek fabryki danych (połączone usługi, zestawy danych i potoku hello) są tworzone automatycznie dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="6fceb-144">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="6fceb-145">Korzystając z narzędzi/API (z wyjątkiem interfejs API .NET), należy zdefiniować za pomocą formatu JSON hello tych jednostek fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="6fceb-145">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="6fceb-146">Aby uzyskać przykłady z definicji JSON dla jednostek fabryki danych, które są używane toocopy danych do/z magazynu obiektów Blob Azure, zobacz [przykłady JSON](#json-examples-for-copying-data-to-and-from-blob-storage  ) sekcji tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="6fceb-146">For samples with JSON definitions for Data Factory entities that are used toocopy data to/from an Azure Blob Storage, see [JSON examples](#json-examples-for-copying-data-to-and-from-blob-storage  ) section of this article.</span></span>

<span data-ttu-id="6fceb-147">Witaj następujące sekcje zawierają szczegółowe informacje o właściwościach JSON, które są używane toodefine fabryki danych jednostek określonych tooAzure magazynu obiektów Blob.</span><span class="sxs-lookup"><span data-stu-id="6fceb-147">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooAzure Blob Storage.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="6fceb-148">Połączona usługa właściwości</span><span class="sxs-lookup"><span data-stu-id="6fceb-148">Linked service properties</span></span>
<span data-ttu-id="6fceb-149">Istnieją dwa typy połączonych usług można użyć toolink fabryki danych Azure tooan usługi Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="6fceb-149">There are two types of linked services you can use toolink an Azure Storage tooan Azure data factory.</span></span> <span data-ttu-id="6fceb-150">Są one: **AzureStorage** połączonej usługi i **element AzureStorageSas** połączonej usługi.</span><span class="sxs-lookup"><span data-stu-id="6fceb-150">They are: **AzureStorage** linked service and **AzureStorageSas** linked service.</span></span> <span data-ttu-id="6fceb-151">Witaj połączoną usługą magazynu Azure zapewnia usłudze fabryka danych hello z toohello dostępu globalny usługi Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="6fceb-151">hello Azure Storage linked service provides hello data factory with global access toohello Azure Storage.</span></span> <span data-ttu-id="6fceb-152">Związana hello Azure magazyn SAS (Shared Access Signature) usługa zapewnia usłudze fabryka danych hello z toohello dostęp ograniczony/czas-powiązane z usługi Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="6fceb-152">Whereas, hello Azure Storage SAS (Shared Access Signature) linked service provides hello data factory with restricted/time-bound access toohello Azure Storage.</span></span> <span data-ttu-id="6fceb-153">Nie istnieją inne różnice między tych dwóch połączonych usług.</span><span class="sxs-lookup"><span data-stu-id="6fceb-153">There are no other differences between these two linked services.</span></span> <span data-ttu-id="6fceb-154">Wybierz usługę hello połączony, który odpowiada Twoim potrzebom.</span><span class="sxs-lookup"><span data-stu-id="6fceb-154">Choose hello linked service that suits your needs.</span></span> <span data-ttu-id="6fceb-155">Hello poniższe sekcje zawierają więcej szczegółowych informacji na temat tych dwóch usług połączonych.</span><span class="sxs-lookup"><span data-stu-id="6fceb-155">hello following sections provide more details on these two linked services.</span></span>

[!INCLUDE [data-factory-azure-storage-linked-services](../../includes/data-factory-azure-storage-linked-services.md)]

## <a name="dataset-properties"></a><span data-ttu-id="6fceb-156">Właściwości zestawu danych</span><span class="sxs-lookup"><span data-stu-id="6fceb-156">Dataset properties</span></span>
<span data-ttu-id="6fceb-157">toospecify toorepresent zestawu danych wejściowych lub wyjściowych danych w magazynie obiektów Blob Azure, właściwość hello typu DataSet hello do: **AzureBlob**.</span><span class="sxs-lookup"><span data-stu-id="6fceb-157">toospecify a dataset toorepresent input or output data in an Azure Blob Storage, you set hello type property of hello dataset to: **AzureBlob**.</span></span> <span data-ttu-id="6fceb-158">Zestaw hello **linkedServiceName** właściwości zestawu danych hello toohello nazwę hello Azure Storage lub SAS magazynu Azure połączonej usługi.</span><span class="sxs-lookup"><span data-stu-id="6fceb-158">Set hello **linkedServiceName** property of hello dataset toohello name of hello Azure Storage or Azure Storage SAS linked service.</span></span>  <span data-ttu-id="6fceb-159">właściwości typu Hello DataSet hello Określ hello **kontenera obiektów blob** i hello **folderu** w magazynie obiektów blob hello.</span><span class="sxs-lookup"><span data-stu-id="6fceb-159">hello type properties of hello dataset specify hello **blob container** and hello **folder** in hello blob storage.</span></span>

<span data-ttu-id="6fceb-160">Pełną listę sekcje JSON & właściwości dostępne do definiowania zestawów danych, zobacz hello [Tworzenie zbiorów danych](data-factory-create-datasets.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="6fceb-160">For a full list of JSON sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="6fceb-161">Sekcje zawierają informacje, takie jak struktury, dostępności i zasad zestawu danych JSON są podobne dla wszystkich typów obiektów dataset (Azure SQL, obiektów blob platformy Azure, Azure tabeli itp.).</span><span class="sxs-lookup"><span data-stu-id="6fceb-161">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="6fceb-162">Fabryka danych obsługuje powitania po zgodne ze specyfikacją CLS .NET na podstawie wartości typu udostępnienie informacji o typie w "strukturę" dla źródeł danych schematu na odczytu obiektów blob platformy Azure: Int16, Int32, Int64, jeden, Double, Decimal, Byte [], Bool, String, Guid, Datetime, Datetimeoffset, Timespan.</span><span class="sxs-lookup"><span data-stu-id="6fceb-162">Data factory supports hello following CLS-compliant .NET based type values for providing type information in “structure” for schema-on-read data sources like Azure blob: Int16, Int32, Int64, Single, Double, Decimal, Byte[], Bool, String, Guid, Datetime, Datetimeoffset, Timespan.</span></span> <span data-ttu-id="6fceb-163">Fabryka danych automatycznie wykonuje konwersje typów przemieszczając się, że magazyn danych ze źródła danych magazynu danych tooa ujścia.</span><span class="sxs-lookup"><span data-stu-id="6fceb-163">Data Factory automatically performs type conversions when moving data from a source data store tooa sink data store.</span></span>

<span data-ttu-id="6fceb-164">Witaj **typeProperties** sekcja jest różne dla każdego typu zestawu danych i zawiera informacje o lokalizacji hello itp., format hello danych w magazynie danych hello.</span><span class="sxs-lookup"><span data-stu-id="6fceb-164">hello **typeProperties** section is different for each type of dataset and provides information about hello location, format etc., of hello data in hello data store.</span></span> <span data-ttu-id="6fceb-165">Witaj typeProperties sekcja dla zestawu danych typu **AzureBlob** dataset zawiera hello następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="6fceb-165">hello typeProperties section for dataset of type **AzureBlob** dataset has hello following properties:</span></span>

| <span data-ttu-id="6fceb-166">Właściwość</span><span class="sxs-lookup"><span data-stu-id="6fceb-166">Property</span></span> | <span data-ttu-id="6fceb-167">Opis</span><span class="sxs-lookup"><span data-stu-id="6fceb-167">Description</span></span> | <span data-ttu-id="6fceb-168">Wymagane</span><span class="sxs-lookup"><span data-stu-id="6fceb-168">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6fceb-169">folderPath</span><span class="sxs-lookup"><span data-stu-id="6fceb-169">folderPath</span></span> |<span data-ttu-id="6fceb-170">Ścieżka toohello kontenera i folderu w magazynie obiektów blob hello.</span><span class="sxs-lookup"><span data-stu-id="6fceb-170">Path toohello container and folder in hello blob storage.</span></span> <span data-ttu-id="6fceb-171">Przykład: myblobcontainer\myblobfolder\\</span><span class="sxs-lookup"><span data-stu-id="6fceb-171">Example: myblobcontainer\myblobfolder\\</span></span> |<span data-ttu-id="6fceb-172">Tak</span><span class="sxs-lookup"><span data-stu-id="6fceb-172">Yes</span></span> |
| <span data-ttu-id="6fceb-173">fileName</span><span class="sxs-lookup"><span data-stu-id="6fceb-173">fileName</span></span> |<span data-ttu-id="6fceb-174">Nazwa obiektu blob hello.</span><span class="sxs-lookup"><span data-stu-id="6fceb-174">Name of hello blob.</span></span> <span data-ttu-id="6fceb-175">Nazwa pliku jest opcjonalna i z uwzględnieniem wielkości liter.</span><span class="sxs-lookup"><span data-stu-id="6fceb-175">fileName is optional and case-sensitive.</span></span><br/><br/><span data-ttu-id="6fceb-176">Jeśli określono nazwę pliku, hello działania (takie jak kopiowanie) działa na hello konkretnego obiektu Blob.</span><span class="sxs-lookup"><span data-stu-id="6fceb-176">If you specify a filename, hello activity (including Copy) works on hello specific Blob.</span></span><br/><br/><span data-ttu-id="6fceb-177">Jeśli nie określono nazwy pliku, kopiowania obejmuje wszystkie obiekty BLOB w hello folderPath dla zestawu danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="6fceb-177">When fileName is not specified, Copy includes all Blobs in hello folderPath for input dataset.</span></span><br/><br/><span data-ttu-id="6fceb-178">Gdy **fileName** dla wyjściowego zestawu danych nie został określony i **preserveHierarchy** nie została określona w zbiornika działania hello nazwą hello wygenerowany plik będzie w powitania po ten format: dane.<Guid>. txt (na przykład:: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="6fceb-178">When **fileName** is not specified for an output dataset and **preserveHierarchy** is not specified in activity sink, hello name of hello generated file would be in hello following this format: Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="6fceb-179">Nie</span><span class="sxs-lookup"><span data-stu-id="6fceb-179">No</span></span> |
| <span data-ttu-id="6fceb-180">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="6fceb-180">partitionedBy</span></span> |<span data-ttu-id="6fceb-181">partitionedBy jest opcjonalna właściwość.</span><span class="sxs-lookup"><span data-stu-id="6fceb-181">partitionedBy is an optional property.</span></span> <span data-ttu-id="6fceb-182">Umożliwia toospecify folderPath dynamiczne i nazwę pliku dla czasu serii danych.</span><span class="sxs-lookup"><span data-stu-id="6fceb-182">You can use it toospecify a dynamic folderPath and filename for time series data.</span></span> <span data-ttu-id="6fceb-183">Na przykład folderPath mogą nadać parametry dla każdej godziny danych.</span><span class="sxs-lookup"><span data-stu-id="6fceb-183">For example, folderPath can be parameterized for every hour of data.</span></span> <span data-ttu-id="6fceb-184">Zobacz hello [przy użyciu sekcji właściwości partitionedBy](#using-partitionedBy-property) szczegółowe informacje i przykłady.</span><span class="sxs-lookup"><span data-stu-id="6fceb-184">See hello [Using partitionedBy property section](#using-partitionedBy-property) for details and examples.</span></span> |<span data-ttu-id="6fceb-185">Nie</span><span class="sxs-lookup"><span data-stu-id="6fceb-185">No</span></span> |
| <span data-ttu-id="6fceb-186">Format</span><span class="sxs-lookup"><span data-stu-id="6fceb-186">format</span></span> | <span data-ttu-id="6fceb-187">obsługiwane są następujące typy format Hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="6fceb-187">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="6fceb-188">Zestaw hello **typu** właściwości w formacie tooone tych wartości.</span><span class="sxs-lookup"><span data-stu-id="6fceb-188">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="6fceb-189">Aby uzyskać więcej informacji, zobacz [formacie tekstowym](data-factory-supported-file-and-compression-formats.md#text-format), [formatu Json](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), i [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sekcje.</span><span class="sxs-lookup"><span data-stu-id="6fceb-189">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="6fceb-190">Jeśli chcesz zbyt**skopiuj pliki jako — jest** między opartych na plikach magazynów (kopia binarnego), Pomiń sekcja format hello w obu definicji zestawu danych wejściowych i wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="6fceb-190">If you want too**copy files as-is** between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="6fceb-191">Nie</span><span class="sxs-lookup"><span data-stu-id="6fceb-191">No</span></span> |
| <span data-ttu-id="6fceb-192">Kompresja</span><span class="sxs-lookup"><span data-stu-id="6fceb-192">compression</span></span> | <span data-ttu-id="6fceb-193">Określ typ hello i poziom kompresji danych hello.</span><span class="sxs-lookup"><span data-stu-id="6fceb-193">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="6fceb-194">Obsługiwane typy to: **GZip**, **Deflate**, **BZip2**, i **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="6fceb-194">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="6fceb-195">Obsługiwane poziomy: **optymalna** i **najszybciej**.</span><span class="sxs-lookup"><span data-stu-id="6fceb-195">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="6fceb-196">Aby uzyskać więcej informacji, zobacz [formaty plików i kompresji w fabryce danych Azure](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="6fceb-196">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="6fceb-197">Nie</span><span class="sxs-lookup"><span data-stu-id="6fceb-197">No</span></span> |

### <a name="using-partitionedby-property"></a><span data-ttu-id="6fceb-198">Za pomocą właściwości partitionedBy</span><span class="sxs-lookup"><span data-stu-id="6fceb-198">Using partitionedBy property</span></span>
<span data-ttu-id="6fceb-199">Jak wspomniano w poprzedniej sekcji hello, można określić folderPath dynamiczne i nazwę pliku dla danych serii czasu z hello **partitionedBy** właściwość [funkcje fabryki danych i zmienne systemu hello](data-factory-functions-variables.md).</span><span class="sxs-lookup"><span data-stu-id="6fceb-199">As mentioned in hello previous section, you can specify a dynamic folderPath and filename for time series data with hello **partitionedBy** property, [Data Factory functions, and hello system variables](data-factory-functions-variables.md).</span></span>

<span data-ttu-id="6fceb-200">Aby uzyskać więcej informacji na zestawy danych serii czasu, planowanie i wycinków, zobacz [tworzenie zestawów danych](data-factory-create-datasets.md) i [planowanie i wykonanie](data-factory-scheduling-and-execution.md) artykułów.</span><span class="sxs-lookup"><span data-stu-id="6fceb-200">For more information on time series datasets, scheduling, and slices, see [Creating Datasets](data-factory-create-datasets.md) and [Scheduling & Execution](data-factory-scheduling-and-execution.md) articles.</span></span>

#### <a name="sample-1"></a><span data-ttu-id="6fceb-201">Przykład 1</span><span class="sxs-lookup"><span data-stu-id="6fceb-201">Sample 1</span></span>

```json
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```

<span data-ttu-id="6fceb-202">W tym przykładzie {wycinka} zostanie zastąpiony hello wartość zmiennej fabryki danych systemu SliceStart w formacie hello (YYYYMMDDHH) określona.</span><span class="sxs-lookup"><span data-stu-id="6fceb-202">In this example, {Slice} is replaced with hello value of Data Factory system variable SliceStart in hello format (YYYYMMDDHH) specified.</span></span> <span data-ttu-id="6fceb-203">Witaj SliceStart odwołuje się czas toostart hello wycinka.</span><span class="sxs-lookup"><span data-stu-id="6fceb-203">hello SliceStart refers toostart time of hello slice.</span></span> <span data-ttu-id="6fceb-204">Witaj folderPath jest różne dla każdego wycinka.</span><span class="sxs-lookup"><span data-stu-id="6fceb-204">hello folderPath is different for each slice.</span></span> <span data-ttu-id="6fceb-205">Na przykład: wikidatagateway/wikisampledataout/2014100103 lub wikidatagateway/wikisampledataout/2014100104</span><span class="sxs-lookup"><span data-stu-id="6fceb-205">For example: wikidatagateway/wikisampledataout/2014100103 or wikidatagateway/wikisampledataout/2014100104</span></span>

#### <a name="sample-2"></a><span data-ttu-id="6fceb-206">Przykład 2</span><span class="sxs-lookup"><span data-stu-id="6fceb-206">Sample 2</span></span>

```json
"folderPath": "wikidatagateway/wikisampledataout/{Year}/{Month}/{Day}",
"fileName": "{Hour}.csv",
"partitionedBy":
 [
    { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
    { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
    { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
    { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "hh" } }
],
```

<span data-ttu-id="6fceb-207">W tym przykładzie rok, miesiąc, dzień i czas SliceStart są wyodrębniane do oddzielnych zmiennych, które są używane przez właściwości folderPath i nazwę pliku.</span><span class="sxs-lookup"><span data-stu-id="6fceb-207">In this example, year, month, day, and time of SliceStart are extracted into separate variables that are used by folderPath and fileName properties.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="6fceb-208">Właściwości działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="6fceb-208">Copy activity properties</span></span>
<span data-ttu-id="6fceb-209">Pełną listę sekcje & właściwości dostępne do definiowania działań, zobacz hello [tworzenie potoków](data-factory-create-pipelines.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="6fceb-209">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="6fceb-210">Właściwości, takie jak nazwa, opis, dane wejściowe i wyjściowe zestawy danych i zasady są dostępne dla wszystkich typów działań.</span><span class="sxs-lookup"><span data-stu-id="6fceb-210">Properties such as name, description, input and output datasets, and policies are available for all types of activities.</span></span> <span data-ttu-id="6fceb-211">Właściwości dostępne w hello **typeProperties** sekcji hello działanie zależy od każdy typ działania.</span><span class="sxs-lookup"><span data-stu-id="6fceb-211">Whereas, properties available in hello **typeProperties** section of hello activity vary with each activity type.</span></span> <span data-ttu-id="6fceb-212">Dla działania kopiowania różnią się w zależności od typów hello źródeł i sink.</span><span class="sxs-lookup"><span data-stu-id="6fceb-212">For Copy activity, they vary depending on hello types of sources and sinks.</span></span> <span data-ttu-id="6fceb-213">Chcesz przenieść dane z magazynu obiektów Blob platformy Azure, należy ustawić typ źródła hello w przypadku działania kopiowania hello zbyt**BlobSource**.</span><span class="sxs-lookup"><span data-stu-id="6fceb-213">If you are moving data from an Azure Blob Storage, you set hello source type in hello copy activity too**BlobSource**.</span></span> <span data-ttu-id="6fceb-214">Podobnie jeśli przenosisz dane tooan magazynu obiektów Blob Azure ustawisz typ ujścia hello w przypadku działania kopiowania hello zbyt**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="6fceb-214">Similarly, if you are moving data tooan Azure Blob Storage, you set hello sink type in hello copy activity too**BlobSink**.</span></span> <span data-ttu-id="6fceb-215">Ta sekcja zawiera listę obsługiwanych przez BlobSource i BlobSink właściwości.</span><span class="sxs-lookup"><span data-stu-id="6fceb-215">This section provides a list of properties supported by BlobSource and BlobSink.</span></span>

<span data-ttu-id="6fceb-216">**BlobSource** obsługuje następujące właściwości w hello hello **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="6fceb-216">**BlobSource** supports hello following properties in hello **typeProperties** section:</span></span>

| <span data-ttu-id="6fceb-217">Właściwość</span><span class="sxs-lookup"><span data-stu-id="6fceb-217">Property</span></span> | <span data-ttu-id="6fceb-218">Opis</span><span class="sxs-lookup"><span data-stu-id="6fceb-218">Description</span></span> | <span data-ttu-id="6fceb-219">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="6fceb-219">Allowed values</span></span> | <span data-ttu-id="6fceb-220">Wymagane</span><span class="sxs-lookup"><span data-stu-id="6fceb-220">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6fceb-221">Cykliczne</span><span class="sxs-lookup"><span data-stu-id="6fceb-221">recursive</span></span> |<span data-ttu-id="6fceb-222">Wskazuje, czy hello są odczytywane dane rekursywnie z podfolderach hello lub tylko hello określonego folderu.</span><span class="sxs-lookup"><span data-stu-id="6fceb-222">Indicates whether hello data is read recursively from hello sub folders or only from hello specified folder.</span></span> |<span data-ttu-id="6fceb-223">TRUE, False (wartość domyślna)</span><span class="sxs-lookup"><span data-stu-id="6fceb-223">True (default value), False</span></span> |<span data-ttu-id="6fceb-224">Nie</span><span class="sxs-lookup"><span data-stu-id="6fceb-224">No</span></span> |

<span data-ttu-id="6fceb-225">**BlobSink** obsługuje następujące właściwości hello **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="6fceb-225">**BlobSink** supports hello following properties **typeProperties** section:</span></span>

| <span data-ttu-id="6fceb-226">Właściwość</span><span class="sxs-lookup"><span data-stu-id="6fceb-226">Property</span></span> | <span data-ttu-id="6fceb-227">Opis</span><span class="sxs-lookup"><span data-stu-id="6fceb-227">Description</span></span> | <span data-ttu-id="6fceb-228">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="6fceb-228">Allowed values</span></span> | <span data-ttu-id="6fceb-229">Wymagane</span><span class="sxs-lookup"><span data-stu-id="6fceb-229">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6fceb-230">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="6fceb-230">copyBehavior</span></span> |<span data-ttu-id="6fceb-231">Definiuje zachowanie kopii hello, gdy źródłem hello jest BlobSource lub systemu plików.</span><span class="sxs-lookup"><span data-stu-id="6fceb-231">Defines hello copy behavior when hello source is BlobSource or FileSystem.</span></span> |<span data-ttu-id="6fceb-232"><b>PreserveHierarchy</b>: zachowuje hello hierarchii plików w folderze docelowym hello.</span><span class="sxs-lookup"><span data-stu-id="6fceb-232"><b>PreserveHierarchy</b>: preserves hello file hierarchy in hello target folder.</span></span> <span data-ttu-id="6fceb-233">Ścieżka względna Hello folderu toosource pliku źródłowego jest identyczne toohello względnej ścieżki folderu tootarget pliku docelowego.</span><span class="sxs-lookup"><span data-stu-id="6fceb-233">hello relative path of source file toosource folder is identical toohello relative path of target file tootarget folder.</span></span><br/><br/><span data-ttu-id="6fceb-234"><b>FlattenHierarchy</b>: wszystkie pliki z folderu źródłowego hello znajdują się w hello najpierw poziomu folderu docelowego.</span><span class="sxs-lookup"><span data-stu-id="6fceb-234"><b>FlattenHierarchy</b>: all files from hello source folder are in hello first level of target folder.</span></span> <span data-ttu-id="6fceb-235">pliki docelowe Hello ma automatycznie wygeneruje nazwę.</span><span class="sxs-lookup"><span data-stu-id="6fceb-235">hello target files have auto generated name.</span></span> <br/><br/><span data-ttu-id="6fceb-236"><b>MergeFiles</b>: scala wszystkie pliki z pliku tooone folderu źródłowego hello.</span><span class="sxs-lookup"><span data-stu-id="6fceb-236"><b>MergeFiles</b>: merges all files from hello source folder tooone file.</span></span> <span data-ttu-id="6fceb-237">Jeśli określono hello nazwa pliku/obiektu Blob, nazwa pliku scalonych hello będzie hello określoną nazwą; w przeciwnym razie będzie nazwa pliku wygenerowana automatycznie.</span><span class="sxs-lookup"><span data-stu-id="6fceb-237">If hello File/Blob Name is specified, hello merged file name would be hello specified name; otherwise, would be auto-generated file name.</span></span> |<span data-ttu-id="6fceb-238">Nie</span><span class="sxs-lookup"><span data-stu-id="6fceb-238">No</span></span> |

<span data-ttu-id="6fceb-239">**BlobSource** obsługuje także te dwie właściwości dla zgodności z poprzednimi wersjami.</span><span class="sxs-lookup"><span data-stu-id="6fceb-239">**BlobSource** also supports these two properties for backward compatibility.</span></span>

* <span data-ttu-id="6fceb-240">**treatEmptyAsNull**: Określa, czy tootreat null lub pusty ciąg jako wartość null.</span><span class="sxs-lookup"><span data-stu-id="6fceb-240">**treatEmptyAsNull**: Specifies whether tootreat null or empty string as null value.</span></span>
* <span data-ttu-id="6fceb-241">**skipHeaderLineCount** — określa liczbę wierszy muszą pominięte.</span><span class="sxs-lookup"><span data-stu-id="6fceb-241">**skipHeaderLineCount** - Specifies how many lines need be skipped.</span></span> <span data-ttu-id="6fceb-242">Dotyczy tylko gdy wejściowy zestaw danych używa TextFormat.</span><span class="sxs-lookup"><span data-stu-id="6fceb-242">It is applicable only when input dataset is using TextFormat.</span></span>

<span data-ttu-id="6fceb-243">Podobnie **BlobSink** obsługuje hello następujące właściwości dla zgodności z poprzednimi wersjami.</span><span class="sxs-lookup"><span data-stu-id="6fceb-243">Similarly, **BlobSink** supports hello following property for backward compatibility.</span></span>

* <span data-ttu-id="6fceb-244">**blobWriterAddHeader**: Określa, czy nagłówek kolumny definicji podczas zapisywania tooan tooadd wyjściowy zestaw danych.</span><span class="sxs-lookup"><span data-stu-id="6fceb-244">**blobWriterAddHeader**: Specifies whether tooadd a header of column definitions while writing tooan output dataset.</span></span>

<span data-ttu-id="6fceb-245">Obsługa hello teraz zestawów danych, następujące właściwości, które implementują hello tę samą funkcjonalność: **treatEmptyAsNull**, **skipLineCount**, **firstRowAsHeader**.</span><span class="sxs-lookup"><span data-stu-id="6fceb-245">Datasets now support hello following properties that implement hello same functionality: **treatEmptyAsNull**, **skipLineCount**, **firstRowAsHeader**.</span></span>

<span data-ttu-id="6fceb-246">Witaj poniższej tabeli znajdują się wskazówki dotyczące przy użyciu hello nowych właściwości zestawu danych, zamiast tych właściwości źródło/ujście obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="6fceb-246">hello following table provides guidance on using hello new dataset properties in place of these blob source/sink properties.</span></span>

| <span data-ttu-id="6fceb-247">Właściwości działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="6fceb-247">Copy Activity property</span></span> | <span data-ttu-id="6fceb-248">Właściwości zestawu danych</span><span class="sxs-lookup"><span data-stu-id="6fceb-248">Dataset property</span></span> |
|:--- |:--- |
| <span data-ttu-id="6fceb-249">skipHeaderLineCount na BlobSource</span><span class="sxs-lookup"><span data-stu-id="6fceb-249">skipHeaderLineCount on BlobSource</span></span> |<span data-ttu-id="6fceb-250">skipLineCount i firstRowAsHeader.</span><span class="sxs-lookup"><span data-stu-id="6fceb-250">skipLineCount and firstRowAsHeader.</span></span> <span data-ttu-id="6fceb-251">Wiersze są pomijane najpierw i Odczytaj hello pierwszego wiersza jako nagłówka.</span><span class="sxs-lookup"><span data-stu-id="6fceb-251">Lines are skipped first and then hello first row is read as a header.</span></span> |
| <span data-ttu-id="6fceb-252">treatEmptyAsNull na BlobSource</span><span class="sxs-lookup"><span data-stu-id="6fceb-252">treatEmptyAsNull on BlobSource</span></span> |<span data-ttu-id="6fceb-253">treatEmptyAsNull w zestawie danych wejściowych</span><span class="sxs-lookup"><span data-stu-id="6fceb-253">treatEmptyAsNull on input dataset</span></span> |
| <span data-ttu-id="6fceb-254">blobWriterAddHeader na BlobSink</span><span class="sxs-lookup"><span data-stu-id="6fceb-254">blobWriterAddHeader on BlobSink</span></span> |<span data-ttu-id="6fceb-255">firstRowAsHeader w zestawie danych wyjściowych</span><span class="sxs-lookup"><span data-stu-id="6fceb-255">firstRowAsHeader on output dataset</span></span> |

<span data-ttu-id="6fceb-256">Zobacz [określenie TextFormat](data-factory-supported-file-and-compression-formats.md#text-format) sekcji, aby uzyskać szczegółowe informacje na temat tych właściwości.</span><span class="sxs-lookup"><span data-stu-id="6fceb-256">See [Specifying TextFormat](data-factory-supported-file-and-compression-formats.md#text-format) section for detailed information on these properties.</span></span>    

### <a name="recursive-and-copybehavior-examples"></a><span data-ttu-id="6fceb-257">Przykłady cyklicznego i copyBehavior</span><span class="sxs-lookup"><span data-stu-id="6fceb-257">recursive and copyBehavior examples</span></span>
<span data-ttu-id="6fceb-258">W tej sekcji opisano hello efekty hello operacji kopiowania dla różnych kombinacji wartości cyklicznej i copyBehavior.</span><span class="sxs-lookup"><span data-stu-id="6fceb-258">This section describes hello resulting behavior of hello Copy operation for different combinations of recursive and copyBehavior values.</span></span>

| <span data-ttu-id="6fceb-259">Cykliczne</span><span class="sxs-lookup"><span data-stu-id="6fceb-259">recursive</span></span> | <span data-ttu-id="6fceb-260">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="6fceb-260">copyBehavior</span></span> | <span data-ttu-id="6fceb-261">Efekty</span><span class="sxs-lookup"><span data-stu-id="6fceb-261">Resulting behavior</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6fceb-262">Wartość true</span><span class="sxs-lookup"><span data-stu-id="6fceb-262">true</span></span> |<span data-ttu-id="6fceb-263">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="6fceb-263">preserveHierarchy</span></span> |<span data-ttu-id="6fceb-264">Dla folderu źródłowego Folder1 z następującej struktury hello:</span><span class="sxs-lookup"><span data-stu-id="6fceb-264">For a source folder Folder1 with hello following structure:</span></span> <br/><br/><span data-ttu-id="6fceb-265">Folder1</span><span class="sxs-lookup"><span data-stu-id="6fceb-265">Folder1</span></span><br/><span data-ttu-id="6fceb-266">&nbsp;&nbsp;&nbsp;&nbsp;Plik1</span><span class="sxs-lookup"><span data-stu-id="6fceb-266">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="6fceb-267">&nbsp;&nbsp;&nbsp;&nbsp;Plik2</span><span class="sxs-lookup"><span data-stu-id="6fceb-267">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="6fceb-268">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="6fceb-268">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="6fceb-269">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Plik3</span><span class="sxs-lookup"><span data-stu-id="6fceb-269">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="6fceb-270">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="6fceb-270">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="6fceb-271">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="6fceb-271">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="6fceb-272">folder docelowy Hello Folder1 jest tworzony z hello takie same struktury jako źródło hello</span><span class="sxs-lookup"><span data-stu-id="6fceb-272">hello target folder Folder1 is created with hello same structure as hello source</span></span><br/><br/><span data-ttu-id="6fceb-273">Folder1</span><span class="sxs-lookup"><span data-stu-id="6fceb-273">Folder1</span></span><br/><span data-ttu-id="6fceb-274">&nbsp;&nbsp;&nbsp;&nbsp;Plik1</span><span class="sxs-lookup"><span data-stu-id="6fceb-274">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="6fceb-275">&nbsp;&nbsp;&nbsp;&nbsp;Plik2</span><span class="sxs-lookup"><span data-stu-id="6fceb-275">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="6fceb-276">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="6fceb-276">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="6fceb-277">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Plik3</span><span class="sxs-lookup"><span data-stu-id="6fceb-277">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="6fceb-278">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="6fceb-278">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="6fceb-279">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5.</span><span class="sxs-lookup"><span data-stu-id="6fceb-279">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5.</span></span> |
| <span data-ttu-id="6fceb-280">Wartość true</span><span class="sxs-lookup"><span data-stu-id="6fceb-280">true</span></span> |<span data-ttu-id="6fceb-281">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="6fceb-281">flattenHierarchy</span></span> |<span data-ttu-id="6fceb-282">Dla folderu źródłowego Folder1 z następującej struktury hello:</span><span class="sxs-lookup"><span data-stu-id="6fceb-282">For a source folder Folder1 with hello following structure:</span></span> <br/><br/><span data-ttu-id="6fceb-283">Folder1</span><span class="sxs-lookup"><span data-stu-id="6fceb-283">Folder1</span></span><br/><span data-ttu-id="6fceb-284">&nbsp;&nbsp;&nbsp;&nbsp;Plik1</span><span class="sxs-lookup"><span data-stu-id="6fceb-284">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="6fceb-285">&nbsp;&nbsp;&nbsp;&nbsp;Plik2</span><span class="sxs-lookup"><span data-stu-id="6fceb-285">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="6fceb-286">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="6fceb-286">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="6fceb-287">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Plik3</span><span class="sxs-lookup"><span data-stu-id="6fceb-287">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="6fceb-288">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="6fceb-288">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="6fceb-289">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="6fceb-289">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="6fceb-290">docelowy Hello Folder1 jest tworzony z następującej struktury hello:</span><span class="sxs-lookup"><span data-stu-id="6fceb-290">hello target Folder1 is created with hello following structure:</span></span> <br/><br/><span data-ttu-id="6fceb-291">Folder1</span><span class="sxs-lookup"><span data-stu-id="6fceb-291">Folder1</span></span><br/><span data-ttu-id="6fceb-292">&nbsp;&nbsp;&nbsp;&nbsp;Nazwa wygenerowana automatycznie Plik1</span><span class="sxs-lookup"><span data-stu-id="6fceb-292">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="6fceb-293">&nbsp;&nbsp;&nbsp;&nbsp;Nazwa wygenerowana automatycznie plik2</span><span class="sxs-lookup"><span data-stu-id="6fceb-293">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><span data-ttu-id="6fceb-294">&nbsp;&nbsp;&nbsp;&nbsp;Nazwa wygenerowana automatycznie plik3</span><span class="sxs-lookup"><span data-stu-id="6fceb-294">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File3</span></span><br/><span data-ttu-id="6fceb-295">&nbsp;&nbsp;&nbsp;&nbsp;Nazwa wygenerowana automatycznie File4</span><span class="sxs-lookup"><span data-stu-id="6fceb-295">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File4</span></span><br/><span data-ttu-id="6fceb-296">&nbsp;&nbsp;&nbsp;&nbsp;Nazwa wygenerowana automatycznie File5</span><span class="sxs-lookup"><span data-stu-id="6fceb-296">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File5</span></span> |
| <span data-ttu-id="6fceb-297">Wartość true</span><span class="sxs-lookup"><span data-stu-id="6fceb-297">true</span></span> |<span data-ttu-id="6fceb-298">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="6fceb-298">mergeFiles</span></span> |<span data-ttu-id="6fceb-299">Dla folderu źródłowego Folder1 z następującej struktury hello:</span><span class="sxs-lookup"><span data-stu-id="6fceb-299">For a source folder Folder1 with hello following structure:</span></span> <br/><br/><span data-ttu-id="6fceb-300">Folder1</span><span class="sxs-lookup"><span data-stu-id="6fceb-300">Folder1</span></span><br/><span data-ttu-id="6fceb-301">&nbsp;&nbsp;&nbsp;&nbsp;Plik1</span><span class="sxs-lookup"><span data-stu-id="6fceb-301">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="6fceb-302">&nbsp;&nbsp;&nbsp;&nbsp;Plik2</span><span class="sxs-lookup"><span data-stu-id="6fceb-302">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="6fceb-303">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="6fceb-303">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="6fceb-304">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Plik3</span><span class="sxs-lookup"><span data-stu-id="6fceb-304">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="6fceb-305">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="6fceb-305">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="6fceb-306">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="6fceb-306">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="6fceb-307">docelowy Hello Folder1 jest tworzony z następującej struktury hello:</span><span class="sxs-lookup"><span data-stu-id="6fceb-307">hello target Folder1 is created with hello following structure:</span></span> <br/><br/><span data-ttu-id="6fceb-308">Folder1</span><span class="sxs-lookup"><span data-stu-id="6fceb-308">Folder1</span></span><br/><span data-ttu-id="6fceb-309">&nbsp;&nbsp;&nbsp;&nbsp;Plik1 + plik2 + plik3 + File4 + pliku 5 zawartości są scalane w jeden plik o nazwie generowanych automatycznie</span><span class="sxs-lookup"><span data-stu-id="6fceb-309">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 + File3 + File4 + File 5 contents are merged into one file with auto-generated file name</span></span> |
| <span data-ttu-id="6fceb-310">wartość false</span><span class="sxs-lookup"><span data-stu-id="6fceb-310">false</span></span> |<span data-ttu-id="6fceb-311">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="6fceb-311">preserveHierarchy</span></span> |<span data-ttu-id="6fceb-312">Dla folderu źródłowego Folder1 z następującej struktury hello:</span><span class="sxs-lookup"><span data-stu-id="6fceb-312">For a source folder Folder1 with hello following structure:</span></span> <br/><br/><span data-ttu-id="6fceb-313">Folder1</span><span class="sxs-lookup"><span data-stu-id="6fceb-313">Folder1</span></span><br/><span data-ttu-id="6fceb-314">&nbsp;&nbsp;&nbsp;&nbsp;Plik1</span><span class="sxs-lookup"><span data-stu-id="6fceb-314">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="6fceb-315">&nbsp;&nbsp;&nbsp;&nbsp;Plik2</span><span class="sxs-lookup"><span data-stu-id="6fceb-315">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="6fceb-316">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="6fceb-316">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="6fceb-317">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Plik3</span><span class="sxs-lookup"><span data-stu-id="6fceb-317">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="6fceb-318">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="6fceb-318">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="6fceb-319">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="6fceb-319">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="6fceb-320">folder docelowy Hello Folder1 jest tworzony z hello następujące struktury</span><span class="sxs-lookup"><span data-stu-id="6fceb-320">hello target folder Folder1 is created with hello following structure</span></span><br/><br/><span data-ttu-id="6fceb-321">Folder1</span><span class="sxs-lookup"><span data-stu-id="6fceb-321">Folder1</span></span><br/><span data-ttu-id="6fceb-322">&nbsp;&nbsp;&nbsp;&nbsp;Plik1</span><span class="sxs-lookup"><span data-stu-id="6fceb-322">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="6fceb-323">&nbsp;&nbsp;&nbsp;&nbsp;Plik2</span><span class="sxs-lookup"><span data-stu-id="6fceb-323">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><br/><br/><span data-ttu-id="6fceb-324">Subfolder1 plik3, File4 i File5 nie są odczytywane.</span><span class="sxs-lookup"><span data-stu-id="6fceb-324">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |
| <span data-ttu-id="6fceb-325">wartość false</span><span class="sxs-lookup"><span data-stu-id="6fceb-325">false</span></span> |<span data-ttu-id="6fceb-326">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="6fceb-326">flattenHierarchy</span></span> |<span data-ttu-id="6fceb-327">Dla folderu źródłowego Folder1 z następującej struktury hello:</span><span class="sxs-lookup"><span data-stu-id="6fceb-327">For a source folder Folder1 with hello following structure:</span></span><br/><br/><span data-ttu-id="6fceb-328">Folder1</span><span class="sxs-lookup"><span data-stu-id="6fceb-328">Folder1</span></span><br/><span data-ttu-id="6fceb-329">&nbsp;&nbsp;&nbsp;&nbsp;Plik1</span><span class="sxs-lookup"><span data-stu-id="6fceb-329">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="6fceb-330">&nbsp;&nbsp;&nbsp;&nbsp;Plik2</span><span class="sxs-lookup"><span data-stu-id="6fceb-330">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="6fceb-331">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="6fceb-331">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="6fceb-332">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Plik3</span><span class="sxs-lookup"><span data-stu-id="6fceb-332">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="6fceb-333">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="6fceb-333">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="6fceb-334">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="6fceb-334">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="6fceb-335">folder docelowy Hello Folder1 jest tworzony z hello następujące struktury</span><span class="sxs-lookup"><span data-stu-id="6fceb-335">hello target folder Folder1 is created with hello following structure</span></span><br/><br/><span data-ttu-id="6fceb-336">Folder1</span><span class="sxs-lookup"><span data-stu-id="6fceb-336">Folder1</span></span><br/><span data-ttu-id="6fceb-337">&nbsp;&nbsp;&nbsp;&nbsp;Nazwa wygenerowana automatycznie Plik1</span><span class="sxs-lookup"><span data-stu-id="6fceb-337">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="6fceb-338">&nbsp;&nbsp;&nbsp;&nbsp;Nazwa wygenerowana automatycznie plik2</span><span class="sxs-lookup"><span data-stu-id="6fceb-338">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><br/><br/><span data-ttu-id="6fceb-339">Subfolder1 plik3, File4 i File5 nie są odczytywane.</span><span class="sxs-lookup"><span data-stu-id="6fceb-339">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |
| <span data-ttu-id="6fceb-340">wartość false</span><span class="sxs-lookup"><span data-stu-id="6fceb-340">false</span></span> |<span data-ttu-id="6fceb-341">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="6fceb-341">mergeFiles</span></span> |<span data-ttu-id="6fceb-342">Dla folderu źródłowego Folder1 z następującej struktury hello:</span><span class="sxs-lookup"><span data-stu-id="6fceb-342">For a source folder Folder1 with hello following structure:</span></span><br/><br/><span data-ttu-id="6fceb-343">Folder1</span><span class="sxs-lookup"><span data-stu-id="6fceb-343">Folder1</span></span><br/><span data-ttu-id="6fceb-344">&nbsp;&nbsp;&nbsp;&nbsp;Plik1</span><span class="sxs-lookup"><span data-stu-id="6fceb-344">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="6fceb-345">&nbsp;&nbsp;&nbsp;&nbsp;Plik2</span><span class="sxs-lookup"><span data-stu-id="6fceb-345">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="6fceb-346">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="6fceb-346">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="6fceb-347">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Plik3</span><span class="sxs-lookup"><span data-stu-id="6fceb-347">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="6fceb-348">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="6fceb-348">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="6fceb-349">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="6fceb-349">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="6fceb-350">folder docelowy Hello Folder1 jest tworzony z hello następujące struktury</span><span class="sxs-lookup"><span data-stu-id="6fceb-350">hello target folder Folder1 is created with hello following structure</span></span><br/><br/><span data-ttu-id="6fceb-351">Folder1</span><span class="sxs-lookup"><span data-stu-id="6fceb-351">Folder1</span></span><br/><span data-ttu-id="6fceb-352">&nbsp;&nbsp;&nbsp;&nbsp;Plik1 + plik2 zawartości są scalane w jeden plik o nazwie wygenerowany automatycznie.</span><span class="sxs-lookup"><span data-stu-id="6fceb-352">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 contents are merged into one file with auto-generated file name.</span></span> <span data-ttu-id="6fceb-353">Nazwa wygenerowana automatycznie Plik1</span><span class="sxs-lookup"><span data-stu-id="6fceb-353">auto-generated name for File1</span></span><br/><br/><span data-ttu-id="6fceb-354">Subfolder1 plik3, File4 i File5 nie są odczytywane.</span><span class="sxs-lookup"><span data-stu-id="6fceb-354">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |

## <a name="walkthrough-use-copy-wizard-toocopy-data-tofrom-blob-storage"></a><span data-ttu-id="6fceb-355">Wskazówki: Użyj Kreatora kopiowania toocopy danych do/z magazynu obiektów Blob</span><span class="sxs-lookup"><span data-stu-id="6fceb-355">Walkthrough: Use Copy Wizard toocopy data to/from Blob Storage</span></span>
<span data-ttu-id="6fceb-356">Oto jak magazynu obiektów blob tooquickly kopiowania danych z platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6fceb-356">Let's look at how tooquickly copy data to/from an Azure blob storage.</span></span> <span data-ttu-id="6fceb-357">W tym przewodniku danych na serwerze źródłowym i docelowym są przechowywane typu: magazyn obiektów Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="6fceb-357">In this walkthrough, both source and destination data stores of type: Azure Blob Storage.</span></span> <span data-ttu-id="6fceb-358">Witaj potoku, w tym przewodniku kopiuje dane z tooanother folderu w hello tego samego kontenera obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="6fceb-358">hello pipeline in this walkthrough copies data from a folder tooanother folder in hello same blob container.</span></span> <span data-ttu-id="6fceb-359">Ten przewodnik jest celowo proste tooshow ustawienia lub właściwości w przypadku używania magazynu obiektów Blob jako źródło lub ujścia.</span><span class="sxs-lookup"><span data-stu-id="6fceb-359">This walkthrough is intentionally simple tooshow you settings or properties when using Blob Storage as a source or sink.</span></span> 

### <a name="prerequisites"></a><span data-ttu-id="6fceb-360">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="6fceb-360">Prerequisites</span></span>
1. <span data-ttu-id="6fceb-361">Utwórz ogólnego przeznaczenia **konta magazynu Azure** Jeśli nie masz już.</span><span class="sxs-lookup"><span data-stu-id="6fceb-361">Create a general-purpose **Azure Storage Account** if you don't have one already.</span></span> <span data-ttu-id="6fceb-362">Użyj magazynu obiektów blob hello jednocześnie jako **źródła** i **docelowego** magazynu danych, w tym przewodniku.</span><span class="sxs-lookup"><span data-stu-id="6fceb-362">You use hello blob storage as both **source** and **destination** data store in this walkthrough.</span></span> <span data-ttu-id="6fceb-363">Jeśli nie masz konta magazynu platformy Azure, zobacz hello [Utwórz konto magazynu](../storage/common/storage-create-storage-account.md#create-a-storage-account) artykuł, aby toocreate kroki, jeden.</span><span class="sxs-lookup"><span data-stu-id="6fceb-363">if you don't have an Azure storage account, see hello [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) article for steps toocreate one.</span></span>
2. <span data-ttu-id="6fceb-364">Tworzenie kontenera obiektów blob o nazwie **adfblobconnector** hello koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="6fceb-364">Create a blob container named **adfblobconnector** in hello storage account.</span></span> 
4. <span data-ttu-id="6fceb-365">Utwórz folder o nazwie **wejściowych** w hello **adfblobconnector** kontenera.</span><span class="sxs-lookup"><span data-stu-id="6fceb-365">Create a folder named **input** in hello **adfblobconnector** container.</span></span>
5. <span data-ttu-id="6fceb-366">Utwórz plik o nazwie **emp.txt** z powitania po zawartości i przekaż go toohello **wejściowych** folderu za pomocą narzędzi takich jak [Eksploratora usługi Storage platformy Azure](https://azurestorageexplorer.codeplex.com/)</span><span class="sxs-lookup"><span data-stu-id="6fceb-366">Create a file named **emp.txt** with hello following content and upload it toohello **input** folder by using tools such as [Azure Storage Explorer](https://azurestorageexplorer.codeplex.com/)</span></span>
    ```json
    John, Doe
    Jane, Doe
    ```
### <a name="create-hello-data-factory"></a><span data-ttu-id="6fceb-367">Tworzenie fabryki danych hello</span><span class="sxs-lookup"><span data-stu-id="6fceb-367">Create hello data factory</span></span>
1. <span data-ttu-id="6fceb-368">Zaloguj się toohello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6fceb-368">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="6fceb-369">Kliknij przycisk **+ nowy** hello lewym górnym rogu kliknij **analizy i analiza**i kliknij przycisk **fabryki danych**.</span><span class="sxs-lookup"><span data-stu-id="6fceb-369">Click **+ NEW** from hello top-left corner, click **Intelligence + analytics**, and click **Data Factory**.</span></span>
3. <span data-ttu-id="6fceb-370">W hello **nowa fabryka danych** bloku:</span><span class="sxs-lookup"><span data-stu-id="6fceb-370">In hello **New data factory** blade:</span></span>   
    1. <span data-ttu-id="6fceb-371">Wprowadź **ADFBlobConnectorDF** dla hello **nazwa**.</span><span class="sxs-lookup"><span data-stu-id="6fceb-371">Enter **ADFBlobConnectorDF** for hello **name**.</span></span> <span data-ttu-id="6fceb-372">Nazwa fabryki danych Azure hello Hello musi być globalnie unikatowe.</span><span class="sxs-lookup"><span data-stu-id="6fceb-372">hello name of hello Azure data factory must be globally unique.</span></span> <span data-ttu-id="6fceb-373">Jeśli wystąpi błąd hello: `*Data factory name “ADFBlobConnectorDF” is not available`, Zmień nazwę hello hello fabryki danych (na przykład yournameADFBlobConnectorDF) i spróbuj ponownie utworzyć.</span><span class="sxs-lookup"><span data-stu-id="6fceb-373">If you receive hello error: `*Data factory name “ADFBlobConnectorDF” is not available`, change hello name of hello data factory (for example, yournameADFBlobConnectorDF) and try creating again.</span></span> <span data-ttu-id="6fceb-374">Artykuł [Data Factory — Naming Rules](data-factory-naming-rules.md) (Fabryka danych — zasady nazewnictwa) zawiera zasady nazewnictwa artefaktów usługi Fabryka danych.</span><span class="sxs-lookup"><span data-stu-id="6fceb-374">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>
    2. <span data-ttu-id="6fceb-375">Wybierz swoją **subskrypcję** platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6fceb-375">Select your Azure **subscription**.</span></span>
    3. <span data-ttu-id="6fceb-376">Dla grupy zasobów, wybierz **Użyj istniejącego** tooselect istniejącego zasobu grupy (lub) wybierz **Utwórz nowy** tooenter nazwę grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="6fceb-376">For Resource Group, select **Use existing** tooselect an existing resource group (or) select **Create new** tooenter a name for a resource group.</span></span>
    4. <span data-ttu-id="6fceb-377">Wybierz **lokalizacji** hello fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="6fceb-377">Select a **location** for hello data factory.</span></span>
    5. <span data-ttu-id="6fceb-378">Wybierz **toodashboard numeru Pin** pole wyboru u dołu hello hello bloku.</span><span class="sxs-lookup"><span data-stu-id="6fceb-378">Select **Pin toodashboard** check box at hello bottom of hello blade.</span></span>
    6. <span data-ttu-id="6fceb-379">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="6fceb-379">Click **Create**.</span></span>
3. <span data-ttu-id="6fceb-380">Po zakończeniu tworzenia hello Zobacz hello **fabryki danych** bloku, jak pokazano w powitania po obrazu: ![strony głównej fabryki danych](./media/data-factory-azure-blob-connector/data-factory-home-page.png)</span><span class="sxs-lookup"><span data-stu-id="6fceb-380">After hello creation is complete, you see hello **Data Factory** blade as shown in hello following image: ![Data factory home page](./media/data-factory-azure-blob-connector/data-factory-home-page.png)</span></span>

### <a name="copy-wizard"></a><span data-ttu-id="6fceb-381">Kreator kopiowania</span><span class="sxs-lookup"><span data-stu-id="6fceb-381">Copy Wizard</span></span>
1. <span data-ttu-id="6fceb-382">Na stronie głównej fabryki danych powitania kliknij hello **kopiowanie danych [Podgląd]** Kafelek toolaunch **kreatora kopiowania danych** w osobnej karcie.</span><span class="sxs-lookup"><span data-stu-id="6fceb-382">On hello Data Factory home page, click hello **Copy data [PREVIEW]** tile toolaunch **Copy Data Wizard** in a separate tab.</span></span>    
    
    > [!NOTE]
    >    <span data-ttu-id="6fceb-383">Jeśli widzisz tej przeglądarki sieci web hello jest zablokowany na "Autoryzowanie...", wyłącz/Usuń zaznaczenie pola wyboru **zablokować pliki cookie innych firm, a dane lokacji** ustawienie (lub) schowaj włączone i utworzyć wyjątek **login.microsoftonline.com**, a następnie spróbuj ponownie uruchomić Kreatora hello.</span><span class="sxs-lookup"><span data-stu-id="6fceb-383">If you see that hello web browser is stuck at "Authorizing...", disable/uncheck **Block third-party cookies and site data** setting (or) keep it enabled and create an exception for **login.microsoftonline.com** and then try launching hello wizard again.</span></span>
2. <span data-ttu-id="6fceb-384">W hello **właściwości** strony:</span><span class="sxs-lookup"><span data-stu-id="6fceb-384">In hello **Properties** page:</span></span>
    1. <span data-ttu-id="6fceb-385">Wprowadź **CopyPipeline** dla **Nazwa zadania**.</span><span class="sxs-lookup"><span data-stu-id="6fceb-385">Enter **CopyPipeline** for **Task name**.</span></span> <span data-ttu-id="6fceb-386">Nazwa zadania Hello jest nazwa hello hello potok w fabryce danych.</span><span class="sxs-lookup"><span data-stu-id="6fceb-386">hello task name is hello name of hello pipeline in your data factory.</span></span>
    2. <span data-ttu-id="6fceb-387">Wprowadź **opis** hello zadania (opcjonalnie).</span><span class="sxs-lookup"><span data-stu-id="6fceb-387">Enter a **description** for hello task (optional).</span></span>
    3. <span data-ttu-id="6fceb-388">Dla **okresach zadań lub harmonogram zadań**, Zachowaj hello **regularnego uruchamiania zgodnie z harmonogramem** opcji.</span><span class="sxs-lookup"><span data-stu-id="6fceb-388">For **Task cadence or Task schedule**, keep hello **Run regularly on schedule** option.</span></span> <span data-ttu-id="6fceb-389">Jeśli chcesz toorun to zadanie tylko raz zamiast cyklicznie uruchamiany zgodnie z harmonogramem, wybierz opcję **uruchom raz teraz**.</span><span class="sxs-lookup"><span data-stu-id="6fceb-389">If you want toorun this task only once instead of run repeatedly on a schedule, select **Run once now**.</span></span> <span data-ttu-id="6fceb-390">Jeśli zostanie wybrana, **uruchom raz teraz** opcji [potoku jednorazowego](data-factory-create-pipelines.md#onetime-pipeline) jest tworzony.</span><span class="sxs-lookup"><span data-stu-id="6fceb-390">If you select, **Run once now** option, a [one-time pipeline](data-factory-create-pipelines.md#onetime-pipeline) is created.</span></span> 
    4. <span data-ttu-id="6fceb-391">Ustawienia hello zachować **wzorzec cykliczny**.</span><span class="sxs-lookup"><span data-stu-id="6fceb-391">Keep hello settings for **Recurring pattern**.</span></span> <span data-ttu-id="6fceb-392">To zadanie codziennie działa między hello rozpoczęcia i zakończenia godzin należy określić w hello następnego kroku.</span><span class="sxs-lookup"><span data-stu-id="6fceb-392">This task runs daily between hello start and end times you specify in hello next step.</span></span>
    5. <span data-ttu-id="6fceb-393">Zmień hello **Data i godzina rozpoczęcia** za**2017-04/21**.</span><span class="sxs-lookup"><span data-stu-id="6fceb-393">Change hello **Start date time** too**04/21/2017**.</span></span> 
    6. <span data-ttu-id="6fceb-394">Zmień hello **Data i godzina zakończenia** za**04/25/2017**.</span><span class="sxs-lookup"><span data-stu-id="6fceb-394">Change hello **End date time** too**04/25/2017**.</span></span> <span data-ttu-id="6fceb-395">Może być data hello tootype zamiast przeglądania hello kalendarza.</span><span class="sxs-lookup"><span data-stu-id="6fceb-395">You may want tootype hello date instead of browsing through hello calendar.</span></span>     
    8. <span data-ttu-id="6fceb-396">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="6fceb-396">Click **Next**.</span></span>
      <span data-ttu-id="6fceb-397">![Skopiuj narzędzie — strona właściwości](./media/data-factory-azure-blob-connector/copy-tool-properties-page.png)</span><span class="sxs-lookup"><span data-stu-id="6fceb-397">![Copy Tool - Properties page](./media/data-factory-azure-blob-connector/copy-tool-properties-page.png)</span></span> 
3. <span data-ttu-id="6fceb-398">Na powitania **magazynu danych źródła** kliknij przycisk **magazyn obiektów Blob Azure** kafelka.</span><span class="sxs-lookup"><span data-stu-id="6fceb-398">On hello **Source data store** page, click **Azure Blob Storage** tile.</span></span> <span data-ttu-id="6fceb-399">Zadanie kopiowania hello są używane magazynu tej strony toospecify hello źródła danych.</span><span class="sxs-lookup"><span data-stu-id="6fceb-399">You use this page toospecify hello source data store for hello copy task.</span></span> <span data-ttu-id="6fceb-400">Możesz użyć istniejącej połączonej usługi magazynu danych lub określić nowy magazyn danych.</span><span class="sxs-lookup"><span data-stu-id="6fceb-400">You can use an existing data store linked service (or) specify a new data store.</span></span> <span data-ttu-id="6fceb-401">toouse istniejące połączone usługi, należy wybrać **z ISTNIEJĄCYMI usługami POŁĄCZONEGO** i wybierz hello prawo połączonej usługi.</span><span class="sxs-lookup"><span data-stu-id="6fceb-401">toouse an existing linked service, you would select **FROM EXISTING LINKED SERVICES** and select hello right linked service.</span></span> 
    <span data-ttu-id="6fceb-402">![Skopiuj narzędzie — strona Sklepu źródła danych](./media/data-factory-azure-blob-connector/copy-tool-source-data-store-page.png)</span><span class="sxs-lookup"><span data-stu-id="6fceb-402">![Copy Tool - Source data store page](./media/data-factory-azure-blob-connector/copy-tool-source-data-store-page.png)</span></span>
4. <span data-ttu-id="6fceb-403">Na powitania **Określ konto magazynu obiektów Blob platformy Azure hello** strony:</span><span class="sxs-lookup"><span data-stu-id="6fceb-403">On hello **Specify hello Azure Blob storage account** page:</span></span>
   1. <span data-ttu-id="6fceb-404">Zachowaj hello automatycznie generowanej nazwę **nazwa połączenia**.</span><span class="sxs-lookup"><span data-stu-id="6fceb-404">Keep hello auto-generated name for **Connection name**.</span></span> <span data-ttu-id="6fceb-405">Nazwa połączenia Hello jest hello hello połączone usługi typu: Magazyn Azure.</span><span class="sxs-lookup"><span data-stu-id="6fceb-405">hello connection name is hello name of hello linked service of type: Azure Storage.</span></span> 
   2. <span data-ttu-id="6fceb-406">Upewnij się, że wybrano opcję **Z subskrypcji Azure** dla ustawienia **Metoda wyboru konta**.</span><span class="sxs-lookup"><span data-stu-id="6fceb-406">Confirm that **From Azure subscriptions** option is selected for **Account selection method**.</span></span>
   3. <span data-ttu-id="6fceb-407">Wybierz subskrypcję platformy Azure lub pozostaw **Zaznacz wszystko** dla **subskrypcji platformy Azure**.</span><span class="sxs-lookup"><span data-stu-id="6fceb-407">Select your Azure subscription or keep **Select all** for **Azure subscription**.</span></span>   
   4. <span data-ttu-id="6fceb-408">Wybierz **konto magazynu Azure** z hello konta dostępne w ramach subskrypcji hello wybrane listy magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="6fceb-408">Select an **Azure storage account** from hello list of Azure storage accounts available in hello selected subscription.</span></span> <span data-ttu-id="6fceb-409">Możesz również tooenter ustawienia konta magazynu ręcznie, wybierając **ręcznie wprowadzić** opcję hello **konta metodę wyboru**.</span><span class="sxs-lookup"><span data-stu-id="6fceb-409">You can also choose tooenter storage account settings manually by selecting **Enter manually** option for hello **Account selection method**.</span></span>
   5. <span data-ttu-id="6fceb-410">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="6fceb-410">Click **Next**.</span></span> 
      <span data-ttu-id="6fceb-411">![Skopiuj narzędzie — Określ konto magazynu obiektów Blob platformy Azure hello](./media/data-factory-azure-blob-connector/copy-tool-specify-azure-blob-storage-account.png)</span><span class="sxs-lookup"><span data-stu-id="6fceb-411">![Copy Tool - Specify hello Azure Blob storage account](./media/data-factory-azure-blob-connector/copy-tool-specify-azure-blob-storage-account.png)</span></span>
5. <span data-ttu-id="6fceb-412">Na **wybierz hello wejściowy plik lub folder** strony:</span><span class="sxs-lookup"><span data-stu-id="6fceb-412">On **Choose hello input file or folder** page:</span></span>
   1. <span data-ttu-id="6fceb-413">Kliknij dwukrotnie **adfblobcontainer**.</span><span class="sxs-lookup"><span data-stu-id="6fceb-413">Double-click **adfblobcontainer**.</span></span>
   2. <span data-ttu-id="6fceb-414">Wybierz **wejściowych**i kliknij przycisk **wybierz**.</span><span class="sxs-lookup"><span data-stu-id="6fceb-414">Select **input**, and click **Choose**.</span></span> <span data-ttu-id="6fceb-415">W tym przewodniku wybierz opcję hello folder wejściowy.</span><span class="sxs-lookup"><span data-stu-id="6fceb-415">In this walkthrough, you select hello input folder.</span></span> <span data-ttu-id="6fceb-416">Hello emp.txt pliku można również wybrać w folderze hello zamiast tego.</span><span class="sxs-lookup"><span data-stu-id="6fceb-416">You could also select hello emp.txt file in hello folder instead.</span></span> 
      <span data-ttu-id="6fceb-417">![Skopiuj narzędzie — Wybierz hello wejściowego pliku lub folderu](./media/data-factory-azure-blob-connector/copy-tool-choose-input-file-or-folder.png)</span><span class="sxs-lookup"><span data-stu-id="6fceb-417">![Copy Tool - Choose hello input file or folder](./media/data-factory-azure-blob-connector/copy-tool-choose-input-file-or-folder.png)</span></span>
6. <span data-ttu-id="6fceb-418">Na powitania **wybierz hello wejściowy plik lub folder** strony:</span><span class="sxs-lookup"><span data-stu-id="6fceb-418">On hello **Choose hello input file or folder** page:</span></span>
    1. <span data-ttu-id="6fceb-419">Upewnij się, że hello **pliku lub folderu** ustawiono zbyt**adfblobconnector/wprowadzania**.</span><span class="sxs-lookup"><span data-stu-id="6fceb-419">Confirm that hello **file or folder** is set too**adfblobconnector/input**.</span></span> <span data-ttu-id="6fceb-420">W przypadku plików hello w podfolderach, na przykład 2017/04/01, 2017/04/02 i tak dalej, wprowadź adfblobconnector/danych wejściowych / {year} / {month} / {day} dla pliku lub folderu.</span><span class="sxs-lookup"><span data-stu-id="6fceb-420">If hello files are in sub folders, for example, 2017/04/01, 2017/04/02, and so on, enter adfblobconnector/input/{year}/{month}/{day} for file or folder.</span></span> <span data-ttu-id="6fceb-421">Po naciśnięciu klawisza TAB poza pole tekstowe hello, zobaczysz trzech formatów tooselect list rozwijanych roku (rrrr), miesiąc (MM) i dzień (dd).</span><span class="sxs-lookup"><span data-stu-id="6fceb-421">When you press TAB out of hello text box, you see three drop-down lists tooselect formats for year (yyyy), month (MM), and day (dd).</span></span> 
    2. <span data-ttu-id="6fceb-422">Nie ustawiaj **skopiuj plik rekursywnie**.</span><span class="sxs-lookup"><span data-stu-id="6fceb-422">Do not set **Copy file recursively**.</span></span> <span data-ttu-id="6fceb-423">Umożliwia wybranie tej opcji przechodzenia toorecursively za pomocą folderów dla miejsca docelowego skopiowanych toohello toobe plików.</span><span class="sxs-lookup"><span data-stu-id="6fceb-423">Select this option toorecursively traverse through folders for files toobe copied toohello destination.</span></span> 
    3. <span data-ttu-id="6fceb-424">Nie hello **binarne kopiowania** opcji.</span><span class="sxs-lookup"><span data-stu-id="6fceb-424">Do not hello **binary copy** option.</span></span> <span data-ttu-id="6fceb-425">Wybierz ten tooperform opcji kopię binarne docelowego toohello pliku źródłowego.</span><span class="sxs-lookup"><span data-stu-id="6fceb-425">Select this option tooperform a binary copy of source file toohello destination.</span></span> <span data-ttu-id="6fceb-426">Nie należy wybierać w ramach tego przewodnika, dzięki czemu można wyświetlić więcej opcji w kolejnych stronach hello.</span><span class="sxs-lookup"><span data-stu-id="6fceb-426">Do not select for this walkthrough so that you can see more options in hello next pages.</span></span> 
    4. <span data-ttu-id="6fceb-427">Upewnij się, że hello **typ kompresji** ustawiono zbyt**Brak**.</span><span class="sxs-lookup"><span data-stu-id="6fceb-427">Confirm that hello **Compression type** is set too**None**.</span></span> <span data-ttu-id="6fceb-428">Wybierz wartość dla tej opcji, jeśli plików źródłowych są kompresowane w jednym z formatów hello obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="6fceb-428">Select a value for this option if your source files are compressed in one of hello supported formats.</span></span> 
    5. <span data-ttu-id="6fceb-429">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="6fceb-429">Click **Next**.</span></span>
    <span data-ttu-id="6fceb-430">![Skopiuj narzędzie — Wybierz hello wejściowego pliku lub folderu](./media/data-factory-azure-blob-connector/chose-input-file-folder.png)</span><span class="sxs-lookup"><span data-stu-id="6fceb-430">![Copy Tool - Choose hello input file or folder](./media/data-factory-azure-blob-connector/chose-input-file-folder.png)</span></span> 
7. <span data-ttu-id="6fceb-431">Na powitania **ustawienia formatu pliku** strony, zobacz ograniczniki hello i hello schemat, który jest automatycznie wykrywane przez kreatora hello podczas analizowania pliku hello.</span><span class="sxs-lookup"><span data-stu-id="6fceb-431">On hello **File format settings** page, you see hello delimiters and hello schema that is auto-detected by hello wizard by parsing hello file.</span></span> 
    1. <span data-ttu-id="6fceb-432">Potwierdź hello następujące opcje:.</span><span class="sxs-lookup"><span data-stu-id="6fceb-432">Confirm hello following options: a.</span></span> <span data-ttu-id="6fceb-433">Witaj **format pliku** ustawiono zbyt**formacie tekstowym**.</span><span class="sxs-lookup"><span data-stu-id="6fceb-433">hello **file format** is set too**Text format**.</span></span> <span data-ttu-id="6fceb-434">Wszystkie formaty hello obsługiwane na liście rozwijanej hello jest widoczny.</span><span class="sxs-lookup"><span data-stu-id="6fceb-434">You can see all hello supported formats in hello drop-down list.</span></span> <span data-ttu-id="6fceb-435">Na przykład: JSON, Avro, ORC, Parquet.</span><span class="sxs-lookup"><span data-stu-id="6fceb-435">For example: JSON, Avro, ORC, Parquet.</span></span>
        <span data-ttu-id="6fceb-436">b.</span><span class="sxs-lookup"><span data-stu-id="6fceb-436">b.</span></span> <span data-ttu-id="6fceb-437">Witaj **ogranicznik kolumny** ustawiono zbyt`Comma (,)`.</span><span class="sxs-lookup"><span data-stu-id="6fceb-437">hello **column delimiter** is set too`Comma (,)`.</span></span> <span data-ttu-id="6fceb-438">Widać hello inne ograniczniki kolumny obsługiwane przez fabrykę danych na liście rozwijanej hello.</span><span class="sxs-lookup"><span data-stu-id="6fceb-438">You can see hello other column delimiters supported by Data Factory in hello drop-down list.</span></span> <span data-ttu-id="6fceb-439">Można również określić niestandardowe ogranicznika.</span><span class="sxs-lookup"><span data-stu-id="6fceb-439">You can also specify a custom delimiter.</span></span>
        <span data-ttu-id="6fceb-440">c.</span><span class="sxs-lookup"><span data-stu-id="6fceb-440">c.</span></span> <span data-ttu-id="6fceb-441">Witaj **ogranicznik wiersza** ustawiono zbyt`Carriage Return + Line feed (\r\n)`.</span><span class="sxs-lookup"><span data-stu-id="6fceb-441">hello **row delimiter** is set too`Carriage Return + Line feed (\r\n)`.</span></span> <span data-ttu-id="6fceb-442">Widać hello inne obsługiwane przez fabrykę danych na liście rozwijanej hello ograniczniki wiersza.</span><span class="sxs-lookup"><span data-stu-id="6fceb-442">You can see hello other row delimiters supported by Data Factory in hello drop-down list.</span></span> <span data-ttu-id="6fceb-443">Można również określić niestandardowe ogranicznika.</span><span class="sxs-lookup"><span data-stu-id="6fceb-443">You can also specify a custom delimiter.</span></span>
        <span data-ttu-id="6fceb-444">d.</span><span class="sxs-lookup"><span data-stu-id="6fceb-444">d.</span></span> <span data-ttu-id="6fceb-445">Witaj **pominąć licznik wierszy** ustawiono zbyt**0**.</span><span class="sxs-lookup"><span data-stu-id="6fceb-445">hello **skip line count** is set too**0**.</span></span> <span data-ttu-id="6fceb-446">Kilka toobe wiersze pominięto u góry hello hello pliku, wprowadź tutaj numer hello.</span><span class="sxs-lookup"><span data-stu-id="6fceb-446">If you want a few lines toobe skipped at hello top of hello file, enter hello number here.</span></span>
        <span data-ttu-id="6fceb-447">e.</span><span class="sxs-lookup"><span data-stu-id="6fceb-447">e.</span></span>  <span data-ttu-id="6fceb-448">Witaj **pierwszy wiersz danych zawiera nazwy kolumn** nie jest ustawiona.</span><span class="sxs-lookup"><span data-stu-id="6fceb-448">hello **first data row contains column names** is not set.</span></span> <span data-ttu-id="6fceb-449">Jeśli pliki źródłowe hello zawiera nazwy kolumn w pierwszym wierszu hello, wybierz tę opcję.</span><span class="sxs-lookup"><span data-stu-id="6fceb-449">If hello source files contain column names in hello first row, select this option.</span></span>
        <span data-ttu-id="6fceb-450">f.</span><span class="sxs-lookup"><span data-stu-id="6fceb-450">f.</span></span> <span data-ttu-id="6fceb-451">Witaj **wartość pusta kolumna jest traktowana jako null** opcja jest ustawiona.</span><span class="sxs-lookup"><span data-stu-id="6fceb-451">hello **treat empty column value as null** option is set.</span></span>
    2. <span data-ttu-id="6fceb-452">Rozwiń węzeł **Zaawansowane ustawienia** toosee zaawansowane możliwości.</span><span class="sxs-lookup"><span data-stu-id="6fceb-452">Expand **Advanced settings** toosee advanced option available.</span></span>
    3. <span data-ttu-id="6fceb-453">U dołu hello hello strony, zobacz hello **Podgląd** danych z pliku emp.txt hello.</span><span class="sxs-lookup"><span data-stu-id="6fceb-453">At hello bottom of hello page, see hello **preview** of data from hello emp.txt file.</span></span>
    4. <span data-ttu-id="6fceb-454">Kliknij przycisk **SCHEMATU** tab na powitania dolnej toosee hello schematu tego kreatora kopiowania hello wykryta przez hello dane w pliku źródłowym hello.</span><span class="sxs-lookup"><span data-stu-id="6fceb-454">Click **SCHEMA** tab at hello bottom toosee hello schema that hello copy wizard inferred by looking at hello data in hello source file.</span></span>
    5. <span data-ttu-id="6fceb-455">Kliknij przycisk **dalej** po Przejrzyj ograniczniki hello i wyświetlić podgląd danych.</span><span class="sxs-lookup"><span data-stu-id="6fceb-455">Click **Next** after you review hello delimiters and preview data.</span></span>
    <span data-ttu-id="6fceb-456">![Skopiuj narzędzie — Ustawienia format pliku](./media/data-factory-azure-blob-connector/copy-tool-file-format-settings.png)</span><span class="sxs-lookup"><span data-stu-id="6fceb-456">![Copy Tool - File format settings](./media/data-factory-azure-blob-connector/copy-tool-file-format-settings.png)</span></span>  
8. <span data-ttu-id="6fceb-457">Na powitania **magazyn danych docelowej strony**, wybierz pozycję **magazyn obiektów Blob Azure**i kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="6fceb-457">On hello **Destination data store page**, select **Azure Blob Storage**, and click **Next**.</span></span> <span data-ttu-id="6fceb-458">Używasz hello magazynu obiektów Blob Azure jako zarówno hello źródłowego i docelowego magazyny danych w ramach tego przewodnika.</span><span class="sxs-lookup"><span data-stu-id="6fceb-458">You are using hello Azure Blob Storage as both hello source and destination data stores in this walkthrough.</span></span>    
    <span data-ttu-id="6fceb-459">![Skopiuj narzędzie — Wybierz miejsce docelowe magazynu danych](media/data-factory-azure-blob-connector/select-destination-data-store.png)</span><span class="sxs-lookup"><span data-stu-id="6fceb-459">![Copy Tool - select destination data store](media/data-factory-azure-blob-connector/select-destination-data-store.png)</span></span>
9. <span data-ttu-id="6fceb-460">Na **Określ konto magazynu obiektów Blob platformy Azure hello** strony:</span><span class="sxs-lookup"><span data-stu-id="6fceb-460">On **Specify hello Azure Blob storage account** page:</span></span>
   1. <span data-ttu-id="6fceb-461">Wprowadź **AzureStorageLinkedService** dla hello **nazwa połączenia** pola.</span><span class="sxs-lookup"><span data-stu-id="6fceb-461">Enter **AzureStorageLinkedService** for hello **Connection name** field.</span></span>
   2. <span data-ttu-id="6fceb-462">Upewnij się, że wybrano opcję **Z subskrypcji Azure** dla ustawienia **Metoda wyboru konta**.</span><span class="sxs-lookup"><span data-stu-id="6fceb-462">Confirm that **From Azure subscriptions** option is selected for **Account selection method**.</span></span>
   3. <span data-ttu-id="6fceb-463">Wybierz swoją **subskrypcję** platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6fceb-463">Select your Azure **subscription**.</span></span>  
   4. <span data-ttu-id="6fceb-464">Wybierz konto magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6fceb-464">Select your Azure storage account.</span></span> 
   5. <span data-ttu-id="6fceb-465">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="6fceb-465">Click **Next**.</span></span>     
10. <span data-ttu-id="6fceb-466">Na powitania **hello wybierz wyjściowy plik lub folder** strony:</span><span class="sxs-lookup"><span data-stu-id="6fceb-466">On hello **Choose hello output file or folder** page:</span></span> 
    6. <span data-ttu-id="6fceb-467">Określ **ścieżka folderu** jako **adfblobconnector/wyjścia / {year} / {month} / {day}**.</span><span class="sxs-lookup"><span data-stu-id="6fceb-467">specify **Folder path** as **adfblobconnector/output/{year}/{month}/{day}**.</span></span> <span data-ttu-id="6fceb-468">Wprowadź **kartę**.</span><span class="sxs-lookup"><span data-stu-id="6fceb-468">Enter **TAB**.</span></span>
    7. <span data-ttu-id="6fceb-469">Dla hello **roku**, wybierz pozycję **rrrr**.</span><span class="sxs-lookup"><span data-stu-id="6fceb-469">For hello **year**, select **yyyy**.</span></span>
    8. <span data-ttu-id="6fceb-470">Dla hello **miesiąca**, upewnij się, że ustawiono zbyt**MM**.</span><span class="sxs-lookup"><span data-stu-id="6fceb-470">For hello **month**, confirm that it is set too**MM**.</span></span>
    9. <span data-ttu-id="6fceb-471">Dla hello **dzień**, upewnij się, że ustawiono zbyt**dd**.</span><span class="sxs-lookup"><span data-stu-id="6fceb-471">For hello **day**, confirm that it is set too**dd**.</span></span>
    10. <span data-ttu-id="6fceb-472">Upewnij się, że hello **typ kompresji** ustawiono zbyt**Brak**.</span><span class="sxs-lookup"><span data-stu-id="6fceb-472">Confirm that hello **compression type** is set too**None**.</span></span>
    11. <span data-ttu-id="6fceb-473">Upewnij się, że hello **skopiuj zachowanie** ustawiono zbyt**Scal pliki**.</span><span class="sxs-lookup"><span data-stu-id="6fceb-473">Confirm that hello **copy behavior** is set too**Merge files**.</span></span> <span data-ttu-id="6fceb-474">Jeśli hello produkt wyjściowy plik z powitalne tej samej nazwie już istnieje, hello nowej zawartości jest dodany toohello tego samego pliku na końcu hello.</span><span class="sxs-lookup"><span data-stu-id="6fceb-474">If hello output file with hello same name already exists, hello new content is added toohello same file at hello end.</span></span>
    12. <span data-ttu-id="6fceb-475">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="6fceb-475">Click **Next**.</span></span>
    <span data-ttu-id="6fceb-476">![Skopiuj narzędzie — Wybierz dane wyjściowe pliku lub folderu](media/data-factory-azure-blob-connector/choose-the-output-file-or-folder.png)</span><span class="sxs-lookup"><span data-stu-id="6fceb-476">![Copy Tool - Choose output file or folder](media/data-factory-azure-blob-connector/choose-the-output-file-or-folder.png)</span></span>
11. <span data-ttu-id="6fceb-477">Na powitania **ustawienia formatu pliku** strony, przejrzyj ustawienia hello, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="6fceb-477">On hello **File format settings** page, review hello settings, and click **Next**.</span></span> <span data-ttu-id="6fceb-478">Jednym z hello tutaj dodatkowe opcje jest tooadd pliku wyjściowego toohello nagłówka.</span><span class="sxs-lookup"><span data-stu-id="6fceb-478">One of hello additional options here is tooadd a header toohello output file.</span></span> <span data-ttu-id="6fceb-479">Jeśli wybierzesz tę opcję, z nazwami kolumn hello zostanie dodany wiersz nagłówka ze schematu hello hello źródła.</span><span class="sxs-lookup"><span data-stu-id="6fceb-479">If you select that option, a header row is added with names of hello columns from hello schema of hello source.</span></span> <span data-ttu-id="6fceb-480">Podczas wyświetlania hello schematu źródła hello można zmienić nazwy hello domyślne nazwy kolumn.</span><span class="sxs-lookup"><span data-stu-id="6fceb-480">You can rename hello default column names when viewing hello schema for hello source.</span></span> <span data-ttu-id="6fceb-481">Na przykład można zmienić hello pierwszej kolumny tooFirst nazwy i drugiej kolumny tooLast nazwy.</span><span class="sxs-lookup"><span data-stu-id="6fceb-481">For example, you could change hello first column tooFirst Name and second column tooLast Name.</span></span> <span data-ttu-id="6fceb-482">Następnie plik wyjściowy hello jest generowany przy użyciu nagłówka o tych nazwach jako nazwy kolumn.</span><span class="sxs-lookup"><span data-stu-id="6fceb-482">Then, hello output file is generated with a header with these names as column names.</span></span> 
    <span data-ttu-id="6fceb-483">![Skopiuj narzędzie — Ustawienia format pliku dla miejsca docelowego](media/data-factory-azure-blob-connector/file-format-destination.png)</span><span class="sxs-lookup"><span data-stu-id="6fceb-483">![Copy Tool - File format settings for destination](media/data-factory-azure-blob-connector/file-format-destination.png)</span></span>
12. <span data-ttu-id="6fceb-484">Na powitania **ustawienia wydajności** strony, upewnij się, że **chmury jednostki** i **równoległe kopie** są ustawiane za**automatycznie**i kliknij przycisk Dalej.</span><span class="sxs-lookup"><span data-stu-id="6fceb-484">On hello **Performance settings** page, confirm that **cloud units** and **parallel copies** are set too**Auto**, and click Next.</span></span> <span data-ttu-id="6fceb-485">Aby uzyskać więcej informacji o tych ustawieniach, zobacz [skopiuj wydajności działania i dostrajania przewodnik](data-factory-copy-activity-performance.md#parallel-copy).</span><span class="sxs-lookup"><span data-stu-id="6fceb-485">For details about these settings, see [Copy activity performance and tuning guide](data-factory-copy-activity-performance.md#parallel-copy).</span></span>
    <span data-ttu-id="6fceb-486">![Skopiuj narzędzie — Ustawienia wydajności](media/data-factory-azure-blob-connector/copy-performance-settings.png)</span><span class="sxs-lookup"><span data-stu-id="6fceb-486">![Copy Tool - Performance settings](media/data-factory-azure-blob-connector/copy-performance-settings.png)</span></span> 
14. <span data-ttu-id="6fceb-487">Na powitania **Podsumowanie** strony, przejrzyj wszystkie ustawienia (właściwości zadania, ustawienia źródłowe i docelowe i ustawień kopii), a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="6fceb-487">On hello **Summary** page, review all settings (task properties, settings for source and destination, and copy settings), and click **Next**.</span></span>
    <span data-ttu-id="6fceb-488">![Skopiuj narzędzie — strona podsumowania](media/data-factory-azure-blob-connector/copy-tool-summary-page.png)</span><span class="sxs-lookup"><span data-stu-id="6fceb-488">![Copy Tool - Summary page](media/data-factory-azure-blob-connector/copy-tool-summary-page.png)</span></span>
15. <span data-ttu-id="6fceb-489">Przejrzyj informacje w hello **Podsumowanie** , a następnie kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="6fceb-489">Review information in hello **Summary** page, and click **Finish**.</span></span> <span data-ttu-id="6fceb-490">Kreator Hello tworzy dwa połączone usługi, dwóch zestawów danych (dane wejściowe i wyjściowe) i jeden potok w fabryce danych hello (z którego uruchamiana jest hello kreatora kopiowania).</span><span class="sxs-lookup"><span data-stu-id="6fceb-490">hello wizard creates two linked services, two datasets (input and output), and one pipeline in hello data factory (from where you launched hello Copy Wizard).</span></span>
    <span data-ttu-id="6fceb-491">![Skopiuj narzędzie - stronę wdrożenia](media/data-factory-azure-blob-connector/copy-tool-deployment-page.png)</span><span class="sxs-lookup"><span data-stu-id="6fceb-491">![Copy Tool - Deployment page](media/data-factory-azure-blob-connector/copy-tool-deployment-page.png)</span></span>

### <a name="monitor-hello-pipeline-copy-task"></a><span data-ttu-id="6fceb-492">Monitor hello potoku (zadanie kopiowania)</span><span class="sxs-lookup"><span data-stu-id="6fceb-492">Monitor hello pipeline (copy task)</span></span>

1. <span data-ttu-id="6fceb-493">Kliknij łącze hello `Click here toomonitor copy pipeline` na powitania **wdrożenia** strony.</span><span class="sxs-lookup"><span data-stu-id="6fceb-493">Click hello link `Click here toomonitor copy pipeline` on hello **Deployment** page.</span></span> 
2. <span data-ttu-id="6fceb-494">Powinny pojawić się hello **monitorowanie i Zarządzanie aplikacją** w osobnej karcie.  ![Monitorowanie aplikacji i zarządzanie](media/data-factory-azure-blob-connector/monitor-manage-app.png)</span><span class="sxs-lookup"><span data-stu-id="6fceb-494">You should see hello **Monitor and Manage application** in a separate tab.  ![Monitor and Manage App](media/data-factory-azure-blob-connector/monitor-manage-app.png)</span></span>
3. <span data-ttu-id="6fceb-495">Hello zmiany **start** czasu u góry hello zbyt`04/19/2017` i **zakończenia** czasu zbyt`04/27/2017`, a następnie kliknij przycisk **Zastosuj**.</span><span class="sxs-lookup"><span data-stu-id="6fceb-495">Change hello **start** time at hello top too`04/19/2017` and **end** time too`04/27/2017`, and then click **Apply**.</span></span> 
4. <span data-ttu-id="6fceb-496">Powinny pojawić się pięć okien działania w hello **okien działania** listy.</span><span class="sxs-lookup"><span data-stu-id="6fceb-496">You should see five activity windows in hello **ACTIVITY WINDOWS** list.</span></span> <span data-ttu-id="6fceb-497">Witaj **WindowStart** razy powinna obejmować wszystkie dni od czasu zakończenia toopipeline potoku.</span><span class="sxs-lookup"><span data-stu-id="6fceb-497">hello **WindowStart** times should cover all days from pipeline start toopipeline end times.</span></span> 
5. <span data-ttu-id="6fceb-498">Kliknij przycisk **Odśwież** przycisk hello **okien działania** listy kilka razy, aż zostanie wyświetlony stan wszystkich okien działania hello hello ustawiono tooReady.</span><span class="sxs-lookup"><span data-stu-id="6fceb-498">Click **Refresh** button for hello **ACTIVITY WINDOWS** list a few times until you see hello status of all hello activity windows is set tooReady.</span></span> 
6. <span data-ttu-id="6fceb-499">Teraz Sprawdź, czy pliki wyjściowe hello są generowane w folderze wyjściowym hello adfblobconnector kontenera.</span><span class="sxs-lookup"><span data-stu-id="6fceb-499">Now, verify that hello output files are generated in hello output folder of adfblobconnector container.</span></span> <span data-ttu-id="6fceb-500">Powinny pojawić się następujące struktury folderów w folderze wyjściowym hello hello:</span><span class="sxs-lookup"><span data-stu-id="6fceb-500">You should see hello following folder structure in hello output folder:</span></span> 
    ```
    2017/04/21
    2017/04/22
    2017/04/23
    2017/04/24
    2017/04/25    
    ```
<span data-ttu-id="6fceb-501">Aby uzyskać szczegółowe informacje o monitorowaniu i zarządzaniu nimi fabryk danych, zobacz [monitora i zarządzanie nimi potoku fabryki danych](data-factory-monitor-manage-app.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="6fceb-501">For detailed information about monitoring and managing data factories, see [Monitor and manage Data Factory pipeline](data-factory-monitor-manage-app.md) article.</span></span> 
 
### <a name="data-factory-entities"></a><span data-ttu-id="6fceb-502">Obiekty fabryki danych</span><span class="sxs-lookup"><span data-stu-id="6fceb-502">Data Factory entities</span></span>
<span data-ttu-id="6fceb-503">Teraz Przełącz kartę toohello tylnej strony głównej hello fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="6fceb-503">Now, switch back toohello tab with hello Data Factory home page.</span></span> <span data-ttu-id="6fceb-504">Zwróć uwagę, że istnieją dwa połączone usługi, dwa zestawy danych i jeden potok w fabryce danych teraz.</span><span class="sxs-lookup"><span data-stu-id="6fceb-504">Notice that there are two linked services, two datasets, and one pipeline in your data factory now.</span></span> 

![Strona główna fabryka danych z jednostkami](media/data-factory-azure-blob-connector/data-factory-home-page-with-numbers.png)

<span data-ttu-id="6fceb-506">Kliknij przycisk **tworzenie i wdrażanie** toolaunch Edytor fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="6fceb-506">Click **Author and deploy** toolaunch Data Factory Editor.</span></span> 

![Edytor fabryki danych](media/data-factory-azure-blob-connector/data-factory-editor.png)

<span data-ttu-id="6fceb-508">Powinny pojawić się powitania po jednostek fabryki danych w fabryce danych:</span><span class="sxs-lookup"><span data-stu-id="6fceb-508">You should see hello following Data Factory entities in your data factory:</span></span> 

 - <span data-ttu-id="6fceb-509">Dwa połączone usługi.</span><span class="sxs-lookup"><span data-stu-id="6fceb-509">Two linked services.</span></span> <span data-ttu-id="6fceb-510">Jeden hello źródła i hello innego hello docelowym.</span><span class="sxs-lookup"><span data-stu-id="6fceb-510">One for hello source and hello other one for hello destination.</span></span> <span data-ttu-id="6fceb-511">Obie te usługi hello połączone można znaleźć toohello tego samego konta magazynu Azure w ramach tego przewodnika.</span><span class="sxs-lookup"><span data-stu-id="6fceb-511">Both hello linked services refer toohello same Azure Storage account in this walkthrough.</span></span> 
 - <span data-ttu-id="6fceb-512">Dwa zestawy danych.</span><span class="sxs-lookup"><span data-stu-id="6fceb-512">Two datasets.</span></span> <span data-ttu-id="6fceb-513">Zestaw wejściowy i wyjściowy zestaw danych.</span><span class="sxs-lookup"><span data-stu-id="6fceb-513">An input dataset and an output dataset.</span></span> <span data-ttu-id="6fceb-514">W tym przewodniku, to oba rozwiązania używają hello sam kontenera obiektów blob, ale odwołuje się foldery toodifferent (dane wejściowe i wyjściowe).</span><span class="sxs-lookup"><span data-stu-id="6fceb-514">In this walkthrough, both use hello same blob container but refer toodifferent folders (input and output).</span></span>
 - <span data-ttu-id="6fceb-515">Potok.</span><span class="sxs-lookup"><span data-stu-id="6fceb-515">A pipeline.</span></span> <span data-ttu-id="6fceb-516">potok Hello zawiera działanie kopiowania, który używa źródła obiektów blob i danych obiektów blob zbiornika toocopy z tooanother obiektów blob platformy Azure w lokalizacji lokalizacji obiektu blob systemu Azure.</span><span class="sxs-lookup"><span data-stu-id="6fceb-516">hello pipeline contains a copy activity that uses a blob source and a blob sink toocopy data from an Azure blob location tooanother Azure blob location.</span></span> 

<span data-ttu-id="6fceb-517">Witaj poniższe sekcje zawierają więcej informacji na temat tych jednostek.</span><span class="sxs-lookup"><span data-stu-id="6fceb-517">hello following sections provide more information about these entities.</span></span> 

#### <a name="linked-services"></a><span data-ttu-id="6fceb-518">Połączone usługi</span><span class="sxs-lookup"><span data-stu-id="6fceb-518">Linked services</span></span>
<span data-ttu-id="6fceb-519">Powinny pojawić się dwa połączonych usług.</span><span class="sxs-lookup"><span data-stu-id="6fceb-519">You should see two linked services.</span></span> <span data-ttu-id="6fceb-520">Jeden hello źródła i hello innego hello docelowym.</span><span class="sxs-lookup"><span data-stu-id="6fceb-520">One for hello source and hello other one for hello destination.</span></span> <span data-ttu-id="6fceb-521">W tym przewodniku zarówno wyglądu definicje hello same z wyjątkiem hello nazwy.</span><span class="sxs-lookup"><span data-stu-id="6fceb-521">In this walkthrough, both definitions look hello same except for hello names.</span></span> <span data-ttu-id="6fceb-522">Witaj **typu** hello połączonej usługi jest ustawiony za**AzureStorage**.</span><span class="sxs-lookup"><span data-stu-id="6fceb-522">hello **type** of hello linked service is set too**AzureStorage**.</span></span> <span data-ttu-id="6fceb-523">Najważniejsze właściwości definicji usługi hello połączony jest hello **connectionString**, który jest używany przez fabryki danych tooconnect tooyour konta magazynu Azure w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="6fceb-523">Most important property of hello linked service definition is hello **connectionString**, which is used by Data Factory tooconnect tooyour Azure Storage account at runtime.</span></span> <span data-ttu-id="6fceb-524">Ignoruj hello hubName właściwości w definicji hello.</span><span class="sxs-lookup"><span data-stu-id="6fceb-524">Ignore hello hubName property in hello definition.</span></span> 

##### <a name="source-blob-storage-linked-service"></a><span data-ttu-id="6fceb-525">Źródła obiektów blob połączoną usługą magazynu</span><span class="sxs-lookup"><span data-stu-id="6fceb-525">Source blob storage linked service</span></span>
```json
{
    "name": "Source-BlobStorage-z4y",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=mystorageaccount;AccountKey=**********"
        }
    }
}
```

##### <a name="destination-blob-storage-linked-service"></a><span data-ttu-id="6fceb-526">Docelowy obiekt blob połączoną usługą magazynu</span><span class="sxs-lookup"><span data-stu-id="6fceb-526">Destination blob storage linked service</span></span>

```json
{
    "name": "Destination-BlobStorage-z4y",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=mystorageaccount;AccountKey=**********"
        }
    }
}
```

<span data-ttu-id="6fceb-527">Aby uzyskać więcej informacji na temat połączoną usługą magazynu Azure, zobacz [połączona usługa właściwości](#linked-service-properties) sekcji.</span><span class="sxs-lookup"><span data-stu-id="6fceb-527">For more information about Azure Storage linked service, see [Linked service properties](#linked-service-properties) section.</span></span> 

#### <a name="datasets"></a><span data-ttu-id="6fceb-528">Zestawy danych</span><span class="sxs-lookup"><span data-stu-id="6fceb-528">Datasets</span></span>
<span data-ttu-id="6fceb-529">Istnieją dwa zestawy danych: zestaw wejściowy i wyjściowy zestaw danych.</span><span class="sxs-lookup"><span data-stu-id="6fceb-529">There are two datasets: an input dataset and an output dataset.</span></span> <span data-ttu-id="6fceb-530">Typ Hello hello dataset jest ustawiona zbyt**AzureBlob** dla obu.</span><span class="sxs-lookup"><span data-stu-id="6fceb-530">hello type of hello dataset is set too**AzureBlob** for both.</span></span> 

<span data-ttu-id="6fceb-531">zestaw danych wejściowych Hello punktów toohello **wejściowych** folderu hello **adfblobconnector** kontenera obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="6fceb-531">hello input dataset points toohello **input** folder of hello **adfblobconnector** blob container.</span></span> <span data-ttu-id="6fceb-532">Witaj **zewnętrznych** właściwość jest ustawiona zbyt**true** dla tego zestawu danych jako hello danych nie został przedstawiony przez potok hello z działanie kopiowania hello, który przyjmuje tego zestawu danych jako dane wejściowe.</span><span class="sxs-lookup"><span data-stu-id="6fceb-532">hello **external** property is set too**true** for this dataset as hello data is not produced by hello pipeline with hello copy activity that takes this dataset as an input.</span></span> 

<span data-ttu-id="6fceb-533">Witaj wyjściowego zestawu danych punktów toohello **dane wyjściowe** folderu hello tego samego kontenera obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="6fceb-533">hello output dataset points toohello **output** folder of hello same blob container.</span></span> <span data-ttu-id="6fceb-534">Witaj wyjściowy zestaw danych używa również hello rok, miesiąc i dzień hello **SliceStart** toodynamically zmiennej systemu obliczyć hello ścieżki do pliku wyjściowego hello.</span><span class="sxs-lookup"><span data-stu-id="6fceb-534">hello output dataset also uses hello year, month, and day of hello **SliceStart** system variable toodynamically evaluate hello path for hello output file.</span></span> <span data-ttu-id="6fceb-535">Listę funkcje i zmienne systemu obsługiwane przez fabrykę danych, zobacz [funkcje fabryki danych i zmienne systemu](data-factory-functions-variables.md).</span><span class="sxs-lookup"><span data-stu-id="6fceb-535">For a list of functions and system variables supported by Data Factory, see [Data Factory functions and system variables](data-factory-functions-variables.md).</span></span> <span data-ttu-id="6fceb-536">Witaj **zewnętrznych** właściwość jest ustawiona zbyt**false** (wartość domyślna), ponieważ ten zestaw danych jest generowany przez potok hello.</span><span class="sxs-lookup"><span data-stu-id="6fceb-536">hello **external** property is set too**false** (default value) because this dataset is produced by hello pipeline.</span></span> 

<span data-ttu-id="6fceb-537">Aby uzyskać więcej informacji na temat właściwości obsługiwanych przez zestaw danych obiektów Blob platformy Azure, zobacz [właściwości zestawu danych](#dataset-properties) sekcji.</span><span class="sxs-lookup"><span data-stu-id="6fceb-537">For more information about properties supported by Azure Blob dataset, see [Dataset properties](#dataset-properties) section.</span></span>

##### <a name="input-dataset"></a><span data-ttu-id="6fceb-538">Wejściowy zestaw danych</span><span class="sxs-lookup"><span data-stu-id="6fceb-538">Input dataset</span></span>

```json
{
    "name": "InputDataset-z4y",
    "properties": {
        "structure": [
            { "name": "Prop_0", "type": "String" },
            { "name": "Prop_1", "type": "String" }
        ],
        "type": "AzureBlob",
        "linkedServiceName": "Source-BlobStorage-z4y",
        "typeProperties": {
            "folderPath": "adfblobconnector/input/",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Day",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
```

##### <a name="output-dataset"></a><span data-ttu-id="6fceb-539">Wyjściowy zestaw danych</span><span class="sxs-lookup"><span data-stu-id="6fceb-539">Output dataset</span></span>

```json
{
    "name": "OutputDataset-z4y",
    "properties": {
        "structure": [
            { "name": "Prop_0", "type": "String" },
            { "name": "Prop_1", "type": "String" }
        ],
        "type": "AzureBlob",
        "linkedServiceName": "Destination-BlobStorage-z4y",
        "typeProperties": {
            "folderPath": "adfblobconnector/output/{year}/{month}/{day}",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            },
            "partitionedBy": [
                { "name": "year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
                { "name": "month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
                { "name": "day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } }
            ]
        },
        "availability": {
            "frequency": "Day",
            "interval": 1
        },
        "external": false,
        "policy": {}
    }
}
```

#### <a name="pipeline"></a><span data-ttu-id="6fceb-540">Potok</span><span class="sxs-lookup"><span data-stu-id="6fceb-540">Pipeline</span></span>
<span data-ttu-id="6fceb-541">potok Hello jest tylko jedno działanie.</span><span class="sxs-lookup"><span data-stu-id="6fceb-541">hello pipeline has just one activity.</span></span> <span data-ttu-id="6fceb-542">Witaj **typu** hello działania jest ustawiony za**kopiowania**.</span><span class="sxs-lookup"><span data-stu-id="6fceb-542">hello **type** of hello activity is set too**Copy**.</span></span>  <span data-ttu-id="6fceb-543">Właściwości typu hello hello działania istnieją dwie sekcje, jeden dla źródła i hello drugi dla obiekt sink.</span><span class="sxs-lookup"><span data-stu-id="6fceb-543">In hello type properties for hello activity, there are two sections, one for source and hello other one for sink.</span></span> <span data-ttu-id="6fceb-544">Typ źródła Hello ustawiono zbyt**BlobSource** jako działania hello jest kopiowanie danych z magazynu obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="6fceb-544">hello source type is set too**BlobSource** as hello activity is copying data from a blob storage.</span></span> <span data-ttu-id="6fceb-545">Witaj typ ujścia ustawiono zbyt**BlobSink** jako działania hello kopiowanie magazynu obiektów blob tooa danych.</span><span class="sxs-lookup"><span data-stu-id="6fceb-545">hello sink type is set too**BlobSink** as hello activity copying data tooa blob storage.</span></span> <span data-ttu-id="6fceb-546">działanie kopiowania Hello przyjmuje InputDataset z4y jako dane wejściowe hello i OutputDataset-z4y jako dane wyjściowe hello.</span><span class="sxs-lookup"><span data-stu-id="6fceb-546">hello copy activity takes InputDataset-z4y as hello input and OutputDataset-z4y as hello output.</span></span> 

<span data-ttu-id="6fceb-547">Aby uzyskać więcej informacji o obsługiwanych przez BlobSource i BlobSink właściwości, zobacz [skopiować właściwości działania](#copy-activity-properties) sekcji.</span><span class="sxs-lookup"><span data-stu-id="6fceb-547">For more information about properties supported by BlobSource and BlobSink, see [Copy activity properties](#copy-activity-properties) section.</span></span> 

```json
{
    "name": "CopyPipeline",
    "properties": {
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource",
                        "recursive": false
                    },
                    "sink": {
                        "type": "BlobSink",
                        "copyBehavior": "MergeFiles",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "InputDataset-z4y"
                    }
                ],
                "outputs": [
                    {
                        "name": "OutputDataset-z4y"
                    }
                ],
                "policy": {
                    "timeout": "1.00:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "style": "StartOfInterval",
                    "retry": 3,
                    "longRetry": 0,
                    "longRetryInterval": "00:00:00"
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "Activity-0-Blob path_ adfblobconnector_input_->OutputDataset-z4y"
            }
        ],
        "start": "2017-04-21T22:34:00Z",
        "end": "2017-04-25T05:00:00Z",
        "isPaused": false,
        "pipelineMode": "Scheduled"
    }
}
```

## <a name="json-examples-for-copying-data-tooand-from-blob-storage"></a><span data-ttu-id="6fceb-548">Przykłady JSON do kopiowania tooand danych z magazynu obiektów Blob</span><span class="sxs-lookup"><span data-stu-id="6fceb-548">JSON examples for copying data tooand from Blob Storage</span></span>  
<span data-ttu-id="6fceb-549">Witaj poniższe przykłady zapewniają definicje JSON przy użyciu można toocreate potoku [portalu Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) lub [programu Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) lub [programu Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="6fceb-549">hello following examples provide sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="6fceb-550">Przedstawiają sposób toocopy tooand danych z magazynu obiektów Blob Azure i bazy danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="6fceb-550">They show how toocopy data tooand from Azure Blob Storage and Azure SQL Database.</span></span> <span data-ttu-id="6fceb-551">Jednak dane mogą być kopiowane **bezpośrednio** z dowolnego źródła tooany z wychwytywanie hello wyrażony w [tutaj](data-factory-data-movement-activities.md#supported-data-stores-and-formats) przy użyciu hello działanie kopiowania w fabryce danych Azure.</span><span class="sxs-lookup"><span data-stu-id="6fceb-551">However, data can be copied **directly** from any of sources tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>

### <a name="json-example-copy-data-from-blob-storage-toosql-database"></a><span data-ttu-id="6fceb-552">Przykład JSON: Kopiowanie danych z magazynu obiektów Blob tooSQL bazy danych</span><span class="sxs-lookup"><span data-stu-id="6fceb-552">JSON Example: Copy data from Blob Storage tooSQL Database</span></span>
<span data-ttu-id="6fceb-553">następujące przykładowe pokazuje Hello:</span><span class="sxs-lookup"><span data-stu-id="6fceb-553">hello following sample shows:</span></span>

1. <span data-ttu-id="6fceb-554">Połączonej usługi typu [AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="6fceb-554">A linked service of type [AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="6fceb-555">Połączonej usługi typu [AzureStorage](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="6fceb-555">A linked service of type [AzureStorage](#linked-service-properties).</span></span>
3. <span data-ttu-id="6fceb-556">Dane wejściowe [dataset](data-factory-create-datasets.md) typu [AzureBlob](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="6fceb-556">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](#dataset-properties).</span></span>
4. <span data-ttu-id="6fceb-557">Dane wyjściowe [dataset](data-factory-create-datasets.md) typu [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="6fceb-557">An output [dataset](data-factory-create-datasets.md) of type [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="6fceb-558">A [potoku](data-factory-create-pipelines.md) z działania kopiowania, która używa [BlobSource](#copy-activity-properties) i [SqlSink](data-factory-azure-sql-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="6fceb-558">A [pipeline](data-factory-create-pipelines.md) with a Copy activity that uses [BlobSource](#copy-activity-properties) and [SqlSink](data-factory-azure-sql-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="6fceb-559">Przykładowe Hello kopiuje dane szeregów czasowych co godzinę z tabeli Azure SQL tooan obiektów blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6fceb-559">hello sample copies time-series data from an Azure blob tooan Azure SQL table hourly.</span></span> <span data-ttu-id="6fceb-560">właściwości JSON Hello używane w te przykłady są opisane w sekcjach poniżej hello próbek.</span><span class="sxs-lookup"><span data-stu-id="6fceb-560">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="6fceb-561">**Azure połączoną usługą SQL:**</span><span class="sxs-lookup"><span data-stu-id="6fceb-561">**Azure SQL linked service:**</span></span>

```json
{
  "name": "AzureSqlLinkedService",
  "properties": {
    "type": "AzureSqlDatabase",
    "typeProperties": {
      "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
    }
  }
}
```
<span data-ttu-id="6fceb-562">**Połączonej usługi magazynu Azure:**</span><span class="sxs-lookup"><span data-stu-id="6fceb-562">**Azure Storage linked service:**</span></span>

```json
{
  "name": "StorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```
<span data-ttu-id="6fceb-563">Fabryka danych Azure obsługuje dwa typy usług magazynu Azure połączony: **AzureStorage** i **element AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="6fceb-563">Azure Data Factory supports two types of Azure Storage linked services: **AzureStorage** and **AzureStorageSas**.</span></span> <span data-ttu-id="6fceb-564">Dla hello pierwszego z nich, określ ciąg połączenia hello, który zawiera klucz konta hello i dla hello późniejszą, należy określić hello Uri dostępu sygnatury dostępu Współdzielonego.</span><span class="sxs-lookup"><span data-stu-id="6fceb-564">For hello first one, you specify hello connection string that includes hello account key and for hello later one, you specify hello Shared Access Signature (SAS) Uri.</span></span> <span data-ttu-id="6fceb-565">Zobacz [połączonych usług](#linked-service-properties) sekcji, aby uzyskać szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="6fceb-565">See [Linked Services](#linked-service-properties) section for details.</span></span>  

<span data-ttu-id="6fceb-566">**Azure wejściowego zestawu danych obiektów Blob:**</span><span class="sxs-lookup"><span data-stu-id="6fceb-566">**Azure Blob input dataset:**</span></span>

<span data-ttu-id="6fceb-567">Dane są pobierane z nowego obiektu blob co godzinę (częstotliwość: godziny, interwał: 1).</span><span class="sxs-lookup"><span data-stu-id="6fceb-567">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="6fceb-568">Witaj folderu ścieżkę i nazwę pliku dla obiekt blob hello dynamicznie są oceniane na podstawie czasu rozpoczęcia hello hello wycinek, który jest przetwarzana.</span><span class="sxs-lookup"><span data-stu-id="6fceb-568">hello folder path and file name for hello blob are dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="6fceb-569">Ścieżka folderu Hello korzysta rok, miesiąc i dzień część czas rozpoczęcia hello, a nazwa pliku hello część hello czas rozpoczęcia.</span><span class="sxs-lookup"><span data-stu-id="6fceb-569">hello folder path uses year, month, and day part of hello start time and file name uses hello hour part of hello start time.</span></span> <span data-ttu-id="6fceb-570">"external": "prawda" ustawienie informuje fabryki danych tabeli hello zewnętrznych toohello fabryki danych i nie jest generowany przez działanie w fabryce danych hello.</span><span class="sxs-lookup"><span data-stu-id="6fceb-570">“external”: “true” setting informs Data Factory that hello table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```json
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/",
      "fileName": "{Hour}.csv",
      "partitionedBy": [
        { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
        { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
        { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
        { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "HH" } }
      ],
      "format": {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "rowDelimiter": "\n"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    },
    "policy": {
      "externalData": {
        "retryInterval": "00:01:00",
        "retryTimeout": "00:10:00",
        "maximumRetry": 3
      }
    }
  }
}
```
<span data-ttu-id="6fceb-571">**Azure SQL wyjściowy zestaw danych:**</span><span class="sxs-lookup"><span data-stu-id="6fceb-571">**Azure SQL output dataset:**</span></span>

<span data-ttu-id="6fceb-572">przykład Witaj kopiuje tabeli tooa danych o nazwie "MyTable" w bazie danych Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="6fceb-572">hello sample copies data tooa table named “MyTable” in an Azure SQL database.</span></span> <span data-ttu-id="6fceb-573">Utwórz tabelę hello w bazie danych Azure SQL z hello taką samą liczbę kolumn, zgodnie z oczekiwaniami toocontain pliku Blob CSV hello.</span><span class="sxs-lookup"><span data-stu-id="6fceb-573">Create hello table in your Azure SQL database with hello same number of columns as you expect hello Blob CSV file toocontain.</span></span> <span data-ttu-id="6fceb-574">Dodawaniu nowych wierszy tabeli toohello co godzinę.</span><span class="sxs-lookup"><span data-stu-id="6fceb-574">New rows are added toohello table every hour.</span></span>

```json
{
  "name": "AzureSqlOutput",
  "properties": {
    "type": "AzureSqlTable",
    "linkedServiceName": "AzureSqlLinkedService",
    "typeProperties": {
      "tableName": "MyOutputTable"
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```
<span data-ttu-id="6fceb-575">**Działanie kopiowania w potoku z obiektu Blob, źródłowy i odbiorczy SQL:**</span><span class="sxs-lookup"><span data-stu-id="6fceb-575">**A copy activity in a pipeline with Blob source and SQL sink:**</span></span>

<span data-ttu-id="6fceb-576">Witaj potoku zawiera działanie kopiowania, który jest skonfigurowany toouse hello wejściowych i wyjściowych zestawów danych i jest toorun zaplanowane co godzinę.</span><span class="sxs-lookup"><span data-stu-id="6fceb-576">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="6fceb-577">W potoku hello definicji JSON, hello **źródła** typu ustawiono zbyt**BlobSource** i **zbiornika** typu ustawiono zbyt**SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="6fceb-577">In hello pipeline JSON definition, hello **source** type is set too**BlobSource** and **sink** type is set too**SqlSink**.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "AzureBlobtoSQL",
        "description": "Copy Activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureBlobInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureSqlOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource"
          },
          "sink": {
            "type": "SqlSink"
          }
        },
       "scheduler": {
          "frequency": "Hour",
          "interval": 1
        },
        "policy": {
          "concurrency": 1,
          "executionPriorityOrder": "OldestFirst",
          "retry": 0,
          "timeout": "01:00:00"
        }
      }
      ]
   }
}
```
### <a name="json-example-copy-data-from-azure-sql-tooazure-blob"></a><span data-ttu-id="6fceb-578">Przykład JSON: Kopiowanie danych z tooAzure Azure SQL Blob</span><span class="sxs-lookup"><span data-stu-id="6fceb-578">JSON Example: Copy data from Azure SQL tooAzure Blob</span></span>
<span data-ttu-id="6fceb-579">następujące przykładowe pokazuje Hello:</span><span class="sxs-lookup"><span data-stu-id="6fceb-579">hello following sample shows:</span></span>

1. <span data-ttu-id="6fceb-580">Połączonej usługi typu [AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="6fceb-580">A linked service of type [AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="6fceb-581">Połączonej usługi typu [AzureStorage](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="6fceb-581">A linked service of type [AzureStorage](#linked-service-properties).</span></span>
3. <span data-ttu-id="6fceb-582">Dane wejściowe [dataset](data-factory-create-datasets.md) typu [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="6fceb-582">An input [dataset](data-factory-create-datasets.md) of type [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="6fceb-583">Dane wyjściowe [dataset](data-factory-create-datasets.md) typu [AzureBlob](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="6fceb-583">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](#dataset-properties).</span></span>
5. <span data-ttu-id="6fceb-584">A [potoku](data-factory-create-pipelines.md) z działaniem kopii, która używa [SqlSource](data-factory-azure-sql-connector.md#copy-activity-properties) i [BlobSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="6fceb-584">A [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [SqlSource](data-factory-azure-sql-connector.md#copy-activity-properties) and [BlobSink](#copy-activity-properties).</span></span>

<span data-ttu-id="6fceb-585">Przykładowe Hello kopiuje dane szeregów czasowych co godzinę z tooan tabeli Azure SQL obiektów blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6fceb-585">hello sample copies time-series data from an Azure SQL table tooan Azure blob hourly.</span></span> <span data-ttu-id="6fceb-586">właściwości JSON Hello używane w te przykłady są opisane w sekcjach poniżej hello próbek.</span><span class="sxs-lookup"><span data-stu-id="6fceb-586">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="6fceb-587">**Azure połączoną usługą SQL:**</span><span class="sxs-lookup"><span data-stu-id="6fceb-587">**Azure SQL linked service:**</span></span>

```json
{
  "name": "AzureSqlLinkedService",
  "properties": {
    "type": "AzureSqlDatabase",
    "typeProperties": {
      "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
    }
  }
}
```
<span data-ttu-id="6fceb-588">**Połączonej usługi magazynu Azure:**</span><span class="sxs-lookup"><span data-stu-id="6fceb-588">**Azure Storage linked service:**</span></span>

```json
{
  "name": "StorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```
<span data-ttu-id="6fceb-589">Fabryka danych Azure obsługuje dwa typy usług magazynu Azure połączony: **AzureStorage** i **element AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="6fceb-589">Azure Data Factory supports two types of Azure Storage linked services: **AzureStorage** and **AzureStorageSas**.</span></span> <span data-ttu-id="6fceb-590">Dla hello pierwszego z nich, określ ciąg połączenia hello, który zawiera klucz konta hello i dla hello późniejszą, należy określić hello Uri dostępu sygnatury dostępu Współdzielonego.</span><span class="sxs-lookup"><span data-stu-id="6fceb-590">For hello first one, you specify hello connection string that includes hello account key and for hello later one, you specify hello Shared Access Signature (SAS) Uri.</span></span> <span data-ttu-id="6fceb-591">Zobacz [połączonych usług](#linked-service-properties) sekcji, aby uzyskać szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="6fceb-591">See [Linked Services](#linked-service-properties) section for details.</span></span>  

<span data-ttu-id="6fceb-592">**Azure SQL wejściowy zestaw danych:**</span><span class="sxs-lookup"><span data-stu-id="6fceb-592">**Azure SQL input dataset:**</span></span>

<span data-ttu-id="6fceb-593">przykład Witaj przyjęto założenie, utworzysz tabelę "MyTable" Azure SQL i zawiera kolumnę o nazwie "timestampcolumn" dla czasu serii danych.</span><span class="sxs-lookup"><span data-stu-id="6fceb-593">hello sample assumes you have created a table “MyTable” in Azure SQL and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="6fceb-594">Ustawienie "external": "prawda" informuje usługi fabryka danych tej tabeli hello zewnętrznych toohello fabryki danych i nie jest generowany przez działanie w fabryce danych hello.</span><span class="sxs-lookup"><span data-stu-id="6fceb-594">Setting “external”: ”true” informs Data Factory service that hello table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```json
{
  "name": "AzureSqlInput",
  "properties": {
    "type": "AzureSqlTable",
    "linkedServiceName": "AzureSqlLinkedService",
    "typeProperties": {
      "tableName": "MyTable"
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    },
    "policy": {
      "externalData": {
        "retryInterval": "00:01:00",
        "retryTimeout": "00:10:00",
        "maximumRetry": 3
      }
    }
  }
}
```

<span data-ttu-id="6fceb-595">**Azure Blob wyjściowy zestaw danych:**</span><span class="sxs-lookup"><span data-stu-id="6fceb-595">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="6fceb-596">Dane są zapisywane tooa nowych obiektów blob, co godzinę (częstotliwość: godziny, interwał: 1).</span><span class="sxs-lookup"><span data-stu-id="6fceb-596">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="6fceb-597">Ścieżka folderu Hello hello obiektu blob dynamicznie jest obliczane na podstawie czasu rozpoczęcia hello hello wycinek, który jest przetwarzana.</span><span class="sxs-lookup"><span data-stu-id="6fceb-597">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="6fceb-598">Ścieżka folderu Hello używa rok, miesiąc, dzień i godziny części hello czas rozpoczęcia.</span><span class="sxs-lookup"><span data-stu-id="6fceb-598">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

```json
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}/",
      "partitionedBy": [
        {
          "name": "Year",
          "value": { "type": "DateTime",  "date": "SliceStart", "format": "yyyy" } },
        { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
        { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
        { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "HH" } }
      ],
      "format": {
        "type": "TextFormat",
        "columnDelimiter": "\t",
        "rowDelimiter": "\n"
      }
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

<span data-ttu-id="6fceb-599">**Działanie kopiowania w potoku z SQL źródłowy i odbiorczy obiektów Blob:**</span><span class="sxs-lookup"><span data-stu-id="6fceb-599">**A copy activity in a pipeline with SQL source and Blob sink:**</span></span>

<span data-ttu-id="6fceb-600">Witaj potoku zawiera działanie kopiowania, który jest skonfigurowany toouse hello wejściowych i wyjściowych zestawów danych i jest toorun zaplanowane co godzinę.</span><span class="sxs-lookup"><span data-stu-id="6fceb-600">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="6fceb-601">W potoku hello definicji JSON, hello **źródła** typu ustawiono zbyt**SqlSource** i **zbiornika** typu ustawiono zbyt**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="6fceb-601">In hello pipeline JSON definition, hello **source** type is set too**SqlSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="6fceb-602">Zapytanie SQL Hello określone dla hello **SqlReaderQuery** właściwości zaznacza danych hello hello poza toocopy godzinę.</span><span class="sxs-lookup"><span data-stu-id="6fceb-602">hello SQL query specified for hello **SqlReaderQuery** property selects hello data in hello past hour toocopy.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-01T19:00:00",
        "description":"pipeline for copy activity",
        "activities":[  
              {
                "name": "AzureSQLtoBlob",
                "description": "copy activity",
                "type": "Copy",
                "inputs": [
                  {
                    "name": "AzureSQLInput"
                  }
                ],
                "outputs": [
                  {
                    "name": "AzureBlobOutput"
                  }
                ],
                "typeProperties": {
                    "source": {
                        "type": "SqlSource",
                        "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                      },
                      "sink": {
                        "type": "BlobSink"
                      }
                },
                   "scheduler": {
                      "frequency": "Hour",
                      "interval": 1
                },
                "policy": {
                      "concurrency": 1,
                      "executionPriorityOrder": "OldestFirst",
                      "retry": 0,
                      "timeout": "01:00:00"
                }
              }
         ]
    }
}
```

> [!NOTE]
> <span data-ttu-id="6fceb-603">toomap kolumny źródłowej toocolumns zestawu danych z obiektu sink zestawu danych, zobacz [mapowania kolumnach dataset w fabryce danych Azure](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="6fceb-603">toomap columns from source dataset toocolumns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="6fceb-604">Wydajność i dostrajania</span><span class="sxs-lookup"><span data-stu-id="6fceb-604">Performance and Tuning</span></span>
<span data-ttu-id="6fceb-605">Zobacz [wydajności działania kopiowania & dostrajanie przewodnik](data-factory-copy-activity-performance.md) toolearn o kluczu czynniki tego wydajność wpływ przenoszenia danych (działanie kopiowania) w usłudze fabryka danych Azure i różne sposoby toooptimize go.</span><span class="sxs-lookup"><span data-stu-id="6fceb-605">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
