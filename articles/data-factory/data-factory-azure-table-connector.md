---
title: Przenoszenie danych do/z tabel Azure | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak przenieść dane z magazynem tabel Azure przy użyciu fabryki danych Azure."
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
ms.openlocfilehash: 792a551ae3dae46c503e5f0dda74cd0ac3a69c3a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="move-data-to-and-from-azure-table-using-azure-data-factory"></a><span data-ttu-id="dc914-103">Przenoszenie danych do i z tabel Azure przy użyciu fabryki danych Azure</span><span class="sxs-lookup"><span data-stu-id="dc914-103">Move data to and from Azure Table using Azure Data Factory</span></span>
<span data-ttu-id="dc914-104">W tym artykule opisano sposób używania działania kopiowania w fabryce danych Azure do przeniesienia danych z magazynu tabel platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="dc914-104">This article explains how to use the Copy Activity in Azure Data Factory to move data to/from Azure Table Storage.</span></span> <span data-ttu-id="dc914-105">Opiera się na [działań przepływu danych](data-factory-data-movement-activities.md) artykułu, który przedstawia ogólny przegląd przenoszenia danych z działania kopiowania.</span><span class="sxs-lookup"><span data-stu-id="dc914-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span> 

<span data-ttu-id="dc914-106">Można skopiować danych z dowolnej obsługiwanej źródłowej magazynu danych do magazynu tabel platformy Azure lub z magazynu tabel Azure żadnych obsługiwanych ujścia magazynu danych.</span><span class="sxs-lookup"><span data-stu-id="dc914-106">You can copy data from any supported source data store to Azure Table Storage or from Azure Table Storage to any supported sink data store.</span></span> <span data-ttu-id="dc914-107">Lista magazynów danych obsługiwane jako źródła lub wychwytywanie przez działanie kopiowania, zobacz [obsługiwane magazyny danych](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabeli.</span><span class="sxs-lookup"><span data-stu-id="dc914-107">For a list of data stores supported as sources or sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> 

## <a name="getting-started"></a><span data-ttu-id="dc914-108">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="dc914-108">Getting started</span></span>
<span data-ttu-id="dc914-109">Można utworzyć potoku o działanie kopiowania, który przenosi dane z magazynu tabel Azure przy użyciu różnych narzędzi/interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="dc914-109">You can create a pipeline with a copy activity that moves data to/from an Azure Table Storage by using different tools/APIs.</span></span>

<span data-ttu-id="dc914-110">Najprostszym sposobem, aby utworzyć potok jest użycie **kreatora kopiowania**.</span><span class="sxs-lookup"><span data-stu-id="dc914-110">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="dc914-111">Zobacz [samouczek: tworzenie potoku za pomocą Kreatora kopiowania](data-factory-copy-data-wizard-tutorial.md) szybkie przewodnik dotyczący tworzenia potoku za pomocą Kreatora kopiowania danych.</span><span class="sxs-lookup"><span data-stu-id="dc914-111">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="dc914-112">Umożliwia także następujące narzędzia do tworzenia potoku: **portalu Azure**, **programu Visual Studio**, **programu Azure PowerShell**, **szablonu usługi Azure Resource Manager**, **interfejs API .NET**, i **interfejsu API REST**.</span><span class="sxs-lookup"><span data-stu-id="dc914-112">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="dc914-113">Zobacz [samouczek działania kopiowania](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) instrukcje krok po kroku utworzyć potok z działaniem kopiowania.</span><span class="sxs-lookup"><span data-stu-id="dc914-113">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="dc914-114">Czy można użyć narzędzia i interfejsy API, należy wykonać następujące kroki, aby utworzyć potok, który przenosi dane z magazynu danych źródła do ujścia magazynu danych:</span><span class="sxs-lookup"><span data-stu-id="dc914-114">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span> 

1. <span data-ttu-id="dc914-115">Utwórz **połączone usługi** Aby połączyć dane wejściowe i wyjściowe są przechowywane w fabryce danych.</span><span class="sxs-lookup"><span data-stu-id="dc914-115">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="dc914-116">Utwórz **zestawów danych** do reprezentowania danych wejściowych i wyjściowych operacji kopiowania.</span><span class="sxs-lookup"><span data-stu-id="dc914-116">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="dc914-117">Utwórz **potoku** aktywnością kopiowania zestawu danych jako dane wejściowe i zestawu danych jako dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="dc914-117">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="dc914-118">Korzystając z kreatora, definicje JSON do tych jednostek fabryki danych (połączone usługi, zestawy danych i potoki) są tworzone automatycznie dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="dc914-118">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="dc914-119">Korzystając z narzędzi/API (z wyjątkiem interfejs API .NET), należy zdefiniować tych jednostek fabryki danych w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="dc914-119">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="dc914-120">Aby uzyskać przykłady z definicji JSON dla jednostek fabryki danych, które są używane do kopiowania danych do/z magazynu tabel Azure, zobacz [przykłady JSON](#json-examples) sekcji tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="dc914-120">For samples with JSON definitions for Data Factory entities that are used to copy data to/from an Azure Table Storage, see [JSON examples](#json-examples) section of this article.</span></span> 

<span data-ttu-id="dc914-121">Poniższe sekcje zawierają szczegółowe informacje o właściwości JSON, które są używane do definiowania jednostek fabryki danych określonej do magazynu tabel platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="dc914-121">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Azure Table Storage:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="dc914-122">Połączona usługa właściwości</span><span class="sxs-lookup"><span data-stu-id="dc914-122">Linked service properties</span></span>
<span data-ttu-id="dc914-123">Istnieją dwa typy połączonych usług używanego do łączenia z magazynu obiektów blob platformy Azure do fabryki danych Azure.</span><span class="sxs-lookup"><span data-stu-id="dc914-123">There are two types of linked services you can use to link an Azure blob storage to an Azure data factory.</span></span> <span data-ttu-id="dc914-124">Są one: **AzureStorage** połączonej usługi i **element AzureStorageSas** połączonej usługi.</span><span class="sxs-lookup"><span data-stu-id="dc914-124">They are: **AzureStorage** linked service and **AzureStorageSas** linked service.</span></span> <span data-ttu-id="dc914-125">Połączoną usługą magazynu Azure zapewnia usłudze fabryka danych z globalnego dostępu do magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="dc914-125">The Azure Storage linked service provides the data factory with global access to the Azure Storage.</span></span> <span data-ttu-id="dc914-126">Związana SAS magazynu Azure (Shared Access Signature) usługa udostępnia fabryka danych z ograniczonej/czas-powiązane z dostępem do magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="dc914-126">Whereas, The Azure Storage SAS (Shared Access Signature) linked service provides the data factory with restricted/time-bound access to the Azure Storage.</span></span> <span data-ttu-id="dc914-127">Nie istnieją inne różnice między tych dwóch połączonych usług.</span><span class="sxs-lookup"><span data-stu-id="dc914-127">There are no other differences between these two linked services.</span></span> <span data-ttu-id="dc914-128">Wybierz połączonej usługi, która odpowiada Twoim potrzebom.</span><span class="sxs-lookup"><span data-stu-id="dc914-128">Choose the linked service that suits your needs.</span></span> <span data-ttu-id="dc914-129">Poniższe sekcje zawierają więcej szczegółowych informacji na temat tych dwóch usług połączonych.</span><span class="sxs-lookup"><span data-stu-id="dc914-129">The following sections provide more details on these two linked services.</span></span>

[!INCLUDE [data-factory-azure-storage-linked-services](../../includes/data-factory-azure-storage-linked-services.md)]

## <a name="dataset-properties"></a><span data-ttu-id="dc914-130">Właściwości zestawu danych</span><span class="sxs-lookup"><span data-stu-id="dc914-130">Dataset properties</span></span>
<span data-ttu-id="dc914-131">Aby uzyskać pełną listę sekcje & właściwości dostępne do definiowania zestawów danych, zobacz [Tworzenie zbiorów danych](data-factory-create-datasets.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="dc914-131">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="dc914-132">Sekcje zawierają informacje, takie jak struktury, dostępności i zasad zestawu danych JSON są podobne dla wszystkich typów obiektów dataset (Azure SQL, obiektów blob platformy Azure, Azure tabeli itp.).</span><span class="sxs-lookup"><span data-stu-id="dc914-132">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="dc914-133">Sekcja typeProperties jest różne dla każdego typu zestawu danych i zawiera informacje o lokalizacji danych w magazynie danych.</span><span class="sxs-lookup"><span data-stu-id="dc914-133">The typeProperties section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="dc914-134">**TypeProperties** sekcja dla zestawu danych typu **AzureTable** ma następujące właściwości.</span><span class="sxs-lookup"><span data-stu-id="dc914-134">The **typeProperties** section for the dataset of type **AzureTable** has the following properties.</span></span>

| <span data-ttu-id="dc914-135">Właściwość</span><span class="sxs-lookup"><span data-stu-id="dc914-135">Property</span></span> | <span data-ttu-id="dc914-136">Opis</span><span class="sxs-lookup"><span data-stu-id="dc914-136">Description</span></span> | <span data-ttu-id="dc914-137">Wymagane</span><span class="sxs-lookup"><span data-stu-id="dc914-137">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="dc914-138">tableName</span><span class="sxs-lookup"><span data-stu-id="dc914-138">tableName</span></span> |<span data-ttu-id="dc914-139">Nazwa tabeli w wystąpieniu bazy danych w tabeli platformy Azure, odnoszący się do połączonej usługi.</span><span class="sxs-lookup"><span data-stu-id="dc914-139">Name of the table in the Azure Table Database instance that linked service refers to.</span></span> |<span data-ttu-id="dc914-140">Tak.</span><span class="sxs-lookup"><span data-stu-id="dc914-140">Yes.</span></span> <span data-ttu-id="dc914-141">W przypadku tableName bez azureTableSourceQuery wszystkie rekordy z tabeli są kopiowane do lokalizacji docelowej.</span><span class="sxs-lookup"><span data-stu-id="dc914-141">When a tableName is specified without an azureTableSourceQuery, all records from the table are copied to the destination.</span></span> <span data-ttu-id="dc914-142">Jeśli określono również azureTableSourceQuery, rekordy z tabeli, która spełnia zapytania są kopiowane do lokalizacji docelowej.</span><span class="sxs-lookup"><span data-stu-id="dc914-142">If an azureTableSourceQuery is also specified, records from the table that satisfies the query are copied to the destination.</span></span> |

### <a name="schema-by-data-factory"></a><span data-ttu-id="dc914-143">Schemat fabryka danych</span><span class="sxs-lookup"><span data-stu-id="dc914-143">Schema by Data Factory</span></span>
<span data-ttu-id="dc914-144">Dla magazynów danych bez schematu, takie jak tabel Azure usługi fabryka danych z wnioskuje schemat w jednym z następujących sposobów:</span><span class="sxs-lookup"><span data-stu-id="dc914-144">For schema-free data stores such as Azure Table, the Data Factory service infers the schema in one of the following ways:</span></span>

1. <span data-ttu-id="dc914-145">Jeśli określisz struktury danych za pomocą **struktury** tej struktury Schema honoruje właściwości w definicji zestawu danych, usługi fabryka danych.</span><span class="sxs-lookup"><span data-stu-id="dc914-145">If you specify the structure of data by using the **structure** property in the dataset definition, the Data Factory service honors this structure as the schema.</span></span> <span data-ttu-id="dc914-146">W tym przypadku jeśli wiersza nie zawiera wartości dla kolumny, wartość null podano dla niego.</span><span class="sxs-lookup"><span data-stu-id="dc914-146">In this case, if a row does not contain a value for a column, a null value is provided for it.</span></span>
2. <span data-ttu-id="dc914-147">Jeśli nie określisz struktury danych za pomocą **struktury** właściwości w definicji zestawu danych, fabryki danych wnioskuje schemat za pomocą pierwszego wiersza w danych.</span><span class="sxs-lookup"><span data-stu-id="dc914-147">If you don't specify the structure of data by using the **structure** property in the dataset definition, Data Factory infers the schema by using the first row in the data.</span></span> <span data-ttu-id="dc914-148">W takim przypadku jeśli pierwszy wiersz zawiera pełną schematu, niektóre kolumny zostaną pominięte w wyniku operacji kopiowania.</span><span class="sxs-lookup"><span data-stu-id="dc914-148">In this case, if the first row does not contain the full schema, some columns are missed in the result of copy operation.</span></span>

<span data-ttu-id="dc914-149">W związku z tym dla źródeł danych bez schematu, najlepszym rozwiązaniem jest zdefiniowanie struktury danych przy użyciu **struktury** właściwości.</span><span class="sxs-lookup"><span data-stu-id="dc914-149">Therefore, for schema-free data sources, the best practice is to specify the structure of data using the **structure** property.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="dc914-150">Właściwości działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="dc914-150">Copy activity properties</span></span>
<span data-ttu-id="dc914-151">Pełną listę sekcje & właściwości dostępne do definiowania działań, zobacz [tworzenie potoków](data-factory-create-pipelines.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="dc914-151">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="dc914-152">Właściwości, takie jak nazwa, opis, dane wejściowe i wyjściowe zestawy danych i zasady są dostępne dla wszystkich typów działań.</span><span class="sxs-lookup"><span data-stu-id="dc914-152">Properties such as name, description, input and output datasets, and policies are available for all types of activities.</span></span>

<span data-ttu-id="dc914-153">Właściwości, które są dostępne w sekcji typeProperties działania z drugiej strony zależą od każdego typu działania.</span><span class="sxs-lookup"><span data-stu-id="dc914-153">Properties available in the typeProperties section of the activity on the other hand vary with each activity type.</span></span> <span data-ttu-id="dc914-154">Dla działania kopiowania różnią się w zależności od typów źródeł i sink.</span><span class="sxs-lookup"><span data-stu-id="dc914-154">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="dc914-155">**AzureTableSource** obsługuje następujące właściwości w sekcji typeProperties:</span><span class="sxs-lookup"><span data-stu-id="dc914-155">**AzureTableSource** supports the following properties in typeProperties section:</span></span>

| <span data-ttu-id="dc914-156">Właściwość</span><span class="sxs-lookup"><span data-stu-id="dc914-156">Property</span></span> | <span data-ttu-id="dc914-157">Opis</span><span class="sxs-lookup"><span data-stu-id="dc914-157">Description</span></span> | <span data-ttu-id="dc914-158">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="dc914-158">Allowed values</span></span> | <span data-ttu-id="dc914-159">Wymagane</span><span class="sxs-lookup"><span data-stu-id="dc914-159">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="dc914-160">azureTableSourceQuery</span><span class="sxs-lookup"><span data-stu-id="dc914-160">azureTableSourceQuery</span></span> |<span data-ttu-id="dc914-161">Użyj niestandardowych zapytania można odczytać danych.</span><span class="sxs-lookup"><span data-stu-id="dc914-161">Use the custom query to read data.</span></span> |<span data-ttu-id="dc914-162">Ciąg zapytania tabeli platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="dc914-162">Azure table query string.</span></span> <span data-ttu-id="dc914-163">Przykłady w następnej sekcji.</span><span class="sxs-lookup"><span data-stu-id="dc914-163">See examples in the next section.</span></span> |<span data-ttu-id="dc914-164">Nie.</span><span class="sxs-lookup"><span data-stu-id="dc914-164">No.</span></span> <span data-ttu-id="dc914-165">W przypadku tableName bez azureTableSourceQuery wszystkie rekordy z tabeli są kopiowane do lokalizacji docelowej.</span><span class="sxs-lookup"><span data-stu-id="dc914-165">When a tableName is specified without an azureTableSourceQuery, all records from the table are copied to the destination.</span></span> <span data-ttu-id="dc914-166">Jeśli określono również azureTableSourceQuery, rekordy z tabeli, która spełnia zapytania są kopiowane do lokalizacji docelowej.</span><span class="sxs-lookup"><span data-stu-id="dc914-166">If an azureTableSourceQuery is also specified, records from the table that satisfies the query are copied to the destination.</span></span> |
| <span data-ttu-id="dc914-167">azureTableSourceIgnoreTableNotFound</span><span class="sxs-lookup"><span data-stu-id="dc914-167">azureTableSourceIgnoreTableNotFound</span></span> |<span data-ttu-id="dc914-168">Wskazuje, czy swallow wyjątek tabela nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="dc914-168">Indicate whether swallow the exception of table not exist.</span></span> |<span data-ttu-id="dc914-169">WARTOŚĆ TRUE</span><span class="sxs-lookup"><span data-stu-id="dc914-169">TRUE</span></span><br/><span data-ttu-id="dc914-170">WARTOŚĆ FALSE</span><span class="sxs-lookup"><span data-stu-id="dc914-170">FALSE</span></span> |<span data-ttu-id="dc914-171">Nie</span><span class="sxs-lookup"><span data-stu-id="dc914-171">No</span></span> |

### <a name="azuretablesourcequery-examples"></a><span data-ttu-id="dc914-172">Przykłady azureTableSourceQuery</span><span class="sxs-lookup"><span data-stu-id="dc914-172">azureTableSourceQuery examples</span></span>
<span data-ttu-id="dc914-173">W przypadku tabel Azure kolumny typu string:</span><span class="sxs-lookup"><span data-stu-id="dc914-173">If Azure Table column is of string type:</span></span>

```JSON
azureTableSourceQuery": "$$Text.Format('PartitionKey ge \\'{0:yyyyMMddHH00_0000}\\' and PartitionKey le \\'{0:yyyyMMddHH00_9999}\\'', SliceStart)"
```

<span data-ttu-id="dc914-174">W przypadku tabel Azure kolumny typu Data/Godzina:</span><span class="sxs-lookup"><span data-stu-id="dc914-174">If Azure Table column is of datetime type:</span></span>

```JSON
"azureTableSourceQuery": "$$Text.Format('DeploymentEndTime gt datetime\\'{0:yyyy-MM-ddTHH:mm:ssZ}\\' and DeploymentEndTime le datetime\\'{1:yyyy-MM-ddTHH:mm:ssZ}\\'', SliceStart, SliceEnd)"
```

<span data-ttu-id="dc914-175">**AzureTableSink** obsługuje następujące właściwości w sekcji typeProperties:</span><span class="sxs-lookup"><span data-stu-id="dc914-175">**AzureTableSink** supports the following properties in typeProperties section:</span></span>

| <span data-ttu-id="dc914-176">Właściwość</span><span class="sxs-lookup"><span data-stu-id="dc914-176">Property</span></span> | <span data-ttu-id="dc914-177">Opis</span><span class="sxs-lookup"><span data-stu-id="dc914-177">Description</span></span> | <span data-ttu-id="dc914-178">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="dc914-178">Allowed values</span></span> | <span data-ttu-id="dc914-179">Wymagane</span><span class="sxs-lookup"><span data-stu-id="dc914-179">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="dc914-180">azureTableDefaultPartitionKeyValue</span><span class="sxs-lookup"><span data-stu-id="dc914-180">azureTableDefaultPartitionKeyValue</span></span> |<span data-ttu-id="dc914-181">Domyślna wartość klucza partycji, które mogą być używane przez obiekt sink.</span><span class="sxs-lookup"><span data-stu-id="dc914-181">Default partition key value that can be used by the sink.</span></span> |<span data-ttu-id="dc914-182">Wartość ciągu.</span><span class="sxs-lookup"><span data-stu-id="dc914-182">A string value.</span></span> |<span data-ttu-id="dc914-183">Nie</span><span class="sxs-lookup"><span data-stu-id="dc914-183">No</span></span> |
| <span data-ttu-id="dc914-184">azureTablePartitionKeyName</span><span class="sxs-lookup"><span data-stu-id="dc914-184">azureTablePartitionKeyName</span></span> |<span data-ttu-id="dc914-185">Określ nazwę kolumny, których wartości są używane jako klucze partycji.</span><span class="sxs-lookup"><span data-stu-id="dc914-185">Specify name of the column whose values are used as partition keys.</span></span> <span data-ttu-id="dc914-186">Jeśli nie zostanie określony, AzureTableDefaultPartitionKeyValue jest używana jako klucza partycji.</span><span class="sxs-lookup"><span data-stu-id="dc914-186">If not specified, AzureTableDefaultPartitionKeyValue is used as the partition key.</span></span> |<span data-ttu-id="dc914-187">Nazwa kolumny.</span><span class="sxs-lookup"><span data-stu-id="dc914-187">A column name.</span></span> |<span data-ttu-id="dc914-188">Nie</span><span class="sxs-lookup"><span data-stu-id="dc914-188">No</span></span> |
| <span data-ttu-id="dc914-189">azureTableRowKeyName</span><span class="sxs-lookup"><span data-stu-id="dc914-189">azureTableRowKeyName</span></span> |<span data-ttu-id="dc914-190">Określ nazwę kolumny, których wartości kolumn używanych jako klucz wiersza.</span><span class="sxs-lookup"><span data-stu-id="dc914-190">Specify name of the column whose column values are used as row key.</span></span> <span data-ttu-id="dc914-191">Jeśli nie zostanie określony, użyj identyfikatora GUID dla każdego wiersza.</span><span class="sxs-lookup"><span data-stu-id="dc914-191">If not specified, use a GUID for each row.</span></span> |<span data-ttu-id="dc914-192">Nazwa kolumny.</span><span class="sxs-lookup"><span data-stu-id="dc914-192">A column name.</span></span> |<span data-ttu-id="dc914-193">Nie</span><span class="sxs-lookup"><span data-stu-id="dc914-193">No</span></span> |
| <span data-ttu-id="dc914-194">azureTableInsertType</span><span class="sxs-lookup"><span data-stu-id="dc914-194">azureTableInsertType</span></span> |<span data-ttu-id="dc914-195">Tryb do wstawiania danych do tabeli platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="dc914-195">The mode to insert data into Azure table.</span></span><br/><br/><span data-ttu-id="dc914-196">Ta właściwość określa, czy wartości zastąpienia lub scalić zostać istniejących wierszy w tabeli wyników ze zgodnymi kluczami partycji i wiersza.</span><span class="sxs-lookup"><span data-stu-id="dc914-196">This property controls whether existing rows in the output table with matching partition and row keys have their values replaced or merged.</span></span> <br/><br/><span data-ttu-id="dc914-197">Aby dowiedzieć się więcej na temat działania tych ustawień (scalania i Zastąp), zobacz [wstawienia lub scalania jednostki](https://msdn.microsoft.com/library/azure/hh452241.aspx) i [wstawienia lub Zastąp jednostki](https://msdn.microsoft.com/library/azure/hh452242.aspx) tematów.</span><span class="sxs-lookup"><span data-stu-id="dc914-197">To learn about how these settings (merge and replace) work, see [Insert or Merge Entity](https://msdn.microsoft.com/library/azure/hh452241.aspx) and [Insert or Replace Entity](https://msdn.microsoft.com/library/azure/hh452242.aspx) topics.</span></span> <br/><br> <span data-ttu-id="dc914-198">To ustawienie jest stosowane na poziomie wiersza, a nie na poziomie tabeli, a żadna z tych opcji usuwa wiersze w tabeli danych wyjściowych, które nie istnieją w danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="dc914-198">This setting applies at the row level, not the table level, and neither option deletes rows in the output table that do not exist in the input.</span></span> |<span data-ttu-id="dc914-199">Merge (ustawienie domyślne)</span><span class="sxs-lookup"><span data-stu-id="dc914-199">merge (default)</span></span><br/><span data-ttu-id="dc914-200">Zamień</span><span class="sxs-lookup"><span data-stu-id="dc914-200">replace</span></span> |<span data-ttu-id="dc914-201">Nie</span><span class="sxs-lookup"><span data-stu-id="dc914-201">No</span></span> |
| <span data-ttu-id="dc914-202">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="dc914-202">writeBatchSize</span></span> |<span data-ttu-id="dc914-203">Wstawia dane do tabeli platformy Azure, gdy zostaje trafiony writeBatchSize lub writeBatchTimeout.</span><span class="sxs-lookup"><span data-stu-id="dc914-203">Inserts data into the Azure table when the writeBatchSize or writeBatchTimeout is hit.</span></span> |<span data-ttu-id="dc914-204">Liczba całkowita (liczba wierszy)</span><span class="sxs-lookup"><span data-stu-id="dc914-204">Integer (number of rows)</span></span> |<span data-ttu-id="dc914-205">Nie (domyślne: 10000)</span><span class="sxs-lookup"><span data-stu-id="dc914-205">No (default: 10000)</span></span> |
| <span data-ttu-id="dc914-206">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="dc914-206">writeBatchTimeout</span></span> |<span data-ttu-id="dc914-207">Wstawia dane do tabeli platformy Azure, gdy zostaje trafiony writeBatchSize lub writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="dc914-207">Inserts data into the Azure table when the writeBatchSize or writeBatchTimeout is hit</span></span> |<span data-ttu-id="dc914-208">Zakres czasu</span><span class="sxs-lookup"><span data-stu-id="dc914-208">timespan</span></span><br/><br/><span data-ttu-id="dc914-209">Przykład: "00:20:00" (20 minut)</span><span class="sxs-lookup"><span data-stu-id="dc914-209">Example: “00:20:00” (20 minutes)</span></span> |<span data-ttu-id="dc914-210">Nie (domyślnie magazynu klienta domyślny limit czasu wartość 90 s)</span><span class="sxs-lookup"><span data-stu-id="dc914-210">No (Default to storage client default timeout value 90 sec)</span></span> |

### <a name="azuretablepartitionkeyname"></a><span data-ttu-id="dc914-211">azureTablePartitionKeyName</span><span class="sxs-lookup"><span data-stu-id="dc914-211">azureTablePartitionKeyName</span></span>
<span data-ttu-id="dc914-212">Mapowanie kolumny źródłowej do przy użyciu translatora właściwości JSON, zanim użyjesz kolumna docelowa jako azureTablePartitionKeyName kolumna docelowa.</span><span class="sxs-lookup"><span data-stu-id="dc914-212">Map a source column to a destination column using the translator JSON property before you can use the destination column as the azureTablePartitionKeyName.</span></span>

<span data-ttu-id="dc914-213">W poniższym przykładzie kolumna źródłowa DivisionID jest zamapowany na kolumny docelowej: DivisionID.</span><span class="sxs-lookup"><span data-stu-id="dc914-213">In the following example, source column DivisionID is mapped to the destination column: DivisionID.</span></span>  

```JSON
"translator": {
    "type": "TabularTranslator",
    "columnMappings": "DivisionID: DivisionID, FirstName: FirstName, LastName: LastName"
}
```
<span data-ttu-id="dc914-214">DivisionID jest określony jako klucza partycji.</span><span class="sxs-lookup"><span data-stu-id="dc914-214">The DivisionID is specified as the partition key.</span></span>

```JSON
"sink": {
    "type": "AzureTableSink",
    "azureTablePartitionKeyName": "DivisionID",
    "writeBatchSize": 100,
    "writeBatchTimeout": "01:00:00"
}
```
## <a name="json-examples"></a><span data-ttu-id="dc914-215">Przykłady JSON</span><span class="sxs-lookup"><span data-stu-id="dc914-215">JSON examples</span></span>
<span data-ttu-id="dc914-216">Poniższe przykłady zapewniają definicje JSON, których można utworzyć potok przy użyciu [portalu Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) lub [programu Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) lub [programu Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="dc914-216">The following examples provide sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="dc914-217">Przedstawiają sposób kopiowania danych do i z magazynu tabel platformy Azure i bazy danych obiektów Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="dc914-217">They show how to copy data to and from Azure Table Storage and Azure Blob Database.</span></span> <span data-ttu-id="dc914-218">Jednak dane mogą być kopiowane **bezpośrednio** z dowolnego źródła do żadnego z obsługiwanych sink.</span><span class="sxs-lookup"><span data-stu-id="dc914-218">However, data can be copied **directly** from any of the sources to any of the supported sinks.</span></span> <span data-ttu-id="dc914-219">Aby uzyskać więcej informacji, zobacz sekcję "obsługiwane magazyny danych i formaty" w [przenoszenia danych za pomocą działania kopiowania](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="dc914-219">For more information, see the section "Supported data stores and formats" in [Move data by using Copy Activity](data-factory-data-movement-activities.md).</span></span>

## <a name="example-copy-data-from-azure-table-to-azure-blob"></a><span data-ttu-id="dc914-220">Przykład: Kopiowanie danych z tabel Azure do obiektów Blob platformy Azure</span><span class="sxs-lookup"><span data-stu-id="dc914-220">Example: Copy data from Azure Table to Azure Blob</span></span>
<span data-ttu-id="dc914-221">Poniższy przykład przedstawia:</span><span class="sxs-lookup"><span data-stu-id="dc914-221">The following sample shows:</span></span>

1. <span data-ttu-id="dc914-222">Połączonej usługi typu [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) (używane dla obiekt blob & tabeli).</span><span class="sxs-lookup"><span data-stu-id="dc914-222">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) (used for both table & blob).</span></span>
2. <span data-ttu-id="dc914-223">Dane wejściowe [dataset](data-factory-create-datasets.md) typu [AzureTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="dc914-223">An input [dataset](data-factory-create-datasets.md) of type [AzureTable](#dataset-properties).</span></span>
3. <span data-ttu-id="dc914-224">Dane wyjściowe [dataset](data-factory-create-datasets.md) typu [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="dc914-224">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="dc914-225">[Potoku](data-factory-create-pipelines.md) z działaniem kopii, która używa [AzureTableSource](#activity-properties) i [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="dc914-225">The [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [AzureTableSource](#activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="dc914-226">Przykład kopiuje dane należące do domyślnej partycji w tabeli obiektu blob Azure co godzinę.</span><span class="sxs-lookup"><span data-stu-id="dc914-226">The sample copies data belonging to the default partition in an Azure Table to a blob every hour.</span></span> <span data-ttu-id="dc914-227">Właściwości JSON używane w te przykłady są opisane w sekcjach poniżej próbek.</span><span class="sxs-lookup"><span data-stu-id="dc914-227">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="dc914-228">**Połączonej usługi magazynu Azure:**</span><span class="sxs-lookup"><span data-stu-id="dc914-228">**Azure storage linked service:**</span></span>

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
<span data-ttu-id="dc914-229">Fabryka danych Azure obsługuje dwa typy usług magazynu Azure połączony: **AzureStorage** i **element AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="dc914-229">Azure Data Factory supports two types of Azure Storage linked services: **AzureStorage** and **AzureStorageSas**.</span></span> <span data-ttu-id="dc914-230">Dla pierwszego z nich Określ ciąg połączenia, który zawiera klucz konta i dla późniejszą, określ identyfikator Uri dostępu sygnatury dostępu Współdzielonego.</span><span class="sxs-lookup"><span data-stu-id="dc914-230">For the first one, you specify the connection string that includes the account key and for the later one, you specify the Shared Access Signature (SAS) Uri.</span></span> <span data-ttu-id="dc914-231">Zobacz [połączonych usług](#linked-service-properties) sekcji, aby uzyskać szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="dc914-231">See [Linked Services](#linked-service-properties) section for details.</span></span>  

<span data-ttu-id="dc914-232">**Azure tabeli wejściowy zestaw danych:**</span><span class="sxs-lookup"><span data-stu-id="dc914-232">**Azure Table input dataset:**</span></span>

<span data-ttu-id="dc914-233">Przykładzie przyjęto założenie, że utworzono tabelę "MyTable" w tabeli platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="dc914-233">The sample assumes you have created a table “MyTable” in Azure Table.</span></span>

<span data-ttu-id="dc914-234">Ustawienie "external": "prawda" informuje usługi fabryka danych czy zestaw danych jest zewnętrzne do fabryki danych i nie jest generowany przez działanie w fabryce danych.</span><span class="sxs-lookup"><span data-stu-id="dc914-234">Setting “external”: ”true” informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

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

<span data-ttu-id="dc914-235">**Azure Blob wyjściowy zestaw danych:**</span><span class="sxs-lookup"><span data-stu-id="dc914-235">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="dc914-236">Dane są zapisywane do nowego obiektu blob co godzinę (częstotliwość: godziny, interwał: 1).</span><span class="sxs-lookup"><span data-stu-id="dc914-236">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="dc914-237">Ścieżka folderu dla obiekt blob jest dynamicznie obliczane na podstawie czasu rozpoczęcia wycinek, który jest przetwarzana.</span><span class="sxs-lookup"><span data-stu-id="dc914-237">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="dc914-238">Ścieżka folderu używa rok, miesiąc, dzień i godziny części czas rozpoczęcia.</span><span class="sxs-lookup"><span data-stu-id="dc914-238">The folder path uses year, month, day, and hours parts of the start time.</span></span>

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

<span data-ttu-id="dc914-239">**Działanie kopiowania w potoku z AzureTableSource i BlobSink:**</span><span class="sxs-lookup"><span data-stu-id="dc914-239">**Copy activity in a pipeline with AzureTableSource and BlobSink:**</span></span>

<span data-ttu-id="dc914-240">Potok zawiera działanie kopiowania, który jest skonfigurowany do używania wejściowe i wyjściowe zestawy danych i jest zaplanowane co godzinę.</span><span class="sxs-lookup"><span data-stu-id="dc914-240">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="dc914-241">W definicji JSON potoku **źródła** ustawiono typ **AzureTableSource** i **zbiornika** ustawiono typ **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="dc914-241">In the pipeline JSON definition, the **source** type is set to **AzureTableSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="dc914-242">Zapytanie SQL określony za pomocą **AzureTableSourceQuery** właściwości wybiera danych z partycji domyślnej co godzinę do skopiowania.</span><span class="sxs-lookup"><span data-stu-id="dc914-242">The SQL query specified with **AzureTableSourceQuery** property selects the data from the default partition every hour to copy.</span></span>

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

## <a name="example-copy-data-from-azure-blob-to-azure-table"></a><span data-ttu-id="dc914-243">Przykład: Kopiowanie danych z obiektu Blob Azure do tabeli platformy Azure</span><span class="sxs-lookup"><span data-stu-id="dc914-243">Example: Copy data from Azure Blob to Azure Table</span></span>
<span data-ttu-id="dc914-244">Poniższy przykład przedstawia:</span><span class="sxs-lookup"><span data-stu-id="dc914-244">The following sample shows:</span></span>

1. <span data-ttu-id="dc914-245">Połączonej usługi typu [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) (używane dla obiekt blob & tabeli)</span><span class="sxs-lookup"><span data-stu-id="dc914-245">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) (used for both table & blob)</span></span>
2. <span data-ttu-id="dc914-246">Dane wejściowe [dataset](data-factory-create-datasets.md) typu [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="dc914-246">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
3. <span data-ttu-id="dc914-247">Dane wyjściowe [dataset](data-factory-create-datasets.md) typu [AzureTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="dc914-247">An output [dataset](data-factory-create-datasets.md) of type [AzureTable](#dataset-properties).</span></span>
4. <span data-ttu-id="dc914-248">[Potoku](data-factory-create-pipelines.md) z działaniem kopii, która używa [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) i [AzureTableSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="dc914-248">The [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [AzureTableSink](#copy-activity-properties).</span></span>

<span data-ttu-id="dc914-249">Kopie próbki szeregów czasowych dane z usługi Azure blob Azure tabeli co godzinę.</span><span class="sxs-lookup"><span data-stu-id="dc914-249">The sample copies time-series data from an Azure blob to an Azure table hourly.</span></span> <span data-ttu-id="dc914-250">Właściwości JSON używane w te przykłady są opisane w sekcjach poniżej próbek.</span><span class="sxs-lookup"><span data-stu-id="dc914-250">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="dc914-251">**Usługa Azure storage (dla tabeli platformy Azure i obiektów Blob) połączonej usługi:**</span><span class="sxs-lookup"><span data-stu-id="dc914-251">**Azure storage (for both Azure Table & Blob) linked service:**</span></span>

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

<span data-ttu-id="dc914-252">Fabryka danych Azure obsługuje dwa typy usług magazynu Azure połączony: **AzureStorage** i **element AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="dc914-252">Azure Data Factory supports two types of Azure Storage linked services: **AzureStorage** and **AzureStorageSas**.</span></span> <span data-ttu-id="dc914-253">Dla pierwszego z nich Określ ciąg połączenia, który zawiera klucz konta i dla późniejszą, określ identyfikator Uri dostępu sygnatury dostępu Współdzielonego.</span><span class="sxs-lookup"><span data-stu-id="dc914-253">For the first one, you specify the connection string that includes the account key and for the later one, you specify the Shared Access Signature (SAS) Uri.</span></span> <span data-ttu-id="dc914-254">Zobacz [połączonych usług](#linked-service-properties) sekcji, aby uzyskać szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="dc914-254">See [Linked Services](#linked-service-properties) section for details.</span></span>

<span data-ttu-id="dc914-255">**Azure wejściowego zestawu danych obiektów Blob:**</span><span class="sxs-lookup"><span data-stu-id="dc914-255">**Azure Blob input dataset:**</span></span>

<span data-ttu-id="dc914-256">Dane są pobierane z nowego obiektu blob co godzinę (częstotliwość: godziny, interwał: 1).</span><span class="sxs-lookup"><span data-stu-id="dc914-256">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="dc914-257">Nazwa i ścieżka pliku folder dla obiektu blob dynamicznie są oceniane na podstawie czasu rozpoczęcia wycinek, który jest przetwarzana.</span><span class="sxs-lookup"><span data-stu-id="dc914-257">The folder path and file name for the blob are dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="dc914-258">Ścieżka folderu korzysta rok, miesiąc i dzień część czas rozpoczęcia, a nazwa pliku godzina część czas rozpoczęcia.</span><span class="sxs-lookup"><span data-stu-id="dc914-258">The folder path uses year, month, and day part of the start time and file name uses the hour part of the start time.</span></span> <span data-ttu-id="dc914-259">"external": ustawienie "prawda" usługi fabryka danych informuje, czy zestaw danych jest zewnętrzne do fabryki danych i nie jest generowany przez działanie w fabryce danych.</span><span class="sxs-lookup"><span data-stu-id="dc914-259">“external”: “true” setting informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

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

<span data-ttu-id="dc914-260">**Tabeli platformy Azure wyjściowy zestaw danych:**</span><span class="sxs-lookup"><span data-stu-id="dc914-260">**Azure Table output dataset:**</span></span>

<span data-ttu-id="dc914-261">Przykład kopiuje dane do tabeli o nazwie "MyTable" w tabeli platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="dc914-261">The sample copies data to a table named “MyTable” in Azure Table.</span></span> <span data-ttu-id="dc914-262">Tworzenie tabeli platformy Azure z taką samą liczbę kolumn, zgodnie z oczekiwaniami pliku Blob CSV zawiera.</span><span class="sxs-lookup"><span data-stu-id="dc914-262">Create an Azure table with the same number of columns as you expect the Blob CSV file to contain.</span></span> <span data-ttu-id="dc914-263">Nowe wiersze są dodawane do tabeli co godzinę.</span><span class="sxs-lookup"><span data-stu-id="dc914-263">New rows are added to the table every hour.</span></span>

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

<span data-ttu-id="dc914-264">**Działanie kopiowania w potoku z BlobSource i AzureTableSink:**</span><span class="sxs-lookup"><span data-stu-id="dc914-264">**Copy activity in a pipeline with BlobSource and AzureTableSink:**</span></span>

<span data-ttu-id="dc914-265">Potok zawiera działanie kopiowania, który jest skonfigurowany do używania wejściowe i wyjściowe zestawy danych i jest zaplanowane co godzinę.</span><span class="sxs-lookup"><span data-stu-id="dc914-265">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="dc914-266">W definicji JSON potoku **źródła** ustawiono typ **BlobSource** i **zbiornika** ustawiono typ **AzureTableSink**.</span><span class="sxs-lookup"><span data-stu-id="dc914-266">In the pipeline JSON definition, the **source** type is set to **BlobSource** and **sink** type is set to **AzureTableSink**.</span></span>

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
## <a name="type-mapping-for-azure-table"></a><span data-ttu-id="dc914-267">Mapowanie typu dla tabeli platformy Azure</span><span class="sxs-lookup"><span data-stu-id="dc914-267">Type Mapping for Azure Table</span></span>
<span data-ttu-id="dc914-268">Jak wspomniano w [działań przepływu danych](data-factory-data-movement-activities.md) artykułu, automatyczne konwersje z typów źródła do zbiornika typy z następujących rozwinięcie wykonuje działanie kopiowania.</span><span class="sxs-lookup"><span data-stu-id="dc914-268">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following two-step approach.</span></span>

1. <span data-ttu-id="dc914-269">Konwertowanie typów natywnych źródła na typ architektury .NET</span><span class="sxs-lookup"><span data-stu-id="dc914-269">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="dc914-270">Konwertowanie na typ macierzysty ujścia typ architektury .NET</span><span class="sxs-lookup"><span data-stu-id="dc914-270">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="dc914-271">Podczas przenoszenia danych do i z tabel Azure, następujące [mapowania zdefiniowane przez usługę Azure tabeli](https://msdn.microsoft.com/library/azure/dd179338.aspx) są używane z typów OData tabeli platformy Azure na typ architektury .NET i na odwrót.</span><span class="sxs-lookup"><span data-stu-id="dc914-271">When moving data to & from Azure Table, the following [mappings defined by Azure Table service](https://msdn.microsoft.com/library/azure/dd179338.aspx) are used from Azure Table OData types to .NET type and vice versa.</span></span>

| <span data-ttu-id="dc914-272">Typ danych OData</span><span class="sxs-lookup"><span data-stu-id="dc914-272">OData Data Type</span></span> | <span data-ttu-id="dc914-273">Typ architektury .NET</span><span class="sxs-lookup"><span data-stu-id="dc914-273">.NET Type</span></span> | <span data-ttu-id="dc914-274">Szczegóły</span><span class="sxs-lookup"><span data-stu-id="dc914-274">Details</span></span> |
| --- | --- | --- |
| <span data-ttu-id="dc914-275">Edm.Binary</span><span class="sxs-lookup"><span data-stu-id="dc914-275">Edm.Binary</span></span> |<span data-ttu-id="dc914-276">Byte]</span><span class="sxs-lookup"><span data-stu-id="dc914-276">byte[]</span></span> |<span data-ttu-id="dc914-277">Tablica bajtów do 64 KB.</span><span class="sxs-lookup"><span data-stu-id="dc914-277">An array of bytes up to 64 KB.</span></span> |
| <span data-ttu-id="dc914-278">Edm.Boolean</span><span class="sxs-lookup"><span data-stu-id="dc914-278">Edm.Boolean</span></span> |<span data-ttu-id="dc914-279">wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="dc914-279">bool</span></span> |<span data-ttu-id="dc914-280">Wartość logiczna.</span><span class="sxs-lookup"><span data-stu-id="dc914-280">A Boolean value.</span></span> |
| <span data-ttu-id="dc914-281">Edm.DateTime</span><span class="sxs-lookup"><span data-stu-id="dc914-281">Edm.DateTime</span></span> |<span data-ttu-id="dc914-282">Data i godzina</span><span class="sxs-lookup"><span data-stu-id="dc914-282">DateTime</span></span> |<span data-ttu-id="dc914-283">Wartość 64-bitowa, wyrażone jako uniwersalny czas koordynowany (UTC).</span><span class="sxs-lookup"><span data-stu-id="dc914-283">A 64-bit value expressed as Coordinated Universal Time (UTC).</span></span> <span data-ttu-id="dc914-284">Obsługiwanym zakresem DateTime zaczyna się od 12:00, a 1 stycznia, 1601 r. N.E.</span><span class="sxs-lookup"><span data-stu-id="dc914-284">The supported DateTime range begins from 12:00 midnight, January 1, 1601 A.D.</span></span> <span data-ttu-id="dc914-285">(R), CZAS UTC.</span><span class="sxs-lookup"><span data-stu-id="dc914-285">(C.E.), UTC.</span></span> <span data-ttu-id="dc914-286">Zakres kończy się po 31 grudnia 9999 r.</span><span class="sxs-lookup"><span data-stu-id="dc914-286">The range ends at December 31, 9999.</span></span> |
| <span data-ttu-id="dc914-287">Edm.Double</span><span class="sxs-lookup"><span data-stu-id="dc914-287">Edm.Double</span></span> |<span data-ttu-id="dc914-288">O podwójnej precyzji</span><span class="sxs-lookup"><span data-stu-id="dc914-288">double</span></span> |<span data-ttu-id="dc914-289">64-bitowej zmiennej punktu wartości.</span><span class="sxs-lookup"><span data-stu-id="dc914-289">A 64-bit floating point value.</span></span> |
| <span data-ttu-id="dc914-290">Edm.Guid</span><span class="sxs-lookup"><span data-stu-id="dc914-290">Edm.Guid</span></span> |<span data-ttu-id="dc914-291">Identyfikator GUID</span><span class="sxs-lookup"><span data-stu-id="dc914-291">Guid</span></span> |<span data-ttu-id="dc914-292">Globalnie unikatowy identyfikator 128-bitowego.</span><span class="sxs-lookup"><span data-stu-id="dc914-292">A 128-bit globally unique identifier.</span></span> |
| <span data-ttu-id="dc914-293">Edm.Int32</span><span class="sxs-lookup"><span data-stu-id="dc914-293">Edm.Int32</span></span> |<span data-ttu-id="dc914-294">Int32</span><span class="sxs-lookup"><span data-stu-id="dc914-294">Int32</span></span> |<span data-ttu-id="dc914-295">32-bitową liczbę całkowitą.</span><span class="sxs-lookup"><span data-stu-id="dc914-295">A 32-bit integer.</span></span> |
| <span data-ttu-id="dc914-296">Edm.Int64</span><span class="sxs-lookup"><span data-stu-id="dc914-296">Edm.Int64</span></span> |<span data-ttu-id="dc914-297">Int64</span><span class="sxs-lookup"><span data-stu-id="dc914-297">Int64</span></span> |<span data-ttu-id="dc914-298">64-bitową liczbę całkowitą.</span><span class="sxs-lookup"><span data-stu-id="dc914-298">A 64-bit integer.</span></span> |
| <span data-ttu-id="dc914-299">Edm.String</span><span class="sxs-lookup"><span data-stu-id="dc914-299">Edm.String</span></span> |<span data-ttu-id="dc914-300">Ciąg</span><span class="sxs-lookup"><span data-stu-id="dc914-300">String</span></span> |<span data-ttu-id="dc914-301">Wartość algorytmem UTF-16.</span><span class="sxs-lookup"><span data-stu-id="dc914-301">A UTF-16-encoded value.</span></span> <span data-ttu-id="dc914-302">Ciągi może być maksymalnie 64 KB.</span><span class="sxs-lookup"><span data-stu-id="dc914-302">String values may be up to 64 KB.</span></span> |

### <a name="type-conversion-sample"></a><span data-ttu-id="dc914-303">Przykładowe konwersji typu</span><span class="sxs-lookup"><span data-stu-id="dc914-303">Type Conversion Sample</span></span>
<span data-ttu-id="dc914-304">Poniższy przykład jest kopiowania danych z obiektu Blob Azure do tabeli platformy Azure z konwersji typu.</span><span class="sxs-lookup"><span data-stu-id="dc914-304">The following sample is for copying data from an Azure Blob to Azure Table with type conversions.</span></span>

<span data-ttu-id="dc914-305">Załóżmy, że zestawu danych obiektów Blob jest w formacie CSV zawiera trzy kolumny.</span><span class="sxs-lookup"><span data-stu-id="dc914-305">Suppose the Blob dataset is in CSV format and contains three columns.</span></span> <span data-ttu-id="dc914-306">Jeden z nich jest kolumną daty/godziny w formacie datetime niestandardowych za pomocą nazwy skróconej francuskim dzień tygodnia.</span><span class="sxs-lookup"><span data-stu-id="dc914-306">One of them is a datetime column with a custom datetime format using abbreviated French names for day of the week.</span></span>

<span data-ttu-id="dc914-307">Definiowanie zestawu danych obiektów Blob, źródłowy następujący wraz z definicji typu dla kolumny.</span><span class="sxs-lookup"><span data-stu-id="dc914-307">Define the Blob Source dataset as follows along with type definitions for the columns.</span></span>

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
<span data-ttu-id="dc914-308">Podana mapowania typu z typu Azure tabeli OData do typów .NET, czy zdefiniować tabeli w tabeli platformy Azure z następującego schematu.</span><span class="sxs-lookup"><span data-stu-id="dc914-308">Given the type mapping from Azure Table OData type to .NET type, you would define the table in Azure Table with the following schema.</span></span>

<span data-ttu-id="dc914-309">**Schemat tabeli platformy Azure:**</span><span class="sxs-lookup"><span data-stu-id="dc914-309">**Azure Table schema:**</span></span>

| <span data-ttu-id="dc914-310">Nazwa kolumny</span><span class="sxs-lookup"><span data-stu-id="dc914-310">Column name</span></span> | <span data-ttu-id="dc914-311">Typ</span><span class="sxs-lookup"><span data-stu-id="dc914-311">Type</span></span> |
| --- | --- |
| <span data-ttu-id="dc914-312">Nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="dc914-312">userid</span></span> |<span data-ttu-id="dc914-313">Edm.Int64</span><span class="sxs-lookup"><span data-stu-id="dc914-313">Edm.Int64</span></span> |
| <span data-ttu-id="dc914-314">name</span><span class="sxs-lookup"><span data-stu-id="dc914-314">name</span></span> |<span data-ttu-id="dc914-315">Edm.String</span><span class="sxs-lookup"><span data-stu-id="dc914-315">Edm.String</span></span> |
| <span data-ttu-id="dc914-316">lastlogindate</span><span class="sxs-lookup"><span data-stu-id="dc914-316">lastlogindate</span></span> |<span data-ttu-id="dc914-317">Edm.DateTime</span><span class="sxs-lookup"><span data-stu-id="dc914-317">Edm.DateTime</span></span> |

<span data-ttu-id="dc914-318">Następnie określ następujący zestaw danych tabel Azure.</span><span class="sxs-lookup"><span data-stu-id="dc914-318">Next, define the Azure Table dataset as follows.</span></span> <span data-ttu-id="dc914-319">Nie trzeba określić "structure" sekcji informacji o typach, ponieważ informacje o typie został już określony w odpowiedni magazyn danych.</span><span class="sxs-lookup"><span data-stu-id="dc914-319">You do not need to specify “structure” section with the type information since the type information is already specified in the underlying data store.</span></span>

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

<span data-ttu-id="dc914-320">W takim przypadku fabryka danych automatycznie konwersje typów w tym polu daty/godziny w formacie datetime niestandardowych przy użyciu kultury "fr-fr" podczas przenoszenia danych z obiektu Blob do tabel Azure.</span><span class="sxs-lookup"><span data-stu-id="dc914-320">In this case, Data Factory automatically does type conversions including the Datetime field with the custom datetime format using the "fr-fr" culture when moving data from Blob to Azure Table.</span></span>

> [!NOTE]
> <span data-ttu-id="dc914-321">Aby mapować kolumn z zestawu źródła danych do kolumn z obiektu sink zestawu danych, zobacz [mapowania kolumnach dataset w fabryce danych Azure](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="dc914-321">To map columns from source dataset to columns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="dc914-322">Wydajność i dostrajania</span><span class="sxs-lookup"><span data-stu-id="dc914-322">Performance and Tuning</span></span>
<span data-ttu-id="dc914-323">Informacje na temat kluczowych czynników tego wydajność wpływ przenoszenia danych (działanie kopiowania) w usłudze fabryka danych Azure i zoptymalizować ją na różne sposoby, zobacz [wydajności działania kopiowania & dostrajanie przewodnik](data-factory-copy-activity-performance.md).</span><span class="sxs-lookup"><span data-stu-id="dc914-323">To learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it, see [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md).</span></span>
