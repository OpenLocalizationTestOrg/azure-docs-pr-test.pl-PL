---
title: aaaMove danych do/z tabel Azure | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toomove danych do/z magazynem tabel Azure przy użyciu fabryki danych Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 07b046b1-7884-4e57-a613-337292416319
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jingwang
ms.openlocfilehash: 3dc3da6d88854674a9108b600534bc5d07575f15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooand-from-azure-table-using-azure-data-factory"></a><span data-ttu-id="39acb-103">Przenieś tooand danych z tabel Azure przy użyciu fabryki danych Azure</span><span class="sxs-lookup"><span data-stu-id="39acb-103">Move data tooand from Azure Table using Azure Data Factory</span></span>
<span data-ttu-id="39acb-104">W tym artykule opisano, jak toouse hello działanie kopiowania w fabryce danych Azure toomove danych z magazynu tabel platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="39acb-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data to/from Azure Table Storage.</span></span> <span data-ttu-id="39acb-105">Opiera się na powitania [działań przepływu danych](data-factory-data-movement-activities.md) artykułu, który przedstawia ogólny przegląd przenoszenia danych z hello działanie kopiowania.</span><span class="sxs-lookup"><span data-stu-id="39acb-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span> 

<span data-ttu-id="39acb-106">Możesz skopiować dane z dowolnych obsługiwanych źródeł danych magazynu tooAzure magazynu tabel lub z magazynu tabel Azure tooany obsługiwane ujścia danych.</span><span class="sxs-lookup"><span data-stu-id="39acb-106">You can copy data from any supported source data store tooAzure Table Storage or from Azure Table Storage tooany supported sink data store.</span></span> <span data-ttu-id="39acb-107">Lista magazynów danych obsługiwane jako źródła lub wychwytywanie przez działanie kopiowania hello, zobacz hello [obsługiwane magazyny danych](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabeli.</span><span class="sxs-lookup"><span data-stu-id="39acb-107">For a list of data stores supported as sources or sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> 

## <a name="getting-started"></a><span data-ttu-id="39acb-108">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="39acb-108">Getting started</span></span>
<span data-ttu-id="39acb-109">Można utworzyć potoku o działanie kopiowania, który przenosi dane z magazynu tabel Azure przy użyciu różnych narzędzi/interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="39acb-109">You can create a pipeline with a copy activity that moves data to/from an Azure Table Storage by using different tools/APIs.</span></span>

<span data-ttu-id="39acb-110">Witaj Najprostszym sposobem toocreate potoku jest toouse hello **kreatora kopiowania**.</span><span class="sxs-lookup"><span data-stu-id="39acb-110">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="39acb-111">Zobacz [samouczek: tworzenie potoku za pomocą Kreatora kopiowania](data-factory-copy-data-wizard-tutorial.md) szybkie przewodnik dotyczący tworzenia potoku za pomocą Kreatora dane Kopiuj hello.</span><span class="sxs-lookup"><span data-stu-id="39acb-111">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="39acb-112">Można również użyć hello następujące narzędzia toocreate potoku: **portalu Azure**, **programu Visual Studio**, **programu Azure PowerShell**, **szablonu usługi Azure Resource Manager** , **Interfejs API .NET**, i **interfejsu API REST**.</span><span class="sxs-lookup"><span data-stu-id="39acb-112">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="39acb-113">Zobacz [samouczek działania kopiowania](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) dla toocreate instrukcje krok po kroku potoku z działaniem kopiowania.</span><span class="sxs-lookup"><span data-stu-id="39acb-113">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="39acb-114">Czy za pomocą narzędzia hello lub interfejsów API, należy wykonać następujące kroki toocreate potok, który przenosi się, że magazyn danych ze źródła danych magazynu danych zbiornika tooa hello:</span><span class="sxs-lookup"><span data-stu-id="39acb-114">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span> 

1. <span data-ttu-id="39acb-115">Utwórz **połączone usługi** toolink usługi fabryka danych tooyour magazynów danych wejściowych i wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="39acb-115">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="39acb-116">Utwórz **zestawów danych** toorepresent wejściowe i wyjściowe dane hello operacji kopiowania.</span><span class="sxs-lookup"><span data-stu-id="39acb-116">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="39acb-117">Utwórz **potoku** aktywnością kopiowania zestawu danych jako dane wejściowe i zestawu danych jako dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="39acb-117">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="39acb-118">Korzystając z Kreatora hello, definicje JSON do tych jednostek fabryki danych (połączone usługi, zestawy danych i potoku hello) są tworzone automatycznie dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="39acb-118">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="39acb-119">Korzystając z narzędzi/API (z wyjątkiem interfejs API .NET), należy zdefiniować za pomocą formatu JSON hello tych jednostek fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="39acb-119">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="39acb-120">Aby uzyskać przykłady z definicji JSON dla jednostek fabryki danych, które są używane toocopy danych do/z magazynu tabel Azure, zobacz [przykłady JSON](#json-examples) sekcji tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="39acb-120">For samples with JSON definitions for Data Factory entities that are used toocopy data to/from an Azure Table Storage, see [JSON examples](#json-examples) section of this article.</span></span> 

<span data-ttu-id="39acb-121">Witaj następujące sekcje zawierają szczegółowe informacje o właściwości JSON, które są używane toodefine fabryki danych jednostek określonych tooAzure magazynu tabel:</span><span class="sxs-lookup"><span data-stu-id="39acb-121">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooAzure Table Storage:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="39acb-122">Połączona usługa właściwości</span><span class="sxs-lookup"><span data-stu-id="39acb-122">Linked service properties</span></span>
<span data-ttu-id="39acb-123">Istnieją dwa typy połączonych usług można użyć toolink fabryki danych Azure tooan magazynu obiektów blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="39acb-123">There are two types of linked services you can use toolink an Azure blob storage tooan Azure data factory.</span></span> <span data-ttu-id="39acb-124">Są one: **AzureStorage** połączonej usługi i **element AzureStorageSas** połączonej usługi.</span><span class="sxs-lookup"><span data-stu-id="39acb-124">They are: **AzureStorage** linked service and **AzureStorageSas** linked service.</span></span> <span data-ttu-id="39acb-125">Witaj połączoną usługą magazynu Azure zapewnia usłudze fabryka danych hello z toohello dostępu globalny usługi Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="39acb-125">hello Azure Storage linked service provides hello data factory with global access toohello Azure Storage.</span></span> <span data-ttu-id="39acb-126">Związana hello Azure magazyn SAS (Shared Access Signature) usługa zapewnia usłudze fabryka danych hello z toohello dostęp ograniczony/czas-powiązane z usługi Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="39acb-126">Whereas, hello Azure Storage SAS (Shared Access Signature) linked service provides hello data factory with restricted/time-bound access toohello Azure Storage.</span></span> <span data-ttu-id="39acb-127">Nie istnieją inne różnice między tych dwóch połączonych usług.</span><span class="sxs-lookup"><span data-stu-id="39acb-127">There are no other differences between these two linked services.</span></span> <span data-ttu-id="39acb-128">Wybierz usługę hello połączony, który odpowiada Twoim potrzebom.</span><span class="sxs-lookup"><span data-stu-id="39acb-128">Choose hello linked service that suits your needs.</span></span> <span data-ttu-id="39acb-129">Hello poniższe sekcje zawierają więcej szczegółowych informacji na temat tych dwóch usług połączonych.</span><span class="sxs-lookup"><span data-stu-id="39acb-129">hello following sections provide more details on these two linked services.</span></span>

[!INCLUDE [data-factory-azure-storage-linked-services](../../includes/data-factory-azure-storage-linked-services.md)]

## <a name="dataset-properties"></a><span data-ttu-id="39acb-130">Właściwości zestawu danych</span><span class="sxs-lookup"><span data-stu-id="39acb-130">Dataset properties</span></span>
<span data-ttu-id="39acb-131">Aby uzyskać pełną listę sekcje & właściwości dostępne do definiowania zestawów danych, zobacz hello [Tworzenie zbiorów danych](data-factory-create-datasets.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="39acb-131">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="39acb-132">Sekcje zawierają informacje, takie jak struktury, dostępności i zasad zestawu danych JSON są podobne dla wszystkich typów obiektów dataset (Azure SQL, obiektów blob platformy Azure, Azure tabeli itp.).</span><span class="sxs-lookup"><span data-stu-id="39acb-132">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="39acb-133">sekcja typeProperties Hello jest różne dla każdego typu zestawu danych i zawiera informacje o lokalizacji hello hello danych w magazynie danych hello.</span><span class="sxs-lookup"><span data-stu-id="39acb-133">hello typeProperties section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="39acb-134">Witaj **typeProperties** sekcja dla zestawu danych hello typu **AzureTable** ma hello następujące właściwości.</span><span class="sxs-lookup"><span data-stu-id="39acb-134">hello **typeProperties** section for hello dataset of type **AzureTable** has hello following properties.</span></span>

| <span data-ttu-id="39acb-135">Właściwość</span><span class="sxs-lookup"><span data-stu-id="39acb-135">Property</span></span> | <span data-ttu-id="39acb-136">Opis</span><span class="sxs-lookup"><span data-stu-id="39acb-136">Description</span></span> | <span data-ttu-id="39acb-137">Wymagane</span><span class="sxs-lookup"><span data-stu-id="39acb-137">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="39acb-138">tableName</span><span class="sxs-lookup"><span data-stu-id="39acb-138">tableName</span></span> |<span data-ttu-id="39acb-139">Nazwa tabeli hello w wystąpieniu bazy danych tabeli Azure hello, która jest połączona usługa odnosi się do.</span><span class="sxs-lookup"><span data-stu-id="39acb-139">Name of hello table in hello Azure Table Database instance that linked service refers to.</span></span> |<span data-ttu-id="39acb-140">Tak.</span><span class="sxs-lookup"><span data-stu-id="39acb-140">Yes.</span></span> <span data-ttu-id="39acb-141">TableName jest określona bez azureTableSourceQuery, wszystkie rekordy z tabeli hello są skopiowanych toohello docelowego.</span><span class="sxs-lookup"><span data-stu-id="39acb-141">When a tableName is specified without an azureTableSourceQuery, all records from hello table are copied toohello destination.</span></span> <span data-ttu-id="39acb-142">Jeśli określono również azureTableSourceQuery, rekordy z tabeli hello, która spełnia hello zapytania są skopiowanych toohello docelowego.</span><span class="sxs-lookup"><span data-stu-id="39acb-142">If an azureTableSourceQuery is also specified, records from hello table that satisfies hello query are copied toohello destination.</span></span> |

### <a name="schema-by-data-factory"></a><span data-ttu-id="39acb-143">Schemat fabryka danych</span><span class="sxs-lookup"><span data-stu-id="39acb-143">Schema by Data Factory</span></span>
<span data-ttu-id="39acb-144">Dla magazynów danych bez schematu, takie jak tabel Azure hello usługi fabryka danych wnioskuje schemat hello w jednym z hello następujące sposoby:</span><span class="sxs-lookup"><span data-stu-id="39acb-144">For schema-free data stores such as Azure Table, hello Data Factory service infers hello schema in one of hello following ways:</span></span>

1. <span data-ttu-id="39acb-145">Jeśli określisz hello struktury danych za pomocą hello **struktury** tej struktury Schema hello honoruje właściwości w definicji zestawu danych hello, hello usługi fabryka danych.</span><span class="sxs-lookup"><span data-stu-id="39acb-145">If you specify hello structure of data by using hello **structure** property in hello dataset definition, hello Data Factory service honors this structure as hello schema.</span></span> <span data-ttu-id="39acb-146">W tym przypadku jeśli wiersza nie zawiera wartości dla kolumny, wartość null podano dla niego.</span><span class="sxs-lookup"><span data-stu-id="39acb-146">In this case, if a row does not contain a value for a column, a null value is provided for it.</span></span>
2. <span data-ttu-id="39acb-147">Jeśli nie określisz hello struktury danych za pomocą hello **struktury** właściwości w definicji zestawu danych hello, fabryki danych wnioskuje schemat hello przy użyciu danych hello hello pierwszego wiersza.</span><span class="sxs-lookup"><span data-stu-id="39acb-147">If you don't specify hello structure of data by using hello **structure** property in hello dataset definition, Data Factory infers hello schema by using hello first row in hello data.</span></span> <span data-ttu-id="39acb-148">W takim przypadku jeśli pierwszy wiersz hello nie zawiera pełnej schematu hello, niektóre kolumny zostaną pominięte w hello wynik operacji kopiowania.</span><span class="sxs-lookup"><span data-stu-id="39acb-148">In this case, if hello first row does not contain hello full schema, some columns are missed in hello result of copy operation.</span></span>

<span data-ttu-id="39acb-149">W związku z tym dla źródeł danych bez schematu hello najlepszym rozwiązaniem jest toospecify hello struktury danych za pomocą hello **struktury** właściwości.</span><span class="sxs-lookup"><span data-stu-id="39acb-149">Therefore, for schema-free data sources, hello best practice is toospecify hello structure of data using hello **structure** property.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="39acb-150">Właściwości działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="39acb-150">Copy activity properties</span></span>
<span data-ttu-id="39acb-151">Pełną listę sekcje & właściwości dostępne do definiowania działań, zobacz hello [tworzenie potoków](data-factory-create-pipelines.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="39acb-151">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="39acb-152">Właściwości, takie jak nazwa, opis, dane wejściowe i wyjściowe zestawy danych i zasady są dostępne dla wszystkich typów działań.</span><span class="sxs-lookup"><span data-stu-id="39acb-152">Properties such as name, description, input and output datasets, and policies are available for all types of activities.</span></span>

<span data-ttu-id="39acb-153">Właściwości dostępne w sekcji typeProperties hello aktywności hello na powitania drugiej zależą od każdego typu działania.</span><span class="sxs-lookup"><span data-stu-id="39acb-153">Properties available in hello typeProperties section of hello activity on hello other hand vary with each activity type.</span></span> <span data-ttu-id="39acb-154">Dla działania kopiowania różnią się w zależności od typów hello źródeł i sink.</span><span class="sxs-lookup"><span data-stu-id="39acb-154">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="39acb-155">**AzureTableSource** obsługuje następujące właściwości w sekcji typeProperties hello:</span><span class="sxs-lookup"><span data-stu-id="39acb-155">**AzureTableSource** supports hello following properties in typeProperties section:</span></span>

| <span data-ttu-id="39acb-156">Właściwość</span><span class="sxs-lookup"><span data-stu-id="39acb-156">Property</span></span> | <span data-ttu-id="39acb-157">Opis</span><span class="sxs-lookup"><span data-stu-id="39acb-157">Description</span></span> | <span data-ttu-id="39acb-158">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="39acb-158">Allowed values</span></span> | <span data-ttu-id="39acb-159">Wymagane</span><span class="sxs-lookup"><span data-stu-id="39acb-159">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="39acb-160">azureTableSourceQuery</span><span class="sxs-lookup"><span data-stu-id="39acb-160">azureTableSourceQuery</span></span> |<span data-ttu-id="39acb-161">Użyj hello zapytanie niestandardowe tooread danych.</span><span class="sxs-lookup"><span data-stu-id="39acb-161">Use hello custom query tooread data.</span></span> |<span data-ttu-id="39acb-162">Ciąg zapytania tabeli platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="39acb-162">Azure table query string.</span></span> <span data-ttu-id="39acb-163">Przykłady w następnej sekcji hello.</span><span class="sxs-lookup"><span data-stu-id="39acb-163">See examples in hello next section.</span></span> |<span data-ttu-id="39acb-164">Nie.</span><span class="sxs-lookup"><span data-stu-id="39acb-164">No.</span></span> <span data-ttu-id="39acb-165">TableName jest określona bez azureTableSourceQuery, wszystkie rekordy z tabeli hello są skopiowanych toohello docelowego.</span><span class="sxs-lookup"><span data-stu-id="39acb-165">When a tableName is specified without an azureTableSourceQuery, all records from hello table are copied toohello destination.</span></span> <span data-ttu-id="39acb-166">Jeśli określono również azureTableSourceQuery, rekordy z tabeli hello, która spełnia hello zapytania są skopiowanych toohello docelowego.</span><span class="sxs-lookup"><span data-stu-id="39acb-166">If an azureTableSourceQuery is also specified, records from hello table that satisfies hello query are copied toohello destination.</span></span> |
| <span data-ttu-id="39acb-167">azureTableSourceIgnoreTableNotFound</span><span class="sxs-lookup"><span data-stu-id="39acb-167">azureTableSourceIgnoreTableNotFound</span></span> |<span data-ttu-id="39acb-168">Wskazuje, czy wyjątek hello swallow tabeli nie istnieją.</span><span class="sxs-lookup"><span data-stu-id="39acb-168">Indicate whether swallow hello exception of table not exist.</span></span> |<span data-ttu-id="39acb-169">WARTOŚĆ TRUE</span><span class="sxs-lookup"><span data-stu-id="39acb-169">TRUE</span></span><br/><span data-ttu-id="39acb-170">WARTOŚĆ FALSE</span><span class="sxs-lookup"><span data-stu-id="39acb-170">FALSE</span></span> |<span data-ttu-id="39acb-171">Nie</span><span class="sxs-lookup"><span data-stu-id="39acb-171">No</span></span> |

### <a name="azuretablesourcequery-examples"></a><span data-ttu-id="39acb-172">Przykłady azureTableSourceQuery</span><span class="sxs-lookup"><span data-stu-id="39acb-172">azureTableSourceQuery examples</span></span>
<span data-ttu-id="39acb-173">W przypadku tabel Azure kolumny typu string:</span><span class="sxs-lookup"><span data-stu-id="39acb-173">If Azure Table column is of string type:</span></span>

```JSON
azureTableSourceQuery": "$$Text.Format('PartitionKey ge \\'{0:yyyyMMddHH00_0000}\\' and PartitionKey le \\'{0:yyyyMMddHH00_9999}\\'', SliceStart)"
```

<span data-ttu-id="39acb-174">W przypadku tabel Azure kolumny typu Data/Godzina:</span><span class="sxs-lookup"><span data-stu-id="39acb-174">If Azure Table column is of datetime type:</span></span>

```JSON
"azureTableSourceQuery": "$$Text.Format('DeploymentEndTime gt datetime\\'{0:yyyy-MM-ddTHH:mm:ssZ}\\' and DeploymentEndTime le datetime\\'{1:yyyy-MM-ddTHH:mm:ssZ}\\'', SliceStart, SliceEnd)"
```

<span data-ttu-id="39acb-175">**AzureTableSink** obsługuje następujące właściwości w sekcji typeProperties hello:</span><span class="sxs-lookup"><span data-stu-id="39acb-175">**AzureTableSink** supports hello following properties in typeProperties section:</span></span>

| <span data-ttu-id="39acb-176">Właściwość</span><span class="sxs-lookup"><span data-stu-id="39acb-176">Property</span></span> | <span data-ttu-id="39acb-177">Opis</span><span class="sxs-lookup"><span data-stu-id="39acb-177">Description</span></span> | <span data-ttu-id="39acb-178">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="39acb-178">Allowed values</span></span> | <span data-ttu-id="39acb-179">Wymagane</span><span class="sxs-lookup"><span data-stu-id="39acb-179">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="39acb-180">azureTableDefaultPartitionKeyValue</span><span class="sxs-lookup"><span data-stu-id="39acb-180">azureTableDefaultPartitionKeyValue</span></span> |<span data-ttu-id="39acb-181">Domyślna wartość klucza partycji, które mogą być używane przez obiekt sink hello.</span><span class="sxs-lookup"><span data-stu-id="39acb-181">Default partition key value that can be used by hello sink.</span></span> |<span data-ttu-id="39acb-182">Wartość ciągu.</span><span class="sxs-lookup"><span data-stu-id="39acb-182">A string value.</span></span> |<span data-ttu-id="39acb-183">Nie</span><span class="sxs-lookup"><span data-stu-id="39acb-183">No</span></span> |
| <span data-ttu-id="39acb-184">azureTablePartitionKeyName</span><span class="sxs-lookup"><span data-stu-id="39acb-184">azureTablePartitionKeyName</span></span> |<span data-ttu-id="39acb-185">Określ nazwę kolumny hello, których wartości są używane jako klucze partycji.</span><span class="sxs-lookup"><span data-stu-id="39acb-185">Specify name of hello column whose values are used as partition keys.</span></span> <span data-ttu-id="39acb-186">Jeśli nie zostanie określony, AzureTableDefaultPartitionKeyValue jest używana jako klucza partycji hello.</span><span class="sxs-lookup"><span data-stu-id="39acb-186">If not specified, AzureTableDefaultPartitionKeyValue is used as hello partition key.</span></span> |<span data-ttu-id="39acb-187">Nazwa kolumny.</span><span class="sxs-lookup"><span data-stu-id="39acb-187">A column name.</span></span> |<span data-ttu-id="39acb-188">Nie</span><span class="sxs-lookup"><span data-stu-id="39acb-188">No</span></span> |
| <span data-ttu-id="39acb-189">azureTableRowKeyName</span><span class="sxs-lookup"><span data-stu-id="39acb-189">azureTableRowKeyName</span></span> |<span data-ttu-id="39acb-190">Określ nazwę kolumny hello, w których wartości kolumn używanych jako klucz wiersza.</span><span class="sxs-lookup"><span data-stu-id="39acb-190">Specify name of hello column whose column values are used as row key.</span></span> <span data-ttu-id="39acb-191">Jeśli nie zostanie określony, użyj identyfikatora GUID dla każdego wiersza.</span><span class="sxs-lookup"><span data-stu-id="39acb-191">If not specified, use a GUID for each row.</span></span> |<span data-ttu-id="39acb-192">Nazwa kolumny.</span><span class="sxs-lookup"><span data-stu-id="39acb-192">A column name.</span></span> |<span data-ttu-id="39acb-193">Nie</span><span class="sxs-lookup"><span data-stu-id="39acb-193">No</span></span> |
| <span data-ttu-id="39acb-194">azureTableInsertType</span><span class="sxs-lookup"><span data-stu-id="39acb-194">azureTableInsertType</span></span> |<span data-ttu-id="39acb-195">Tryb Hello tooinsert dane w tabeli platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="39acb-195">hello mode tooinsert data into Azure table.</span></span><br/><br/><span data-ttu-id="39acb-196">Ta właściwość określa, czy wartości zastąpienia lub scalić zostać istniejących wierszy w tabeli wyników hello ze zgodnymi kluczami partycji i wiersza.</span><span class="sxs-lookup"><span data-stu-id="39acb-196">This property controls whether existing rows in hello output table with matching partition and row keys have their values replaced or merged.</span></span> <br/><br/><span data-ttu-id="39acb-197">toolearn informacji na temat tych ustawień (scalania i Zastąp) działania, zobacz [wstawienia lub scalania jednostki](https://msdn.microsoft.com/library/azure/hh452241.aspx) i [wstawienia lub Zastąp jednostki](https://msdn.microsoft.com/library/azure/hh452242.aspx) tematów.</span><span class="sxs-lookup"><span data-stu-id="39acb-197">toolearn about how these settings (merge and replace) work, see [Insert or Merge Entity](https://msdn.microsoft.com/library/azure/hh452241.aspx) and [Insert or Replace Entity](https://msdn.microsoft.com/library/azure/hh452242.aspx) topics.</span></span> <br/><br> <span data-ttu-id="39acb-198">To ustawienie jest stosowane na poziomie wiersza hello, nie poziomu tabeli hello i żadna z tych opcji usuwa wiersze w tabeli wyników hello, które nie istnieją w danych wejściowych hello.</span><span class="sxs-lookup"><span data-stu-id="39acb-198">This setting applies at hello row level, not hello table level, and neither option deletes rows in hello output table that do not exist in hello input.</span></span> |<span data-ttu-id="39acb-199">Merge (ustawienie domyślne)</span><span class="sxs-lookup"><span data-stu-id="39acb-199">merge (default)</span></span><br/><span data-ttu-id="39acb-200">Zamień</span><span class="sxs-lookup"><span data-stu-id="39acb-200">replace</span></span> |<span data-ttu-id="39acb-201">Nie</span><span class="sxs-lookup"><span data-stu-id="39acb-201">No</span></span> |
| <span data-ttu-id="39acb-202">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="39acb-202">writeBatchSize</span></span> |<span data-ttu-id="39acb-203">Wstawia dane do hello tabeli platformy Azure, gdy zostaje trafiony hello writeBatchSize lub writeBatchTimeout.</span><span class="sxs-lookup"><span data-stu-id="39acb-203">Inserts data into hello Azure table when hello writeBatchSize or writeBatchTimeout is hit.</span></span> |<span data-ttu-id="39acb-204">Liczba całkowita (liczba wierszy)</span><span class="sxs-lookup"><span data-stu-id="39acb-204">Integer (number of rows)</span></span> |<span data-ttu-id="39acb-205">Nie (domyślne: 10000)</span><span class="sxs-lookup"><span data-stu-id="39acb-205">No (default: 10000)</span></span> |
| <span data-ttu-id="39acb-206">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="39acb-206">writeBatchTimeout</span></span> |<span data-ttu-id="39acb-207">Wstawia dane do hello tabeli platformy Azure, gdy zostaje trafiony hello writeBatchSize lub writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="39acb-207">Inserts data into hello Azure table when hello writeBatchSize or writeBatchTimeout is hit</span></span> |<span data-ttu-id="39acb-208">Zakres czasu</span><span class="sxs-lookup"><span data-stu-id="39acb-208">timespan</span></span><br/><br/><span data-ttu-id="39acb-209">Przykład: "00:20:00" (20 minut)</span><span class="sxs-lookup"><span data-stu-id="39acb-209">Example: “00:20:00” (20 minutes)</span></span> |<span data-ttu-id="39acb-210">Nie (domyślna toostorage klienta domyślny limit czasu operacji wartość 90 s)</span><span class="sxs-lookup"><span data-stu-id="39acb-210">No (Default toostorage client default timeout value 90 sec)</span></span> |

### <a name="azuretablepartitionkeyname"></a><span data-ttu-id="39acb-211">azureTablePartitionKeyName</span><span class="sxs-lookup"><span data-stu-id="39acb-211">azureTablePartitionKeyName</span></span>
<span data-ttu-id="39acb-212">Mapowanie kolumny docelowej tooa kolumny źródła przy użyciu właściwości JSON translator hello, zanim będzie możliwe użycie kolumna docelowa hello jako hello azureTablePartitionKeyName.</span><span class="sxs-lookup"><span data-stu-id="39acb-212">Map a source column tooa destination column using hello translator JSON property before you can use hello destination column as hello azureTablePartitionKeyName.</span></span>

<span data-ttu-id="39acb-213">W hello poniższy przykład, kolumna źródłowa DivisionID jest kolumna docelowa zamapowanych toohello: DivisionID.</span><span class="sxs-lookup"><span data-stu-id="39acb-213">In hello following example, source column DivisionID is mapped toohello destination column: DivisionID.</span></span>  

```JSON
"translator": {
    "type": "TabularTranslator",
    "columnMappings": "DivisionID: DivisionID, FirstName: FirstName, LastName: LastName"
}
```
<span data-ttu-id="39acb-214">Witaj DivisionID jest określony jako klucza partycji hello.</span><span class="sxs-lookup"><span data-stu-id="39acb-214">hello DivisionID is specified as hello partition key.</span></span>

```JSON
"sink": {
    "type": "AzureTableSink",
    "azureTablePartitionKeyName": "DivisionID",
    "writeBatchSize": 100,
    "writeBatchTimeout": "01:00:00"
}
```
## <a name="json-examples"></a><span data-ttu-id="39acb-215">Przykłady JSON</span><span class="sxs-lookup"><span data-stu-id="39acb-215">JSON examples</span></span>
<span data-ttu-id="39acb-216">Witaj poniższe przykłady zapewniają definicje JSON przy użyciu można toocreate potoku [portalu Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) lub [programu Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) lub [programu Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="39acb-216">hello following examples provide sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="39acb-217">Przedstawiają sposób toocopy tooand danych z magazynu tabel platformy Azure i bazy danych obiektów Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="39acb-217">They show how toocopy data tooand from Azure Table Storage and Azure Blob Database.</span></span> <span data-ttu-id="39acb-218">Jednak dane mogą być kopiowane **bezpośrednio** za pomocą dowolnego hello tooany źródeł z wychwytywanie hello obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="39acb-218">However, data can be copied **directly** from any of hello sources tooany of hello supported sinks.</span></span> <span data-ttu-id="39acb-219">Aby uzyskać więcej informacji, zobacz sekcję hello, "obsługiwane magazyny danych i formaty" w [przenoszenia danych za pomocą działania kopiowania](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="39acb-219">For more information, see hello section "Supported data stores and formats" in [Move data by using Copy Activity](data-factory-data-movement-activities.md).</span></span>

## <a name="example-copy-data-from-azure-table-tooazure-blob"></a><span data-ttu-id="39acb-220">Przykład: Kopiowanie danych z tabel Azure tooAzure obiektów Blob</span><span class="sxs-lookup"><span data-stu-id="39acb-220">Example: Copy data from Azure Table tooAzure Blob</span></span>
<span data-ttu-id="39acb-221">następujące przykładowe pokazuje Hello:</span><span class="sxs-lookup"><span data-stu-id="39acb-221">hello following sample shows:</span></span>

1. <span data-ttu-id="39acb-222">Połączonej usługi typu [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) (używane dla obiekt blob & tabeli).</span><span class="sxs-lookup"><span data-stu-id="39acb-222">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) (used for both table & blob).</span></span>
2. <span data-ttu-id="39acb-223">Dane wejściowe [dataset](data-factory-create-datasets.md) typu [AzureTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="39acb-223">An input [dataset](data-factory-create-datasets.md) of type [AzureTable](#dataset-properties).</span></span>
3. <span data-ttu-id="39acb-224">Dane wyjściowe [dataset](data-factory-create-datasets.md) typu [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="39acb-224">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="39acb-225">Witaj [potoku](data-factory-create-pipelines.md) z działaniem kopii, która używa [AzureTableSource](#activity-properties) i [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="39acb-225">hello [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [AzureTableSource](#activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="39acb-226">przykład Witaj kopiuje dane należące toohello domyślnej partycji w obiekcie blob tooa tabel Azure co godzinę.</span><span class="sxs-lookup"><span data-stu-id="39acb-226">hello sample copies data belonging toohello default partition in an Azure Table tooa blob every hour.</span></span> <span data-ttu-id="39acb-227">właściwości JSON Hello używane w te przykłady są opisane w sekcjach poniżej hello próbek.</span><span class="sxs-lookup"><span data-stu-id="39acb-227">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="39acb-228">**Połączonej usługi magazynu Azure:**</span><span class="sxs-lookup"><span data-stu-id="39acb-228">**Azure storage linked service:**</span></span>

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
<span data-ttu-id="39acb-229">Fabryka danych Azure obsługuje dwa typy usług magazynu Azure połączony: **AzureStorage** i **element AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="39acb-229">Azure Data Factory supports two types of Azure Storage linked services: **AzureStorage** and **AzureStorageSas**.</span></span> <span data-ttu-id="39acb-230">Dla hello pierwszego z nich, określ ciąg połączenia hello, który zawiera klucz konta hello i dla hello późniejszą, należy określić hello Uri dostępu sygnatury dostępu Współdzielonego.</span><span class="sxs-lookup"><span data-stu-id="39acb-230">For hello first one, you specify hello connection string that includes hello account key and for hello later one, you specify hello Shared Access Signature (SAS) Uri.</span></span> <span data-ttu-id="39acb-231">Zobacz [połączonych usług](#linked-service-properties) sekcji, aby uzyskać szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="39acb-231">See [Linked Services](#linked-service-properties) section for details.</span></span>  

<span data-ttu-id="39acb-232">**Azure tabeli wejściowy zestaw danych:**</span><span class="sxs-lookup"><span data-stu-id="39acb-232">**Azure Table input dataset:**</span></span>

<span data-ttu-id="39acb-233">przykład Witaj przyjęto założenie, że utworzono tabelę "MyTable" w tabeli platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="39acb-233">hello sample assumes you have created a table “MyTable” in Azure Table.</span></span>

<span data-ttu-id="39acb-234">Ustawienie "external": "prawda" informuje hello usługi fabryka danych tego elementu dataset hello zewnętrznych toohello fabryki danych i nie jest generowany przez działanie w fabryce danych hello.</span><span class="sxs-lookup"><span data-stu-id="39acb-234">Setting “external”: ”true” informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```JSON
{
  "name": "AzureTableInput",
  "properties": {
    "type": "AzureTable",
    "linkedServiceName": "StorageLinkedService",
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

<span data-ttu-id="39acb-235">**Azure Blob wyjściowy zestaw danych:**</span><span class="sxs-lookup"><span data-stu-id="39acb-235">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="39acb-236">Dane są zapisywane tooa nowych obiektów blob, co godzinę (częstotliwość: godziny, interwał: 1).</span><span class="sxs-lookup"><span data-stu-id="39acb-236">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="39acb-237">Ścieżka folderu Hello hello obiektu blob dynamicznie jest obliczane na podstawie czasu rozpoczęcia hello hello wycinek, który jest przetwarzana.</span><span class="sxs-lookup"><span data-stu-id="39acb-237">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="39acb-238">Ścieżka folderu Hello używa rok, miesiąc, dzień i godziny części hello czas rozpoczęcia.</span><span class="sxs-lookup"><span data-stu-id="39acb-238">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

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

<span data-ttu-id="39acb-239">**Działanie kopiowania w potoku z AzureTableSource i BlobSink:**</span><span class="sxs-lookup"><span data-stu-id="39acb-239">**Copy activity in a pipeline with AzureTableSource and BlobSink:**</span></span>

<span data-ttu-id="39acb-240">Witaj potoku zawiera działanie kopiowania, który jest skonfigurowany toouse hello wejściowych i wyjściowych zestawów danych i jest toorun zaplanowane co godzinę.</span><span class="sxs-lookup"><span data-stu-id="39acb-240">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="39acb-241">W potoku hello definicji JSON, hello **źródła** typu ustawiono zbyt**AzureTableSource** i **zbiornika** typu ustawiono zbyt**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="39acb-241">In hello pipeline JSON definition, hello **source** type is set too**AzureTableSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="39acb-242">Zapytanie SQL Hello określony za pomocą **AzureTableSourceQuery** właściwości wybiera hello danych z partycji domyślnej hello toocopy co godzinę.</span><span class="sxs-lookup"><span data-stu-id="39acb-242">hello SQL query specified with **AzureTableSourceQuery** property selects hello data from hello default partition every hour toocopy.</span></span>

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-01T19:00:00",
        "description":"pipeline for copy activity",
        "activities":[  
            {
                "name": "AzureTabletoBlob",
                "description": "copy activity",
                "type": "Copy",
                "inputs": [
                      {
                        "name": "AzureTableInput"
                    }
                ],
                "outputs": [
                      {
                            "name": "AzureBlobOutput"
                      }
                ],
                "typeProperties": {
                      "source": {
                        "type": "AzureTableSource",
                        "AzureTableSourceQuery": "PartitionKey eq 'DefaultPartitionKey'"
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

## <a name="example-copy-data-from-azure-blob-tooazure-table"></a><span data-ttu-id="39acb-243">Przykład: Kopiowanie danych z obiektu Blob Azure tooAzure tabeli</span><span class="sxs-lookup"><span data-stu-id="39acb-243">Example: Copy data from Azure Blob tooAzure Table</span></span>
<span data-ttu-id="39acb-244">następujące przykładowe pokazuje Hello:</span><span class="sxs-lookup"><span data-stu-id="39acb-244">hello following sample shows:</span></span>

1. <span data-ttu-id="39acb-245">Połączonej usługi typu [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) (używane dla obiekt blob & tabeli)</span><span class="sxs-lookup"><span data-stu-id="39acb-245">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) (used for both table & blob)</span></span>
2. <span data-ttu-id="39acb-246">Dane wejściowe [dataset](data-factory-create-datasets.md) typu [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="39acb-246">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
3. <span data-ttu-id="39acb-247">Dane wyjściowe [dataset](data-factory-create-datasets.md) typu [AzureTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="39acb-247">An output [dataset](data-factory-create-datasets.md) of type [AzureTable](#dataset-properties).</span></span>
4. <span data-ttu-id="39acb-248">Witaj [potoku](data-factory-create-pipelines.md) z działaniem kopii, która używa [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) i [AzureTableSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="39acb-248">hello [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [AzureTableSink](#copy-activity-properties).</span></span>

<span data-ttu-id="39acb-249">Przykładowe Hello kopiuje dane szeregów czasowych co godzinę z tooan obiektów blob platformy Azure tabeli platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="39acb-249">hello sample copies time-series data from an Azure blob tooan Azure table hourly.</span></span> <span data-ttu-id="39acb-250">właściwości JSON Hello używane w te przykłady są opisane w sekcjach poniżej hello próbek.</span><span class="sxs-lookup"><span data-stu-id="39acb-250">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="39acb-251">**Usługa Azure storage (dla tabeli platformy Azure i obiektów Blob) połączonej usługi:**</span><span class="sxs-lookup"><span data-stu-id="39acb-251">**Azure storage (for both Azure Table & Blob) linked service:**</span></span>

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

<span data-ttu-id="39acb-252">Fabryka danych Azure obsługuje dwa typy usług magazynu Azure połączony: **AzureStorage** i **element AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="39acb-252">Azure Data Factory supports two types of Azure Storage linked services: **AzureStorage** and **AzureStorageSas**.</span></span> <span data-ttu-id="39acb-253">Dla hello pierwszego z nich, określ ciąg połączenia hello, który zawiera klucz konta hello i dla hello późniejszą, należy określić hello Uri dostępu sygnatury dostępu Współdzielonego.</span><span class="sxs-lookup"><span data-stu-id="39acb-253">For hello first one, you specify hello connection string that includes hello account key and for hello later one, you specify hello Shared Access Signature (SAS) Uri.</span></span> <span data-ttu-id="39acb-254">Zobacz [połączonych usług](#linked-service-properties) sekcji, aby uzyskać szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="39acb-254">See [Linked Services](#linked-service-properties) section for details.</span></span>

<span data-ttu-id="39acb-255">**Azure wejściowego zestawu danych obiektów Blob:**</span><span class="sxs-lookup"><span data-stu-id="39acb-255">**Azure Blob input dataset:**</span></span>

<span data-ttu-id="39acb-256">Dane są pobierane z nowego obiektu blob co godzinę (częstotliwość: godziny, interwał: 1).</span><span class="sxs-lookup"><span data-stu-id="39acb-256">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="39acb-257">Witaj folderu ścieżkę i nazwę pliku dla obiekt blob hello dynamicznie są oceniane na podstawie czasu rozpoczęcia hello hello wycinek, który jest przetwarzana.</span><span class="sxs-lookup"><span data-stu-id="39acb-257">hello folder path and file name for hello blob are dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="39acb-258">Ścieżka folderu Hello korzysta rok, miesiąc i dzień część czas rozpoczęcia hello, a nazwa pliku hello część hello czas rozpoczęcia.</span><span class="sxs-lookup"><span data-stu-id="39acb-258">hello folder path uses year, month, and day part of hello start time and file name uses hello hour part of hello start time.</span></span> <span data-ttu-id="39acb-259">"external": "prawda" ustawienie informuje hello usługi fabryka danych tego elementu dataset hello zewnętrznych toohello fabryki danych i nie jest generowany przez działanie w fabryce danych hello.</span><span class="sxs-lookup"><span data-stu-id="39acb-259">“external”: “true” setting informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

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

<span data-ttu-id="39acb-260">**Tabeli platformy Azure wyjściowy zestaw danych:**</span><span class="sxs-lookup"><span data-stu-id="39acb-260">**Azure Table output dataset:**</span></span>

<span data-ttu-id="39acb-261">przykład Witaj kopiuje tabeli tooa danych o nazwie "MyTable" w tabeli platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="39acb-261">hello sample copies data tooa table named “MyTable” in Azure Table.</span></span> <span data-ttu-id="39acb-262">Tworzenie tabeli platformy Azure z hello taką samą liczbę kolumn, zgodnie z oczekiwaniami toocontain pliku Blob CSV hello.</span><span class="sxs-lookup"><span data-stu-id="39acb-262">Create an Azure table with hello same number of columns as you expect hello Blob CSV file toocontain.</span></span> <span data-ttu-id="39acb-263">Dodawaniu nowych wierszy tabeli toohello co godzinę.</span><span class="sxs-lookup"><span data-stu-id="39acb-263">New rows are added toohello table every hour.</span></span>

```JSON
{
  "name": "AzureTableOutput",
  "properties": {
    "type": "AzureTable",
    "linkedServiceName": "StorageLinkedService",
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

<span data-ttu-id="39acb-264">**Działanie kopiowania w potoku z BlobSource i AzureTableSink:**</span><span class="sxs-lookup"><span data-stu-id="39acb-264">**Copy activity in a pipeline with BlobSource and AzureTableSink:**</span></span>

<span data-ttu-id="39acb-265">Witaj potoku zawiera działanie kopiowania, który jest skonfigurowany toouse hello wejściowych i wyjściowych zestawów danych i jest toorun zaplanowane co godzinę.</span><span class="sxs-lookup"><span data-stu-id="39acb-265">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="39acb-266">W potoku hello definicji JSON, hello **źródła** typu ustawiono zbyt**BlobSource** i **zbiornika** typu ustawiono zbyt**AzureTableSink**.</span><span class="sxs-lookup"><span data-stu-id="39acb-266">In hello pipeline JSON definition, hello **source** type is set too**BlobSource** and **sink** type is set too**AzureTableSink**.</span></span>

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "AzureBlobtoTable",
        "description": "Copy Activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureBlobInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureTableOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource"
          },
          "sink": {
            "type": "AzureTableSink",
            "writeBatchSize": 100,
            "writeBatchTimeout": "01:00:00"
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
## <a name="type-mapping-for-azure-table"></a><span data-ttu-id="39acb-267">Mapowanie typu dla tabeli platformy Azure</span><span class="sxs-lookup"><span data-stu-id="39acb-267">Type Mapping for Azure Table</span></span>
<span data-ttu-id="39acb-268">Jak wspomniano w hello [działań przepływu danych](data-factory-data-movement-activities.md) wykonuje działanie kopiowania artykułu, automatyczne konwersje z typów toosink typy źródła z powitania po rozwinięcie.</span><span class="sxs-lookup"><span data-stu-id="39acb-268">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types toosink types with hello following two-step approach.</span></span>

1. <span data-ttu-id="39acb-269">Konwertować z typu too.NET typów natywnych źródła</span><span class="sxs-lookup"><span data-stu-id="39acb-269">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="39acb-270">Konwertować z typu sink toonative typu .NET</span><span class="sxs-lookup"><span data-stu-id="39acb-270">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="39acb-271">Podczas przenoszenia danych za & z tabel Azure, hello po [mapowania zdefiniowane przez usługę Azure tabeli](https://msdn.microsoft.com/library/azure/dd179338.aspx) są używane z typu too.NET typy OData tabeli platformy Azure i na odwrót.</span><span class="sxs-lookup"><span data-stu-id="39acb-271">When moving data too& from Azure Table, hello following [mappings defined by Azure Table service](https://msdn.microsoft.com/library/azure/dd179338.aspx) are used from Azure Table OData types too.NET type and vice versa.</span></span>

| <span data-ttu-id="39acb-272">Typ danych OData</span><span class="sxs-lookup"><span data-stu-id="39acb-272">OData Data Type</span></span> | <span data-ttu-id="39acb-273">Typ architektury .NET</span><span class="sxs-lookup"><span data-stu-id="39acb-273">.NET Type</span></span> | <span data-ttu-id="39acb-274">Szczegóły</span><span class="sxs-lookup"><span data-stu-id="39acb-274">Details</span></span> |
| --- | --- | --- |
| <span data-ttu-id="39acb-275">Edm.Binary</span><span class="sxs-lookup"><span data-stu-id="39acb-275">Edm.Binary</span></span> |<span data-ttu-id="39acb-276">Byte]</span><span class="sxs-lookup"><span data-stu-id="39acb-276">byte[]</span></span> |<span data-ttu-id="39acb-277">Tablica bajtów się too64 KB.</span><span class="sxs-lookup"><span data-stu-id="39acb-277">An array of bytes up too64 KB.</span></span> |
| <span data-ttu-id="39acb-278">Edm.Boolean</span><span class="sxs-lookup"><span data-stu-id="39acb-278">Edm.Boolean</span></span> |<span data-ttu-id="39acb-279">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="39acb-279">bool</span></span> |<span data-ttu-id="39acb-280">Wartość logiczna.</span><span class="sxs-lookup"><span data-stu-id="39acb-280">A Boolean value.</span></span> |
| <span data-ttu-id="39acb-281">Edm.DateTime</span><span class="sxs-lookup"><span data-stu-id="39acb-281">Edm.DateTime</span></span> |<span data-ttu-id="39acb-282">Data i godzina</span><span class="sxs-lookup"><span data-stu-id="39acb-282">DateTime</span></span> |<span data-ttu-id="39acb-283">Wartość 64-bitowa, wyrażone jako uniwersalny czas koordynowany (UTC).</span><span class="sxs-lookup"><span data-stu-id="39acb-283">A 64-bit value expressed as Coordinated Universal Time (UTC).</span></span> <span data-ttu-id="39acb-284">Witaj obsługiwany zakres zaczyna się od 12:00, a 1 stycznia, 1601 r. N.E. daty/godziny</span><span class="sxs-lookup"><span data-stu-id="39acb-284">hello supported DateTime range begins from 12:00 midnight, January 1, 1601 A.D.</span></span> <span data-ttu-id="39acb-285">(R), CZAS UTC.</span><span class="sxs-lookup"><span data-stu-id="39acb-285">(C.E.), UTC.</span></span> <span data-ttu-id="39acb-286">zakres Hello kończy się na 31 grudnia 9999 r.</span><span class="sxs-lookup"><span data-stu-id="39acb-286">hello range ends at December 31, 9999.</span></span> |
| <span data-ttu-id="39acb-287">Edm.Double</span><span class="sxs-lookup"><span data-stu-id="39acb-287">Edm.Double</span></span> |<span data-ttu-id="39acb-288">O podwójnej precyzji</span><span class="sxs-lookup"><span data-stu-id="39acb-288">double</span></span> |<span data-ttu-id="39acb-289">64-bitowej zmiennej punktu wartości.</span><span class="sxs-lookup"><span data-stu-id="39acb-289">A 64-bit floating point value.</span></span> |
| <span data-ttu-id="39acb-290">Edm.Guid</span><span class="sxs-lookup"><span data-stu-id="39acb-290">Edm.Guid</span></span> |<span data-ttu-id="39acb-291">Identyfikator GUID</span><span class="sxs-lookup"><span data-stu-id="39acb-291">Guid</span></span> |<span data-ttu-id="39acb-292">Globalnie unikatowy identyfikator 128-bitowego.</span><span class="sxs-lookup"><span data-stu-id="39acb-292">A 128-bit globally unique identifier.</span></span> |
| <span data-ttu-id="39acb-293">Edm.Int32</span><span class="sxs-lookup"><span data-stu-id="39acb-293">Edm.Int32</span></span> |<span data-ttu-id="39acb-294">Int32</span><span class="sxs-lookup"><span data-stu-id="39acb-294">Int32</span></span> |<span data-ttu-id="39acb-295">32-bitową liczbę całkowitą.</span><span class="sxs-lookup"><span data-stu-id="39acb-295">A 32-bit integer.</span></span> |
| <span data-ttu-id="39acb-296">Edm.Int64</span><span class="sxs-lookup"><span data-stu-id="39acb-296">Edm.Int64</span></span> |<span data-ttu-id="39acb-297">Int64</span><span class="sxs-lookup"><span data-stu-id="39acb-297">Int64</span></span> |<span data-ttu-id="39acb-298">64-bitową liczbę całkowitą.</span><span class="sxs-lookup"><span data-stu-id="39acb-298">A 64-bit integer.</span></span> |
| <span data-ttu-id="39acb-299">Edm.String</span><span class="sxs-lookup"><span data-stu-id="39acb-299">Edm.String</span></span> |<span data-ttu-id="39acb-300">Ciąg</span><span class="sxs-lookup"><span data-stu-id="39acb-300">String</span></span> |<span data-ttu-id="39acb-301">Wartość algorytmem UTF-16.</span><span class="sxs-lookup"><span data-stu-id="39acb-301">A UTF-16-encoded value.</span></span> <span data-ttu-id="39acb-302">Wartości parametrów może być aktywne too64 KB.</span><span class="sxs-lookup"><span data-stu-id="39acb-302">String values may be up too64 KB.</span></span> |

### <a name="type-conversion-sample"></a><span data-ttu-id="39acb-303">Przykładowe konwersji typu</span><span class="sxs-lookup"><span data-stu-id="39acb-303">Type Conversion Sample</span></span>
<span data-ttu-id="39acb-304">następujące przykładowe Hello jest kopiowania danych z tabeli tooAzure obiektów Blob platformy Azure z konwersji typu.</span><span class="sxs-lookup"><span data-stu-id="39acb-304">hello following sample is for copying data from an Azure Blob tooAzure Table with type conversions.</span></span>

<span data-ttu-id="39acb-305">Załóżmy, że hello zestawu danych obiektów Blob jest w formacie CSV zawiera trzy kolumny.</span><span class="sxs-lookup"><span data-stu-id="39acb-305">Suppose hello Blob dataset is in CSV format and contains three columns.</span></span> <span data-ttu-id="39acb-306">Jeden z nich jest kolumną daty/godziny w formacie datetime niestandardowych za pomocą nazwy skróconej francuskim dzień tygodnia hello.</span><span class="sxs-lookup"><span data-stu-id="39acb-306">One of them is a datetime column with a custom datetime format using abbreviated French names for day of hello week.</span></span>

<span data-ttu-id="39acb-307">Definiowanie zestawu danych obiektów Blob źródła hello następujący wraz z definicji typu dla kolumny hello.</span><span class="sxs-lookup"><span data-stu-id="39acb-307">Define hello Blob Source dataset as follows along with type definitions for hello columns.</span></span>

```JSON
{
    "name": " AzureBlobInput",
    "properties":
    {
         "structure":
          [
                { "name": "userid", "type": "Int64"},
                { "name": "name", "type": "String"},
                { "name": "lastlogindate", "type": "Datetime", "culture": "fr-fr", "format": "ddd-MM-YYYY"}
          ],
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/myfolder",
            "fileName":"myfile.csv",
            "format":
            {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "external": true,
        "availability":
        {
            "frequency": "Hour",
            "interval": 1,
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
<span data-ttu-id="39acb-308">Biorąc pod uwagę mapowanie typu hello z too.NET typu OData tabeli platformy Azure, czy definiuje hello tabeli w tabeli platformy Azure z hello następującego schematu.</span><span class="sxs-lookup"><span data-stu-id="39acb-308">Given hello type mapping from Azure Table OData type too.NET type, you would define hello table in Azure Table with hello following schema.</span></span>

<span data-ttu-id="39acb-309">**Schemat tabeli platformy Azure:**</span><span class="sxs-lookup"><span data-stu-id="39acb-309">**Azure Table schema:**</span></span>

| <span data-ttu-id="39acb-310">Nazwa kolumny</span><span class="sxs-lookup"><span data-stu-id="39acb-310">Column name</span></span> | <span data-ttu-id="39acb-311">Typ</span><span class="sxs-lookup"><span data-stu-id="39acb-311">Type</span></span> |
| --- | --- |
| <span data-ttu-id="39acb-312">Nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="39acb-312">userid</span></span> |<span data-ttu-id="39acb-313">Edm.Int64</span><span class="sxs-lookup"><span data-stu-id="39acb-313">Edm.Int64</span></span> |
| <span data-ttu-id="39acb-314">name</span><span class="sxs-lookup"><span data-stu-id="39acb-314">name</span></span> |<span data-ttu-id="39acb-315">Edm.String</span><span class="sxs-lookup"><span data-stu-id="39acb-315">Edm.String</span></span> |
| <span data-ttu-id="39acb-316">lastlogindate</span><span class="sxs-lookup"><span data-stu-id="39acb-316">lastlogindate</span></span> |<span data-ttu-id="39acb-317">Edm.DateTime</span><span class="sxs-lookup"><span data-stu-id="39acb-317">Edm.DateTime</span></span> |

<span data-ttu-id="39acb-318">Następnie określ następujący hello Azure tabeli dataset.</span><span class="sxs-lookup"><span data-stu-id="39acb-318">Next, define hello Azure Table dataset as follows.</span></span> <span data-ttu-id="39acb-319">Nie trzeba toospecify "structure" sekcji informacji o typach powitania od informacji o typie hello został już określony w hello bazowy magazynu danych.</span><span class="sxs-lookup"><span data-stu-id="39acb-319">You do not need toospecify “structure” section with hello type information since hello type information is already specified in hello underlying data store.</span></span>

```JSON
{
  "name": "AzureTableOutput",
  "properties": {
    "type": "AzureTable",
    "linkedServiceName": "StorageLinkedService",
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

<span data-ttu-id="39acb-320">W takim przypadku fabryka danych automatycznie konwersje typów tym hello pola daty/godziny w formacie datetime niestandardowych hello przy użyciu kultury "fr-fr" hello, podczas przenoszenia danych z obiektu Blob tooAzure tabeli.</span><span class="sxs-lookup"><span data-stu-id="39acb-320">In this case, Data Factory automatically does type conversions including hello Datetime field with hello custom datetime format using hello "fr-fr" culture when moving data from Blob tooAzure Table.</span></span>

> [!NOTE]
> <span data-ttu-id="39acb-321">toomap kolumny źródłowej toocolumns zestawu danych z obiektu sink zestawu danych, zobacz [mapowania kolumnach dataset w fabryce danych Azure](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="39acb-321">toomap columns from source dataset toocolumns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="39acb-322">Wydajność i dostrajania</span><span class="sxs-lookup"><span data-stu-id="39acb-322">Performance and Tuning</span></span>
<span data-ttu-id="39acb-323">toolearn o kluczu czynniki tego wydajność wpływ przenoszenia danych (działanie kopiowania) w usłudze fabryka danych Azure i różne sposoby toooptimize, zobacz [wydajności działania kopiowania & dostrajanie przewodnik](data-factory-copy-activity-performance.md).</span><span class="sxs-lookup"><span data-stu-id="39acb-323">toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it, see [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md).</span></span>
