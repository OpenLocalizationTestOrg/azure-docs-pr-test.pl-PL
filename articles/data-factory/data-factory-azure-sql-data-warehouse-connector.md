---
title: "Kopiowanie danych do/z usługi Azure SQL Data Warehouse | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak skopiować dane z usługi Azure SQL Data Warehouse przy użyciu fabryki danych Azure"
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
ms.openlocfilehash: 8cba89e0947646b498af07aa484511bf07bf7b0e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="copy-data-to-and-from-azure-sql-data-warehouse-using-azure-data-factory"></a><span data-ttu-id="594a1-103">Kopiowanie danych do i z usługi Azure SQL Data Warehouse przy użyciu fabryki danych Azure</span><span class="sxs-lookup"><span data-stu-id="594a1-103">Copy data to and from Azure SQL Data Warehouse using Azure Data Factory</span></span>
<span data-ttu-id="594a1-104">W tym artykule opisano sposób korzystania działanie kopiowania w fabryce danych Azure, aby przenieść dane z usługi Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="594a1-104">This article explains how to use the Copy Activity in Azure Data Factory to move data to/from Azure SQL Data Warehouse.</span></span> <span data-ttu-id="594a1-105">Opiera się na [działań przepływu danych](data-factory-data-movement-activities.md) artykułu, który przedstawia ogólny przegląd przenoszenia danych z działania kopiowania.</span><span class="sxs-lookup"><span data-stu-id="594a1-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>  

> [!TIP]
> <span data-ttu-id="594a1-106">Aby uzyskać najlepszą wydajność, użyj programu PolyBase, aby załadować dane do usługi Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="594a1-106">To achieve best performance, use PolyBase to load data into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="594a1-107">[Użyj programu PolyBase, aby załadować dane do usługi Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#use-polybase-to-load-data-into-azure-sql-data-warehouse) sekcja zawiera szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="594a1-107">The [Use PolyBase to load data into Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#use-polybase-to-load-data-into-azure-sql-data-warehouse) section has details.</span></span> <span data-ttu-id="594a1-108">Aby uzyskać wskazówki z przypadkiem użycia, zobacz [załadować 1 TB do usługi Azure SQL Data Warehouse z fabryką danych Azure w obszarze 15 minut](data-factory-load-sql-data-warehouse.md).</span><span class="sxs-lookup"><span data-stu-id="594a1-108">For a walkthrough with a use case, see [Load 1 TB into Azure SQL Data Warehouse under 15 minutes with Azure Data Factory](data-factory-load-sql-data-warehouse.md).</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="594a1-109">Obsługiwane scenariusze</span><span class="sxs-lookup"><span data-stu-id="594a1-109">Supported scenarios</span></span>
<span data-ttu-id="594a1-110">Dane należy skopiować **z usługi Azure SQL Data Warehouse** do następujących danych przechowuje:</span><span class="sxs-lookup"><span data-stu-id="594a1-110">You can copy data **from Azure SQL Data Warehouse** to the following data stores:</span></span>

[!INCLUDE [data-factory-supported-sinks](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="594a1-111">Możesz skopiować dane z następujących baz danych **Azure SQL Data Warehouse**:</span><span class="sxs-lookup"><span data-stu-id="594a1-111">You can copy data from the following data stores **to Azure SQL Data Warehouse**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

> [!TIP]
> <span data-ttu-id="594a1-112">Podczas kopiowania danych z serwera SQL lub bazy danych SQL Azure do usługi Azure SQL Data Warehouse, jeśli tabela nie istnieje w magazynie docelowym, fabryki danych może automatycznie tworzyć tabeli w usłudze SQL Data Warehouse przy użyciu schematu tabeli w magazynie źródła danych.</span><span class="sxs-lookup"><span data-stu-id="594a1-112">When copying data from SQL Server or Azure SQL Database to Azure SQL Data Warehouse, if the table does not exist in the destination store, Data Factory can automatically create the table in SQL Data Warehouse by using the schema of the table in the source data store.</span></span> <span data-ttu-id="594a1-113">Zobacz [automatycznego tworzenia tabel](#auto-table-creation) szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="594a1-113">See [Auto table creation](#auto-table-creation) for details.</span></span>

## <a name="supported-authentication-type"></a><span data-ttu-id="594a1-114">Obsługiwany typ uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="594a1-114">Supported authentication type</span></span>
<span data-ttu-id="594a1-115">Azure SQL Data Warehouse łącznika Obsługa uwierzytelniania podstawowego.</span><span class="sxs-lookup"><span data-stu-id="594a1-115">Azure SQL Data Warehouse connector support basic authentication.</span></span>

## <a name="getting-started"></a><span data-ttu-id="594a1-116">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="594a1-116">Getting started</span></span>
<span data-ttu-id="594a1-117">Można utworzyć potok z działania kopiowania, który przenosi dane z usługi Azure SQL Data Warehouse przy użyciu różnych narzędzi/interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="594a1-117">You can create a pipeline with a copy activity that moves data to/from an Azure SQL Data Warehouse by using different tools/APIs.</span></span>

<span data-ttu-id="594a1-118">Najprostszym sposobem, aby utworzyć potok, który kopiuje dane z magazynu danych SQL Azure jest za pomocą Kreatora kopiowania danych.</span><span class="sxs-lookup"><span data-stu-id="594a1-118">The easiest way to create a pipeline that copies data to/from Azure SQL Data Warehouse is to use the Copy data wizard.</span></span> <span data-ttu-id="594a1-119">Zobacz [samouczek: ładowanie danych do usługi SQL Data Warehouse z fabryką danych](../sql-data-warehouse/sql-data-warehouse-load-with-data-factory.md) szybkie przewodnik dotyczący tworzenia potoku za pomocą Kreatora kopiowania danych.</span><span class="sxs-lookup"><span data-stu-id="594a1-119">See [Tutorial: Load data into SQL Data Warehouse with Data Factory](../sql-data-warehouse/sql-data-warehouse-load-with-data-factory.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="594a1-120">Umożliwia także następujące narzędzia do tworzenia potoku: **portalu Azure**, **programu Visual Studio**, **programu Azure PowerShell**, **szablonu usługi Azure Resource Manager**, **interfejs API .NET**, i **interfejsu API REST**.</span><span class="sxs-lookup"><span data-stu-id="594a1-120">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="594a1-121">Zobacz [samouczek działania kopiowania](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) instrukcje krok po kroku utworzyć potok z działaniem kopiowania.</span><span class="sxs-lookup"><span data-stu-id="594a1-121">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span>

<span data-ttu-id="594a1-122">Czy można użyć narzędzia i interfejsy API, należy wykonać następujące kroki, aby utworzyć potok, który przenosi dane z magazynu danych źródła do ujścia magazynu danych:</span><span class="sxs-lookup"><span data-stu-id="594a1-122">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="594a1-123">Utwórz **fabryki danych**.</span><span class="sxs-lookup"><span data-stu-id="594a1-123">Create a **data factory**.</span></span> <span data-ttu-id="594a1-124">Fabryka danych może zawierać co najmniej jeden potoków.</span><span class="sxs-lookup"><span data-stu-id="594a1-124">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="594a1-125">Utwórz **połączone usługi** Aby połączyć dane wejściowe i wyjściowe są przechowywane w fabryce danych.</span><span class="sxs-lookup"><span data-stu-id="594a1-125">Create **linked services** to link input and output data stores to your data factory.</span></span> <span data-ttu-id="594a1-126">Na przykład jeśli kopiujesz danych z magazynu obiektów blob platformy Azure do usługi Azure SQL data warehouse, Utwórz dwa połączone usługi, aby połączyć Twoje konto magazynu Azure i usługi Azure SQL data warehouse z fabryką danych.</span><span class="sxs-lookup"><span data-stu-id="594a1-126">For example, if you are copying data from an Azure blob storage to an Azure SQL data warehouse, you create two linked services to link your Azure storage account and Azure SQL data warehouse to your data factory.</span></span> <span data-ttu-id="594a1-127">Dla właściwości połączonej usługi, które są specyficzne dla usługi Azure SQL Data Warehouse, zobacz [połączona usługa właściwości](#linked-service-properties) sekcji.</span><span class="sxs-lookup"><span data-stu-id="594a1-127">For linked service properties that are specific to Azure SQL Data Warehouse, see [linked service properties](#linked-service-properties) section.</span></span> 
3. <span data-ttu-id="594a1-128">Utwórz **zestawów danych** do reprezentowania danych wejściowych i wyjściowych operacji kopiowania.</span><span class="sxs-lookup"><span data-stu-id="594a1-128">Create **datasets** to represent input and output data for the copy operation.</span></span> <span data-ttu-id="594a1-129">W tym przykładzie wymienionych w ostatnim kroku tworzenia zestawu danych, aby określić folder, który zawiera dane wejściowe i kontener obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="594a1-129">In the example mentioned in the last step, you create a dataset to specify the blob container and folder that contains the input data.</span></span> <span data-ttu-id="594a1-130">I Utwórz innego elementu dataset, aby określić tabeli w magazynie danych Azure SQL, która przechowuje dane skopiowane z magazynu obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="594a1-130">And, you create another dataset to specify the table in the Azure SQL data warehouse that holds the data copied from the blob storage.</span></span> <span data-ttu-id="594a1-131">Dla właściwości zestawu danych, które są specyficzne dla usługi Azure SQL Data Warehouse, zobacz [właściwości zestawu danych](#dataset-properties) sekcji.</span><span class="sxs-lookup"><span data-stu-id="594a1-131">For dataset properties that are specific to Azure SQL Data Warehouse, see [dataset properties](#dataset-properties) section.</span></span>
4. <span data-ttu-id="594a1-132">Utwórz **potoku** aktywnością kopiowania zestawu danych jako dane wejściowe i zestawu danych jako dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="594a1-132">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="594a1-133">W przykładzie wspomniano wcześniej używasz BlobSource jako źródło i SqlDWSink jako zbiorniku dla działania kopiowania.</span><span class="sxs-lookup"><span data-stu-id="594a1-133">In the example mentioned earlier, you use BlobSource as a source and SqlDWSink as a sink for the copy activity.</span></span> <span data-ttu-id="594a1-134">Podobnie magazyn danych SQL Azure są kopiowane do magazynu obiektów Blob Azure, należy użyć SqlDWSource i BlobSink w przypadku działania kopiowania.</span><span class="sxs-lookup"><span data-stu-id="594a1-134">Similarly, if you are copying from Azure SQL Data Warehouse to Azure Blob Storage, you use SqlDWSource and BlobSink in the copy activity.</span></span> <span data-ttu-id="594a1-135">Właściwości działania kopiowania, które są specyficzne dla usługi Azure SQL Data Warehouse, zobacz [skopiować właściwości działania](#copy-activity-properties) sekcji.</span><span class="sxs-lookup"><span data-stu-id="594a1-135">For copy activity properties that are specific to Azure SQL Data Warehouse, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="594a1-136">Aby uzyskać szczegółowe informacje dotyczące sposobu używania magazynu danych jako źródło lub zbiorniku kliknij łącze w poprzedniej sekcji dla magazynu danych.</span><span class="sxs-lookup"><span data-stu-id="594a1-136">For details on how to use a data store as a source or a sink, click the link in the previous section for your data store.</span></span>

<span data-ttu-id="594a1-137">Korzystając z kreatora, definicje JSON do tych jednostek fabryki danych (połączone usługi, zestawy danych i potoki) są tworzone automatycznie dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="594a1-137">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="594a1-138">Korzystając z narzędzi/API (z wyjątkiem interfejs API .NET), należy zdefiniować tych jednostek fabryki danych w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="594a1-138">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="594a1-139">Dla przykładów z definicji JSON dla jednostek fabryki danych, które są używane do kopiowania danych do/z usługi Azure SQL Data Warehouse, zobacz [przykłady JSON](#json-examples-for-copying-data-to-and-from-sql-data-warehouse) sekcji tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="594a1-139">For samples with JSON definitions for Data Factory entities that are used to copy data to/from an Azure SQL Data Warehouse, see [JSON examples](#json-examples-for-copying-data-to-and-from-sql-data-warehouse) section of this article.</span></span>

<span data-ttu-id="594a1-140">Poniższe sekcje zawierają szczegółowe informacje o właściwości JSON, które są używane do definiowania określonych jednostek fabryki danych Azure SQL Data Warehouse:</span><span class="sxs-lookup"><span data-stu-id="594a1-140">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Azure SQL Data Warehouse:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="594a1-141">Połączona usługa właściwości</span><span class="sxs-lookup"><span data-stu-id="594a1-141">Linked service properties</span></span>
<span data-ttu-id="594a1-142">Poniższa tabela zawiera opis specyficzne dla usługi Azure SQL Data Warehouse połączone elementy JSON.</span><span class="sxs-lookup"><span data-stu-id="594a1-142">The following table provides description for JSON elements specific to Azure SQL Data Warehouse linked service.</span></span>

| <span data-ttu-id="594a1-143">Właściwość</span><span class="sxs-lookup"><span data-stu-id="594a1-143">Property</span></span> | <span data-ttu-id="594a1-144">Opis</span><span class="sxs-lookup"><span data-stu-id="594a1-144">Description</span></span> | <span data-ttu-id="594a1-145">Wymagane</span><span class="sxs-lookup"><span data-stu-id="594a1-145">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="594a1-146">type</span><span class="sxs-lookup"><span data-stu-id="594a1-146">type</span></span> |<span data-ttu-id="594a1-147">Właściwość type musi mieć ustawioną: **AzureSqlDW**</span><span class="sxs-lookup"><span data-stu-id="594a1-147">The type property must be set to: **AzureSqlDW**</span></span> |<span data-ttu-id="594a1-148">Tak</span><span class="sxs-lookup"><span data-stu-id="594a1-148">Yes</span></span> |
| <span data-ttu-id="594a1-149">Parametry połączenia</span><span class="sxs-lookup"><span data-stu-id="594a1-149">connectionString</span></span> |<span data-ttu-id="594a1-150">Podaj informacje wymagane do połączenia z wystąpieniem usługi Azure SQL Data Warehouse właściwości connectionString.</span><span class="sxs-lookup"><span data-stu-id="594a1-150">Specify information needed to connect to the Azure SQL Data Warehouse instance for the connectionString property.</span></span> <span data-ttu-id="594a1-151">Obsługiwane jest tylko uwierzytelnianie podstawowe.</span><span class="sxs-lookup"><span data-stu-id="594a1-151">Only basic authentication is supported.</span></span> |<span data-ttu-id="594a1-152">Tak</span><span class="sxs-lookup"><span data-stu-id="594a1-152">Yes</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="594a1-153">Skonfiguruj [zapory bazy danych SQL Azure](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure) i serwer bazy danych do [Zezwalaj usługom Azure na dostęp do serwera](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure).</span><span class="sxs-lookup"><span data-stu-id="594a1-153">Configure [Azure SQL Database Firewall](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure) and the database server to [allow Azure Services to access the server](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure).</span></span> <span data-ttu-id="594a1-154">Ponadto jeśli kopiujesz danych Azure SQL Data Warehouse z poza tym Azure z lokalnych źródeł danych z bramą fabryki danych, należy skonfigurować odpowiedni zakres adresów IP dla komputera, który wysyła dane do usługi Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="594a1-154">Additionally, if you are copying data to Azure SQL Data Warehouse from outside Azure including from on-premises data sources with data factory gateway, configure appropriate IP address range for the machine that is sending data to Azure SQL Data Warehouse.</span></span>

## <a name="dataset-properties"></a><span data-ttu-id="594a1-155">Właściwości zestawu danych</span><span class="sxs-lookup"><span data-stu-id="594a1-155">Dataset properties</span></span>
<span data-ttu-id="594a1-156">Aby uzyskać pełną listę sekcje & właściwości dostępne do definiowania zestawów danych, zobacz [Tworzenie zbiorów danych](data-factory-create-datasets.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="594a1-156">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="594a1-157">Sekcje zawierają informacje, takie jak struktury, dostępności i zasad zestawu danych JSON są podobne dla wszystkich typów obiektów dataset (Azure SQL, obiektów blob platformy Azure, Azure tabeli itp.).</span><span class="sxs-lookup"><span data-stu-id="594a1-157">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="594a1-158">Sekcja typeProperties jest różne dla każdego typu zestawu danych i zawiera informacje o lokalizacji danych w magazynie danych.</span><span class="sxs-lookup"><span data-stu-id="594a1-158">The typeProperties section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="594a1-159">**TypeProperties** sekcja dla zestawu danych typu **AzureSqlDWTable** ma następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="594a1-159">The **typeProperties** section for the dataset of type **AzureSqlDWTable** has the following properties:</span></span>

| <span data-ttu-id="594a1-160">Właściwość</span><span class="sxs-lookup"><span data-stu-id="594a1-160">Property</span></span> | <span data-ttu-id="594a1-161">Opis</span><span class="sxs-lookup"><span data-stu-id="594a1-161">Description</span></span> | <span data-ttu-id="594a1-162">Wymagane</span><span class="sxs-lookup"><span data-stu-id="594a1-162">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="594a1-163">tableName</span><span class="sxs-lookup"><span data-stu-id="594a1-163">tableName</span></span> |<span data-ttu-id="594a1-164">Nazwa tabeli lub widoku w bazie danych Azure SQL Data Warehouse, odnoszący się do połączonej usługi.</span><span class="sxs-lookup"><span data-stu-id="594a1-164">Name of the table or view in the Azure SQL Data Warehouse database that the linked service refers to.</span></span> |<span data-ttu-id="594a1-165">Tak</span><span class="sxs-lookup"><span data-stu-id="594a1-165">Yes</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="594a1-166">Właściwości działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="594a1-166">Copy activity properties</span></span>
<span data-ttu-id="594a1-167">Pełną listę sekcje & właściwości dostępne do definiowania działań, zobacz [tworzenie potoków](data-factory-create-pipelines.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="594a1-167">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="594a1-168">Właściwości, takie jak nazwa, opis, dane wejściowe i wyjściowe tabel i zasady są dostępne dla wszystkich typów działań.</span><span class="sxs-lookup"><span data-stu-id="594a1-168">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

> [!NOTE]
> <span data-ttu-id="594a1-169">Działanie kopiowania przyjmuje tylko jeden parametr wejściowy i tworzy tylko jedno wyjście.</span><span class="sxs-lookup"><span data-stu-id="594a1-169">The Copy Activity takes only one input and produces only one output.</span></span>

<span data-ttu-id="594a1-170">Właściwości, które są dostępne w sekcji typeProperties działania różnić się z każdym typem działania.</span><span class="sxs-lookup"><span data-stu-id="594a1-170">Whereas, properties available in the typeProperties section of the activity vary with each activity type.</span></span> <span data-ttu-id="594a1-171">Dla działania kopiowania różnią się w zależności od typów źródeł i sink.</span><span class="sxs-lookup"><span data-stu-id="594a1-171">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

### <a name="sqldwsource"></a><span data-ttu-id="594a1-172">SqlDWSource</span><span class="sxs-lookup"><span data-stu-id="594a1-172">SqlDWSource</span></span>
<span data-ttu-id="594a1-173">Jeśli źródło jest typu **SqlDWSource**, są dostępne w następujących właściwości **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="594a1-173">When source is of type **SqlDWSource**, the following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="594a1-174">Właściwość</span><span class="sxs-lookup"><span data-stu-id="594a1-174">Property</span></span> | <span data-ttu-id="594a1-175">Opis</span><span class="sxs-lookup"><span data-stu-id="594a1-175">Description</span></span> | <span data-ttu-id="594a1-176">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="594a1-176">Allowed values</span></span> | <span data-ttu-id="594a1-177">Wymagane</span><span class="sxs-lookup"><span data-stu-id="594a1-177">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="594a1-178">sqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="594a1-178">sqlReaderQuery</span></span> |<span data-ttu-id="594a1-179">Użyj niestandardowych zapytania można odczytać danych.</span><span class="sxs-lookup"><span data-stu-id="594a1-179">Use the custom query to read data.</span></span> |<span data-ttu-id="594a1-180">Ciąg zapytania SQL.</span><span class="sxs-lookup"><span data-stu-id="594a1-180">SQL query string.</span></span> <span data-ttu-id="594a1-181">Na przykład: Wybierz * z MyTable.</span><span class="sxs-lookup"><span data-stu-id="594a1-181">For example: select * from MyTable.</span></span> |<span data-ttu-id="594a1-182">Nie</span><span class="sxs-lookup"><span data-stu-id="594a1-182">No</span></span> |
| <span data-ttu-id="594a1-183">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="594a1-183">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="594a1-184">Nazwa procedury przechowywanej, która odczytuje dane z tabeli źródłowej.</span><span class="sxs-lookup"><span data-stu-id="594a1-184">Name of the stored procedure that reads data from the source table.</span></span> |<span data-ttu-id="594a1-185">Nazwa procedury składowanej.</span><span class="sxs-lookup"><span data-stu-id="594a1-185">Name of the stored procedure.</span></span> <span data-ttu-id="594a1-186">Ostatniej instrukcji SQL musi być instrukcji SELECT w procedurze składowanej.</span><span class="sxs-lookup"><span data-stu-id="594a1-186">The last SQL statement must be a SELECT statement in the stored procedure.</span></span> |<span data-ttu-id="594a1-187">Nie</span><span class="sxs-lookup"><span data-stu-id="594a1-187">No</span></span> |
| <span data-ttu-id="594a1-188">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="594a1-188">storedProcedureParameters</span></span> |<span data-ttu-id="594a1-189">Parametry dla procedury składowanej.</span><span class="sxs-lookup"><span data-stu-id="594a1-189">Parameters for the stored procedure.</span></span> |<span data-ttu-id="594a1-190">Par nazwa/wartość.</span><span class="sxs-lookup"><span data-stu-id="594a1-190">Name/value pairs.</span></span> <span data-ttu-id="594a1-191">Nazwy i wielkość liter w wyrazie parametry muszą być zgodne, nazwy i wielkość liter w wyrazie parametry procedury składowanej.</span><span class="sxs-lookup"><span data-stu-id="594a1-191">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> |<span data-ttu-id="594a1-192">Nie</span><span class="sxs-lookup"><span data-stu-id="594a1-192">No</span></span> |

<span data-ttu-id="594a1-193">Jeśli **sqlReaderQuery** określono dla SqlDWSource, odbywa się działanie kopii tego zapytania względem źródła magazynu danych SQL Azure umożliwiają pobieranie danych.</span><span class="sxs-lookup"><span data-stu-id="594a1-193">If the **sqlReaderQuery** is specified for the SqlDWSource, the Copy Activity runs this query against the Azure SQL Data Warehouse source to get the data.</span></span>

<span data-ttu-id="594a1-194">Można również określić procedury składowanej, podając **sqlReaderStoredProcedureName** i **storedProcedureParameters** (jeśli jest to procedura składowana pobiera parametry).</span><span class="sxs-lookup"><span data-stu-id="594a1-194">Alternatively, you can specify a stored procedure by specifying the **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if the stored procedure takes parameters).</span></span>

<span data-ttu-id="594a1-195">Jeśli nie określisz sqlReaderQuery lub sqlReaderStoredProcedureName kolumny zdefiniowane w sekcji struktury zestawu danych JSON służą do skonstruowania zapytania w celu uruchomienia usługi Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="594a1-195">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, the columns defined in the structure section of the dataset JSON are used to build a query to run against the Azure SQL Data Warehouse.</span></span> <span data-ttu-id="594a1-196">Przykład: `select column1, column2 from mytable`.</span><span class="sxs-lookup"><span data-stu-id="594a1-196">Example: `select column1, column2 from mytable`.</span></span> <span data-ttu-id="594a1-197">Jeśli definicji zestawu danych nie ma on struktury, wszystkie kolumny są wybierane w tabeli.</span><span class="sxs-lookup"><span data-stu-id="594a1-197">If the dataset definition does not have the structure, all columns are selected from the table.</span></span>

#### <a name="sqldwsource-example"></a><span data-ttu-id="594a1-198">Przykład SqlDWSource</span><span class="sxs-lookup"><span data-stu-id="594a1-198">SqlDWSource example</span></span>

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
<span data-ttu-id="594a1-199">**Definicja procedury składowanej:**</span><span class="sxs-lookup"><span data-stu-id="594a1-199">**The stored procedure definition:**</span></span>

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

### <a name="sqldwsink"></a><span data-ttu-id="594a1-200">SqlDWSink</span><span class="sxs-lookup"><span data-stu-id="594a1-200">SqlDWSink</span></span>
<span data-ttu-id="594a1-201">**SqlDWSink** obsługuje następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="594a1-201">**SqlDWSink** supports the following properties:</span></span>

| <span data-ttu-id="594a1-202">Właściwość</span><span class="sxs-lookup"><span data-stu-id="594a1-202">Property</span></span> | <span data-ttu-id="594a1-203">Opis</span><span class="sxs-lookup"><span data-stu-id="594a1-203">Description</span></span> | <span data-ttu-id="594a1-204">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="594a1-204">Allowed values</span></span> | <span data-ttu-id="594a1-205">Wymagane</span><span class="sxs-lookup"><span data-stu-id="594a1-205">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="594a1-206">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="594a1-206">sqlWriterCleanupScript</span></span> |<span data-ttu-id="594a1-207">Określ kwerendę dla działania kopiowania do wykonania w taki sposób, że dane określonych wycinek jest wyczyszczone.</span><span class="sxs-lookup"><span data-stu-id="594a1-207">Specify a query for Copy Activity to execute such that data of a specific slice is cleaned up.</span></span> <span data-ttu-id="594a1-208">Aby uzyskać więcej informacji, zobacz [sekcji powtarzalności](#repeatability-during-copy).</span><span class="sxs-lookup"><span data-stu-id="594a1-208">For details, see [repeatability section](#repeatability-during-copy).</span></span> |<span data-ttu-id="594a1-209">Instrukcja zapytania.</span><span class="sxs-lookup"><span data-stu-id="594a1-209">A query statement.</span></span> |<span data-ttu-id="594a1-210">Nie</span><span class="sxs-lookup"><span data-stu-id="594a1-210">No</span></span> |
| <span data-ttu-id="594a1-211">allowPolyBase</span><span class="sxs-lookup"><span data-stu-id="594a1-211">allowPolyBase</span></span> |<span data-ttu-id="594a1-212">Wskazuje, czy do użycia zamiast mechanizmu BULKINSERT PolyBase (jeśli jest to wymagane).</span><span class="sxs-lookup"><span data-stu-id="594a1-212">Indicates whether to use PolyBase (when applicable) instead of BULKINSERT mechanism.</span></span> <br/><br/> <span data-ttu-id="594a1-213">**Przy użyciu programu PolyBase jest zalecanym sposobem ładowanie danych do usługi SQL Data Warehouse.**</span><span class="sxs-lookup"><span data-stu-id="594a1-213">**Using PolyBase is the recommended way to load data into SQL Data Warehouse.**</span></span> <span data-ttu-id="594a1-214">Zobacz [Użyj programu PolyBase, aby załadować dane do usługi Azure SQL Data Warehouse](#use-polybase-to-load-data-into-azure-sql-data-warehouse) sekcji dla ograniczenia i szczegółów.</span><span class="sxs-lookup"><span data-stu-id="594a1-214">See [Use PolyBase to load data into Azure SQL Data Warehouse](#use-polybase-to-load-data-into-azure-sql-data-warehouse) section for constraints and details.</span></span> |<span data-ttu-id="594a1-215">True</span><span class="sxs-lookup"><span data-stu-id="594a1-215">True</span></span> <br/><span data-ttu-id="594a1-216">Wartość FAŁSZ (ustawienie domyślne)</span><span class="sxs-lookup"><span data-stu-id="594a1-216">False (default)</span></span> |<span data-ttu-id="594a1-217">Nie</span><span class="sxs-lookup"><span data-stu-id="594a1-217">No</span></span> |
| <span data-ttu-id="594a1-218">Usługi</span><span class="sxs-lookup"><span data-stu-id="594a1-218">polyBaseSettings</span></span> |<span data-ttu-id="594a1-219">Grupy właściwości, które można określić, kiedy **allowPolybase** właściwość jest ustawiona na **true**.</span><span class="sxs-lookup"><span data-stu-id="594a1-219">A group of properties that can be specified when the **allowPolybase** property is set to **true**.</span></span> |&nbsp; |<span data-ttu-id="594a1-220">Nie</span><span class="sxs-lookup"><span data-stu-id="594a1-220">No</span></span> |
| <span data-ttu-id="594a1-221">rejectValue</span><span class="sxs-lookup"><span data-stu-id="594a1-221">rejectValue</span></span> |<span data-ttu-id="594a1-222">Określa liczbę lub odsetek wierszy, które można odrzucić przed zapytanie nie powiedzie się.</span><span class="sxs-lookup"><span data-stu-id="594a1-222">Specifies the number or percentage of rows that can be rejected before the query fails.</span></span> <br/><br/><span data-ttu-id="594a1-223">Dowiedz się więcej o opcjach Odrzuć PolyBase **argumenty** sekcji [Tworzenie tabeli zewnętrznej (Transact-SQL)](https://msdn.microsoft.com/library/dn935021.aspx) tematu.</span><span class="sxs-lookup"><span data-stu-id="594a1-223">Learn more about the PolyBase’s reject options in the **Arguments** section of [CREATE EXTERNAL TABLE (Transact-SQL)](https://msdn.microsoft.com/library/dn935021.aspx) topic.</span></span> |<span data-ttu-id="594a1-224">0 (domyślnie), 1, 2...</span><span class="sxs-lookup"><span data-stu-id="594a1-224">0 (default), 1, 2, …</span></span> |<span data-ttu-id="594a1-225">Nie</span><span class="sxs-lookup"><span data-stu-id="594a1-225">No</span></span> |
| <span data-ttu-id="594a1-226">dla właściwości rejectType</span><span class="sxs-lookup"><span data-stu-id="594a1-226">rejectType</span></span> |<span data-ttu-id="594a1-227">Określa, czy opcja rejectValue jest określona jako wartość literału lub wartość procentowa.</span><span class="sxs-lookup"><span data-stu-id="594a1-227">Specifies whether the rejectValue option is specified as a literal value or a percentage.</span></span> |<span data-ttu-id="594a1-228">Wartość (ustawienie domyślne), wartość procentowa</span><span class="sxs-lookup"><span data-stu-id="594a1-228">Value (default), Percentage</span></span> |<span data-ttu-id="594a1-229">Nie</span><span class="sxs-lookup"><span data-stu-id="594a1-229">No</span></span> |
| <span data-ttu-id="594a1-230">rejectSampleValue</span><span class="sxs-lookup"><span data-stu-id="594a1-230">rejectSampleValue</span></span> |<span data-ttu-id="594a1-231">Określa liczbę wierszy do pobrania przed PolyBase ponownie oblicza procent odrzuconych wierszy.</span><span class="sxs-lookup"><span data-stu-id="594a1-231">Determines the number of rows to retrieve before the PolyBase recalculates the percentage of rejected rows.</span></span> |<span data-ttu-id="594a1-232">1, 2, …</span><span class="sxs-lookup"><span data-stu-id="594a1-232">1, 2, …</span></span> |<span data-ttu-id="594a1-233">Tak, jeśli **dla właściwości rejectType** jest **procent**</span><span class="sxs-lookup"><span data-stu-id="594a1-233">Yes, if **rejectType** is **percentage**</span></span> |
| <span data-ttu-id="594a1-234">useTypeDefault</span><span class="sxs-lookup"><span data-stu-id="594a1-234">useTypeDefault</span></span> |<span data-ttu-id="594a1-235">Określa sposób obsługi brakujących wartości w rozdzielane pliki tekstowe, jeśli PolyBase pobiera dane z pliku tekstowego.</span><span class="sxs-lookup"><span data-stu-id="594a1-235">Specifies how to handle missing values in delimited text files when PolyBase retrieves data from the text file.</span></span><br/><br/><span data-ttu-id="594a1-236">Dowiedz się więcej o tej właściwości z sekcji argumenty w [utworzyć EXTERNAL FILE FORMAT (Transact-SQL)](https://msdn.microsoft.com/library/dn935026.aspx).</span><span class="sxs-lookup"><span data-stu-id="594a1-236">Learn more about this property from the Arguments section in [CREATE EXTERNAL FILE FORMAT (Transact-SQL)](https://msdn.microsoft.com/library/dn935026.aspx).</span></span> |<span data-ttu-id="594a1-237">Wartość true, False (ustawienie domyślne)</span><span class="sxs-lookup"><span data-stu-id="594a1-237">True, False (default)</span></span> |<span data-ttu-id="594a1-238">Nie</span><span class="sxs-lookup"><span data-stu-id="594a1-238">No</span></span> |
| <span data-ttu-id="594a1-239">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="594a1-239">writeBatchSize</span></span> |<span data-ttu-id="594a1-240">Wstawia dane do tabeli SQL, gdy writeBatchSize osiągnie rozmiar buforu</span><span class="sxs-lookup"><span data-stu-id="594a1-240">Inserts data into the SQL table when the buffer size reaches writeBatchSize</span></span> |<span data-ttu-id="594a1-241">Liczba całkowita (liczba wierszy)</span><span class="sxs-lookup"><span data-stu-id="594a1-241">Integer (number of rows)</span></span> |<span data-ttu-id="594a1-242">Nie (domyślne: 10000)</span><span class="sxs-lookup"><span data-stu-id="594a1-242">No (default: 10000)</span></span> |
| <span data-ttu-id="594a1-243">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="594a1-243">writeBatchTimeout</span></span> |<span data-ttu-id="594a1-244">Czas na ukończenie zanim upłynie limit czasu operacji wstawiania wsadowego oczekiwania.</span><span class="sxs-lookup"><span data-stu-id="594a1-244">Wait time for the batch insert operation to complete before it times out.</span></span> |<span data-ttu-id="594a1-245">Zakres czasu</span><span class="sxs-lookup"><span data-stu-id="594a1-245">timespan</span></span><br/><br/> <span data-ttu-id="594a1-246">Przykład: "00: 30:00" (30 minut).</span><span class="sxs-lookup"><span data-stu-id="594a1-246">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="594a1-247">Nie</span><span class="sxs-lookup"><span data-stu-id="594a1-247">No</span></span> |

#### <a name="sqldwsink-example"></a><span data-ttu-id="594a1-248">Przykład SqlDWSink</span><span class="sxs-lookup"><span data-stu-id="594a1-248">SqlDWSink example</span></span>

```JSON
"sink": {
    "type": "SqlDWSink",
    "allowPolyBase": true
}
```

## <a name="use-polybase-to-load-data-into-azure-sql-data-warehouse"></a><span data-ttu-id="594a1-249">Użyj programu PolyBase, aby załadować dane do magazynu danych SQL Azure</span><span class="sxs-lookup"><span data-stu-id="594a1-249">Use PolyBase to load data into Azure SQL Data Warehouse</span></span>
<span data-ttu-id="594a1-250">Przy użyciu  **[PolyBase](https://docs.microsoft.com/sql/relational-databases/polybase/polybase-guide)**  jest wydajny sposób ładowania dużych ilości danych do magazynu danych SQL Azure z wysokiej przepływności.</span><span class="sxs-lookup"><span data-stu-id="594a1-250">Using **[PolyBase](https://docs.microsoft.com/sql/relational-databases/polybase/polybase-guide)** is an efficient way of loading large amount of data into Azure SQL Data Warehouse with high throughput.</span></span> <span data-ttu-id="594a1-251">Przy użyciu programu PolyBase zamiast domyślnego mechanizmu BULKINSERT widać duże korzyści w przepływności.</span><span class="sxs-lookup"><span data-stu-id="594a1-251">You can see a large gain in the throughput by using PolyBase instead of the default BULKINSERT mechanism.</span></span> <span data-ttu-id="594a1-252">Zobacz [skopiuj numer odwołania wydajności](data-factory-copy-activity-performance.md#performance-reference) z szczegółowe porównanie.</span><span class="sxs-lookup"><span data-stu-id="594a1-252">See [copy performance reference number](data-factory-copy-activity-performance.md#performance-reference) with detailed comparison.</span></span> <span data-ttu-id="594a1-253">Aby uzyskać wskazówki z przypadkiem użycia, zobacz [załadować 1 TB do usługi Azure SQL Data Warehouse z fabryką danych Azure w obszarze 15 minut](data-factory-load-sql-data-warehouse.md).</span><span class="sxs-lookup"><span data-stu-id="594a1-253">For a walkthrough with a use case, see [Load 1 TB into Azure SQL Data Warehouse under 15 minutes with Azure Data Factory](data-factory-load-sql-data-warehouse.md).</span></span>

* <span data-ttu-id="594a1-254">Jeśli źródło danych jest w **obiektów Blob platformy Azure lub usługi Azure Data Lake Store**i format jest zgodny z PolyBase, można skopiować bezpośrednio do usługi Azure SQL Data Warehouse przy użyciu programu PolyBase.</span><span class="sxs-lookup"><span data-stu-id="594a1-254">If your source data is in **Azure Blob or Azure Data Lake Store**, and the format is compatible with PolyBase, you can directly copy to Azure SQL Data Warehouse using PolyBase.</span></span> <span data-ttu-id="594a1-255">Zobacz  **[bezpośrednich kopii przy użyciu programu PolyBase](#direct-copy-using-polybase)**  ze szczegółami.</span><span class="sxs-lookup"><span data-stu-id="594a1-255">See **[Direct copy using PolyBase](#direct-copy-using-polybase)** with details.</span></span>
* <span data-ttu-id="594a1-256">Jeśli Twoje źródła magazynu danych i format nie jest początkowo obsługiwana przez aparat PolyBase, możesz użyć  **[przemieszczane kopiowania przy użyciu programu PolyBase](#staged-copy-using-polybase)**  funkcji zamiast tego.</span><span class="sxs-lookup"><span data-stu-id="594a1-256">If your source data store and format is not originally supported by PolyBase, you can use the **[Staged Copy using PolyBase](#staged-copy-using-polybase)** feature instead.</span></span> <span data-ttu-id="594a1-257">Udostępnia również możesz lepszą przepustowość automatycznie konwersji danych do formatu zgodnego PolyBase i przechowywanie danych w magazynie obiektów Blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="594a1-257">It also provides you better throughput by automatically converting the data into PolyBase-compatible format and storing the data in Azure Blob storage.</span></span> <span data-ttu-id="594a1-258">Następnie ładuje dane do usługi SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="594a1-258">It then loads data into SQL Data Warehouse.</span></span>

<span data-ttu-id="594a1-259">Ustaw `allowPolyBase` właściwości **true** jak pokazano w poniższym przykładzie dla fabryki danych Azure, skopiuj dane do usługi Azure SQL Data Warehouse przy użyciu programu PolyBase.</span><span class="sxs-lookup"><span data-stu-id="594a1-259">Set the `allowPolyBase` property to **true** as shown in the following example for Azure Data Factory to use PolyBase to copy data into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="594a1-260">Podczas allowPolyBase jest ustawiona na wartość true, można określić za pomocą właściwości specyficzne dla programu PolyBase `polyBaseSettings` grupy właściwości.</span><span class="sxs-lookup"><span data-stu-id="594a1-260">When you set allowPolyBase to true, you can specify PolyBase specific properties using the `polyBaseSettings` property group.</span></span> <span data-ttu-id="594a1-261">zobacz [SqlDWSink](#SqlDWSink) sekcji, aby uzyskać więcej informacji o właściwościach, które mogą korzystać z usługi.</span><span class="sxs-lookup"><span data-stu-id="594a1-261">see the [SqlDWSink](#SqlDWSink) section for details about properties that you can use with polyBaseSettings.</span></span>

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

### <a name="direct-copy-using-polybase"></a><span data-ttu-id="594a1-262">Bezpośrednie kopiowania przy użyciu programu PolyBase</span><span class="sxs-lookup"><span data-stu-id="594a1-262">Direct copy using PolyBase</span></span>
<span data-ttu-id="594a1-263">Aparat PolyBase magazynu danych SQL obsługuje bezpośrednio obiektów Blob platformy Azure i usługi Azure Data Lake Store (przy użyciu nazwy głównej usługi) jako źródło i wymagania format określonego pliku.</span><span class="sxs-lookup"><span data-stu-id="594a1-263">SQL Data Warehouse PolyBase directly support Azure Blob and Azure Data Lake Store (using service principal) as source and with specific file format requirements.</span></span> <span data-ttu-id="594a1-264">Jeśli źródło danych spełnia kryteria opisane w tej sekcji, możesz bezpośrednio skopiować z magazynu danych źródła do usługi Azure SQL Data Warehouse przy użyciu programu PolyBase.</span><span class="sxs-lookup"><span data-stu-id="594a1-264">If your source data meets the criteria described in this section, you can directly copy from source data store to Azure SQL Data Warehouse using PolyBase.</span></span> <span data-ttu-id="594a1-265">W przeciwnym razie można użyć [przemieszczane kopiowania przy użyciu programu PolyBase](#staged-copy-using-polybase).</span><span class="sxs-lookup"><span data-stu-id="594a1-265">Otherwise, you can use [Staged Copy using PolyBase](#staged-copy-using-polybase).</span></span>

> [!TIP]
> <span data-ttu-id="594a1-266">Aby skopiować dane z usługi Data Lake Store SQL Data Warehouse wydajnie, Dowiedz się więcej o [fabryki danych Azure ułatwia nawet wygodny do ujawniania wgląd w dane dotyczące danych podczas korzystania z usługi Data Lake Store z usługi SQL Data Warehouse](https://blogs.msdn.microsoft.com/azuredatalake/2017/04/08/azure-data-factory-makes-it-even-easier-and-convenient-to-uncover-insights-from-data-when-using-data-lake-store-with-sql-data-warehouse/).</span><span class="sxs-lookup"><span data-stu-id="594a1-266">To copy data from Data Lake Store to SQL Data Warehouse efficiently, learn more from [Azure Data Factory makes it even easier and convenient to uncover insights from data when using Data Lake Store with SQL Data Warehouse](https://blogs.msdn.microsoft.com/azuredatalake/2017/04/08/azure-data-factory-makes-it-even-easier-and-convenient-to-uncover-insights-from-data-when-using-data-lake-store-with-sql-data-warehouse/).</span></span>

<span data-ttu-id="594a1-267">Jeśli nie zostały spełnione wymagania, fabryki danych Azure sprawdza ustawienia i automatycznie powraca do mechanizmu BULKINSERT przenoszenia danych.</span><span class="sxs-lookup"><span data-stu-id="594a1-267">If the requirements are not met, Azure Data Factory checks the settings and automatically falls back to the BULKINSERT mechanism for the data movement.</span></span>

1. <span data-ttu-id="594a1-268">**Źródło połączona usługa** jest typu: **AzureStorage** lub **AzureDataLakeStore z uwierzytelnianiem główna usługi**.</span><span class="sxs-lookup"><span data-stu-id="594a1-268">**Source linked service** is of type: **AzureStorage** or **AzureDataLakeStore with service principal authentication**.</span></span>  
2. <span data-ttu-id="594a1-269">**Wejściowy zestaw danych** jest typu: **AzureBlob** lub **AzureDataLakeStore**i wpisz w formacie `type` właściwości **OrcFormat**, lub **TextFormat** z następujących konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="594a1-269">The **input dataset** is of type: **AzureBlob** or **AzureDataLakeStore**, and the format type under `type` properties is **OrcFormat**, or **TextFormat** with the following configurations:</span></span>

   1. <span data-ttu-id="594a1-270">`rowDelimiter`musi być  **\n** .</span><span class="sxs-lookup"><span data-stu-id="594a1-270">`rowDelimiter` must be **\n**.</span></span>
   2. <span data-ttu-id="594a1-271">`nullValue`ustawiono **pusty ciąg** (""), lub `treatEmptyAsNull` ustawiono **true**.</span><span class="sxs-lookup"><span data-stu-id="594a1-271">`nullValue` is set to **empty string** (""), or `treatEmptyAsNull` is set to **true**.</span></span>
   3. <span data-ttu-id="594a1-272">`encodingName`ustawiono **utf-8**, która jest **domyślne** wartość.</span><span class="sxs-lookup"><span data-stu-id="594a1-272">`encodingName` is set to **utf-8**, which is **default** value.</span></span>
   4. <span data-ttu-id="594a1-273">`escapeChar`, `quoteChar`, `firstRowAsHeader`, i `skipLineCount` nie zostały określone.</span><span class="sxs-lookup"><span data-stu-id="594a1-273">`escapeChar`, `quoteChar`, `firstRowAsHeader`, and `skipLineCount` are not specified.</span></span>
   5. <span data-ttu-id="594a1-274">`compression`może być **bez kompresji**, **GZip**, lub **Deflate**.</span><span class="sxs-lookup"><span data-stu-id="594a1-274">`compression` can be **no compression**, **GZip**, or **Deflate**.</span></span>

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

3. <span data-ttu-id="594a1-275">Brak nie `skipHeaderLineCount` w obszarze **BlobSource** lub **AzureDataLakeStore** dla działania kopiowania w potoku.</span><span class="sxs-lookup"><span data-stu-id="594a1-275">There is no `skipHeaderLineCount` setting under **BlobSource** or **AzureDataLakeStore** for the Copy activity in the pipeline.</span></span>
4. <span data-ttu-id="594a1-276">Brak nie `sliceIdentifierColumnName` w obszarze **SqlDWSink** dla działania kopiowania w potoku.</span><span class="sxs-lookup"><span data-stu-id="594a1-276">There is no `sliceIdentifierColumnName` setting under **SqlDWSink** for the Copy activity in the pipeline.</span></span> <span data-ttu-id="594a1-277">(PolyBase gwarantuje, że wszystkie dane są aktualizowane lub nic nie jest aktualizowana w jednym przebiegu.</span><span class="sxs-lookup"><span data-stu-id="594a1-277">(PolyBase guarantees that all data is updated or nothing is updated in a single run.</span></span> <span data-ttu-id="594a1-278">Aby osiągnąć **powtarzalności**, można użyć `sqlWriterCleanupScript`).</span><span class="sxs-lookup"><span data-stu-id="594a1-278">To achieve **repeatability**, you could use `sqlWriterCleanupScript`).</span></span>
5. <span data-ttu-id="594a1-279">Brak nie `columnMapping` używane w skojarzonych w kopii działania.</span><span class="sxs-lookup"><span data-stu-id="594a1-279">There is no `columnMapping` being used in the associated in Copy activity.</span></span>

### <a name="staged-copy-using-polybase"></a><span data-ttu-id="594a1-280">Kopiuj przygotowanego przy użyciu programu PolyBase</span><span class="sxs-lookup"><span data-stu-id="594a1-280">Staged Copy using PolyBase</span></span>
<span data-ttu-id="594a1-281">Źródło danych nie spełnia kryteriów wprowadzone w poprzedniej sekcji, umożliwia kopiowanie danych za pośrednictwem tymczasowego przemieszczania magazynu obiektów Blob Azure (nie może być magazyn w warstwie Premium).</span><span class="sxs-lookup"><span data-stu-id="594a1-281">When your source data doesn’t meet the criteria introduced in the previous section, you can enable copying data via an interim staging Azure Blob Storage (cannot be Premium Storage).</span></span> <span data-ttu-id="594a1-282">W takim przypadku fabryki danych Azure automatycznie dokonuje przekształcenia danych spełnia wymagania dotyczące formatu danych PolyBase, a następnie użyj programu PolyBase, aby załadować dane do usługi SQL Data Warehouse i na ostatnich oczyszczania tymczasowego danych z magazynu obiektów Blob.</span><span class="sxs-lookup"><span data-stu-id="594a1-282">In this case, Azure Data Factory automatically performs transformations on the data to meet data format requirements of PolyBase, then use PolyBase to load data into SQL Data Warehouse, and at last clean-up your temp data from the Blob storage.</span></span> <span data-ttu-id="594a1-283">Zobacz [przemieszczane kopiowania](data-factory-copy-activity-performance.md#staged-copy) szczegółowe informacje na temat jak kopiowanie danych za pośrednictwem tymczasowych obiektów Blob platformy Azure działa na ogół.</span><span class="sxs-lookup"><span data-stu-id="594a1-283">See [Staged Copy](data-factory-copy-activity-performance.md#staged-copy) for details on how copying data via a staging Azure Blob works in general.</span></span>

> [!NOTE]
> <span data-ttu-id="594a1-284">Podczas kopiowania danych z danych z lokalnego magazynu do usługi Azure SQL Data Warehouse przy użyciu programu PolyBase i przemieszczania, jeśli wersja bramy zarządzania danymi znajduje się poniżej 2.4 środowiska JRE (Java Runtime Environment) jest wymagana na komputerze bramy, służący do przekształcania danych źródłowych właściwego formatu.</span><span class="sxs-lookup"><span data-stu-id="594a1-284">When copying data from an on-prem data store into Azure SQL Data Warehouse using PolyBase and staging, if your Data Management Gateway version is below 2.4, JRE (Java Runtime Environment) is required on your gateway machine that is used to transform your source data into proper format.</span></span> <span data-ttu-id="594a1-285">Sugerują, że uaktualnienie bramy do najnowszej wersji w celu uniknięcia takiej zależności.</span><span class="sxs-lookup"><span data-stu-id="594a1-285">Suggest you upgrade your gateway to the latest to avoid such dependency.</span></span>
>

<span data-ttu-id="594a1-286">Aby użyć tej funkcji, należy utworzyć [połączonej usługi magazynu Azure](data-factory-azure-blob-connector.md#azure-storage-linked-service) odwołujący się do konta magazynu Azure, które ma magazynu tymczasowego obiektu blob, następnie określ `enableStaging` i `stagingSettings` właściwości dla działania kopiowania, jak pokazano w poniższym kodzie:</span><span class="sxs-lookup"><span data-stu-id="594a1-286">To use this feature, create an [Azure Storage linked service](data-factory-azure-blob-connector.md#azure-storage-linked-service) that refers to the Azure Storage Account that has the interim blob storage, then specify the `enableStaging` and `stagingSettings` properties for the Copy Activity as shown in the following code:</span></span>

```json
"activities":[  
{
    "name": "Sample copy activity from SQL Server to SQL Data Warehouse via PolyBase",
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

## <a name="best-practices-when-using-polybase"></a><span data-ttu-id="594a1-287">Najlepsze rozwiązania w sytuacji, gdy przy użyciu programu PolyBase</span><span class="sxs-lookup"><span data-stu-id="594a1-287">Best practices when using PolyBase</span></span>
<span data-ttu-id="594a1-288">Poniższe sekcje zawierają dodatkowe wskazówki te, które są wymienione w [najlepsze rozwiązania dotyczące usługi Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="594a1-288">The following sections provide additional best practices to the ones that are mentioned in [Best practices for Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-best-practices.md).</span></span>

### <a name="required-database-permission"></a><span data-ttu-id="594a1-289">Uprawnienia wymagane bazy danych</span><span class="sxs-lookup"><span data-stu-id="594a1-289">Required database permission</span></span>
<span data-ttu-id="594a1-290">Aby użyć programu PolyBase, wymaga użytkownika używane do ładowania danych do usługi SQL Data Warehouse [uprawnienia "CONTROL"](https://msdn.microsoft.com/library/ms191291.aspx) w docelowej bazie danych.</span><span class="sxs-lookup"><span data-stu-id="594a1-290">To use PolyBase, it requires the user being used to load data into SQL Data Warehouse has the ["CONTROL" permission](https://msdn.microsoft.com/library/ms191291.aspx) on the target database.</span></span> <span data-ttu-id="594a1-291">Jest jednym ze sposobów osiągnięcia, które można dodać tego użytkownika jako członka roli "db_owner".</span><span class="sxs-lookup"><span data-stu-id="594a1-291">One way to achieve that is to add that user as a member of "db_owner" role.</span></span> <span data-ttu-id="594a1-292">Dowiedz się, jak to zrobić, postępując [w tej sekcji](../sql-data-warehouse/sql-data-warehouse-overview-manage-security.md#authorization).</span><span class="sxs-lookup"><span data-stu-id="594a1-292">Learn how to do that by following [this section](../sql-data-warehouse/sql-data-warehouse-overview-manage-security.md#authorization).</span></span>

### <a name="row-size-and-data-type-limitation"></a><span data-ttu-id="594a1-293">Rozmiar wiersza i danych typu ograniczenia</span><span class="sxs-lookup"><span data-stu-id="594a1-293">Row size and data type limitation</span></span>
<span data-ttu-id="594a1-294">Program Polybase obciążenia są ograniczone do ładowania wierszy, zarówno mniejszy niż **1 MB** i nie można załadować VARCHR(MAX), NVARCHAR(MAX) lub VARBINARY(MAX).</span><span class="sxs-lookup"><span data-stu-id="594a1-294">Polybase loads are limited to loading rows both smaller than **1 MB** and cannot load to VARCHR(MAX), NVARCHAR(MAX) or VARBINARY(MAX).</span></span> <span data-ttu-id="594a1-295">Zapoznaj się [tutaj](../sql-data-warehouse/sql-data-warehouse-service-capacity-limits.md#loads).</span><span class="sxs-lookup"><span data-stu-id="594a1-295">Refer to [here](../sql-data-warehouse/sql-data-warehouse-service-capacity-limits.md#loads).</span></span>

<span data-ttu-id="594a1-296">Jeśli masz dane źródłowe z wierszami o rozmiarze większym niż 1 MB, można podzielić tabel źródłowych w pionie na kilka małych sieci, gdy największy rozmiar wiersza dla każdego z nich nie przekracza limit.</span><span class="sxs-lookup"><span data-stu-id="594a1-296">If you have source data with rows of size greater than 1 MB, you may want to split the source tables vertically into several small ones where the largest row size of each of them does not exceed the limit.</span></span> <span data-ttu-id="594a1-297">Mniejsze tabele następnie można załadować przy użyciu programu PolyBase i scalane w usłudze Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="594a1-297">The smaller tables can then be loaded using PolyBase and merged together in Azure SQL Data Warehouse.</span></span>

### <a name="sql-data-warehouse-resource-class"></a><span data-ttu-id="594a1-298">Klasa zasobów magazynu danych SQL</span><span class="sxs-lookup"><span data-stu-id="594a1-298">SQL Data Warehouse resource class</span></span>
<span data-ttu-id="594a1-299">Aby uzyskać najlepsze możliwe przepływności, należy wziąć pod uwagę można przypisać większą klasa zasobów do użytkownika używane do ładowania danych do usługi SQL Data Warehouse przy użyciu programu PolyBase.</span><span class="sxs-lookup"><span data-stu-id="594a1-299">To achieve best possible throughput, consider to assign larger resource class to the user being used to load data into SQL Data Warehouse via PolyBase.</span></span> <span data-ttu-id="594a1-300">Dowiedz się, jak to zrobić, postępując [zmienić przykład klasy zasobów użytkownika](../sql-data-warehouse/sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).</span><span class="sxs-lookup"><span data-stu-id="594a1-300">Learn how to do that by following [Change a user resource class example](../sql-data-warehouse/sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).</span></span>

### <a name="tablename-in-azure-sql-data-warehouse"></a><span data-ttu-id="594a1-301">tableName w magazynie danych SQL Azure</span><span class="sxs-lookup"><span data-stu-id="594a1-301">tableName in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="594a1-302">Poniższa tabela zawiera przykłady dotyczące sposobu określania **tableName** właściwość w zestawie danych JSON dla różnych kombinacji nazwy schematu i tabeli.</span><span class="sxs-lookup"><span data-stu-id="594a1-302">The following table provides examples on how to specify the **tableName** property in dataset JSON for various combinations of schema and table name.</span></span>

| <span data-ttu-id="594a1-303">Schemat bazy danych</span><span class="sxs-lookup"><span data-stu-id="594a1-303">DB Schema</span></span> | <span data-ttu-id="594a1-304">Nazwa tabeli</span><span class="sxs-lookup"><span data-stu-id="594a1-304">Table name</span></span> | <span data-ttu-id="594a1-305">Właściwość tableName JSON</span><span class="sxs-lookup"><span data-stu-id="594a1-305">tableName JSON property</span></span> |
| --- | --- | --- |
| <span data-ttu-id="594a1-306">właściciel bazy danych</span><span class="sxs-lookup"><span data-stu-id="594a1-306">dbo</span></span> |<span data-ttu-id="594a1-307">MyTable</span><span class="sxs-lookup"><span data-stu-id="594a1-307">MyTable</span></span> |<span data-ttu-id="594a1-308">MyTable lub dbo. MyTable lub [dbo]. [MyTable]</span><span class="sxs-lookup"><span data-stu-id="594a1-308">MyTable or dbo.MyTable or [dbo].[MyTable]</span></span> |
| <span data-ttu-id="594a1-309">dbo1</span><span class="sxs-lookup"><span data-stu-id="594a1-309">dbo1</span></span> |<span data-ttu-id="594a1-310">MyTable</span><span class="sxs-lookup"><span data-stu-id="594a1-310">MyTable</span></span> |<span data-ttu-id="594a1-311">dbo1. MyTable lub [dbo1]. [MyTable]</span><span class="sxs-lookup"><span data-stu-id="594a1-311">dbo1.MyTable or [dbo1].[MyTable]</span></span> |
| <span data-ttu-id="594a1-312">właściciel bazy danych</span><span class="sxs-lookup"><span data-stu-id="594a1-312">dbo</span></span> |<span data-ttu-id="594a1-313">My.Table</span><span class="sxs-lookup"><span data-stu-id="594a1-313">My.Table</span></span> |<span data-ttu-id="594a1-314">[My.Table] lub [dbo]. [My.Table]</span><span class="sxs-lookup"><span data-stu-id="594a1-314">[My.Table] or [dbo].[My.Table]</span></span> |
| <span data-ttu-id="594a1-315">dbo1</span><span class="sxs-lookup"><span data-stu-id="594a1-315">dbo1</span></span> |<span data-ttu-id="594a1-316">My.Table</span><span class="sxs-lookup"><span data-stu-id="594a1-316">My.Table</span></span> |<span data-ttu-id="594a1-317">[dbo1]. [My.Table]</span><span class="sxs-lookup"><span data-stu-id="594a1-317">[dbo1].[My.Table]</span></span> |

<span data-ttu-id="594a1-318">Jeśli zostanie wyświetlony następujący błąd, może to być problem z wartość określona dla właściwości tableName.</span><span class="sxs-lookup"><span data-stu-id="594a1-318">If you see the following error, it could be an issue with the value you specified for the tableName property.</span></span> <span data-ttu-id="594a1-319">Poniższa tabela dla poprawne sposobu na określenie wartości dla właściwości tableName JSON.</span><span class="sxs-lookup"><span data-stu-id="594a1-319">See the table for the correct way to specify values for the tableName JSON property.</span></span>  

```
Type=System.Data.SqlClient.SqlException,Message=Invalid object name 'stg.Account_test'.,Source=.Net SqlClient Data Provider
```

### <a name="columns-with-default-values"></a><span data-ttu-id="594a1-320">Kolumn z wartościami domyślnymi</span><span class="sxs-lookup"><span data-stu-id="594a1-320">Columns with default values</span></span>
<span data-ttu-id="594a1-321">Obecnie funkcja PolyBase w fabryce danych akceptuje tylko taką samą liczbę kolumn w tabeli docelowej.</span><span class="sxs-lookup"><span data-stu-id="594a1-321">Currently, PolyBase feature in Data Factory only accepts the same number of columns as in the target table.</span></span> <span data-ttu-id="594a1-322">Przykład tabeli z kolumnami cztery i jeden z nich jest zdefiniowana z wartością domyślną.</span><span class="sxs-lookup"><span data-stu-id="594a1-322">Say, you have a table with four columns and one of them is defined with a default value.</span></span> <span data-ttu-id="594a1-323">Dane wejściowe nadal powinien zawierać cztery kolumny.</span><span class="sxs-lookup"><span data-stu-id="594a1-323">The input data should still contain four columns.</span></span> <span data-ttu-id="594a1-324">Udostępnia zestaw danych wejściowych 3 kolumny spowoduje uzyskanie błąd podobny do następującego:</span><span class="sxs-lookup"><span data-stu-id="594a1-324">Providing a 3-column input dataset would yield an error similar to the following message:</span></span>

```
All columns of the table must be specified in the INSERT BULK statement.
```
<span data-ttu-id="594a1-325">Wartość NULL jest specjalny rodzaj wartości domyślnej.</span><span class="sxs-lookup"><span data-stu-id="594a1-325">NULL value is a special form of default value.</span></span> <span data-ttu-id="594a1-326">W przypadku wartości Null kolumny danych wejściowych (w obiekcie blob) dla tej kolumny może być pusta (nie może być brakuje wejściowy zestaw danych).</span><span class="sxs-lookup"><span data-stu-id="594a1-326">If the column is nullable, the input data (in blob) for that column could be empty (cannot be missing from the input dataset).</span></span> <span data-ttu-id="594a1-327">Program PolyBase wstawia wartość NULL w przypadku ich w magazynie danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="594a1-327">PolyBase inserts NULL for them in the Azure SQL Data Warehouse.</span></span>  

## <a name="auto-table-creation"></a><span data-ttu-id="594a1-328">Automatyczne tworzenie tabeli</span><span class="sxs-lookup"><span data-stu-id="594a1-328">Auto table creation</span></span>
<span data-ttu-id="594a1-329">Jeśli używasz kreatora kopiowania, aby skopiować dane z serwera SQL lub bazy danych SQL Azure do usługi Azure SQL Data Warehouse, tabeli, która odpowiada tabela źródłowa nie istnieje w magazynie docelowym fabryki danych może automatycznie tworzyć tabeli w magazynie danych przy użyciu schematu tabeli źródłowej.</span><span class="sxs-lookup"><span data-stu-id="594a1-329">If you are using Copy Wizard to copy data from SQL Server or Azure SQL Database to Azure SQL Data Warehouse and the table that corresponds to the source table does not exist in the destination store, Data Factory can automatically create the table in the data warehouse by using the source table schema.</span></span>

<span data-ttu-id="594a1-330">Fabryka danych tworzy tabeli w magazynie docelowym o takiej samej nazwie tabeli w magazynie źródła danych.</span><span class="sxs-lookup"><span data-stu-id="594a1-330">Data Factory creates the table in the destination store with the same table name in the source data store.</span></span> <span data-ttu-id="594a1-331">Typy danych kolumn są wybierane w oparciu następujące mapowania typu.</span><span class="sxs-lookup"><span data-stu-id="594a1-331">The data types for columns are chosen based on the following type mapping.</span></span> <span data-ttu-id="594a1-332">W razie potrzeby wykonuje konwersje typów, aby rozwiązać wszelkie niezgodności między magazynami źródłowym i docelowym.</span><span class="sxs-lookup"><span data-stu-id="594a1-332">If needed, it performs type conversions to fix any incompatibilities between source and destination stores.</span></span> <span data-ttu-id="594a1-333">Używa okrężnego tabeli dystrybucji.</span><span class="sxs-lookup"><span data-stu-id="594a1-333">It also uses Round Robin table distribution.</span></span>

| <span data-ttu-id="594a1-334">Typ kolumny źródłowej bazy danych SQL</span><span class="sxs-lookup"><span data-stu-id="594a1-334">Source SQL Database column type</span></span> | <span data-ttu-id="594a1-335">Typ kolumny docelowej magazynu danych SQL (limit rozmiaru)</span><span class="sxs-lookup"><span data-stu-id="594a1-335">Destination SQL DW column type (size limitation)</span></span> |
| --- | --- |
| <span data-ttu-id="594a1-336">int</span><span class="sxs-lookup"><span data-stu-id="594a1-336">Int</span></span> | <span data-ttu-id="594a1-337">int</span><span class="sxs-lookup"><span data-stu-id="594a1-337">Int</span></span> |
| <span data-ttu-id="594a1-338">BigInt</span><span class="sxs-lookup"><span data-stu-id="594a1-338">BigInt</span></span> | <span data-ttu-id="594a1-339">BigInt</span><span class="sxs-lookup"><span data-stu-id="594a1-339">BigInt</span></span> |
| <span data-ttu-id="594a1-340">SmallInt</span><span class="sxs-lookup"><span data-stu-id="594a1-340">SmallInt</span></span> | <span data-ttu-id="594a1-341">SmallInt</span><span class="sxs-lookup"><span data-stu-id="594a1-341">SmallInt</span></span> |
| <span data-ttu-id="594a1-342">TinyInt</span><span class="sxs-lookup"><span data-stu-id="594a1-342">TinyInt</span></span> | <span data-ttu-id="594a1-343">TinyInt</span><span class="sxs-lookup"><span data-stu-id="594a1-343">TinyInt</span></span> |
| <span data-ttu-id="594a1-344">bitowe</span><span class="sxs-lookup"><span data-stu-id="594a1-344">Bit</span></span> | <span data-ttu-id="594a1-345">bitowe</span><span class="sxs-lookup"><span data-stu-id="594a1-345">Bit</span></span> |
| <span data-ttu-id="594a1-346">Decimal</span><span class="sxs-lookup"><span data-stu-id="594a1-346">Decimal</span></span> | <span data-ttu-id="594a1-347">Decimal</span><span class="sxs-lookup"><span data-stu-id="594a1-347">Decimal</span></span> |
| <span data-ttu-id="594a1-348">numeryczne</span><span class="sxs-lookup"><span data-stu-id="594a1-348">Numeric</span></span> | <span data-ttu-id="594a1-349">Decimal</span><span class="sxs-lookup"><span data-stu-id="594a1-349">Decimal</span></span> |
| <span data-ttu-id="594a1-350">Float</span><span class="sxs-lookup"><span data-stu-id="594a1-350">Float</span></span> | <span data-ttu-id="594a1-351">Float</span><span class="sxs-lookup"><span data-stu-id="594a1-351">Float</span></span> |
| <span data-ttu-id="594a1-352">oszczędność pieniędzy</span><span class="sxs-lookup"><span data-stu-id="594a1-352">Money</span></span> | <span data-ttu-id="594a1-353">oszczędność pieniędzy</span><span class="sxs-lookup"><span data-stu-id="594a1-353">Money</span></span> |
| <span data-ttu-id="594a1-354">Real</span><span class="sxs-lookup"><span data-stu-id="594a1-354">Real</span></span> | <span data-ttu-id="594a1-355">Real</span><span class="sxs-lookup"><span data-stu-id="594a1-355">Real</span></span> |
| <span data-ttu-id="594a1-356">SmallMoney</span><span class="sxs-lookup"><span data-stu-id="594a1-356">SmallMoney</span></span> | <span data-ttu-id="594a1-357">SmallMoney</span><span class="sxs-lookup"><span data-stu-id="594a1-357">SmallMoney</span></span> |
| <span data-ttu-id="594a1-358">Binarne</span><span class="sxs-lookup"><span data-stu-id="594a1-358">Binary</span></span> | <span data-ttu-id="594a1-359">Binarne</span><span class="sxs-lookup"><span data-stu-id="594a1-359">Binary</span></span> |
| <span data-ttu-id="594a1-360">varbinary</span><span class="sxs-lookup"><span data-stu-id="594a1-360">Varbinary</span></span> | <span data-ttu-id="594a1-361">Varbinary (maksymalnie 8000)</span><span class="sxs-lookup"><span data-stu-id="594a1-361">Varbinary (up to 8000)</span></span> |
| <span data-ttu-id="594a1-362">Date</span><span class="sxs-lookup"><span data-stu-id="594a1-362">Date</span></span> | <span data-ttu-id="594a1-363">Date</span><span class="sxs-lookup"><span data-stu-id="594a1-363">Date</span></span> |
| <span data-ttu-id="594a1-364">Data i godzina</span><span class="sxs-lookup"><span data-stu-id="594a1-364">DateTime</span></span> | <span data-ttu-id="594a1-365">Data i godzina</span><span class="sxs-lookup"><span data-stu-id="594a1-365">DateTime</span></span> |
| <span data-ttu-id="594a1-366">DateTime2</span><span class="sxs-lookup"><span data-stu-id="594a1-366">DateTime2</span></span> | <span data-ttu-id="594a1-367">DateTime2</span><span class="sxs-lookup"><span data-stu-id="594a1-367">DateTime2</span></span> |
| <span data-ttu-id="594a1-368">Time</span><span class="sxs-lookup"><span data-stu-id="594a1-368">Time</span></span> | <span data-ttu-id="594a1-369">Time</span><span class="sxs-lookup"><span data-stu-id="594a1-369">Time</span></span> |
| <span data-ttu-id="594a1-370">DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="594a1-370">DateTimeOffset</span></span> | <span data-ttu-id="594a1-371">DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="594a1-371">DateTimeOffset</span></span> |
| <span data-ttu-id="594a1-372">SmallDateTime</span><span class="sxs-lookup"><span data-stu-id="594a1-372">SmallDateTime</span></span> | <span data-ttu-id="594a1-373">SmallDateTime</span><span class="sxs-lookup"><span data-stu-id="594a1-373">SmallDateTime</span></span> |
| <span data-ttu-id="594a1-374">Tekst</span><span class="sxs-lookup"><span data-stu-id="594a1-374">Text</span></span> | <span data-ttu-id="594a1-375">Varchar (maksymalnie 8000)</span><span class="sxs-lookup"><span data-stu-id="594a1-375">Varchar (up to 8000)</span></span> |
| <span data-ttu-id="594a1-376">NText</span><span class="sxs-lookup"><span data-stu-id="594a1-376">NText</span></span> | <span data-ttu-id="594a1-377">NVarChar (maksymalnie 4000)</span><span class="sxs-lookup"><span data-stu-id="594a1-377">NVarChar (up to 4000)</span></span> |
| <span data-ttu-id="594a1-378">Image (Obraz)</span><span class="sxs-lookup"><span data-stu-id="594a1-378">Image</span></span> | <span data-ttu-id="594a1-379">VarBinary (maksymalnie 8000)</span><span class="sxs-lookup"><span data-stu-id="594a1-379">VarBinary (up to 8000)</span></span> |
| <span data-ttu-id="594a1-380">Unikatowy identyfikator</span><span class="sxs-lookup"><span data-stu-id="594a1-380">UniqueIdentifier</span></span> | <span data-ttu-id="594a1-381">Unikatowy identyfikator</span><span class="sxs-lookup"><span data-stu-id="594a1-381">UniqueIdentifier</span></span> |
| <span data-ttu-id="594a1-382">char</span><span class="sxs-lookup"><span data-stu-id="594a1-382">Char</span></span> | <span data-ttu-id="594a1-383">char</span><span class="sxs-lookup"><span data-stu-id="594a1-383">Char</span></span> |
| <span data-ttu-id="594a1-384">NChar</span><span class="sxs-lookup"><span data-stu-id="594a1-384">NChar</span></span> | <span data-ttu-id="594a1-385">NChar</span><span class="sxs-lookup"><span data-stu-id="594a1-385">NChar</span></span> |
| <span data-ttu-id="594a1-386">VarChar</span><span class="sxs-lookup"><span data-stu-id="594a1-386">VarChar</span></span> | <span data-ttu-id="594a1-387">VarChar (maksymalnie 8000)</span><span class="sxs-lookup"><span data-stu-id="594a1-387">VarChar (up to 8000)</span></span> |
| <span data-ttu-id="594a1-388">NVarChar</span><span class="sxs-lookup"><span data-stu-id="594a1-388">NVarChar</span></span> | <span data-ttu-id="594a1-389">NVarChar (maksymalnie 4000)</span><span class="sxs-lookup"><span data-stu-id="594a1-389">NVarChar (up to 4000)</span></span> |
| <span data-ttu-id="594a1-390">XML</span><span class="sxs-lookup"><span data-stu-id="594a1-390">Xml</span></span> | <span data-ttu-id="594a1-391">Varchar (maksymalnie 8000)</span><span class="sxs-lookup"><span data-stu-id="594a1-391">Varchar (up to 8000)</span></span> |

[!INCLUDE [data-factory-type-repeatability-for-sql-sources](../../includes/data-factory-type-repeatability-for-sql-sources.md)]

## <a name="type-mapping-for-azure-sql-data-warehouse"></a><span data-ttu-id="594a1-392">Mapowanie typu dla usługi Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="594a1-392">Type mapping for Azure SQL Data Warehouse</span></span>
<span data-ttu-id="594a1-393">Jak wspomniano w [działań przepływu danych](data-factory-data-movement-activities.md) artykułu, wykonuje działanie kopiowania automatyczne konwersje z typów źródła do zbiornika typów o następujące podejście krok 2:</span><span class="sxs-lookup"><span data-stu-id="594a1-393">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following 2-step approach:</span></span>

1. <span data-ttu-id="594a1-394">Konwertowanie typów natywnych źródła na typ architektury .NET</span><span class="sxs-lookup"><span data-stu-id="594a1-394">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="594a1-395">Konwertowanie na typ macierzysty ujścia typ architektury .NET</span><span class="sxs-lookup"><span data-stu-id="594a1-395">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="594a1-396">Podczas przenoszenia danych do i z usługi Azure SQL Data Warehouse, następujące mapowania są używane z typu SQL typ architektury .NET i na odwrót.</span><span class="sxs-lookup"><span data-stu-id="594a1-396">When moving data to & from Azure SQL Data Warehouse, the following mappings are used from SQL type to .NET type and vice versa.</span></span>

<span data-ttu-id="594a1-397">Mapowanie jest taka sama jak [mapowanie typu danych serwera SQL dla ADO.NET](https://msdn.microsoft.com/library/cc716729.aspx).</span><span class="sxs-lookup"><span data-stu-id="594a1-397">The mapping is same as the [SQL Server Data Type Mapping for ADO.NET](https://msdn.microsoft.com/library/cc716729.aspx).</span></span>

| <span data-ttu-id="594a1-398">Typ aparatu bazy danych programu SQL Server</span><span class="sxs-lookup"><span data-stu-id="594a1-398">SQL Server Database Engine type</span></span> | <span data-ttu-id="594a1-399">Typ programu .NET framework</span><span class="sxs-lookup"><span data-stu-id="594a1-399">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="594a1-400">bigint</span><span class="sxs-lookup"><span data-stu-id="594a1-400">bigint</span></span> |<span data-ttu-id="594a1-401">Int64</span><span class="sxs-lookup"><span data-stu-id="594a1-401">Int64</span></span> |
| <span data-ttu-id="594a1-402">Binarne</span><span class="sxs-lookup"><span data-stu-id="594a1-402">binary</span></span> |<span data-ttu-id="594a1-403">Byte]</span><span class="sxs-lookup"><span data-stu-id="594a1-403">Byte[]</span></span> |
| <span data-ttu-id="594a1-404">bitowe</span><span class="sxs-lookup"><span data-stu-id="594a1-404">bit</span></span> |<span data-ttu-id="594a1-405">Wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="594a1-405">Boolean</span></span> |
| <span data-ttu-id="594a1-406">char</span><span class="sxs-lookup"><span data-stu-id="594a1-406">char</span></span> |<span data-ttu-id="594a1-407">Ciąg, Char]</span><span class="sxs-lookup"><span data-stu-id="594a1-407">String, Char[]</span></span> |
| <span data-ttu-id="594a1-408">Data</span><span class="sxs-lookup"><span data-stu-id="594a1-408">date</span></span> |<span data-ttu-id="594a1-409">Data i godzina</span><span class="sxs-lookup"><span data-stu-id="594a1-409">DateTime</span></span> |
| <span data-ttu-id="594a1-410">Data i godzina</span><span class="sxs-lookup"><span data-stu-id="594a1-410">Datetime</span></span> |<span data-ttu-id="594a1-411">Data i godzina</span><span class="sxs-lookup"><span data-stu-id="594a1-411">DateTime</span></span> |
| <span data-ttu-id="594a1-412">datetime2</span><span class="sxs-lookup"><span data-stu-id="594a1-412">datetime2</span></span> |<span data-ttu-id="594a1-413">Data i godzina</span><span class="sxs-lookup"><span data-stu-id="594a1-413">DateTime</span></span> |
| <span data-ttu-id="594a1-414">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="594a1-414">Datetimeoffset</span></span> |<span data-ttu-id="594a1-415">DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="594a1-415">DateTimeOffset</span></span> |
| <span data-ttu-id="594a1-416">Decimal</span><span class="sxs-lookup"><span data-stu-id="594a1-416">Decimal</span></span> |<span data-ttu-id="594a1-417">Decimal</span><span class="sxs-lookup"><span data-stu-id="594a1-417">Decimal</span></span> |
| <span data-ttu-id="594a1-418">Atrybut FILESTREAM (varbinary(max))</span><span class="sxs-lookup"><span data-stu-id="594a1-418">FILESTREAM attribute (varbinary(max))</span></span> |<span data-ttu-id="594a1-419">Byte]</span><span class="sxs-lookup"><span data-stu-id="594a1-419">Byte[]</span></span> |
| <span data-ttu-id="594a1-420">Float</span><span class="sxs-lookup"><span data-stu-id="594a1-420">Float</span></span> |<span data-ttu-id="594a1-421">O podwójnej precyzji</span><span class="sxs-lookup"><span data-stu-id="594a1-421">Double</span></span> |
| <span data-ttu-id="594a1-422">Obraz</span><span class="sxs-lookup"><span data-stu-id="594a1-422">image</span></span> |<span data-ttu-id="594a1-423">Byte]</span><span class="sxs-lookup"><span data-stu-id="594a1-423">Byte[]</span></span> |
| <span data-ttu-id="594a1-424">int</span><span class="sxs-lookup"><span data-stu-id="594a1-424">int</span></span> |<span data-ttu-id="594a1-425">Int32</span><span class="sxs-lookup"><span data-stu-id="594a1-425">Int32</span></span> |
| <span data-ttu-id="594a1-426">oszczędność pieniędzy</span><span class="sxs-lookup"><span data-stu-id="594a1-426">money</span></span> |<span data-ttu-id="594a1-427">Decimal</span><span class="sxs-lookup"><span data-stu-id="594a1-427">Decimal</span></span> |
| <span data-ttu-id="594a1-428">nchar</span><span class="sxs-lookup"><span data-stu-id="594a1-428">nchar</span></span> |<span data-ttu-id="594a1-429">Ciąg, Char]</span><span class="sxs-lookup"><span data-stu-id="594a1-429">String, Char[]</span></span> |
| <span data-ttu-id="594a1-430">ntext</span><span class="sxs-lookup"><span data-stu-id="594a1-430">ntext</span></span> |<span data-ttu-id="594a1-431">Ciąg, Char]</span><span class="sxs-lookup"><span data-stu-id="594a1-431">String, Char[]</span></span> |
| <span data-ttu-id="594a1-432">numeryczne</span><span class="sxs-lookup"><span data-stu-id="594a1-432">numeric</span></span> |<span data-ttu-id="594a1-433">Decimal</span><span class="sxs-lookup"><span data-stu-id="594a1-433">Decimal</span></span> |
| <span data-ttu-id="594a1-434">nvarchar</span><span class="sxs-lookup"><span data-stu-id="594a1-434">nvarchar</span></span> |<span data-ttu-id="594a1-435">Ciąg, Char]</span><span class="sxs-lookup"><span data-stu-id="594a1-435">String, Char[]</span></span> |
| <span data-ttu-id="594a1-436">rzeczywiste</span><span class="sxs-lookup"><span data-stu-id="594a1-436">real</span></span> |<span data-ttu-id="594a1-437">Pojedynczy</span><span class="sxs-lookup"><span data-stu-id="594a1-437">Single</span></span> |
| <span data-ttu-id="594a1-438">ROWVERSION</span><span class="sxs-lookup"><span data-stu-id="594a1-438">rowversion</span></span> |<span data-ttu-id="594a1-439">Byte]</span><span class="sxs-lookup"><span data-stu-id="594a1-439">Byte[]</span></span> |
| <span data-ttu-id="594a1-440">smalldatetime</span><span class="sxs-lookup"><span data-stu-id="594a1-440">smalldatetime</span></span> |<span data-ttu-id="594a1-441">Data i godzina</span><span class="sxs-lookup"><span data-stu-id="594a1-441">DateTime</span></span> |
| <span data-ttu-id="594a1-442">smallint</span><span class="sxs-lookup"><span data-stu-id="594a1-442">smallint</span></span> |<span data-ttu-id="594a1-443">Int16</span><span class="sxs-lookup"><span data-stu-id="594a1-443">Int16</span></span> |
| <span data-ttu-id="594a1-444">smallmoney</span><span class="sxs-lookup"><span data-stu-id="594a1-444">smallmoney</span></span> |<span data-ttu-id="594a1-445">Decimal</span><span class="sxs-lookup"><span data-stu-id="594a1-445">Decimal</span></span> |
| <span data-ttu-id="594a1-446">sql_variant</span><span class="sxs-lookup"><span data-stu-id="594a1-446">sql_variant</span></span> |<span data-ttu-id="594a1-447">Obiekt *</span><span class="sxs-lookup"><span data-stu-id="594a1-447">Object *</span></span> |
| <span data-ttu-id="594a1-448">Tekst</span><span class="sxs-lookup"><span data-stu-id="594a1-448">text</span></span> |<span data-ttu-id="594a1-449">Ciąg, Char]</span><span class="sxs-lookup"><span data-stu-id="594a1-449">String, Char[]</span></span> |
| <span data-ttu-id="594a1-450">time</span><span class="sxs-lookup"><span data-stu-id="594a1-450">time</span></span> |<span data-ttu-id="594a1-451">Zakres czasu</span><span class="sxs-lookup"><span data-stu-id="594a1-451">TimeSpan</span></span> |
| <span data-ttu-id="594a1-452">sygnatura czasowa</span><span class="sxs-lookup"><span data-stu-id="594a1-452">timestamp</span></span> |<span data-ttu-id="594a1-453">Byte]</span><span class="sxs-lookup"><span data-stu-id="594a1-453">Byte[]</span></span> |
| <span data-ttu-id="594a1-454">tinyint</span><span class="sxs-lookup"><span data-stu-id="594a1-454">tinyint</span></span> |<span data-ttu-id="594a1-455">Bajtów</span><span class="sxs-lookup"><span data-stu-id="594a1-455">Byte</span></span> |
| <span data-ttu-id="594a1-456">Unikatowy identyfikator</span><span class="sxs-lookup"><span data-stu-id="594a1-456">uniqueidentifier</span></span> |<span data-ttu-id="594a1-457">Identyfikator GUID</span><span class="sxs-lookup"><span data-stu-id="594a1-457">Guid</span></span> |
| <span data-ttu-id="594a1-458">varbinary</span><span class="sxs-lookup"><span data-stu-id="594a1-458">varbinary</span></span> |<span data-ttu-id="594a1-459">Byte]</span><span class="sxs-lookup"><span data-stu-id="594a1-459">Byte[]</span></span> |
| <span data-ttu-id="594a1-460">varchar</span><span class="sxs-lookup"><span data-stu-id="594a1-460">varchar</span></span> |<span data-ttu-id="594a1-461">Ciąg, Char]</span><span class="sxs-lookup"><span data-stu-id="594a1-461">String, Char[]</span></span> |
| <span data-ttu-id="594a1-462">xml</span><span class="sxs-lookup"><span data-stu-id="594a1-462">xml</span></span> |<span data-ttu-id="594a1-463">XML</span><span class="sxs-lookup"><span data-stu-id="594a1-463">Xml</span></span> |

<span data-ttu-id="594a1-464">Można również mapować kolumn z zestawu źródła danych do kolumn z zestawu danych zbiornika w definicji działania kopiowania.</span><span class="sxs-lookup"><span data-stu-id="594a1-464">You can also map columns from source dataset to columns from sink dataset in the copy activity definition.</span></span> <span data-ttu-id="594a1-465">Aby uzyskać więcej informacji, zobacz [mapowania kolumnach dataset w fabryce danych Azure](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="594a1-465">For details, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="json-examples-for-copying-data-to-and-from-sql-data-warehouse"></a><span data-ttu-id="594a1-466">Przykłady JSON do kopiowania danych z magazynu danych SQL</span><span class="sxs-lookup"><span data-stu-id="594a1-466">JSON examples for copying data to and from SQL Data Warehouse</span></span>
<span data-ttu-id="594a1-467">Poniższe przykłady zapewniają definicje JSON, których można utworzyć potok przy użyciu [portalu Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) lub [programu Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) lub [programu Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="594a1-467">The following examples provide sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="594a1-468">Przedstawiają sposób kopiowania danych do i z usługi Azure SQL Data Warehouse i magazynu obiektów Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="594a1-468">They show how to copy data to and from Azure SQL Data Warehouse and Azure Blob Storage.</span></span> <span data-ttu-id="594a1-469">Jednak dane mogą być kopiowane **bezpośrednio** z dowolnego źródła do dowolnego wychwytywanie podane [tutaj](data-factory-data-movement-activities.md#supported-data-stores-and-formats) za pomocą działania kopiowania w fabryce danych Azure.</span><span class="sxs-lookup"><span data-stu-id="594a1-469">However, data can be copied **directly** from any of sources to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>

### <a name="example-copy-data-from-azure-sql-data-warehouse-to-azure-blob"></a><span data-ttu-id="594a1-470">Przykład: Kopiowanie danych z magazynu danych SQL Azure do obiektów Blob platformy Azure</span><span class="sxs-lookup"><span data-stu-id="594a1-470">Example: Copy data from Azure SQL Data Warehouse to Azure Blob</span></span>
<span data-ttu-id="594a1-471">Przykład definiuje następujące jednostek fabryki danych:</span><span class="sxs-lookup"><span data-stu-id="594a1-471">The sample defines the following Data Factory entities:</span></span>

1. <span data-ttu-id="594a1-472">Połączonej usługi typu [AzureSqlDW](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="594a1-472">A linked service of type [AzureSqlDW](#linked-service-properties).</span></span>
2. <span data-ttu-id="594a1-473">Połączonej usługi typu [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="594a1-473">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="594a1-474">Dane wejściowe [dataset](data-factory-create-datasets.md) typu [AzureSqlDWTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="594a1-474">An input [dataset](data-factory-create-datasets.md) of type [AzureSqlDWTable](#dataset-properties).</span></span>
4. <span data-ttu-id="594a1-475">Dane wyjściowe [dataset](data-factory-create-datasets.md) typu [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="594a1-475">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="594a1-476">A [potoku](data-factory-create-pipelines.md) z działaniem kopii, która używa [SqlDWSource](#copy-activity-properties) i [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="594a1-476">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [SqlDWSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="594a1-477">Przykład kopiuje szeregów czasowych (co godzinę, codziennie, itp.) dane z tabeli w bazie danych Azure SQL Data Warehouse do obiektu blob co godzinę.</span><span class="sxs-lookup"><span data-stu-id="594a1-477">The sample copies time-series (hourly, daily, etc.) data from a table in Azure SQL Data Warehouse database to a blob every hour.</span></span> <span data-ttu-id="594a1-478">Właściwości JSON używane w te przykłady są opisane w sekcjach poniżej próbek.</span><span class="sxs-lookup"><span data-stu-id="594a1-478">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="594a1-479">**Usługa Azure SQL Data Warehouse połączonej usługi:**</span><span class="sxs-lookup"><span data-stu-id="594a1-479">**Azure SQL Data Warehouse linked service:**</span></span>

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
<span data-ttu-id="594a1-480">**Magazyn obiektów Blob Azure połączonej usługi:**</span><span class="sxs-lookup"><span data-stu-id="594a1-480">**Azure Blob storage linked service:**</span></span>

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
<span data-ttu-id="594a1-481">**Usługa Azure SQL Data Warehouse wejściowy zestaw danych:**</span><span class="sxs-lookup"><span data-stu-id="594a1-481">**Azure SQL Data Warehouse input dataset:**</span></span>

<span data-ttu-id="594a1-482">Przykładzie przyjęto założenie, utworzono tabelę "MyTable" w magazynie danych SQL Azure i zawiera kolumnę o nazwie "timestampcolumn" dla czasu serii danych.</span><span class="sxs-lookup"><span data-stu-id="594a1-482">The sample assumes you have created a table “MyTable” in Azure SQL Data Warehouse and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="594a1-483">Ustawienie "external": "prawda" informuje usługi fabryka danych czy zestaw danych jest zewnętrzne do fabryki danych i nie jest generowany przez działanie w fabryce danych.</span><span class="sxs-lookup"><span data-stu-id="594a1-483">Setting “external”: ”true” informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

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
<span data-ttu-id="594a1-484">**Azure Blob wyjściowy zestaw danych:**</span><span class="sxs-lookup"><span data-stu-id="594a1-484">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="594a1-485">Dane są zapisywane do nowego obiektu blob co godzinę (częstotliwość: godziny, interwał: 1).</span><span class="sxs-lookup"><span data-stu-id="594a1-485">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="594a1-486">Ścieżka folderu dla obiekt blob jest dynamicznie obliczane na podstawie czasu rozpoczęcia wycinek, który jest przetwarzana.</span><span class="sxs-lookup"><span data-stu-id="594a1-486">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="594a1-487">Ścieżka folderu używa rok, miesiąc, dzień i godziny części czas rozpoczęcia.</span><span class="sxs-lookup"><span data-stu-id="594a1-487">The folder path uses year, month, day, and hours parts of the start time.</span></span>

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

<span data-ttu-id="594a1-488">**Działanie kopiowania w potoku z SqlDWSource i BlobSink:**</span><span class="sxs-lookup"><span data-stu-id="594a1-488">**Copy activity in a pipeline with SqlDWSource and BlobSink:**</span></span>

<span data-ttu-id="594a1-489">Potok zawiera działanie kopiowania, który jest skonfigurowany do używania wejściowe i wyjściowe zestawy danych i jest zaplanowane co godzinę.</span><span class="sxs-lookup"><span data-stu-id="594a1-489">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="594a1-490">W definicji JSON potoku **źródła** ustawiono typ **SqlDWSource** i **zbiornika** ustawiono typ **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="594a1-490">In the pipeline JSON definition, the **source** type is set to **SqlDWSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="594a1-491">Określony dla zapytania SQL **SqlReaderQuery** właściwości wybiera dane w ostatniej godziny do skopiowania.</span><span class="sxs-lookup"><span data-stu-id="594a1-491">The SQL query specified for the **SqlReaderQuery** property selects the data in the past hour to copy.</span></span>

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
> <span data-ttu-id="594a1-492">W tym przykładzie **sqlReaderQuery** dla SqlDWSource został określony.</span><span class="sxs-lookup"><span data-stu-id="594a1-492">In the example, **sqlReaderQuery** is specified for the SqlDWSource.</span></span> <span data-ttu-id="594a1-493">Działanie kopiowania uruchamia to zapytanie względem źródła magazynu danych SQL Azure umożliwiają pobieranie danych.</span><span class="sxs-lookup"><span data-stu-id="594a1-493">The Copy Activity runs this query against the Azure SQL Data Warehouse source to get the data.</span></span>
>
> <span data-ttu-id="594a1-494">Można również określić procedury składowanej, podając **sqlReaderStoredProcedureName** i **storedProcedureParameters** (jeśli jest to procedura składowana pobiera parametry).</span><span class="sxs-lookup"><span data-stu-id="594a1-494">Alternatively, you can specify a stored procedure by specifying the **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if the stored procedure takes parameters).</span></span>
>
> <span data-ttu-id="594a1-495">Jeśli nie określisz sqlReaderQuery lub sqlReaderStoredProcedureName kolumny zdefiniowane w sekcji struktury zestawu danych JSON służą do skonstruowania zapytania (Wybierz Kolumna1, Kolumna2 z mytable) w celu uruchomienia usługi Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="594a1-495">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, the columns defined in the structure section of the dataset JSON are used to build a query (select column1, column2 from mytable) to run against the Azure SQL Data Warehouse.</span></span> <span data-ttu-id="594a1-496">Jeśli definicji zestawu danych nie ma on struktury, wszystkie kolumny są wybierane w tabeli.</span><span class="sxs-lookup"><span data-stu-id="594a1-496">If the dataset definition does not have the structure, all columns are selected from the table.</span></span>
>
>

### <a name="example-copy-data-from-azure-blob-to-azure-sql-data-warehouse"></a><span data-ttu-id="594a1-497">Przykład: Kopiowanie danych z obiektu Blob Azure do usługi Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="594a1-497">Example: Copy data from Azure Blob to Azure SQL Data Warehouse</span></span>
<span data-ttu-id="594a1-498">Przykład definiuje następujące jednostek fabryki danych:</span><span class="sxs-lookup"><span data-stu-id="594a1-498">The sample defines the following Data Factory entities:</span></span>

1. <span data-ttu-id="594a1-499">Połączonej usługi typu [AzureSqlDW](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="594a1-499">A linked service of type [AzureSqlDW](#linked-service-properties).</span></span>
2. <span data-ttu-id="594a1-500">Połączonej usługi typu [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="594a1-500">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="594a1-501">Dane wejściowe [dataset](data-factory-create-datasets.md) typu [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="594a1-501">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="594a1-502">Dane wyjściowe [dataset](data-factory-create-datasets.md) typu [AzureSqlDWTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="594a1-502">An output [dataset](data-factory-create-datasets.md) of type [AzureSqlDWTable](#dataset-properties).</span></span>
5. <span data-ttu-id="594a1-503">A [potoku](data-factory-create-pipelines.md) z działaniem kopii, która używa [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) i [SqlDWSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="594a1-503">A [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [SqlDWSink](#copy-activity-properties).</span></span>

<span data-ttu-id="594a1-504">Kopie próbki szeregów czasowych danych (co godzinę, codziennie, itp.) z platformy Azure blob do tabeli w usłudze Azure SQL Data Warehouse bazy danych co godzinę.</span><span class="sxs-lookup"><span data-stu-id="594a1-504">The sample copies time-series data (hourly, daily, etc.) from Azure blob to a table in Azure SQL Data Warehouse database every hour.</span></span> <span data-ttu-id="594a1-505">Właściwości JSON używane w te przykłady są opisane w sekcjach poniżej próbek.</span><span class="sxs-lookup"><span data-stu-id="594a1-505">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="594a1-506">**Usługa Azure SQL Data Warehouse połączonej usługi:**</span><span class="sxs-lookup"><span data-stu-id="594a1-506">**Azure SQL Data Warehouse linked service:**</span></span>

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
<span data-ttu-id="594a1-507">**Magazyn obiektów Blob Azure połączonej usługi:**</span><span class="sxs-lookup"><span data-stu-id="594a1-507">**Azure Blob storage linked service:**</span></span>

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
<span data-ttu-id="594a1-508">**Azure wejściowego zestawu danych obiektów Blob:**</span><span class="sxs-lookup"><span data-stu-id="594a1-508">**Azure Blob input dataset:**</span></span>

<span data-ttu-id="594a1-509">Dane są pobierane z nowego obiektu blob co godzinę (częstotliwość: godziny, interwał: 1).</span><span class="sxs-lookup"><span data-stu-id="594a1-509">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="594a1-510">Nazwa i ścieżka pliku folder dla obiektu blob dynamicznie są oceniane na podstawie czasu rozpoczęcia wycinek, który jest przetwarzana.</span><span class="sxs-lookup"><span data-stu-id="594a1-510">The folder path and file name for the blob are dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="594a1-511">Ścieżka folderu korzysta rok, miesiąc i dzień część czas rozpoczęcia, a nazwa pliku godzina część czas rozpoczęcia.</span><span class="sxs-lookup"><span data-stu-id="594a1-511">The folder path uses year, month, and day part of the start time and file name uses the hour part of the start time.</span></span> <span data-ttu-id="594a1-512">"external": ustawienie "prawda" usługi fabryka danych informuje, że w tej tabeli zewnętrznej dla fabryki danych i nie jest generowany przez działanie w fabryce danych.</span><span class="sxs-lookup"><span data-stu-id="594a1-512">“external”: “true” setting informs the Data Factory service that this table is external to the data factory and is not produced by an activity in the data factory.</span></span>

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
<span data-ttu-id="594a1-513">**Usługa Azure SQL Data Warehouse wyjściowy zestaw danych:**</span><span class="sxs-lookup"><span data-stu-id="594a1-513">**Azure SQL Data Warehouse output dataset:**</span></span>

<span data-ttu-id="594a1-514">Przykład kopiuje dane do tabeli o nazwie "MyTable" w usłudze Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="594a1-514">The sample copies data to a table named “MyTable” in Azure SQL Data Warehouse.</span></span> <span data-ttu-id="594a1-515">Tworzenie tabeli w magazynie danych SQL Azure z taką samą liczbę kolumn zgodnie z oczekiwaniami pliku Blob CSV zawiera.</span><span class="sxs-lookup"><span data-stu-id="594a1-515">Create the table in Azure SQL Data Warehouse with the same number of columns as you expect the Blob CSV file to contain.</span></span> <span data-ttu-id="594a1-516">Nowe wiersze są dodawane do tabeli co godzinę.</span><span class="sxs-lookup"><span data-stu-id="594a1-516">New rows are added to the table every hour.</span></span>

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
<span data-ttu-id="594a1-517">**Działanie kopiowania w potoku z BlobSource i SqlDWSink:**</span><span class="sxs-lookup"><span data-stu-id="594a1-517">**Copy activity in a pipeline with BlobSource and SqlDWSink:**</span></span>

<span data-ttu-id="594a1-518">Potok zawiera działanie kopiowania, który jest skonfigurowany do używania wejściowe i wyjściowe zestawy danych i jest zaplanowane co godzinę.</span><span class="sxs-lookup"><span data-stu-id="594a1-518">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="594a1-519">W definicji JSON potoku **źródła** ustawiono typ **BlobSource** i **zbiornika** ustawiono typ **SqlDWSink**.</span><span class="sxs-lookup"><span data-stu-id="594a1-519">In the pipeline JSON definition, the **source** type is set to **BlobSource** and **sink** type is set to **SqlDWSink**.</span></span>

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
<span data-ttu-id="594a1-520">Aby uzyskać wskazówki, zobacz zobacz [załadować 1 TB do usługi Azure SQL Data Warehouse z fabryką danych Azure w obszarze 15 minut](data-factory-load-sql-data-warehouse.md) i [ładowanie danych z fabryką danych Azure](../sql-data-warehouse/sql-data-warehouse-get-started-load-with-azure-data-factory.md) artykułu w dokumentacji usługi Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="594a1-520">For a walkthrough, see the see [Load 1 TB into Azure SQL Data Warehouse under 15 minutes with Azure Data Factory](data-factory-load-sql-data-warehouse.md) and [Load data with Azure Data Factory](../sql-data-warehouse/sql-data-warehouse-get-started-load-with-azure-data-factory.md) article in the Azure SQL Data Warehouse documentation.</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="594a1-521">Wydajność i dostrajania</span><span class="sxs-lookup"><span data-stu-id="594a1-521">Performance and Tuning</span></span>
<span data-ttu-id="594a1-522">Zobacz [wydajności działania kopiowania & dostrajanie przewodnik](data-factory-copy-activity-performance.md) Aby dowiedzieć się więcej o kluczowych czynników tego wydajność wpływ przenoszenia danych (działanie kopiowania) w usłudze fabryka danych Azure i zoptymalizować ją na różne sposoby.</span><span class="sxs-lookup"><span data-stu-id="594a1-522">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
