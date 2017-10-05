---
title: "Przenieść dane z usługi Amazon Redshift przy użyciu fabryki danych | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat sposobu przenoszenia danych z usługi Amazon Redshift przy użyciu fabryki danych Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 01d15078-58dc-455c-9d9d-98fbdf4ea51e
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jingwang
ms.openlocfilehash: bccb941363952bb2251629240a88148a6527d62e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="move-data-from-amazon-redshift-using-azure-data-factory"></a><span data-ttu-id="85044-103">Przenoszenie danych z Redshift Amazon przy użyciu fabryki danych Azure</span><span class="sxs-lookup"><span data-stu-id="85044-103">Move data From Amazon Redshift using Azure Data Factory</span></span>
<span data-ttu-id="85044-104">W tym artykule opisano sposób używania działania kopiowania w fabryce danych Azure do przenoszenia danych z Amazon Redshift.</span><span class="sxs-lookup"><span data-stu-id="85044-104">This article explains how to use the Copy Activity in Azure Data Factory to move data from Amazon Redshift.</span></span> <span data-ttu-id="85044-105">Artykuł opiera się na [działań przepływu danych](data-factory-data-movement-activities.md) artykułu, który przedstawia ogólny przegląd przenoszenia danych z działania kopiowania.</span><span class="sxs-lookup"><span data-stu-id="85044-105">The article builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span> 

<span data-ttu-id="85044-106">Możesz skopiować dane z Amazon Redshift żadnych obsługiwanych ujścia magazynu danych.</span><span class="sxs-lookup"><span data-stu-id="85044-106">You can copy data from Amazon Redshift to any supported sink data store.</span></span> <span data-ttu-id="85044-107">Lista magazynów danych obsługiwane jako wychwytywanie przez działanie kopiowania, zobacz [obsługiwane magazyny danych](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="85044-107">For a list of data stores supported as sinks by the copy activity, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="85044-108">Fabryka danych obecnie obsługuje przenoszenia danych z Amazon Redshift do innych magazynów danych, ale nie do przenoszenia danych z innych magazynów danych do Amazon Redshift.</span><span class="sxs-lookup"><span data-stu-id="85044-108">Data factory currently supports moving data from Amazon Redshift to other data stores, but not for moving data from other data stores to Amazon Redshift.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="85044-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="85044-109">Prerequisites</span></span>
* <span data-ttu-id="85044-110">Jeśli przenosisz dane z lokalnym magazynem danych, zainstaluj [brama zarządzania danymi](data-factory-data-management-gateway.md) na maszynie lokalnej.</span><span class="sxs-lookup"><span data-stu-id="85044-110">If you are moving data to an on-premises data store, install [Data Management Gateway](data-factory-data-management-gateway.md) on an on-premises machine.</span></span> <span data-ttu-id="85044-111">Następnie przyznać brama zarządzania danymi (Użyj adres IP komputera) dostęp do klastra Amazon Redshift.</span><span class="sxs-lookup"><span data-stu-id="85044-111">Then, Grant Data Management Gateway (use IP address of the machine) the access to Amazon Redshift cluster.</span></span> <span data-ttu-id="85044-112">Zobacz [autoryzowania dostępu do klastra](http://docs.aws.amazon.com/redshift/latest/gsg/rs-gsg-authorize-cluster-access.html) instrukcje.</span><span class="sxs-lookup"><span data-stu-id="85044-112">See [Authorize access to the cluster](http://docs.aws.amazon.com/redshift/latest/gsg/rs-gsg-authorize-cluster-access.html) for instructions.</span></span>
* <span data-ttu-id="85044-113">Jeśli przenosisz dane do magazynu danych Azure, zobacz [zakresy IP centrum danych Azure](https://www.microsoft.com/download/details.aspx?id=41653) koncentruje się na adres IP obliczeniowe i zakresy SQL używane przez usługi Azure data.</span><span class="sxs-lookup"><span data-stu-id="85044-113">If you are moving data to an Azure data store, see [Azure Data Center IP Ranges](https://www.microsoft.com/download/details.aspx?id=41653) for the Compute IP address and SQL ranges used by the Azure data centers.</span></span>

## <a name="getting-started"></a><span data-ttu-id="85044-114">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="85044-114">Getting started</span></span>
<span data-ttu-id="85044-115">Można utworzyć potok z działania kopiowania, który przenosi dane ze źródła Amazon Redshift przy użyciu różnych narzędzi/interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="85044-115">You can create a pipeline with a copy activity that moves data from an Amazon Redshift source by using different tools/APIs.</span></span>

<span data-ttu-id="85044-116">Najprostszym sposobem, aby utworzyć potok jest użycie **kreatora kopiowania**.</span><span class="sxs-lookup"><span data-stu-id="85044-116">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="85044-117">Zobacz [samouczek: tworzenie potoku za pomocą Kreatora kopiowania](data-factory-copy-data-wizard-tutorial.md) szybkie przewodnik dotyczący tworzenia potoku za pomocą Kreatora kopiowania danych.</span><span class="sxs-lookup"><span data-stu-id="85044-117">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="85044-118">Umożliwia także następujące narzędzia do tworzenia potoku: **portalu Azure**, **programu Visual Studio**, **programu Azure PowerShell**, **szablonu usługi Azure Resource Manager**, **interfejs API .NET**, i **interfejsu API REST**.</span><span class="sxs-lookup"><span data-stu-id="85044-118">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="85044-119">Zobacz [samouczek działania kopiowania](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) instrukcje krok po kroku utworzyć potok z działaniem kopiowania.</span><span class="sxs-lookup"><span data-stu-id="85044-119">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="85044-120">Czy można użyć narzędzia i interfejsy API, należy wykonać następujące kroki, aby utworzyć potok, który przenosi dane z magazynu danych źródła do ujścia magazynu danych:</span><span class="sxs-lookup"><span data-stu-id="85044-120">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span> 

1. <span data-ttu-id="85044-121">Utwórz **połączone usługi** Aby połączyć dane wejściowe i wyjściowe są przechowywane w fabryce danych.</span><span class="sxs-lookup"><span data-stu-id="85044-121">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="85044-122">Utwórz **zestawów danych** do reprezentowania danych wejściowych i wyjściowych operacji kopiowania.</span><span class="sxs-lookup"><span data-stu-id="85044-122">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="85044-123">Utwórz **potoku** aktywnością kopiowania zestawu danych jako dane wejściowe i zestawu danych jako dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="85044-123">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="85044-124">Korzystając z kreatora, definicje JSON do tych jednostek fabryki danych (połączone usługi, zestawy danych i potoki) są tworzone automatycznie dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="85044-124">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="85044-125">Korzystając z narzędzi/API (z wyjątkiem interfejs API .NET), należy zdefiniować tych jednostek fabryki danych w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="85044-125">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="85044-126">Dla przykładu z definicji JSON dla jednostek fabryki danych, które są używane do kopiowania danych z magazynu danych Amazon Redshift, zobacz [przykład JSON: kopiowanie danych z Amazon Redshift do obiektów Blob platformy Azure](#json-example-copy-data-from-amazon-redshift-to-azure-blob) sekcji tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="85044-126">For a sample with JSON definitions for Data Factory entities that are used to copy data from an Amazon Redshift data store, see [JSON example: Copy data from Amazon Redshift to Azure Blob](#json-example-copy-data-from-amazon-redshift-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="85044-127">Poniższe sekcje zawierają szczegółowe informacje o właściwości JSON, które są używane do definiowania jednostek fabryki danych określonej do Amazon Redshift:</span><span class="sxs-lookup"><span data-stu-id="85044-127">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Amazon Redshift:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="85044-128">Połączona usługa właściwości</span><span class="sxs-lookup"><span data-stu-id="85044-128">Linked service properties</span></span>
<span data-ttu-id="85044-129">Poniższa tabela zawiera opis specyficzne dla usługi Amazon Redshift połączone elementy JSON.</span><span class="sxs-lookup"><span data-stu-id="85044-129">The following table provides description for JSON elements specific to Amazon Redshift linked service.</span></span>

| <span data-ttu-id="85044-130">Właściwość</span><span class="sxs-lookup"><span data-stu-id="85044-130">Property</span></span> | <span data-ttu-id="85044-131">Opis</span><span class="sxs-lookup"><span data-stu-id="85044-131">Description</span></span> | <span data-ttu-id="85044-132">Wymagane</span><span class="sxs-lookup"><span data-stu-id="85044-132">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="85044-133">type</span><span class="sxs-lookup"><span data-stu-id="85044-133">type</span></span> |<span data-ttu-id="85044-134">Właściwość type musi mieć ustawioną: **AmazonRedshift**.</span><span class="sxs-lookup"><span data-stu-id="85044-134">The type property must be set to: **AmazonRedshift**.</span></span> |<span data-ttu-id="85044-135">Tak</span><span class="sxs-lookup"><span data-stu-id="85044-135">Yes</span></span> |
| <span data-ttu-id="85044-136">serwer</span><span class="sxs-lookup"><span data-stu-id="85044-136">server</span></span> |<span data-ttu-id="85044-137">IP adres lub nazwę hosta serwera Amazon Redshift.</span><span class="sxs-lookup"><span data-stu-id="85044-137">IP address or host name of the Amazon Redshift server.</span></span> |<span data-ttu-id="85044-138">Tak</span><span class="sxs-lookup"><span data-stu-id="85044-138">Yes</span></span> |
| <span data-ttu-id="85044-139">port</span><span class="sxs-lookup"><span data-stu-id="85044-139">port</span></span> |<span data-ttu-id="85044-140">Numer portu TCP używany przez serwer Amazon Redshift do nasłuchiwania dla połączeń klienta.</span><span class="sxs-lookup"><span data-stu-id="85044-140">The number of the TCP port that the Amazon Redshift server uses to listen for client connections.</span></span> |<span data-ttu-id="85044-141">Nie, wartość domyślna: 5439</span><span class="sxs-lookup"><span data-stu-id="85044-141">No, default value: 5439</span></span> |
| <span data-ttu-id="85044-142">Bazy danych</span><span class="sxs-lookup"><span data-stu-id="85044-142">database</span></span> |<span data-ttu-id="85044-143">Nazwa bazy danych Amazon Redshift.</span><span class="sxs-lookup"><span data-stu-id="85044-143">Name of the Amazon Redshift database.</span></span> |<span data-ttu-id="85044-144">Tak</span><span class="sxs-lookup"><span data-stu-id="85044-144">Yes</span></span> |
| <span data-ttu-id="85044-145">nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="85044-145">username</span></span> |<span data-ttu-id="85044-146">Nazwa użytkownika, który ma dostęp do bazy danych.</span><span class="sxs-lookup"><span data-stu-id="85044-146">Name of user who has access to the database.</span></span> |<span data-ttu-id="85044-147">Tak</span><span class="sxs-lookup"><span data-stu-id="85044-147">Yes</span></span> |
| <span data-ttu-id="85044-148">hasło</span><span class="sxs-lookup"><span data-stu-id="85044-148">password</span></span> |<span data-ttu-id="85044-149">Hasło dla konta użytkownika.</span><span class="sxs-lookup"><span data-stu-id="85044-149">Password for the user account.</span></span> |<span data-ttu-id="85044-150">Tak</span><span class="sxs-lookup"><span data-stu-id="85044-150">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="85044-151">Właściwości zestawu danych</span><span class="sxs-lookup"><span data-stu-id="85044-151">Dataset properties</span></span>
<span data-ttu-id="85044-152">Aby uzyskać pełną listę sekcje & właściwości dostępne do definiowania zestawów danych, zobacz [Tworzenie zbiorów danych](data-factory-create-datasets.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="85044-152">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="85044-153">Sekcje, takie jak struktury, dostępności i zasady są podobne dla wszystkich typów obiektów dataset (Azure SQL, obiektów blob platformy Azure, Azure tabeli itp.).</span><span class="sxs-lookup"><span data-stu-id="85044-153">Sections such as structure, availability, and policy are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="85044-154">**TypeProperties** sekcja jest różne dla każdego typu zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="85044-154">The **typeProperties** section is different for each type of dataset.</span></span> <span data-ttu-id="85044-155">Zawiera informacje o lokalizacji danych w magazynie danych.</span><span class="sxs-lookup"><span data-stu-id="85044-155">It provides information about the location of the data in the data store.</span></span> <span data-ttu-id="85044-156">TypeProperties sekcja dla zestawu danych typu **RelationalTable** (w tym Amazon Redshift zestawu danych) ma następujące właściwości</span><span class="sxs-lookup"><span data-stu-id="85044-156">The typeProperties section for dataset of type **RelationalTable** (which includes Amazon Redshift dataset) has the following properties</span></span>

| <span data-ttu-id="85044-157">Właściwość</span><span class="sxs-lookup"><span data-stu-id="85044-157">Property</span></span> | <span data-ttu-id="85044-158">Opis</span><span class="sxs-lookup"><span data-stu-id="85044-158">Description</span></span> | <span data-ttu-id="85044-159">Wymagane</span><span class="sxs-lookup"><span data-stu-id="85044-159">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="85044-160">tableName</span><span class="sxs-lookup"><span data-stu-id="85044-160">tableName</span></span> |<span data-ttu-id="85044-161">Nazwa tabeli w bazie danych Amazon Redshift, odnoszący się do połączonej usługi.</span><span class="sxs-lookup"><span data-stu-id="85044-161">Name of the table in the Amazon Redshift database that linked service refers to.</span></span> |<span data-ttu-id="85044-162">Nie (Jeśli **zapytania** z **RelationalSource** jest określona)</span><span class="sxs-lookup"><span data-stu-id="85044-162">No (if **query** of **RelationalSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="85044-163">Właściwości działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="85044-163">Copy activity properties</span></span>
<span data-ttu-id="85044-164">Pełną listę sekcje & właściwości dostępne do definiowania działań, zobacz [tworzenie potoków](data-factory-create-pipelines.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="85044-164">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="85044-165">Właściwości, takie jak nazwa, opis, dane wejściowe i wyjściowe tabel i zasady są dostępne dla wszystkich typów działań.</span><span class="sxs-lookup"><span data-stu-id="85044-165">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

<span data-ttu-id="85044-166">Właściwości dostępne w **typeProperties** sekcji działania zależne od każdego typu działania.</span><span class="sxs-lookup"><span data-stu-id="85044-166">Whereas, properties available in the **typeProperties** section of the activity vary with each activity type.</span></span> <span data-ttu-id="85044-167">Dla działania kopiowania różnią się w zależności od typów źródeł i sink.</span><span class="sxs-lookup"><span data-stu-id="85044-167">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="85044-168">Gdy źródło działanie kopiowania jest typu **RelationalSource** (która obejmuje usługi Amazon Redshift), w sekcji typeProperties dostępne są następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="85044-168">When source of copy activity is of type **RelationalSource** (which includes Amazon Redshift), the following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="85044-169">Właściwość</span><span class="sxs-lookup"><span data-stu-id="85044-169">Property</span></span> | <span data-ttu-id="85044-170">Opis</span><span class="sxs-lookup"><span data-stu-id="85044-170">Description</span></span> | <span data-ttu-id="85044-171">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="85044-171">Allowed values</span></span> | <span data-ttu-id="85044-172">Wymagane</span><span class="sxs-lookup"><span data-stu-id="85044-172">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="85044-173">query</span><span class="sxs-lookup"><span data-stu-id="85044-173">query</span></span> |<span data-ttu-id="85044-174">Użyj niestandardowych zapytania można odczytać danych.</span><span class="sxs-lookup"><span data-stu-id="85044-174">Use the custom query to read data.</span></span> |<span data-ttu-id="85044-175">Ciąg zapytania SQL.</span><span class="sxs-lookup"><span data-stu-id="85044-175">SQL query string.</span></span> <span data-ttu-id="85044-176">Na przykład: Wybierz * z MyTable.</span><span class="sxs-lookup"><span data-stu-id="85044-176">For example: select * from MyTable.</span></span> |<span data-ttu-id="85044-177">Nie (Jeśli **tableName** z **dataset** jest określona)</span><span class="sxs-lookup"><span data-stu-id="85044-177">No (if **tableName** of **dataset** is specified)</span></span> |

## <a name="json-example-copy-data-from-amazon-redshift-to-azure-blob"></a><span data-ttu-id="85044-178">Przykład JSON: kopiowanie danych z Amazon Redshift do obiektów Blob platformy Azure</span><span class="sxs-lookup"><span data-stu-id="85044-178">JSON example: Copy data from Amazon Redshift to Azure Blob</span></span>
<span data-ttu-id="85044-179">W tym przykładzie pokazano, jak skopiować dane z bazy danych Amazon Redshift do magazynu obiektów Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="85044-179">This sample shows how to copy data from an Amazon Redshift database to an Azure Blob Storage.</span></span> <span data-ttu-id="85044-180">Jednak dane mogą być kopiowane **bezpośrednio** do dowolnego wychwytywanie podane [tutaj](data-factory-data-movement-activities.md#supported-data-stores-and-formats) za pomocą działania kopiowania w fabryce danych Azure.</span><span class="sxs-lookup"><span data-stu-id="85044-180">However, data can be copied **directly** to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>  

<span data-ttu-id="85044-181">Przykład zawiera następujące obiekty fabryki danych:</span><span class="sxs-lookup"><span data-stu-id="85044-181">The sample has the following data factory entities:</span></span>

* <span data-ttu-id="85044-182">Połączonej usługi typu [AmazonRedshift](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="85044-182">A linked service of type [AmazonRedshift](#linked-service-properties).</span></span>
* <span data-ttu-id="85044-183">Połączonej usługi typu [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="85044-183">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="85044-184">Dane wejściowe [dataset](data-factory-create-datasets.md) typu [RelationalTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="85044-184">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](#dataset-properties).</span></span>
* <span data-ttu-id="85044-185">Dane wyjściowe [dataset](data-factory-create-datasets.md) typu [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="85044-185">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="85044-186">A [potoku](data-factory-create-pipelines.md) z działaniem kopii, która używa [RelationalSource](#copy-activity-properties) i [BlobSink](data-factory-azure-blob-connector.md##copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="85044-186">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md##copy-activity-properties).</span></span>

<span data-ttu-id="85044-187">Przykład kopiuje dane z wyniku kwerendy w Amazon Redshift do obiektu blob co godzinę.</span><span class="sxs-lookup"><span data-stu-id="85044-187">The sample copies data from a query result in Amazon Redshift to a blob every hour.</span></span> <span data-ttu-id="85044-188">Właściwości JSON używane w te przykłady są opisane w sekcjach poniżej próbek.</span><span class="sxs-lookup"><span data-stu-id="85044-188">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="85044-189">**Amazon Redshift połączonej usługi:**</span><span class="sxs-lookup"><span data-stu-id="85044-189">**Amazon Redshift linked service:**</span></span>

```json
{
    "name": "AmazonRedshiftLinkedService",
    "properties":
    {
        "type": "AmazonRedshift",
        "typeProperties":
        {
            "server": "< The IP address or host name of the Amazon Redshift server >",
            "port": <The number of the TCP port that the Amazon Redshift server uses to listen for client connections.>,
            "database": "<The database name of the Amazon Redshift database>",
            "username": "<username>",
            "password": "<password>"
        }
    }
}
```

<span data-ttu-id="85044-190">**Połączonej usługi magazynu Azure:**</span><span class="sxs-lookup"><span data-stu-id="85044-190">**Azure Storage linked service:**</span></span>

```json
{
  "name": "AzureStorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```
<span data-ttu-id="85044-191">**Zestaw danych wejściowych Amazon Redshift:**</span><span class="sxs-lookup"><span data-stu-id="85044-191">**Amazon Redshift input dataset:**</span></span>

<span data-ttu-id="85044-192">Ustawienie `"external": true` usługi fabryka danych informuje, czy zestaw danych jest zewnętrzne do fabryki danych i nie jest generowany przez działanie w fabryce danych.</span><span class="sxs-lookup"><span data-stu-id="85044-192">Setting `"external": true` informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span> <span data-ttu-id="85044-193">Ustaw tę właściwość na wartość true w wejściowy zestaw danych, który nie jest generowany przez działania w potoku.</span><span class="sxs-lookup"><span data-stu-id="85044-193">Set this property to true on an input dataset that is not produced by an activity in the pipeline.</span></span>

```json
{
    "name": "AmazonRedshiftInputDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "AmazonRedshiftLinkedService",
        "typeProperties": {
            "tableName": "<Table name>"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

<span data-ttu-id="85044-194">**Azure Blob wyjściowy zestaw danych:**</span><span class="sxs-lookup"><span data-stu-id="85044-194">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="85044-195">Dane są zapisywane do nowego obiektu blob co godzinę (częstotliwość: godziny, interwał: 1).</span><span class="sxs-lookup"><span data-stu-id="85044-195">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="85044-196">Ścieżka folderu dla obiekt blob jest dynamicznie obliczane na podstawie czasu rozpoczęcia wycinek, który jest przetwarzana.</span><span class="sxs-lookup"><span data-stu-id="85044-196">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="85044-197">Ścieżka folderu używa rok, miesiąc, dzień i godziny części czas rozpoczęcia.</span><span class="sxs-lookup"><span data-stu-id="85044-197">The folder path uses year, month, day, and hours parts of the start time.</span></span>

```json
{
    "name": "AzureBlobOutputDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/fromamazonredshift/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
            },
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
            ]
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="85044-198">**Działanie kopiowania w potoku ze źródłem Azure Redshift (RelationalSource) i ujście obiektów Blob:**</span><span class="sxs-lookup"><span data-stu-id="85044-198">**Copy activity in a pipeline with Azure Redshift source (RelationalSource) and Blob sink:**</span></span>

<span data-ttu-id="85044-199">Potok zawiera działanie kopiowania, który jest skonfigurowany do używania wejściowe i wyjściowe zestawy danych i jest zaplanowane co godzinę.</span><span class="sxs-lookup"><span data-stu-id="85044-199">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="85044-200">W definicji JSON potoku **źródła** ustawiono typ **RelationalSource** i **zbiornika** ustawiono typ **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="85044-200">In the pipeline JSON definition, the **source** type is set to **RelationalSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="85044-201">Określony dla zapytania SQL **zapytania** właściwości wybiera dane w ostatniej godziny do skopiowania.</span><span class="sxs-lookup"><span data-stu-id="85044-201">The SQL query specified for the **query** property selects the data in the past hour to copy.</span></span>

```json
{
    "name": "CopyAmazonRedshiftToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', WindowStart, WindowEnd)"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "AmazonRedshiftInputDataset"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOutputDataSet"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "AmazonRedshiftToBlob"
            }
        ],
        "start": "2014-06-01T18:00:00Z",
        "end": "2014-06-01T19:00:00Z"
    }
}
```
### <a name="type-mapping-for-amazon-redshift"></a><span data-ttu-id="85044-202">Mapowanie typu dla Amazon Redshift</span><span class="sxs-lookup"><span data-stu-id="85044-202">Type mapping for Amazon Redshift</span></span>
<span data-ttu-id="85044-203">Jak wspomniano w [działań przepływu danych](data-factory-data-movement-activities.md) artykułu, automatyczne konwersje z typów źródła do zbiornika typy z następujących rozwinięcie wykonuje działania kopiowania:</span><span class="sxs-lookup"><span data-stu-id="85044-203">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following two-step approach:</span></span>

1. <span data-ttu-id="85044-204">Konwertowanie typów natywnych źródła na typ architektury .NET</span><span class="sxs-lookup"><span data-stu-id="85044-204">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="85044-205">Konwertowanie na typ macierzysty ujścia typ architektury .NET</span><span class="sxs-lookup"><span data-stu-id="85044-205">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="85044-206">Podczas przenoszenia danych do Amazon Redshift, następujące mapowania są używane z typów Amazon Redshift do typów .NET.</span><span class="sxs-lookup"><span data-stu-id="85044-206">When moving data to Amazon Redshift, the following mappings are used from Amazon Redshift types to .NET types.</span></span>

| <span data-ttu-id="85044-207">Typ Redshift Amazon</span><span class="sxs-lookup"><span data-stu-id="85044-207">Amazon Redshift Type</span></span> | <span data-ttu-id="85044-208">Typ na podstawie .NET</span><span class="sxs-lookup"><span data-stu-id="85044-208">.NET Based Type</span></span> |
| --- | --- |
| <span data-ttu-id="85044-209">SMALLINT</span><span class="sxs-lookup"><span data-stu-id="85044-209">SMALLINT</span></span> |<span data-ttu-id="85044-210">Int16</span><span class="sxs-lookup"><span data-stu-id="85044-210">Int16</span></span> |
| <span data-ttu-id="85044-211">LICZBA CAŁKOWITA</span><span class="sxs-lookup"><span data-stu-id="85044-211">INTEGER</span></span> |<span data-ttu-id="85044-212">Int32</span><span class="sxs-lookup"><span data-stu-id="85044-212">Int32</span></span> |
| <span data-ttu-id="85044-213">BIGINT</span><span class="sxs-lookup"><span data-stu-id="85044-213">BIGINT</span></span> |<span data-ttu-id="85044-214">Int64</span><span class="sxs-lookup"><span data-stu-id="85044-214">Int64</span></span> |
| <span data-ttu-id="85044-215">DECIMAL</span><span class="sxs-lookup"><span data-stu-id="85044-215">DECIMAL</span></span> |<span data-ttu-id="85044-216">Decimal</span><span class="sxs-lookup"><span data-stu-id="85044-216">Decimal</span></span> |
| <span data-ttu-id="85044-217">RZECZYWISTE</span><span class="sxs-lookup"><span data-stu-id="85044-217">REAL</span></span> |<span data-ttu-id="85044-218">Pojedynczy</span><span class="sxs-lookup"><span data-stu-id="85044-218">Single</span></span> |
| <span data-ttu-id="85044-219">PODWÓJNEJ PRECYZJI</span><span class="sxs-lookup"><span data-stu-id="85044-219">DOUBLE PRECISION</span></span> |<span data-ttu-id="85044-220">O podwójnej precyzji</span><span class="sxs-lookup"><span data-stu-id="85044-220">Double</span></span> |
| <span data-ttu-id="85044-221">WARTOŚĆ LOGICZNA</span><span class="sxs-lookup"><span data-stu-id="85044-221">BOOLEAN</span></span> |<span data-ttu-id="85044-222">Ciąg</span><span class="sxs-lookup"><span data-stu-id="85044-222">String</span></span> |
| <span data-ttu-id="85044-223">CHAR</span><span class="sxs-lookup"><span data-stu-id="85044-223">CHAR</span></span> |<span data-ttu-id="85044-224">Ciąg</span><span class="sxs-lookup"><span data-stu-id="85044-224">String</span></span> |
| <span data-ttu-id="85044-225">VARCHAR</span><span class="sxs-lookup"><span data-stu-id="85044-225">VARCHAR</span></span> |<span data-ttu-id="85044-226">Ciąg</span><span class="sxs-lookup"><span data-stu-id="85044-226">String</span></span> |
| <span data-ttu-id="85044-227">DATA</span><span class="sxs-lookup"><span data-stu-id="85044-227">DATE</span></span> |<span data-ttu-id="85044-228">Data i godzina</span><span class="sxs-lookup"><span data-stu-id="85044-228">DateTime</span></span> |
| <span data-ttu-id="85044-229">ZNACZNIK CZASU</span><span class="sxs-lookup"><span data-stu-id="85044-229">TIMESTAMP</span></span> |<span data-ttu-id="85044-230">Data i godzina</span><span class="sxs-lookup"><span data-stu-id="85044-230">DateTime</span></span> |
| <span data-ttu-id="85044-231">TEKST</span><span class="sxs-lookup"><span data-stu-id="85044-231">TEXT</span></span> |<span data-ttu-id="85044-232">Ciąg</span><span class="sxs-lookup"><span data-stu-id="85044-232">String</span></span> |

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="85044-233">Obiekt sink kolumn mapy źródła</span><span class="sxs-lookup"><span data-stu-id="85044-233">Map source to sink columns</span></span>
<span data-ttu-id="85044-234">Aby uzyskać informacje dotyczące mapowania kolumn w zestawie źródła danych do kolumn w zestawie danych zbiornika, zobacz [mapowania kolumnach dataset w fabryce danych Azure](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="85044-234">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="85044-235">Odczyt powtarzalny ze źródłami relacyjnymi</span><span class="sxs-lookup"><span data-stu-id="85044-235">Repeatable read from relational sources</span></span>
<span data-ttu-id="85044-236">Podczas kopiowania danych z danych relacyjnych przechowuje, należy pamiętać, aby uniknąć niezamierzone wyniki powtarzalności.</span><span class="sxs-lookup"><span data-stu-id="85044-236">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="85044-237">Fabryka danych Azure możesz ponownie ręcznie wycinek.</span><span class="sxs-lookup"><span data-stu-id="85044-237">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="85044-238">Można również skonfigurować zasady ponawiania dla zestawu danych, aby wycinek jest uruchamiany ponownie, gdy wystąpi błąd.</span><span class="sxs-lookup"><span data-stu-id="85044-238">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="85044-239">Podczas wycinek zostanie uruchomiona ponownie w obu przypadkach, należy się upewnić, że te same dane jest do odczytu niezależnie od tego, ile razy wycinek jest uruchamiany.</span><span class="sxs-lookup"><span data-stu-id="85044-239">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="85044-240">Zobacz [Repeatable odczytywać relacyjne źródła](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)</span><span class="sxs-lookup"><span data-stu-id="85044-240">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="85044-241">Wydajność i dostrajania</span><span class="sxs-lookup"><span data-stu-id="85044-241">Performance and Tuning</span></span>
<span data-ttu-id="85044-242">Zobacz [wydajności działania kopiowania & dostrajanie przewodnik](data-factory-copy-activity-performance.md) Aby dowiedzieć się więcej o kluczowych czynników tego wydajność wpływ przenoszenia danych (działanie kopiowania) w usłudze fabryka danych Azure i zoptymalizować ją na różne sposoby.</span><span class="sxs-lookup"><span data-stu-id="85044-242">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="85044-243">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="85044-243">Next Steps</span></span>
<span data-ttu-id="85044-244">Zobacz następujące artykuły:</span><span class="sxs-lookup"><span data-stu-id="85044-244">See the following articles:</span></span>

* <span data-ttu-id="85044-245">[Samouczek działania kopiowania](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) instrukcje krok po kroku do tworzenia potoku z działania kopiowania.</span><span class="sxs-lookup"><span data-stu-id="85044-245">[Copy Activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions for creating a pipeline with a Copy Activity.</span></span>
