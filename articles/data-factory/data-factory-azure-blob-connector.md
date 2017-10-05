---
title: "Kopiowanie danych do/z magazynu obiektów Blob platformy Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak skopiować dane obiektów blob w fabryce danych Azure. Użyj naszej próbki: kopiowanie danych do i z magazynu obiektów Blob Azure i bazy danych SQL Azure."
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
ms.openlocfilehash: 2cf955b52010869a4e753c441e17bdd32fd2e63d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="copy-data-to-or-from-azure-blob-storage-using-azure-data-factory"></a><span data-ttu-id="2862d-105">Kopiowanie danych do i z magazynu obiektów Blob Azure przy użyciu fabryki danych Azure</span><span class="sxs-lookup"><span data-stu-id="2862d-105">Copy data to or from Azure Blob Storage using Azure Data Factory</span></span>
<span data-ttu-id="2862d-106">W tym artykule opisano sposób korzystania działanie kopiowania w fabryce danych Azure, aby skopiować dane do i z magazynu obiektów Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="2862d-106">This article explains how to use the Copy Activity in Azure Data Factory to copy data to and from Azure Blob Storage.</span></span> <span data-ttu-id="2862d-107">Opiera się na [działań przepływu danych](data-factory-data-movement-activities.md) artykułu, który przedstawia ogólny przegląd przenoszenia danych z działania kopiowania.</span><span class="sxs-lookup"><span data-stu-id="2862d-107">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

## <a name="overview"></a><span data-ttu-id="2862d-108">Omówienie</span><span class="sxs-lookup"><span data-stu-id="2862d-108">Overview</span></span>
<span data-ttu-id="2862d-109">Dane należy skopiować z dowolnego źródła obsługiwanych magazynu danych do magazynu obiektów Blob Azure lub z magazynu obiektów Blob Azure żadnych obsługiwanych ujścia magazynu danych.</span><span class="sxs-lookup"><span data-stu-id="2862d-109">You can copy data from any supported source data store to Azure Blob Storage or from Azure Blob Storage to any supported sink data store.</span></span> <span data-ttu-id="2862d-110">Poniższa tabela zawiera listę magazynów danych są obsługiwane jako źródła lub wychwytywanie przez działanie kopiowania.</span><span class="sxs-lookup"><span data-stu-id="2862d-110">The following table provides a list of data stores supported as sources or sinks by the copy activity.</span></span> <span data-ttu-id="2862d-111">Na przykład można przenieść dane **z** bazy danych programu SQL Server lub bazy danych Azure SQL **do** magazynu obiektów blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="2862d-111">For example, you can move data **from** a SQL Server database or an Azure SQL database **to** an Azure blob storage.</span></span> <span data-ttu-id="2862d-112">I dane należy skopiować **z** magazynu obiektów blob Azure **do** magazyn danych SQL Azure lub kolekcji usługi Azure DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="2862d-112">And, you can copy data **from** Azure blob storage **to** an Azure SQL Data Warehouse or an Azure Cosmos DB collection.</span></span> 

## <a name="supported-scenarios"></a><span data-ttu-id="2862d-113">Obsługiwane scenariusze</span><span class="sxs-lookup"><span data-stu-id="2862d-113">Supported scenarios</span></span>
<span data-ttu-id="2862d-114">Dane należy skopiować **z magazynu obiektów Blob Azure** do następujących danych przechowuje:</span><span class="sxs-lookup"><span data-stu-id="2862d-114">You can copy data **from Azure Blob Storage** to the following data stores:</span></span>

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="2862d-115">Możesz skopiować dane z następujących baz danych **do magazynu obiektów Blob Azure**:</span><span class="sxs-lookup"><span data-stu-id="2862d-115">You can copy data from the following data stores **to Azure Blob Storage**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]
 
> [!IMPORTANT]
> <span data-ttu-id="2862d-116">Działanie kopiowania obsługuje kopiowanie danych z/do ogólnego przeznaczenia kont usługi Azure Storage i magazynu obiektów Blob aktywny/Superpaska.</span><span class="sxs-lookup"><span data-stu-id="2862d-116">Copy Activity supports copying data from/to both general-purpose Azure Storage accounts and Hot/Cool Blob storage.</span></span> <span data-ttu-id="2862d-117">Działanie obsługuje **czytania z bloku, Dołącz lub stronicowe**, ale obsługuje **zapisywania tylko blokowe obiekty BLOB**.</span><span class="sxs-lookup"><span data-stu-id="2862d-117">The activity supports **reading from block, append, or page blobs**, but supports **writing to only block blobs**.</span></span> <span data-ttu-id="2862d-118">Usługa Azure Premium Storage nie jest obsługiwany jako zbiorniku, ponieważ nie jest obsługiwana przez stronicowych obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="2862d-118">Azure Premium Storage is not supported as a sink because it is backed by page blobs.</span></span>
> 
> <span data-ttu-id="2862d-119">Aktywność kopiowania nie powoduje usunięcia danych ze źródła, po dane pomyślnie są kopiowane do lokalizacji docelowej.</span><span class="sxs-lookup"><span data-stu-id="2862d-119">Copy Activity does not delete data from the source after the data is successfully copied to the destination.</span></span> <span data-ttu-id="2862d-120">Jeśli chcesz usunąć źródło danych po pomyślnym kopiowania, tworzenia [działania niestandardowego](data-factory-use-custom-activities.md) usunąć dane i użyć działania w potoku.</span><span class="sxs-lookup"><span data-stu-id="2862d-120">If you need to delete source data after a successful copy, create a [custom activity](data-factory-use-custom-activities.md) to delete the data and use the activity in the pipeline.</span></span> <span data-ttu-id="2862d-121">Na przykład zobacz [usuwania obiektów blob lub folderu przykładem w witrynie GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/DeleteBlobFileFolderCustomActivity).</span><span class="sxs-lookup"><span data-stu-id="2862d-121">For an example, see the [Delete blob or folder sample on GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/DeleteBlobFileFolderCustomActivity).</span></span> 

## <a name="get-started"></a><span data-ttu-id="2862d-122">Rozpoczęcie pracy</span><span class="sxs-lookup"><span data-stu-id="2862d-122">Get started</span></span>
<span data-ttu-id="2862d-123">Można utworzyć potoku o działanie kopiowania, który przenosi dane z magazynu obiektów Blob Azure przy użyciu różnych narzędzi/interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="2862d-123">You can create a pipeline with a copy activity that moves data to/from an Azure Blob Storage by using different tools/APIs.</span></span>

<span data-ttu-id="2862d-124">Najprostszym sposobem, aby utworzyć potok jest użycie **kreatora kopiowania**.</span><span class="sxs-lookup"><span data-stu-id="2862d-124">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="2862d-125">Ten artykuł zawiera [wskazówki](#walkthrough-use-copy-wizard-to-copy-data-tofrom-blob-storage) do tworzenia potoku można skopiować danych z lokalizacji magazynu obiektów Blob Azure do innej lokalizacji magazynu obiektów Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="2862d-125">This article has a [walkthrough](#walkthrough-use-copy-wizard-to-copy-data-tofrom-blob-storage) for creating a pipeline to copy data from an Azure Blob Storage location  to another Azure Blob Storage location.</span></span> <span data-ttu-id="2862d-126">Samouczek przedstawiający tworzenie potoku, aby skopiować dane z magazynu obiektów Blob Azure do bazy danych SQL Azure, zobacz [samouczek: tworzenie potoku za pomocą Kreatora kopiowania](data-factory-copy-data-wizard-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="2862d-126">For a tutorial on creating a pipeline to copy data from an Azure Blob Storage to Azure SQL Database, see [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md).</span></span>

<span data-ttu-id="2862d-127">Umożliwia także następujące narzędzia do tworzenia potoku: **portalu Azure**, **programu Visual Studio**, **programu Azure PowerShell**, **szablonu usługi Azure Resource Manager**, **interfejs API .NET**, i **interfejsu API REST**.</span><span class="sxs-lookup"><span data-stu-id="2862d-127">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="2862d-128">Zobacz [samouczek działania kopiowania](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) instrukcje krok po kroku utworzyć potok z działaniem kopiowania.</span><span class="sxs-lookup"><span data-stu-id="2862d-128">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span>

<span data-ttu-id="2862d-129">Czy można użyć narzędzia i interfejsy API, należy wykonać następujące kroki, aby utworzyć potok, który przenosi dane z magazynu danych źródła do ujścia magazynu danych:</span><span class="sxs-lookup"><span data-stu-id="2862d-129">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="2862d-130">Utwórz **fabryki danych**.</span><span class="sxs-lookup"><span data-stu-id="2862d-130">Create a **data factory**.</span></span> <span data-ttu-id="2862d-131">Fabryka danych może zawierać co najmniej jeden potoków.</span><span class="sxs-lookup"><span data-stu-id="2862d-131">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="2862d-132">Utwórz **połączone usługi** Aby połączyć dane wejściowe i wyjściowe są przechowywane w fabryce danych.</span><span class="sxs-lookup"><span data-stu-id="2862d-132">Create **linked services** to link input and output data stores to your data factory.</span></span> <span data-ttu-id="2862d-133">Na przykład jeśli kopiujesz danych z magazynu obiektów blob platformy Azure do bazy danych Azure SQL, Utwórz dwa połączone usługi, aby połączyć z kontem magazynu platformy Azure i bazą danych Azure SQL z fabryką danych.</span><span class="sxs-lookup"><span data-stu-id="2862d-133">For example, if you are copying data from an Azure blob storage to an Azure SQL database, you create two linked services to link your Azure storage account and Azure SQL database to your data factory.</span></span> <span data-ttu-id="2862d-134">Dla właściwości połączonej usługi, które są specyficzne dla usługi Azure Blob Storage, zobacz [połączona usługa właściwości](#linked-service-properties) sekcji.</span><span class="sxs-lookup"><span data-stu-id="2862d-134">For linked service properties that are specific to Azure Blob Storage, see [linked service properties](#linked-service-properties) section.</span></span> 
2. <span data-ttu-id="2862d-135">Utwórz **zestawów danych** do reprezentowania danych wejściowych i wyjściowych operacji kopiowania.</span><span class="sxs-lookup"><span data-stu-id="2862d-135">Create **datasets** to represent input and output data for the copy operation.</span></span> <span data-ttu-id="2862d-136">W tym przykładzie wymienionych w ostatnim kroku tworzenia zestawu danych, aby określić folder, który zawiera dane wejściowe i kontener obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="2862d-136">In the example mentioned in the last step, you create a dataset to specify the blob container and folder that contains the input data.</span></span> <span data-ttu-id="2862d-137">I Utwórz innego elementu dataset, aby określić tabeli SQL w bazie danych Azure SQL, która przechowuje dane skopiowane z magazynu obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="2862d-137">And, you create another dataset to specify the SQL table in the Azure SQL database that holds the data copied from the blob storage.</span></span> <span data-ttu-id="2862d-138">Dla właściwości zestawu danych, które są specyficzne dla usługi Azure Blob Storage, zobacz [właściwości zestawu danych](#dataset-properties) sekcji.</span><span class="sxs-lookup"><span data-stu-id="2862d-138">For dataset properties that are specific to Azure Blob Storage, see [dataset properties](#dataset-properties) section.</span></span>
3. <span data-ttu-id="2862d-139">Utwórz **potoku** aktywnością kopiowania zestawu danych jako dane wejściowe i zestawu danych jako dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="2862d-139">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="2862d-140">W przykładzie wspomniano wcześniej używasz BlobSource jako źródło i SqlSink jako zbiorniku dla działania kopiowania.</span><span class="sxs-lookup"><span data-stu-id="2862d-140">In the example mentioned earlier, you use BlobSource as a source and SqlSink as a sink for the copy activity.</span></span> <span data-ttu-id="2862d-141">Podobnie baza danych SQL Azure są kopiowane do magazynu obiektów Blob Azure, należy użyć SqlSource i BlobSink w przypadku działania kopiowania.</span><span class="sxs-lookup"><span data-stu-id="2862d-141">Similarly, if you are copying from Azure SQL Database to Azure Blob Storage, you use SqlSource and BlobSink in the copy activity.</span></span> <span data-ttu-id="2862d-142">Dla właściwości działania kopiowania, które są specyficzne dla usługi Azure Blob Storage, zobacz [skopiować właściwości działania](#copy-activity-properties) sekcji.</span><span class="sxs-lookup"><span data-stu-id="2862d-142">For copy activity properties that are specific to Azure Blob Storage, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="2862d-143">Aby uzyskać szczegółowe informacje dotyczące sposobu używania magazynu danych jako źródło lub zbiorniku kliknij łącze w poprzedniej sekcji dla magazynu danych.</span><span class="sxs-lookup"><span data-stu-id="2862d-143">For details on how to use a data store as a source or a sink, click the link in the previous section for your data store.</span></span>  

<span data-ttu-id="2862d-144">Korzystając z kreatora, definicje JSON do tych jednostek fabryki danych (połączone usługi, zestawy danych i potoki) są tworzone automatycznie dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="2862d-144">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="2862d-145">Korzystając z narzędzi/API (z wyjątkiem interfejs API .NET), należy zdefiniować tych jednostek fabryki danych w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="2862d-145">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="2862d-146">Aby uzyskać przykłady z definicji JSON dla jednostek fabryki danych, które są używane do kopiowania danych do/z magazynu obiektów Blob platformy Azure, zobacz [przykłady JSON](#json-examples-for-copying-data-to-and-from-blob-storage  ) sekcji tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="2862d-146">For samples with JSON definitions for Data Factory entities that are used to copy data to/from an Azure Blob Storage, see [JSON examples](#json-examples-for-copying-data-to-and-from-blob-storage  ) section of this article.</span></span>

<span data-ttu-id="2862d-147">Poniższe sekcje zawierają szczegółowe informacje o właściwości JSON, które są używane do definiowania jednostek fabryki danych określonej do magazynu obiektów Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="2862d-147">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Azure Blob Storage.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="2862d-148">Połączona usługa właściwości</span><span class="sxs-lookup"><span data-stu-id="2862d-148">Linked service properties</span></span>
<span data-ttu-id="2862d-149">Istnieją dwa typy połączonych usług używanego do łączenia usługi Azure Storage do fabryki danych Azure.</span><span class="sxs-lookup"><span data-stu-id="2862d-149">There are two types of linked services you can use to link an Azure Storage to an Azure data factory.</span></span> <span data-ttu-id="2862d-150">Są one: **AzureStorage** połączonej usługi i **element AzureStorageSas** połączonej usługi.</span><span class="sxs-lookup"><span data-stu-id="2862d-150">They are: **AzureStorage** linked service and **AzureStorageSas** linked service.</span></span> <span data-ttu-id="2862d-151">Połączoną usługą magazynu Azure zapewnia usłudze fabryka danych z globalnego dostępu do magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="2862d-151">The Azure Storage linked service provides the data factory with global access to the Azure Storage.</span></span> <span data-ttu-id="2862d-152">Związana SAS magazynu Azure (Shared Access Signature) usługa udostępnia fabryka danych z ograniczonej/czas-powiązane z dostępem do magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="2862d-152">Whereas, The Azure Storage SAS (Shared Access Signature) linked service provides the data factory with restricted/time-bound access to the Azure Storage.</span></span> <span data-ttu-id="2862d-153">Nie istnieją inne różnice między tych dwóch połączonych usług.</span><span class="sxs-lookup"><span data-stu-id="2862d-153">There are no other differences between these two linked services.</span></span> <span data-ttu-id="2862d-154">Wybierz połączonej usługi, która odpowiada Twoim potrzebom.</span><span class="sxs-lookup"><span data-stu-id="2862d-154">Choose the linked service that suits your needs.</span></span> <span data-ttu-id="2862d-155">Poniższe sekcje zawierają więcej szczegółowych informacji na temat tych dwóch usług połączonych.</span><span class="sxs-lookup"><span data-stu-id="2862d-155">The following sections provide more details on these two linked services.</span></span>

[!INCLUDE [data-factory-azure-storage-linked-services](../../includes/data-factory-azure-storage-linked-services.md)]

## <a name="dataset-properties"></a><span data-ttu-id="2862d-156">Właściwości zestawu danych</span><span class="sxs-lookup"><span data-stu-id="2862d-156">Dataset properties</span></span>
<span data-ttu-id="2862d-157">Aby określić zestaw danych do reprezentowania danych wejściowych lub wyjściowych w magazynie obiektów Blob Azure, należy ustawić właściwości type elementu dataset do: **AzureBlob**.</span><span class="sxs-lookup"><span data-stu-id="2862d-157">To specify a dataset to represent input or output data in an Azure Blob Storage, you set the type property of the dataset to: **AzureBlob**.</span></span> <span data-ttu-id="2862d-158">Ustaw **linkedServiceName** właściwości zestawu danych do nazwy usługi Azure Storage lub SAS magazynu Azure połączonej usługi.</span><span class="sxs-lookup"><span data-stu-id="2862d-158">Set the **linkedServiceName** property of the dataset to the name of the Azure Storage or Azure Storage SAS linked service.</span></span>  <span data-ttu-id="2862d-159">Określ typ właściwości zestawu danych **kontenera obiektów blob** i **folderu** w magazynie obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="2862d-159">The type properties of the dataset specify the **blob container** and the **folder** in the blob storage.</span></span>

<span data-ttu-id="2862d-160">Aby uzyskać pełną listę sekcje JSON & właściwości dostępne do definiowania zestawów danych, zobacz [Tworzenie zbiorów danych](data-factory-create-datasets.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="2862d-160">For a full list of JSON sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="2862d-161">Sekcje zawierają informacje, takie jak struktury, dostępności i zasad zestawu danych JSON są podobne dla wszystkich typów obiektów dataset (Azure SQL, obiektów blob platformy Azure, Azure tabeli itp.).</span><span class="sxs-lookup"><span data-stu-id="2862d-161">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="2862d-162">Fabryka danych obsługuje następujące wartości typu .NET zgodne ze specyfikacją CLS, na podstawie udostępnienie informacji o typie w "strukturę" dla źródeł danych schematu na odczytu obiektów blob platformy Azure: Int16, Int32, Int64, jeden, Double, Decimal, Byte [], Bool, String, Guid, Datetime, Datetimeoffset, Timespan.</span><span class="sxs-lookup"><span data-stu-id="2862d-162">Data factory supports the following CLS-compliant .NET based type values for providing type information in “structure” for schema-on-read data sources like Azure blob: Int16, Int32, Int64, Single, Double, Decimal, Byte[], Bool, String, Guid, Datetime, Datetimeoffset, Timespan.</span></span> <span data-ttu-id="2862d-163">Fabryka danych automatycznie wykonuje konwersje typów podczas przenoszenia danych z magazynu danych źródła do ujścia magazynu danych.</span><span class="sxs-lookup"><span data-stu-id="2862d-163">Data Factory automatically performs type conversions when moving data from a source data store to a sink data store.</span></span>

<span data-ttu-id="2862d-164">**TypeProperties** sekcja jest różne dla każdego typu zestawu danych i zawiera informacje o lokalizacji, itp., formatowania danych w magazynie danych.</span><span class="sxs-lookup"><span data-stu-id="2862d-164">The **typeProperties** section is different for each type of dataset and provides information about the location, format etc., of the data in the data store.</span></span> <span data-ttu-id="2862d-165">TypeProperties sekcja dla zestawu danych typu **AzureBlob** zestawu danych ma następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="2862d-165">The typeProperties section for dataset of type **AzureBlob** dataset has the following properties:</span></span>

| <span data-ttu-id="2862d-166">Właściwość</span><span class="sxs-lookup"><span data-stu-id="2862d-166">Property</span></span> | <span data-ttu-id="2862d-167">Opis</span><span class="sxs-lookup"><span data-stu-id="2862d-167">Description</span></span> | <span data-ttu-id="2862d-168">Wymagane</span><span class="sxs-lookup"><span data-stu-id="2862d-168">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2862d-169">folderPath</span><span class="sxs-lookup"><span data-stu-id="2862d-169">folderPath</span></span> |<span data-ttu-id="2862d-170">Ścieżka do kontenera i folderu w magazynie obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="2862d-170">Path to the container and folder in the blob storage.</span></span> <span data-ttu-id="2862d-171">Przykład: myblobcontainer\myblobfolder\\</span><span class="sxs-lookup"><span data-stu-id="2862d-171">Example: myblobcontainer\myblobfolder\\</span></span> |<span data-ttu-id="2862d-172">Tak</span><span class="sxs-lookup"><span data-stu-id="2862d-172">Yes</span></span> |
| <span data-ttu-id="2862d-173">fileName</span><span class="sxs-lookup"><span data-stu-id="2862d-173">fileName</span></span> |<span data-ttu-id="2862d-174">Nazwa obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="2862d-174">Name of the blob.</span></span> <span data-ttu-id="2862d-175">Nazwa pliku jest opcjonalna i z uwzględnieniem wielkości liter.</span><span class="sxs-lookup"><span data-stu-id="2862d-175">fileName is optional and case-sensitive.</span></span><br/><br/><span data-ttu-id="2862d-176">Jeśli określono nazwę pliku, działania (w tym kopiowania) działa na konkretnego obiektu Blob.</span><span class="sxs-lookup"><span data-stu-id="2862d-176">If you specify a filename, the activity (including Copy) works on the specific Blob.</span></span><br/><br/><span data-ttu-id="2862d-177">Jeśli nie określono nazwy pliku, kopiowania obejmuje wszystkie obiekty BLOB w ścieżce folderu dla zestawu danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="2862d-177">When fileName is not specified, Copy includes all Blobs in the folderPath for input dataset.</span></span><br/><br/><span data-ttu-id="2862d-178">Gdy **fileName** dla wyjściowego zestawu danych nie został określony i **preserveHierarchy** nie została określona w zbiornika działania nazwę wygenerowanego pliku będzie poniżej tego formatu: danych.<Guid>. txt (na przykład:: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="2862d-178">When **fileName** is not specified for an output dataset and **preserveHierarchy** is not specified in activity sink, the name of the generated file would be in the following this format: Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="2862d-179">Nie</span><span class="sxs-lookup"><span data-stu-id="2862d-179">No</span></span> |
| <span data-ttu-id="2862d-180">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="2862d-180">partitionedBy</span></span> |<span data-ttu-id="2862d-181">partitionedBy jest opcjonalna właściwość.</span><span class="sxs-lookup"><span data-stu-id="2862d-181">partitionedBy is an optional property.</span></span> <span data-ttu-id="2862d-182">Można go określić folderPath dynamiczne i nazwę pliku dla danych w serii. czas.</span><span class="sxs-lookup"><span data-stu-id="2862d-182">You can use it to specify a dynamic folderPath and filename for time series data.</span></span> <span data-ttu-id="2862d-183">Na przykład folderPath mogą nadać parametry dla każdej godziny danych.</span><span class="sxs-lookup"><span data-stu-id="2862d-183">For example, folderPath can be parameterized for every hour of data.</span></span> <span data-ttu-id="2862d-184">Zobacz [przy użyciu sekcji właściwości partitionedBy](#using-partitionedBy-property) szczegółowe informacje i przykłady.</span><span class="sxs-lookup"><span data-stu-id="2862d-184">See the [Using partitionedBy property section](#using-partitionedBy-property) for details and examples.</span></span> |<span data-ttu-id="2862d-185">Nie</span><span class="sxs-lookup"><span data-stu-id="2862d-185">No</span></span> |
| <span data-ttu-id="2862d-186">Format</span><span class="sxs-lookup"><span data-stu-id="2862d-186">format</span></span> | <span data-ttu-id="2862d-187">Obsługiwane są następujące typy format: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="2862d-187">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="2862d-188">Ustaw **typu** właściwości w formacie do jednej z tych wartości.</span><span class="sxs-lookup"><span data-stu-id="2862d-188">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="2862d-189">Aby uzyskać więcej informacji, zobacz [formacie tekstowym](data-factory-supported-file-and-compression-formats.md#text-format), [formatu Json](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), i [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sekcje.</span><span class="sxs-lookup"><span data-stu-id="2862d-189">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="2862d-190">Jeśli chcesz **skopiuj pliki jako — jest** między opartych na plikach magazynów (kopia binarnego), Pomiń sekcji format w obu definicji zestawu danych wejściowych i wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="2862d-190">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="2862d-191">Nie</span><span class="sxs-lookup"><span data-stu-id="2862d-191">No</span></span> |
| <span data-ttu-id="2862d-192">Kompresja</span><span class="sxs-lookup"><span data-stu-id="2862d-192">compression</span></span> | <span data-ttu-id="2862d-193">Określ typ i poziom kompresji danych.</span><span class="sxs-lookup"><span data-stu-id="2862d-193">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="2862d-194">Obsługiwane typy to: **GZip**, **Deflate**, **BZip2**, i **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="2862d-194">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="2862d-195">Obsługiwane poziomy: **optymalna** i **najszybciej**.</span><span class="sxs-lookup"><span data-stu-id="2862d-195">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="2862d-196">Aby uzyskać więcej informacji, zobacz [formaty plików i kompresji w fabryce danych Azure](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="2862d-196">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="2862d-197">Nie</span><span class="sxs-lookup"><span data-stu-id="2862d-197">No</span></span> |

### <a name="using-partitionedby-property"></a><span data-ttu-id="2862d-198">Za pomocą właściwości partitionedBy</span><span class="sxs-lookup"><span data-stu-id="2862d-198">Using partitionedBy property</span></span>
<span data-ttu-id="2862d-199">Jak wspomniano w poprzedniej sekcji, można określić folderPath dynamiczne i nazwę pliku dla czasu danych serii za pomocą **partitionedBy** właściwość [funkcje fabryki danych i zmienne systemu](data-factory-functions-variables.md).</span><span class="sxs-lookup"><span data-stu-id="2862d-199">As mentioned in the previous section, you can specify a dynamic folderPath and filename for time series data with the **partitionedBy** property, [Data Factory functions, and the system variables](data-factory-functions-variables.md).</span></span>

<span data-ttu-id="2862d-200">Aby uzyskać więcej informacji na zestawy danych serii czasu, planowanie i wycinków, zobacz [tworzenie zestawów danych](data-factory-create-datasets.md) i [planowanie i wykonanie](data-factory-scheduling-and-execution.md) artykułów.</span><span class="sxs-lookup"><span data-stu-id="2862d-200">For more information on time series datasets, scheduling, and slices, see [Creating Datasets](data-factory-create-datasets.md) and [Scheduling & Execution](data-factory-scheduling-and-execution.md) articles.</span></span>

#### <a name="sample-1"></a><span data-ttu-id="2862d-201">Przykład 1</span><span class="sxs-lookup"><span data-stu-id="2862d-201">Sample 1</span></span>

```json
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```

<span data-ttu-id="2862d-202">W tym przykładzie {wycinka} zostanie zastąpiony wartością zmiennej systemowej SliceStart fabryki danych w formacie (YYYYMMDDHH) określona.</span><span class="sxs-lookup"><span data-stu-id="2862d-202">In this example, {Slice} is replaced with the value of Data Factory system variable SliceStart in the format (YYYYMMDDHH) specified.</span></span> <span data-ttu-id="2862d-203">SliceStart odnosi się uruchomienie wycinka.</span><span class="sxs-lookup"><span data-stu-id="2862d-203">The SliceStart refers to start time of the slice.</span></span> <span data-ttu-id="2862d-204">Element folderPath jest różne dla każdego wycinka.</span><span class="sxs-lookup"><span data-stu-id="2862d-204">The folderPath is different for each slice.</span></span> <span data-ttu-id="2862d-205">Na przykład: wikidatagateway/wikisampledataout/2014100103 lub wikidatagateway/wikisampledataout/2014100104</span><span class="sxs-lookup"><span data-stu-id="2862d-205">For example: wikidatagateway/wikisampledataout/2014100103 or wikidatagateway/wikisampledataout/2014100104</span></span>

#### <a name="sample-2"></a><span data-ttu-id="2862d-206">Przykład 2</span><span class="sxs-lookup"><span data-stu-id="2862d-206">Sample 2</span></span>

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

<span data-ttu-id="2862d-207">W tym przykładzie rok, miesiąc, dzień i czas SliceStart są wyodrębniane do oddzielnych zmiennych, które są używane przez właściwości folderPath i nazwę pliku.</span><span class="sxs-lookup"><span data-stu-id="2862d-207">In this example, year, month, day, and time of SliceStart are extracted into separate variables that are used by folderPath and fileName properties.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="2862d-208">Właściwości działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="2862d-208">Copy activity properties</span></span>
<span data-ttu-id="2862d-209">Pełną listę sekcje & właściwości dostępne do definiowania działań, zobacz [tworzenie potoków](data-factory-create-pipelines.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="2862d-209">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="2862d-210">Właściwości, takie jak nazwa, opis, dane wejściowe i wyjściowe zestawy danych i zasady są dostępne dla wszystkich typów działań.</span><span class="sxs-lookup"><span data-stu-id="2862d-210">Properties such as name, description, input and output datasets, and policies are available for all types of activities.</span></span> <span data-ttu-id="2862d-211">Właściwości dostępne w **typeProperties** sekcji działania zależne od każdego typu działania.</span><span class="sxs-lookup"><span data-stu-id="2862d-211">Whereas, properties available in the **typeProperties** section of the activity vary with each activity type.</span></span> <span data-ttu-id="2862d-212">Dla działania kopiowania różnią się w zależności od typów źródeł i sink.</span><span class="sxs-lookup"><span data-stu-id="2862d-212">For Copy activity, they vary depending on the types of sources and sinks.</span></span> <span data-ttu-id="2862d-213">Jeśli przenosisz dane z magazynu obiektów Blob platformy Azure, w przypadku działania kopiowania, aby ustawić typ źródła **BlobSource**.</span><span class="sxs-lookup"><span data-stu-id="2862d-213">If you are moving data from an Azure Blob Storage, you set the source type in the copy activity to **BlobSource**.</span></span> <span data-ttu-id="2862d-214">Podobnie jeśli przenosisz dane do magazynu obiektów Blob Azure, należy ustawić typ ujścia w działanie kopiowania do **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="2862d-214">Similarly, if you are moving data to an Azure Blob Storage, you set the sink type in the copy activity to **BlobSink**.</span></span> <span data-ttu-id="2862d-215">Ta sekcja zawiera listę obsługiwanych przez BlobSource i BlobSink właściwości.</span><span class="sxs-lookup"><span data-stu-id="2862d-215">This section provides a list of properties supported by BlobSource and BlobSink.</span></span>

<span data-ttu-id="2862d-216">**BlobSource** obsługuje następujące właściwości w **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="2862d-216">**BlobSource** supports the following properties in the **typeProperties** section:</span></span>

| <span data-ttu-id="2862d-217">Właściwość</span><span class="sxs-lookup"><span data-stu-id="2862d-217">Property</span></span> | <span data-ttu-id="2862d-218">Opis</span><span class="sxs-lookup"><span data-stu-id="2862d-218">Description</span></span> | <span data-ttu-id="2862d-219">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="2862d-219">Allowed values</span></span> | <span data-ttu-id="2862d-220">Wymagane</span><span class="sxs-lookup"><span data-stu-id="2862d-220">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="2862d-221">Cykliczne</span><span class="sxs-lookup"><span data-stu-id="2862d-221">recursive</span></span> |<span data-ttu-id="2862d-222">Wskazuje, czy dane są odczytywane rekursywnie z folderów sub lub tylko określonego folderu.</span><span class="sxs-lookup"><span data-stu-id="2862d-222">Indicates whether the data is read recursively from the sub folders or only from the specified folder.</span></span> |<span data-ttu-id="2862d-223">TRUE, False (wartość domyślna)</span><span class="sxs-lookup"><span data-stu-id="2862d-223">True (default value), False</span></span> |<span data-ttu-id="2862d-224">Nie</span><span class="sxs-lookup"><span data-stu-id="2862d-224">No</span></span> |

<span data-ttu-id="2862d-225">**BlobSink** obsługuje następujące właściwości **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="2862d-225">**BlobSink** supports the following properties **typeProperties** section:</span></span>

| <span data-ttu-id="2862d-226">Właściwość</span><span class="sxs-lookup"><span data-stu-id="2862d-226">Property</span></span> | <span data-ttu-id="2862d-227">Opis</span><span class="sxs-lookup"><span data-stu-id="2862d-227">Description</span></span> | <span data-ttu-id="2862d-228">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="2862d-228">Allowed values</span></span> | <span data-ttu-id="2862d-229">Wymagane</span><span class="sxs-lookup"><span data-stu-id="2862d-229">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="2862d-230">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="2862d-230">copyBehavior</span></span> |<span data-ttu-id="2862d-231">Określa zachowanie kopiowania, gdy źródłem jest BlobSource lub systemu plików.</span><span class="sxs-lookup"><span data-stu-id="2862d-231">Defines the copy behavior when the source is BlobSource or FileSystem.</span></span> |<span data-ttu-id="2862d-232"><b>PreserveHierarchy</b>: zachowuje hierarchię plików w folderze docelowym.</span><span class="sxs-lookup"><span data-stu-id="2862d-232"><b>PreserveHierarchy</b>: preserves the file hierarchy in the target folder.</span></span> <span data-ttu-id="2862d-233">Względna ścieżka pliku źródłowego do folderu źródłowego jest taka sama jak ścieżka względna docelowego pliku do folderu docelowego.</span><span class="sxs-lookup"><span data-stu-id="2862d-233">The relative path of source file to source folder is identical to the relative path of target file to target folder.</span></span><br/><br/><span data-ttu-id="2862d-234"><b>FlattenHierarchy</b>: wszystkie pliki z folderu źródłowego znajdują się w pierwszym poziomem folderu docelowego.</span><span class="sxs-lookup"><span data-stu-id="2862d-234"><b>FlattenHierarchy</b>: all files from the source folder are in the first level of target folder.</span></span> <span data-ttu-id="2862d-235">Pliki docelowe mają automatycznie wygeneruje nazwę.</span><span class="sxs-lookup"><span data-stu-id="2862d-235">The target files have auto generated name.</span></span> <br/><br/><span data-ttu-id="2862d-236"><b>MergeFiles</b>: scala wszystkie pliki z folderu źródłowego do jednego pliku.</span><span class="sxs-lookup"><span data-stu-id="2862d-236"><b>MergeFiles</b>: merges all files from the source folder to one file.</span></span> <span data-ttu-id="2862d-237">Jeśli zostanie określona nazwa pliku/obiektów Blob, nazwa scalony plik jest określona nazwa; w przeciwnym razie będzie nazwa pliku wygenerowana automatycznie.</span><span class="sxs-lookup"><span data-stu-id="2862d-237">If the File/Blob Name is specified, the merged file name would be the specified name; otherwise, would be auto-generated file name.</span></span> |<span data-ttu-id="2862d-238">Nie</span><span class="sxs-lookup"><span data-stu-id="2862d-238">No</span></span> |

<span data-ttu-id="2862d-239">**BlobSource** obsługuje także te dwie właściwości dla zgodności z poprzednimi wersjami.</span><span class="sxs-lookup"><span data-stu-id="2862d-239">**BlobSource** also supports these two properties for backward compatibility.</span></span>

* <span data-ttu-id="2862d-240">**treatEmptyAsNull**: Określa, czy traktować null lub pusty ciąg jako wartość null.</span><span class="sxs-lookup"><span data-stu-id="2862d-240">**treatEmptyAsNull**: Specifies whether to treat null or empty string as null value.</span></span>
* <span data-ttu-id="2862d-241">**skipHeaderLineCount** — określa liczbę wierszy muszą pominięte.</span><span class="sxs-lookup"><span data-stu-id="2862d-241">**skipHeaderLineCount** - Specifies how many lines need be skipped.</span></span> <span data-ttu-id="2862d-242">Dotyczy tylko gdy wejściowy zestaw danych używa TextFormat.</span><span class="sxs-lookup"><span data-stu-id="2862d-242">It is applicable only when input dataset is using TextFormat.</span></span>

<span data-ttu-id="2862d-243">Podobnie **BlobSink** obsługuje następujące właściwości dla zgodności z poprzednimi wersjami.</span><span class="sxs-lookup"><span data-stu-id="2862d-243">Similarly, **BlobSink** supports the following property for backward compatibility.</span></span>

* <span data-ttu-id="2862d-244">**blobWriterAddHeader**: Określa, czy mają zostać dodane podczas zapisywania wyjściowy zestaw danych nagłówka definicje kolumn.</span><span class="sxs-lookup"><span data-stu-id="2862d-244">**blobWriterAddHeader**: Specifies whether to add a header of column definitions while writing to an output dataset.</span></span>

<span data-ttu-id="2862d-245">Zestawy danych obsługuje teraz następujące właściwości, które implementuje te same funkcje: **treatEmptyAsNull**, **skipLineCount**, **firstRowAsHeader**.</span><span class="sxs-lookup"><span data-stu-id="2862d-245">Datasets now support the following properties that implement the same functionality: **treatEmptyAsNull**, **skipLineCount**, **firstRowAsHeader**.</span></span>

<span data-ttu-id="2862d-246">Poniższa tabela zawiera wskazówki dotyczące przy użyciu nowych właściwości zestawu danych, zamiast tych właściwości źródło/ujście obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="2862d-246">The following table provides guidance on using the new dataset properties in place of these blob source/sink properties.</span></span>

| <span data-ttu-id="2862d-247">Właściwości działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="2862d-247">Copy Activity property</span></span> | <span data-ttu-id="2862d-248">Właściwości zestawu danych</span><span class="sxs-lookup"><span data-stu-id="2862d-248">Dataset property</span></span> |
|:--- |:--- |
| <span data-ttu-id="2862d-249">skipHeaderLineCount na BlobSource</span><span class="sxs-lookup"><span data-stu-id="2862d-249">skipHeaderLineCount on BlobSource</span></span> |<span data-ttu-id="2862d-250">skipLineCount i firstRowAsHeader.</span><span class="sxs-lookup"><span data-stu-id="2862d-250">skipLineCount and firstRowAsHeader.</span></span> <span data-ttu-id="2862d-251">Wiersze są pomijane najpierw i Odczytaj pierwszego wiersza jako nagłówka.</span><span class="sxs-lookup"><span data-stu-id="2862d-251">Lines are skipped first and then the first row is read as a header.</span></span> |
| <span data-ttu-id="2862d-252">treatEmptyAsNull na BlobSource</span><span class="sxs-lookup"><span data-stu-id="2862d-252">treatEmptyAsNull on BlobSource</span></span> |<span data-ttu-id="2862d-253">treatEmptyAsNull w zestawie danych wejściowych</span><span class="sxs-lookup"><span data-stu-id="2862d-253">treatEmptyAsNull on input dataset</span></span> |
| <span data-ttu-id="2862d-254">blobWriterAddHeader na BlobSink</span><span class="sxs-lookup"><span data-stu-id="2862d-254">blobWriterAddHeader on BlobSink</span></span> |<span data-ttu-id="2862d-255">firstRowAsHeader w zestawie danych wyjściowych</span><span class="sxs-lookup"><span data-stu-id="2862d-255">firstRowAsHeader on output dataset</span></span> |

<span data-ttu-id="2862d-256">Zobacz [określenie TextFormat](data-factory-supported-file-and-compression-formats.md#text-format) sekcji, aby uzyskać szczegółowe informacje na temat tych właściwości.</span><span class="sxs-lookup"><span data-stu-id="2862d-256">See [Specifying TextFormat](data-factory-supported-file-and-compression-formats.md#text-format) section for detailed information on these properties.</span></span>    

### <a name="recursive-and-copybehavior-examples"></a><span data-ttu-id="2862d-257">Przykłady cyklicznego i copyBehavior</span><span class="sxs-lookup"><span data-stu-id="2862d-257">recursive and copyBehavior examples</span></span>
<span data-ttu-id="2862d-258">W tej sekcji opisano efekty operacji kopiowania dla różnych kombinacji wartości cyklicznej i copyBehavior.</span><span class="sxs-lookup"><span data-stu-id="2862d-258">This section describes the resulting behavior of the Copy operation for different combinations of recursive and copyBehavior values.</span></span>

| <span data-ttu-id="2862d-259">Cykliczne</span><span class="sxs-lookup"><span data-stu-id="2862d-259">recursive</span></span> | <span data-ttu-id="2862d-260">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="2862d-260">copyBehavior</span></span> | <span data-ttu-id="2862d-261">Efekty</span><span class="sxs-lookup"><span data-stu-id="2862d-261">Resulting behavior</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2862d-262">Wartość true</span><span class="sxs-lookup"><span data-stu-id="2862d-262">true</span></span> |<span data-ttu-id="2862d-263">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="2862d-263">preserveHierarchy</span></span> |<span data-ttu-id="2862d-264">Dla folderu źródłowego Folder1 o następującej strukturze:</span><span class="sxs-lookup"><span data-stu-id="2862d-264">For a source folder Folder1 with the following structure:</span></span> <br/><br/><span data-ttu-id="2862d-265">Folder1</span><span class="sxs-lookup"><span data-stu-id="2862d-265">Folder1</span></span><br/><span data-ttu-id="2862d-266">&nbsp;&nbsp;&nbsp;&nbsp;Plik1</span><span class="sxs-lookup"><span data-stu-id="2862d-266">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="2862d-267">&nbsp;&nbsp;&nbsp;&nbsp;Plik2</span><span class="sxs-lookup"><span data-stu-id="2862d-267">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="2862d-268">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="2862d-268">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="2862d-269">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Plik3</span><span class="sxs-lookup"><span data-stu-id="2862d-269">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="2862d-270">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="2862d-270">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="2862d-271">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="2862d-271">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="2862d-272">folder docelowy Folder1 jest tworzony z tej samej struktury jako źródło</span><span class="sxs-lookup"><span data-stu-id="2862d-272">the target folder Folder1 is created with the same structure as the source</span></span><br/><br/><span data-ttu-id="2862d-273">Folder1</span><span class="sxs-lookup"><span data-stu-id="2862d-273">Folder1</span></span><br/><span data-ttu-id="2862d-274">&nbsp;&nbsp;&nbsp;&nbsp;Plik1</span><span class="sxs-lookup"><span data-stu-id="2862d-274">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="2862d-275">&nbsp;&nbsp;&nbsp;&nbsp;Plik2</span><span class="sxs-lookup"><span data-stu-id="2862d-275">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="2862d-276">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="2862d-276">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="2862d-277">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Plik3</span><span class="sxs-lookup"><span data-stu-id="2862d-277">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="2862d-278">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="2862d-278">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="2862d-279">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5.</span><span class="sxs-lookup"><span data-stu-id="2862d-279">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5.</span></span> |
| <span data-ttu-id="2862d-280">Wartość true</span><span class="sxs-lookup"><span data-stu-id="2862d-280">true</span></span> |<span data-ttu-id="2862d-281">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="2862d-281">flattenHierarchy</span></span> |<span data-ttu-id="2862d-282">Dla folderu źródłowego Folder1 o następującej strukturze:</span><span class="sxs-lookup"><span data-stu-id="2862d-282">For a source folder Folder1 with the following structure:</span></span> <br/><br/><span data-ttu-id="2862d-283">Folder1</span><span class="sxs-lookup"><span data-stu-id="2862d-283">Folder1</span></span><br/><span data-ttu-id="2862d-284">&nbsp;&nbsp;&nbsp;&nbsp;Plik1</span><span class="sxs-lookup"><span data-stu-id="2862d-284">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="2862d-285">&nbsp;&nbsp;&nbsp;&nbsp;Plik2</span><span class="sxs-lookup"><span data-stu-id="2862d-285">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="2862d-286">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="2862d-286">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="2862d-287">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Plik3</span><span class="sxs-lookup"><span data-stu-id="2862d-287">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="2862d-288">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="2862d-288">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="2862d-289">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="2862d-289">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="2862d-290">element docelowy Folder1, utworzono o następującej strukturze:</span><span class="sxs-lookup"><span data-stu-id="2862d-290">the target Folder1 is created with the following structure:</span></span> <br/><br/><span data-ttu-id="2862d-291">Folder1</span><span class="sxs-lookup"><span data-stu-id="2862d-291">Folder1</span></span><br/><span data-ttu-id="2862d-292">&nbsp;&nbsp;&nbsp;&nbsp;Nazwa wygenerowana automatycznie Plik1</span><span class="sxs-lookup"><span data-stu-id="2862d-292">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="2862d-293">&nbsp;&nbsp;&nbsp;&nbsp;Nazwa wygenerowana automatycznie plik2</span><span class="sxs-lookup"><span data-stu-id="2862d-293">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><span data-ttu-id="2862d-294">&nbsp;&nbsp;&nbsp;&nbsp;Nazwa wygenerowana automatycznie plik3</span><span class="sxs-lookup"><span data-stu-id="2862d-294">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File3</span></span><br/><span data-ttu-id="2862d-295">&nbsp;&nbsp;&nbsp;&nbsp;Nazwa wygenerowana automatycznie File4</span><span class="sxs-lookup"><span data-stu-id="2862d-295">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File4</span></span><br/><span data-ttu-id="2862d-296">&nbsp;&nbsp;&nbsp;&nbsp;Nazwa wygenerowana automatycznie File5</span><span class="sxs-lookup"><span data-stu-id="2862d-296">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File5</span></span> |
| <span data-ttu-id="2862d-297">Wartość true</span><span class="sxs-lookup"><span data-stu-id="2862d-297">true</span></span> |<span data-ttu-id="2862d-298">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="2862d-298">mergeFiles</span></span> |<span data-ttu-id="2862d-299">Dla folderu źródłowego Folder1 o następującej strukturze:</span><span class="sxs-lookup"><span data-stu-id="2862d-299">For a source folder Folder1 with the following structure:</span></span> <br/><br/><span data-ttu-id="2862d-300">Folder1</span><span class="sxs-lookup"><span data-stu-id="2862d-300">Folder1</span></span><br/><span data-ttu-id="2862d-301">&nbsp;&nbsp;&nbsp;&nbsp;Plik1</span><span class="sxs-lookup"><span data-stu-id="2862d-301">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="2862d-302">&nbsp;&nbsp;&nbsp;&nbsp;Plik2</span><span class="sxs-lookup"><span data-stu-id="2862d-302">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="2862d-303">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="2862d-303">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="2862d-304">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Plik3</span><span class="sxs-lookup"><span data-stu-id="2862d-304">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="2862d-305">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="2862d-305">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="2862d-306">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="2862d-306">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="2862d-307">element docelowy Folder1, utworzono o następującej strukturze:</span><span class="sxs-lookup"><span data-stu-id="2862d-307">the target Folder1 is created with the following structure:</span></span> <br/><br/><span data-ttu-id="2862d-308">Folder1</span><span class="sxs-lookup"><span data-stu-id="2862d-308">Folder1</span></span><br/><span data-ttu-id="2862d-309">&nbsp;&nbsp;&nbsp;&nbsp;Plik1 + plik2 + plik3 + File4 + pliku 5 zawartości są scalane w jeden plik o nazwie generowanych automatycznie</span><span class="sxs-lookup"><span data-stu-id="2862d-309">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 + File3 + File4 + File 5 contents are merged into one file with auto-generated file name</span></span> |
| <span data-ttu-id="2862d-310">wartość false</span><span class="sxs-lookup"><span data-stu-id="2862d-310">false</span></span> |<span data-ttu-id="2862d-311">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="2862d-311">preserveHierarchy</span></span> |<span data-ttu-id="2862d-312">Dla folderu źródłowego Folder1 o następującej strukturze:</span><span class="sxs-lookup"><span data-stu-id="2862d-312">For a source folder Folder1 with the following structure:</span></span> <br/><br/><span data-ttu-id="2862d-313">Folder1</span><span class="sxs-lookup"><span data-stu-id="2862d-313">Folder1</span></span><br/><span data-ttu-id="2862d-314">&nbsp;&nbsp;&nbsp;&nbsp;Plik1</span><span class="sxs-lookup"><span data-stu-id="2862d-314">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="2862d-315">&nbsp;&nbsp;&nbsp;&nbsp;Plik2</span><span class="sxs-lookup"><span data-stu-id="2862d-315">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="2862d-316">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="2862d-316">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="2862d-317">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Plik3</span><span class="sxs-lookup"><span data-stu-id="2862d-317">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="2862d-318">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="2862d-318">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="2862d-319">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="2862d-319">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="2862d-320">folder docelowy Folder1 jest tworzony o następującej strukturze</span><span class="sxs-lookup"><span data-stu-id="2862d-320">the target folder Folder1 is created with the following structure</span></span><br/><br/><span data-ttu-id="2862d-321">Folder1</span><span class="sxs-lookup"><span data-stu-id="2862d-321">Folder1</span></span><br/><span data-ttu-id="2862d-322">&nbsp;&nbsp;&nbsp;&nbsp;Plik1</span><span class="sxs-lookup"><span data-stu-id="2862d-322">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="2862d-323">&nbsp;&nbsp;&nbsp;&nbsp;Plik2</span><span class="sxs-lookup"><span data-stu-id="2862d-323">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><br/><br/><span data-ttu-id="2862d-324">Subfolder1 plik3, File4 i File5 nie są odczytywane.</span><span class="sxs-lookup"><span data-stu-id="2862d-324">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |
| <span data-ttu-id="2862d-325">wartość false</span><span class="sxs-lookup"><span data-stu-id="2862d-325">false</span></span> |<span data-ttu-id="2862d-326">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="2862d-326">flattenHierarchy</span></span> |<span data-ttu-id="2862d-327">Dla folderu źródłowego Folder1 o następującej strukturze:</span><span class="sxs-lookup"><span data-stu-id="2862d-327">For a source folder Folder1 with the following structure:</span></span><br/><br/><span data-ttu-id="2862d-328">Folder1</span><span class="sxs-lookup"><span data-stu-id="2862d-328">Folder1</span></span><br/><span data-ttu-id="2862d-329">&nbsp;&nbsp;&nbsp;&nbsp;Plik1</span><span class="sxs-lookup"><span data-stu-id="2862d-329">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="2862d-330">&nbsp;&nbsp;&nbsp;&nbsp;Plik2</span><span class="sxs-lookup"><span data-stu-id="2862d-330">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="2862d-331">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="2862d-331">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="2862d-332">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Plik3</span><span class="sxs-lookup"><span data-stu-id="2862d-332">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="2862d-333">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="2862d-333">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="2862d-334">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="2862d-334">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="2862d-335">folder docelowy Folder1 jest tworzony o następującej strukturze</span><span class="sxs-lookup"><span data-stu-id="2862d-335">the target folder Folder1 is created with the following structure</span></span><br/><br/><span data-ttu-id="2862d-336">Folder1</span><span class="sxs-lookup"><span data-stu-id="2862d-336">Folder1</span></span><br/><span data-ttu-id="2862d-337">&nbsp;&nbsp;&nbsp;&nbsp;Nazwa wygenerowana automatycznie Plik1</span><span class="sxs-lookup"><span data-stu-id="2862d-337">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="2862d-338">&nbsp;&nbsp;&nbsp;&nbsp;Nazwa wygenerowana automatycznie plik2</span><span class="sxs-lookup"><span data-stu-id="2862d-338">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><br/><br/><span data-ttu-id="2862d-339">Subfolder1 plik3, File4 i File5 nie są odczytywane.</span><span class="sxs-lookup"><span data-stu-id="2862d-339">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |
| <span data-ttu-id="2862d-340">wartość false</span><span class="sxs-lookup"><span data-stu-id="2862d-340">false</span></span> |<span data-ttu-id="2862d-341">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="2862d-341">mergeFiles</span></span> |<span data-ttu-id="2862d-342">Dla folderu źródłowego Folder1 o następującej strukturze:</span><span class="sxs-lookup"><span data-stu-id="2862d-342">For a source folder Folder1 with the following structure:</span></span><br/><br/><span data-ttu-id="2862d-343">Folder1</span><span class="sxs-lookup"><span data-stu-id="2862d-343">Folder1</span></span><br/><span data-ttu-id="2862d-344">&nbsp;&nbsp;&nbsp;&nbsp;Plik1</span><span class="sxs-lookup"><span data-stu-id="2862d-344">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="2862d-345">&nbsp;&nbsp;&nbsp;&nbsp;Plik2</span><span class="sxs-lookup"><span data-stu-id="2862d-345">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="2862d-346">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="2862d-346">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="2862d-347">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Plik3</span><span class="sxs-lookup"><span data-stu-id="2862d-347">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="2862d-348">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="2862d-348">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="2862d-349">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="2862d-349">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="2862d-350">folder docelowy Folder1 jest tworzony o następującej strukturze</span><span class="sxs-lookup"><span data-stu-id="2862d-350">the target folder Folder1 is created with the following structure</span></span><br/><br/><span data-ttu-id="2862d-351">Folder1</span><span class="sxs-lookup"><span data-stu-id="2862d-351">Folder1</span></span><br/><span data-ttu-id="2862d-352">&nbsp;&nbsp;&nbsp;&nbsp;Plik1 + plik2 zawartości są scalane w jeden plik o nazwie wygenerowany automatycznie.</span><span class="sxs-lookup"><span data-stu-id="2862d-352">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 contents are merged into one file with auto-generated file name.</span></span> <span data-ttu-id="2862d-353">Nazwa wygenerowana automatycznie Plik1</span><span class="sxs-lookup"><span data-stu-id="2862d-353">auto-generated name for File1</span></span><br/><br/><span data-ttu-id="2862d-354">Subfolder1 plik3, File4 i File5 nie są odczytywane.</span><span class="sxs-lookup"><span data-stu-id="2862d-354">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |

## <a name="walkthrough-use-copy-wizard-to-copy-data-tofrom-blob-storage"></a><span data-ttu-id="2862d-355">Wskazówki: Kreator kopiowania Użyj kopiowanie danych do/z magazynu obiektów Blob</span><span class="sxs-lookup"><span data-stu-id="2862d-355">Walkthrough: Use Copy Wizard to copy data to/from Blob Storage</span></span>
<span data-ttu-id="2862d-356">Oto jak szybko skopiować dane z magazynu obiektów blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="2862d-356">Let's look at how to quickly copy data to/from an Azure blob storage.</span></span> <span data-ttu-id="2862d-357">W tym przewodniku danych na serwerze źródłowym i docelowym są przechowywane typu: magazyn obiektów Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="2862d-357">In this walkthrough, both source and destination data stores of type: Azure Blob Storage.</span></span> <span data-ttu-id="2862d-358">Potok, w tym przewodniku kopiuje dane z folderu do innego folderu, w tym samym kontenerze obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="2862d-358">The pipeline in this walkthrough copies data from a folder to another folder in the same blob container.</span></span> <span data-ttu-id="2862d-359">Ten przewodnik jest celowo proste wyświetlić ustawienia lub właściwości w przypadku używania magazynu obiektów Blob jako źródło lub obiekt sink.</span><span class="sxs-lookup"><span data-stu-id="2862d-359">This walkthrough is intentionally simple to show you settings or properties when using Blob Storage as a source or sink.</span></span> 

### <a name="prerequisites"></a><span data-ttu-id="2862d-360">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="2862d-360">Prerequisites</span></span>
1. <span data-ttu-id="2862d-361">Utwórz ogólnego przeznaczenia **konta magazynu Azure** Jeśli nie masz już.</span><span class="sxs-lookup"><span data-stu-id="2862d-361">Create a general-purpose **Azure Storage Account** if you don't have one already.</span></span> <span data-ttu-id="2862d-362">Użyj magazynu obiektów blob jako zarówno **źródła** i **docelowego** magazynu danych, w tym przewodniku.</span><span class="sxs-lookup"><span data-stu-id="2862d-362">You use the blob storage as both **source** and **destination** data store in this walkthrough.</span></span> <span data-ttu-id="2862d-363">Jeśli nie masz konta magazynu platformy Azure, zobacz [Utwórz konto magazynu](../storage/common/storage-create-storage-account.md#create-a-storage-account) artykułu kroki go utworzyć.</span><span class="sxs-lookup"><span data-stu-id="2862d-363">if you don't have an Azure storage account, see the [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) article for steps to create one.</span></span>
2. <span data-ttu-id="2862d-364">Tworzenie kontenera obiektów blob o nazwie **adfblobconnector** na koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="2862d-364">Create a blob container named **adfblobconnector** in the storage account.</span></span> 
4. <span data-ttu-id="2862d-365">Utwórz folder o nazwie **wejściowych** w **adfblobconnector** kontenera.</span><span class="sxs-lookup"><span data-stu-id="2862d-365">Create a folder named **input** in the **adfblobconnector** container.</span></span>
5. <span data-ttu-id="2862d-366">Utwórz plik o nazwie **emp.txt** z następujących zawartości i przekaż go do **wejściowych** folderu za pomocą narzędzi takich jak [Eksploratora usługi Storage platformy Azure](https://azurestorageexplorer.codeplex.com/)</span><span class="sxs-lookup"><span data-stu-id="2862d-366">Create a file named **emp.txt** with the following content and upload it to the **input** folder by using tools such as [Azure Storage Explorer](https://azurestorageexplorer.codeplex.com/)</span></span>
    ```json
    John, Doe
    Jane, Doe
    ```
### <a name="create-the-data-factory"></a><span data-ttu-id="2862d-367">Tworzenie fabryki danych</span><span class="sxs-lookup"><span data-stu-id="2862d-367">Create the data factory</span></span>
1. <span data-ttu-id="2862d-368">Zaloguj się w witrynie [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="2862d-368">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="2862d-369">Kliknij przycisk **+ nowy** z lewego górnego rogu, kliknij przycisk **analizy i analiza**i kliknij przycisk **fabryki danych**.</span><span class="sxs-lookup"><span data-stu-id="2862d-369">Click **+ NEW** from the top-left corner, click **Intelligence + analytics**, and click **Data Factory**.</span></span>
3. <span data-ttu-id="2862d-370">W bloku **Nowa fabryka danych**:</span><span class="sxs-lookup"><span data-stu-id="2862d-370">In the **New data factory** blade:</span></span>   
    1. <span data-ttu-id="2862d-371">Wprowadź **ADFBlobConnectorDF** dla **nazwa**.</span><span class="sxs-lookup"><span data-stu-id="2862d-371">Enter **ADFBlobConnectorDF** for the **name**.</span></span> <span data-ttu-id="2862d-372">Nazwa fabryki danych Azure musi być globalnie unikatowa.</span><span class="sxs-lookup"><span data-stu-id="2862d-372">The name of the Azure data factory must be globally unique.</span></span> <span data-ttu-id="2862d-373">Jeśli zostanie wyświetlony błąd: `*Data factory name “ADFBlobConnectorDF” is not available`, Zmień nazwę fabryki danych (na przykład yournameADFBlobConnectorDF) i spróbuj ponownie utworzyć.</span><span class="sxs-lookup"><span data-stu-id="2862d-373">If you receive the error: `*Data factory name “ADFBlobConnectorDF” is not available`, change the name of the data factory (for example, yournameADFBlobConnectorDF) and try creating again.</span></span> <span data-ttu-id="2862d-374">Artykuł [Data Factory — Naming Rules](data-factory-naming-rules.md) (Fabryka danych — zasady nazewnictwa) zawiera zasady nazewnictwa artefaktów usługi Fabryka danych.</span><span class="sxs-lookup"><span data-stu-id="2862d-374">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>
    2. <span data-ttu-id="2862d-375">Wybierz swoją **subskrypcję** platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="2862d-375">Select your Azure **subscription**.</span></span>
    3. <span data-ttu-id="2862d-376">Dla grupy zasobów, wybierz **Użyj istniejącego** wybierz istniejącą grupę zasobów (lub) wybierz **Utwórz nowy** wprowadź nazwę grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="2862d-376">For Resource Group, select **Use existing** to select an existing resource group (or) select **Create new** to enter a name for a resource group.</span></span>
    4. <span data-ttu-id="2862d-377">Wybierz **lokalizację** fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="2862d-377">Select a **location** for the data factory.</span></span>
    5. <span data-ttu-id="2862d-378">Zaznacz pole wyboru **Przypnij do pulpitu nawigacyjnego** u dołu bloku.</span><span class="sxs-lookup"><span data-stu-id="2862d-378">Select **Pin to dashboard** check box at the bottom of the blade.</span></span>
    6. <span data-ttu-id="2862d-379">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="2862d-379">Click **Create**.</span></span>
3. <span data-ttu-id="2862d-380">Po zakończeniu tworzenia zobacz **fabryki danych** bloku, jak pokazano na poniższej ilustracji: ![strony głównej fabryki danych](./media/data-factory-azure-blob-connector/data-factory-home-page.png)</span><span class="sxs-lookup"><span data-stu-id="2862d-380">After the creation is complete, you see the **Data Factory** blade as shown in the following image: ![Data factory home page](./media/data-factory-azure-blob-connector/data-factory-home-page.png)</span></span>

### <a name="copy-wizard"></a><span data-ttu-id="2862d-381">Kreator kopiowania</span><span class="sxs-lookup"><span data-stu-id="2862d-381">Copy Wizard</span></span>
1. <span data-ttu-id="2862d-382">Na stronie głównej fabryki danych, kliknij przycisk **kopiowanie danych [Podgląd]** Kafelek, aby uruchomić **kreatora kopiowania danych** w osobnej karcie.</span><span class="sxs-lookup"><span data-stu-id="2862d-382">On the Data Factory home page, click the **Copy data [PREVIEW]** tile to launch **Copy Data Wizard** in a separate tab.</span></span>    
    
    > [!NOTE]
    >    <span data-ttu-id="2862d-383">Jeśli zobaczysz, że przeglądarki sieci web jest zablokowany na "Autoryzowanie...", wyłącz/Usuń zaznaczenie pola wyboru **zablokować pliki cookie innych firm, a dane lokacji** ustawienie (lub) schowaj włączone i utworzyć wyjątek **login.microsoftonline.com**, a następnie spróbuj ponownie uruchomić kreatora.</span><span class="sxs-lookup"><span data-stu-id="2862d-383">If you see that the web browser is stuck at "Authorizing...", disable/uncheck **Block third-party cookies and site data** setting (or) keep it enabled and create an exception for **login.microsoftonline.com** and then try launching the wizard again.</span></span>
2. <span data-ttu-id="2862d-384">Na stronie **Właściwości**:</span><span class="sxs-lookup"><span data-stu-id="2862d-384">In the **Properties** page:</span></span>
    1. <span data-ttu-id="2862d-385">Wprowadź **CopyPipeline** dla **Nazwa zadania**.</span><span class="sxs-lookup"><span data-stu-id="2862d-385">Enter **CopyPipeline** for **Task name**.</span></span> <span data-ttu-id="2862d-386">Nazwa zadania jest nazwą potok w fabryce danych.</span><span class="sxs-lookup"><span data-stu-id="2862d-386">The task name is the name of the pipeline in your data factory.</span></span>
    2. <span data-ttu-id="2862d-387">Wprowadź **opis** zadania (opcjonalnie).</span><span class="sxs-lookup"><span data-stu-id="2862d-387">Enter a **description** for the task (optional).</span></span>
    3. <span data-ttu-id="2862d-388">Dla **okresach zadań lub harmonogram zadań**, Zachowaj **regularnego uruchamiania zgodnie z harmonogramem** opcji.</span><span class="sxs-lookup"><span data-stu-id="2862d-388">For **Task cadence or Task schedule**, keep the **Run regularly on schedule** option.</span></span> <span data-ttu-id="2862d-389">Jeśli chcesz uruchomić to zadanie tylko raz zamiast uruchamiania wielokrotnie zgodnie z harmonogramem, wybierz opcję **uruchom raz teraz**.</span><span class="sxs-lookup"><span data-stu-id="2862d-389">If you want to run this task only once instead of run repeatedly on a schedule, select **Run once now**.</span></span> <span data-ttu-id="2862d-390">Jeśli zostanie wybrana, **uruchom raz teraz** opcji [potoku jednorazowego](data-factory-create-pipelines.md#onetime-pipeline) jest tworzony.</span><span class="sxs-lookup"><span data-stu-id="2862d-390">If you select, **Run once now** option, a [one-time pipeline](data-factory-create-pipelines.md#onetime-pipeline) is created.</span></span> 
    4. <span data-ttu-id="2862d-391">Zachowaj ustawienia **wzorzec cykliczny**.</span><span class="sxs-lookup"><span data-stu-id="2862d-391">Keep the settings for **Recurring pattern**.</span></span> <span data-ttu-id="2862d-392">To zadanie jest uruchamiane codziennie od godziny rozpoczęcia i zakończenia, które określisz w następnym kroku.</span><span class="sxs-lookup"><span data-stu-id="2862d-392">This task runs daily between the start and end times you specify in the next step.</span></span>
    5. <span data-ttu-id="2862d-393">Zmień **Data i godzina rozpoczęcia** do **2017-04/21**.</span><span class="sxs-lookup"><span data-stu-id="2862d-393">Change the **Start date time** to **04/21/2017**.</span></span> 
    6. <span data-ttu-id="2862d-394">Zmień **Data i godzina zakończenia** do **04/25/2017**.</span><span class="sxs-lookup"><span data-stu-id="2862d-394">Change the **End date time** to **04/25/2017**.</span></span> <span data-ttu-id="2862d-395">Możesz wpisać datę zamiast przeglądania kalendarza.</span><span class="sxs-lookup"><span data-stu-id="2862d-395">You may want to type the date instead of browsing through the calendar.</span></span>     
    8. <span data-ttu-id="2862d-396">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="2862d-396">Click **Next**.</span></span>
      <span data-ttu-id="2862d-397">![Skopiuj narzędzie — strona właściwości](./media/data-factory-azure-blob-connector/copy-tool-properties-page.png)</span><span class="sxs-lookup"><span data-stu-id="2862d-397">![Copy Tool - Properties page](./media/data-factory-azure-blob-connector/copy-tool-properties-page.png)</span></span> 
3. <span data-ttu-id="2862d-398">Na stronie **Magazyn danych źródłowych** kliknij kafelek **Azure Blob Storage**.</span><span class="sxs-lookup"><span data-stu-id="2862d-398">On the **Source data store** page, click **Azure Blob Storage** tile.</span></span> <span data-ttu-id="2862d-399">Ta strona służy do określania magazynu danych źródłowych do zadania kopiowania.</span><span class="sxs-lookup"><span data-stu-id="2862d-399">You use this page to specify the source data store for the copy task.</span></span> <span data-ttu-id="2862d-400">Możesz użyć istniejącej połączonej usługi magazynu danych lub określić nowy magazyn danych.</span><span class="sxs-lookup"><span data-stu-id="2862d-400">You can use an existing data store linked service (or) specify a new data store.</span></span> <span data-ttu-id="2862d-401">Aby korzystać z istniejącą połączoną usługę, należy wybrać **z ISTNIEJĄCYMI usługami POŁĄCZONEGO** i wybierz prawa połączonej usługi.</span><span class="sxs-lookup"><span data-stu-id="2862d-401">To use an existing linked service, you would select **FROM EXISTING LINKED SERVICES** and select the right linked service.</span></span> 
    <span data-ttu-id="2862d-402">![Skopiuj narzędzie — strona Sklepu źródła danych](./media/data-factory-azure-blob-connector/copy-tool-source-data-store-page.png)</span><span class="sxs-lookup"><span data-stu-id="2862d-402">![Copy Tool - Source data store page](./media/data-factory-azure-blob-connector/copy-tool-source-data-store-page.png)</span></span>
4. <span data-ttu-id="2862d-403">Na stronie **Określanie konta usługi Azure Blob Storage**:</span><span class="sxs-lookup"><span data-stu-id="2862d-403">On the **Specify the Azure Blob storage account** page:</span></span>
   1. <span data-ttu-id="2862d-404">Zachowaj nazwę automatycznie generowanej **nazwa połączenia**.</span><span class="sxs-lookup"><span data-stu-id="2862d-404">Keep the auto-generated name for **Connection name**.</span></span> <span data-ttu-id="2862d-405">Nazwa połączenia jest nazwa połączonej usługi typu: Magazyn Azure.</span><span class="sxs-lookup"><span data-stu-id="2862d-405">The connection name is the name of the linked service of type: Azure Storage.</span></span> 
   2. <span data-ttu-id="2862d-406">Upewnij się, że wybrano opcję **Z subskrypcji Azure** dla ustawienia **Metoda wyboru konta**.</span><span class="sxs-lookup"><span data-stu-id="2862d-406">Confirm that **From Azure subscriptions** option is selected for **Account selection method**.</span></span>
   3. <span data-ttu-id="2862d-407">Wybierz subskrypcję platformy Azure lub pozostaw **Zaznacz wszystko** dla **subskrypcji platformy Azure**.</span><span class="sxs-lookup"><span data-stu-id="2862d-407">Select your Azure subscription or keep **Select all** for **Azure subscription**.</span></span>   
   4. <span data-ttu-id="2862d-408">Wybierz **konto usługi Azure Storage** z listy kont usługi Azure Storage dostępnych w ramach wybranej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="2862d-408">Select an **Azure storage account** from the list of Azure storage accounts available in the selected subscription.</span></span> <span data-ttu-id="2862d-409">Można również ręcznie wprowadź ustawienia konta magazynu, wybierając **ręcznie wprowadzić** opcja dla **konta metodę wyboru**.</span><span class="sxs-lookup"><span data-stu-id="2862d-409">You can also choose to enter storage account settings manually by selecting **Enter manually** option for the **Account selection method**.</span></span>
   5. <span data-ttu-id="2862d-410">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="2862d-410">Click **Next**.</span></span> 
      <span data-ttu-id="2862d-411">![Skopiuj narzędzie — Określ konto magazynu obiektów Blob platformy Azure](./media/data-factory-azure-blob-connector/copy-tool-specify-azure-blob-storage-account.png)</span><span class="sxs-lookup"><span data-stu-id="2862d-411">![Copy Tool - Specify the Azure Blob storage account](./media/data-factory-azure-blob-connector/copy-tool-specify-azure-blob-storage-account.png)</span></span>
5. <span data-ttu-id="2862d-412">Na stronie **Wybieranie pliku lub folderu wejściowego**:</span><span class="sxs-lookup"><span data-stu-id="2862d-412">On **Choose the input file or folder** page:</span></span>
   1. <span data-ttu-id="2862d-413">Kliknij dwukrotnie **adfblobcontainer**.</span><span class="sxs-lookup"><span data-stu-id="2862d-413">Double-click **adfblobcontainer**.</span></span>
   2. <span data-ttu-id="2862d-414">Wybierz **wejściowych**i kliknij przycisk **wybierz**.</span><span class="sxs-lookup"><span data-stu-id="2862d-414">Select **input**, and click **Choose**.</span></span> <span data-ttu-id="2862d-415">W tym przewodniku wybierz opcję folder wejściowy.</span><span class="sxs-lookup"><span data-stu-id="2862d-415">In this walkthrough, you select the input folder.</span></span> <span data-ttu-id="2862d-416">Plik emp.txt można również wybrać w folderze zamiast tego.</span><span class="sxs-lookup"><span data-stu-id="2862d-416">You could also select the emp.txt file in the folder instead.</span></span> 
      <span data-ttu-id="2862d-417">![Skopiuj narzędzie — Wybierz wejściowy plik lub folder](./media/data-factory-azure-blob-connector/copy-tool-choose-input-file-or-folder.png)</span><span class="sxs-lookup"><span data-stu-id="2862d-417">![Copy Tool - Choose the input file or folder](./media/data-factory-azure-blob-connector/copy-tool-choose-input-file-or-folder.png)</span></span>
6. <span data-ttu-id="2862d-418">Na **wybierz wejściowy plik lub folder** strony:</span><span class="sxs-lookup"><span data-stu-id="2862d-418">On the **Choose the input file or folder** page:</span></span>
    1. <span data-ttu-id="2862d-419">Upewnij się, że **pliku lub folderu** ustawiono **adfblobconnector/wprowadzania**.</span><span class="sxs-lookup"><span data-stu-id="2862d-419">Confirm that the **file or folder** is set to **adfblobconnector/input**.</span></span> <span data-ttu-id="2862d-420">Jeśli pliki znajdują się w podfolderach, na przykład 2017/04/01, 2017/04/02 i tak dalej, wprowadź adfblobconnector/danych wejściowych / {year} / {month} / {day} dla pliku lub folderu.</span><span class="sxs-lookup"><span data-stu-id="2862d-420">If the files are in sub folders, for example, 2017/04/01, 2017/04/02, and so on, enter adfblobconnector/input/{year}/{month}/{day} for file or folder.</span></span> <span data-ttu-id="2862d-421">Po naciśnięciu klawisza TAB poza pola tekstowego, jest wyświetlany trzy listy rozwijanej, aby wybrać formaty roku (rrrr), miesiąc (MM) i dzień (dd).</span><span class="sxs-lookup"><span data-stu-id="2862d-421">When you press TAB out of the text box, you see three drop-down lists to select formats for year (yyyy), month (MM), and day (dd).</span></span> 
    2. <span data-ttu-id="2862d-422">Nie ustawiaj **skopiuj plik rekursywnie**.</span><span class="sxs-lookup"><span data-stu-id="2862d-422">Do not set **Copy file recursively**.</span></span> <span data-ttu-id="2862d-423">Wybierz tę opcję, aby rekursywnie przechodzenia przez foldery dla plików do skopiowania do miejsca docelowego.</span><span class="sxs-lookup"><span data-stu-id="2862d-423">Select this option to recursively traverse through folders for files to be copied to the destination.</span></span> 
    3. <span data-ttu-id="2862d-424">Nie **binarne kopiowania** opcji.</span><span class="sxs-lookup"><span data-stu-id="2862d-424">Do not the **binary copy** option.</span></span> <span data-ttu-id="2862d-425">Wybierz tę opcję, aby wykonać kopię binarnego pliku źródłowego do docelowego.</span><span class="sxs-lookup"><span data-stu-id="2862d-425">Select this option to perform a binary copy of source file to the destination.</span></span> <span data-ttu-id="2862d-426">Nie należy wybierać w ramach tego przewodnika, dzięki czemu można wyświetlić więcej opcji w kolejnych stronach.</span><span class="sxs-lookup"><span data-stu-id="2862d-426">Do not select for this walkthrough so that you can see more options in the next pages.</span></span> 
    4. <span data-ttu-id="2862d-427">Upewnij się, że **typ kompresji** ustawiono **Brak**.</span><span class="sxs-lookup"><span data-stu-id="2862d-427">Confirm that the **Compression type** is set to **None**.</span></span> <span data-ttu-id="2862d-428">Wybierz wartość dla tej opcji, jeśli kompresji w jednym z obsługiwanych formatów plików źródła.</span><span class="sxs-lookup"><span data-stu-id="2862d-428">Select a value for this option if your source files are compressed in one of the supported formats.</span></span> 
    5. <span data-ttu-id="2862d-429">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="2862d-429">Click **Next**.</span></span>
    <span data-ttu-id="2862d-430">![Skopiuj narzędzie — Wybierz wejściowy plik lub folder](./media/data-factory-azure-blob-connector/chose-input-file-folder.png)</span><span class="sxs-lookup"><span data-stu-id="2862d-430">![Copy Tool - Choose the input file or folder](./media/data-factory-azure-blob-connector/chose-input-file-folder.png)</span></span> 
7. <span data-ttu-id="2862d-431">Na stronie **Ustawienia formatu pliku** są wyświetlane ograniczniki i schemat wykrywany automatycznie przez kreatora w ramach analizy pliku.</span><span class="sxs-lookup"><span data-stu-id="2862d-431">On the **File format settings** page, you see the delimiters and the schema that is auto-detected by the wizard by parsing the file.</span></span> 
    1. <span data-ttu-id="2862d-432">Potwierdź następujące opcje:.</span><span class="sxs-lookup"><span data-stu-id="2862d-432">Confirm the following options: a.</span></span> <span data-ttu-id="2862d-433">**Format pliku** ustawiono **formacie tekstowym**.</span><span class="sxs-lookup"><span data-stu-id="2862d-433">The **file format** is set to **Text format**.</span></span> <span data-ttu-id="2862d-434">Widać obsługiwanych formatów na liście rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="2862d-434">You can see all the supported formats in the drop-down list.</span></span> <span data-ttu-id="2862d-435">Na przykład: JSON, Avro, ORC, Parquet.</span><span class="sxs-lookup"><span data-stu-id="2862d-435">For example: JSON, Avro, ORC, Parquet.</span></span>
        <span data-ttu-id="2862d-436">b.</span><span class="sxs-lookup"><span data-stu-id="2862d-436">b.</span></span> <span data-ttu-id="2862d-437">**Ogranicznik kolumny** ma ustawioną wartość `Comma (,)`.</span><span class="sxs-lookup"><span data-stu-id="2862d-437">The **column delimiter** is set to `Comma (,)`.</span></span> <span data-ttu-id="2862d-438">Widać inne ograniczniki kolumny obsługiwane przez fabrykę danych na liście rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="2862d-438">You can see the other column delimiters supported by Data Factory in the drop-down list.</span></span> <span data-ttu-id="2862d-439">Można również określić niestandardowe ogranicznika.</span><span class="sxs-lookup"><span data-stu-id="2862d-439">You can also specify a custom delimiter.</span></span>
        <span data-ttu-id="2862d-440">c.</span><span class="sxs-lookup"><span data-stu-id="2862d-440">c.</span></span> <span data-ttu-id="2862d-441">**Ogranicznik wiersza** ma ustawioną wartość `Carriage Return + Line feed (\r\n)`.</span><span class="sxs-lookup"><span data-stu-id="2862d-441">The **row delimiter** is set to `Carriage Return + Line feed (\r\n)`.</span></span> <span data-ttu-id="2862d-442">Widać inne ograniczniki wiersza obsługiwane przez fabrykę danych na liście rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="2862d-442">You can see the other row delimiters supported by Data Factory in the drop-down list.</span></span> <span data-ttu-id="2862d-443">Można również określić niestandardowe ogranicznika.</span><span class="sxs-lookup"><span data-stu-id="2862d-443">You can also specify a custom delimiter.</span></span>
        <span data-ttu-id="2862d-444">d.</span><span class="sxs-lookup"><span data-stu-id="2862d-444">d.</span></span> <span data-ttu-id="2862d-445">**Pominąć licznik wierszy** ustawiono **0**.</span><span class="sxs-lookup"><span data-stu-id="2862d-445">The **skip line count** is set to **0**.</span></span> <span data-ttu-id="2862d-446">Jeśli chcesz kilka wierszy do pominięcia w górnej części pliku, wprowadź numer tutaj.</span><span class="sxs-lookup"><span data-stu-id="2862d-446">If you want a few lines to be skipped at the top of the file, enter the number here.</span></span>
        <span data-ttu-id="2862d-447">e.</span><span class="sxs-lookup"><span data-stu-id="2862d-447">e.</span></span>  <span data-ttu-id="2862d-448">**Pierwszy wiersz danych zawiera nazwy kolumn** nie jest ustawiona.</span><span class="sxs-lookup"><span data-stu-id="2862d-448">The **first data row contains column names** is not set.</span></span> <span data-ttu-id="2862d-449">Jeśli pliki źródłowe zawierają nazwy kolumn w pierwszym wierszu, wybierz tę opcję.</span><span class="sxs-lookup"><span data-stu-id="2862d-449">If the source files contain column names in the first row, select this option.</span></span>
        <span data-ttu-id="2862d-450">f.</span><span class="sxs-lookup"><span data-stu-id="2862d-450">f.</span></span> <span data-ttu-id="2862d-451">**Wartość pusta kolumna jest traktowana jako null** opcja jest ustawiona.</span><span class="sxs-lookup"><span data-stu-id="2862d-451">The **treat empty column value as null** option is set.</span></span>
    2. <span data-ttu-id="2862d-452">Rozwiń węzeł **Zaawansowane ustawienia** do zaawansowanej opcji dostępnych w temacie.</span><span class="sxs-lookup"><span data-stu-id="2862d-452">Expand **Advanced settings** to see advanced option available.</span></span>
    3. <span data-ttu-id="2862d-453">W dolnej części strony, zobacz **Podgląd** danych z pliku emp.txt.</span><span class="sxs-lookup"><span data-stu-id="2862d-453">At the bottom of the page, see the **preview** of data from the emp.txt file.</span></span>
    4. <span data-ttu-id="2862d-454">Kliknij przycisk **SCHEMATU** u dołu, aby wyświetlić schemat, który Kreator kopiowania wykryta przez dane w pliku źródłowym.</span><span class="sxs-lookup"><span data-stu-id="2862d-454">Click **SCHEMA** tab at the bottom to see the schema that the copy wizard inferred by looking at the data in the source file.</span></span>
    5. <span data-ttu-id="2862d-455">Po przejrzeniu ograniczników i wyświetleniu podglądu danych kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="2862d-455">Click **Next** after you review the delimiters and preview data.</span></span>
    <span data-ttu-id="2862d-456">![Skopiuj narzędzie — Ustawienia format pliku](./media/data-factory-azure-blob-connector/copy-tool-file-format-settings.png)</span><span class="sxs-lookup"><span data-stu-id="2862d-456">![Copy Tool - File format settings](./media/data-factory-azure-blob-connector/copy-tool-file-format-settings.png)</span></span>  
8. <span data-ttu-id="2862d-457">Na **magazyn danych docelowej strony**, wybierz pozycję **magazyn obiektów Blob Azure**i kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="2862d-457">On the **Destination data store page**, select **Azure Blob Storage**, and click **Next**.</span></span> <span data-ttu-id="2862d-458">Używasz magazynu obiektów Blob Azure jako zarówno źródłowe i docelowe magazyny danych w ramach tego przewodnika.</span><span class="sxs-lookup"><span data-stu-id="2862d-458">You are using the Azure Blob Storage as both the source and destination data stores in this walkthrough.</span></span>    
    <span data-ttu-id="2862d-459">![Skopiuj narzędzie — Wybierz miejsce docelowe magazynu danych](media/data-factory-azure-blob-connector/select-destination-data-store.png)</span><span class="sxs-lookup"><span data-stu-id="2862d-459">![Copy Tool - select destination data store](media/data-factory-azure-blob-connector/select-destination-data-store.png)</span></span>
9. <span data-ttu-id="2862d-460">Na **Określ konto magazynu obiektów Blob platformy Azure** strony:</span><span class="sxs-lookup"><span data-stu-id="2862d-460">On **Specify the Azure Blob storage account** page:</span></span>
   1. <span data-ttu-id="2862d-461">Wprowadź **AzureStorageLinkedService** dla **nazwa połączenia** pola.</span><span class="sxs-lookup"><span data-stu-id="2862d-461">Enter **AzureStorageLinkedService** for the **Connection name** field.</span></span>
   2. <span data-ttu-id="2862d-462">Upewnij się, że wybrano opcję **Z subskrypcji Azure** dla ustawienia **Metoda wyboru konta**.</span><span class="sxs-lookup"><span data-stu-id="2862d-462">Confirm that **From Azure subscriptions** option is selected for **Account selection method**.</span></span>
   3. <span data-ttu-id="2862d-463">Wybierz swoją **subskrypcję** platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="2862d-463">Select your Azure **subscription**.</span></span>  
   4. <span data-ttu-id="2862d-464">Wybierz konto magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="2862d-464">Select your Azure storage account.</span></span> 
   5. <span data-ttu-id="2862d-465">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="2862d-465">Click **Next**.</span></span>     
10. <span data-ttu-id="2862d-466">Na **wybierz dane wyjściowe pliku lub folderu** strony:</span><span class="sxs-lookup"><span data-stu-id="2862d-466">On the **Choose the output file or folder** page:</span></span> 
    6. <span data-ttu-id="2862d-467">Określ **ścieżka folderu** jako **adfblobconnector/wyjścia / {year} / {month} / {day}**.</span><span class="sxs-lookup"><span data-stu-id="2862d-467">specify **Folder path** as **adfblobconnector/output/{year}/{month}/{day}**.</span></span> <span data-ttu-id="2862d-468">Wprowadź **kartę**.</span><span class="sxs-lookup"><span data-stu-id="2862d-468">Enter **TAB**.</span></span>
    7. <span data-ttu-id="2862d-469">Aby uzyskać **roku**, wybierz pozycję **rrrr**.</span><span class="sxs-lookup"><span data-stu-id="2862d-469">For the **year**, select **yyyy**.</span></span>
    8. <span data-ttu-id="2862d-470">Aby uzyskać **miesiąca**, upewnij się, że jest ustawiona na **MM**.</span><span class="sxs-lookup"><span data-stu-id="2862d-470">For the **month**, confirm that it is set to **MM**.</span></span>
    9. <span data-ttu-id="2862d-471">Aby uzyskać **dzień**, upewnij się, że jest ustawiona na **dd**.</span><span class="sxs-lookup"><span data-stu-id="2862d-471">For the **day**, confirm that it is set to **dd**.</span></span>
    10. <span data-ttu-id="2862d-472">Upewnij się, że **typ kompresji** ustawiono **Brak**.</span><span class="sxs-lookup"><span data-stu-id="2862d-472">Confirm that the **compression type** is set to **None**.</span></span>
    11. <span data-ttu-id="2862d-473">Upewnij się, że **skopiuj zachowanie** ustawiono **Scal pliki**.</span><span class="sxs-lookup"><span data-stu-id="2862d-473">Confirm that the **copy behavior** is set to **Merge files**.</span></span> <span data-ttu-id="2862d-474">Jeśli plik wyjściowy o takiej samej nazwie już istnieje, Nowa zawartość jest dodawana do tego samego pliku na końcu.</span><span class="sxs-lookup"><span data-stu-id="2862d-474">If the output file with the same name already exists, the new content is added to the same file at the end.</span></span>
    12. <span data-ttu-id="2862d-475">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="2862d-475">Click **Next**.</span></span>
    <span data-ttu-id="2862d-476">![Skopiuj narzędzie — Wybierz dane wyjściowe pliku lub folderu](media/data-factory-azure-blob-connector/choose-the-output-file-or-folder.png)</span><span class="sxs-lookup"><span data-stu-id="2862d-476">![Copy Tool - Choose output file or folder](media/data-factory-azure-blob-connector/choose-the-output-file-or-folder.png)</span></span>
11. <span data-ttu-id="2862d-477">Na **ustawienia formatu pliku** strony, przejrzyj ustawienia i kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="2862d-477">On the **File format settings** page, review the settings, and click **Next**.</span></span> <span data-ttu-id="2862d-478">Jednym z dodatkowe opcje jest dodanie nagłówka do pliku wyjściowego.</span><span class="sxs-lookup"><span data-stu-id="2862d-478">One of the additional options here is to add a header to the output file.</span></span> <span data-ttu-id="2862d-479">Jeśli wybrano tę opcję z nazwami kolumn zostanie dodany wiersz nagłówka ze schematu źródła.</span><span class="sxs-lookup"><span data-stu-id="2862d-479">If you select that option, a header row is added with names of the columns from the schema of the source.</span></span> <span data-ttu-id="2862d-480">Podczas wyświetlania schematu źródła, można zmienić domyślne nazwy kolumn.</span><span class="sxs-lookup"><span data-stu-id="2862d-480">You can rename the default column names when viewing the schema for the source.</span></span> <span data-ttu-id="2862d-481">Na przykład można zmienić pierwszej kolumny Imię i nazwisko drugą kolumnę.</span><span class="sxs-lookup"><span data-stu-id="2862d-481">For example, you could change the first column to First Name and second column to Last Name.</span></span> <span data-ttu-id="2862d-482">Następnie plik wyjściowy jest generowany przy użyciu nagłówka o tych nazwach jako nazwy kolumn.</span><span class="sxs-lookup"><span data-stu-id="2862d-482">Then, the output file is generated with a header with these names as column names.</span></span> 
    <span data-ttu-id="2862d-483">![Skopiuj narzędzie — Ustawienia format pliku dla miejsca docelowego](media/data-factory-azure-blob-connector/file-format-destination.png)</span><span class="sxs-lookup"><span data-stu-id="2862d-483">![Copy Tool - File format settings for destination](media/data-factory-azure-blob-connector/file-format-destination.png)</span></span>
12. <span data-ttu-id="2862d-484">Na **ustawienia wydajności** strony, upewnij się, że **chmury jednostki** i **równoległe kopie** ustawiono **automatycznie**i kliknij przycisk Dalej.</span><span class="sxs-lookup"><span data-stu-id="2862d-484">On the **Performance settings** page, confirm that **cloud units** and **parallel copies** are set to **Auto**, and click Next.</span></span> <span data-ttu-id="2862d-485">Aby uzyskać więcej informacji o tych ustawieniach, zobacz [skopiuj wydajności działania i dostrajania przewodnik](data-factory-copy-activity-performance.md#parallel-copy).</span><span class="sxs-lookup"><span data-stu-id="2862d-485">For details about these settings, see [Copy activity performance and tuning guide](data-factory-copy-activity-performance.md#parallel-copy).</span></span>
    <span data-ttu-id="2862d-486">![Skopiuj narzędzie — Ustawienia wydajności](media/data-factory-azure-blob-connector/copy-performance-settings.png)</span><span class="sxs-lookup"><span data-stu-id="2862d-486">![Copy Tool - Performance settings](media/data-factory-azure-blob-connector/copy-performance-settings.png)</span></span> 
14. <span data-ttu-id="2862d-487">Na **Podsumowanie** strony, przejrzyj wszystkie ustawienia (właściwości zadania, ustawienia źródłowe i docelowe i ustawień kopii), a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="2862d-487">On the **Summary** page, review all settings (task properties, settings for source and destination, and copy settings), and click **Next**.</span></span>
    <span data-ttu-id="2862d-488">![Skopiuj narzędzie — strona podsumowania](media/data-factory-azure-blob-connector/copy-tool-summary-page.png)</span><span class="sxs-lookup"><span data-stu-id="2862d-488">![Copy Tool - Summary page](media/data-factory-azure-blob-connector/copy-tool-summary-page.png)</span></span>
15. <span data-ttu-id="2862d-489">Przejrzyj informacje na stronie **Podsumowanie** i kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="2862d-489">Review information in the **Summary** page, and click **Finish**.</span></span> <span data-ttu-id="2862d-490">Kreator utworzy dwie połączone usługi, dwa zestawy danych (wejściowy i wyjściowy) i jeden potok w fabryce danych (z której został uruchomiony Kreator kopiowania).</span><span class="sxs-lookup"><span data-stu-id="2862d-490">The wizard creates two linked services, two datasets (input and output), and one pipeline in the data factory (from where you launched the Copy Wizard).</span></span>
    <span data-ttu-id="2862d-491">![Skopiuj narzędzie - stronę wdrożenia](media/data-factory-azure-blob-connector/copy-tool-deployment-page.png)</span><span class="sxs-lookup"><span data-stu-id="2862d-491">![Copy Tool - Deployment page](media/data-factory-azure-blob-connector/copy-tool-deployment-page.png)</span></span>

### <a name="monitor-the-pipeline-copy-task"></a><span data-ttu-id="2862d-492">Monitor potoku (zadanie kopiowania)</span><span class="sxs-lookup"><span data-stu-id="2862d-492">Monitor the pipeline (copy task)</span></span>

1. <span data-ttu-id="2862d-493">Kliknij łącze `Click here to monitor copy pipeline` na **wdrożenia** strony.</span><span class="sxs-lookup"><span data-stu-id="2862d-493">Click the link `Click here to monitor copy pipeline` on the **Deployment** page.</span></span> 
2. <span data-ttu-id="2862d-494">Powinny pojawić się **monitorowanie i Zarządzanie aplikacją** w osobnej karcie.  ![Monitorowanie aplikacji i zarządzanie](media/data-factory-azure-blob-connector/monitor-manage-app.png)</span><span class="sxs-lookup"><span data-stu-id="2862d-494">You should see the **Monitor and Manage application** in a separate tab.  ![Monitor and Manage App](media/data-factory-azure-blob-connector/monitor-manage-app.png)</span></span>
3. <span data-ttu-id="2862d-495">Zmień **start** czasu na górze do `04/19/2017` i **zakończenia** czas na `04/27/2017`, a następnie kliknij przycisk **Zastosuj**.</span><span class="sxs-lookup"><span data-stu-id="2862d-495">Change the **start** time at the top to `04/19/2017` and **end** time to `04/27/2017`, and then click **Apply**.</span></span> 
4. <span data-ttu-id="2862d-496">Powinny pojawić się pięć okien działania w **okien działania** listy.</span><span class="sxs-lookup"><span data-stu-id="2862d-496">You should see five activity windows in the **ACTIVITY WINDOWS** list.</span></span> <span data-ttu-id="2862d-497">**WindowStart** razy powinna obejmować wszystkie dni od początku potoku do potoku godziny zakończenia.</span><span class="sxs-lookup"><span data-stu-id="2862d-497">The **WindowStart** times should cover all days from pipeline start to pipeline end times.</span></span> 
5. <span data-ttu-id="2862d-498">Kliknij przycisk **Odśwież** przycisk dla **okien działania** listy kilka razy, aż zostanie wyświetlony stan wszystkich okien działania jest ustawiony na gotowe.</span><span class="sxs-lookup"><span data-stu-id="2862d-498">Click **Refresh** button for the **ACTIVITY WINDOWS** list a few times until you see the status of all the activity windows is set to Ready.</span></span> 
6. <span data-ttu-id="2862d-499">Teraz Sprawdź, czy pliki wyjściowe są generowane w folderze wyjściowym adfblobconnector kontenera.</span><span class="sxs-lookup"><span data-stu-id="2862d-499">Now, verify that the output files are generated in the output folder of adfblobconnector container.</span></span> <span data-ttu-id="2862d-500">Powinny pojawić się następujące struktury folderów w folderze wyjściowym:</span><span class="sxs-lookup"><span data-stu-id="2862d-500">You should see the following folder structure in the output folder:</span></span> 
    ```
    2017/04/21
    2017/04/22
    2017/04/23
    2017/04/24
    2017/04/25    
    ```
<span data-ttu-id="2862d-501">Aby uzyskać szczegółowe informacje o monitorowaniu i zarządzaniu nimi fabryk danych, zobacz [monitora i zarządzanie nimi potoku fabryki danych](data-factory-monitor-manage-app.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="2862d-501">For detailed information about monitoring and managing data factories, see [Monitor and manage Data Factory pipeline](data-factory-monitor-manage-app.md) article.</span></span> 
 
### <a name="data-factory-entities"></a><span data-ttu-id="2862d-502">Obiekty fabryki danych</span><span class="sxs-lookup"><span data-stu-id="2862d-502">Data Factory entities</span></span>
<span data-ttu-id="2862d-503">Teraz przejdź do karty na stronie głównej fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="2862d-503">Now, switch back to the tab with the Data Factory home page.</span></span> <span data-ttu-id="2862d-504">Zwróć uwagę, że istnieją dwa połączone usługi, dwa zestawy danych i jeden potok w fabryce danych teraz.</span><span class="sxs-lookup"><span data-stu-id="2862d-504">Notice that there are two linked services, two datasets, and one pipeline in your data factory now.</span></span> 

![Strona główna fabryka danych z jednostkami](media/data-factory-azure-blob-connector/data-factory-home-page-with-numbers.png)

<span data-ttu-id="2862d-506">Kliknij przycisk **tworzenie i wdrażanie** można uruchomić Edytor fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="2862d-506">Click **Author and deploy** to launch Data Factory Editor.</span></span> 

![Edytor fabryki danych](media/data-factory-azure-blob-connector/data-factory-editor.png)

<span data-ttu-id="2862d-508">Następujące jednostek fabryki danych powinny być widoczne w fabryce danych:</span><span class="sxs-lookup"><span data-stu-id="2862d-508">You should see the following Data Factory entities in your data factory:</span></span> 

 - <span data-ttu-id="2862d-509">Dwa połączone usługi.</span><span class="sxs-lookup"><span data-stu-id="2862d-509">Two linked services.</span></span> <span data-ttu-id="2862d-510">Jeden dla źródła i drugą dla miejsca docelowego.</span><span class="sxs-lookup"><span data-stu-id="2862d-510">One for the source and the other one for the destination.</span></span> <span data-ttu-id="2862d-511">Usługi połączonej odwoływać się do tego samego konta magazynu Azure w ramach tego przewodnika.</span><span class="sxs-lookup"><span data-stu-id="2862d-511">Both the linked services refer to the same Azure Storage account in this walkthrough.</span></span> 
 - <span data-ttu-id="2862d-512">Dwa zestawy danych.</span><span class="sxs-lookup"><span data-stu-id="2862d-512">Two datasets.</span></span> <span data-ttu-id="2862d-513">Zestaw wejściowy i wyjściowy zestaw danych.</span><span class="sxs-lookup"><span data-stu-id="2862d-513">An input dataset and an output dataset.</span></span> <span data-ttu-id="2862d-514">W tym przewodniku zarówno używać tego samego kontenera obiektów blob, ale odwołuje się do innych folderów (dane wejściowe i wyjściowe).</span><span class="sxs-lookup"><span data-stu-id="2862d-514">In this walkthrough, both use the same blob container but refer to different folders (input and output).</span></span>
 - <span data-ttu-id="2862d-515">Potok.</span><span class="sxs-lookup"><span data-stu-id="2862d-515">A pipeline.</span></span> <span data-ttu-id="2862d-516">Potok zawiera działanie kopiowania, który używa źródła obiektów blob i sink obiektów blob można skopiować danych z lokalizacji obiektów blob platformy Azure do innej lokalizacji obiektu blob systemu Azure.</span><span class="sxs-lookup"><span data-stu-id="2862d-516">The pipeline contains a copy activity that uses a blob source and a blob sink to copy data from an Azure blob location to another Azure blob location.</span></span> 

<span data-ttu-id="2862d-517">Poniższe sekcje zawierają więcej informacji na temat tych jednostek.</span><span class="sxs-lookup"><span data-stu-id="2862d-517">The following sections provide more information about these entities.</span></span> 

#### <a name="linked-services"></a><span data-ttu-id="2862d-518">Połączone usługi</span><span class="sxs-lookup"><span data-stu-id="2862d-518">Linked services</span></span>
<span data-ttu-id="2862d-519">Powinny pojawić się dwa połączonych usług.</span><span class="sxs-lookup"><span data-stu-id="2862d-519">You should see two linked services.</span></span> <span data-ttu-id="2862d-520">Jeden dla źródła i drugą dla miejsca docelowego.</span><span class="sxs-lookup"><span data-stu-id="2862d-520">One for the source and the other one for the destination.</span></span> <span data-ttu-id="2862d-521">W tym przewodniku zarówno definicje wyglądają tak samo, z wyjątkiem nazwy.</span><span class="sxs-lookup"><span data-stu-id="2862d-521">In this walkthrough, both definitions look the same except for the names.</span></span> <span data-ttu-id="2862d-522">**Typu** połączonej usługi jest ustawiony na wartość **AzureStorage**.</span><span class="sxs-lookup"><span data-stu-id="2862d-522">The **type** of the linked service is set to **AzureStorage**.</span></span> <span data-ttu-id="2862d-523">Najważniejsze właściwości definicji połączonej usługi jest **connectionString**, który jest używany przez fabryki danych do łączenia się z kontem magazynu Azure w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="2862d-523">Most important property of the linked service definition is the **connectionString**, which is used by Data Factory to connect to your Azure Storage account at runtime.</span></span> <span data-ttu-id="2862d-524">Ignoruj właściwości hubName w definicji.</span><span class="sxs-lookup"><span data-stu-id="2862d-524">Ignore the hubName property in the definition.</span></span> 

##### <a name="source-blob-storage-linked-service"></a><span data-ttu-id="2862d-525">Źródła obiektów blob połączoną usługą magazynu</span><span class="sxs-lookup"><span data-stu-id="2862d-525">Source blob storage linked service</span></span>
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

##### <a name="destination-blob-storage-linked-service"></a><span data-ttu-id="2862d-526">Docelowy obiekt blob połączoną usługą magazynu</span><span class="sxs-lookup"><span data-stu-id="2862d-526">Destination blob storage linked service</span></span>

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

<span data-ttu-id="2862d-527">Aby uzyskać więcej informacji na temat połączoną usługą magazynu Azure, zobacz [połączona usługa właściwości](#linked-service-properties) sekcji.</span><span class="sxs-lookup"><span data-stu-id="2862d-527">For more information about Azure Storage linked service, see [Linked service properties](#linked-service-properties) section.</span></span> 

#### <a name="datasets"></a><span data-ttu-id="2862d-528">Zestawy danych</span><span class="sxs-lookup"><span data-stu-id="2862d-528">Datasets</span></span>
<span data-ttu-id="2862d-529">Istnieją dwa zestawy danych: zestaw wejściowy i wyjściowy zestaw danych.</span><span class="sxs-lookup"><span data-stu-id="2862d-529">There are two datasets: an input dataset and an output dataset.</span></span> <span data-ttu-id="2862d-530">Typ zestawu danych jest ustawiony na **AzureBlob** dla obu.</span><span class="sxs-lookup"><span data-stu-id="2862d-530">The type of the dataset is set to **AzureBlob** for both.</span></span> 

<span data-ttu-id="2862d-531">Wejściowy zestaw danych wskazuje **wejściowych** folderu **adfblobconnector** kontenera obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="2862d-531">The input dataset points to the **input** folder of the **adfblobconnector** blob container.</span></span> <span data-ttu-id="2862d-532">**Zewnętrznych** właściwość jest ustawiona na **true** dla tego zestawu danych jako dane nie jest generowany przez potok wraz z działanie kopiowania, który przyjmuje tego zestawu danych jako dane wejściowe.</span><span class="sxs-lookup"><span data-stu-id="2862d-532">The **external** property is set to **true** for this dataset as the data is not produced by the pipeline with the copy activity that takes this dataset as an input.</span></span> 

<span data-ttu-id="2862d-533">Wskazuje wyjściowy zestaw danych **dane wyjściowe** folder z tego samego kontenera obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="2862d-533">The output dataset points to the **output** folder of the same blob container.</span></span> <span data-ttu-id="2862d-534">Wyjściowy zestaw danych używa również rok, miesiąc i dzień **SliceStart** zmienna można dynamicznie obliczyć ścieżki do pliku wyjściowego.</span><span class="sxs-lookup"><span data-stu-id="2862d-534">The output dataset also uses the year, month, and day of the **SliceStart** system variable to dynamically evaluate the path for the output file.</span></span> <span data-ttu-id="2862d-535">Listę funkcje i zmienne systemu obsługiwane przez fabrykę danych, zobacz [funkcje fabryki danych i zmienne systemu](data-factory-functions-variables.md).</span><span class="sxs-lookup"><span data-stu-id="2862d-535">For a list of functions and system variables supported by Data Factory, see [Data Factory functions and system variables](data-factory-functions-variables.md).</span></span> <span data-ttu-id="2862d-536">**Zewnętrznych** właściwość jest ustawiona na **false** (wartość domyślna), ponieważ ten zestaw danych jest generowany przez potok.</span><span class="sxs-lookup"><span data-stu-id="2862d-536">The **external** property is set to **false** (default value) because this dataset is produced by the pipeline.</span></span> 

<span data-ttu-id="2862d-537">Aby uzyskać więcej informacji na temat właściwości obsługiwanych przez zestaw danych obiektów Blob platformy Azure, zobacz [właściwości zestawu danych](#dataset-properties) sekcji.</span><span class="sxs-lookup"><span data-stu-id="2862d-537">For more information about properties supported by Azure Blob dataset, see [Dataset properties](#dataset-properties) section.</span></span>

##### <a name="input-dataset"></a><span data-ttu-id="2862d-538">Wejściowy zestaw danych</span><span class="sxs-lookup"><span data-stu-id="2862d-538">Input dataset</span></span>

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

##### <a name="output-dataset"></a><span data-ttu-id="2862d-539">Wyjściowy zestaw danych</span><span class="sxs-lookup"><span data-stu-id="2862d-539">Output dataset</span></span>

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

#### <a name="pipeline"></a><span data-ttu-id="2862d-540">Potok</span><span class="sxs-lookup"><span data-stu-id="2862d-540">Pipeline</span></span>
<span data-ttu-id="2862d-541">Potok zawiera tylko jedno działanie.</span><span class="sxs-lookup"><span data-stu-id="2862d-541">The pipeline has just one activity.</span></span> <span data-ttu-id="2862d-542">**Typu** działania jest ustawiony na wartość **kopiowania**.</span><span class="sxs-lookup"><span data-stu-id="2862d-542">The **type** of the activity is set to **Copy**.</span></span>  <span data-ttu-id="2862d-543">We właściwościach typu działania istnieją dwie sekcje, jeden dla źródła i drugą dla obiekt sink.</span><span class="sxs-lookup"><span data-stu-id="2862d-543">In the type properties for the activity, there are two sections, one for source and the other one for sink.</span></span> <span data-ttu-id="2862d-544">Typ źródłowy ma ustawioną wartość **BlobSource** jako działanie kopiuje dane z magazynu obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="2862d-544">The source type is set to **BlobSource** as the activity is copying data from a blob storage.</span></span> <span data-ttu-id="2862d-545">Typ ujścia ma ustawioną wartość **BlobSink** jako działania kopiowania danych do magazynu obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="2862d-545">The sink type is set to **BlobSink** as the activity copying data to a blob storage.</span></span> <span data-ttu-id="2862d-546">Działanie kopiowania przyjmuje jako dane wejściowe InputDataset-z4y i OutputDataset-z4y jako dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="2862d-546">The copy activity takes InputDataset-z4y as the input and OutputDataset-z4y as the output.</span></span> 

<span data-ttu-id="2862d-547">Aby uzyskać więcej informacji o obsługiwanych przez BlobSource i BlobSink właściwości, zobacz [skopiować właściwości działania](#copy-activity-properties) sekcji.</span><span class="sxs-lookup"><span data-stu-id="2862d-547">For more information about properties supported by BlobSource and BlobSink, see [Copy activity properties](#copy-activity-properties) section.</span></span> 

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

## <a name="json-examples-for-copying-data-to-and-from-blob-storage"></a><span data-ttu-id="2862d-548">Przykłady JSON do kopiowania danych z magazynu obiektów Blob</span><span class="sxs-lookup"><span data-stu-id="2862d-548">JSON examples for copying data to and from Blob Storage</span></span>  
<span data-ttu-id="2862d-549">Poniższe przykłady zapewniają definicje JSON, których można utworzyć potok przy użyciu [portalu Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) lub [programu Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) lub [programu Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="2862d-549">The following examples provide sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="2862d-550">Przedstawiają sposób kopiowania danych do i z magazynu obiektów Blob Azure i bazy danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="2862d-550">They show how to copy data to and from Azure Blob Storage and Azure SQL Database.</span></span> <span data-ttu-id="2862d-551">Jednak dane mogą być kopiowane **bezpośrednio** z dowolnego źródła do dowolnego wychwytywanie podane [tutaj](data-factory-data-movement-activities.md#supported-data-stores-and-formats) za pomocą działania kopiowania w fabryce danych Azure.</span><span class="sxs-lookup"><span data-stu-id="2862d-551">However, data can be copied **directly** from any of sources to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>

### <a name="json-example-copy-data-from-blob-storage-to-sql-database"></a><span data-ttu-id="2862d-552">Przykład JSON: Kopiowanie danych z magazynu obiektów Blob do bazy danych SQL</span><span class="sxs-lookup"><span data-stu-id="2862d-552">JSON Example: Copy data from Blob Storage to SQL Database</span></span>
<span data-ttu-id="2862d-553">Poniższy przykład przedstawia:</span><span class="sxs-lookup"><span data-stu-id="2862d-553">The following sample shows:</span></span>

1. <span data-ttu-id="2862d-554">Połączonej usługi typu [AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="2862d-554">A linked service of type [AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="2862d-555">Połączonej usługi typu [AzureStorage](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="2862d-555">A linked service of type [AzureStorage](#linked-service-properties).</span></span>
3. <span data-ttu-id="2862d-556">Dane wejściowe [dataset](data-factory-create-datasets.md) typu [AzureBlob](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="2862d-556">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](#dataset-properties).</span></span>
4. <span data-ttu-id="2862d-557">Dane wyjściowe [dataset](data-factory-create-datasets.md) typu [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="2862d-557">An output [dataset](data-factory-create-datasets.md) of type [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="2862d-558">A [potoku](data-factory-create-pipelines.md) z działania kopiowania, która używa [BlobSource](#copy-activity-properties) i [SqlSink](data-factory-azure-sql-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="2862d-558">A [pipeline](data-factory-create-pipelines.md) with a Copy activity that uses [BlobSource](#copy-activity-properties) and [SqlSink](data-factory-azure-sql-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="2862d-559">Kopie próbki szeregów czasowych dane z usługi Azure blob do bazy danych SQL Azure tabeli co godzinę.</span><span class="sxs-lookup"><span data-stu-id="2862d-559">The sample copies time-series data from an Azure blob to an Azure SQL table hourly.</span></span> <span data-ttu-id="2862d-560">Właściwości JSON używane w te przykłady są opisane w sekcjach poniżej próbek.</span><span class="sxs-lookup"><span data-stu-id="2862d-560">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="2862d-561">**Azure połączoną usługą SQL:**</span><span class="sxs-lookup"><span data-stu-id="2862d-561">**Azure SQL linked service:**</span></span>

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
<span data-ttu-id="2862d-562">**Połączonej usługi magazynu Azure:**</span><span class="sxs-lookup"><span data-stu-id="2862d-562">**Azure Storage linked service:**</span></span>

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
<span data-ttu-id="2862d-563">Fabryka danych Azure obsługuje dwa typy usług magazynu Azure połączony: **AzureStorage** i **element AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="2862d-563">Azure Data Factory supports two types of Azure Storage linked services: **AzureStorage** and **AzureStorageSas**.</span></span> <span data-ttu-id="2862d-564">Dla pierwszego z nich Określ ciąg połączenia, który zawiera klucz konta i dla późniejszą, określ identyfikator Uri dostępu sygnatury dostępu Współdzielonego.</span><span class="sxs-lookup"><span data-stu-id="2862d-564">For the first one, you specify the connection string that includes the account key and for the later one, you specify the Shared Access Signature (SAS) Uri.</span></span> <span data-ttu-id="2862d-565">Zobacz [połączonych usług](#linked-service-properties) sekcji, aby uzyskać szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="2862d-565">See [Linked Services](#linked-service-properties) section for details.</span></span>  

<span data-ttu-id="2862d-566">**Azure wejściowego zestawu danych obiektów Blob:**</span><span class="sxs-lookup"><span data-stu-id="2862d-566">**Azure Blob input dataset:**</span></span>

<span data-ttu-id="2862d-567">Dane są pobierane z nowego obiektu blob co godzinę (częstotliwość: godziny, interwał: 1).</span><span class="sxs-lookup"><span data-stu-id="2862d-567">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="2862d-568">Nazwa i ścieżka pliku folder dla obiektu blob dynamicznie są oceniane na podstawie czasu rozpoczęcia wycinek, który jest przetwarzana.</span><span class="sxs-lookup"><span data-stu-id="2862d-568">The folder path and file name for the blob are dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="2862d-569">Ścieżka folderu korzysta rok, miesiąc i dzień część czas rozpoczęcia, a nazwa pliku godzina część czas rozpoczęcia.</span><span class="sxs-lookup"><span data-stu-id="2862d-569">The folder path uses year, month, and day part of the start time and file name uses the hour part of the start time.</span></span> <span data-ttu-id="2862d-570">"external": ustawienie "prawda" fabryki danych informuje, że w tabeli zewnętrznej dla fabryki danych i nie jest generowany przez działanie w fabryce danych.</span><span class="sxs-lookup"><span data-stu-id="2862d-570">“external”: “true” setting informs Data Factory that the table is external to the data factory and is not produced by an activity in the data factory.</span></span>

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
<span data-ttu-id="2862d-571">**Azure SQL wyjściowy zestaw danych:**</span><span class="sxs-lookup"><span data-stu-id="2862d-571">**Azure SQL output dataset:**</span></span>

<span data-ttu-id="2862d-572">Kopie przykładowych danych do tabeli o nazwie "MyTable" w bazie danych Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="2862d-572">The sample copies data to a table named “MyTable” in an Azure SQL database.</span></span> <span data-ttu-id="2862d-573">Tworzenie tabeli w bazie danych Azure SQL z taką samą liczbę kolumn, zgodnie z oczekiwaniami pliku Blob CSV zawiera.</span><span class="sxs-lookup"><span data-stu-id="2862d-573">Create the table in your Azure SQL database with the same number of columns as you expect the Blob CSV file to contain.</span></span> <span data-ttu-id="2862d-574">Nowe wiersze są dodawane do tabeli co godzinę.</span><span class="sxs-lookup"><span data-stu-id="2862d-574">New rows are added to the table every hour.</span></span>

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
<span data-ttu-id="2862d-575">**Działanie kopiowania w potoku z obiektu Blob, źródłowy i odbiorczy SQL:**</span><span class="sxs-lookup"><span data-stu-id="2862d-575">**A copy activity in a pipeline with Blob source and SQL sink:**</span></span>

<span data-ttu-id="2862d-576">Potok zawiera działanie kopiowania, który jest skonfigurowany do używania wejściowe i wyjściowe zestawy danych i jest zaplanowane co godzinę.</span><span class="sxs-lookup"><span data-stu-id="2862d-576">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="2862d-577">W definicji JSON potoku **źródła** ustawiono typ **BlobSource** i **zbiornika** ustawiono typ **SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="2862d-577">In the pipeline JSON definition, the **source** type is set to **BlobSource** and **sink** type is set to **SqlSink**.</span></span>

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
### <a name="json-example-copy-data-from-azure-sql-to-azure-blob"></a><span data-ttu-id="2862d-578">Przykład JSON: Kopiowanie danych z bazy danych SQL Azure do obiektów Blob platformy Azure</span><span class="sxs-lookup"><span data-stu-id="2862d-578">JSON Example: Copy data from Azure SQL to Azure Blob</span></span>
<span data-ttu-id="2862d-579">Poniższy przykład przedstawia:</span><span class="sxs-lookup"><span data-stu-id="2862d-579">The following sample shows:</span></span>

1. <span data-ttu-id="2862d-580">Połączonej usługi typu [AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="2862d-580">A linked service of type [AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="2862d-581">Połączonej usługi typu [AzureStorage](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="2862d-581">A linked service of type [AzureStorage](#linked-service-properties).</span></span>
3. <span data-ttu-id="2862d-582">Dane wejściowe [dataset](data-factory-create-datasets.md) typu [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="2862d-582">An input [dataset](data-factory-create-datasets.md) of type [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="2862d-583">Dane wyjściowe [dataset](data-factory-create-datasets.md) typu [AzureBlob](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="2862d-583">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](#dataset-properties).</span></span>
5. <span data-ttu-id="2862d-584">A [potoku](data-factory-create-pipelines.md) z działaniem kopii, która używa [SqlSource](data-factory-azure-sql-connector.md#copy-activity-properties) i [BlobSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="2862d-584">A [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [SqlSource](data-factory-azure-sql-connector.md#copy-activity-properties) and [BlobSink](#copy-activity-properties).</span></span>

<span data-ttu-id="2862d-585">Przykład kopiuje dane szeregów czasowych z tabeli Azure SQL do obiektów blob platformy Azure co godzinę.</span><span class="sxs-lookup"><span data-stu-id="2862d-585">The sample copies time-series data from an Azure SQL table to an Azure blob hourly.</span></span> <span data-ttu-id="2862d-586">Właściwości JSON używane w te przykłady są opisane w sekcjach poniżej próbek.</span><span class="sxs-lookup"><span data-stu-id="2862d-586">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="2862d-587">**Azure połączoną usługą SQL:**</span><span class="sxs-lookup"><span data-stu-id="2862d-587">**Azure SQL linked service:**</span></span>

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
<span data-ttu-id="2862d-588">**Połączonej usługi magazynu Azure:**</span><span class="sxs-lookup"><span data-stu-id="2862d-588">**Azure Storage linked service:**</span></span>

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
<span data-ttu-id="2862d-589">Fabryka danych Azure obsługuje dwa typy usług magazynu Azure połączony: **AzureStorage** i **element AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="2862d-589">Azure Data Factory supports two types of Azure Storage linked services: **AzureStorage** and **AzureStorageSas**.</span></span> <span data-ttu-id="2862d-590">Dla pierwszego z nich Określ ciąg połączenia, który zawiera klucz konta i dla późniejszą, określ identyfikator Uri dostępu sygnatury dostępu Współdzielonego.</span><span class="sxs-lookup"><span data-stu-id="2862d-590">For the first one, you specify the connection string that includes the account key and for the later one, you specify the Shared Access Signature (SAS) Uri.</span></span> <span data-ttu-id="2862d-591">Zobacz [połączonych usług](#linked-service-properties) sekcji, aby uzyskać szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="2862d-591">See [Linked Services](#linked-service-properties) section for details.</span></span>  

<span data-ttu-id="2862d-592">**Azure SQL wejściowy zestaw danych:**</span><span class="sxs-lookup"><span data-stu-id="2862d-592">**Azure SQL input dataset:**</span></span>

<span data-ttu-id="2862d-593">Przykład przyjęto założenie, utworzono tabelę "MyTable" w języku SQL Azure i zawiera kolumnę o nazwie "timestampcolumn" dla czasu serii danych.</span><span class="sxs-lookup"><span data-stu-id="2862d-593">The sample assumes you have created a table “MyTable” in Azure SQL and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="2862d-594">Ustawienie "external": "prawda" informuje usługi fabryka danych czy tabeli zewnętrznej dla fabryki danych i nie jest generowany przez działanie w fabryce danych.</span><span class="sxs-lookup"><span data-stu-id="2862d-594">Setting “external”: ”true” informs Data Factory service that the table is external to the data factory and is not produced by an activity in the data factory.</span></span>

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

<span data-ttu-id="2862d-595">**Azure Blob wyjściowy zestaw danych:**</span><span class="sxs-lookup"><span data-stu-id="2862d-595">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="2862d-596">Dane są zapisywane do nowego obiektu blob co godzinę (częstotliwość: godziny, interwał: 1).</span><span class="sxs-lookup"><span data-stu-id="2862d-596">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="2862d-597">Ścieżka folderu dla obiekt blob jest dynamicznie obliczane na podstawie czasu rozpoczęcia wycinek, który jest przetwarzana.</span><span class="sxs-lookup"><span data-stu-id="2862d-597">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="2862d-598">Ścieżka folderu używa rok, miesiąc, dzień i godziny części czas rozpoczęcia.</span><span class="sxs-lookup"><span data-stu-id="2862d-598">The folder path uses year, month, day, and hours parts of the start time.</span></span>

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

<span data-ttu-id="2862d-599">**Działanie kopiowania w potoku z SQL źródłowy i odbiorczy obiektów Blob:**</span><span class="sxs-lookup"><span data-stu-id="2862d-599">**A copy activity in a pipeline with SQL source and Blob sink:**</span></span>

<span data-ttu-id="2862d-600">Potok zawiera działanie kopiowania, który jest skonfigurowany do używania wejściowe i wyjściowe zestawy danych i jest zaplanowane co godzinę.</span><span class="sxs-lookup"><span data-stu-id="2862d-600">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="2862d-601">W definicji JSON potoku **źródła** ustawiono typ **SqlSource** i **zbiornika** ustawiono typ **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="2862d-601">In the pipeline JSON definition, the **source** type is set to **SqlSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="2862d-602">Określony dla zapytania SQL **SqlReaderQuery** właściwości wybiera dane w ostatniej godziny do skopiowania.</span><span class="sxs-lookup"><span data-stu-id="2862d-602">The SQL query specified for the **SqlReaderQuery** property selects the data in the past hour to copy.</span></span>

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
> <span data-ttu-id="2862d-603">Aby mapować kolumn z zestawu źródła danych do kolumn z obiektu sink zestawu danych, zobacz [mapowania kolumnach dataset w fabryce danych Azure](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="2862d-603">To map columns from source dataset to columns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="2862d-604">Wydajność i dostrajania</span><span class="sxs-lookup"><span data-stu-id="2862d-604">Performance and Tuning</span></span>
<span data-ttu-id="2862d-605">Zobacz [wydajności działania kopiowania & dostrajanie przewodnik](data-factory-copy-activity-performance.md) Aby dowiedzieć się więcej o kluczowych czynników tego wydajność wpływ przenoszenia danych (działanie kopiowania) w usłudze fabryka danych Azure i zoptymalizować ją na różne sposoby.</span><span class="sxs-lookup"><span data-stu-id="2862d-605">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
