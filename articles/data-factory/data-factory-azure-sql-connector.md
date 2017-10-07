---
title: aaaCopy danych do/z bazy danych SQL Azure | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toocopy danych do/z bazy danych SQL Azure przy użyciu fabryki danych Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 484f735b-8464-40ba-a9fc-820e6553159e
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: d2ff16191afb028da75699c5e4d0bb310538db0f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tooand-from-azure-sql-database-using-azure-data-factory"></a><span data-ttu-id="fe331-103">Skopiuj tooand danych z bazy danych SQL Azure przy użyciu fabryki danych Azure</span><span class="sxs-lookup"><span data-stu-id="fe331-103">Copy data tooand from Azure SQL Database using Azure Data Factory</span></span>
<span data-ttu-id="fe331-104">W tym artykule opisano, jak toouse hello działanie kopiowania w fabryce danych Azure toomove danych tooand z bazy danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="fe331-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data tooand from Azure SQL Database.</span></span> <span data-ttu-id="fe331-105">Opiera się na powitania [działań przepływu danych](data-factory-data-movement-activities.md) artykułu, który przedstawia ogólny przegląd przenoszenia danych z hello działanie kopiowania.</span><span class="sxs-lookup"><span data-stu-id="fe331-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>  

## <a name="supported-scenarios"></a><span data-ttu-id="fe331-106">Obsługiwane scenariusze</span><span class="sxs-lookup"><span data-stu-id="fe331-106">Supported scenarios</span></span>
<span data-ttu-id="fe331-107">Dane należy skopiować **z bazy danych SQL Azure** toohello po magazynów danych:</span><span class="sxs-lookup"><span data-stu-id="fe331-107">You can copy data **from Azure SQL Database** toohello following data stores:</span></span>

[!INCLUDE [data-factory-supported-sinks](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="fe331-108">Można skopiować danych z powitania po magazyny danych **tooAzure bazy danych SQL**:</span><span class="sxs-lookup"><span data-stu-id="fe331-108">You can copy data from hello following data stores **tooAzure SQL Database**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

## <a name="supported-authentication-type"></a><span data-ttu-id="fe331-109">Obsługiwany typ uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="fe331-109">Supported authentication type</span></span>
<span data-ttu-id="fe331-110">Łącznik bazy danych SQL Azure obsługuje uwierzytelnianie podstawowe.</span><span class="sxs-lookup"><span data-stu-id="fe331-110">Azure SQL Database connector supports basic authentication.</span></span>

## <a name="getting-started"></a><span data-ttu-id="fe331-111">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="fe331-111">Getting started</span></span>
<span data-ttu-id="fe331-112">Można utworzyć potoku o działanie kopiowania, który przenosi dane z bazy danych SQL Azure za pomocą różnych narzędzi/interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="fe331-112">You can create a pipeline with a copy activity that moves data to/from an Azure SQL Database by using different tools/APIs.</span></span>

<span data-ttu-id="fe331-113">Witaj Najprostszym sposobem toocreate potoku jest toouse hello **kreatora kopiowania**.</span><span class="sxs-lookup"><span data-stu-id="fe331-113">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="fe331-114">Zobacz [samouczek: tworzenie potoku za pomocą Kreatora kopiowania](data-factory-copy-data-wizard-tutorial.md) szybkie przewodnik dotyczący tworzenia potoku za pomocą Kreatora dane Kopiuj hello.</span><span class="sxs-lookup"><span data-stu-id="fe331-114">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="fe331-115">Można również użyć hello następujące narzędzia toocreate potoku: **portalu Azure**, **programu Visual Studio**, **programu Azure PowerShell**, **szablonu usługi Azure Resource Manager** , **Interfejs API .NET**, i **interfejsu API REST**.</span><span class="sxs-lookup"><span data-stu-id="fe331-115">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="fe331-116">Zobacz [samouczek działania kopiowania](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) dla toocreate instrukcje krok po kroku potoku z działaniem kopiowania.</span><span class="sxs-lookup"><span data-stu-id="fe331-116">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="fe331-117">Czy za pomocą narzędzia hello lub interfejsów API, należy wykonać następujące kroki toocreate potok, który przenosi się, że magazyn danych ze źródła danych magazynu danych zbiornika tooa hello:</span><span class="sxs-lookup"><span data-stu-id="fe331-117">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span> 

1. <span data-ttu-id="fe331-118">Utwórz **fabryki danych**.</span><span class="sxs-lookup"><span data-stu-id="fe331-118">Create a **data factory**.</span></span> <span data-ttu-id="fe331-119">Fabryka danych może zawierać co najmniej jeden potoków.</span><span class="sxs-lookup"><span data-stu-id="fe331-119">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="fe331-120">Utwórz **połączone usługi** toolink usługi fabryka danych tooyour magazynów danych wejściowych i wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="fe331-120">Create **linked services** toolink input and output data stores tooyour data factory.</span></span> <span data-ttu-id="fe331-121">Na przykład jeśli dane są kopiowane z bazy danych Azure SQL tooan magazynu obiektów blob platformy Azure, utworzysz dwie toolink połączonych usług Twoje konto magazynu Azure i fabryki danych tooyour bazy danych Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="fe331-121">For example, if you are copying data from an Azure blob storage tooan Azure SQL database, you create two linked services toolink your Azure storage account and Azure SQL database tooyour data factory.</span></span> <span data-ttu-id="fe331-122">Dla właściwości połączonej usługi, które są określone tooAzure bazy danych SQL, zobacz [połączona usługa właściwości](#linked-service-properties) sekcji.</span><span class="sxs-lookup"><span data-stu-id="fe331-122">For linked service properties that are specific tooAzure SQL Database, see [linked service properties](#linked-service-properties) section.</span></span> 
3. <span data-ttu-id="fe331-123">Utwórz **zestawów danych** toorepresent wejściowe i wyjściowe dane hello operacji kopiowania.</span><span class="sxs-lookup"><span data-stu-id="fe331-123">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> <span data-ttu-id="fe331-124">Przykład Witaj wymienionych w ostatnim kroku hello służy do tworzenia kontenera obiektów blob hello toospecify zestawu danych i folderu zawierającego hello danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="fe331-124">In hello example mentioned in hello last step, you create a dataset toospecify hello blob container and folder that contains hello input data.</span></span> <span data-ttu-id="fe331-125">I utwórz inny zestaw danych toospecify hello tabeli SQL w bazie danych Azure SQL hello przechowujący dane hello skopiowane z magazynu obiektów blob hello.</span><span class="sxs-lookup"><span data-stu-id="fe331-125">And, you create another dataset toospecify hello SQL table in hello Azure SQL database  that holds hello data copied from hello blob storage.</span></span> <span data-ttu-id="fe331-126">Dla właściwości zestawu danych, które są określone tooAzure usługi Data Lake Store, zobacz [właściwości zestawu danych](#dataset-properties) sekcji.</span><span class="sxs-lookup"><span data-stu-id="fe331-126">For dataset properties that are specific tooAzure Data Lake Store, see [dataset properties](#dataset-properties) section.</span></span>
4. <span data-ttu-id="fe331-127">Utwórz **potoku** aktywnością kopiowania zestawu danych jako dane wejściowe i zestawu danych jako dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="fe331-127">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="fe331-128">W przykładzie hello wspomniano wcześniej używa BlobSource jako źródło i SqlSink jako zbiorniku dla aktywności kopiowania hello.</span><span class="sxs-lookup"><span data-stu-id="fe331-128">In hello example mentioned earlier, you use BlobSource as a source and SqlSink as a sink for hello copy activity.</span></span> <span data-ttu-id="fe331-129">Podobnie są kopiowane z bazy danych SQL Azure tooAzure magazynu obiektów Blob, należy użyć SqlSource i BlobSink w przypadku działania kopiowania hello.</span><span class="sxs-lookup"><span data-stu-id="fe331-129">Similarly, if you are copying from Azure SQL Database tooAzure Blob Storage, you use SqlSource and BlobSink in hello copy activity.</span></span> <span data-ttu-id="fe331-130">Dla właściwości działania kopiowania, które są określone tooAzure bazy danych SQL, zobacz [skopiować właściwości działania](#copy-activity-properties) sekcji.</span><span class="sxs-lookup"><span data-stu-id="fe331-130">For copy activity properties that are specific tooAzure SQL Database, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="fe331-131">Szczegółowe informacje dotyczące sposobu toouse, Magazyn danych, jako źródło lub zbiorniku kliknij łącze hello w poprzedniej sekcji powitania dla magazynu danych.</span><span class="sxs-lookup"><span data-stu-id="fe331-131">For details on how toouse a data store as a source or a sink, click hello link in hello previous section for your data store.</span></span>

<span data-ttu-id="fe331-132">Korzystając z Kreatora hello, definicje JSON do tych jednostek fabryki danych (połączone usługi, zestawy danych i potoku hello) są tworzone automatycznie dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="fe331-132">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="fe331-133">Korzystając z narzędzi/API (z wyjątkiem interfejs API .NET), należy zdefiniować za pomocą formatu JSON hello tych jednostek fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="fe331-133">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="fe331-134">Aby uzyskać przykłady z definicji JSON dla jednostek fabryki danych, które są używane toocopy danych do/z bazy danych SQL Azure, zobacz [przykłady JSON](#json-examples-for-copying-data-to-and-from-sql-database) sekcji tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="fe331-134">For samples with JSON definitions for Data Factory entities that are used toocopy data to/from an Azure SQL Database, see [JSON examples](#json-examples-for-copying-data-to-and-from-sql-database) section of this article.</span></span> 

<span data-ttu-id="fe331-135">Witaj następujące sekcje zawierają szczegółowe informacje o właściwości JSON, które są używane toodefine fabryki danych jednostek określonych tooAzure bazy danych SQL:</span><span class="sxs-lookup"><span data-stu-id="fe331-135">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooAzure SQL Database:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="fe331-136">Połączona usługa właściwości</span><span class="sxs-lookup"><span data-stu-id="fe331-136">Linked service properties</span></span>
<span data-ttu-id="fe331-137">Azure SQL połączone łącza usługi fabryka danych tooyour bazy danych Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="fe331-137">An Azure SQL linked service links an Azure SQL database tooyour data factory.</span></span> <span data-ttu-id="fe331-138">Witaj w poniższej tabeli zawiera opis JSON elementy określonych tooAzure SQL połączonej usługi.</span><span class="sxs-lookup"><span data-stu-id="fe331-138">hello following table provides description for JSON elements specific tooAzure SQL linked service.</span></span>

| <span data-ttu-id="fe331-139">Właściwość</span><span class="sxs-lookup"><span data-stu-id="fe331-139">Property</span></span> | <span data-ttu-id="fe331-140">Opis</span><span class="sxs-lookup"><span data-stu-id="fe331-140">Description</span></span> | <span data-ttu-id="fe331-141">Wymagane</span><span class="sxs-lookup"><span data-stu-id="fe331-141">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="fe331-142">type</span><span class="sxs-lookup"><span data-stu-id="fe331-142">type</span></span> |<span data-ttu-id="fe331-143">musi mieć ustawioną właściwość type Hello: **AzureSqlDatabase**</span><span class="sxs-lookup"><span data-stu-id="fe331-143">hello type property must be set to: **AzureSqlDatabase**</span></span> |<span data-ttu-id="fe331-144">Tak</span><span class="sxs-lookup"><span data-stu-id="fe331-144">Yes</span></span> |
| <span data-ttu-id="fe331-145">Parametry połączenia</span><span class="sxs-lookup"><span data-stu-id="fe331-145">connectionString</span></span> |<span data-ttu-id="fe331-146">Określ informacje niezbędne wystąpienie bazy danych SQL Azure toohello tooconnect hello właściwości connectionString.</span><span class="sxs-lookup"><span data-stu-id="fe331-146">Specify information needed tooconnect toohello Azure SQL Database instance for hello connectionString property.</span></span> <span data-ttu-id="fe331-147">Obsługiwane jest tylko uwierzytelnianie podstawowe.</span><span class="sxs-lookup"><span data-stu-id="fe331-147">Only basic authentication is supported.</span></span> |<span data-ttu-id="fe331-148">Tak</span><span class="sxs-lookup"><span data-stu-id="fe331-148">Yes</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="fe331-149">Skonfiguruj [zapory bazy danych SQL Azure](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure) hello serwera bazy danych za[Zezwól serwerowi hello tooaccess usług Azure](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure).</span><span class="sxs-lookup"><span data-stu-id="fe331-149">Configure [Azure SQL Database Firewall](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure) hello database server too[allow Azure Services tooaccess hello server](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure).</span></span> <span data-ttu-id="fe331-150">Ponadto jeśli kopiujesz tooAzure danych bazy danych SQL z poza tym Azure z lokalnych źródeł danych z bramą fabryki danych, należy skonfigurować odpowiedni zakres adresów IP dla maszyny hello, który wysyła dane tooAzure bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="fe331-150">Additionally, if you are copying data tooAzure SQL Database from outside Azure including from on-premises data sources with data factory gateway, configure appropriate IP address range for hello machine that is sending data tooAzure SQL Database.</span></span>

## <a name="dataset-properties"></a><span data-ttu-id="fe331-151">Właściwości zestawu danych</span><span class="sxs-lookup"><span data-stu-id="fe331-151">Dataset properties</span></span>
<span data-ttu-id="fe331-152">toospecify toorepresent zestawu danych wejściowych lub wyjściowych danych w bazie danych Azure SQL, ustawić właściwości typu hello hello zestawu danych, aby: **AzureSqlTable**.</span><span class="sxs-lookup"><span data-stu-id="fe331-152">toospecify a dataset toorepresent input or output data in an Azure SQL database, you set hello type property of hello dataset to: **AzureSqlTable**.</span></span> <span data-ttu-id="fe331-153">Zestaw hello **linkedServiceName** właściwości zestawu danych hello toohello nazwę hello Azure SQL połączonej usługi.</span><span class="sxs-lookup"><span data-stu-id="fe331-153">Set hello **linkedServiceName** property of hello dataset toohello name of hello Azure SQL linked service.</span></span>  

<span data-ttu-id="fe331-154">Aby uzyskać pełną listę sekcje & właściwości dostępne do definiowania zestawów danych, zobacz hello [Tworzenie zbiorów danych](data-factory-create-datasets.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="fe331-154">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="fe331-155">Sekcje zawierają informacje, takie jak struktury, dostępności i zasad zestawu danych JSON są podobne dla wszystkich typów obiektów dataset (Azure SQL, obiektów blob platformy Azure, Azure tabeli itp.).</span><span class="sxs-lookup"><span data-stu-id="fe331-155">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="fe331-156">sekcja typeProperties Hello jest różne dla każdego typu zestawu danych i zawiera informacje o lokalizacji hello hello danych w magazynie danych hello.</span><span class="sxs-lookup"><span data-stu-id="fe331-156">hello typeProperties section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="fe331-157">Witaj **typeProperties** sekcja dla zestawu danych hello typu **AzureSqlTable** ma hello następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="fe331-157">hello **typeProperties** section for hello dataset of type **AzureSqlTable** has hello following properties:</span></span>

| <span data-ttu-id="fe331-158">Właściwość</span><span class="sxs-lookup"><span data-stu-id="fe331-158">Property</span></span> | <span data-ttu-id="fe331-159">Opis</span><span class="sxs-lookup"><span data-stu-id="fe331-159">Description</span></span> | <span data-ttu-id="fe331-160">Wymagane</span><span class="sxs-lookup"><span data-stu-id="fe331-160">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="fe331-161">tableName</span><span class="sxs-lookup"><span data-stu-id="fe331-161">tableName</span></span> |<span data-ttu-id="fe331-162">Nazwa hello tabeli lub widoku w wystąpieniu bazy danych SQL Azure hello, która jest połączona usługa odnosi się do.</span><span class="sxs-lookup"><span data-stu-id="fe331-162">Name of hello table or view in hello Azure SQL Database instance that linked service refers to.</span></span> |<span data-ttu-id="fe331-163">Tak</span><span class="sxs-lookup"><span data-stu-id="fe331-163">Yes</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="fe331-164">Właściwości działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="fe331-164">Copy activity properties</span></span>
<span data-ttu-id="fe331-165">Pełną listę sekcje & właściwości dostępne do definiowania działań, zobacz hello [tworzenie potoków](data-factory-create-pipelines.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="fe331-165">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="fe331-166">Właściwości, takie jak nazwa, opis, dane wejściowe i wyjściowe tabel i zasady są dostępne dla wszystkich typów działań.</span><span class="sxs-lookup"><span data-stu-id="fe331-166">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

> [!NOTE]
> <span data-ttu-id="fe331-167">Witaj działanie kopiowania przyjmuje tylko jeden parametr wejściowy i tworzy tylko jedno wyjście.</span><span class="sxs-lookup"><span data-stu-id="fe331-167">hello Copy Activity takes only one input and produces only one output.</span></span>

<span data-ttu-id="fe331-168">Właściwości dostępne w hello **typeProperties** sekcji hello działanie zależy od każdy typ działania.</span><span class="sxs-lookup"><span data-stu-id="fe331-168">Whereas, properties available in hello **typeProperties** section of hello activity vary with each activity type.</span></span> <span data-ttu-id="fe331-169">Dla działania kopiowania różnią się w zależności od typów hello źródeł i sink.</span><span class="sxs-lookup"><span data-stu-id="fe331-169">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="fe331-170">Chcesz przenieść dane z bazy danych Azure SQL, należy ustawić typ źródła hello w przypadku działania kopiowania hello zbyt**SqlSource**.</span><span class="sxs-lookup"><span data-stu-id="fe331-170">If you are moving data from an Azure SQL database, you set hello source type in hello copy activity too**SqlSource**.</span></span> <span data-ttu-id="fe331-171">Podobnie jeśli przenosisz bazę danych Azure SQL tooan danych ustawisz typ ujścia hello w przypadku działania kopiowania hello zbyt**SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="fe331-171">Similarly, if you are moving data tooan Azure SQL database, you set hello sink type in hello copy activity too**SqlSink**.</span></span> <span data-ttu-id="fe331-172">Ta sekcja zawiera listę obsługiwanych przez SqlSource i SqlSink właściwości.</span><span class="sxs-lookup"><span data-stu-id="fe331-172">This section provides a list of properties supported by SqlSource and SqlSink.</span></span>

### <a name="sqlsource"></a><span data-ttu-id="fe331-173">SqlSource</span><span class="sxs-lookup"><span data-stu-id="fe331-173">SqlSource</span></span>
<span data-ttu-id="fe331-174">W przypadku działania kopiowania, gdy źródłem hello jest typu **SqlSource**, dostępne są następujące właściwości hello **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="fe331-174">In copy activity, when hello source is of type **SqlSource**, hello following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="fe331-175">Właściwość</span><span class="sxs-lookup"><span data-stu-id="fe331-175">Property</span></span> | <span data-ttu-id="fe331-176">Opis</span><span class="sxs-lookup"><span data-stu-id="fe331-176">Description</span></span> | <span data-ttu-id="fe331-177">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="fe331-177">Allowed values</span></span> | <span data-ttu-id="fe331-178">Wymagane</span><span class="sxs-lookup"><span data-stu-id="fe331-178">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="fe331-179">sqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="fe331-179">sqlReaderQuery</span></span> |<span data-ttu-id="fe331-180">Użyj hello zapytanie niestandardowe tooread danych.</span><span class="sxs-lookup"><span data-stu-id="fe331-180">Use hello custom query tooread data.</span></span> |<span data-ttu-id="fe331-181">Ciąg zapytania SQL.</span><span class="sxs-lookup"><span data-stu-id="fe331-181">SQL query string.</span></span> <span data-ttu-id="fe331-182">Przykład: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="fe331-182">Example: `select * from MyTable`.</span></span> |<span data-ttu-id="fe331-183">Nie</span><span class="sxs-lookup"><span data-stu-id="fe331-183">No</span></span> |
| <span data-ttu-id="fe331-184">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="fe331-184">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="fe331-185">Nazwa hello przechowywane procedury, która odczytuje dane z hello tabeli źródłowej.</span><span class="sxs-lookup"><span data-stu-id="fe331-185">Name of hello stored procedure that reads data from hello source table.</span></span> |<span data-ttu-id="fe331-186">Nazwa hello procedury składowanej.</span><span class="sxs-lookup"><span data-stu-id="fe331-186">Name of hello stored procedure.</span></span> <span data-ttu-id="fe331-187">Witaj ostatniej instrukcji SQL musi być instrukcji SELECT w procedurze hello przechowywane.</span><span class="sxs-lookup"><span data-stu-id="fe331-187">hello last SQL statement must be a SELECT statement in hello stored procedure.</span></span> |<span data-ttu-id="fe331-188">Nie</span><span class="sxs-lookup"><span data-stu-id="fe331-188">No</span></span> |
| <span data-ttu-id="fe331-189">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="fe331-189">storedProcedureParameters</span></span> |<span data-ttu-id="fe331-190">Parametry hello procedury składowanej.</span><span class="sxs-lookup"><span data-stu-id="fe331-190">Parameters for hello stored procedure.</span></span> |<span data-ttu-id="fe331-191">Par nazwa/wartość.</span><span class="sxs-lookup"><span data-stu-id="fe331-191">Name/value pairs.</span></span> <span data-ttu-id="fe331-192">Nazwy i wielkość liter w wyrazie parametry muszą być zgodne, hello nazwy i parametry procedury przechowywane hello wielkości liter.</span><span class="sxs-lookup"><span data-stu-id="fe331-192">Names and casing of parameters must match hello names and casing of hello stored procedure parameters.</span></span> |<span data-ttu-id="fe331-193">Nie</span><span class="sxs-lookup"><span data-stu-id="fe331-193">No</span></span> |

<span data-ttu-id="fe331-194">Jeśli hello **sqlReaderQuery** określono hello SqlSource, hello odbywa się działanie kopii tego zapytania względem hello bazy danych SQL Azure źródła tooget hello danych.</span><span class="sxs-lookup"><span data-stu-id="fe331-194">If hello **sqlReaderQuery** is specified for hello SqlSource, hello Copy Activity runs this query against hello Azure SQL Database source tooget hello data.</span></span> <span data-ttu-id="fe331-195">Alternatywnie można określić procedury składowanej, określając hello **sqlReaderStoredProcedureName** i **storedProcedureParameters** (jeśli hello procedura składowana pobiera parametry).</span><span class="sxs-lookup"><span data-stu-id="fe331-195">Alternatively, you can specify a stored procedure by specifying hello **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if hello stored procedure takes parameters).</span></span>

<span data-ttu-id="fe331-196">Jeśli nie określisz sqlReaderQuery lub sqlReaderStoredProcedureName hello kolumn zdefiniowanych w sekcji Struktura hello hello zestawu danych JSON są używane toobuild kwerendy (`select column1, column2 from mytable`) toorun przed hello bazy danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="fe331-196">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, hello columns defined in hello structure section of hello dataset JSON are used toobuild a query (`select column1, column2 from mytable`) toorun against hello Azure SQL Database.</span></span> <span data-ttu-id="fe331-197">Jeśli hello definicji zestawu danych nie ma on struktury hello, wszystkie kolumny są wybierane w tabeli hello.</span><span class="sxs-lookup"><span data-stu-id="fe331-197">If hello dataset definition does not have hello structure, all columns are selected from hello table.</span></span>

> [!NOTE]
> <span data-ttu-id="fe331-198">Jeśli używasz **sqlReaderStoredProcedureName**, należy nadal toospecify wartość dla hello **tableName** właściwości w elemencie dataset hello JSON.</span><span class="sxs-lookup"><span data-stu-id="fe331-198">When you use **sqlReaderStoredProcedureName**, you still need toospecify a value for hello **tableName** property in hello dataset JSON.</span></span> <span data-ttu-id="fe331-199">Nie ma żadnych operacji sprawdzania poprawności, jednak wykonywać na tej tabeli.</span><span class="sxs-lookup"><span data-stu-id="fe331-199">There are no validations performed against this table though.</span></span>
>
>

### <a name="sqlsource-example"></a><span data-ttu-id="fe331-200">Przykład SqlSource</span><span class="sxs-lookup"><span data-stu-id="fe331-200">SqlSource example</span></span>

```JSON
"source": {
    "type": "SqlSource",
    "sqlReaderStoredProcedureName": "CopyTestSrcStoredProcedureWithParameters",
    "storedProcedureParameters": {
        "stringData": { "value": "str3" },
        "identifier": { "value": "$$Text.Format('{0:yyyy}', SliceStart)", "type": "Int"}
    }
}
```

<span data-ttu-id="fe331-201">**Definicja procedury przechowywane Hello:**</span><span class="sxs-lookup"><span data-stu-id="fe331-201">**hello stored procedure definition:**</span></span>

```SQL
CREATE PROCEDURE CopyTestSrcStoredProcedureWithParameters
(
    @stringData varchar(20),
    @identifier int
)
AS
SET NOCOUNT ON;
BEGIN
     select *
     from dbo.UnitTestSrcTable
     where dbo.UnitTestSrcTable.stringData != stringData
    and dbo.UnitTestSrcTable.identifier != identifier
END
GO
```

### <a name="sqlsink"></a><span data-ttu-id="fe331-202">SqlSink</span><span class="sxs-lookup"><span data-stu-id="fe331-202">SqlSink</span></span>
<span data-ttu-id="fe331-203">**SqlSink** obsługuje hello następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="fe331-203">**SqlSink** supports hello following properties:</span></span>

| <span data-ttu-id="fe331-204">Właściwość</span><span class="sxs-lookup"><span data-stu-id="fe331-204">Property</span></span> | <span data-ttu-id="fe331-205">Opis</span><span class="sxs-lookup"><span data-stu-id="fe331-205">Description</span></span> | <span data-ttu-id="fe331-206">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="fe331-206">Allowed values</span></span> | <span data-ttu-id="fe331-207">Wymagane</span><span class="sxs-lookup"><span data-stu-id="fe331-207">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="fe331-208">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="fe331-208">writeBatchTimeout</span></span> |<span data-ttu-id="fe331-209">Czas toocomplete operacji wstawiania wsadowego hello oczekiwania, zanim upłynie limit czasu.</span><span class="sxs-lookup"><span data-stu-id="fe331-209">Wait time for hello batch insert operation toocomplete before it times out.</span></span> |<span data-ttu-id="fe331-210">Zakres czasu</span><span class="sxs-lookup"><span data-stu-id="fe331-210">timespan</span></span><br/><br/> <span data-ttu-id="fe331-211">Przykład: "00: 30:00" (30 minut).</span><span class="sxs-lookup"><span data-stu-id="fe331-211">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="fe331-212">Nie</span><span class="sxs-lookup"><span data-stu-id="fe331-212">No</span></span> |
| <span data-ttu-id="fe331-213">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="fe331-213">writeBatchSize</span></span> |<span data-ttu-id="fe331-214">Wstawia dane do tabeli SQL hello, gdy osiągnie rozmiar buforu hello writeBatchSize.</span><span class="sxs-lookup"><span data-stu-id="fe331-214">Inserts data into hello SQL table when hello buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="fe331-215">Liczba całkowita (liczba wierszy)</span><span class="sxs-lookup"><span data-stu-id="fe331-215">Integer (number of rows)</span></span> |<span data-ttu-id="fe331-216">Nie (domyślne: 10000)</span><span class="sxs-lookup"><span data-stu-id="fe331-216">No (default: 10000)</span></span> |
| <span data-ttu-id="fe331-217">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="fe331-217">sqlWriterCleanupScript</span></span> |<span data-ttu-id="fe331-218">Określ kwerendę dla działania kopiowania tooexecute tak, aby dane określonych wycinek jest wyczyszczone.</span><span class="sxs-lookup"><span data-stu-id="fe331-218">Specify a query for Copy Activity tooexecute such that data of a specific slice is cleaned up.</span></span> <span data-ttu-id="fe331-219">Aby uzyskać więcej informacji, zobacz [powtarzalne kopiowania](#repeatable-copy).</span><span class="sxs-lookup"><span data-stu-id="fe331-219">For more information, see [repeatable copy](#repeatable-copy).</span></span> |<span data-ttu-id="fe331-220">Instrukcja zapytania.</span><span class="sxs-lookup"><span data-stu-id="fe331-220">A query statement.</span></span> |<span data-ttu-id="fe331-221">Nie</span><span class="sxs-lookup"><span data-stu-id="fe331-221">No</span></span> |
| <span data-ttu-id="fe331-222">sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="fe331-222">sliceIdentifierColumnName</span></span> |<span data-ttu-id="fe331-223">Określ nazwę kolumny dla działania kopiowania toofill o identyfikatorze wycinek automatycznie generowane, która jest używana tooclean zapasowych określonych wycinek czas ponownego uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="fe331-223">Specify a column name for Copy Activity toofill with auto generated slice identifier, which is used tooclean up data of a specific slice when rerun.</span></span> <span data-ttu-id="fe331-224">Aby uzyskać więcej informacji, zobacz [powtarzalne kopiowania](#repeatable-copy).</span><span class="sxs-lookup"><span data-stu-id="fe331-224">For more information, see [repeatable copy](#repeatable-copy).</span></span> |<span data-ttu-id="fe331-225">Nazwa kolumny kolumnę o typie danych binary(32).</span><span class="sxs-lookup"><span data-stu-id="fe331-225">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="fe331-226">Nie</span><span class="sxs-lookup"><span data-stu-id="fe331-226">No</span></span> |
| <span data-ttu-id="fe331-227">sqlWriterStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="fe331-227">sqlWriterStoredProcedureName</span></span> |<span data-ttu-id="fe331-228">Nazwa hello procedury składowanej danych upserts (aktualizacje/INSERT) do tabeli docelowej hello.</span><span class="sxs-lookup"><span data-stu-id="fe331-228">Name of hello stored procedure that upserts (updates/inserts) data into hello target table.</span></span> |<span data-ttu-id="fe331-229">Nazwa hello procedury składowanej.</span><span class="sxs-lookup"><span data-stu-id="fe331-229">Name of hello stored procedure.</span></span> |<span data-ttu-id="fe331-230">Nie</span><span class="sxs-lookup"><span data-stu-id="fe331-230">No</span></span> |
| <span data-ttu-id="fe331-231">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="fe331-231">storedProcedureParameters</span></span> |<span data-ttu-id="fe331-232">Parametry hello procedury składowanej.</span><span class="sxs-lookup"><span data-stu-id="fe331-232">Parameters for hello stored procedure.</span></span> |<span data-ttu-id="fe331-233">Par nazwa/wartość.</span><span class="sxs-lookup"><span data-stu-id="fe331-233">Name/value pairs.</span></span> <span data-ttu-id="fe331-234">Nazwy i wielkość liter w wyrazie parametry muszą być zgodne, hello nazwy i parametry procedury przechowywane hello wielkości liter.</span><span class="sxs-lookup"><span data-stu-id="fe331-234">Names and casing of parameters must match hello names and casing of hello stored procedure parameters.</span></span> |<span data-ttu-id="fe331-235">Nie</span><span class="sxs-lookup"><span data-stu-id="fe331-235">No</span></span> |
| <span data-ttu-id="fe331-236">sqlWriterTableType</span><span class="sxs-lookup"><span data-stu-id="fe331-236">sqlWriterTableType</span></span> |<span data-ttu-id="fe331-237">Określ toobe nazwy typu tabeli używany w procedurze hello przechowywane.</span><span class="sxs-lookup"><span data-stu-id="fe331-237">Specify a table type name toobe used in hello stored procedure.</span></span> <span data-ttu-id="fe331-238">Działanie kopiowania udostępnia dane hello przenoszone w tabeli tymczasowej o tym typie tabeli.</span><span class="sxs-lookup"><span data-stu-id="fe331-238">Copy activity makes hello data being moved available in a temp table with this table type.</span></span> <span data-ttu-id="fe331-239">Procedura składowana kod następnie można scalać dane hello kopiowane z istniejącymi danymi.</span><span class="sxs-lookup"><span data-stu-id="fe331-239">Stored procedure code can then merge hello data being copied with existing data.</span></span> |<span data-ttu-id="fe331-240">Nazwa typu tabeli.</span><span class="sxs-lookup"><span data-stu-id="fe331-240">A table type name.</span></span> |<span data-ttu-id="fe331-241">Nie</span><span class="sxs-lookup"><span data-stu-id="fe331-241">No</span></span> |

#### <a name="sqlsink-example"></a><span data-ttu-id="fe331-242">Przykład SqlSink</span><span class="sxs-lookup"><span data-stu-id="fe331-242">SqlSink example</span></span>

```JSON
"sink": {
    "type": "SqlSink",
    "writeBatchSize": 1000000,
    "writeBatchTimeout": "00:05:00",
    "sqlWriterStoredProcedureName": "CopyTestStoredProcedureWithParameters",
    "sqlWriterTableType": "CopyTestTableType",
    "storedProcedureParameters": {
        "identifier": { "value": "1", "type": "Int" },
        "stringData": { "value": "str1" },
        "decimalData": { "value": "1", "type": "Decimal" }
    }
}
```

## <a name="json-examples-for-copying-data-tooand-from-sql-database"></a><span data-ttu-id="fe331-243">Przykłady JSON do kopiowania tooand danych z bazy danych SQL</span><span class="sxs-lookup"><span data-stu-id="fe331-243">JSON examples for copying data tooand from SQL Database</span></span>
<span data-ttu-id="fe331-244">Witaj poniższe przykłady zapewniają definicje JSON przy użyciu można toocreate potoku [portalu Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) lub [programu Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) lub [programu Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="fe331-244">hello following examples provide sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="fe331-245">Przedstawiają sposób toocopy tooand danych z bazy danych SQL Azure i magazynu obiektów Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="fe331-245">They show how toocopy data tooand from Azure SQL Database and Azure Blob Storage.</span></span> <span data-ttu-id="fe331-246">Jednak dane mogą być kopiowane **bezpośrednio** z dowolnego źródła tooany z wychwytywanie hello wyrażony w [tutaj](data-factory-data-movement-activities.md#supported-data-stores-and-formats) przy użyciu hello działanie kopiowania w fabryce danych Azure.</span><span class="sxs-lookup"><span data-stu-id="fe331-246">However, data can be copied **directly** from any of sources tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>

### <a name="example-copy-data-from-azure-sql-database-tooazure-blob"></a><span data-ttu-id="fe331-247">Przykład: Kopiowanie danych z bazy danych SQL Azure tooAzure obiektów Blob</span><span class="sxs-lookup"><span data-stu-id="fe331-247">Example: Copy data from Azure SQL Database tooAzure Blob</span></span>
<span data-ttu-id="fe331-248">Witaj sam definiuje powitania po jednostek fabryki danych:</span><span class="sxs-lookup"><span data-stu-id="fe331-248">hello same defines hello following Data Factory entities:</span></span>

1. <span data-ttu-id="fe331-249">Połączonej usługi typu [AzureSqlDatabase](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="fe331-249">A linked service of type [AzureSqlDatabase](#linked-service-properties).</span></span>
2. <span data-ttu-id="fe331-250">Połączonej usługi typu [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="fe331-250">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="fe331-251">Dane wejściowe [dataset](data-factory-create-datasets.md) typu [AzureSqlTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="fe331-251">An input [dataset](data-factory-create-datasets.md) of type [AzureSqlTable](#dataset-properties).</span></span>
4. <span data-ttu-id="fe331-252">Dane wyjściowe [dataset](data-factory-create-datasets.md) typu [obiektów Blob platformy Azure](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="fe331-252">An output [dataset](data-factory-create-datasets.md) of type [Azure Blob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="fe331-253">A [potoku](data-factory-create-pipelines.md) z działania kopiowania, która używa [SqlSource](#copy-activity-properties) i [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="fe331-253">A [pipeline](data-factory-create-pipelines.md) with a Copy activity that uses [SqlSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="fe331-254">Przykładowe Hello kopiuje dane szeregów czasowych (co godzinę, codziennie, itp.) z tabeli w obiekcie blob tooa bazy danych Azure SQL co godzinę.</span><span class="sxs-lookup"><span data-stu-id="fe331-254">hello sample copies time-series data (hourly, daily, etc.) from a table in Azure SQL database tooa blob every hour.</span></span> <span data-ttu-id="fe331-255">właściwości JSON Hello używane w te przykłady są opisane w sekcjach poniżej hello próbek.</span><span class="sxs-lookup"><span data-stu-id="fe331-255">hello JSON properties used in these samples are described in sections following hello samples.</span></span>  

<span data-ttu-id="fe331-256">**Baza danych SQL Azure połączonej usługi:**</span><span class="sxs-lookup"><span data-stu-id="fe331-256">**Azure SQL Database linked service:**</span></span>

```JSON
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
<span data-ttu-id="fe331-257">Zobacz hello [połączoną usługę SQL Azure](#linked-service) sekcji hello listy właściwości obsługiwanych przez tej połączonej usługi.</span><span class="sxs-lookup"><span data-stu-id="fe331-257">See hello [Azure SQL Linked Service](#linked-service) section for hello list of properties supported by this linked service.</span></span>

<span data-ttu-id="fe331-258">**Magazyn obiektów Blob Azure połączonej usługi:**</span><span class="sxs-lookup"><span data-stu-id="fe331-258">**Azure Blob storage linked service:**</span></span>

```JSON
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
<span data-ttu-id="fe331-259">Zobacz hello [obiektów Blob platformy Azure](data-factory-azure-blob-connector.md#azure-storage-linked-service) artykułu hello listy właściwości obsługiwanych przez tej połączonej usługi.</span><span class="sxs-lookup"><span data-stu-id="fe331-259">See hello [Azure Blob](data-factory-azure-blob-connector.md#azure-storage-linked-service) article for hello list of properties supported by this linked service.</span></span>


<span data-ttu-id="fe331-260">**Azure SQL wejściowy zestaw danych:**</span><span class="sxs-lookup"><span data-stu-id="fe331-260">**Azure SQL input dataset:**</span></span>

<span data-ttu-id="fe331-261">przykład Witaj przyjęto założenie, utworzysz tabelę "MyTable" Azure SQL i zawiera kolumnę o nazwie "timestampcolumn" dla czasu serii danych.</span><span class="sxs-lookup"><span data-stu-id="fe331-261">hello sample assumes you have created a table “MyTable” in Azure SQL and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="fe331-262">Ustawienie "external": "prawda" informuje usługi fabryka danych Azure hello tego elementu dataset hello zewnętrznych toohello fabryki danych i nie jest generowany przez działanie w fabryce danych hello.</span><span class="sxs-lookup"><span data-stu-id="fe331-262">Setting “external”: ”true” informs hello Azure Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```JSON
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

<span data-ttu-id="fe331-263">Zobacz hello [właściwości typu zestawu danych Azure SQL](#dataset) sekcji hello listy właściwości obsługiwany przez dany typ zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="fe331-263">See hello [Azure SQL dataset type properties](#dataset) section for hello list of properties supported by this dataset type.</span></span>  

<span data-ttu-id="fe331-264">**Azure Blob wyjściowy zestaw danych:**</span><span class="sxs-lookup"><span data-stu-id="fe331-264">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="fe331-265">Dane są zapisywane tooa nowych obiektów blob, co godzinę (częstotliwość: godziny, interwał: 1).</span><span class="sxs-lookup"><span data-stu-id="fe331-265">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="fe331-266">Ścieżka folderu Hello hello obiektu blob dynamicznie jest obliczane na podstawie czasu rozpoczęcia hello hello wycinek, który jest przetwarzana.</span><span class="sxs-lookup"><span data-stu-id="fe331-266">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="fe331-267">Ścieżka folderu Hello używa rok, miesiąc, dzień i godziny części hello czas rozpoczęcia.</span><span class="sxs-lookup"><span data-stu-id="fe331-267">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

```JSON
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
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "yyyy"
          }
        },
        {
          "name": "Month",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "MM"
          }
        },
        {
          "name": "Day",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "dd"
          }
        },
        {
          "name": "Hour",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "HH"
          }
        }
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
<span data-ttu-id="fe331-268">Zobacz hello [właściwości typu zestawu danych obiektów Blob platformy Azure](data-factory-azure-blob-connector.md#dataset-properties) sekcji hello listy właściwości obsługiwany przez dany typ zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="fe331-268">See hello [Azure Blob dataset type properties](data-factory-azure-blob-connector.md#dataset-properties) section for hello list of properties supported by this dataset type.</span></span>  

<span data-ttu-id="fe331-269">**Działanie kopiowania w potoku z SQL źródłowy i odbiorczy obiektów Blob:**</span><span class="sxs-lookup"><span data-stu-id="fe331-269">**A copy activity in a pipeline with SQL source and Blob sink:**</span></span>

<span data-ttu-id="fe331-270">Witaj potoku zawiera działanie kopiowania, który jest skonfigurowany toouse hello wejściowych i wyjściowych zestawów danych i jest toorun zaplanowane co godzinę.</span><span class="sxs-lookup"><span data-stu-id="fe331-270">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="fe331-271">W potoku hello definicji JSON, hello **źródła** typu ustawiono zbyt**SqlSource** i **zbiornika** typu ustawiono zbyt**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="fe331-271">In hello pipeline JSON definition, hello **source** type is set too**SqlSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="fe331-272">Zapytanie SQL Hello określone dla hello **SqlReaderQuery** właściwości zaznacza danych hello hello poza toocopy godzinę.</span><span class="sxs-lookup"><span data-stu-id="fe331-272">hello SQL query specified for hello **SqlReaderQuery** property selects hello data in hello past hour toocopy.</span></span>

```JSON
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
<span data-ttu-id="fe331-273">Przykład Witaj **sqlReaderQuery** dla hello SqlSource został określony.</span><span class="sxs-lookup"><span data-stu-id="fe331-273">In hello example, **sqlReaderQuery** is specified for hello SqlSource.</span></span> <span data-ttu-id="fe331-274">Działanie kopiowania Hello jest uruchamiana to zapytanie dla hello hello tooget danymi bazy danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="fe331-274">hello Copy Activity runs this query against hello Azure SQL Database source tooget hello data.</span></span> <span data-ttu-id="fe331-275">Alternatywnie można określić procedury składowanej, określając hello **sqlReaderStoredProcedureName** i **storedProcedureParameters** (jeśli hello procedura składowana pobiera parametry).</span><span class="sxs-lookup"><span data-stu-id="fe331-275">Alternatively, you can specify a stored procedure by specifying hello **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if hello stored procedure takes parameters).</span></span>

<span data-ttu-id="fe331-276">Jeśli nie określisz sqlReaderQuery lub sqlReaderStoredProcedureName hello kolumn zdefiniowanych w sekcji Struktura hello hello zestawu danych JSON są używane toobuild toorun zapytania względem hello bazy danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="fe331-276">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, hello columns defined in hello structure section of hello dataset JSON are used toobuild a query toorun against hello Azure SQL Database.</span></span> <span data-ttu-id="fe331-277">Na przykład: `select column1, column2 from mytable`.</span><span class="sxs-lookup"><span data-stu-id="fe331-277">For example: `select column1, column2 from mytable`.</span></span> <span data-ttu-id="fe331-278">Jeśli hello definicji zestawu danych nie ma on struktury hello, wszystkie kolumny są wybierane w tabeli hello.</span><span class="sxs-lookup"><span data-stu-id="fe331-278">If hello dataset definition does not have hello structure, all columns are selected from hello table.</span></span>

<span data-ttu-id="fe331-279">Zobacz hello [źródła Sql](#sqlsource) sekcji i [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) hello listę obsługiwanych przez SqlSource i BlobSink właściwości.</span><span class="sxs-lookup"><span data-stu-id="fe331-279">See hello [Sql Source](#sqlsource) section and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) for hello list of properties supported by SqlSource and BlobSink.</span></span>

### <a name="example-copy-data-from-azure-blob-tooazure-sql-database"></a><span data-ttu-id="fe331-280">Przykład: Kopiowanie danych z obiektu Blob Azure tooAzure bazy danych SQL</span><span class="sxs-lookup"><span data-stu-id="fe331-280">Example: Copy data from Azure Blob tooAzure SQL Database</span></span>
<span data-ttu-id="fe331-281">przykład Witaj definiuje powitania po jednostek fabryki danych:</span><span class="sxs-lookup"><span data-stu-id="fe331-281">hello sample defines hello following Data Factory entities:</span></span>  

1. <span data-ttu-id="fe331-282">Połączonej usługi typu [AzureSqlDatabase](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="fe331-282">A linked service of type [AzureSqlDatabase](#linked-service-properties).</span></span>
2. <span data-ttu-id="fe331-283">Połączonej usługi typu [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="fe331-283">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="fe331-284">Dane wejściowe [dataset](data-factory-create-datasets.md) typu [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="fe331-284">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="fe331-285">Dane wyjściowe [dataset](data-factory-create-datasets.md) typu [AzureSqlTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="fe331-285">An output [dataset](data-factory-create-datasets.md) of type [AzureSqlTable](#dataset-properties).</span></span>
5. <span data-ttu-id="fe331-286">A [potoku](data-factory-create-pipelines.md) z działaniem kopii, która używa [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) i [SqlSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="fe331-286">A [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [SqlSink](#copy-activity-properties).</span></span>

<span data-ttu-id="fe331-287">Przykładowe Hello kopiuje dane szeregów czasowych (co godzinę, codziennie, itp.) z tabeli tooa obiektów blob platformy Azure w bazie danych Azure SQL co godzinę.</span><span class="sxs-lookup"><span data-stu-id="fe331-287">hello sample copies time-series data (hourly, daily, etc.) from Azure blob tooa table in Azure SQL database every hour.</span></span> <span data-ttu-id="fe331-288">właściwości JSON Hello używane w te przykłady są opisane w sekcjach poniżej hello próbek.</span><span class="sxs-lookup"><span data-stu-id="fe331-288">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="fe331-289">**Azure połączoną usługą SQL:**</span><span class="sxs-lookup"><span data-stu-id="fe331-289">**Azure SQL linked service:**</span></span>

```JSON
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
<span data-ttu-id="fe331-290">Zobacz hello [połączoną usługę SQL Azure](#linked-service) sekcji hello listy właściwości obsługiwanych przez tej połączonej usługi.</span><span class="sxs-lookup"><span data-stu-id="fe331-290">See hello [Azure SQL Linked Service](#linked-service) section for hello list of properties supported by this linked service.</span></span>

<span data-ttu-id="fe331-291">**Magazyn obiektów Blob Azure połączonej usługi:**</span><span class="sxs-lookup"><span data-stu-id="fe331-291">**Azure Blob storage linked service:**</span></span>

```JSON
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
<span data-ttu-id="fe331-292">Zobacz hello [obiektów Blob platformy Azure](data-factory-azure-blob-connector.md#azure-storage-linked-service) artykułu hello listy właściwości obsługiwanych przez tej połączonej usługi.</span><span class="sxs-lookup"><span data-stu-id="fe331-292">See hello [Azure Blob](data-factory-azure-blob-connector.md#azure-storage-linked-service) article for hello list of properties supported by this linked service.</span></span>


<span data-ttu-id="fe331-293">**Azure wejściowego zestawu danych obiektów Blob:**</span><span class="sxs-lookup"><span data-stu-id="fe331-293">**Azure Blob input dataset:**</span></span>

<span data-ttu-id="fe331-294">Dane są pobierane z nowego obiektu blob co godzinę (częstotliwość: godziny, interwał: 1).</span><span class="sxs-lookup"><span data-stu-id="fe331-294">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="fe331-295">Witaj folderu ścieżkę i nazwę pliku dla obiekt blob hello dynamicznie są oceniane na podstawie czasu rozpoczęcia hello hello wycinek, który jest przetwarzana.</span><span class="sxs-lookup"><span data-stu-id="fe331-295">hello folder path and file name for hello blob are dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="fe331-296">Ścieżka folderu Hello korzysta rok, miesiąc i dzień część czas rozpoczęcia hello, a nazwa pliku hello część hello czas rozpoczęcia.</span><span class="sxs-lookup"><span data-stu-id="fe331-296">hello folder path uses year, month, and day part of hello start time and file name uses hello hour part of hello start time.</span></span> <span data-ttu-id="fe331-297">"external": ustawienie "prawda" hello usługi fabryka danych informuje, że ta tabela zewnętrznych toohello fabryki danych i nie jest generowany przez działanie w fabryce danych hello.</span><span class="sxs-lookup"><span data-stu-id="fe331-297">“external”: “true” setting informs hello Data Factory service that this table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```JSON
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/",
      "fileName": "{Hour}.csv",
      "partitionedBy": [
        {
          "name": "Year",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "yyyy"
          }
        },
        {
          "name": "Month",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "MM"
          }
        },
        {
          "name": "Day",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "dd"
          }
        },
        {
          "name": "Hour",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "HH"
          }
        }
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
<span data-ttu-id="fe331-298">Zobacz hello [właściwości typu zestawu danych obiektów Blob platformy Azure](data-factory-azure-blob-connector.md#dataset-properties) sekcji hello listy właściwości obsługiwany przez dany typ zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="fe331-298">See hello [Azure Blob dataset type properties](data-factory-azure-blob-connector.md#dataset-properties) section for hello list of properties supported by this dataset type.</span></span>

<span data-ttu-id="fe331-299">**Baza danych SQL Azure wyjściowy zestaw danych:**</span><span class="sxs-lookup"><span data-stu-id="fe331-299">**Azure SQL Database output dataset:**</span></span>

<span data-ttu-id="fe331-300">przykład Witaj kopiuje tabeli tooa danych o nazwie "MyTable" w języku SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="fe331-300">hello sample copies data tooa table named “MyTable” in Azure SQL.</span></span> <span data-ttu-id="fe331-301">Utwórz tabelę hello SQL Azure z hello taką samą liczbę kolumn, zgodnie z oczekiwaniami toocontain pliku Blob CSV hello.</span><span class="sxs-lookup"><span data-stu-id="fe331-301">Create hello table in Azure SQL with hello same number of columns as you expect hello Blob CSV file toocontain.</span></span> <span data-ttu-id="fe331-302">Dodawaniu nowych wierszy tabeli toohello co godzinę.</span><span class="sxs-lookup"><span data-stu-id="fe331-302">New rows are added toohello table every hour.</span></span>

```JSON
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
<span data-ttu-id="fe331-303">Zobacz hello [właściwości typu zestawu danych Azure SQL](#dataset) sekcji hello listy właściwości obsługiwany przez dany typ zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="fe331-303">See hello [Azure SQL dataset type properties](#dataset) section for hello list of properties supported by this dataset type.</span></span>

<span data-ttu-id="fe331-304">**Działanie kopiowania w potoku z obiektu Blob, źródłowy i odbiorczy SQL:**</span><span class="sxs-lookup"><span data-stu-id="fe331-304">**A copy activity in a pipeline with Blob source and SQL sink:**</span></span>

<span data-ttu-id="fe331-305">Witaj potoku zawiera działanie kopiowania, który jest skonfigurowany toouse hello wejściowych i wyjściowych zestawów danych i jest toorun zaplanowane co godzinę.</span><span class="sxs-lookup"><span data-stu-id="fe331-305">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="fe331-306">W potoku hello definicji JSON, hello **źródła** typu ustawiono zbyt**BlobSource** i **zbiornika** typu ustawiono zbyt**SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="fe331-306">In hello pipeline JSON definition, hello **source** type is set too**BlobSource** and **sink** type is set too**SqlSink**.</span></span>

```JSON
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
            "type": "BlobSource",
            "blobColumnSeparators": ","
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
<span data-ttu-id="fe331-307">Zobacz hello [zbiornika Sql](#sqlsink) sekcji i [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) hello listę obsługiwanych przez SqlSink i BlobSource właściwości.</span><span class="sxs-lookup"><span data-stu-id="fe331-307">See hello [Sql Sink](#sqlsink) section and [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) for hello list of properties supported by SqlSink and BlobSource.</span></span>

## <a name="identity-columns-in-hello-target-database"></a><span data-ttu-id="fe331-308">Kolumny tożsamości w hello docelowej bazy danych</span><span class="sxs-lookup"><span data-stu-id="fe331-308">Identity columns in hello target database</span></span>
<span data-ttu-id="fe331-309">Ta sekcja zawiera przykład kopiowanie danych z tabeli źródłowej bez tożsamości tooa docelowej tabeli z kolumny tożsamości.</span><span class="sxs-lookup"><span data-stu-id="fe331-309">This section provides an example for copying data from a source table without an identity column tooa destination table with an identity column.</span></span>

<span data-ttu-id="fe331-310">**Tabela źródłowa:**</span><span class="sxs-lookup"><span data-stu-id="fe331-310">**Source table:**</span></span>

```SQL
create table dbo.SourceTbl
(
       name varchar(100),
       age int
)
```
<span data-ttu-id="fe331-311">**Tabela docelowa:**</span><span class="sxs-lookup"><span data-stu-id="fe331-311">**Destination table:**</span></span>

```SQL
create table dbo.TargetTbl
(
       identifier int identity(1,1),
       name varchar(100),
       age int
)
```
<span data-ttu-id="fe331-312">Należy zauważyć, że tabela docelowa hello ma kolumny tożsamości.</span><span class="sxs-lookup"><span data-stu-id="fe331-312">Notice that hello target table has an identity column.</span></span>

<span data-ttu-id="fe331-313">**Źródło zestawu danych JSON definicji**</span><span class="sxs-lookup"><span data-stu-id="fe331-313">**Source dataset JSON definition**</span></span>

```JSON
{
    "name": "SampleSource",
    "properties": {
        "type": " SqlServerTable",
        "linkedServiceName": "TestIdentitySQL",
        "typeProperties": {
            "tableName": "SourceTbl"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
```
<span data-ttu-id="fe331-314">**Docelowy zestaw danych JSON definicji**</span><span class="sxs-lookup"><span data-stu-id="fe331-314">**Destination dataset JSON definition**</span></span>

```JSON
{
    "name": "SampleTarget",
    "properties": {
        "structure": [
            { "name": "name" },
            { "name": "age" }
        ],
        "type": "AzureSqlTable",
        "linkedServiceName": "TestIdentitySQLSource",
        "typeProperties": {
            "tableName": "TargetTbl"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": false,
        "policy": {}
    }    
}
```

<span data-ttu-id="fe331-315">Należy zauważyć, że jako tabela źródłowa i docelowa mają różne schemat (element docelowy ma dodatkową kolumnę z tożsamością).</span><span class="sxs-lookup"><span data-stu-id="fe331-315">Notice that as your source and target table have different schema (target has an additional column with identity).</span></span> <span data-ttu-id="fe331-316">W tym scenariuszu należy toospecify **struktury** właściwości w definicji zestawu danych docelowego hello, która nie zawiera kolumny tożsamości hello.</span><span class="sxs-lookup"><span data-stu-id="fe331-316">In this scenario, you need toospecify **structure** property in hello target dataset definition, which doesn’t include hello identity column.</span></span>

## <a name="invoke-stored-procedure-from-sql-sink"></a><span data-ttu-id="fe331-317">Wywołaj procedurę składowaną z zbiornika SQL</span><span class="sxs-lookup"><span data-stu-id="fe331-317">Invoke stored procedure from SQL sink</span></span>
<span data-ttu-id="fe331-318">Na przykład wywoływania procedury składowanej z obiektu sink SQL w działaniu kopiowania potoku, zobacz [wywołaj procedurę składowaną dla obiekt sink SQL w przypadku działania kopiowania](data-factory-invoke-stored-procedure-from-copy-activity.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="fe331-318">For an example of invoking a stored procedure from SQL sink in a copy activity of a pipeline, see [Invoke stored procedure for SQL sink in copy activity](data-factory-invoke-stored-procedure-from-copy-activity.md) article.</span></span> 

## <a name="type-mapping-for-azure-sql-database"></a><span data-ttu-id="fe331-319">Mapowanie typu dla bazy danych SQL Azure</span><span class="sxs-lookup"><span data-stu-id="fe331-319">Type mapping for Azure SQL Database</span></span>
<span data-ttu-id="fe331-320">Jak wspomniano w hello [działań przepływu danych](data-factory-data-movement-activities.md) artykułu działanie kopiowania przeprowadza automatyczne konwersje z typów toosink typy źródła z hello następujące podejście krok 2:</span><span class="sxs-lookup"><span data-stu-id="fe331-320">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article Copy activity performs automatic type conversions from source types toosink types with hello following 2-step approach:</span></span>

1. <span data-ttu-id="fe331-321">Konwertować z typu too.NET typów natywnych źródła</span><span class="sxs-lookup"><span data-stu-id="fe331-321">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="fe331-322">Konwertować z typu sink toonative typu .NET</span><span class="sxs-lookup"><span data-stu-id="fe331-322">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="fe331-323">Podczas przenoszenia tooand danych z bazy danych SQL Azure, hello następujące mapowania są używane z too.NET typu SQL i odwrotnie.</span><span class="sxs-lookup"><span data-stu-id="fe331-323">When moving data tooand from Azure SQL Database, hello following mappings are used from SQL type too.NET type and vice versa.</span></span> <span data-ttu-id="fe331-324">Mapowanie Hello jest taki sam jak hello mapowanie typu danych serwera SQL dla ADO.NET.</span><span class="sxs-lookup"><span data-stu-id="fe331-324">hello mapping is same as hello SQL Server Data Type Mapping for ADO.NET.</span></span>

| <span data-ttu-id="fe331-325">Typ aparatu bazy danych programu SQL Server</span><span class="sxs-lookup"><span data-stu-id="fe331-325">SQL Server Database Engine type</span></span> | <span data-ttu-id="fe331-326">Typ programu .NET framework</span><span class="sxs-lookup"><span data-stu-id="fe331-326">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="fe331-327">bigint</span><span class="sxs-lookup"><span data-stu-id="fe331-327">bigint</span></span> |<span data-ttu-id="fe331-328">Int64</span><span class="sxs-lookup"><span data-stu-id="fe331-328">Int64</span></span> |
| <span data-ttu-id="fe331-329">Binarne</span><span class="sxs-lookup"><span data-stu-id="fe331-329">binary</span></span> |<span data-ttu-id="fe331-330">Byte]</span><span class="sxs-lookup"><span data-stu-id="fe331-330">Byte[]</span></span> |
| <span data-ttu-id="fe331-331">bitowe</span><span class="sxs-lookup"><span data-stu-id="fe331-331">bit</span></span> |<span data-ttu-id="fe331-332">Wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="fe331-332">Boolean</span></span> |
| <span data-ttu-id="fe331-333">char</span><span class="sxs-lookup"><span data-stu-id="fe331-333">char</span></span> |<span data-ttu-id="fe331-334">Ciąg, Char]</span><span class="sxs-lookup"><span data-stu-id="fe331-334">String, Char[]</span></span> |
| <span data-ttu-id="fe331-335">Data</span><span class="sxs-lookup"><span data-stu-id="fe331-335">date</span></span> |<span data-ttu-id="fe331-336">Data i godzina</span><span class="sxs-lookup"><span data-stu-id="fe331-336">DateTime</span></span> |
| <span data-ttu-id="fe331-337">Data i godzina</span><span class="sxs-lookup"><span data-stu-id="fe331-337">Datetime</span></span> |<span data-ttu-id="fe331-338">Data i godzina</span><span class="sxs-lookup"><span data-stu-id="fe331-338">DateTime</span></span> |
| <span data-ttu-id="fe331-339">datetime2</span><span class="sxs-lookup"><span data-stu-id="fe331-339">datetime2</span></span> |<span data-ttu-id="fe331-340">Data i godzina</span><span class="sxs-lookup"><span data-stu-id="fe331-340">DateTime</span></span> |
| <span data-ttu-id="fe331-341">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="fe331-341">Datetimeoffset</span></span> |<span data-ttu-id="fe331-342">DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="fe331-342">DateTimeOffset</span></span> |
| <span data-ttu-id="fe331-343">Decimal</span><span class="sxs-lookup"><span data-stu-id="fe331-343">Decimal</span></span> |<span data-ttu-id="fe331-344">Decimal</span><span class="sxs-lookup"><span data-stu-id="fe331-344">Decimal</span></span> |
| <span data-ttu-id="fe331-345">Atrybut FILESTREAM (varbinary(max))</span><span class="sxs-lookup"><span data-stu-id="fe331-345">FILESTREAM attribute (varbinary(max))</span></span> |<span data-ttu-id="fe331-346">Byte]</span><span class="sxs-lookup"><span data-stu-id="fe331-346">Byte[]</span></span> |
| <span data-ttu-id="fe331-347">Float</span><span class="sxs-lookup"><span data-stu-id="fe331-347">Float</span></span> |<span data-ttu-id="fe331-348">O podwójnej precyzji</span><span class="sxs-lookup"><span data-stu-id="fe331-348">Double</span></span> |
| <span data-ttu-id="fe331-349">Obraz</span><span class="sxs-lookup"><span data-stu-id="fe331-349">image</span></span> |<span data-ttu-id="fe331-350">Byte]</span><span class="sxs-lookup"><span data-stu-id="fe331-350">Byte[]</span></span> |
| <span data-ttu-id="fe331-351">int</span><span class="sxs-lookup"><span data-stu-id="fe331-351">int</span></span> |<span data-ttu-id="fe331-352">Int32</span><span class="sxs-lookup"><span data-stu-id="fe331-352">Int32</span></span> |
| <span data-ttu-id="fe331-353">oszczędność pieniędzy</span><span class="sxs-lookup"><span data-stu-id="fe331-353">money</span></span> |<span data-ttu-id="fe331-354">Decimal</span><span class="sxs-lookup"><span data-stu-id="fe331-354">Decimal</span></span> |
| <span data-ttu-id="fe331-355">nchar</span><span class="sxs-lookup"><span data-stu-id="fe331-355">nchar</span></span> |<span data-ttu-id="fe331-356">Ciąg, Char]</span><span class="sxs-lookup"><span data-stu-id="fe331-356">String, Char[]</span></span> |
| <span data-ttu-id="fe331-357">ntext</span><span class="sxs-lookup"><span data-stu-id="fe331-357">ntext</span></span> |<span data-ttu-id="fe331-358">Ciąg, Char]</span><span class="sxs-lookup"><span data-stu-id="fe331-358">String, Char[]</span></span> |
| <span data-ttu-id="fe331-359">numeryczne</span><span class="sxs-lookup"><span data-stu-id="fe331-359">numeric</span></span> |<span data-ttu-id="fe331-360">Decimal</span><span class="sxs-lookup"><span data-stu-id="fe331-360">Decimal</span></span> |
| <span data-ttu-id="fe331-361">nvarchar</span><span class="sxs-lookup"><span data-stu-id="fe331-361">nvarchar</span></span> |<span data-ttu-id="fe331-362">Ciąg, Char]</span><span class="sxs-lookup"><span data-stu-id="fe331-362">String, Char[]</span></span> |
| <span data-ttu-id="fe331-363">rzeczywiste</span><span class="sxs-lookup"><span data-stu-id="fe331-363">real</span></span> |<span data-ttu-id="fe331-364">Pojedynczy</span><span class="sxs-lookup"><span data-stu-id="fe331-364">Single</span></span> |
| <span data-ttu-id="fe331-365">ROWVERSION</span><span class="sxs-lookup"><span data-stu-id="fe331-365">rowversion</span></span> |<span data-ttu-id="fe331-366">Byte]</span><span class="sxs-lookup"><span data-stu-id="fe331-366">Byte[]</span></span> |
| <span data-ttu-id="fe331-367">smalldatetime</span><span class="sxs-lookup"><span data-stu-id="fe331-367">smalldatetime</span></span> |<span data-ttu-id="fe331-368">Data i godzina</span><span class="sxs-lookup"><span data-stu-id="fe331-368">DateTime</span></span> |
| <span data-ttu-id="fe331-369">smallint</span><span class="sxs-lookup"><span data-stu-id="fe331-369">smallint</span></span> |<span data-ttu-id="fe331-370">Int16</span><span class="sxs-lookup"><span data-stu-id="fe331-370">Int16</span></span> |
| <span data-ttu-id="fe331-371">smallmoney</span><span class="sxs-lookup"><span data-stu-id="fe331-371">smallmoney</span></span> |<span data-ttu-id="fe331-372">Decimal</span><span class="sxs-lookup"><span data-stu-id="fe331-372">Decimal</span></span> |
| <span data-ttu-id="fe331-373">sql_variant</span><span class="sxs-lookup"><span data-stu-id="fe331-373">sql_variant</span></span> |<span data-ttu-id="fe331-374">Obiekt *</span><span class="sxs-lookup"><span data-stu-id="fe331-374">Object *</span></span> |
| <span data-ttu-id="fe331-375">Tekst</span><span class="sxs-lookup"><span data-stu-id="fe331-375">text</span></span> |<span data-ttu-id="fe331-376">Ciąg, Char]</span><span class="sxs-lookup"><span data-stu-id="fe331-376">String, Char[]</span></span> |
| <span data-ttu-id="fe331-377">time</span><span class="sxs-lookup"><span data-stu-id="fe331-377">time</span></span> |<span data-ttu-id="fe331-378">Zakres czasu</span><span class="sxs-lookup"><span data-stu-id="fe331-378">TimeSpan</span></span> |
| <span data-ttu-id="fe331-379">sygnatura czasowa</span><span class="sxs-lookup"><span data-stu-id="fe331-379">timestamp</span></span> |<span data-ttu-id="fe331-380">Byte]</span><span class="sxs-lookup"><span data-stu-id="fe331-380">Byte[]</span></span> |
| <span data-ttu-id="fe331-381">tinyint</span><span class="sxs-lookup"><span data-stu-id="fe331-381">tinyint</span></span> |<span data-ttu-id="fe331-382">Bajtów</span><span class="sxs-lookup"><span data-stu-id="fe331-382">Byte</span></span> |
| <span data-ttu-id="fe331-383">Unikatowy identyfikator</span><span class="sxs-lookup"><span data-stu-id="fe331-383">uniqueidentifier</span></span> |<span data-ttu-id="fe331-384">Identyfikator GUID</span><span class="sxs-lookup"><span data-stu-id="fe331-384">Guid</span></span> |
| <span data-ttu-id="fe331-385">varbinary</span><span class="sxs-lookup"><span data-stu-id="fe331-385">varbinary</span></span> |<span data-ttu-id="fe331-386">Byte]</span><span class="sxs-lookup"><span data-stu-id="fe331-386">Byte[]</span></span> |
| <span data-ttu-id="fe331-387">varchar</span><span class="sxs-lookup"><span data-stu-id="fe331-387">varchar</span></span> |<span data-ttu-id="fe331-388">Ciąg, Char]</span><span class="sxs-lookup"><span data-stu-id="fe331-388">String, Char[]</span></span> |
| <span data-ttu-id="fe331-389">xml</span><span class="sxs-lookup"><span data-stu-id="fe331-389">xml</span></span> |<span data-ttu-id="fe331-390">XML</span><span class="sxs-lookup"><span data-stu-id="fe331-390">Xml</span></span> |

## <a name="map-source-toosink-columns"></a><span data-ttu-id="fe331-391">Mapowanie kolumny toosink źródłowe</span><span class="sxs-lookup"><span data-stu-id="fe331-391">Map source toosink columns</span></span>
<span data-ttu-id="fe331-392">toolearn o mapowanie kolumn w źródłowej toocolumns zestawu danych w zestawie danych zbiornika, zobacz [mapowania kolumnach dataset w fabryce danych Azure](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="fe331-392">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-copy"></a><span data-ttu-id="fe331-393">Kopiuj powtarzalne</span><span class="sxs-lookup"><span data-stu-id="fe331-393">Repeatable copy</span></span>
<span data-ttu-id="fe331-394">Podczas kopiowania danych tooSQL bazy danych serwera, działanie kopiowania hello dołącza tabeli ujścia toohello danych domyślnie.</span><span class="sxs-lookup"><span data-stu-id="fe331-394">When copying data tooSQL Server Database, hello copy activity appends data toohello sink table by default.</span></span> <span data-ttu-id="fe331-395">Zamiast tego zobacz tooperform UPSERT [tooSqlSink powtarzalne zapisu](data-factory-repeatable-copy.md#repeatable-write-to-sqlsink) artykułu.</span><span class="sxs-lookup"><span data-stu-id="fe331-395">tooperform an UPSERT instead,  See [Repeatable write tooSqlSink](data-factory-repeatable-copy.md#repeatable-write-to-sqlsink) article.</span></span> 

<span data-ttu-id="fe331-396">Podczas kopiowania danych z baz danych relacyjnych, zachowania powtarzalności w uwadze tooavoid niezamierzone wyników.</span><span class="sxs-lookup"><span data-stu-id="fe331-396">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="fe331-397">Fabryka danych Azure możesz ponownie ręcznie wycinek.</span><span class="sxs-lookup"><span data-stu-id="fe331-397">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="fe331-398">Można również skonfigurować zasady ponawiania dla zestawu danych, aby wycinek jest uruchamiany ponownie, gdy wystąpi błąd.</span><span class="sxs-lookup"><span data-stu-id="fe331-398">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="fe331-399">W przypadku wycinek zostanie uruchomiona ponownie w obu przypadkach, należy się upewnić, że hello tych samych danych toomake jest do odczytu niezależnie od tego, jak często wycinek jest uruchamiany.</span><span class="sxs-lookup"><span data-stu-id="fe331-399">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="fe331-400">Zobacz [Repeatable odczytywać źródłami relacyjnymi](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="fe331-400">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="fe331-401">Wydajność i dostrajania</span><span class="sxs-lookup"><span data-stu-id="fe331-401">Performance and Tuning</span></span>
<span data-ttu-id="fe331-402">Zobacz [wydajności działania kopiowania & dostrajanie przewodnik](data-factory-copy-activity-performance.md) toolearn o kluczu czynniki tego wydajność wpływ przenoszenia danych (działanie kopiowania) w usłudze fabryka danych Azure i różne sposoby toooptimize go.</span><span class="sxs-lookup"><span data-stu-id="fe331-402">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
