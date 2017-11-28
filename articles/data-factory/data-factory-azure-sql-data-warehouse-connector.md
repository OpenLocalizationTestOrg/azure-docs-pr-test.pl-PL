---
title: "aaaCopy danych do/z usługi Azure SQL Data Warehouse | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocopy danych do/z usługi Azure SQL Data Warehouse przy użyciu fabryki danych Azure"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: d90fa9bd-4b79-458a-8d40-e896835cfd4a
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: 75bfcf3c99844fc1297ca500107da23cf875e41f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tooand-from-azure-sql-data-warehouse-using-azure-data-factory"></a><span data-ttu-id="8e31e-103">Skopiuj tooand danych z usługi Azure SQL Data Warehouse przy użyciu fabryki danych Azure</span><span class="sxs-lookup"><span data-stu-id="8e31e-103">Copy data tooand from Azure SQL Data Warehouse using Azure Data Factory</span></span>
<span data-ttu-id="8e31e-104">W tym artykule opisano, jak toouse hello działanie kopiowania danych toomove fabryki danych Azure z usługą Magazyn danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="8e31e-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data to/from Azure SQL Data Warehouse.</span></span> <span data-ttu-id="8e31e-105">Opiera się na powitania [działań przepływu danych](data-factory-data-movement-activities.md) artykułu, który przedstawia ogólny przegląd przenoszenia danych z hello działanie kopiowania.</span><span class="sxs-lookup"><span data-stu-id="8e31e-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>  

> [!TIP]
> <span data-ttu-id="8e31e-106">tooachieve najlepszych wydajności, użyj programu PolyBase tooload danych do usługi Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="8e31e-106">tooachieve best performance, use PolyBase tooload data into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="8e31e-107">Witaj [Użyj programu PolyBase tooload danych do usługi Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#use-polybase-to-load-data-into-azure-sql-data-warehouse) sekcja zawiera szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="8e31e-107">hello [Use PolyBase tooload data into Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#use-polybase-to-load-data-into-azure-sql-data-warehouse) section has details.</span></span> <span data-ttu-id="8e31e-108">Aby uzyskać wskazówki z przypadkiem użycia, zobacz [załadować 1 TB do usługi Azure SQL Data Warehouse z fabryką danych Azure w obszarze 15 minut](data-factory-load-sql-data-warehouse.md).</span><span class="sxs-lookup"><span data-stu-id="8e31e-108">For a walkthrough with a use case, see [Load 1 TB into Azure SQL Data Warehouse under 15 minutes with Azure Data Factory](data-factory-load-sql-data-warehouse.md).</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="8e31e-109">Obsługiwane scenariusze</span><span class="sxs-lookup"><span data-stu-id="8e31e-109">Supported scenarios</span></span>
<span data-ttu-id="8e31e-110">Dane należy skopiować **z usługi Azure SQL Data Warehouse** toohello po magazynów danych:</span><span class="sxs-lookup"><span data-stu-id="8e31e-110">You can copy data **from Azure SQL Data Warehouse** toohello following data stores:</span></span>

[!INCLUDE [data-factory-supported-sinks](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="8e31e-111">Można skopiować danych z powitania po magazyny danych **tooAzure SQL Data Warehouse**:</span><span class="sxs-lookup"><span data-stu-id="8e31e-111">You can copy data from hello following data stores **tooAzure SQL Data Warehouse**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

> [!TIP]
> <span data-ttu-id="8e31e-112">Podczas kopiowania danych z tooAzure serwera SQL lub bazy danych SQL Azure SQL Data Warehouse, jeśli tabela hello nie istnieje w magazynie docelowym hello, fabryki danych może automatycznie tworzyć hello tabeli w usłudze SQL Data Warehouse za pomocą schematu hello hello tabeli w źródle hello Magazyn danych.</span><span class="sxs-lookup"><span data-stu-id="8e31e-112">When copying data from SQL Server or Azure SQL Database tooAzure SQL Data Warehouse, if hello table does not exist in hello destination store, Data Factory can automatically create hello table in SQL Data Warehouse by using hello schema of hello table in hello source data store.</span></span> <span data-ttu-id="8e31e-113">Zobacz [automatycznego tworzenia tabel](#auto-table-creation) szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="8e31e-113">See [Auto table creation](#auto-table-creation) for details.</span></span>

## <a name="supported-authentication-type"></a><span data-ttu-id="8e31e-114">Obsługiwany typ uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="8e31e-114">Supported authentication type</span></span>
<span data-ttu-id="8e31e-115">Azure SQL Data Warehouse łącznika Obsługa uwierzytelniania podstawowego.</span><span class="sxs-lookup"><span data-stu-id="8e31e-115">Azure SQL Data Warehouse connector support basic authentication.</span></span>

## <a name="getting-started"></a><span data-ttu-id="8e31e-116">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="8e31e-116">Getting started</span></span>
<span data-ttu-id="8e31e-117">Można utworzyć potok z działania kopiowania, który przenosi dane z usługi Azure SQL Data Warehouse przy użyciu różnych narzędzi/interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="8e31e-117">You can create a pipeline with a copy activity that moves data to/from an Azure SQL Data Warehouse by using different tools/APIs.</span></span>

<span data-ttu-id="8e31e-118">Witaj Najprostszym sposobem toocreate potok, który kopiuje dane z usługi Azure SQL Data Warehouse jest toouse hello kopiowania danych kreatora.</span><span class="sxs-lookup"><span data-stu-id="8e31e-118">hello easiest way toocreate a pipeline that copies data to/from Azure SQL Data Warehouse is toouse hello Copy data wizard.</span></span> <span data-ttu-id="8e31e-119">Zobacz [samouczek: ładowanie danych do usługi SQL Data Warehouse z fabryką danych](../sql-data-warehouse/sql-data-warehouse-load-with-data-factory.md) szybkie przewodnik dotyczący tworzenia potoku za pomocą Kreatora dane Kopiuj hello.</span><span class="sxs-lookup"><span data-stu-id="8e31e-119">See [Tutorial: Load data into SQL Data Warehouse with Data Factory](../sql-data-warehouse/sql-data-warehouse-load-with-data-factory.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="8e31e-120">Można również użyć hello następujące narzędzia toocreate potoku: **portalu Azure**, **programu Visual Studio**, **programu Azure PowerShell**, **szablonu usługi Azure Resource Manager** , **Interfejs API .NET**, i **interfejsu API REST**.</span><span class="sxs-lookup"><span data-stu-id="8e31e-120">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="8e31e-121">Zobacz [samouczek działania kopiowania](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) dla toocreate instrukcje krok po kroku potoku z działaniem kopiowania.</span><span class="sxs-lookup"><span data-stu-id="8e31e-121">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span>

<span data-ttu-id="8e31e-122">Czy za pomocą narzędzia hello lub interfejsów API, należy wykonać następujące kroki toocreate potok, który przenosi się, że magazyn danych ze źródła danych magazynu danych zbiornika tooa hello:</span><span class="sxs-lookup"><span data-stu-id="8e31e-122">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="8e31e-123">Utwórz **fabryki danych**.</span><span class="sxs-lookup"><span data-stu-id="8e31e-123">Create a **data factory**.</span></span> <span data-ttu-id="8e31e-124">Fabryka danych może zawierać co najmniej jeden potoków.</span><span class="sxs-lookup"><span data-stu-id="8e31e-124">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="8e31e-125">Utwórz **połączone usługi** toolink usługi fabryka danych tooyour magazynów danych wejściowych i wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="8e31e-125">Create **linked services** toolink input and output data stores tooyour data factory.</span></span> <span data-ttu-id="8e31e-126">Na przykład jeśli dane są kopiowane z magazynu danych Azure SQL tooan magazynu obiektów blob platformy Azure, utworzysz dwie toolink połączonych usług Twoje konto magazynu Azure i fabryki danych tooyour magazynu danych Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="8e31e-126">For example, if you are copying data from an Azure blob storage tooan Azure SQL data warehouse, you create two linked services toolink your Azure storage account and Azure SQL data warehouse tooyour data factory.</span></span> <span data-ttu-id="8e31e-127">Dla właściwości połączonej usługi, które są określone tooAzure SQL Data Warehouse, zobacz [połączona usługa właściwości](#linked-service-properties) sekcji.</span><span class="sxs-lookup"><span data-stu-id="8e31e-127">For linked service properties that are specific tooAzure SQL Data Warehouse, see [linked service properties](#linked-service-properties) section.</span></span> 
3. <span data-ttu-id="8e31e-128">Utwórz **zestawów danych** toorepresent wejściowe i wyjściowe dane hello operacji kopiowania.</span><span class="sxs-lookup"><span data-stu-id="8e31e-128">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> <span data-ttu-id="8e31e-129">Przykład Witaj wymienionych w ostatnim kroku hello służy do tworzenia kontenera obiektów blob hello toospecify zestawu danych i folderu zawierającego hello danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="8e31e-129">In hello example mentioned in hello last step, you create a dataset toospecify hello blob container and folder that contains hello input data.</span></span> <span data-ttu-id="8e31e-130">I utwórz inny zestaw danych toospecify hello tabeli w hello Azure SQL data warehouse przechowuje dane hello skopiowane z magazynu obiektów blob hello.</span><span class="sxs-lookup"><span data-stu-id="8e31e-130">And, you create another dataset toospecify hello table in hello Azure SQL data warehouse that holds hello data copied from hello blob storage.</span></span> <span data-ttu-id="8e31e-131">Dla właściwości zestawu danych, które są określone tooAzure SQL Data Warehouse, zobacz [właściwości zestawu danych](#dataset-properties) sekcji.</span><span class="sxs-lookup"><span data-stu-id="8e31e-131">For dataset properties that are specific tooAzure SQL Data Warehouse, see [dataset properties](#dataset-properties) section.</span></span>
4. <span data-ttu-id="8e31e-132">Utwórz **potoku** aktywnością kopiowania zestawu danych jako dane wejściowe i zestawu danych jako dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="8e31e-132">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="8e31e-133">W przykładzie hello wspomniano wcześniej używa BlobSource jako źródło i SqlDWSink jako zbiorniku dla aktywności kopiowania hello.</span><span class="sxs-lookup"><span data-stu-id="8e31e-133">In hello example mentioned earlier, you use BlobSource as a source and SqlDWSink as a sink for hello copy activity.</span></span> <span data-ttu-id="8e31e-134">Podobnie są kopiowane z usługi Azure SQL Data Warehouse tooAzure magazynu obiektów Blob, należy użyć SqlDWSource i BlobSink w przypadku działania kopiowania hello.</span><span class="sxs-lookup"><span data-stu-id="8e31e-134">Similarly, if you are copying from Azure SQL Data Warehouse tooAzure Blob Storage, you use SqlDWSource and BlobSink in hello copy activity.</span></span> <span data-ttu-id="8e31e-135">Dla właściwości działania kopiowania, które są określone tooAzure SQL Data Warehouse, zobacz [skopiować właściwości działania](#copy-activity-properties) sekcji.</span><span class="sxs-lookup"><span data-stu-id="8e31e-135">For copy activity properties that are specific tooAzure SQL Data Warehouse, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="8e31e-136">Szczegółowe informacje dotyczące sposobu toouse, Magazyn danych, jako źródło lub zbiorniku kliknij łącze hello w poprzedniej sekcji powitania dla magazynu danych.</span><span class="sxs-lookup"><span data-stu-id="8e31e-136">For details on how toouse a data store as a source or a sink, click hello link in hello previous section for your data store.</span></span>

<span data-ttu-id="8e31e-137">Korzystając z Kreatora hello, definicje JSON do tych jednostek fabryki danych (połączone usługi, zestawy danych i potoku hello) są tworzone automatycznie dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="8e31e-137">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="8e31e-138">Korzystając z narzędzi/API (z wyjątkiem interfejs API .NET), należy zdefiniować za pomocą formatu JSON hello tych jednostek fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="8e31e-138">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="8e31e-139">Dla przykładów z definicji JSON dla jednostek fabryki danych, które są używane toocopy danych do/z usługi Azure SQL Data Warehouse, zobacz [przykłady JSON](#json-examples-for-copying-data-to-and-from-sql-data-warehouse) sekcji tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="8e31e-139">For samples with JSON definitions for Data Factory entities that are used toocopy data to/from an Azure SQL Data Warehouse, see [JSON examples](#json-examples-for-copying-data-to-and-from-sql-data-warehouse) section of this article.</span></span>

<span data-ttu-id="8e31e-140">Witaj następujące sekcje zawierają szczegółowe informacje o właściwości JSON, które są używane toodefine fabryki danych jednostek określonych tooAzure SQL Data Warehouse:</span><span class="sxs-lookup"><span data-stu-id="8e31e-140">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooAzure SQL Data Warehouse:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="8e31e-141">Połączona usługa właściwości</span><span class="sxs-lookup"><span data-stu-id="8e31e-141">Linked service properties</span></span>
<span data-ttu-id="8e31e-142">Witaj w poniższej tabeli przedstawiono opis dla określonych tooAzure elementów JSON usługi SQL Data Warehouse połączone.</span><span class="sxs-lookup"><span data-stu-id="8e31e-142">hello following table provides description for JSON elements specific tooAzure SQL Data Warehouse linked service.</span></span>

| <span data-ttu-id="8e31e-143">Właściwość</span><span class="sxs-lookup"><span data-stu-id="8e31e-143">Property</span></span> | <span data-ttu-id="8e31e-144">Opis</span><span class="sxs-lookup"><span data-stu-id="8e31e-144">Description</span></span> | <span data-ttu-id="8e31e-145">Wymagane</span><span class="sxs-lookup"><span data-stu-id="8e31e-145">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8e31e-146">type</span><span class="sxs-lookup"><span data-stu-id="8e31e-146">type</span></span> |<span data-ttu-id="8e31e-147">musi mieć ustawioną właściwość type Hello: **AzureSqlDW**</span><span class="sxs-lookup"><span data-stu-id="8e31e-147">hello type property must be set to: **AzureSqlDW**</span></span> |<span data-ttu-id="8e31e-148">Tak</span><span class="sxs-lookup"><span data-stu-id="8e31e-148">Yes</span></span> |
| <span data-ttu-id="8e31e-149">Parametry połączenia</span><span class="sxs-lookup"><span data-stu-id="8e31e-149">connectionString</span></span> |<span data-ttu-id="8e31e-150">Określ informacje potrzebne wystąpienia usługi Azure SQL Data Warehouse toohello tooconnect hello właściwości connectionString.</span><span class="sxs-lookup"><span data-stu-id="8e31e-150">Specify information needed tooconnect toohello Azure SQL Data Warehouse instance for hello connectionString property.</span></span> <span data-ttu-id="8e31e-151">Obsługiwane jest tylko uwierzytelnianie podstawowe.</span><span class="sxs-lookup"><span data-stu-id="8e31e-151">Only basic authentication is supported.</span></span> |<span data-ttu-id="8e31e-152">Tak</span><span class="sxs-lookup"><span data-stu-id="8e31e-152">Yes</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="8e31e-153">Skonfiguruj [zapory bazy danych SQL Azure](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure) i hello serwera bazy danych za[Zezwól serwerowi hello tooaccess usług Azure](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure).</span><span class="sxs-lookup"><span data-stu-id="8e31e-153">Configure [Azure SQL Database Firewall](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure) and hello database server too[allow Azure Services tooaccess hello server](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure).</span></span> <span data-ttu-id="8e31e-154">Ponadto jeśli kopiujesz tooAzure danych magazynu danych SQL z poza tym Azure z lokalnych źródeł danych z bramą fabryki danych, należy skonfigurować odpowiedni zakres adresów IP dla maszyny hello, który wysyła dane tooAzure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="8e31e-154">Additionally, if you are copying data tooAzure SQL Data Warehouse from outside Azure including from on-premises data sources with data factory gateway, configure appropriate IP address range for hello machine that is sending data tooAzure SQL Data Warehouse.</span></span>

## <a name="dataset-properties"></a><span data-ttu-id="8e31e-155">Właściwości zestawu danych</span><span class="sxs-lookup"><span data-stu-id="8e31e-155">Dataset properties</span></span>
<span data-ttu-id="8e31e-156">Aby uzyskać pełną listę sekcje & właściwości dostępne do definiowania zestawów danych, zobacz hello [Tworzenie zbiorów danych](data-factory-create-datasets.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="8e31e-156">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="8e31e-157">Sekcje zawierają informacje, takie jak struktury, dostępności i zasad zestawu danych JSON są podobne dla wszystkich typów obiektów dataset (Azure SQL, obiektów blob platformy Azure, Azure tabeli itp.).</span><span class="sxs-lookup"><span data-stu-id="8e31e-157">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="8e31e-158">sekcja typeProperties Hello jest różne dla każdego typu zestawu danych i zawiera informacje o lokalizacji hello hello danych w magazynie danych hello.</span><span class="sxs-lookup"><span data-stu-id="8e31e-158">hello typeProperties section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="8e31e-159">Witaj **typeProperties** sekcja dla zestawu danych hello typu **AzureSqlDWTable** ma hello następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="8e31e-159">hello **typeProperties** section for hello dataset of type **AzureSqlDWTable** has hello following properties:</span></span>

| <span data-ttu-id="8e31e-160">Właściwość</span><span class="sxs-lookup"><span data-stu-id="8e31e-160">Property</span></span> | <span data-ttu-id="8e31e-161">Opis</span><span class="sxs-lookup"><span data-stu-id="8e31e-161">Description</span></span> | <span data-ttu-id="8e31e-162">Wymagane</span><span class="sxs-lookup"><span data-stu-id="8e31e-162">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8e31e-163">tableName</span><span class="sxs-lookup"><span data-stu-id="8e31e-163">tableName</span></span> |<span data-ttu-id="8e31e-164">Nazwa hello tabeli lub widoku w bazie danych Azure SQL Data Warehouse hello, który hello połączonej usługi odwołuje się do.</span><span class="sxs-lookup"><span data-stu-id="8e31e-164">Name of hello table or view in hello Azure SQL Data Warehouse database that hello linked service refers to.</span></span> |<span data-ttu-id="8e31e-165">Tak</span><span class="sxs-lookup"><span data-stu-id="8e31e-165">Yes</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="8e31e-166">Właściwości działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="8e31e-166">Copy activity properties</span></span>
<span data-ttu-id="8e31e-167">Pełną listę sekcje & właściwości dostępne do definiowania działań, zobacz hello [tworzenie potoków](data-factory-create-pipelines.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="8e31e-167">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="8e31e-168">Właściwości, takie jak nazwa, opis, dane wejściowe i wyjściowe tabel i zasady są dostępne dla wszystkich typów działań.</span><span class="sxs-lookup"><span data-stu-id="8e31e-168">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

> [!NOTE]
> <span data-ttu-id="8e31e-169">Witaj działanie kopiowania przyjmuje tylko jeden parametr wejściowy i tworzy tylko jedno wyjście.</span><span class="sxs-lookup"><span data-stu-id="8e31e-169">hello Copy Activity takes only one input and produces only one output.</span></span>

<span data-ttu-id="8e31e-170">Właściwości, które są dostępne w sekcji typeProperties hello działania hello różnić się z każdym typem działania.</span><span class="sxs-lookup"><span data-stu-id="8e31e-170">Whereas, properties available in hello typeProperties section of hello activity vary with each activity type.</span></span> <span data-ttu-id="8e31e-171">Dla działania kopiowania różnią się w zależności od typów hello źródeł i sink.</span><span class="sxs-lookup"><span data-stu-id="8e31e-171">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

### <a name="sqldwsource"></a><span data-ttu-id="8e31e-172">SqlDWSource</span><span class="sxs-lookup"><span data-stu-id="8e31e-172">SqlDWSource</span></span>
<span data-ttu-id="8e31e-173">Jeśli źródło jest typu **SqlDWSource**, dostępne są następujące właściwości hello **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="8e31e-173">When source is of type **SqlDWSource**, hello following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="8e31e-174">Właściwość</span><span class="sxs-lookup"><span data-stu-id="8e31e-174">Property</span></span> | <span data-ttu-id="8e31e-175">Opis</span><span class="sxs-lookup"><span data-stu-id="8e31e-175">Description</span></span> | <span data-ttu-id="8e31e-176">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="8e31e-176">Allowed values</span></span> | <span data-ttu-id="8e31e-177">Wymagane</span><span class="sxs-lookup"><span data-stu-id="8e31e-177">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="8e31e-178">sqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="8e31e-178">sqlReaderQuery</span></span> |<span data-ttu-id="8e31e-179">Użyj hello zapytanie niestandardowe tooread danych.</span><span class="sxs-lookup"><span data-stu-id="8e31e-179">Use hello custom query tooread data.</span></span> |<span data-ttu-id="8e31e-180">Ciąg zapytania SQL.</span><span class="sxs-lookup"><span data-stu-id="8e31e-180">SQL query string.</span></span> <span data-ttu-id="8e31e-181">Na przykład: Wybierz * z MyTable.</span><span class="sxs-lookup"><span data-stu-id="8e31e-181">For example: select * from MyTable.</span></span> |<span data-ttu-id="8e31e-182">Nie</span><span class="sxs-lookup"><span data-stu-id="8e31e-182">No</span></span> |
| <span data-ttu-id="8e31e-183">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="8e31e-183">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="8e31e-184">Nazwa hello przechowywane procedury, która odczytuje dane z hello tabeli źródłowej.</span><span class="sxs-lookup"><span data-stu-id="8e31e-184">Name of hello stored procedure that reads data from hello source table.</span></span> |<span data-ttu-id="8e31e-185">Nazwa hello procedury składowanej.</span><span class="sxs-lookup"><span data-stu-id="8e31e-185">Name of hello stored procedure.</span></span> <span data-ttu-id="8e31e-186">Witaj ostatniej instrukcji SQL musi być instrukcji SELECT w procedurze hello przechowywane.</span><span class="sxs-lookup"><span data-stu-id="8e31e-186">hello last SQL statement must be a SELECT statement in hello stored procedure.</span></span> |<span data-ttu-id="8e31e-187">Nie</span><span class="sxs-lookup"><span data-stu-id="8e31e-187">No</span></span> |
| <span data-ttu-id="8e31e-188">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="8e31e-188">storedProcedureParameters</span></span> |<span data-ttu-id="8e31e-189">Parametry hello procedury składowanej.</span><span class="sxs-lookup"><span data-stu-id="8e31e-189">Parameters for hello stored procedure.</span></span> |<span data-ttu-id="8e31e-190">Par nazwa/wartość.</span><span class="sxs-lookup"><span data-stu-id="8e31e-190">Name/value pairs.</span></span> <span data-ttu-id="8e31e-191">Nazwy i wielkość liter w wyrazie parametry muszą być zgodne, hello nazwy i parametry procedury przechowywane hello wielkości liter.</span><span class="sxs-lookup"><span data-stu-id="8e31e-191">Names and casing of parameters must match hello names and casing of hello stored procedure parameters.</span></span> |<span data-ttu-id="8e31e-192">Nie</span><span class="sxs-lookup"><span data-stu-id="8e31e-192">No</span></span> |

<span data-ttu-id="8e31e-193">Jeśli hello **sqlReaderQuery** określono hello SqlDWSource, hello odbywa się działanie kopii tego zapytania względem hello Azure SQL Data Warehouse źródła tooget hello danych.</span><span class="sxs-lookup"><span data-stu-id="8e31e-193">If hello **sqlReaderQuery** is specified for hello SqlDWSource, hello Copy Activity runs this query against hello Azure SQL Data Warehouse source tooget hello data.</span></span>

<span data-ttu-id="8e31e-194">Alternatywnie można określić procedury składowanej, określając hello **sqlReaderStoredProcedureName** i **storedProcedureParameters** (jeśli hello procedura składowana pobiera parametry).</span><span class="sxs-lookup"><span data-stu-id="8e31e-194">Alternatively, you can specify a stored procedure by specifying hello **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if hello stored procedure takes parameters).</span></span>

<span data-ttu-id="8e31e-195">Jeśli nie określisz sqlReaderQuery lub sqlReaderStoredProcedureName hello kolumn zdefiniowanych w sekcji Struktura hello hello zestawu danych JSON są używane toobuild toorun zapytania względem hello Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="8e31e-195">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, hello columns defined in hello structure section of hello dataset JSON are used toobuild a query toorun against hello Azure SQL Data Warehouse.</span></span> <span data-ttu-id="8e31e-196">Przykład: `select column1, column2 from mytable`.</span><span class="sxs-lookup"><span data-stu-id="8e31e-196">Example: `select column1, column2 from mytable`.</span></span> <span data-ttu-id="8e31e-197">Jeśli hello definicji zestawu danych nie ma on struktury hello, wszystkie kolumny są wybierane w tabeli hello.</span><span class="sxs-lookup"><span data-stu-id="8e31e-197">If hello dataset definition does not have hello structure, all columns are selected from hello table.</span></span>

#### <a name="sqldwsource-example"></a><span data-ttu-id="8e31e-198">Przykład SqlDWSource</span><span class="sxs-lookup"><span data-stu-id="8e31e-198">SqlDWSource example</span></span>

```JSON
"source": {
    "type": "SqlDWSource",
    "sqlReaderStoredProcedureName": "CopyTestSrcStoredProcedureWithParameters",
    "storedProcedureParameters": {
        "stringData": { "value": "str3" },
        "identifier": { "value": "$$Text.Format('{0:yyyy}', SliceStart)", "type": "Int"}
    }
}
```
<span data-ttu-id="8e31e-199">**Definicja procedury przechowywane Hello:**</span><span class="sxs-lookup"><span data-stu-id="8e31e-199">**hello stored procedure definition:**</span></span>

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

### <a name="sqldwsink"></a><span data-ttu-id="8e31e-200">SqlDWSink</span><span class="sxs-lookup"><span data-stu-id="8e31e-200">SqlDWSink</span></span>
<span data-ttu-id="8e31e-201">**SqlDWSink** obsługuje hello następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="8e31e-201">**SqlDWSink** supports hello following properties:</span></span>

| <span data-ttu-id="8e31e-202">Właściwość</span><span class="sxs-lookup"><span data-stu-id="8e31e-202">Property</span></span> | <span data-ttu-id="8e31e-203">Opis</span><span class="sxs-lookup"><span data-stu-id="8e31e-203">Description</span></span> | <span data-ttu-id="8e31e-204">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="8e31e-204">Allowed values</span></span> | <span data-ttu-id="8e31e-205">Wymagane</span><span class="sxs-lookup"><span data-stu-id="8e31e-205">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="8e31e-206">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="8e31e-206">sqlWriterCleanupScript</span></span> |<span data-ttu-id="8e31e-207">Określ kwerendę dla działania kopiowania tooexecute tak, aby dane określonych wycinek jest wyczyszczone.</span><span class="sxs-lookup"><span data-stu-id="8e31e-207">Specify a query for Copy Activity tooexecute such that data of a specific slice is cleaned up.</span></span> <span data-ttu-id="8e31e-208">Aby uzyskać więcej informacji, zobacz [sekcji powtarzalności](#repeatability-during-copy).</span><span class="sxs-lookup"><span data-stu-id="8e31e-208">For details, see [repeatability section](#repeatability-during-copy).</span></span> |<span data-ttu-id="8e31e-209">Instrukcja zapytania.</span><span class="sxs-lookup"><span data-stu-id="8e31e-209">A query statement.</span></span> |<span data-ttu-id="8e31e-210">Nie</span><span class="sxs-lookup"><span data-stu-id="8e31e-210">No</span></span> |
| <span data-ttu-id="8e31e-211">allowPolyBase</span><span class="sxs-lookup"><span data-stu-id="8e31e-211">allowPolyBase</span></span> |<span data-ttu-id="8e31e-212">Wskazuje, czy toouse PolyBase (jeśli jest to wymagane) zamiast BULKINSERT mechanizmu.</span><span class="sxs-lookup"><span data-stu-id="8e31e-212">Indicates whether toouse PolyBase (when applicable) instead of BULKINSERT mechanism.</span></span> <br/><br/> <span data-ttu-id="8e31e-213">**Przy użyciu programu PolyBase jest hello zalecany sposób tooload danych do usługi SQL Data Warehouse.**</span><span class="sxs-lookup"><span data-stu-id="8e31e-213">**Using PolyBase is hello recommended way tooload data into SQL Data Warehouse.**</span></span> <span data-ttu-id="8e31e-214">Zobacz [Użyj programu PolyBase tooload danych do usługi Azure SQL Data Warehouse](#use-polybase-to-load-data-into-azure-sql-data-warehouse) sekcji dla ograniczenia i szczegółów.</span><span class="sxs-lookup"><span data-stu-id="8e31e-214">See [Use PolyBase tooload data into Azure SQL Data Warehouse](#use-polybase-to-load-data-into-azure-sql-data-warehouse) section for constraints and details.</span></span> |<span data-ttu-id="8e31e-215">True</span><span class="sxs-lookup"><span data-stu-id="8e31e-215">True</span></span> <br/><span data-ttu-id="8e31e-216">Wartość FAŁSZ (ustawienie domyślne)</span><span class="sxs-lookup"><span data-stu-id="8e31e-216">False (default)</span></span> |<span data-ttu-id="8e31e-217">Nie</span><span class="sxs-lookup"><span data-stu-id="8e31e-217">No</span></span> |
| <span data-ttu-id="8e31e-218">Usługi</span><span class="sxs-lookup"><span data-stu-id="8e31e-218">polyBaseSettings</span></span> |<span data-ttu-id="8e31e-219">Grupa właściwości, które można określić podczas hello **allowPolybase** właściwość jest ustawiona zbyt**true**.</span><span class="sxs-lookup"><span data-stu-id="8e31e-219">A group of properties that can be specified when hello **allowPolybase** property is set too**true**.</span></span> |&nbsp; |<span data-ttu-id="8e31e-220">Nie</span><span class="sxs-lookup"><span data-stu-id="8e31e-220">No</span></span> |
| <span data-ttu-id="8e31e-221">rejectValue</span><span class="sxs-lookup"><span data-stu-id="8e31e-221">rejectValue</span></span> |<span data-ttu-id="8e31e-222">Określa numer hello lub procent wierszy, które można odrzucić przed hello działanie nie powiodło się.</span><span class="sxs-lookup"><span data-stu-id="8e31e-222">Specifies hello number or percentage of rows that can be rejected before hello query fails.</span></span> <br/><br/><span data-ttu-id="8e31e-223">Dowiedz się więcej na temat hello PolyBase Odrzuć opcje w hello **argumenty** sekcji [Tworzenie tabeli zewnętrznej (Transact-SQL)](https://msdn.microsoft.com/library/dn935021.aspx) tematu.</span><span class="sxs-lookup"><span data-stu-id="8e31e-223">Learn more about hello PolyBase’s reject options in hello **Arguments** section of [CREATE EXTERNAL TABLE (Transact-SQL)](https://msdn.microsoft.com/library/dn935021.aspx) topic.</span></span> |<span data-ttu-id="8e31e-224">0 (domyślnie), 1, 2...</span><span class="sxs-lookup"><span data-stu-id="8e31e-224">0 (default), 1, 2, …</span></span> |<span data-ttu-id="8e31e-225">Nie</span><span class="sxs-lookup"><span data-stu-id="8e31e-225">No</span></span> |
| <span data-ttu-id="8e31e-226">dla właściwości rejectType</span><span class="sxs-lookup"><span data-stu-id="8e31e-226">rejectType</span></span> |<span data-ttu-id="8e31e-227">Określa, czy opcja rejectValue hello jest określona jako wartość literału lub wartość procentowa.</span><span class="sxs-lookup"><span data-stu-id="8e31e-227">Specifies whether hello rejectValue option is specified as a literal value or a percentage.</span></span> |<span data-ttu-id="8e31e-228">Wartość (ustawienie domyślne), wartość procentowa</span><span class="sxs-lookup"><span data-stu-id="8e31e-228">Value (default), Percentage</span></span> |<span data-ttu-id="8e31e-229">Nie</span><span class="sxs-lookup"><span data-stu-id="8e31e-229">No</span></span> |
| <span data-ttu-id="8e31e-230">rejectSampleValue</span><span class="sxs-lookup"><span data-stu-id="8e31e-230">rejectSampleValue</span></span> |<span data-ttu-id="8e31e-231">Określa liczbę hello tooretrieve wierszy przed hello PolyBase ponownie oblicza hello procent odrzuconych wierszy.</span><span class="sxs-lookup"><span data-stu-id="8e31e-231">Determines hello number of rows tooretrieve before hello PolyBase recalculates hello percentage of rejected rows.</span></span> |<span data-ttu-id="8e31e-232">1, 2, …</span><span class="sxs-lookup"><span data-stu-id="8e31e-232">1, 2, …</span></span> |<span data-ttu-id="8e31e-233">Tak, jeśli **dla właściwości rejectType** jest **procent**</span><span class="sxs-lookup"><span data-stu-id="8e31e-233">Yes, if **rejectType** is **percentage**</span></span> |
| <span data-ttu-id="8e31e-234">useTypeDefault</span><span class="sxs-lookup"><span data-stu-id="8e31e-234">useTypeDefault</span></span> |<span data-ttu-id="8e31e-235">Określa, jak toohandle brakujących wartości w rozdzielane pliki tekstowe po programie PolyBase pobiera dane z pliku tekstowego hello.</span><span class="sxs-lookup"><span data-stu-id="8e31e-235">Specifies how toohandle missing values in delimited text files when PolyBase retrieves data from hello text file.</span></span><br/><br/><span data-ttu-id="8e31e-236">Dowiedz się więcej o tej właściwości z sekcji argumenty hello w [utworzyć EXTERNAL FILE FORMAT (Transact-SQL)](https://msdn.microsoft.com/library/dn935026.aspx).</span><span class="sxs-lookup"><span data-stu-id="8e31e-236">Learn more about this property from hello Arguments section in [CREATE EXTERNAL FILE FORMAT (Transact-SQL)](https://msdn.microsoft.com/library/dn935026.aspx).</span></span> |<span data-ttu-id="8e31e-237">Wartość true, False (ustawienie domyślne)</span><span class="sxs-lookup"><span data-stu-id="8e31e-237">True, False (default)</span></span> |<span data-ttu-id="8e31e-238">Nie</span><span class="sxs-lookup"><span data-stu-id="8e31e-238">No</span></span> |
| <span data-ttu-id="8e31e-239">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="8e31e-239">writeBatchSize</span></span> |<span data-ttu-id="8e31e-240">Wstawia dane do tabeli SQL hello, gdy osiągnie rozmiar buforu hello writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="8e31e-240">Inserts data into hello SQL table when hello buffer size reaches writeBatchSize</span></span> |<span data-ttu-id="8e31e-241">Liczba całkowita (liczba wierszy)</span><span class="sxs-lookup"><span data-stu-id="8e31e-241">Integer (number of rows)</span></span> |<span data-ttu-id="8e31e-242">Nie (domyślne: 10000)</span><span class="sxs-lookup"><span data-stu-id="8e31e-242">No (default: 10000)</span></span> |
| <span data-ttu-id="8e31e-243">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="8e31e-243">writeBatchTimeout</span></span> |<span data-ttu-id="8e31e-244">Czas toocomplete operacji wstawiania wsadowego hello oczekiwania, zanim upłynie limit czasu.</span><span class="sxs-lookup"><span data-stu-id="8e31e-244">Wait time for hello batch insert operation toocomplete before it times out.</span></span> |<span data-ttu-id="8e31e-245">Zakres czasu</span><span class="sxs-lookup"><span data-stu-id="8e31e-245">timespan</span></span><br/><br/> <span data-ttu-id="8e31e-246">Przykład: "00: 30:00" (30 minut).</span><span class="sxs-lookup"><span data-stu-id="8e31e-246">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="8e31e-247">Nie</span><span class="sxs-lookup"><span data-stu-id="8e31e-247">No</span></span> |

#### <a name="sqldwsink-example"></a><span data-ttu-id="8e31e-248">Przykład SqlDWSink</span><span class="sxs-lookup"><span data-stu-id="8e31e-248">SqlDWSink example</span></span>

```JSON
"sink": {
    "type": "SqlDWSink",
    "allowPolyBase": true
}
```

## <a name="use-polybase-tooload-data-into-azure-sql-data-warehouse"></a><span data-ttu-id="8e31e-249">Użyj programu PolyBase tooload danych do magazynu danych SQL Azure</span><span class="sxs-lookup"><span data-stu-id="8e31e-249">Use PolyBase tooload data into Azure SQL Data Warehouse</span></span>
<span data-ttu-id="8e31e-250">Przy użyciu  **[PolyBase](https://docs.microsoft.com/sql/relational-databases/polybase/polybase-guide)**  jest wydajny sposób ładowania dużych ilości danych do magazynu danych SQL Azure z wysokiej przepływności.</span><span class="sxs-lookup"><span data-stu-id="8e31e-250">Using **[PolyBase](https://docs.microsoft.com/sql/relational-databases/polybase/polybase-guide)** is an efficient way of loading large amount of data into Azure SQL Data Warehouse with high throughput.</span></span> <span data-ttu-id="8e31e-251">Widać duże korzyści hello przepływność przy użyciu programu PolyBase zamiast hello domyślnego mechanizmu BULKINSERT.</span><span class="sxs-lookup"><span data-stu-id="8e31e-251">You can see a large gain in hello throughput by using PolyBase instead of hello default BULKINSERT mechanism.</span></span> <span data-ttu-id="8e31e-252">Zobacz [skopiuj numer odwołania wydajności](data-factory-copy-activity-performance.md#performance-reference) z szczegółowe porównanie.</span><span class="sxs-lookup"><span data-stu-id="8e31e-252">See [copy performance reference number](data-factory-copy-activity-performance.md#performance-reference) with detailed comparison.</span></span> <span data-ttu-id="8e31e-253">Aby uzyskać wskazówki z przypadkiem użycia, zobacz [załadować 1 TB do usługi Azure SQL Data Warehouse z fabryką danych Azure w obszarze 15 minut](data-factory-load-sql-data-warehouse.md).</span><span class="sxs-lookup"><span data-stu-id="8e31e-253">For a walkthrough with a use case, see [Load 1 TB into Azure SQL Data Warehouse under 15 minutes with Azure Data Factory](data-factory-load-sql-data-warehouse.md).</span></span>

* <span data-ttu-id="8e31e-254">Jeśli źródło danych jest w **obiektów Blob platformy Azure lub usługi Azure Data Lake Store**i hello format jest zgodny z PolyBase, możesz bezpośrednio skopiować tooAzure SQL Data Warehouse przy użyciu programu PolyBase.</span><span class="sxs-lookup"><span data-stu-id="8e31e-254">If your source data is in **Azure Blob or Azure Data Lake Store**, and hello format is compatible with PolyBase, you can directly copy tooAzure SQL Data Warehouse using PolyBase.</span></span> <span data-ttu-id="8e31e-255">Zobacz  **[bezpośrednich kopii przy użyciu programu PolyBase](#direct-copy-using-polybase)**  ze szczegółami.</span><span class="sxs-lookup"><span data-stu-id="8e31e-255">See **[Direct copy using PolyBase](#direct-copy-using-polybase)** with details.</span></span>
* <span data-ttu-id="8e31e-256">Jeśli Twoje źródła magazynu danych i format nie jest początkowo obsługiwana przez aparat PolyBase, możesz użyć hello  **[przemieszczane kopiowania przy użyciu programu PolyBase](#staged-copy-using-polybase)**  funkcji zamiast tego.</span><span class="sxs-lookup"><span data-stu-id="8e31e-256">If your source data store and format is not originally supported by PolyBase, you can use hello **[Staged Copy using PolyBase](#staged-copy-using-polybase)** feature instead.</span></span> <span data-ttu-id="8e31e-257">Udostępnia również możesz lepszą przepustowość automatycznie konwersji danych hello na format zgodny PolyBase i przechowywanie danych hello w magazynie obiektów Blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="8e31e-257">It also provides you better throughput by automatically converting hello data into PolyBase-compatible format and storing hello data in Azure Blob storage.</span></span> <span data-ttu-id="8e31e-258">Następnie ładuje dane do usługi SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="8e31e-258">It then loads data into SQL Data Warehouse.</span></span>

<span data-ttu-id="8e31e-259">Zestaw hello `allowPolyBase` właściwości zbyt**true** pokazane na powitania poniższy przykład dla fabryki danych Azure toouse PolyBase toocopy danych do usługi Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="8e31e-259">Set hello `allowPolyBase` property too**true** as shown in hello following example for Azure Data Factory toouse PolyBase toocopy data into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="8e31e-260">Po ustawieniu allowPolyBase tootrue można określić właściwości specyficzne dla programu PolyBase przy użyciu hello `polyBaseSettings` grupy właściwości.</span><span class="sxs-lookup"><span data-stu-id="8e31e-260">When you set allowPolyBase tootrue, you can specify PolyBase specific properties using hello `polyBaseSettings` property group.</span></span> <span data-ttu-id="8e31e-261">Zobacz hello [SqlDWSink](#SqlDWSink) sekcji, aby uzyskać więcej informacji o właściwościach, które mogą korzystać z usługi.</span><span class="sxs-lookup"><span data-stu-id="8e31e-261">see hello [SqlDWSink](#SqlDWSink) section for details about properties that you can use with polyBaseSettings.</span></span>

```JSON
"sink": {
    "type": "SqlDWSink",
    "allowPolyBase": true,
    "polyBaseSettings":
    {
        "rejectType": "percentage",
        "rejectValue": 10.0,
        "rejectSampleValue": 100,
        "useTypeDefault": true
    }
}
```

### <a name="direct-copy-using-polybase"></a><span data-ttu-id="8e31e-262">Bezpośrednie kopiowania przy użyciu programu PolyBase</span><span class="sxs-lookup"><span data-stu-id="8e31e-262">Direct copy using PolyBase</span></span>
<span data-ttu-id="8e31e-263">Aparat PolyBase magazynu danych SQL obsługuje bezpośrednio obiektów Blob platformy Azure i usługi Azure Data Lake Store (przy użyciu nazwy głównej usługi) jako źródło i wymagania format określonego pliku.</span><span class="sxs-lookup"><span data-stu-id="8e31e-263">SQL Data Warehouse PolyBase directly support Azure Blob and Azure Data Lake Store (using service principal) as source and with specific file format requirements.</span></span> <span data-ttu-id="8e31e-264">Jeśli źródło danych spełnia kryteria hello opisane w tej sekcji, możesz skopiować bezpośrednio ze źródła danych magazynu tooAzure, który SQL Data Warehouse przy użyciu programu PolyBase.</span><span class="sxs-lookup"><span data-stu-id="8e31e-264">If your source data meets hello criteria described in this section, you can directly copy from source data store tooAzure SQL Data Warehouse using PolyBase.</span></span> <span data-ttu-id="8e31e-265">W przeciwnym razie można użyć [przemieszczane kopiowania przy użyciu programu PolyBase](#staged-copy-using-polybase).</span><span class="sxs-lookup"><span data-stu-id="8e31e-265">Otherwise, you can use [Staged Copy using PolyBase](#staged-copy-using-polybase).</span></span>

> [!TIP]
> <span data-ttu-id="8e31e-266">toocopy dane z usługi Data Lake Store tooSQL hurtowni danych, Dowiedz się więcej o [fabryki danych Azure ułatwia nawet łatwiejsze i wygodne toouncover wgląd w dane dotyczące danych podczas korzystania z usługi Data Lake Store z usługi SQL Data Warehouse](https://blogs.msdn.microsoft.com/azuredatalake/2017/04/08/azure-data-factory-makes-it-even-easier-and-convenient-to-uncover-insights-from-data-when-using-data-lake-store-with-sql-data-warehouse/).</span><span class="sxs-lookup"><span data-stu-id="8e31e-266">toocopy data from Data Lake Store tooSQL Data Warehouse efficiently, learn more from [Azure Data Factory makes it even easier and convenient toouncover insights from data when using Data Lake Store with SQL Data Warehouse](https://blogs.msdn.microsoft.com/azuredatalake/2017/04/08/azure-data-factory-makes-it-even-easier-and-convenient-to-uncover-insights-from-data-when-using-data-lake-store-with-sql-data-warehouse/).</span></span>

<span data-ttu-id="8e31e-267">Jeśli nie są spełnione wymagania hello, fabryki danych Azure sprawdza ustawienia hello i automatycznie powraca mechanizm BULKINSERT toohello hello przenoszenia danych.</span><span class="sxs-lookup"><span data-stu-id="8e31e-267">If hello requirements are not met, Azure Data Factory checks hello settings and automatically falls back toohello BULKINSERT mechanism for hello data movement.</span></span>

1. <span data-ttu-id="8e31e-268">**Źródło połączona usługa** jest typu: **AzureStorage** lub **AzureDataLakeStore z uwierzytelnianiem główna usługi**.</span><span class="sxs-lookup"><span data-stu-id="8e31e-268">**Source linked service** is of type: **AzureStorage** or **AzureDataLakeStore with service principal authentication**.</span></span>  
2. <span data-ttu-id="8e31e-269">Witaj **wejściowy zestaw danych** jest typu: **AzureBlob** lub **AzureDataLakeStore**, i hello typ formatu w obszarze `type` właściwości **OrcFormat** , lub **TextFormat** z hello następujące konfiguracje:</span><span class="sxs-lookup"><span data-stu-id="8e31e-269">hello **input dataset** is of type: **AzureBlob** or **AzureDataLakeStore**, and hello format type under `type` properties is **OrcFormat**, or **TextFormat** with hello following configurations:</span></span>

   1. <span data-ttu-id="8e31e-270">`rowDelimiter`musi być  **\n** .</span><span class="sxs-lookup"><span data-stu-id="8e31e-270">`rowDelimiter` must be **\n**.</span></span>
   2. <span data-ttu-id="8e31e-271">`nullValue`ustawiono zbyt**pusty ciąg** (""), lub `treatEmptyAsNull` ustawiono zbyt**true**.</span><span class="sxs-lookup"><span data-stu-id="8e31e-271">`nullValue` is set too**empty string** (""), or `treatEmptyAsNull` is set too**true**.</span></span>
   3. <span data-ttu-id="8e31e-272">`encodingName`ustawiono zbyt**utf-8**, która jest **domyślne** wartość.</span><span class="sxs-lookup"><span data-stu-id="8e31e-272">`encodingName` is set too**utf-8**, which is **default** value.</span></span>
   4. <span data-ttu-id="8e31e-273">`escapeChar`, `quoteChar`, `firstRowAsHeader`, i `skipLineCount` nie zostały określone.</span><span class="sxs-lookup"><span data-stu-id="8e31e-273">`escapeChar`, `quoteChar`, `firstRowAsHeader`, and `skipLineCount` are not specified.</span></span>
   5. <span data-ttu-id="8e31e-274">`compression`może być **bez kompresji**, **GZip**, lub **Deflate**.</span><span class="sxs-lookup"><span data-stu-id="8e31e-274">`compression` can be **no compression**, **GZip**, or **Deflate**.</span></span>

    ```JSON
    "typeProperties": {
       "folderPath": "<blobpath>",
       "format": {
           "type": "TextFormat",     
           "columnDelimiter": "<any delimiter>",
           "rowDelimiter": "\n",       
           "nullValue": "",           
           "encodingName": "utf-8"    
       },
       "compression": {  
           "type": "GZip",  
           "level": "Optimal"  
       }  
    },
    ```

3. <span data-ttu-id="8e31e-275">Brak nie `skipHeaderLineCount` w obszarze **BlobSource** lub **AzureDataLakeStore** dla hello działanie kopiowania w potoku hello.</span><span class="sxs-lookup"><span data-stu-id="8e31e-275">There is no `skipHeaderLineCount` setting under **BlobSource** or **AzureDataLakeStore** for hello Copy activity in hello pipeline.</span></span>
4. <span data-ttu-id="8e31e-276">Brak nie `sliceIdentifierColumnName` w obszarze **SqlDWSink** dla hello działanie kopiowania w potoku hello.</span><span class="sxs-lookup"><span data-stu-id="8e31e-276">There is no `sliceIdentifierColumnName` setting under **SqlDWSink** for hello Copy activity in hello pipeline.</span></span> <span data-ttu-id="8e31e-277">(PolyBase gwarantuje, że wszystkie dane są aktualizowane lub nic nie jest aktualizowana w jednym przebiegu.</span><span class="sxs-lookup"><span data-stu-id="8e31e-277">(PolyBase guarantees that all data is updated or nothing is updated in a single run.</span></span> <span data-ttu-id="8e31e-278">tooachieve **powtarzalności**, można użyć `sqlWriterCleanupScript`).</span><span class="sxs-lookup"><span data-stu-id="8e31e-278">tooachieve **repeatability**, you could use `sqlWriterCleanupScript`).</span></span>
5. <span data-ttu-id="8e31e-279">Brak nie `columnMapping` używany w hello skojarzony w przypadku działania kopiowania.</span><span class="sxs-lookup"><span data-stu-id="8e31e-279">There is no `columnMapping` being used in hello associated in Copy activity.</span></span>

### <a name="staged-copy-using-polybase"></a><span data-ttu-id="8e31e-280">Kopiuj przygotowanego przy użyciu programu PolyBase</span><span class="sxs-lookup"><span data-stu-id="8e31e-280">Staged Copy using PolyBase</span></span>
<span data-ttu-id="8e31e-281">Źródło danych nie spełnia kryteriów hello wprowadzone w poprzedniej sekcji hello, umożliwia kopiowanie danych za pośrednictwem tymczasowego przemieszczania magazynu obiektów Blob Azure (nie może być magazyn w warstwie Premium).</span><span class="sxs-lookup"><span data-stu-id="8e31e-281">When your source data doesn’t meet hello criteria introduced in hello previous section, you can enable copying data via an interim staging Azure Blob Storage (cannot be Premium Storage).</span></span> <span data-ttu-id="8e31e-282">W takim przypadku fabryki danych Azure automatycznie wykonuje przekształcenia na powitania toomeet dane formatu wymagania dotyczące danych PolyBase, a następnie użyj programu PolyBase tooload danych do usługi SQL Data Warehouse i ostatnio oczyszczania tymczasowego danych z magazynu obiektów Blob hello.</span><span class="sxs-lookup"><span data-stu-id="8e31e-282">In this case, Azure Data Factory automatically performs transformations on hello data toomeet data format requirements of PolyBase, then use PolyBase tooload data into SQL Data Warehouse, and at last clean-up your temp data from hello Blob storage.</span></span> <span data-ttu-id="8e31e-283">Zobacz [przemieszczane kopiowania](data-factory-copy-activity-performance.md#staged-copy) szczegółowe informacje na temat jak kopiowanie danych za pośrednictwem tymczasowych obiektów Blob platformy Azure działa na ogół.</span><span class="sxs-lookup"><span data-stu-id="8e31e-283">See [Staged Copy](data-factory-copy-activity-performance.md#staged-copy) for details on how copying data via a staging Azure Blob works in general.</span></span>

> [!NOTE]
> <span data-ttu-id="8e31e-284">Podczas kopiowania danych z danych z lokalnego magazynu do usługi Azure SQL Data Warehouse przy użyciu programu PolyBase i przemieszczania, jeśli wersja bramy zarządzania danymi znajduje się poniżej 2.4 środowiska JRE (Java Runtime Environment) jest wymagane dla bramy komputera, który jest używany tootransform źródło danych do prawidłowego formatu.</span><span class="sxs-lookup"><span data-stu-id="8e31e-284">When copying data from an on-prem data store into Azure SQL Data Warehouse using PolyBase and staging, if your Data Management Gateway version is below 2.4, JRE (Java Runtime Environment) is required on your gateway machine that is used tootransform your source data into proper format.</span></span> <span data-ttu-id="8e31e-285">Sugerują, że uaktualnienie najnowszej bramy tooavoid w toohello tych zależności.</span><span class="sxs-lookup"><span data-stu-id="8e31e-285">Suggest you upgrade your gateway toohello latest tooavoid such dependency.</span></span>
>

<span data-ttu-id="8e31e-286">toouse tej funkcji, Utwórz [połączonej usługi magazynu Azure](data-factory-azure-blob-connector.md#azure-storage-linked-service) przywołujący toohello konta magazynu Azure, które ma hello tymczasowego obiektu blob magazynu, następnie określ hello `enableStaging` i `stagingSettings` właściwości hello działanie kopiowania jak pokazano w hello następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="8e31e-286">toouse this feature, create an [Azure Storage linked service](data-factory-azure-blob-connector.md#azure-storage-linked-service) that refers toohello Azure Storage Account that has hello interim blob storage, then specify hello `enableStaging` and `stagingSettings` properties for hello Copy Activity as shown in hello following code:</span></span>

```json
"activities":[  
{
    "name": "Sample copy activity from SQL Server tooSQL Data Warehouse via PolyBase",
    "type": "Copy",
    "inputs": [{ "name": "OnpremisesSQLServerInput" }],
    "outputs": [{ "name": "AzureSQLDWOutput" }],
    "typeProperties": {
        "source": {
            "type": "SqlSource",
        },
        "sink": {
            "type": "SqlDwSink",
            "allowPolyBase": true
        },
        "enableStaging": true,
        "stagingSettings": {
            "linkedServiceName": "MyStagingBlob"
        }
    }
}
]
```

## <a name="best-practices-when-using-polybase"></a><span data-ttu-id="8e31e-287">Najlepsze rozwiązania w sytuacji, gdy przy użyciu programu PolyBase</span><span class="sxs-lookup"><span data-stu-id="8e31e-287">Best practices when using PolyBase</span></span>
<span data-ttu-id="8e31e-288">Witaj poniższe sekcje zawierają dodatkowe toohello najlepsze praktyki te, które są wymienione w [najlepsze rozwiązania dotyczące usługi Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="8e31e-288">hello following sections provide additional best practices toohello ones that are mentioned in [Best practices for Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-best-practices.md).</span></span>

### <a name="required-database-permission"></a><span data-ttu-id="8e31e-289">Uprawnienia wymagane bazy danych</span><span class="sxs-lookup"><span data-stu-id="8e31e-289">Required database permission</span></span>
<span data-ttu-id="8e31e-290">toouse PolyBase wymaga hello użytkownika jest tooload używane dane do usługi SQL Data Warehouse ma hello [uprawnienia "CONTROL"](https://msdn.microsoft.com/library/ms191291.aspx) na powitania docelowej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="8e31e-290">toouse PolyBase, it requires hello user being used tooload data into SQL Data Warehouse has hello ["CONTROL" permission](https://msdn.microsoft.com/library/ms191291.aspx) on hello target database.</span></span> <span data-ttu-id="8e31e-291">Jednym ze sposobów tooachieve, który jest tooadd ten użytkownik jest członkiem roli "db_owner".</span><span class="sxs-lookup"><span data-stu-id="8e31e-291">One way tooachieve that is tooadd that user as a member of "db_owner" role.</span></span> <span data-ttu-id="8e31e-292">Dowiedz się, jak toodo który wykonując [w tej sekcji](../sql-data-warehouse/sql-data-warehouse-overview-manage-security.md#authorization).</span><span class="sxs-lookup"><span data-stu-id="8e31e-292">Learn how toodo that by following [this section](../sql-data-warehouse/sql-data-warehouse-overview-manage-security.md#authorization).</span></span>

### <a name="row-size-and-data-type-limitation"></a><span data-ttu-id="8e31e-293">Rozmiar wiersza i danych typu ograniczenia</span><span class="sxs-lookup"><span data-stu-id="8e31e-293">Row size and data type limitation</span></span>
<span data-ttu-id="8e31e-294">Program Polybase obciążenia są ograniczone tooloading wierszy zarówno mniejszy niż **1 MB** i nie można załadować tooVARCHR(MAX), NVARCHAR(MAX) lub VARBINARY(MAX).</span><span class="sxs-lookup"><span data-stu-id="8e31e-294">Polybase loads are limited tooloading rows both smaller than **1 MB** and cannot load tooVARCHR(MAX), NVARCHAR(MAX) or VARBINARY(MAX).</span></span> <span data-ttu-id="8e31e-295">Odwołuje się zbyt[tutaj](../sql-data-warehouse/sql-data-warehouse-service-capacity-limits.md#loads).</span><span class="sxs-lookup"><span data-stu-id="8e31e-295">Refer too[here](../sql-data-warehouse/sql-data-warehouse-service-capacity-limits.md#loads).</span></span>

<span data-ttu-id="8e31e-296">Jeśli masz dane źródłowe z wierszami o rozmiarze większym niż 1 MB, można tabel źródłowych hello toosplit w pionie do kilku małych sieci, gdy największy rozmiar wiersza hello każdego z nich nie przekracza hello limit.</span><span class="sxs-lookup"><span data-stu-id="8e31e-296">If you have source data with rows of size greater than 1 MB, you may want toosplit hello source tables vertically into several small ones where hello largest row size of each of them does not exceed hello limit.</span></span> <span data-ttu-id="8e31e-297">następnie można załadować tabel mniejszych Hello, przy użyciu programu PolyBase i scalane w usłudze Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="8e31e-297">hello smaller tables can then be loaded using PolyBase and merged together in Azure SQL Data Warehouse.</span></span>

### <a name="sql-data-warehouse-resource-class"></a><span data-ttu-id="8e31e-298">Klasa zasobów magazynu danych SQL</span><span class="sxs-lookup"><span data-stu-id="8e31e-298">SQL Data Warehouse resource class</span></span>
<span data-ttu-id="8e31e-299">tooachieve najlepsze możliwe przepływności, należy wziąć pod uwagę tooassign większych zasobów klasy toohello użytkownika są używane tooload danych do usługi SQL Data Warehouse przy użyciu programu PolyBase.</span><span class="sxs-lookup"><span data-stu-id="8e31e-299">tooachieve best possible throughput, consider tooassign larger resource class toohello user being used tooload data into SQL Data Warehouse via PolyBase.</span></span> <span data-ttu-id="8e31e-300">Dowiedz się, jak toodo który wykonując [zmienić przykład klasy zasobów użytkownika](../sql-data-warehouse/sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).</span><span class="sxs-lookup"><span data-stu-id="8e31e-300">Learn how toodo that by following [Change a user resource class example](../sql-data-warehouse/sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).</span></span>

### <a name="tablename-in-azure-sql-data-warehouse"></a><span data-ttu-id="8e31e-301">tableName w magazynie danych SQL Azure</span><span class="sxs-lookup"><span data-stu-id="8e31e-301">tableName in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="8e31e-302">Witaj poniższej tabeli przedstawiono przykłady dotyczące toospecify hello **tableName** właściwość w zestawie danych JSON dla różnych kombinacji nazwy schematu i tabeli.</span><span class="sxs-lookup"><span data-stu-id="8e31e-302">hello following table provides examples on how toospecify hello **tableName** property in dataset JSON for various combinations of schema and table name.</span></span>

| <span data-ttu-id="8e31e-303">Schemat bazy danych</span><span class="sxs-lookup"><span data-stu-id="8e31e-303">DB Schema</span></span> | <span data-ttu-id="8e31e-304">Nazwa tabeli</span><span class="sxs-lookup"><span data-stu-id="8e31e-304">Table name</span></span> | <span data-ttu-id="8e31e-305">Właściwość tableName JSON</span><span class="sxs-lookup"><span data-stu-id="8e31e-305">tableName JSON property</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8e31e-306">właściciel bazy danych</span><span class="sxs-lookup"><span data-stu-id="8e31e-306">dbo</span></span> |<span data-ttu-id="8e31e-307">MyTable</span><span class="sxs-lookup"><span data-stu-id="8e31e-307">MyTable</span></span> |<span data-ttu-id="8e31e-308">MyTable lub dbo. MyTable lub [dbo]. [MyTable]</span><span class="sxs-lookup"><span data-stu-id="8e31e-308">MyTable or dbo.MyTable or [dbo].[MyTable]</span></span> |
| <span data-ttu-id="8e31e-309">dbo1</span><span class="sxs-lookup"><span data-stu-id="8e31e-309">dbo1</span></span> |<span data-ttu-id="8e31e-310">MyTable</span><span class="sxs-lookup"><span data-stu-id="8e31e-310">MyTable</span></span> |<span data-ttu-id="8e31e-311">dbo1. MyTable lub [dbo1]. [MyTable]</span><span class="sxs-lookup"><span data-stu-id="8e31e-311">dbo1.MyTable or [dbo1].[MyTable]</span></span> |
| <span data-ttu-id="8e31e-312">właściciel bazy danych</span><span class="sxs-lookup"><span data-stu-id="8e31e-312">dbo</span></span> |<span data-ttu-id="8e31e-313">My.Table</span><span class="sxs-lookup"><span data-stu-id="8e31e-313">My.Table</span></span> |<span data-ttu-id="8e31e-314">[My.Table] lub [dbo]. [My.Table]</span><span class="sxs-lookup"><span data-stu-id="8e31e-314">[My.Table] or [dbo].[My.Table]</span></span> |
| <span data-ttu-id="8e31e-315">dbo1</span><span class="sxs-lookup"><span data-stu-id="8e31e-315">dbo1</span></span> |<span data-ttu-id="8e31e-316">My.Table</span><span class="sxs-lookup"><span data-stu-id="8e31e-316">My.Table</span></span> |<span data-ttu-id="8e31e-317">[dbo1]. [My.Table]</span><span class="sxs-lookup"><span data-stu-id="8e31e-317">[dbo1].[My.Table]</span></span> |

<span data-ttu-id="8e31e-318">Jeśli zostanie wyświetlony następujący błąd hello, może to być problem z wartością hello, który został określony jako właściwość tableName hello.</span><span class="sxs-lookup"><span data-stu-id="8e31e-318">If you see hello following error, it could be an issue with hello value you specified for hello tableName property.</span></span> <span data-ttu-id="8e31e-319">Zobacz tabelę hello hello prawidłowy sposób toospecify wartości dla właściwości JSON tableName hello.</span><span class="sxs-lookup"><span data-stu-id="8e31e-319">See hello table for hello correct way toospecify values for hello tableName JSON property.</span></span>  

```
Type=System.Data.SqlClient.SqlException,Message=Invalid object name 'stg.Account_test'.,Source=.Net SqlClient Data Provider
```

### <a name="columns-with-default-values"></a><span data-ttu-id="8e31e-320">Kolumn z wartościami domyślnymi</span><span class="sxs-lookup"><span data-stu-id="8e31e-320">Columns with default values</span></span>
<span data-ttu-id="8e31e-321">Obecnie PolyBase akceptuje tylko funkcji w fabryce danych hello taką samą liczbę kolumn w tabeli docelowej hello.</span><span class="sxs-lookup"><span data-stu-id="8e31e-321">Currently, PolyBase feature in Data Factory only accepts hello same number of columns as in hello target table.</span></span> <span data-ttu-id="8e31e-322">Przykład tabeli z kolumnami cztery i jeden z nich jest zdefiniowana z wartością domyślną.</span><span class="sxs-lookup"><span data-stu-id="8e31e-322">Say, you have a table with four columns and one of them is defined with a default value.</span></span> <span data-ttu-id="8e31e-323">dane wejściowe Hello nadal powinien zawierać cztery kolumny.</span><span class="sxs-lookup"><span data-stu-id="8e31e-323">hello input data should still contain four columns.</span></span> <span data-ttu-id="8e31e-324">Zapewnianie 3 kolumny zestawu danych wejściowych ważnością toohello podobne błąd następującego komunikatu:</span><span class="sxs-lookup"><span data-stu-id="8e31e-324">Providing a 3-column input dataset would yield an error similar toohello following message:</span></span>

```
All columns of hello table must be specified in hello INSERT BULK statement.
```
<span data-ttu-id="8e31e-325">Wartość NULL jest specjalny rodzaj wartości domyślnej.</span><span class="sxs-lookup"><span data-stu-id="8e31e-325">NULL value is a special form of default value.</span></span> <span data-ttu-id="8e31e-326">W przypadku wartości Null kolumny hello danych wejściowych hello (w obiekcie blob) dla tej kolumny może być pusta (nie może być brakuje hello wejściowy zestaw danych).</span><span class="sxs-lookup"><span data-stu-id="8e31e-326">If hello column is nullable, hello input data (in blob) for that column could be empty (cannot be missing from hello input dataset).</span></span> <span data-ttu-id="8e31e-327">Program PolyBase wstawia wartości NULL dla nich hello Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="8e31e-327">PolyBase inserts NULL for them in hello Azure SQL Data Warehouse.</span></span>  

## <a name="auto-table-creation"></a><span data-ttu-id="8e31e-328">Automatyczne tworzenie tabeli</span><span class="sxs-lookup"><span data-stu-id="8e31e-328">Auto table creation</span></span>
<span data-ttu-id="8e31e-329">Jeśli używasz kreatora kopiowania toocopy danych z programu SQL Server lub bazy danych SQL Azure tooAzure SQL Data Warehouse i hello tabeli, która odpowiada toohello tabela źródłowa nie istnieje w magazynie docelowym hello, fabryki danych może automatycznie tworzyć hello tabeli w hello Magazyn danych przy użyciu schematu tabeli źródłowej hello.</span><span class="sxs-lookup"><span data-stu-id="8e31e-329">If you are using Copy Wizard toocopy data from SQL Server or Azure SQL Database tooAzure SQL Data Warehouse and hello table that corresponds toohello source table does not exist in hello destination store, Data Factory can automatically create hello table in hello data warehouse by using hello source table schema.</span></span>

<span data-ttu-id="8e31e-330">Fabryka danych tworzy hello tabeli w magazynie docelowym hello z hello sama nazwa w magazynie danych źródła hello tabeli.</span><span class="sxs-lookup"><span data-stu-id="8e31e-330">Data Factory creates hello table in hello destination store with hello same table name in hello source data store.</span></span> <span data-ttu-id="8e31e-331">Hello typy danych kolumn są wybierane oparte na powitania po mapowania typu.</span><span class="sxs-lookup"><span data-stu-id="8e31e-331">hello data types for columns are chosen based on hello following type mapping.</span></span> <span data-ttu-id="8e31e-332">W razie potrzeby wykonuje toofix konwersje typu wszelkie niezgodności między magazynami źródłowym i docelowym.</span><span class="sxs-lookup"><span data-stu-id="8e31e-332">If needed, it performs type conversions toofix any incompatibilities between source and destination stores.</span></span> <span data-ttu-id="8e31e-333">Używa okrężnego tabeli dystrybucji.</span><span class="sxs-lookup"><span data-stu-id="8e31e-333">It also uses Round Robin table distribution.</span></span>

| <span data-ttu-id="8e31e-334">Typ kolumny źródłowej bazy danych SQL</span><span class="sxs-lookup"><span data-stu-id="8e31e-334">Source SQL Database column type</span></span> | <span data-ttu-id="8e31e-335">Typ kolumny docelowej magazynu danych SQL (limit rozmiaru)</span><span class="sxs-lookup"><span data-stu-id="8e31e-335">Destination SQL DW column type (size limitation)</span></span> |
| --- | --- |
| <span data-ttu-id="8e31e-336">int</span><span class="sxs-lookup"><span data-stu-id="8e31e-336">Int</span></span> | <span data-ttu-id="8e31e-337">int</span><span class="sxs-lookup"><span data-stu-id="8e31e-337">Int</span></span> |
| <span data-ttu-id="8e31e-338">BigInt</span><span class="sxs-lookup"><span data-stu-id="8e31e-338">BigInt</span></span> | <span data-ttu-id="8e31e-339">BigInt</span><span class="sxs-lookup"><span data-stu-id="8e31e-339">BigInt</span></span> |
| <span data-ttu-id="8e31e-340">SmallInt</span><span class="sxs-lookup"><span data-stu-id="8e31e-340">SmallInt</span></span> | <span data-ttu-id="8e31e-341">SmallInt</span><span class="sxs-lookup"><span data-stu-id="8e31e-341">SmallInt</span></span> |
| <span data-ttu-id="8e31e-342">TinyInt</span><span class="sxs-lookup"><span data-stu-id="8e31e-342">TinyInt</span></span> | <span data-ttu-id="8e31e-343">TinyInt</span><span class="sxs-lookup"><span data-stu-id="8e31e-343">TinyInt</span></span> |
| <span data-ttu-id="8e31e-344">bitowe</span><span class="sxs-lookup"><span data-stu-id="8e31e-344">Bit</span></span> | <span data-ttu-id="8e31e-345">bitowe</span><span class="sxs-lookup"><span data-stu-id="8e31e-345">Bit</span></span> |
| <span data-ttu-id="8e31e-346">Decimal</span><span class="sxs-lookup"><span data-stu-id="8e31e-346">Decimal</span></span> | <span data-ttu-id="8e31e-347">Decimal</span><span class="sxs-lookup"><span data-stu-id="8e31e-347">Decimal</span></span> |
| <span data-ttu-id="8e31e-348">numeryczne</span><span class="sxs-lookup"><span data-stu-id="8e31e-348">Numeric</span></span> | <span data-ttu-id="8e31e-349">Decimal</span><span class="sxs-lookup"><span data-stu-id="8e31e-349">Decimal</span></span> |
| <span data-ttu-id="8e31e-350">Float</span><span class="sxs-lookup"><span data-stu-id="8e31e-350">Float</span></span> | <span data-ttu-id="8e31e-351">Float</span><span class="sxs-lookup"><span data-stu-id="8e31e-351">Float</span></span> |
| <span data-ttu-id="8e31e-352">oszczędność pieniędzy</span><span class="sxs-lookup"><span data-stu-id="8e31e-352">Money</span></span> | <span data-ttu-id="8e31e-353">oszczędność pieniędzy</span><span class="sxs-lookup"><span data-stu-id="8e31e-353">Money</span></span> |
| <span data-ttu-id="8e31e-354">Real</span><span class="sxs-lookup"><span data-stu-id="8e31e-354">Real</span></span> | <span data-ttu-id="8e31e-355">Real</span><span class="sxs-lookup"><span data-stu-id="8e31e-355">Real</span></span> |
| <span data-ttu-id="8e31e-356">SmallMoney</span><span class="sxs-lookup"><span data-stu-id="8e31e-356">SmallMoney</span></span> | <span data-ttu-id="8e31e-357">SmallMoney</span><span class="sxs-lookup"><span data-stu-id="8e31e-357">SmallMoney</span></span> |
| <span data-ttu-id="8e31e-358">Binarne</span><span class="sxs-lookup"><span data-stu-id="8e31e-358">Binary</span></span> | <span data-ttu-id="8e31e-359">Binarne</span><span class="sxs-lookup"><span data-stu-id="8e31e-359">Binary</span></span> |
| <span data-ttu-id="8e31e-360">varbinary</span><span class="sxs-lookup"><span data-stu-id="8e31e-360">Varbinary</span></span> | <span data-ttu-id="8e31e-361">Varbinary (up too8000)</span><span class="sxs-lookup"><span data-stu-id="8e31e-361">Varbinary (up too8000)</span></span> |
| <span data-ttu-id="8e31e-362">Date</span><span class="sxs-lookup"><span data-stu-id="8e31e-362">Date</span></span> | <span data-ttu-id="8e31e-363">Date</span><span class="sxs-lookup"><span data-stu-id="8e31e-363">Date</span></span> |
| <span data-ttu-id="8e31e-364">Data i godzina</span><span class="sxs-lookup"><span data-stu-id="8e31e-364">DateTime</span></span> | <span data-ttu-id="8e31e-365">Data i godzina</span><span class="sxs-lookup"><span data-stu-id="8e31e-365">DateTime</span></span> |
| <span data-ttu-id="8e31e-366">DateTime2</span><span class="sxs-lookup"><span data-stu-id="8e31e-366">DateTime2</span></span> | <span data-ttu-id="8e31e-367">DateTime2</span><span class="sxs-lookup"><span data-stu-id="8e31e-367">DateTime2</span></span> |
| <span data-ttu-id="8e31e-368">Time</span><span class="sxs-lookup"><span data-stu-id="8e31e-368">Time</span></span> | <span data-ttu-id="8e31e-369">Time</span><span class="sxs-lookup"><span data-stu-id="8e31e-369">Time</span></span> |
| <span data-ttu-id="8e31e-370">DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="8e31e-370">DateTimeOffset</span></span> | <span data-ttu-id="8e31e-371">DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="8e31e-371">DateTimeOffset</span></span> |
| <span data-ttu-id="8e31e-372">SmallDateTime</span><span class="sxs-lookup"><span data-stu-id="8e31e-372">SmallDateTime</span></span> | <span data-ttu-id="8e31e-373">SmallDateTime</span><span class="sxs-lookup"><span data-stu-id="8e31e-373">SmallDateTime</span></span> |
| <span data-ttu-id="8e31e-374">Tekst</span><span class="sxs-lookup"><span data-stu-id="8e31e-374">Text</span></span> | <span data-ttu-id="8e31e-375">Varchar (up too8000)</span><span class="sxs-lookup"><span data-stu-id="8e31e-375">Varchar (up too8000)</span></span> |
| <span data-ttu-id="8e31e-376">NText</span><span class="sxs-lookup"><span data-stu-id="8e31e-376">NText</span></span> | <span data-ttu-id="8e31e-377">NVarChar (up too4000)</span><span class="sxs-lookup"><span data-stu-id="8e31e-377">NVarChar (up too4000)</span></span> |
| <span data-ttu-id="8e31e-378">Image (Obraz)</span><span class="sxs-lookup"><span data-stu-id="8e31e-378">Image</span></span> | <span data-ttu-id="8e31e-379">VarBinary (up too8000)</span><span class="sxs-lookup"><span data-stu-id="8e31e-379">VarBinary (up too8000)</span></span> |
| <span data-ttu-id="8e31e-380">Unikatowy identyfikator</span><span class="sxs-lookup"><span data-stu-id="8e31e-380">UniqueIdentifier</span></span> | <span data-ttu-id="8e31e-381">Unikatowy identyfikator</span><span class="sxs-lookup"><span data-stu-id="8e31e-381">UniqueIdentifier</span></span> |
| <span data-ttu-id="8e31e-382">char</span><span class="sxs-lookup"><span data-stu-id="8e31e-382">Char</span></span> | <span data-ttu-id="8e31e-383">char</span><span class="sxs-lookup"><span data-stu-id="8e31e-383">Char</span></span> |
| <span data-ttu-id="8e31e-384">NChar</span><span class="sxs-lookup"><span data-stu-id="8e31e-384">NChar</span></span> | <span data-ttu-id="8e31e-385">NChar</span><span class="sxs-lookup"><span data-stu-id="8e31e-385">NChar</span></span> |
| <span data-ttu-id="8e31e-386">VarChar</span><span class="sxs-lookup"><span data-stu-id="8e31e-386">VarChar</span></span> | <span data-ttu-id="8e31e-387">VarChar (up too8000)</span><span class="sxs-lookup"><span data-stu-id="8e31e-387">VarChar (up too8000)</span></span> |
| <span data-ttu-id="8e31e-388">NVarChar</span><span class="sxs-lookup"><span data-stu-id="8e31e-388">NVarChar</span></span> | <span data-ttu-id="8e31e-389">NVarChar (up too4000)</span><span class="sxs-lookup"><span data-stu-id="8e31e-389">NVarChar (up too4000)</span></span> |
| <span data-ttu-id="8e31e-390">XML</span><span class="sxs-lookup"><span data-stu-id="8e31e-390">Xml</span></span> | <span data-ttu-id="8e31e-391">Varchar (up too8000)</span><span class="sxs-lookup"><span data-stu-id="8e31e-391">Varchar (up too8000)</span></span> |

[!INCLUDE [data-factory-type-repeatability-for-sql-sources](../../includes/data-factory-type-repeatability-for-sql-sources.md)]

## <a name="type-mapping-for-azure-sql-data-warehouse"></a><span data-ttu-id="8e31e-392">Mapowanie typu dla usługi Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="8e31e-392">Type mapping for Azure SQL Data Warehouse</span></span>
<span data-ttu-id="8e31e-393">Jak wspomniano w hello [działań przepływu danych](data-factory-data-movement-activities.md) wykonuje działanie kopiowania artykułu, automatyczne konwersje z typów toosink typy źródła z hello następujące podejście krok 2:</span><span class="sxs-lookup"><span data-stu-id="8e31e-393">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types toosink types with hello following 2-step approach:</span></span>

1. <span data-ttu-id="8e31e-394">Konwertować z typu too.NET typów natywnych źródła</span><span class="sxs-lookup"><span data-stu-id="8e31e-394">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="8e31e-395">Konwertować z typu sink toonative typu .NET</span><span class="sxs-lookup"><span data-stu-id="8e31e-395">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="8e31e-396">Podczas przenoszenia danych za & z usługi Azure SQL Data Warehouse, hello następujące mapowania są używane z too.NET typu SQL i odwrotnie.</span><span class="sxs-lookup"><span data-stu-id="8e31e-396">When moving data too& from Azure SQL Data Warehouse, hello following mappings are used from SQL type too.NET type and vice versa.</span></span>

<span data-ttu-id="8e31e-397">Mapowanie Hello jest taki sam jak hello [mapowanie typu danych serwera SQL dla ADO.NET](https://msdn.microsoft.com/library/cc716729.aspx).</span><span class="sxs-lookup"><span data-stu-id="8e31e-397">hello mapping is same as hello [SQL Server Data Type Mapping for ADO.NET](https://msdn.microsoft.com/library/cc716729.aspx).</span></span>

| <span data-ttu-id="8e31e-398">Typ aparatu bazy danych programu SQL Server</span><span class="sxs-lookup"><span data-stu-id="8e31e-398">SQL Server Database Engine type</span></span> | <span data-ttu-id="8e31e-399">Typ programu .NET framework</span><span class="sxs-lookup"><span data-stu-id="8e31e-399">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="8e31e-400">bigint</span><span class="sxs-lookup"><span data-stu-id="8e31e-400">bigint</span></span> |<span data-ttu-id="8e31e-401">Int64</span><span class="sxs-lookup"><span data-stu-id="8e31e-401">Int64</span></span> |
| <span data-ttu-id="8e31e-402">Binarne</span><span class="sxs-lookup"><span data-stu-id="8e31e-402">binary</span></span> |<span data-ttu-id="8e31e-403">Byte]</span><span class="sxs-lookup"><span data-stu-id="8e31e-403">Byte[]</span></span> |
| <span data-ttu-id="8e31e-404">bitowe</span><span class="sxs-lookup"><span data-stu-id="8e31e-404">bit</span></span> |<span data-ttu-id="8e31e-405">Wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="8e31e-405">Boolean</span></span> |
| <span data-ttu-id="8e31e-406">char</span><span class="sxs-lookup"><span data-stu-id="8e31e-406">char</span></span> |<span data-ttu-id="8e31e-407">Ciąg, Char]</span><span class="sxs-lookup"><span data-stu-id="8e31e-407">String, Char[]</span></span> |
| <span data-ttu-id="8e31e-408">Data</span><span class="sxs-lookup"><span data-stu-id="8e31e-408">date</span></span> |<span data-ttu-id="8e31e-409">Data i godzina</span><span class="sxs-lookup"><span data-stu-id="8e31e-409">DateTime</span></span> |
| <span data-ttu-id="8e31e-410">Data i godzina</span><span class="sxs-lookup"><span data-stu-id="8e31e-410">Datetime</span></span> |<span data-ttu-id="8e31e-411">Data i godzina</span><span class="sxs-lookup"><span data-stu-id="8e31e-411">DateTime</span></span> |
| <span data-ttu-id="8e31e-412">datetime2</span><span class="sxs-lookup"><span data-stu-id="8e31e-412">datetime2</span></span> |<span data-ttu-id="8e31e-413">Data i godzina</span><span class="sxs-lookup"><span data-stu-id="8e31e-413">DateTime</span></span> |
| <span data-ttu-id="8e31e-414">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="8e31e-414">Datetimeoffset</span></span> |<span data-ttu-id="8e31e-415">DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="8e31e-415">DateTimeOffset</span></span> |
| <span data-ttu-id="8e31e-416">Decimal</span><span class="sxs-lookup"><span data-stu-id="8e31e-416">Decimal</span></span> |<span data-ttu-id="8e31e-417">Decimal</span><span class="sxs-lookup"><span data-stu-id="8e31e-417">Decimal</span></span> |
| <span data-ttu-id="8e31e-418">Atrybut FILESTREAM (varbinary(max))</span><span class="sxs-lookup"><span data-stu-id="8e31e-418">FILESTREAM attribute (varbinary(max))</span></span> |<span data-ttu-id="8e31e-419">Byte]</span><span class="sxs-lookup"><span data-stu-id="8e31e-419">Byte[]</span></span> |
| <span data-ttu-id="8e31e-420">Float</span><span class="sxs-lookup"><span data-stu-id="8e31e-420">Float</span></span> |<span data-ttu-id="8e31e-421">O podwójnej precyzji</span><span class="sxs-lookup"><span data-stu-id="8e31e-421">Double</span></span> |
| <span data-ttu-id="8e31e-422">Obraz</span><span class="sxs-lookup"><span data-stu-id="8e31e-422">image</span></span> |<span data-ttu-id="8e31e-423">Byte]</span><span class="sxs-lookup"><span data-stu-id="8e31e-423">Byte[]</span></span> |
| <span data-ttu-id="8e31e-424">int</span><span class="sxs-lookup"><span data-stu-id="8e31e-424">int</span></span> |<span data-ttu-id="8e31e-425">Int32</span><span class="sxs-lookup"><span data-stu-id="8e31e-425">Int32</span></span> |
| <span data-ttu-id="8e31e-426">oszczędność pieniędzy</span><span class="sxs-lookup"><span data-stu-id="8e31e-426">money</span></span> |<span data-ttu-id="8e31e-427">Decimal</span><span class="sxs-lookup"><span data-stu-id="8e31e-427">Decimal</span></span> |
| <span data-ttu-id="8e31e-428">nchar</span><span class="sxs-lookup"><span data-stu-id="8e31e-428">nchar</span></span> |<span data-ttu-id="8e31e-429">Ciąg, Char]</span><span class="sxs-lookup"><span data-stu-id="8e31e-429">String, Char[]</span></span> |
| <span data-ttu-id="8e31e-430">ntext</span><span class="sxs-lookup"><span data-stu-id="8e31e-430">ntext</span></span> |<span data-ttu-id="8e31e-431">Ciąg, Char]</span><span class="sxs-lookup"><span data-stu-id="8e31e-431">String, Char[]</span></span> |
| <span data-ttu-id="8e31e-432">numeryczne</span><span class="sxs-lookup"><span data-stu-id="8e31e-432">numeric</span></span> |<span data-ttu-id="8e31e-433">Decimal</span><span class="sxs-lookup"><span data-stu-id="8e31e-433">Decimal</span></span> |
| <span data-ttu-id="8e31e-434">nvarchar</span><span class="sxs-lookup"><span data-stu-id="8e31e-434">nvarchar</span></span> |<span data-ttu-id="8e31e-435">Ciąg, Char]</span><span class="sxs-lookup"><span data-stu-id="8e31e-435">String, Char[]</span></span> |
| <span data-ttu-id="8e31e-436">rzeczywiste</span><span class="sxs-lookup"><span data-stu-id="8e31e-436">real</span></span> |<span data-ttu-id="8e31e-437">Pojedynczy</span><span class="sxs-lookup"><span data-stu-id="8e31e-437">Single</span></span> |
| <span data-ttu-id="8e31e-438">ROWVERSION</span><span class="sxs-lookup"><span data-stu-id="8e31e-438">rowversion</span></span> |<span data-ttu-id="8e31e-439">Byte]</span><span class="sxs-lookup"><span data-stu-id="8e31e-439">Byte[]</span></span> |
| <span data-ttu-id="8e31e-440">smalldatetime</span><span class="sxs-lookup"><span data-stu-id="8e31e-440">smalldatetime</span></span> |<span data-ttu-id="8e31e-441">Data i godzina</span><span class="sxs-lookup"><span data-stu-id="8e31e-441">DateTime</span></span> |
| <span data-ttu-id="8e31e-442">smallint</span><span class="sxs-lookup"><span data-stu-id="8e31e-442">smallint</span></span> |<span data-ttu-id="8e31e-443">Int16</span><span class="sxs-lookup"><span data-stu-id="8e31e-443">Int16</span></span> |
| <span data-ttu-id="8e31e-444">smallmoney</span><span class="sxs-lookup"><span data-stu-id="8e31e-444">smallmoney</span></span> |<span data-ttu-id="8e31e-445">Decimal</span><span class="sxs-lookup"><span data-stu-id="8e31e-445">Decimal</span></span> |
| <span data-ttu-id="8e31e-446">sql_variant</span><span class="sxs-lookup"><span data-stu-id="8e31e-446">sql_variant</span></span> |<span data-ttu-id="8e31e-447">Obiekt *</span><span class="sxs-lookup"><span data-stu-id="8e31e-447">Object *</span></span> |
| <span data-ttu-id="8e31e-448">Tekst</span><span class="sxs-lookup"><span data-stu-id="8e31e-448">text</span></span> |<span data-ttu-id="8e31e-449">Ciąg, Char]</span><span class="sxs-lookup"><span data-stu-id="8e31e-449">String, Char[]</span></span> |
| <span data-ttu-id="8e31e-450">time</span><span class="sxs-lookup"><span data-stu-id="8e31e-450">time</span></span> |<span data-ttu-id="8e31e-451">Zakres czasu</span><span class="sxs-lookup"><span data-stu-id="8e31e-451">TimeSpan</span></span> |
| <span data-ttu-id="8e31e-452">sygnatura czasowa</span><span class="sxs-lookup"><span data-stu-id="8e31e-452">timestamp</span></span> |<span data-ttu-id="8e31e-453">Byte]</span><span class="sxs-lookup"><span data-stu-id="8e31e-453">Byte[]</span></span> |
| <span data-ttu-id="8e31e-454">tinyint</span><span class="sxs-lookup"><span data-stu-id="8e31e-454">tinyint</span></span> |<span data-ttu-id="8e31e-455">Bajtów</span><span class="sxs-lookup"><span data-stu-id="8e31e-455">Byte</span></span> |
| <span data-ttu-id="8e31e-456">Unikatowy identyfikator</span><span class="sxs-lookup"><span data-stu-id="8e31e-456">uniqueidentifier</span></span> |<span data-ttu-id="8e31e-457">Identyfikator GUID</span><span class="sxs-lookup"><span data-stu-id="8e31e-457">Guid</span></span> |
| <span data-ttu-id="8e31e-458">varbinary</span><span class="sxs-lookup"><span data-stu-id="8e31e-458">varbinary</span></span> |<span data-ttu-id="8e31e-459">Byte]</span><span class="sxs-lookup"><span data-stu-id="8e31e-459">Byte[]</span></span> |
| <span data-ttu-id="8e31e-460">varchar</span><span class="sxs-lookup"><span data-stu-id="8e31e-460">varchar</span></span> |<span data-ttu-id="8e31e-461">Ciąg, Char]</span><span class="sxs-lookup"><span data-stu-id="8e31e-461">String, Char[]</span></span> |
| <span data-ttu-id="8e31e-462">xml</span><span class="sxs-lookup"><span data-stu-id="8e31e-462">xml</span></span> |<span data-ttu-id="8e31e-463">XML</span><span class="sxs-lookup"><span data-stu-id="8e31e-463">Xml</span></span> |

<span data-ttu-id="8e31e-464">Można również mapować kolumn z źródła toocolumns zestawu danych z zestawu danych zbiornika w definicji działania kopiowania hello.</span><span class="sxs-lookup"><span data-stu-id="8e31e-464">You can also map columns from source dataset toocolumns from sink dataset in hello copy activity definition.</span></span> <span data-ttu-id="8e31e-465">Aby uzyskać więcej informacji, zobacz [mapowania kolumnach dataset w fabryce danych Azure](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="8e31e-465">For details, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="json-examples-for-copying-data-tooand-from-sql-data-warehouse"></a><span data-ttu-id="8e31e-466">Przykłady JSON do kopiowania tooand danych z magazynu danych SQL</span><span class="sxs-lookup"><span data-stu-id="8e31e-466">JSON examples for copying data tooand from SQL Data Warehouse</span></span>
<span data-ttu-id="8e31e-467">Witaj poniższe przykłady zapewniają definicje JSON przy użyciu można toocreate potoku [portalu Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) lub [programu Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) lub [programu Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="8e31e-467">hello following examples provide sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="8e31e-468">Przedstawiają sposób toocopy tooand danych z magazynu danych SQL Azure i magazynu obiektów Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="8e31e-468">They show how toocopy data tooand from Azure SQL Data Warehouse and Azure Blob Storage.</span></span> <span data-ttu-id="8e31e-469">Jednak dane mogą być kopiowane **bezpośrednio** z dowolnego źródła tooany z wychwytywanie hello wyrażony w [tutaj](data-factory-data-movement-activities.md#supported-data-stores-and-formats) przy użyciu hello działanie kopiowania w fabryce danych Azure.</span><span class="sxs-lookup"><span data-stu-id="8e31e-469">However, data can be copied **directly** from any of sources tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>

### <a name="example-copy-data-from-azure-sql-data-warehouse-tooazure-blob"></a><span data-ttu-id="8e31e-470">Przykład: Kopiowanie danych z usługi Azure SQL Data Warehouse tooAzure obiektów Blob</span><span class="sxs-lookup"><span data-stu-id="8e31e-470">Example: Copy data from Azure SQL Data Warehouse tooAzure Blob</span></span>
<span data-ttu-id="8e31e-471">przykład Witaj definiuje powitania po jednostek fabryki danych:</span><span class="sxs-lookup"><span data-stu-id="8e31e-471">hello sample defines hello following Data Factory entities:</span></span>

1. <span data-ttu-id="8e31e-472">Połączonej usługi typu [AzureSqlDW](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="8e31e-472">A linked service of type [AzureSqlDW](#linked-service-properties).</span></span>
2. <span data-ttu-id="8e31e-473">Połączonej usługi typu [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="8e31e-473">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="8e31e-474">Dane wejściowe [dataset](data-factory-create-datasets.md) typu [AzureSqlDWTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="8e31e-474">An input [dataset](data-factory-create-datasets.md) of type [AzureSqlDWTable](#dataset-properties).</span></span>
4. <span data-ttu-id="8e31e-475">Dane wyjściowe [dataset](data-factory-create-datasets.md) typu [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="8e31e-475">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="8e31e-476">A [potoku](data-factory-create-pipelines.md) z działaniem kopii, która używa [SqlDWSource](#copy-activity-properties) i [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="8e31e-476">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [SqlDWSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="8e31e-477">przykład Witaj kopiuje dane (co godzinę, codziennie, itp.) szeregów czasowych, z tabeli w obiekcie blob tooa bazy danych magazynu danych SQL Azure co godzinę.</span><span class="sxs-lookup"><span data-stu-id="8e31e-477">hello sample copies time-series (hourly, daily, etc.) data from a table in Azure SQL Data Warehouse database tooa blob every hour.</span></span> <span data-ttu-id="8e31e-478">właściwości JSON Hello używane w te przykłady są opisane w sekcjach poniżej hello próbek.</span><span class="sxs-lookup"><span data-stu-id="8e31e-478">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="8e31e-479">**Usługa Azure SQL Data Warehouse połączonej usługi:**</span><span class="sxs-lookup"><span data-stu-id="8e31e-479">**Azure SQL Data Warehouse linked service:**</span></span>

```JSON
{
  "name": "AzureSqlDWLinkedService",
  "properties": {
    "type": "AzureSqlDW",
    "typeProperties": {
      "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
    }
  }
}
```
<span data-ttu-id="8e31e-480">**Magazyn obiektów Blob Azure połączonej usługi:**</span><span class="sxs-lookup"><span data-stu-id="8e31e-480">**Azure Blob storage linked service:**</span></span>

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
<span data-ttu-id="8e31e-481">**Usługa Azure SQL Data Warehouse wejściowy zestaw danych:**</span><span class="sxs-lookup"><span data-stu-id="8e31e-481">**Azure SQL Data Warehouse input dataset:**</span></span>

<span data-ttu-id="8e31e-482">przykład Witaj przyjęto założenie, utworzono tabelę "MyTable" w magazynie danych SQL Azure i zawiera kolumnę o nazwie "timestampcolumn" dla czasu serii danych.</span><span class="sxs-lookup"><span data-stu-id="8e31e-482">hello sample assumes you have created a table “MyTable” in Azure SQL Data Warehouse and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="8e31e-483">Ustawienie "external": "prawda" informuje hello usługi fabryka danych tego elementu dataset hello zewnętrznych toohello fabryki danych i nie jest generowany przez działanie w fabryce danych hello.</span><span class="sxs-lookup"><span data-stu-id="8e31e-483">Setting “external”: ”true” informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```JSON
{
  "name": "AzureSqlDWInput",
  "properties": {
    "type": "AzureSqlDWTable",
    "linkedServiceName": "AzureSqlDWLinkedService",
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
<span data-ttu-id="8e31e-484">**Azure Blob wyjściowy zestaw danych:**</span><span class="sxs-lookup"><span data-stu-id="8e31e-484">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="8e31e-485">Dane są zapisywane tooa nowych obiektów blob, co godzinę (częstotliwość: godziny, interwał: 1).</span><span class="sxs-lookup"><span data-stu-id="8e31e-485">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="8e31e-486">Ścieżka folderu Hello hello obiektu blob dynamicznie jest obliczane na podstawie czasu rozpoczęcia hello hello wycinek, który jest przetwarzana.</span><span class="sxs-lookup"><span data-stu-id="8e31e-486">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="8e31e-487">Ścieżka folderu Hello używa rok, miesiąc, dzień i godziny części hello czas rozpoczęcia.</span><span class="sxs-lookup"><span data-stu-id="8e31e-487">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

```JSON
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

<span data-ttu-id="8e31e-488">**Działanie kopiowania w potoku z SqlDWSource i BlobSink:**</span><span class="sxs-lookup"><span data-stu-id="8e31e-488">**Copy activity in a pipeline with SqlDWSource and BlobSink:**</span></span>

<span data-ttu-id="8e31e-489">Witaj potoku zawiera działanie kopiowania, który jest skonfigurowany toouse hello wejściowych i wyjściowych zestawów danych i jest toorun zaplanowane co godzinę.</span><span class="sxs-lookup"><span data-stu-id="8e31e-489">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="8e31e-490">W potoku hello definicji JSON, hello **źródła** typu ustawiono zbyt**SqlDWSource** i **zbiornika** typu ustawiono zbyt**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="8e31e-490">In hello pipeline JSON definition, hello **source** type is set too**SqlDWSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="8e31e-491">Zapytanie SQL Hello określone dla hello **SqlReaderQuery** właściwości zaznacza danych hello hello poza toocopy godzinę.</span><span class="sxs-lookup"><span data-stu-id="8e31e-491">hello SQL query specified for hello **SqlReaderQuery** property selects hello data in hello past hour toocopy.</span></span>

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline for copy activity",
    "activities":[  
      {
        "name": "AzureSQLDWtoBlob",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureSqlDWInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "SqlDWSource",
            "sqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
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
> <span data-ttu-id="8e31e-492">Przykład Witaj **sqlReaderQuery** dla hello SqlDWSource został określony.</span><span class="sxs-lookup"><span data-stu-id="8e31e-492">In hello example, **sqlReaderQuery** is specified for hello SqlDWSource.</span></span> <span data-ttu-id="8e31e-493">Działanie kopiowania Hello jest uruchamiana to zapytanie dla hello Azure SQL Data Warehouse źródła tooget hello danych.</span><span class="sxs-lookup"><span data-stu-id="8e31e-493">hello Copy Activity runs this query against hello Azure SQL Data Warehouse source tooget hello data.</span></span>
>
> <span data-ttu-id="8e31e-494">Alternatywnie można określić procedury składowanej, określając hello **sqlReaderStoredProcedureName** i **storedProcedureParameters** (jeśli hello procedura składowana pobiera parametry).</span><span class="sxs-lookup"><span data-stu-id="8e31e-494">Alternatively, you can specify a stored procedure by specifying hello **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if hello stored procedure takes parameters).</span></span>
>
> <span data-ttu-id="8e31e-495">Jeśli nie określisz sqlReaderQuery lub sqlReaderStoredProcedureName hello kolumn zdefiniowanych w sekcji Struktura hello hello zestawu danych JSON są używane toobuild kwerendy (Wybierz Kolumna1, Kolumna2 z mytable) toorun przed hello Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="8e31e-495">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, hello columns defined in hello structure section of hello dataset JSON are used toobuild a query (select column1, column2 from mytable) toorun against hello Azure SQL Data Warehouse.</span></span> <span data-ttu-id="8e31e-496">Jeśli hello definicji zestawu danych nie ma on struktury hello, wszystkie kolumny są wybierane w tabeli hello.</span><span class="sxs-lookup"><span data-stu-id="8e31e-496">If hello dataset definition does not have hello structure, all columns are selected from hello table.</span></span>
>
>

### <a name="example-copy-data-from-azure-blob-tooazure-sql-data-warehouse"></a><span data-ttu-id="8e31e-497">Przykład: Kopiowanie danych z tooAzure obiektów Blob platformy Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="8e31e-497">Example: Copy data from Azure Blob tooAzure SQL Data Warehouse</span></span>
<span data-ttu-id="8e31e-498">przykład Witaj definiuje powitania po jednostek fabryki danych:</span><span class="sxs-lookup"><span data-stu-id="8e31e-498">hello sample defines hello following Data Factory entities:</span></span>

1. <span data-ttu-id="8e31e-499">Połączonej usługi typu [AzureSqlDW](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="8e31e-499">A linked service of type [AzureSqlDW](#linked-service-properties).</span></span>
2. <span data-ttu-id="8e31e-500">Połączonej usługi typu [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="8e31e-500">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="8e31e-501">Dane wejściowe [dataset](data-factory-create-datasets.md) typu [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="8e31e-501">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="8e31e-502">Dane wyjściowe [dataset](data-factory-create-datasets.md) typu [AzureSqlDWTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="8e31e-502">An output [dataset](data-factory-create-datasets.md) of type [AzureSqlDWTable](#dataset-properties).</span></span>
5. <span data-ttu-id="8e31e-503">A [potoku](data-factory-create-pipelines.md) z działaniem kopii, która używa [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) i [SqlDWSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="8e31e-503">A [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [SqlDWSink](#copy-activity-properties).</span></span>

<span data-ttu-id="8e31e-504">Przykładowe Hello kopiuje dane szeregów czasowych (co godzinę, codziennie, itp.) z tabeli tooa obiektów blob platformy Azure w bazie danych magazynu danych SQL Azure co godzinę.</span><span class="sxs-lookup"><span data-stu-id="8e31e-504">hello sample copies time-series data (hourly, daily, etc.) from Azure blob tooa table in Azure SQL Data Warehouse database every hour.</span></span> <span data-ttu-id="8e31e-505">właściwości JSON Hello używane w te przykłady są opisane w sekcjach poniżej hello próbek.</span><span class="sxs-lookup"><span data-stu-id="8e31e-505">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="8e31e-506">**Usługa Azure SQL Data Warehouse połączonej usługi:**</span><span class="sxs-lookup"><span data-stu-id="8e31e-506">**Azure SQL Data Warehouse linked service:**</span></span>

```JSON
{
  "name": "AzureSqlDWLinkedService",
  "properties": {
    "type": "AzureSqlDW",
    "typeProperties": {
      "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
    }
  }
}
```
<span data-ttu-id="8e31e-507">**Magazyn obiektów Blob Azure połączonej usługi:**</span><span class="sxs-lookup"><span data-stu-id="8e31e-507">**Azure Blob storage linked service:**</span></span>

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
<span data-ttu-id="8e31e-508">**Azure wejściowego zestawu danych obiektów Blob:**</span><span class="sxs-lookup"><span data-stu-id="8e31e-508">**Azure Blob input dataset:**</span></span>

<span data-ttu-id="8e31e-509">Dane są pobierane z nowego obiektu blob co godzinę (częstotliwość: godziny, interwał: 1).</span><span class="sxs-lookup"><span data-stu-id="8e31e-509">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="8e31e-510">Witaj folderu ścieżkę i nazwę pliku dla obiekt blob hello dynamicznie są oceniane na podstawie czasu rozpoczęcia hello hello wycinek, który jest przetwarzana.</span><span class="sxs-lookup"><span data-stu-id="8e31e-510">hello folder path and file name for hello blob are dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="8e31e-511">Ścieżka folderu Hello korzysta rok, miesiąc i dzień część czas rozpoczęcia hello, a nazwa pliku hello część hello czas rozpoczęcia.</span><span class="sxs-lookup"><span data-stu-id="8e31e-511">hello folder path uses year, month, and day part of hello start time and file name uses hello hour part of hello start time.</span></span> <span data-ttu-id="8e31e-512">"external": ustawienie "prawda" hello usługi fabryka danych informuje, że ta tabela zewnętrznych toohello fabryki danych i nie jest generowany przez działanie w fabryce danych hello.</span><span class="sxs-lookup"><span data-stu-id="8e31e-512">“external”: “true” setting informs hello Data Factory service that this table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```JSON
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}",
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
<span data-ttu-id="8e31e-513">**Usługa Azure SQL Data Warehouse wyjściowy zestaw danych:**</span><span class="sxs-lookup"><span data-stu-id="8e31e-513">**Azure SQL Data Warehouse output dataset:**</span></span>

<span data-ttu-id="8e31e-514">przykład Witaj kopiuje tabeli tooa danych o nazwie "MyTable" w usłudze Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="8e31e-514">hello sample copies data tooa table named “MyTable” in Azure SQL Data Warehouse.</span></span> <span data-ttu-id="8e31e-515">Utwórz tabelę hello w usłudze Azure SQL Data Warehouse przy użyciu hello taką samą liczbę kolumn, zgodnie z oczekiwaniami toocontain pliku Blob CSV hello.</span><span class="sxs-lookup"><span data-stu-id="8e31e-515">Create hello table in Azure SQL Data Warehouse with hello same number of columns as you expect hello Blob CSV file toocontain.</span></span> <span data-ttu-id="8e31e-516">Dodawaniu nowych wierszy tabeli toohello co godzinę.</span><span class="sxs-lookup"><span data-stu-id="8e31e-516">New rows are added toohello table every hour.</span></span>

```JSON
{
  "name": "AzureSqlDWOutput",
  "properties": {
    "type": "AzureSqlDWTable",
    "linkedServiceName": "AzureSqlDWLinkedService",
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
<span data-ttu-id="8e31e-517">**Działanie kopiowania w potoku z BlobSource i SqlDWSink:**</span><span class="sxs-lookup"><span data-stu-id="8e31e-517">**Copy activity in a pipeline with BlobSource and SqlDWSink:**</span></span>

<span data-ttu-id="8e31e-518">Witaj potoku zawiera działanie kopiowania, który jest skonfigurowany toouse hello wejściowych i wyjściowych zestawów danych i jest toorun zaplanowane co godzinę.</span><span class="sxs-lookup"><span data-stu-id="8e31e-518">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="8e31e-519">W potoku hello definicji JSON, hello **źródła** typu ustawiono zbyt**BlobSource** i **zbiornika** typu ustawiono zbyt**SqlDWSink**.</span><span class="sxs-lookup"><span data-stu-id="8e31e-519">In hello pipeline JSON definition, hello **source** type is set too**BlobSource** and **sink** type is set too**SqlDWSink**.</span></span>

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "AzureBlobtoSQLDW",
        "description": "Copy Activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureBlobInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureSqlDWOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource",
            "blobColumnSeparators": ","
          },
          "sink": {
            "type": "SqlDWSink",
            "allowPolyBase": true
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
<span data-ttu-id="8e31e-520">Aby uzyskać wskazówki, zobacz Zobacz hello [załadować 1 TB do usługi Azure SQL Data Warehouse z fabryką danych Azure w obszarze 15 minut](data-factory-load-sql-data-warehouse.md) i [ładowanie danych z fabryką danych Azure](../sql-data-warehouse/sql-data-warehouse-get-started-load-with-azure-data-factory.md) artykułu w hello Azure SQL Data Warehouse dokumentacja.</span><span class="sxs-lookup"><span data-stu-id="8e31e-520">For a walkthrough, see hello see [Load 1 TB into Azure SQL Data Warehouse under 15 minutes with Azure Data Factory](data-factory-load-sql-data-warehouse.md) and [Load data with Azure Data Factory](../sql-data-warehouse/sql-data-warehouse-get-started-load-with-azure-data-factory.md) article in hello Azure SQL Data Warehouse documentation.</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="8e31e-521">Wydajność i dostrajania</span><span class="sxs-lookup"><span data-stu-id="8e31e-521">Performance and Tuning</span></span>
<span data-ttu-id="8e31e-522">Zobacz [wydajności działania kopiowania & dostrajanie przewodnik](data-factory-copy-activity-performance.md) toolearn o kluczu czynniki tego wydajność wpływ przenoszenia danych (działanie kopiowania) w usłudze fabryka danych Azure i różne sposoby toooptimize go.</span><span class="sxs-lookup"><span data-stu-id="8e31e-522">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
