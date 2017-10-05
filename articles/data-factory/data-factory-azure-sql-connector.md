---
title: Kopiowanie danych do/z bazy danych SQL Azure | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak skopiować dane z bazy danych SQL Azure przy użyciu fabryki danych Azure."
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
ms.openlocfilehash: a64d13fa7dc5f50c259b98774be80b603dce400a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="copy-data-to-and-from-azure-sql-database-using-azure-data-factory"></a><span data-ttu-id="fa976-103">Kopiowanie danych do i z bazy danych SQL Azure przy użyciu fabryki danych Azure</span><span class="sxs-lookup"><span data-stu-id="fa976-103">Copy data to and from Azure SQL Database using Azure Data Factory</span></span>
<span data-ttu-id="fa976-104">W tym artykule opisano sposób używania działania kopiowania w fabryce danych Azure do przenoszenia danych do i z bazy danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="fa976-104">This article explains how to use the Copy Activity in Azure Data Factory to move data to and from Azure SQL Database.</span></span> <span data-ttu-id="fa976-105">Opiera się na [działań przepływu danych](data-factory-data-movement-activities.md) artykułu, który przedstawia ogólny przegląd przenoszenia danych z działania kopiowania.</span><span class="sxs-lookup"><span data-stu-id="fa976-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>  

## <a name="supported-scenarios"></a><span data-ttu-id="fa976-106">Obsługiwane scenariusze</span><span class="sxs-lookup"><span data-stu-id="fa976-106">Supported scenarios</span></span>
<span data-ttu-id="fa976-107">Dane należy skopiować **z bazy danych SQL Azure** do następujących danych przechowuje:</span><span class="sxs-lookup"><span data-stu-id="fa976-107">You can copy data **from Azure SQL Database** to the following data stores:</span></span>

[!INCLUDE [data-factory-supported-sinks](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="fa976-108">Możesz skopiować dane z następujących baz danych **bazą danych SQL Azure**:</span><span class="sxs-lookup"><span data-stu-id="fa976-108">You can copy data from the following data stores **to Azure SQL Database**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

## <a name="supported-authentication-type"></a><span data-ttu-id="fa976-109">Obsługiwany typ uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="fa976-109">Supported authentication type</span></span>
<span data-ttu-id="fa976-110">Łącznik bazy danych SQL Azure obsługuje uwierzytelnianie podstawowe.</span><span class="sxs-lookup"><span data-stu-id="fa976-110">Azure SQL Database connector supports basic authentication.</span></span>

## <a name="getting-started"></a><span data-ttu-id="fa976-111">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="fa976-111">Getting started</span></span>
<span data-ttu-id="fa976-112">Można utworzyć potoku o działanie kopiowania, który przenosi dane z bazy danych SQL Azure za pomocą różnych narzędzi/interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="fa976-112">You can create a pipeline with a copy activity that moves data to/from an Azure SQL Database by using different tools/APIs.</span></span>

<span data-ttu-id="fa976-113">Najprostszym sposobem, aby utworzyć potok jest użycie **kreatora kopiowania**.</span><span class="sxs-lookup"><span data-stu-id="fa976-113">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="fa976-114">Zobacz [samouczek: tworzenie potoku za pomocą Kreatora kopiowania](data-factory-copy-data-wizard-tutorial.md) szybkie przewodnik dotyczący tworzenia potoku za pomocą Kreatora kopiowania danych.</span><span class="sxs-lookup"><span data-stu-id="fa976-114">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="fa976-115">Umożliwia także następujące narzędzia do tworzenia potoku: **portalu Azure**, **programu Visual Studio**, **programu Azure PowerShell**, **szablonu usługi Azure Resource Manager**, **interfejs API .NET**, i **interfejsu API REST**.</span><span class="sxs-lookup"><span data-stu-id="fa976-115">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="fa976-116">Zobacz [samouczek działania kopiowania](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) instrukcje krok po kroku utworzyć potok z działaniem kopiowania.</span><span class="sxs-lookup"><span data-stu-id="fa976-116">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="fa976-117">Czy można użyć narzędzia i interfejsy API, należy wykonać następujące kroki, aby utworzyć potok, który przenosi dane z magazynu danych źródła do ujścia magazynu danych:</span><span class="sxs-lookup"><span data-stu-id="fa976-117">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span> 

1. <span data-ttu-id="fa976-118">Utwórz **fabryki danych**.</span><span class="sxs-lookup"><span data-stu-id="fa976-118">Create a **data factory**.</span></span> <span data-ttu-id="fa976-119">Fabryka danych może zawierać co najmniej jeden potoków.</span><span class="sxs-lookup"><span data-stu-id="fa976-119">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="fa976-120">Utwórz **połączone usługi** Aby połączyć dane wejściowe i wyjściowe są przechowywane w fabryce danych.</span><span class="sxs-lookup"><span data-stu-id="fa976-120">Create **linked services** to link input and output data stores to your data factory.</span></span> <span data-ttu-id="fa976-121">Na przykład jeśli kopiujesz danych z magazynu obiektów blob platformy Azure do bazy danych Azure SQL, Utwórz dwa połączone usługi, aby połączyć z kontem magazynu platformy Azure i bazą danych Azure SQL z fabryką danych.</span><span class="sxs-lookup"><span data-stu-id="fa976-121">For example, if you are copying data from an Azure blob storage to an Azure SQL database, you create two linked services to link your Azure storage account and Azure SQL database to your data factory.</span></span> <span data-ttu-id="fa976-122">Dla właściwości połączonej usługi, które są specyficzne dla bazy danych SQL Azure, zobacz [połączona usługa właściwości](#linked-service-properties) sekcji.</span><span class="sxs-lookup"><span data-stu-id="fa976-122">For linked service properties that are specific to Azure SQL Database, see [linked service properties](#linked-service-properties) section.</span></span> 
3. <span data-ttu-id="fa976-123">Utwórz **zestawów danych** do reprezentowania danych wejściowych i wyjściowych operacji kopiowania.</span><span class="sxs-lookup"><span data-stu-id="fa976-123">Create **datasets** to represent input and output data for the copy operation.</span></span> <span data-ttu-id="fa976-124">W tym przykładzie wymienionych w ostatnim kroku tworzenia zestawu danych, aby określić folder, który zawiera dane wejściowe i kontener obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="fa976-124">In the example mentioned in the last step, you create a dataset to specify the blob container and folder that contains the input data.</span></span> <span data-ttu-id="fa976-125">I Utwórz innego elementu dataset, aby określić tabeli SQL w bazie danych Azure SQL, która przechowuje dane skopiowane z magazynu obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="fa976-125">And, you create another dataset to specify the SQL table in the Azure SQL database  that holds the data copied from the blob storage.</span></span> <span data-ttu-id="fa976-126">Dla właściwości zestawu danych, które są specyficzne dla usługi Azure Data Lake Store, zobacz [właściwości zestawu danych](#dataset-properties) sekcji.</span><span class="sxs-lookup"><span data-stu-id="fa976-126">For dataset properties that are specific to Azure Data Lake Store, see [dataset properties](#dataset-properties) section.</span></span>
4. <span data-ttu-id="fa976-127">Utwórz **potoku** aktywnością kopiowania zestawu danych jako dane wejściowe i zestawu danych jako dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="fa976-127">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="fa976-128">W przykładzie wspomniano wcześniej używasz BlobSource jako źródło i SqlSink jako zbiorniku dla działania kopiowania.</span><span class="sxs-lookup"><span data-stu-id="fa976-128">In the example mentioned earlier, you use BlobSource as a source and SqlSink as a sink for the copy activity.</span></span> <span data-ttu-id="fa976-129">Podobnie baza danych SQL Azure są kopiowane do magazynu obiektów Blob Azure, należy użyć SqlSource i BlobSink w przypadku działania kopiowania.</span><span class="sxs-lookup"><span data-stu-id="fa976-129">Similarly, if you are copying from Azure SQL Database to Azure Blob Storage, you use SqlSource and BlobSink in the copy activity.</span></span> <span data-ttu-id="fa976-130">Dla właściwości działania kopiowania, które są specyficzne dla bazy danych SQL Azure, zobacz [skopiować właściwości działania](#copy-activity-properties) sekcji.</span><span class="sxs-lookup"><span data-stu-id="fa976-130">For copy activity properties that are specific to Azure SQL Database, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="fa976-131">Aby uzyskać szczegółowe informacje dotyczące sposobu używania magazynu danych jako źródło lub zbiorniku kliknij łącze w poprzedniej sekcji dla magazynu danych.</span><span class="sxs-lookup"><span data-stu-id="fa976-131">For details on how to use a data store as a source or a sink, click the link in the previous section for your data store.</span></span>

<span data-ttu-id="fa976-132">Korzystając z kreatora, definicje JSON do tych jednostek fabryki danych (połączone usługi, zestawy danych i potoki) są tworzone automatycznie dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="fa976-132">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="fa976-133">Korzystając z narzędzi/API (z wyjątkiem interfejs API .NET), należy zdefiniować tych jednostek fabryki danych w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="fa976-133">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="fa976-134">Aby uzyskać przykłady z definicji JSON dla jednostek fabryki danych, które są używane do kopiowania danych do/z bazy danych SQL Azure, zobacz [przykłady JSON](#json-examples-for-copying-data-to-and-from-sql-database) sekcji tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="fa976-134">For samples with JSON definitions for Data Factory entities that are used to copy data to/from an Azure SQL Database, see [JSON examples](#json-examples-for-copying-data-to-and-from-sql-database) section of this article.</span></span> 

<span data-ttu-id="fa976-135">Poniższe sekcje zawierają szczegółowe informacje o właściwości JSON, które są używane do definiowania jednostek fabryki danych określonej do bazy danych SQL Azure:</span><span class="sxs-lookup"><span data-stu-id="fa976-135">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Azure SQL Database:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="fa976-136">Połączona usługa właściwości</span><span class="sxs-lookup"><span data-stu-id="fa976-136">Linked service properties</span></span>
<span data-ttu-id="fa976-137">Azure SQL połączone usługi łączy bazy danych Azure SQL z fabryką danych.</span><span class="sxs-lookup"><span data-stu-id="fa976-137">An Azure SQL linked service links an Azure SQL database to your data factory.</span></span> <span data-ttu-id="fa976-138">Poniższa tabela zawiera opis specyficzne dla usługi Azure SQL połączone elementy JSON.</span><span class="sxs-lookup"><span data-stu-id="fa976-138">The following table provides description for JSON elements specific to Azure SQL linked service.</span></span>

| <span data-ttu-id="fa976-139">Właściwość</span><span class="sxs-lookup"><span data-stu-id="fa976-139">Property</span></span> | <span data-ttu-id="fa976-140">Opis</span><span class="sxs-lookup"><span data-stu-id="fa976-140">Description</span></span> | <span data-ttu-id="fa976-141">Wymagane</span><span class="sxs-lookup"><span data-stu-id="fa976-141">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="fa976-142">type</span><span class="sxs-lookup"><span data-stu-id="fa976-142">type</span></span> |<span data-ttu-id="fa976-143">Właściwość type musi mieć ustawioną: **AzureSqlDatabase**</span><span class="sxs-lookup"><span data-stu-id="fa976-143">The type property must be set to: **AzureSqlDatabase**</span></span> |<span data-ttu-id="fa976-144">Tak</span><span class="sxs-lookup"><span data-stu-id="fa976-144">Yes</span></span> |
| <span data-ttu-id="fa976-145">Parametry połączenia</span><span class="sxs-lookup"><span data-stu-id="fa976-145">connectionString</span></span> |<span data-ttu-id="fa976-146">Podaj informacje wymagane do połączenia z wystąpieniem bazy danych SQL Azure dla właściwości connectionString.</span><span class="sxs-lookup"><span data-stu-id="fa976-146">Specify information needed to connect to the Azure SQL Database instance for the connectionString property.</span></span> <span data-ttu-id="fa976-147">Obsługiwane jest tylko uwierzytelnianie podstawowe.</span><span class="sxs-lookup"><span data-stu-id="fa976-147">Only basic authentication is supported.</span></span> |<span data-ttu-id="fa976-148">Tak</span><span class="sxs-lookup"><span data-stu-id="fa976-148">Yes</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="fa976-149">Skonfiguruj [zapory bazy danych SQL Azure](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure) serwera bazy danych do [Zezwalaj usługom Azure na dostęp do serwera](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure).</span><span class="sxs-lookup"><span data-stu-id="fa976-149">Configure [Azure SQL Database Firewall](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure) the database server to [allow Azure Services to access the server](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure).</span></span> <span data-ttu-id="fa976-150">Ponadto jeśli kopiujesz danych do bazy danych SQL Azure z poza tym Azure z lokalnych źródeł danych z bramą fabryki danych, należy skonfigurować odpowiedni zakres adresów IP dla komputera, który wysyła dane do bazy danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="fa976-150">Additionally, if you are copying data to Azure SQL Database from outside Azure including from on-premises data sources with data factory gateway, configure appropriate IP address range for the machine that is sending data to Azure SQL Database.</span></span>

## <a name="dataset-properties"></a><span data-ttu-id="fa976-151">Właściwości zestawu danych</span><span class="sxs-lookup"><span data-stu-id="fa976-151">Dataset properties</span></span>
<span data-ttu-id="fa976-152">Aby określić zestaw danych do reprezentowania danych wejściowych lub wyjściowych w bazie danych Azure SQL, należy ustawić właściwość type zestawu danych do: **AzureSqlTable**.</span><span class="sxs-lookup"><span data-stu-id="fa976-152">To specify a dataset to represent input or output data in an Azure SQL database, you set the type property of the dataset to: **AzureSqlTable**.</span></span> <span data-ttu-id="fa976-153">Ustaw **linkedServiceName** właściwości zestawu danych do nazwy Azure SQL połączonej usługi.</span><span class="sxs-lookup"><span data-stu-id="fa976-153">Set the **linkedServiceName** property of the dataset to the name of the Azure SQL linked service.</span></span>  

<span data-ttu-id="fa976-154">Aby uzyskać pełną listę sekcje & właściwości dostępne do definiowania zestawów danych, zobacz [Tworzenie zbiorów danych](data-factory-create-datasets.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="fa976-154">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="fa976-155">Sekcje zawierają informacje, takie jak struktury, dostępności i zasad zestawu danych JSON są podobne dla wszystkich typów obiektów dataset (Azure SQL, obiektów blob platformy Azure, Azure tabeli itp.).</span><span class="sxs-lookup"><span data-stu-id="fa976-155">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="fa976-156">Sekcja typeProperties jest różne dla każdego typu zestawu danych i zawiera informacje o lokalizacji danych w magazynie danych.</span><span class="sxs-lookup"><span data-stu-id="fa976-156">The typeProperties section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="fa976-157">**TypeProperties** sekcja dla zestawu danych typu **AzureSqlTable** ma następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="fa976-157">The **typeProperties** section for the dataset of type **AzureSqlTable** has the following properties:</span></span>

| <span data-ttu-id="fa976-158">Właściwość</span><span class="sxs-lookup"><span data-stu-id="fa976-158">Property</span></span> | <span data-ttu-id="fa976-159">Opis</span><span class="sxs-lookup"><span data-stu-id="fa976-159">Description</span></span> | <span data-ttu-id="fa976-160">Wymagane</span><span class="sxs-lookup"><span data-stu-id="fa976-160">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="fa976-161">tableName</span><span class="sxs-lookup"><span data-stu-id="fa976-161">tableName</span></span> |<span data-ttu-id="fa976-162">Nazwa tabeli lub widoku w wystąpieniu bazy danych SQL Azure, odnoszący się do połączonej usługi.</span><span class="sxs-lookup"><span data-stu-id="fa976-162">Name of the table or view in the Azure SQL Database instance that linked service refers to.</span></span> |<span data-ttu-id="fa976-163">Tak</span><span class="sxs-lookup"><span data-stu-id="fa976-163">Yes</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="fa976-164">Właściwości działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="fa976-164">Copy activity properties</span></span>
<span data-ttu-id="fa976-165">Pełną listę sekcje & właściwości dostępne do definiowania działań, zobacz [tworzenie potoków](data-factory-create-pipelines.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="fa976-165">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="fa976-166">Właściwości, takie jak nazwa, opis, dane wejściowe i wyjściowe tabel i zasady są dostępne dla wszystkich typów działań.</span><span class="sxs-lookup"><span data-stu-id="fa976-166">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

> [!NOTE]
> <span data-ttu-id="fa976-167">Działanie kopiowania przyjmuje tylko jeden parametr wejściowy i tworzy tylko jedno wyjście.</span><span class="sxs-lookup"><span data-stu-id="fa976-167">The Copy Activity takes only one input and produces only one output.</span></span>

<span data-ttu-id="fa976-168">Właściwości dostępne w **typeProperties** sekcji działania zależne od każdego typu działania.</span><span class="sxs-lookup"><span data-stu-id="fa976-168">Whereas, properties available in the **typeProperties** section of the activity vary with each activity type.</span></span> <span data-ttu-id="fa976-169">Dla działania kopiowania różnią się w zależności od typów źródeł i sink.</span><span class="sxs-lookup"><span data-stu-id="fa976-169">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="fa976-170">Jeśli przenosisz dane z bazy danych Azure SQL, w przypadku działania kopiowania, aby ustawić typ źródła **SqlSource**.</span><span class="sxs-lookup"><span data-stu-id="fa976-170">If you are moving data from an Azure SQL database, you set the source type in the copy activity to **SqlSource**.</span></span> <span data-ttu-id="fa976-171">Podobnie jeśli przenosisz dane do bazy danych Azure SQL, należy ustawić typ ujścia w działanie kopiowania do **SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="fa976-171">Similarly, if you are moving data to an Azure SQL database, you set the sink type in the copy activity to **SqlSink**.</span></span> <span data-ttu-id="fa976-172">Ta sekcja zawiera listę obsługiwanych przez SqlSource i SqlSink właściwości.</span><span class="sxs-lookup"><span data-stu-id="fa976-172">This section provides a list of properties supported by SqlSource and SqlSink.</span></span>

### <a name="sqlsource"></a><span data-ttu-id="fa976-173">SqlSource</span><span class="sxs-lookup"><span data-stu-id="fa976-173">SqlSource</span></span>
<span data-ttu-id="fa976-174">W przypadku działania kopiowania, gdy źródłem jest typu **SqlSource**, są dostępne w następujących właściwości **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="fa976-174">In copy activity, when the source is of type **SqlSource**, the following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="fa976-175">Właściwość</span><span class="sxs-lookup"><span data-stu-id="fa976-175">Property</span></span> | <span data-ttu-id="fa976-176">Opis</span><span class="sxs-lookup"><span data-stu-id="fa976-176">Description</span></span> | <span data-ttu-id="fa976-177">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="fa976-177">Allowed values</span></span> | <span data-ttu-id="fa976-178">Wymagane</span><span class="sxs-lookup"><span data-stu-id="fa976-178">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="fa976-179">sqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="fa976-179">sqlReaderQuery</span></span> |<span data-ttu-id="fa976-180">Użyj niestandardowych zapytania można odczytać danych.</span><span class="sxs-lookup"><span data-stu-id="fa976-180">Use the custom query to read data.</span></span> |<span data-ttu-id="fa976-181">Ciąg zapytania SQL.</span><span class="sxs-lookup"><span data-stu-id="fa976-181">SQL query string.</span></span> <span data-ttu-id="fa976-182">Przykład: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="fa976-182">Example: `select * from MyTable`.</span></span> |<span data-ttu-id="fa976-183">Nie</span><span class="sxs-lookup"><span data-stu-id="fa976-183">No</span></span> |
| <span data-ttu-id="fa976-184">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="fa976-184">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="fa976-185">Nazwa procedury przechowywanej, która odczytuje dane z tabeli źródłowej.</span><span class="sxs-lookup"><span data-stu-id="fa976-185">Name of the stored procedure that reads data from the source table.</span></span> |<span data-ttu-id="fa976-186">Nazwa procedury składowanej.</span><span class="sxs-lookup"><span data-stu-id="fa976-186">Name of the stored procedure.</span></span> <span data-ttu-id="fa976-187">Ostatniej instrukcji SQL musi być instrukcji SELECT w procedurze składowanej.</span><span class="sxs-lookup"><span data-stu-id="fa976-187">The last SQL statement must be a SELECT statement in the stored procedure.</span></span> |<span data-ttu-id="fa976-188">Nie</span><span class="sxs-lookup"><span data-stu-id="fa976-188">No</span></span> |
| <span data-ttu-id="fa976-189">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="fa976-189">storedProcedureParameters</span></span> |<span data-ttu-id="fa976-190">Parametry dla procedury składowanej.</span><span class="sxs-lookup"><span data-stu-id="fa976-190">Parameters for the stored procedure.</span></span> |<span data-ttu-id="fa976-191">Par nazwa/wartość.</span><span class="sxs-lookup"><span data-stu-id="fa976-191">Name/value pairs.</span></span> <span data-ttu-id="fa976-192">Nazwy i wielkość liter w wyrazie parametry muszą być zgodne, nazwy i wielkość liter w wyrazie parametry procedury składowanej.</span><span class="sxs-lookup"><span data-stu-id="fa976-192">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> |<span data-ttu-id="fa976-193">Nie</span><span class="sxs-lookup"><span data-stu-id="fa976-193">No</span></span> |

<span data-ttu-id="fa976-194">Jeśli **sqlReaderQuery** określono dla SqlSource, odbywa się działanie kopii tego zapytania względem źródła bazy danych SQL Azure umożliwiają pobieranie danych.</span><span class="sxs-lookup"><span data-stu-id="fa976-194">If the **sqlReaderQuery** is specified for the SqlSource, the Copy Activity runs this query against the Azure SQL Database source to get the data.</span></span> <span data-ttu-id="fa976-195">Można również określić procedury składowanej, podając **sqlReaderStoredProcedureName** i **storedProcedureParameters** (jeśli jest to procedura składowana pobiera parametry).</span><span class="sxs-lookup"><span data-stu-id="fa976-195">Alternatively, you can specify a stored procedure by specifying the **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if the stored procedure takes parameters).</span></span>

<span data-ttu-id="fa976-196">Jeśli nie określisz sqlReaderQuery lub sqlReaderStoredProcedureName kolumny zdefiniowane w sekcji struktury zestawu danych JSON są używane w celu skonstruowania zapytania (`select column1, column2 from mytable`) w celu uruchomienia bazy danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="fa976-196">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, the columns defined in the structure section of the dataset JSON are used to build a query (`select column1, column2 from mytable`) to run against the Azure SQL Database.</span></span> <span data-ttu-id="fa976-197">Jeśli definicji zestawu danych nie ma on struktury, wszystkie kolumny są wybierane w tabeli.</span><span class="sxs-lookup"><span data-stu-id="fa976-197">If the dataset definition does not have the structure, all columns are selected from the table.</span></span>

> [!NOTE]
> <span data-ttu-id="fa976-198">Jeśli używasz **sqlReaderStoredProcedureName**, należy określić wartość dla **tableName** właściwość w zestawie danych JSON.</span><span class="sxs-lookup"><span data-stu-id="fa976-198">When you use **sqlReaderStoredProcedureName**, you still need to specify a value for the **tableName** property in the dataset JSON.</span></span> <span data-ttu-id="fa976-199">Nie ma żadnych operacji sprawdzania poprawności, jednak wykonywać na tej tabeli.</span><span class="sxs-lookup"><span data-stu-id="fa976-199">There are no validations performed against this table though.</span></span>
>
>

### <a name="sqlsource-example"></a><span data-ttu-id="fa976-200">Przykład SqlSource</span><span class="sxs-lookup"><span data-stu-id="fa976-200">SqlSource example</span></span>

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

<span data-ttu-id="fa976-201">**Definicja procedury składowanej:**</span><span class="sxs-lookup"><span data-stu-id="fa976-201">**The stored procedure definition:**</span></span>

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

### <a name="sqlsink"></a><span data-ttu-id="fa976-202">SqlSink</span><span class="sxs-lookup"><span data-stu-id="fa976-202">SqlSink</span></span>
<span data-ttu-id="fa976-203">**SqlSink** obsługuje następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="fa976-203">**SqlSink** supports the following properties:</span></span>

| <span data-ttu-id="fa976-204">Właściwość</span><span class="sxs-lookup"><span data-stu-id="fa976-204">Property</span></span> | <span data-ttu-id="fa976-205">Opis</span><span class="sxs-lookup"><span data-stu-id="fa976-205">Description</span></span> | <span data-ttu-id="fa976-206">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="fa976-206">Allowed values</span></span> | <span data-ttu-id="fa976-207">Wymagane</span><span class="sxs-lookup"><span data-stu-id="fa976-207">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="fa976-208">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="fa976-208">writeBatchTimeout</span></span> |<span data-ttu-id="fa976-209">Czas na ukończenie zanim upłynie limit czasu operacji wstawiania wsadowego oczekiwania.</span><span class="sxs-lookup"><span data-stu-id="fa976-209">Wait time for the batch insert operation to complete before it times out.</span></span> |<span data-ttu-id="fa976-210">Zakres czasu</span><span class="sxs-lookup"><span data-stu-id="fa976-210">timespan</span></span><br/><br/> <span data-ttu-id="fa976-211">Przykład: "00: 30:00" (30 minut).</span><span class="sxs-lookup"><span data-stu-id="fa976-211">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="fa976-212">Nie</span><span class="sxs-lookup"><span data-stu-id="fa976-212">No</span></span> |
| <span data-ttu-id="fa976-213">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="fa976-213">writeBatchSize</span></span> |<span data-ttu-id="fa976-214">Wstawia dane do tabeli SQL, gdy writeBatchSize osiągnie rozmiar buforu.</span><span class="sxs-lookup"><span data-stu-id="fa976-214">Inserts data into the SQL table when the buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="fa976-215">Liczba całkowita (liczba wierszy)</span><span class="sxs-lookup"><span data-stu-id="fa976-215">Integer (number of rows)</span></span> |<span data-ttu-id="fa976-216">Nie (domyślne: 10000)</span><span class="sxs-lookup"><span data-stu-id="fa976-216">No (default: 10000)</span></span> |
| <span data-ttu-id="fa976-217">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="fa976-217">sqlWriterCleanupScript</span></span> |<span data-ttu-id="fa976-218">Określ kwerendę dla działania kopiowania do wykonania w taki sposób, że dane określonych wycinek jest wyczyszczone.</span><span class="sxs-lookup"><span data-stu-id="fa976-218">Specify a query for Copy Activity to execute such that data of a specific slice is cleaned up.</span></span> <span data-ttu-id="fa976-219">Aby uzyskać więcej informacji, zobacz [powtarzalne kopiowania](#repeatable-copy).</span><span class="sxs-lookup"><span data-stu-id="fa976-219">For more information, see [repeatable copy](#repeatable-copy).</span></span> |<span data-ttu-id="fa976-220">Instrukcja zapytania.</span><span class="sxs-lookup"><span data-stu-id="fa976-220">A query statement.</span></span> |<span data-ttu-id="fa976-221">Nie</span><span class="sxs-lookup"><span data-stu-id="fa976-221">No</span></span> |
| <span data-ttu-id="fa976-222">sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="fa976-222">sliceIdentifierColumnName</span></span> |<span data-ttu-id="fa976-223">Określ nazwę kolumny dla aktywności kopiowania wypełnić automatycznie generowane wycinek identyfikator, który służy do oczyszczania danych określonego wycinek czas ponownego uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="fa976-223">Specify a column name for Copy Activity to fill with auto generated slice identifier, which is used to clean up data of a specific slice when rerun.</span></span> <span data-ttu-id="fa976-224">Aby uzyskać więcej informacji, zobacz [powtarzalne kopiowania](#repeatable-copy).</span><span class="sxs-lookup"><span data-stu-id="fa976-224">For more information, see [repeatable copy](#repeatable-copy).</span></span> |<span data-ttu-id="fa976-225">Nazwa kolumny kolumnę o typie danych binary(32).</span><span class="sxs-lookup"><span data-stu-id="fa976-225">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="fa976-226">Nie</span><span class="sxs-lookup"><span data-stu-id="fa976-226">No</span></span> |
| <span data-ttu-id="fa976-227">sqlWriterStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="fa976-227">sqlWriterStoredProcedureName</span></span> |<span data-ttu-id="fa976-228">Nazwa procedury składowanej danych upserts (aktualizacje/INSERT) do tabeli docelowej.</span><span class="sxs-lookup"><span data-stu-id="fa976-228">Name of the stored procedure that upserts (updates/inserts) data into the target table.</span></span> |<span data-ttu-id="fa976-229">Nazwa procedury składowanej.</span><span class="sxs-lookup"><span data-stu-id="fa976-229">Name of the stored procedure.</span></span> |<span data-ttu-id="fa976-230">Nie</span><span class="sxs-lookup"><span data-stu-id="fa976-230">No</span></span> |
| <span data-ttu-id="fa976-231">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="fa976-231">storedProcedureParameters</span></span> |<span data-ttu-id="fa976-232">Parametry dla procedury składowanej.</span><span class="sxs-lookup"><span data-stu-id="fa976-232">Parameters for the stored procedure.</span></span> |<span data-ttu-id="fa976-233">Par nazwa/wartość.</span><span class="sxs-lookup"><span data-stu-id="fa976-233">Name/value pairs.</span></span> <span data-ttu-id="fa976-234">Nazwy i wielkość liter w wyrazie parametry muszą być zgodne, nazwy i wielkość liter w wyrazie parametry procedury składowanej.</span><span class="sxs-lookup"><span data-stu-id="fa976-234">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> |<span data-ttu-id="fa976-235">Nie</span><span class="sxs-lookup"><span data-stu-id="fa976-235">No</span></span> |
| <span data-ttu-id="fa976-236">sqlWriterTableType</span><span class="sxs-lookup"><span data-stu-id="fa976-236">sqlWriterTableType</span></span> |<span data-ttu-id="fa976-237">Określ nazwę typu tabeli do użycia w procedurze składowanej.</span><span class="sxs-lookup"><span data-stu-id="fa976-237">Specify a table type name to be used in the stored procedure.</span></span> <span data-ttu-id="fa976-238">Działanie kopiowania udostępnia dane jest przenoszony w tabeli tymczasowej o tym typie tabeli.</span><span class="sxs-lookup"><span data-stu-id="fa976-238">Copy activity makes the data being moved available in a temp table with this table type.</span></span> <span data-ttu-id="fa976-239">Kod procedury składowanej można następnie scalić dane są kopiowane z istniejącymi danymi.</span><span class="sxs-lookup"><span data-stu-id="fa976-239">Stored procedure code can then merge the data being copied with existing data.</span></span> |<span data-ttu-id="fa976-240">Nazwa typu tabeli.</span><span class="sxs-lookup"><span data-stu-id="fa976-240">A table type name.</span></span> |<span data-ttu-id="fa976-241">Nie</span><span class="sxs-lookup"><span data-stu-id="fa976-241">No</span></span> |

#### <a name="sqlsink-example"></a><span data-ttu-id="fa976-242">Przykład SqlSink</span><span class="sxs-lookup"><span data-stu-id="fa976-242">SqlSink example</span></span>

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

## <a name="json-examples-for-copying-data-to-and-from-sql-database"></a><span data-ttu-id="fa976-243">Przykłady JSON do kopiowania danych z bazy danych SQL</span><span class="sxs-lookup"><span data-stu-id="fa976-243">JSON examples for copying data to and from SQL Database</span></span>
<span data-ttu-id="fa976-244">Poniższe przykłady zapewniają definicje JSON, których można utworzyć potok przy użyciu [portalu Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) lub [programu Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) lub [programu Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="fa976-244">The following examples provide sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="fa976-245">Przedstawiają sposób kopiowania danych do i z usługi Azure SQL Database oraz magazynu obiektów Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="fa976-245">They show how to copy data to and from Azure SQL Database and Azure Blob Storage.</span></span> <span data-ttu-id="fa976-246">Jednak dane mogą być kopiowane **bezpośrednio** z dowolnego źródła do dowolnego wychwytywanie podane [tutaj](data-factory-data-movement-activities.md#supported-data-stores-and-formats) za pomocą działania kopiowania w fabryce danych Azure.</span><span class="sxs-lookup"><span data-stu-id="fa976-246">However, data can be copied **directly** from any of sources to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>

### <a name="example-copy-data-from-azure-sql-database-to-azure-blob"></a><span data-ttu-id="fa976-247">Przykład: Kopiowanie danych z bazy danych SQL Azure do obiektów Blob platformy Azure</span><span class="sxs-lookup"><span data-stu-id="fa976-247">Example: Copy data from Azure SQL Database to Azure Blob</span></span>
<span data-ttu-id="fa976-248">Taki sam definiuje następujące jednostek fabryki danych:</span><span class="sxs-lookup"><span data-stu-id="fa976-248">The same defines the following Data Factory entities:</span></span>

1. <span data-ttu-id="fa976-249">Połączonej usługi typu [AzureSqlDatabase](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="fa976-249">A linked service of type [AzureSqlDatabase](#linked-service-properties).</span></span>
2. <span data-ttu-id="fa976-250">Połączonej usługi typu [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="fa976-250">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="fa976-251">Dane wejściowe [dataset](data-factory-create-datasets.md) typu [AzureSqlTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="fa976-251">An input [dataset](data-factory-create-datasets.md) of type [AzureSqlTable](#dataset-properties).</span></span>
4. <span data-ttu-id="fa976-252">Dane wyjściowe [dataset](data-factory-create-datasets.md) typu [obiektów Blob platformy Azure](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="fa976-252">An output [dataset](data-factory-create-datasets.md) of type [Azure Blob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="fa976-253">A [potoku](data-factory-create-pipelines.md) z działania kopiowania, która używa [SqlSource](#copy-activity-properties) i [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="fa976-253">A [pipeline](data-factory-create-pipelines.md) with a Copy activity that uses [SqlSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="fa976-254">Przykład kopiuje dane szeregów czasowych (co godzinę, codziennie, itp.) z tabeli w bazie danych Azure SQL do obiektu blob co godzinę.</span><span class="sxs-lookup"><span data-stu-id="fa976-254">The sample copies time-series data (hourly, daily, etc.) from a table in Azure SQL database to a blob every hour.</span></span> <span data-ttu-id="fa976-255">Właściwości JSON używane w te przykłady są opisane w sekcjach poniżej próbek.</span><span class="sxs-lookup"><span data-stu-id="fa976-255">The JSON properties used in these samples are described in sections following the samples.</span></span>  

<span data-ttu-id="fa976-256">**Baza danych SQL Azure połączonej usługi:**</span><span class="sxs-lookup"><span data-stu-id="fa976-256">**Azure SQL Database linked service:**</span></span>

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
<span data-ttu-id="fa976-257">Zobacz [połączoną usługę SQL Azure](#linked-service) sekcji listy właściwości obsługiwanych przez tej połączonej usługi.</span><span class="sxs-lookup"><span data-stu-id="fa976-257">See the [Azure SQL Linked Service](#linked-service) section for the list of properties supported by this linked service.</span></span>

<span data-ttu-id="fa976-258">**Magazyn obiektów Blob Azure połączonej usługi:**</span><span class="sxs-lookup"><span data-stu-id="fa976-258">**Azure Blob storage linked service:**</span></span>

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
<span data-ttu-id="fa976-259">Zobacz [obiektów Blob platformy Azure](data-factory-azure-blob-connector.md#azure-storage-linked-service) artykułu dla listy właściwości obsługiwanych przez tej połączonej usługi.</span><span class="sxs-lookup"><span data-stu-id="fa976-259">See the [Azure Blob](data-factory-azure-blob-connector.md#azure-storage-linked-service) article for the list of properties supported by this linked service.</span></span>


<span data-ttu-id="fa976-260">**Azure SQL wejściowy zestaw danych:**</span><span class="sxs-lookup"><span data-stu-id="fa976-260">**Azure SQL input dataset:**</span></span>

<span data-ttu-id="fa976-261">Przykład przyjęto założenie, utworzono tabelę "MyTable" w języku SQL Azure i zawiera kolumnę o nazwie "timestampcolumn" dla czasu serii danych.</span><span class="sxs-lookup"><span data-stu-id="fa976-261">The sample assumes you have created a table “MyTable” in Azure SQL and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="fa976-262">Ustawienie "external": "prawda" informuje usługi fabryka danych Azure czy zestaw danych jest zewnętrzne do fabryki danych i nie jest generowany przez działanie w fabryce danych.</span><span class="sxs-lookup"><span data-stu-id="fa976-262">Setting “external”: ”true” informs the Azure Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

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

<span data-ttu-id="fa976-263">Zobacz [właściwości typu zestawu danych Azure SQL](#dataset) sekcji listy właściwości obsługiwany przez dany typ zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="fa976-263">See the [Azure SQL dataset type properties](#dataset) section for the list of properties supported by this dataset type.</span></span>  

<span data-ttu-id="fa976-264">**Azure Blob wyjściowy zestaw danych:**</span><span class="sxs-lookup"><span data-stu-id="fa976-264">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="fa976-265">Dane są zapisywane do nowego obiektu blob co godzinę (częstotliwość: godziny, interwał: 1).</span><span class="sxs-lookup"><span data-stu-id="fa976-265">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="fa976-266">Ścieżka folderu dla obiekt blob jest dynamicznie obliczane na podstawie czasu rozpoczęcia wycinek, który jest przetwarzana.</span><span class="sxs-lookup"><span data-stu-id="fa976-266">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="fa976-267">Ścieżka folderu używa rok, miesiąc, dzień i godziny części czas rozpoczęcia.</span><span class="sxs-lookup"><span data-stu-id="fa976-267">The folder path uses year, month, day, and hours parts of the start time.</span></span>

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
<span data-ttu-id="fa976-268">Zobacz [właściwości typu zestawu danych obiektów Blob platformy Azure](data-factory-azure-blob-connector.md#dataset-properties) sekcji listy właściwości obsługiwany przez dany typ zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="fa976-268">See the [Azure Blob dataset type properties](data-factory-azure-blob-connector.md#dataset-properties) section for the list of properties supported by this dataset type.</span></span>  

<span data-ttu-id="fa976-269">**Działanie kopiowania w potoku z SQL źródłowy i odbiorczy obiektów Blob:**</span><span class="sxs-lookup"><span data-stu-id="fa976-269">**A copy activity in a pipeline with SQL source and Blob sink:**</span></span>

<span data-ttu-id="fa976-270">Potok zawiera działanie kopiowania, który jest skonfigurowany do używania wejściowe i wyjściowe zestawy danych i jest zaplanowane co godzinę.</span><span class="sxs-lookup"><span data-stu-id="fa976-270">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="fa976-271">W definicji JSON potoku **źródła** ustawiono typ **SqlSource** i **zbiornika** ustawiono typ **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="fa976-271">In the pipeline JSON definition, the **source** type is set to **SqlSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="fa976-272">Określony dla zapytania SQL **SqlReaderQuery** właściwości wybiera dane w ostatniej godziny do skopiowania.</span><span class="sxs-lookup"><span data-stu-id="fa976-272">The SQL query specified for the **SqlReaderQuery** property selects the data in the past hour to copy.</span></span>

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
<span data-ttu-id="fa976-273">W tym przykładzie **sqlReaderQuery** dla SqlSource został określony.</span><span class="sxs-lookup"><span data-stu-id="fa976-273">In the example, **sqlReaderQuery** is specified for the SqlSource.</span></span> <span data-ttu-id="fa976-274">Działanie kopiowania jest uruchamiana ta kwerenda dla źródłowej bazy danych SQL Azure umożliwiają pobieranie danych.</span><span class="sxs-lookup"><span data-stu-id="fa976-274">The Copy Activity runs this query against the Azure SQL Database source to get the data.</span></span> <span data-ttu-id="fa976-275">Można również określić procedury składowanej, podając **sqlReaderStoredProcedureName** i **storedProcedureParameters** (jeśli jest to procedura składowana pobiera parametry).</span><span class="sxs-lookup"><span data-stu-id="fa976-275">Alternatively, you can specify a stored procedure by specifying the **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if the stored procedure takes parameters).</span></span>

<span data-ttu-id="fa976-276">Jeśli nie określisz sqlReaderQuery lub sqlReaderStoredProcedureName kolumny zdefiniowane w sekcji struktury zestawu danych JSON służą do skonstruowania zapytania do bazy danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="fa976-276">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, the columns defined in the structure section of the dataset JSON are used to build a query to run against the Azure SQL Database.</span></span> <span data-ttu-id="fa976-277">Na przykład: `select column1, column2 from mytable`.</span><span class="sxs-lookup"><span data-stu-id="fa976-277">For example: `select column1, column2 from mytable`.</span></span> <span data-ttu-id="fa976-278">Jeśli definicji zestawu danych nie ma on struktury, wszystkie kolumny są wybierane w tabeli.</span><span class="sxs-lookup"><span data-stu-id="fa976-278">If the dataset definition does not have the structure, all columns are selected from the table.</span></span>

<span data-ttu-id="fa976-279">Zobacz [źródła Sql](#sqlsource) sekcji i [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) listę obsługiwanych przez SqlSource i BlobSink właściwości.</span><span class="sxs-lookup"><span data-stu-id="fa976-279">See the [Sql Source](#sqlsource) section and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) for the list of properties supported by SqlSource and BlobSink.</span></span>

### <a name="example-copy-data-from-azure-blob-to-azure-sql-database"></a><span data-ttu-id="fa976-280">Przykład: Kopiowanie danych z obiektów Blob platformy Azure do bazy danych SQL Azure</span><span class="sxs-lookup"><span data-stu-id="fa976-280">Example: Copy data from Azure Blob to Azure SQL Database</span></span>
<span data-ttu-id="fa976-281">Przykład definiuje następujące jednostek fabryki danych:</span><span class="sxs-lookup"><span data-stu-id="fa976-281">The sample defines the following Data Factory entities:</span></span>  

1. <span data-ttu-id="fa976-282">Połączonej usługi typu [AzureSqlDatabase](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="fa976-282">A linked service of type [AzureSqlDatabase](#linked-service-properties).</span></span>
2. <span data-ttu-id="fa976-283">Połączonej usługi typu [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="fa976-283">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="fa976-284">Dane wejściowe [dataset](data-factory-create-datasets.md) typu [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="fa976-284">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="fa976-285">Dane wyjściowe [dataset](data-factory-create-datasets.md) typu [AzureSqlTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="fa976-285">An output [dataset](data-factory-create-datasets.md) of type [AzureSqlTable](#dataset-properties).</span></span>
5. <span data-ttu-id="fa976-286">A [potoku](data-factory-create-pipelines.md) z działaniem kopii, która używa [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) i [SqlSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="fa976-286">A [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [SqlSink](#copy-activity-properties).</span></span>

<span data-ttu-id="fa976-287">Kopie próbki szeregów czasowych danych (co godzinę, codziennie, itp.) z usługi Azure blob do tabeli w usłudze Azure SQL bazy danych co godzinę.</span><span class="sxs-lookup"><span data-stu-id="fa976-287">The sample copies time-series data (hourly, daily, etc.) from Azure blob to a table in Azure SQL database every hour.</span></span> <span data-ttu-id="fa976-288">Właściwości JSON używane w te przykłady są opisane w sekcjach poniżej próbek.</span><span class="sxs-lookup"><span data-stu-id="fa976-288">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="fa976-289">**Azure połączoną usługą SQL:**</span><span class="sxs-lookup"><span data-stu-id="fa976-289">**Azure SQL linked service:**</span></span>

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
<span data-ttu-id="fa976-290">Zobacz [połączoną usługę SQL Azure](#linked-service) sekcji listy właściwości obsługiwanych przez tej połączonej usługi.</span><span class="sxs-lookup"><span data-stu-id="fa976-290">See the [Azure SQL Linked Service](#linked-service) section for the list of properties supported by this linked service.</span></span>

<span data-ttu-id="fa976-291">**Magazyn obiektów Blob Azure połączonej usługi:**</span><span class="sxs-lookup"><span data-stu-id="fa976-291">**Azure Blob storage linked service:**</span></span>

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
<span data-ttu-id="fa976-292">Zobacz [obiektów Blob platformy Azure](data-factory-azure-blob-connector.md#azure-storage-linked-service) artykułu dla listy właściwości obsługiwanych przez tej połączonej usługi.</span><span class="sxs-lookup"><span data-stu-id="fa976-292">See the [Azure Blob](data-factory-azure-blob-connector.md#azure-storage-linked-service) article for the list of properties supported by this linked service.</span></span>


<span data-ttu-id="fa976-293">**Azure wejściowego zestawu danych obiektów Blob:**</span><span class="sxs-lookup"><span data-stu-id="fa976-293">**Azure Blob input dataset:**</span></span>

<span data-ttu-id="fa976-294">Dane są pobierane z nowego obiektu blob co godzinę (częstotliwość: godziny, interwał: 1).</span><span class="sxs-lookup"><span data-stu-id="fa976-294">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="fa976-295">Nazwa i ścieżka pliku folder dla obiektu blob dynamicznie są oceniane na podstawie czasu rozpoczęcia wycinek, który jest przetwarzana.</span><span class="sxs-lookup"><span data-stu-id="fa976-295">The folder path and file name for the blob are dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="fa976-296">Ścieżka folderu korzysta rok, miesiąc i dzień część czas rozpoczęcia, a nazwa pliku godzina część czas rozpoczęcia.</span><span class="sxs-lookup"><span data-stu-id="fa976-296">The folder path uses year, month, and day part of the start time and file name uses the hour part of the start time.</span></span> <span data-ttu-id="fa976-297">"external": ustawienie "prawda" usługi fabryka danych informuje, że w tej tabeli zewnętrznej dla fabryki danych i nie jest generowany przez działanie w fabryce danych.</span><span class="sxs-lookup"><span data-stu-id="fa976-297">“external”: “true” setting informs the Data Factory service that this table is external to the data factory and is not produced by an activity in the data factory.</span></span>

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
<span data-ttu-id="fa976-298">Zobacz [właściwości typu zestawu danych obiektów Blob platformy Azure](data-factory-azure-blob-connector.md#dataset-properties) sekcji listy właściwości obsługiwany przez dany typ zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="fa976-298">See the [Azure Blob dataset type properties](data-factory-azure-blob-connector.md#dataset-properties) section for the list of properties supported by this dataset type.</span></span>

<span data-ttu-id="fa976-299">**Baza danych SQL Azure wyjściowy zestaw danych:**</span><span class="sxs-lookup"><span data-stu-id="fa976-299">**Azure SQL Database output dataset:**</span></span>

<span data-ttu-id="fa976-300">Przykład kopiuje dane do tabeli o nazwie "MyTable" w języku SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="fa976-300">The sample copies data to a table named “MyTable” in Azure SQL.</span></span> <span data-ttu-id="fa976-301">Tworzenie tabeli SQL Azure z taką samą liczbę kolumn zgodnie z oczekiwaniami pliku Blob CSV zawiera.</span><span class="sxs-lookup"><span data-stu-id="fa976-301">Create the table in Azure SQL with the same number of columns as you expect the Blob CSV file to contain.</span></span> <span data-ttu-id="fa976-302">Nowe wiersze są dodawane do tabeli co godzinę.</span><span class="sxs-lookup"><span data-stu-id="fa976-302">New rows are added to the table every hour.</span></span>

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
<span data-ttu-id="fa976-303">Zobacz [właściwości typu zestawu danych Azure SQL](#dataset) sekcji listy właściwości obsługiwany przez dany typ zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="fa976-303">See the [Azure SQL dataset type properties](#dataset) section for the list of properties supported by this dataset type.</span></span>

<span data-ttu-id="fa976-304">**Działanie kopiowania w potoku z obiektu Blob, źródłowy i odbiorczy SQL:**</span><span class="sxs-lookup"><span data-stu-id="fa976-304">**A copy activity in a pipeline with Blob source and SQL sink:**</span></span>

<span data-ttu-id="fa976-305">Potok zawiera działanie kopiowania, który jest skonfigurowany do używania wejściowe i wyjściowe zestawy danych i jest zaplanowane co godzinę.</span><span class="sxs-lookup"><span data-stu-id="fa976-305">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="fa976-306">W definicji JSON potoku **źródła** ustawiono typ **BlobSource** i **zbiornika** ustawiono typ **SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="fa976-306">In the pipeline JSON definition, the **source** type is set to **BlobSource** and **sink** type is set to **SqlSink**.</span></span>

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
<span data-ttu-id="fa976-307">Zobacz [zbiornika Sql](#sqlsink) sekcji i [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) listę obsługiwanych przez SqlSink i BlobSource właściwości.</span><span class="sxs-lookup"><span data-stu-id="fa976-307">See the [Sql Sink](#sqlsink) section and [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) for the list of properties supported by SqlSink and BlobSource.</span></span>

## <a name="identity-columns-in-the-target-database"></a><span data-ttu-id="fa976-308">Kolumny tożsamości w docelowej bazie danych</span><span class="sxs-lookup"><span data-stu-id="fa976-308">Identity columns in the target database</span></span>
<span data-ttu-id="fa976-309">Ta sekcja zawiera przykład kopiowanie danych z tabeli źródłowej bez kolumny tożsamości do tabeli docelowej z kolumny tożsamości.</span><span class="sxs-lookup"><span data-stu-id="fa976-309">This section provides an example for copying data from a source table without an identity column to a destination table with an identity column.</span></span>

<span data-ttu-id="fa976-310">**Tabela źródłowa:**</span><span class="sxs-lookup"><span data-stu-id="fa976-310">**Source table:**</span></span>

```SQL
create table dbo.SourceTbl
(
       name varchar(100),
       age int
)
```
<span data-ttu-id="fa976-311">**Tabela docelowa:**</span><span class="sxs-lookup"><span data-stu-id="fa976-311">**Destination table:**</span></span>

```SQL
create table dbo.TargetTbl
(
       identifier int identity(1,1),
       name varchar(100),
       age int
)
```
<span data-ttu-id="fa976-312">Zwróć uwagę, że tabela docelowa ma kolumny tożsamości.</span><span class="sxs-lookup"><span data-stu-id="fa976-312">Notice that the target table has an identity column.</span></span>

<span data-ttu-id="fa976-313">**Źródło zestawu danych JSON definicji**</span><span class="sxs-lookup"><span data-stu-id="fa976-313">**Source dataset JSON definition**</span></span>

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
<span data-ttu-id="fa976-314">**Docelowy zestaw danych JSON definicji**</span><span class="sxs-lookup"><span data-stu-id="fa976-314">**Destination dataset JSON definition**</span></span>

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

<span data-ttu-id="fa976-315">Należy zauważyć, że jako tabela źródłowa i docelowa mają różne schemat (element docelowy ma dodatkową kolumnę z tożsamością).</span><span class="sxs-lookup"><span data-stu-id="fa976-315">Notice that as your source and target table have different schema (target has an additional column with identity).</span></span> <span data-ttu-id="fa976-316">W tym scenariuszu, należy określić **struktury** właściwości w definicji zestawu danych docelowego, który nie zawiera kolumny tożsamości.</span><span class="sxs-lookup"><span data-stu-id="fa976-316">In this scenario, you need to specify **structure** property in the target dataset definition, which doesn’t include the identity column.</span></span>

## <a name="invoke-stored-procedure-from-sql-sink"></a><span data-ttu-id="fa976-317">Wywołaj procedurę składowaną z zbiornika SQL</span><span class="sxs-lookup"><span data-stu-id="fa976-317">Invoke stored procedure from SQL sink</span></span>
<span data-ttu-id="fa976-318">Na przykład wywoływania procedury składowanej z obiektu sink SQL w działaniu kopiowania potoku, zobacz [wywołaj procedurę składowaną dla obiekt sink SQL w przypadku działania kopiowania](data-factory-invoke-stored-procedure-from-copy-activity.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="fa976-318">For an example of invoking a stored procedure from SQL sink in a copy activity of a pipeline, see [Invoke stored procedure for SQL sink in copy activity](data-factory-invoke-stored-procedure-from-copy-activity.md) article.</span></span> 

## <a name="type-mapping-for-azure-sql-database"></a><span data-ttu-id="fa976-319">Mapowanie typu dla bazy danych SQL Azure</span><span class="sxs-lookup"><span data-stu-id="fa976-319">Type mapping for Azure SQL Database</span></span>
<span data-ttu-id="fa976-320">Jak wspomniano w [działań przepływu danych](data-factory-data-movement-activities.md) artykułu działanie kopiowania przeprowadza automatyczne konwersje z typów źródła do zbiornika typów o następujące podejście krok 2:</span><span class="sxs-lookup"><span data-stu-id="fa976-320">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article Copy activity performs automatic type conversions from source types to sink types with the following 2-step approach:</span></span>

1. <span data-ttu-id="fa976-321">Konwertowanie typów natywnych źródła na typ architektury .NET</span><span class="sxs-lookup"><span data-stu-id="fa976-321">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="fa976-322">Konwertowanie na typ macierzysty ujścia typ architektury .NET</span><span class="sxs-lookup"><span data-stu-id="fa976-322">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="fa976-323">Podczas przenoszenia danych do i z bazy danych SQL Azure, następujące mapowania są używane z typu SQL typ architektury .NET i na odwrót.</span><span class="sxs-lookup"><span data-stu-id="fa976-323">When moving data to and from Azure SQL Database, the following mappings are used from SQL type to .NET type and vice versa.</span></span> <span data-ttu-id="fa976-324">Mapowanie jest taka sama jak mapowanie typu danych serwera SQL dla ADO.NET.</span><span class="sxs-lookup"><span data-stu-id="fa976-324">The mapping is same as the SQL Server Data Type Mapping for ADO.NET.</span></span>

| <span data-ttu-id="fa976-325">Typ aparatu bazy danych programu SQL Server</span><span class="sxs-lookup"><span data-stu-id="fa976-325">SQL Server Database Engine type</span></span> | <span data-ttu-id="fa976-326">Typ programu .NET framework</span><span class="sxs-lookup"><span data-stu-id="fa976-326">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="fa976-327">bigint</span><span class="sxs-lookup"><span data-stu-id="fa976-327">bigint</span></span> |<span data-ttu-id="fa976-328">Int64</span><span class="sxs-lookup"><span data-stu-id="fa976-328">Int64</span></span> |
| <span data-ttu-id="fa976-329">Binarne</span><span class="sxs-lookup"><span data-stu-id="fa976-329">binary</span></span> |<span data-ttu-id="fa976-330">Byte]</span><span class="sxs-lookup"><span data-stu-id="fa976-330">Byte[]</span></span> |
| <span data-ttu-id="fa976-331">bitowe</span><span class="sxs-lookup"><span data-stu-id="fa976-331">bit</span></span> |<span data-ttu-id="fa976-332">Wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="fa976-332">Boolean</span></span> |
| <span data-ttu-id="fa976-333">char</span><span class="sxs-lookup"><span data-stu-id="fa976-333">char</span></span> |<span data-ttu-id="fa976-334">Ciąg, Char]</span><span class="sxs-lookup"><span data-stu-id="fa976-334">String, Char[]</span></span> |
| <span data-ttu-id="fa976-335">Data</span><span class="sxs-lookup"><span data-stu-id="fa976-335">date</span></span> |<span data-ttu-id="fa976-336">Data i godzina</span><span class="sxs-lookup"><span data-stu-id="fa976-336">DateTime</span></span> |
| <span data-ttu-id="fa976-337">Data i godzina</span><span class="sxs-lookup"><span data-stu-id="fa976-337">Datetime</span></span> |<span data-ttu-id="fa976-338">Data i godzina</span><span class="sxs-lookup"><span data-stu-id="fa976-338">DateTime</span></span> |
| <span data-ttu-id="fa976-339">datetime2</span><span class="sxs-lookup"><span data-stu-id="fa976-339">datetime2</span></span> |<span data-ttu-id="fa976-340">Data i godzina</span><span class="sxs-lookup"><span data-stu-id="fa976-340">DateTime</span></span> |
| <span data-ttu-id="fa976-341">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="fa976-341">Datetimeoffset</span></span> |<span data-ttu-id="fa976-342">DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="fa976-342">DateTimeOffset</span></span> |
| <span data-ttu-id="fa976-343">Decimal</span><span class="sxs-lookup"><span data-stu-id="fa976-343">Decimal</span></span> |<span data-ttu-id="fa976-344">Decimal</span><span class="sxs-lookup"><span data-stu-id="fa976-344">Decimal</span></span> |
| <span data-ttu-id="fa976-345">Atrybut FILESTREAM (varbinary(max))</span><span class="sxs-lookup"><span data-stu-id="fa976-345">FILESTREAM attribute (varbinary(max))</span></span> |<span data-ttu-id="fa976-346">Byte]</span><span class="sxs-lookup"><span data-stu-id="fa976-346">Byte[]</span></span> |
| <span data-ttu-id="fa976-347">Float</span><span class="sxs-lookup"><span data-stu-id="fa976-347">Float</span></span> |<span data-ttu-id="fa976-348">O podwójnej precyzji</span><span class="sxs-lookup"><span data-stu-id="fa976-348">Double</span></span> |
| <span data-ttu-id="fa976-349">Obraz</span><span class="sxs-lookup"><span data-stu-id="fa976-349">image</span></span> |<span data-ttu-id="fa976-350">Byte]</span><span class="sxs-lookup"><span data-stu-id="fa976-350">Byte[]</span></span> |
| <span data-ttu-id="fa976-351">int</span><span class="sxs-lookup"><span data-stu-id="fa976-351">int</span></span> |<span data-ttu-id="fa976-352">Int32</span><span class="sxs-lookup"><span data-stu-id="fa976-352">Int32</span></span> |
| <span data-ttu-id="fa976-353">oszczędność pieniędzy</span><span class="sxs-lookup"><span data-stu-id="fa976-353">money</span></span> |<span data-ttu-id="fa976-354">Decimal</span><span class="sxs-lookup"><span data-stu-id="fa976-354">Decimal</span></span> |
| <span data-ttu-id="fa976-355">nchar</span><span class="sxs-lookup"><span data-stu-id="fa976-355">nchar</span></span> |<span data-ttu-id="fa976-356">Ciąg, Char]</span><span class="sxs-lookup"><span data-stu-id="fa976-356">String, Char[]</span></span> |
| <span data-ttu-id="fa976-357">ntext</span><span class="sxs-lookup"><span data-stu-id="fa976-357">ntext</span></span> |<span data-ttu-id="fa976-358">Ciąg, Char]</span><span class="sxs-lookup"><span data-stu-id="fa976-358">String, Char[]</span></span> |
| <span data-ttu-id="fa976-359">numeryczne</span><span class="sxs-lookup"><span data-stu-id="fa976-359">numeric</span></span> |<span data-ttu-id="fa976-360">Decimal</span><span class="sxs-lookup"><span data-stu-id="fa976-360">Decimal</span></span> |
| <span data-ttu-id="fa976-361">nvarchar</span><span class="sxs-lookup"><span data-stu-id="fa976-361">nvarchar</span></span> |<span data-ttu-id="fa976-362">Ciąg, Char]</span><span class="sxs-lookup"><span data-stu-id="fa976-362">String, Char[]</span></span> |
| <span data-ttu-id="fa976-363">rzeczywiste</span><span class="sxs-lookup"><span data-stu-id="fa976-363">real</span></span> |<span data-ttu-id="fa976-364">Pojedynczy</span><span class="sxs-lookup"><span data-stu-id="fa976-364">Single</span></span> |
| <span data-ttu-id="fa976-365">ROWVERSION</span><span class="sxs-lookup"><span data-stu-id="fa976-365">rowversion</span></span> |<span data-ttu-id="fa976-366">Byte]</span><span class="sxs-lookup"><span data-stu-id="fa976-366">Byte[]</span></span> |
| <span data-ttu-id="fa976-367">smalldatetime</span><span class="sxs-lookup"><span data-stu-id="fa976-367">smalldatetime</span></span> |<span data-ttu-id="fa976-368">Data i godzina</span><span class="sxs-lookup"><span data-stu-id="fa976-368">DateTime</span></span> |
| <span data-ttu-id="fa976-369">smallint</span><span class="sxs-lookup"><span data-stu-id="fa976-369">smallint</span></span> |<span data-ttu-id="fa976-370">Int16</span><span class="sxs-lookup"><span data-stu-id="fa976-370">Int16</span></span> |
| <span data-ttu-id="fa976-371">smallmoney</span><span class="sxs-lookup"><span data-stu-id="fa976-371">smallmoney</span></span> |<span data-ttu-id="fa976-372">Decimal</span><span class="sxs-lookup"><span data-stu-id="fa976-372">Decimal</span></span> |
| <span data-ttu-id="fa976-373">sql_variant</span><span class="sxs-lookup"><span data-stu-id="fa976-373">sql_variant</span></span> |<span data-ttu-id="fa976-374">Obiekt *</span><span class="sxs-lookup"><span data-stu-id="fa976-374">Object *</span></span> |
| <span data-ttu-id="fa976-375">Tekst</span><span class="sxs-lookup"><span data-stu-id="fa976-375">text</span></span> |<span data-ttu-id="fa976-376">Ciąg, Char]</span><span class="sxs-lookup"><span data-stu-id="fa976-376">String, Char[]</span></span> |
| <span data-ttu-id="fa976-377">time</span><span class="sxs-lookup"><span data-stu-id="fa976-377">time</span></span> |<span data-ttu-id="fa976-378">Zakres czasu</span><span class="sxs-lookup"><span data-stu-id="fa976-378">TimeSpan</span></span> |
| <span data-ttu-id="fa976-379">sygnatura czasowa</span><span class="sxs-lookup"><span data-stu-id="fa976-379">timestamp</span></span> |<span data-ttu-id="fa976-380">Byte]</span><span class="sxs-lookup"><span data-stu-id="fa976-380">Byte[]</span></span> |
| <span data-ttu-id="fa976-381">tinyint</span><span class="sxs-lookup"><span data-stu-id="fa976-381">tinyint</span></span> |<span data-ttu-id="fa976-382">Bajtów</span><span class="sxs-lookup"><span data-stu-id="fa976-382">Byte</span></span> |
| <span data-ttu-id="fa976-383">Unikatowy identyfikator</span><span class="sxs-lookup"><span data-stu-id="fa976-383">uniqueidentifier</span></span> |<span data-ttu-id="fa976-384">Identyfikator GUID</span><span class="sxs-lookup"><span data-stu-id="fa976-384">Guid</span></span> |
| <span data-ttu-id="fa976-385">varbinary</span><span class="sxs-lookup"><span data-stu-id="fa976-385">varbinary</span></span> |<span data-ttu-id="fa976-386">Byte]</span><span class="sxs-lookup"><span data-stu-id="fa976-386">Byte[]</span></span> |
| <span data-ttu-id="fa976-387">varchar</span><span class="sxs-lookup"><span data-stu-id="fa976-387">varchar</span></span> |<span data-ttu-id="fa976-388">Ciąg, Char]</span><span class="sxs-lookup"><span data-stu-id="fa976-388">String, Char[]</span></span> |
| <span data-ttu-id="fa976-389">xml</span><span class="sxs-lookup"><span data-stu-id="fa976-389">xml</span></span> |<span data-ttu-id="fa976-390">XML</span><span class="sxs-lookup"><span data-stu-id="fa976-390">Xml</span></span> |

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="fa976-391">Obiekt sink kolumn mapy źródła</span><span class="sxs-lookup"><span data-stu-id="fa976-391">Map source to sink columns</span></span>
<span data-ttu-id="fa976-392">Aby uzyskać informacje dotyczące mapowania kolumn w zestawie źródła danych do kolumn w zestawie danych zbiornika, zobacz [mapowania kolumnach dataset w fabryce danych Azure](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="fa976-392">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-copy"></a><span data-ttu-id="fa976-393">Kopiuj powtarzalne</span><span class="sxs-lookup"><span data-stu-id="fa976-393">Repeatable copy</span></span>
<span data-ttu-id="fa976-394">Podczas kopiowania danych do bazy danych serwera SQL, działanie kopiowania dołącza dane do tabeli ujścia domyślnie.</span><span class="sxs-lookup"><span data-stu-id="fa976-394">When copying data to SQL Server Database, the copy activity appends data to the sink table by default.</span></span> <span data-ttu-id="fa976-395">Aby zamiast tego przeprowadzić UPSERT, zobacz [Repeatable zapisu SqlSink](data-factory-repeatable-copy.md#repeatable-write-to-sqlsink) artykułu.</span><span class="sxs-lookup"><span data-stu-id="fa976-395">To perform an UPSERT instead,  See [Repeatable write to SqlSink](data-factory-repeatable-copy.md#repeatable-write-to-sqlsink) article.</span></span> 

<span data-ttu-id="fa976-396">Podczas kopiowania danych z danych relacyjnych przechowuje, należy pamiętać, aby uniknąć niezamierzone wyniki powtarzalności.</span><span class="sxs-lookup"><span data-stu-id="fa976-396">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="fa976-397">Fabryka danych Azure możesz ponownie ręcznie wycinek.</span><span class="sxs-lookup"><span data-stu-id="fa976-397">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="fa976-398">Można również skonfigurować zasady ponawiania dla zestawu danych, aby wycinek jest uruchamiany ponownie, gdy wystąpi błąd.</span><span class="sxs-lookup"><span data-stu-id="fa976-398">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="fa976-399">Podczas wycinek zostanie uruchomiona ponownie w obu przypadkach, należy się upewnić, że te same dane jest do odczytu niezależnie od tego, ile razy wycinek jest uruchamiany.</span><span class="sxs-lookup"><span data-stu-id="fa976-399">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="fa976-400">Zobacz [Repeatable odczytywać źródłami relacyjnymi](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="fa976-400">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="fa976-401">Wydajność i dostrajania</span><span class="sxs-lookup"><span data-stu-id="fa976-401">Performance and Tuning</span></span>
<span data-ttu-id="fa976-402">Zobacz [wydajności działania kopiowania & dostrajanie przewodnik](data-factory-copy-activity-performance.md) Aby dowiedzieć się więcej o kluczowych czynników tego wydajność wpływ przenoszenia danych (działanie kopiowania) w usłudze fabryka danych Azure i zoptymalizować ją na różne sposoby.</span><span class="sxs-lookup"><span data-stu-id="fa976-402">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
