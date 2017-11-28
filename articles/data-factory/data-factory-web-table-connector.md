---
title: "Przenoszenie danych z tabeli sieci Web przy użyciu fabryki danych Azure | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat sposobu przenoszenia danych z tabeli na stronie sieci Web przy użyciu fabryki danych Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: f54a26a4-baa4-4255-9791-5a8f935898e2
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jingwang
ms.openlocfilehash: 9e006bc7289fa0239f1650ac6ad43dd159e3c7e0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="move-data-from-a-web-table-source-using-azure-data-factory"></a><span data-ttu-id="0ef79-103">Przenoszenie danych ze źródła tabeli sieci Web przy użyciu fabryki danych Azure</span><span class="sxs-lookup"><span data-stu-id="0ef79-103">Move data from a Web table source using Azure Data Factory</span></span>
<span data-ttu-id="0ef79-104">Ten artykuł przedstawia sposób użycia działanie kopiowania w fabryce danych Azure do przenoszenia danych z tabeli na stronie sieci Web w magazynie danych obsługiwanych ujścia.</span><span class="sxs-lookup"><span data-stu-id="0ef79-104">This article outlines how to use the Copy Activity in Azure Data Factory to move data from a table in a Web page to a supported sink data store.</span></span> <span data-ttu-id="0ef79-105">W tym artykule opiera się na [działań przepływu danych](data-factory-data-movement-activities.md) artykułu, który przedstawia ogólne omówienie przepływu danych działanie kopiowania i listę magazynów danych są obsługiwane jako źródła/sink.</span><span class="sxs-lookup"><span data-stu-id="0ef79-105">This article builds on the [data movement activities](data-factory-data-movement-activities.md) article that presents a general overview of data movement with copy activity and the list of data stores supported as sources/sinks.</span></span>

<span data-ttu-id="0ef79-106">Fabryka danych aktualnie obsługuje tylko przenoszenia danych z tabeli sieci Web do innych magazynów danych, ale nie przenoszenia danych z innych danych są przechowywane w tabeli docelowej lokalizacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="0ef79-106">Data factory currently supports only moving data from a Web table to other data stores, but not moving data from other data stores to a Web table destination.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0ef79-107">Ten łącznik sieci Web obsługuje obecnie tylko wyodrębnianie zawartości tabeli ze strony HTML.</span><span class="sxs-lookup"><span data-stu-id="0ef79-107">This Web connector currently supports only extracting table content from an HTML page.</span></span> <span data-ttu-id="0ef79-108">Aby pobrać dane z punktu końcowego protokołu HTTP/s, użyj [łącznika HTTP](data-factory-http-connector.md) zamiast tego.</span><span class="sxs-lookup"><span data-stu-id="0ef79-108">To retrieve data from a HTTP/s endpoint, use [HTTP connector](data-factory-http-connector.md) instead.</span></span>

## <a name="getting-started"></a><span data-ttu-id="0ef79-109">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="0ef79-109">Getting started</span></span>
<span data-ttu-id="0ef79-110">Można utworzyć potok z działania kopiowania, który przenosi dane z magazynu lokalnego Cassandra danych przy użyciu różnych narzędzi/interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="0ef79-110">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="0ef79-111">Najprostszym sposobem, aby utworzyć potok jest użycie **kreatora kopiowania**.</span><span class="sxs-lookup"><span data-stu-id="0ef79-111">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="0ef79-112">Zobacz [samouczek: tworzenie potoku za pomocą Kreatora kopiowania](data-factory-copy-data-wizard-tutorial.md) szybkie przewodnik dotyczący tworzenia potoku za pomocą Kreatora kopiowania danych.</span><span class="sxs-lookup"><span data-stu-id="0ef79-112">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span> 
- <span data-ttu-id="0ef79-113">Umożliwia także następujące narzędzia do tworzenia potoku: **portalu Azure**, **programu Visual Studio**, **programu Azure PowerShell**, **szablonu usługi Azure Resource Manager**, **interfejs API .NET**, i **interfejsu API REST**.</span><span class="sxs-lookup"><span data-stu-id="0ef79-113">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="0ef79-114">Zobacz [samouczek działania kopiowania](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) instrukcje krok po kroku utworzyć potok z działaniem kopiowania.</span><span class="sxs-lookup"><span data-stu-id="0ef79-114">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="0ef79-115">Czy można użyć narzędzia i interfejsy API, należy wykonać następujące kroki, aby utworzyć potok, który przenosi dane z magazynu danych źródła do ujścia magazynu danych:</span><span class="sxs-lookup"><span data-stu-id="0ef79-115">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="0ef79-116">Utwórz **połączone usługi** Aby połączyć dane wejściowe i wyjściowe są przechowywane w fabryce danych.</span><span class="sxs-lookup"><span data-stu-id="0ef79-116">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="0ef79-117">Utwórz **zestawów danych** do reprezentowania danych wejściowych i wyjściowych operacji kopiowania.</span><span class="sxs-lookup"><span data-stu-id="0ef79-117">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="0ef79-118">Utwórz **potoku** aktywnością kopiowania zestawu danych jako dane wejściowe i zestawu danych jako dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="0ef79-118">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="0ef79-119">Korzystając z kreatora, definicje JSON do tych jednostek fabryki danych (połączone usługi, zestawy danych i potoki) są tworzone automatycznie dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="0ef79-119">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="0ef79-120">Korzystając z narzędzi/API (z wyjątkiem interfejs API .NET), należy zdefiniować tych jednostek fabryki danych w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="0ef79-120">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="0ef79-121">Dla przykładu z definicji JSON dla jednostek fabryki danych, które są używane do skopiowania danych z tabeli sieci web, zobacz [przykład JSON: kopiowanie danych z tabeli sieci Web do obiektów Blob platformy Azure](#json-example-copy-data-from-web-table-to-azure-blob) sekcji tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="0ef79-121">For a sample with JSON definitions for Data Factory entities that are used to copy data from a web table, see [JSON example: Copy data from Web table to Azure Blob](#json-example-copy-data-from-web-table-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="0ef79-122">Poniższe sekcje zawierają szczegółowe informacje o właściwości JSON, które są używane do definiowania jednostek fabryki danych określonej do tabeli sieci Web:</span><span class="sxs-lookup"><span data-stu-id="0ef79-122">The following sections provide details about JSON properties that are used to define Data Factory entities specific to a Web table:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="0ef79-123">Połączona usługa właściwości</span><span class="sxs-lookup"><span data-stu-id="0ef79-123">Linked service properties</span></span>
<span data-ttu-id="0ef79-124">Poniższa tabela zawiera opis elementów JSON specyficzne dla połączonej usługi sieci Web.</span><span class="sxs-lookup"><span data-stu-id="0ef79-124">The following table provides description for JSON elements specific to Web linked service.</span></span>

| <span data-ttu-id="0ef79-125">Właściwość</span><span class="sxs-lookup"><span data-stu-id="0ef79-125">Property</span></span> | <span data-ttu-id="0ef79-126">Opis</span><span class="sxs-lookup"><span data-stu-id="0ef79-126">Description</span></span> | <span data-ttu-id="0ef79-127">Wymagane</span><span class="sxs-lookup"><span data-stu-id="0ef79-127">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0ef79-128">type</span><span class="sxs-lookup"><span data-stu-id="0ef79-128">type</span></span> |<span data-ttu-id="0ef79-129">Właściwość type musi mieć ustawioną: **sieci Web**</span><span class="sxs-lookup"><span data-stu-id="0ef79-129">The type property must be set to: **Web**</span></span> |<span data-ttu-id="0ef79-130">Tak</span><span class="sxs-lookup"><span data-stu-id="0ef79-130">Yes</span></span> |
| <span data-ttu-id="0ef79-131">Url</span><span class="sxs-lookup"><span data-stu-id="0ef79-131">Url</span></span> |<span data-ttu-id="0ef79-132">Adres URL źródła w sieci Web</span><span class="sxs-lookup"><span data-stu-id="0ef79-132">URL to the Web source</span></span> |<span data-ttu-id="0ef79-133">Tak</span><span class="sxs-lookup"><span data-stu-id="0ef79-133">Yes</span></span> |
| <span data-ttu-id="0ef79-134">Typ authenticationType</span><span class="sxs-lookup"><span data-stu-id="0ef79-134">authenticationType</span></span> |<span data-ttu-id="0ef79-135">Anonimowe.</span><span class="sxs-lookup"><span data-stu-id="0ef79-135">Anonymous.</span></span> |<span data-ttu-id="0ef79-136">Tak</span><span class="sxs-lookup"><span data-stu-id="0ef79-136">Yes</span></span> |

### <a name="using-anonymous-authentication"></a><span data-ttu-id="0ef79-137">Przy użyciu uwierzytelniania anonimowego</span><span class="sxs-lookup"><span data-stu-id="0ef79-137">Using Anonymous authentication</span></span>

```json
{
    "name": "web",
    "properties":
    {
        "type": "Web",
        "typeProperties":
        {
            "authenticationType": "Anonymous",
            "url" : "https://en.wikipedia.org/wiki/"
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="0ef79-138">Właściwości zestawu danych</span><span class="sxs-lookup"><span data-stu-id="0ef79-138">Dataset properties</span></span>
<span data-ttu-id="0ef79-139">Aby uzyskać pełną listę sekcje & właściwości dostępne do definiowania zestawów danych, zobacz [Tworzenie zbiorów danych](data-factory-create-datasets.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="0ef79-139">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="0ef79-140">Sekcje zawierają informacje, takie jak struktury, dostępności i zasad zestawu danych JSON są podobne dla wszystkich typów obiektów dataset (Azure SQL, obiektów blob platformy Azure, Azure tabeli itp.).</span><span class="sxs-lookup"><span data-stu-id="0ef79-140">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="0ef79-141">**TypeProperties** sekcja jest różne dla każdego typu zestawu danych i zawiera informacje o lokalizacji danych w magazynie danych.</span><span class="sxs-lookup"><span data-stu-id="0ef79-141">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="0ef79-142">TypeProperties sekcja dla zestawu danych typu **tabeli WebTable** ma następujące właściwości</span><span class="sxs-lookup"><span data-stu-id="0ef79-142">The typeProperties section for dataset of type **WebTable** has the following properties</span></span>

| <span data-ttu-id="0ef79-143">Właściwość</span><span class="sxs-lookup"><span data-stu-id="0ef79-143">Property</span></span> | <span data-ttu-id="0ef79-144">Opis</span><span class="sxs-lookup"><span data-stu-id="0ef79-144">Description</span></span> | <span data-ttu-id="0ef79-145">Wymagane</span><span class="sxs-lookup"><span data-stu-id="0ef79-145">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="0ef79-146">type</span><span class="sxs-lookup"><span data-stu-id="0ef79-146">type</span></span> |<span data-ttu-id="0ef79-147">Typ zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="0ef79-147">type of the dataset.</span></span> <span data-ttu-id="0ef79-148">należy wybrać opcję **tabeli WebTable**</span><span class="sxs-lookup"><span data-stu-id="0ef79-148">must be set to **WebTable**</span></span> |<span data-ttu-id="0ef79-149">Tak</span><span class="sxs-lookup"><span data-stu-id="0ef79-149">Yes</span></span> |
| <span data-ttu-id="0ef79-150">Ścieżka</span><span class="sxs-lookup"><span data-stu-id="0ef79-150">path</span></span> |<span data-ttu-id="0ef79-151">Względny adres URL do zasobu, który zawiera tabelę.</span><span class="sxs-lookup"><span data-stu-id="0ef79-151">A relative URL to the resource that contains the table.</span></span> |<span data-ttu-id="0ef79-152">Nie.</span><span class="sxs-lookup"><span data-stu-id="0ef79-152">No.</span></span> <span data-ttu-id="0ef79-153">Jeśli ścieżka nie jest określona, używana jest tylko adres URL określony w definicji połączonej usługi.</span><span class="sxs-lookup"><span data-stu-id="0ef79-153">When path is not specified, only the URL specified in the linked service definition is used.</span></span> |
| <span data-ttu-id="0ef79-154">Indeks</span><span class="sxs-lookup"><span data-stu-id="0ef79-154">index</span></span> |<span data-ttu-id="0ef79-155">Indeks tabeli w zasobie.</span><span class="sxs-lookup"><span data-stu-id="0ef79-155">The index of the table in the resource.</span></span> <span data-ttu-id="0ef79-156">Zobacz [Get indeksu tabeli na stronie HTML](#get-index-of-a-table-in-an-html-page) sekcji, aby instrukcje dotyczące pobierania indeksu tabeli na stronie HTML.</span><span class="sxs-lookup"><span data-stu-id="0ef79-156">See [Get index of a table in an HTML page](#get-index-of-a-table-in-an-html-page) section for steps to getting index of a table in an HTML page.</span></span> |<span data-ttu-id="0ef79-157">Tak</span><span class="sxs-lookup"><span data-stu-id="0ef79-157">Yes</span></span> |

<span data-ttu-id="0ef79-158">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="0ef79-158">**Example:**</span></span>

```json
{
    "name": "WebTableInput",
    "properties": {
        "type": "WebTable",
        "linkedServiceName": "WebLinkedService",
        "typeProperties": {
            "index": 1,
            "path": "AFI's_100_Years...100_Movies"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}
```

## <a name="copy-activity-properties"></a><span data-ttu-id="0ef79-159">Właściwości działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="0ef79-159">Copy activity properties</span></span>
<span data-ttu-id="0ef79-160">Pełną listę sekcje & właściwości dostępne do definiowania działań, zobacz [tworzenie potoków](data-factory-create-pipelines.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="0ef79-160">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="0ef79-161">Właściwości, takie jak nazwa, opis, dane wejściowe i wyjściowe tabel i zasady są dostępne dla wszystkich typów działań.</span><span class="sxs-lookup"><span data-stu-id="0ef79-161">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="0ef79-162">Właściwości, które są dostępne w sekcji typeProperties działania różnić się z każdym typem działania.</span><span class="sxs-lookup"><span data-stu-id="0ef79-162">Whereas, properties available in the typeProperties section of the activity vary with each activity type.</span></span> <span data-ttu-id="0ef79-163">Dla działania kopiowania różnią się w zależności od typów źródeł i sink.</span><span class="sxs-lookup"><span data-stu-id="0ef79-163">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="0ef79-164">Obecnie, gdy źródła w przypadku działania kopiowania jest typu **WebSource**, są obsługiwane żadne dodatkowe właściwości.</span><span class="sxs-lookup"><span data-stu-id="0ef79-164">Currently, when the source in copy activity is of type **WebSource**, no additional properties are supported.</span></span>


## <a name="json-example-copy-data-from-web-table-to-azure-blob"></a><span data-ttu-id="0ef79-165">Przykład JSON: kopiowanie danych z tabeli sieci Web do obiektów Blob platformy Azure</span><span class="sxs-lookup"><span data-stu-id="0ef79-165">JSON example: Copy data from Web table to Azure Blob</span></span>
<span data-ttu-id="0ef79-166">Poniższy przykład przedstawia:</span><span class="sxs-lookup"><span data-stu-id="0ef79-166">The following sample shows:</span></span>

1. <span data-ttu-id="0ef79-167">Połączonej usługi typu [Web](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="0ef79-167">A linked service of type [Web](#linked-service-properties).</span></span>
2. <span data-ttu-id="0ef79-168">Połączonej usługi typu [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="0ef79-168">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="0ef79-169">Dane wejściowe [dataset](data-factory-create-datasets.md) typu [tabeli WebTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="0ef79-169">An input [dataset](data-factory-create-datasets.md) of type [WebTable](#dataset-properties).</span></span>
4. <span data-ttu-id="0ef79-170">Dane wyjściowe [dataset](data-factory-create-datasets.md) typu [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="0ef79-170">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="0ef79-171">A [potoku](data-factory-create-pipelines.md) z działaniem kopii, która używa [WebSource](#copy-activity-properties) i [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="0ef79-171">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [WebSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="0ef79-172">Przykład kopiuje dane z tabeli sieci Web do obiektów blob platformy Azure co godzinę.</span><span class="sxs-lookup"><span data-stu-id="0ef79-172">The sample copies data from a Web table to an Azure blob every hour.</span></span> <span data-ttu-id="0ef79-173">Właściwości JSON używane w te przykłady są opisane w sekcjach poniżej próbek.</span><span class="sxs-lookup"><span data-stu-id="0ef79-173">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="0ef79-174">Poniższy przykład pokazuje, jak można skopiować danych z tabeli sieci Web do obiektów blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="0ef79-174">The following sample shows how to copy data from a Web table to an Azure blob.</span></span> <span data-ttu-id="0ef79-175">Jednak dane mogą być kopiowane bezpośrednio do wychwytywanie w [działań przepływu danych](data-factory-data-movement-activities.md) artykułu za pomocą działania kopiowania w fabryce danych Azure.</span><span class="sxs-lookup"><span data-stu-id="0ef79-175">However, data can be copied directly to any of the sinks stated in the [Data Movement Activities](data-factory-data-movement-activities.md) article by using the Copy Activity in Azure Data Factory.</span></span>

<span data-ttu-id="0ef79-176">**Sieci Web połączonej usługi** w tym przykładzie korzysta z usługi sieci Web połączone przy użyciu uwierzytelniania anonimowego.</span><span class="sxs-lookup"><span data-stu-id="0ef79-176">**Web linked service** This example uses the Web linked service with anonymous authentication.</span></span> <span data-ttu-id="0ef79-177">Zobacz [sieci Web połączonej usługi](#linked-service-properties) sekcji dla różnych typów uwierzytelniania, można użyć.</span><span class="sxs-lookup"><span data-stu-id="0ef79-177">See [Web linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

```json
{
    "name": "WebLinkedService",
    "properties":
    {
        "type": "Web",
        "typeProperties":
        {
            "authenticationType": "Anonymous",
            "url" : "https://en.wikipedia.org/wiki/"
        }
    }
}
```

<span data-ttu-id="0ef79-178">**Połączona usługa Azure Storage**</span><span class="sxs-lookup"><span data-stu-id="0ef79-178">**Azure Storage linked service**</span></span>

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

<span data-ttu-id="0ef79-179">**Wejściowy zestaw danych tabeli WebTable** ustawienie **zewnętrznych** do **true** usługi fabryka danych informuje, czy zestaw danych jest zewnętrzne do fabryki danych i nie jest generowany przez działanie w danych fabryka.</span><span class="sxs-lookup"><span data-stu-id="0ef79-179">**WebTable input dataset** Setting **external** to **true** informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

> [!NOTE]
> <span data-ttu-id="0ef79-180">Zobacz [Get indeksu tabeli na stronie HTML](#get-index-of-a-table-in-an-html-page) sekcji, aby instrukcje dotyczące pobierania indeksu tabeli na stronie HTML.</span><span class="sxs-lookup"><span data-stu-id="0ef79-180">See [Get index of a table in an HTML page](#get-index-of-a-table-in-an-html-page) section for steps to getting index of a table in an HTML page.</span></span>  
>
>

```json
{
    "name": "WebTableInput",
    "properties": {
        "type": "WebTable",
        "linkedServiceName": "WebLinkedService",
        "typeProperties": {
            "index": 1,
            "path": "AFI's_100_Years...100_Movies"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}
```


<span data-ttu-id="0ef79-181">**Azure Blob wyjściowy zestaw danych**</span><span class="sxs-lookup"><span data-stu-id="0ef79-181">**Azure Blob output dataset**</span></span>

<span data-ttu-id="0ef79-182">Dane są zapisywane do nowego obiektu blob co godzinę (częstotliwość: godziny, interwał: 1).</span><span class="sxs-lookup"><span data-stu-id="0ef79-182">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span>

```json
{
    "name": "AzureBlobOutput",
    "properties":
    {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties":
        {
            "folderPath": "adfgetstarted/Movies"
        },
        "availability":
        {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```



<span data-ttu-id="0ef79-183">**W potoku z działanie kopiowania**</span><span class="sxs-lookup"><span data-stu-id="0ef79-183">**Pipeline with Copy activity**</span></span>

<span data-ttu-id="0ef79-184">Potok zawiera działanie kopiowania, który jest skonfigurowany do używania wejściowe i wyjściowe zestawy danych i jest zaplanowane co godzinę.</span><span class="sxs-lookup"><span data-stu-id="0ef79-184">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="0ef79-185">W definicji JSON potoku **źródła** ustawiono typ **WebSource** i **zbiornika** ustawiono typ **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="0ef79-185">In the pipeline JSON definition, the **source** type is set to **WebSource** and **sink** type is set to **BlobSink**.</span></span>

<span data-ttu-id="0ef79-186">Zobacz [właściwości typu WebSource](#copy-activity-type-properties) listę obsługiwanych przez WebSource właściwości.</span><span class="sxs-lookup"><span data-stu-id="0ef79-186">See [WebSource type properties](#copy-activity-type-properties) for the list of properties supported by the WebSource.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "WebTableToAzureBlob",
        "description": "Copy from a Web table to an Azure blob",
        "type": "Copy",
        "inputs": [
          {
            "name": "WebTableInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "WebSource"
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

## <a name="get-index-of-a-table-in-an-html-page"></a><span data-ttu-id="0ef79-187">Pobierz indeksu tabeli na stronie HTML</span><span class="sxs-lookup"><span data-stu-id="0ef79-187">Get index of a table in an HTML page</span></span>
1. <span data-ttu-id="0ef79-188">Uruchom **Excel 2016** i przejdź do **danych** kartę.</span><span class="sxs-lookup"><span data-stu-id="0ef79-188">Launch **Excel 2016** and switch to the **Data** tab.</span></span>  
2. <span data-ttu-id="0ef79-189">Kliknij przycisk **nowe zapytanie** na pasku narzędzi, wskaż polecenie **z innych źródeł** i kliknij przycisk **z sieci Web**.</span><span class="sxs-lookup"><span data-stu-id="0ef79-189">Click **New Query** on the toolbar, point to **From Other Sources** and click **From Web**.</span></span>

    ![Power Query menu](./media/data-factory-web-table-connector/PowerQuery-Menu.png)
3. <span data-ttu-id="0ef79-191">W **z sieci Web** okna dialogowego wprowadź **adres URL** można skorzystać w połączonej usłudze JSON (na przykład: https://en.wikipedia.org/wiki/) oraz ścieżkę należy określić dla zestawu danych (na przykład: AFI % 27s_ 100_Years... 100_Movies) i kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="0ef79-191">In the **From Web** dialog box, enter **URL** that you would use in linked service JSON (for example: https://en.wikipedia.org/wiki/) along with path you would specify for the dataset (for example: AFI%27s_100_Years...100_Movies), and click **OK**.</span></span>

    ![Z okna dialogowego sieci Web](./media/data-factory-web-table-connector/FromWeb-DialogBox.png)

    <span data-ttu-id="0ef79-193">Adres URL używany w tym przykładzie: https://en.wikipedia.org/wiki/AFI%27s_100_Years...100_Movies</span><span class="sxs-lookup"><span data-stu-id="0ef79-193">URL used in this example: https://en.wikipedia.org/wiki/AFI%27s_100_Years...100_Movies</span></span>
4. <span data-ttu-id="0ef79-194">Jeśli widzisz **zawartości sieci Web Access** oknie dialogowym Wybierz prawa **adres URL**, **uwierzytelniania**i kliknij przycisk **Connect**.</span><span class="sxs-lookup"><span data-stu-id="0ef79-194">If you see **Access Web content** dialog box, select the right **URL**, **authentication**, and click **Connect**.</span></span>

   ![Okno dialogowe zawartości sieci Web Access](./media/data-factory-web-table-connector/AccessWebContentDialog.png)
5. <span data-ttu-id="0ef79-196">Kliknij przycisk **tabeli** elementu w widoku drzewa, aby wyświetlić zawartość z tabeli, a następnie kliknij przycisk **Edytuj** znajdujący się u dołu.</span><span class="sxs-lookup"><span data-stu-id="0ef79-196">Click a **table** item in the tree view to see content from the table and then click **Edit** button at the bottom.</span></span>  

   ![Nawigator okna dialogowego](./media/data-factory-web-table-connector/Navigator-DialogBox.png)
6. <span data-ttu-id="0ef79-198">W **edytora zapytań** okna, kliknij przycisk **Zaawansowany edytor** przycisk na pasku narzędzi.</span><span class="sxs-lookup"><span data-stu-id="0ef79-198">In the **Query Editor** window, click **Advanced Editor** button on the toolbar.</span></span>

    ![Przycisk Zaawansowane Edytora](./media/data-factory-web-table-connector/QueryEditor-AdvancedEditorButton.png)
7. <span data-ttu-id="0ef79-200">W oknie dialogowym Zaawansowany edytor numer obok "Source" jest indeksem.</span><span class="sxs-lookup"><span data-stu-id="0ef79-200">In the Advanced Editor dialog box, the number next to "Source" is the index.</span></span>

    ![Zaawansowany edytor - indeksu](./media/data-factory-web-table-connector/AdvancedEditor-Index.png)

<span data-ttu-id="0ef79-202">Jeśli korzystasz z programu Excel 2013, użyj [Microsoft Power Query dla programu Excel](https://www.microsoft.com/download/details.aspx?id=39379) można uzyskać indeksu.</span><span class="sxs-lookup"><span data-stu-id="0ef79-202">If you are using Excel 2013, use [Microsoft Power Query for Excel](https://www.microsoft.com/download/details.aspx?id=39379) to get the index.</span></span> <span data-ttu-id="0ef79-203">Zobacz [Connect do strony sieci web](https://support.office.com/article/Connect-to-a-web-page-Power-Query-b2725d67-c9e8-43e6-a590-c0a175bd64d8) artykułu, aby uzyskać szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="0ef79-203">See [Connect to a web page](https://support.office.com/article/Connect-to-a-web-page-Power-Query-b2725d67-c9e8-43e6-a590-c0a175bd64d8) article for details.</span></span> <span data-ttu-id="0ef79-204">Te kroki są podobne, jeśli używasz [Microsoft Power BI Desktop](https://powerbi.microsoft.com/desktop/).</span><span class="sxs-lookup"><span data-stu-id="0ef79-204">The steps are similar if you are using [Microsoft Power BI for Desktop](https://powerbi.microsoft.com/desktop/).</span></span>

> [!NOTE]
> <span data-ttu-id="0ef79-205">Aby mapować kolumn z zestawu źródła danych do kolumn z obiektu sink zestawu danych, zobacz [mapowania kolumnach dataset w fabryce danych Azure](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="0ef79-205">To map columns from source dataset to columns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="0ef79-206">Wydajność i dostrajania</span><span class="sxs-lookup"><span data-stu-id="0ef79-206">Performance and Tuning</span></span>
<span data-ttu-id="0ef79-207">Zobacz [wydajności działania kopiowania & dostrajanie przewodnik](data-factory-copy-activity-performance.md) Aby dowiedzieć się więcej o kluczowych czynników tego wydajność wpływ przenoszenia danych (działanie kopiowania) w usłudze fabryka danych Azure i zoptymalizować ją na różne sposoby.</span><span class="sxs-lookup"><span data-stu-id="0ef79-207">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
