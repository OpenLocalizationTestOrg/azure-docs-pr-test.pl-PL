---
title: "aaaMove danych z tabeli sieci Web przy użyciu fabryki danych Azure | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat sposobu toomove danych z tabeli w sieci Web stronę przy użyciu fabryki danych Azure."
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
ms.openlocfilehash: e52216305583ebbe71ed896522f361bb22f01278
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-a-web-table-source-using-azure-data-factory"></a><span data-ttu-id="a0dba-103">Przenoszenie danych ze źródła tabeli sieci Web przy użyciu fabryki danych Azure</span><span class="sxs-lookup"><span data-stu-id="a0dba-103">Move data from a Web table source using Azure Data Factory</span></span>
<span data-ttu-id="a0dba-104">W tym artykule opisano, jak toouse hello działanie kopiowania danych toomove fabryki danych Azure z tabeli w tooa strony sieci Web obsługiwane ujścia magazynu danych.</span><span class="sxs-lookup"><span data-stu-id="a0dba-104">This article outlines how toouse hello Copy Activity in Azure Data Factory toomove data from a table in a Web page tooa supported sink data store.</span></span> <span data-ttu-id="a0dba-105">W tym artykule opiera się na powitania [działań przepływu danych](data-factory-data-movement-activities.md) artykułu, który przedstawia ogólne omówienie przepływu danych kopię działania i hello listy magazynów danych są obsługiwane jako źródła/sink.</span><span class="sxs-lookup"><span data-stu-id="a0dba-105">This article builds on hello [data movement activities](data-factory-data-movement-activities.md) article that presents a general overview of data movement with copy activity and hello list of data stores supported as sources/sinks.</span></span>

<span data-ttu-id="a0dba-106">Fabryka danych aktualnie obsługuje tylko przechowuje przenoszenia danych z danych tooother tabeli sieci Web, ale nie przenoszenia danych z innych danych przechowuje tooa Web tabeli docelowej.</span><span class="sxs-lookup"><span data-stu-id="a0dba-106">Data factory currently supports only moving data from a Web table tooother data stores, but not moving data from other data stores tooa Web table destination.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a0dba-107">Ten łącznik sieci Web obsługuje obecnie tylko wyodrębnianie zawartości tabeli ze strony HTML.</span><span class="sxs-lookup"><span data-stu-id="a0dba-107">This Web connector currently supports only extracting table content from an HTML page.</span></span> <span data-ttu-id="a0dba-108">Użyj tooretrieve danych z punktu końcowego protokołu HTTP/s [łącznika HTTP](data-factory-http-connector.md) zamiast tego.</span><span class="sxs-lookup"><span data-stu-id="a0dba-108">tooretrieve data from a HTTP/s endpoint, use [HTTP connector](data-factory-http-connector.md) instead.</span></span>

## <a name="getting-started"></a><span data-ttu-id="a0dba-109">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="a0dba-109">Getting started</span></span>
<span data-ttu-id="a0dba-110">Można utworzyć potok z działania kopiowania, który przenosi dane z magazynu lokalnego Cassandra danych przy użyciu różnych narzędzi/interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="a0dba-110">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="a0dba-111">Witaj Najprostszym sposobem toocreate potoku jest toouse hello **kreatora kopiowania**.</span><span class="sxs-lookup"><span data-stu-id="a0dba-111">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="a0dba-112">Zobacz [samouczek: tworzenie potoku za pomocą Kreatora kopiowania](data-factory-copy-data-wizard-tutorial.md) szybkie przewodnik dotyczący tworzenia potoku za pomocą Kreatora dane Kopiuj hello.</span><span class="sxs-lookup"><span data-stu-id="a0dba-112">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span> 
- <span data-ttu-id="a0dba-113">Można również użyć hello następujące narzędzia toocreate potoku: **portalu Azure**, **programu Visual Studio**, **programu Azure PowerShell**, **szablonu usługi Azure Resource Manager** , **Interfejs API .NET**, i **interfejsu API REST**.</span><span class="sxs-lookup"><span data-stu-id="a0dba-113">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="a0dba-114">Zobacz [samouczek działania kopiowania](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) dla toocreate instrukcje krok po kroku potoku z działaniem kopiowania.</span><span class="sxs-lookup"><span data-stu-id="a0dba-114">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="a0dba-115">Czy za pomocą narzędzia hello lub interfejsów API, należy wykonać następujące kroki toocreate potok, który przenosi się, że magazyn danych ze źródła danych magazynu danych zbiornika tooa hello:</span><span class="sxs-lookup"><span data-stu-id="a0dba-115">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="a0dba-116">Utwórz **połączone usługi** toolink usługi fabryka danych tooyour magazynów danych wejściowych i wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="a0dba-116">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="a0dba-117">Utwórz **zestawów danych** toorepresent wejściowe i wyjściowe dane hello operacji kopiowania.</span><span class="sxs-lookup"><span data-stu-id="a0dba-117">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="a0dba-118">Utwórz **potoku** aktywnością kopiowania zestawu danych jako dane wejściowe i zestawu danych jako dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="a0dba-118">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="a0dba-119">Korzystając z Kreatora hello, definicje JSON do tych jednostek fabryki danych (połączone usługi, zestawy danych i potoku hello) są tworzone automatycznie dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="a0dba-119">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="a0dba-120">Korzystając z narzędzi/API (z wyjątkiem interfejs API .NET), należy zdefiniować za pomocą formatu JSON hello tych jednostek fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="a0dba-120">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="a0dba-121">Dla przykładu z definicji JSON dla jednostek fabryki danych, które są używane toocopy danych z tabeli sieci web, zobacz [przykład JSON: kopiowanie danych z sieci Web tooAzure tabeli obiektów Blob](#json-example-copy-data-from-web-table-to-azure-blob) sekcji tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="a0dba-121">For a sample with JSON definitions for Data Factory entities that are used toocopy data from a web table, see [JSON example: Copy data from Web table tooAzure Blob](#json-example-copy-data-from-web-table-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="a0dba-122">Witaj następujące sekcje zawierają szczegółowe informacje o właściwości JSON, które są używane toodefine fabryki danych jednostek tooa określonej sieci Web tabeli:</span><span class="sxs-lookup"><span data-stu-id="a0dba-122">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooa Web table:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="a0dba-123">Połączona usługa właściwości</span><span class="sxs-lookup"><span data-stu-id="a0dba-123">Linked service properties</span></span>
<span data-ttu-id="a0dba-124">Hello w poniższej tabeli przedstawiono opis usługi określonego tooWeb połączone elementy JSON.</span><span class="sxs-lookup"><span data-stu-id="a0dba-124">hello following table provides description for JSON elements specific tooWeb linked service.</span></span>

| <span data-ttu-id="a0dba-125">Właściwość</span><span class="sxs-lookup"><span data-stu-id="a0dba-125">Property</span></span> | <span data-ttu-id="a0dba-126">Opis</span><span class="sxs-lookup"><span data-stu-id="a0dba-126">Description</span></span> | <span data-ttu-id="a0dba-127">Wymagane</span><span class="sxs-lookup"><span data-stu-id="a0dba-127">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a0dba-128">type</span><span class="sxs-lookup"><span data-stu-id="a0dba-128">type</span></span> |<span data-ttu-id="a0dba-129">musi mieć ustawioną właściwość type Hello: **sieci Web**</span><span class="sxs-lookup"><span data-stu-id="a0dba-129">hello type property must be set to: **Web**</span></span> |<span data-ttu-id="a0dba-130">Tak</span><span class="sxs-lookup"><span data-stu-id="a0dba-130">Yes</span></span> |
| <span data-ttu-id="a0dba-131">Url</span><span class="sxs-lookup"><span data-stu-id="a0dba-131">Url</span></span> |<span data-ttu-id="a0dba-132">Adres URL źródła toohello w sieci Web</span><span class="sxs-lookup"><span data-stu-id="a0dba-132">URL toohello Web source</span></span> |<span data-ttu-id="a0dba-133">Tak</span><span class="sxs-lookup"><span data-stu-id="a0dba-133">Yes</span></span> |
| <span data-ttu-id="a0dba-134">Typ authenticationType</span><span class="sxs-lookup"><span data-stu-id="a0dba-134">authenticationType</span></span> |<span data-ttu-id="a0dba-135">Anonimowe.</span><span class="sxs-lookup"><span data-stu-id="a0dba-135">Anonymous.</span></span> |<span data-ttu-id="a0dba-136">Tak</span><span class="sxs-lookup"><span data-stu-id="a0dba-136">Yes</span></span> |

### <a name="using-anonymous-authentication"></a><span data-ttu-id="a0dba-137">Przy użyciu uwierzytelniania anonimowego</span><span class="sxs-lookup"><span data-stu-id="a0dba-137">Using Anonymous authentication</span></span>

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

## <a name="dataset-properties"></a><span data-ttu-id="a0dba-138">Właściwości zestawu danych</span><span class="sxs-lookup"><span data-stu-id="a0dba-138">Dataset properties</span></span>
<span data-ttu-id="a0dba-139">Aby uzyskać pełną listę sekcje & właściwości dostępne do definiowania zestawów danych, zobacz hello [Tworzenie zbiorów danych](data-factory-create-datasets.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="a0dba-139">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="a0dba-140">Sekcje zawierają informacje, takie jak struktury, dostępności i zasad zestawu danych JSON są podobne dla wszystkich typów obiektów dataset (Azure SQL, obiektów blob platformy Azure, Azure tabeli itp.).</span><span class="sxs-lookup"><span data-stu-id="a0dba-140">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="a0dba-141">Witaj **typeProperties** sekcja zawiera informacje o lokalizacji hello hello danych w magazynie danych hello i różni się dla każdego typu zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="a0dba-141">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="a0dba-142">Witaj typeProperties sekcja dla zestawu danych typu **tabeli WebTable** ma następujące właściwości hello</span><span class="sxs-lookup"><span data-stu-id="a0dba-142">hello typeProperties section for dataset of type **WebTable** has hello following properties</span></span>

| <span data-ttu-id="a0dba-143">Właściwość</span><span class="sxs-lookup"><span data-stu-id="a0dba-143">Property</span></span> | <span data-ttu-id="a0dba-144">Opis</span><span class="sxs-lookup"><span data-stu-id="a0dba-144">Description</span></span> | <span data-ttu-id="a0dba-145">Wymagane</span><span class="sxs-lookup"><span data-stu-id="a0dba-145">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="a0dba-146">type</span><span class="sxs-lookup"><span data-stu-id="a0dba-146">type</span></span> |<span data-ttu-id="a0dba-147">Typ hello zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="a0dba-147">type of hello dataset.</span></span> <span data-ttu-id="a0dba-148">musi być ustawiona zbyt**tabeli WebTable**</span><span class="sxs-lookup"><span data-stu-id="a0dba-148">must be set too**WebTable**</span></span> |<span data-ttu-id="a0dba-149">Tak</span><span class="sxs-lookup"><span data-stu-id="a0dba-149">Yes</span></span> |
| <span data-ttu-id="a0dba-150">Ścieżka</span><span class="sxs-lookup"><span data-stu-id="a0dba-150">path</span></span> |<span data-ttu-id="a0dba-151">Względny adres URL toohello zasób zawiera tabelę hello.</span><span class="sxs-lookup"><span data-stu-id="a0dba-151">A relative URL toohello resource that contains hello table.</span></span> |<span data-ttu-id="a0dba-152">Nie.</span><span class="sxs-lookup"><span data-stu-id="a0dba-152">No.</span></span> <span data-ttu-id="a0dba-153">Jeśli ścieżka nie jest określona, tylko hello adresu URL określonego w definicji usługi połączone hello jest używany.</span><span class="sxs-lookup"><span data-stu-id="a0dba-153">When path is not specified, only hello URL specified in hello linked service definition is used.</span></span> |
| <span data-ttu-id="a0dba-154">Indeks</span><span class="sxs-lookup"><span data-stu-id="a0dba-154">index</span></span> |<span data-ttu-id="a0dba-155">Indeks Hello hello tabeli w zasobie hello.</span><span class="sxs-lookup"><span data-stu-id="a0dba-155">hello index of hello table in hello resource.</span></span> <span data-ttu-id="a0dba-156">Zobacz [Get indeksu tabeli na stronie HTML](#get-index-of-a-table-in-an-html-page) sekcji kroki toogetting indeksu tabeli na stronie HTML.</span><span class="sxs-lookup"><span data-stu-id="a0dba-156">See [Get index of a table in an HTML page](#get-index-of-a-table-in-an-html-page) section for steps toogetting index of a table in an HTML page.</span></span> |<span data-ttu-id="a0dba-157">Tak</span><span class="sxs-lookup"><span data-stu-id="a0dba-157">Yes</span></span> |

<span data-ttu-id="a0dba-158">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="a0dba-158">**Example:**</span></span>

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

## <a name="copy-activity-properties"></a><span data-ttu-id="a0dba-159">Właściwości działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="a0dba-159">Copy activity properties</span></span>
<span data-ttu-id="a0dba-160">Pełną listę sekcje & właściwości dostępne do definiowania działań, zobacz hello [tworzenie potoków](data-factory-create-pipelines.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="a0dba-160">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="a0dba-161">Właściwości, takie jak nazwa, opis, dane wejściowe i wyjściowe tabel i zasady są dostępne dla wszystkich typów działań.</span><span class="sxs-lookup"><span data-stu-id="a0dba-161">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="a0dba-162">Właściwości, które są dostępne w sekcji typeProperties hello działania hello różnić się z każdym typem działania.</span><span class="sxs-lookup"><span data-stu-id="a0dba-162">Whereas, properties available in hello typeProperties section of hello activity vary with each activity type.</span></span> <span data-ttu-id="a0dba-163">Dla działania kopiowania różnią się w zależności od typów hello źródeł i sink.</span><span class="sxs-lookup"><span data-stu-id="a0dba-163">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="a0dba-164">Obecnie, gdy hello źródła w przypadku działania kopiowania jest typu **WebSource**, są obsługiwane żadne dodatkowe właściwości.</span><span class="sxs-lookup"><span data-stu-id="a0dba-164">Currently, when hello source in copy activity is of type **WebSource**, no additional properties are supported.</span></span>


## <a name="json-example-copy-data-from-web-table-tooazure-blob"></a><span data-ttu-id="a0dba-165">Przykład JSON: kopiowanie danych z sieci Web tooAzure tabeli obiektów Blob</span><span class="sxs-lookup"><span data-stu-id="a0dba-165">JSON example: Copy data from Web table tooAzure Blob</span></span>
<span data-ttu-id="a0dba-166">następujące przykładowe pokazuje Hello:</span><span class="sxs-lookup"><span data-stu-id="a0dba-166">hello following sample shows:</span></span>

1. <span data-ttu-id="a0dba-167">Połączonej usługi typu [Web](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="a0dba-167">A linked service of type [Web](#linked-service-properties).</span></span>
2. <span data-ttu-id="a0dba-168">Połączonej usługi typu [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="a0dba-168">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="a0dba-169">Dane wejściowe [dataset](data-factory-create-datasets.md) typu [tabeli WebTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="a0dba-169">An input [dataset](data-factory-create-datasets.md) of type [WebTable](#dataset-properties).</span></span>
4. <span data-ttu-id="a0dba-170">Dane wyjściowe [dataset](data-factory-create-datasets.md) typu [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="a0dba-170">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="a0dba-171">A [potoku](data-factory-create-pipelines.md) z działaniem kopii, która używa [WebSource](#copy-activity-properties) i [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="a0dba-171">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [WebSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="a0dba-172">przykład Witaj kopiuje dane z sieci Web tooan tabeli obiektów blob platformy Azure co godzinę.</span><span class="sxs-lookup"><span data-stu-id="a0dba-172">hello sample copies data from a Web table tooan Azure blob every hour.</span></span> <span data-ttu-id="a0dba-173">właściwości JSON Hello używane w te przykłady są opisane w sekcjach poniżej hello próbek.</span><span class="sxs-lookup"><span data-stu-id="a0dba-173">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="a0dba-174">następujące przykładowe Hello pokazuje, jak obiekt blob danych toocopy z tooan tabeli sieci Web Azure.</span><span class="sxs-lookup"><span data-stu-id="a0dba-174">hello following sample shows how toocopy data from a Web table tooan Azure blob.</span></span> <span data-ttu-id="a0dba-175">Jednak dane mogą być kopiowane bezpośrednio tooany hello wychwytywanie hello podane w [działań przepływu danych](data-factory-data-movement-activities.md) artykułu przy użyciu hello działanie kopiowania w fabryce danych Azure.</span><span class="sxs-lookup"><span data-stu-id="a0dba-175">However, data can be copied directly tooany of hello sinks stated in hello [Data Movement Activities](data-factory-data-movement-activities.md) article by using hello Copy Activity in Azure Data Factory.</span></span>

<span data-ttu-id="a0dba-176">**Sieci Web połączonej usługi** w tym przykładzie używa hello sieci Web połączonej usługi przy użyciu uwierzytelniania anonimowego.</span><span class="sxs-lookup"><span data-stu-id="a0dba-176">**Web linked service** This example uses hello Web linked service with anonymous authentication.</span></span> <span data-ttu-id="a0dba-177">Zobacz [sieci Web połączonej usługi](#linked-service-properties) sekcji dla różnych typów uwierzytelniania, można użyć.</span><span class="sxs-lookup"><span data-stu-id="a0dba-177">See [Web linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

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

<span data-ttu-id="a0dba-178">**Połączona usługa Azure Storage**</span><span class="sxs-lookup"><span data-stu-id="a0dba-178">**Azure Storage linked service**</span></span>

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

<span data-ttu-id="a0dba-179">**Wejściowy zestaw danych tabeli WebTable** ustawienie **zewnętrznych** za**true** informuje hello usługi fabryka danych tego elementu dataset hello zewnętrznych toohello fabryki danych i nie jest generowany przez działanie w hello Fabryka danych.</span><span class="sxs-lookup"><span data-stu-id="a0dba-179">**WebTable input dataset** Setting **external** too**true** informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

> [!NOTE]
> <span data-ttu-id="a0dba-180">Zobacz [Get indeksu tabeli na stronie HTML](#get-index-of-a-table-in-an-html-page) sekcji kroki toogetting indeksu tabeli na stronie HTML.</span><span class="sxs-lookup"><span data-stu-id="a0dba-180">See [Get index of a table in an HTML page](#get-index-of-a-table-in-an-html-page) section for steps toogetting index of a table in an HTML page.</span></span>  
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


<span data-ttu-id="a0dba-181">**Azure Blob wyjściowy zestaw danych**</span><span class="sxs-lookup"><span data-stu-id="a0dba-181">**Azure Blob output dataset**</span></span>

<span data-ttu-id="a0dba-182">Dane są zapisywane tooa nowych obiektów blob, co godzinę (częstotliwość: godziny, interwał: 1).</span><span class="sxs-lookup"><span data-stu-id="a0dba-182">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span>

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



<span data-ttu-id="a0dba-183">**W potoku z działanie kopiowania**</span><span class="sxs-lookup"><span data-stu-id="a0dba-183">**Pipeline with Copy activity**</span></span>

<span data-ttu-id="a0dba-184">Witaj potoku zawiera działanie kopiowania, który jest skonfigurowany toouse hello wejściowych i wyjściowych zestawów danych i jest toorun zaplanowane co godzinę.</span><span class="sxs-lookup"><span data-stu-id="a0dba-184">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="a0dba-185">W potoku hello definicji JSON, hello **źródła** typu ustawiono zbyt**WebSource** i **zbiornika** typu ustawiono zbyt**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="a0dba-185">In hello pipeline JSON definition, hello **source** type is set too**WebSource** and **sink** type is set too**BlobSink**.</span></span>

<span data-ttu-id="a0dba-186">Zobacz [właściwości typu WebSource](#copy-activity-type-properties) hello listę obsługiwanych przez hello WebSource właściwości.</span><span class="sxs-lookup"><span data-stu-id="a0dba-186">See [WebSource type properties](#copy-activity-type-properties) for hello list of properties supported by hello WebSource.</span></span>

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
        "description": "Copy from a Web table tooan Azure blob",
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

## <a name="get-index-of-a-table-in-an-html-page"></a><span data-ttu-id="a0dba-187">Pobierz indeksu tabeli na stronie HTML</span><span class="sxs-lookup"><span data-stu-id="a0dba-187">Get index of a table in an HTML page</span></span>
1. <span data-ttu-id="a0dba-188">Uruchom **Excel 2016** i przełączanie toohello **danych** kartę.</span><span class="sxs-lookup"><span data-stu-id="a0dba-188">Launch **Excel 2016** and switch toohello **Data** tab.</span></span>  
2. <span data-ttu-id="a0dba-189">Kliknij przycisk **nowe zapytanie** na powitania narzędzi za punkt**z innych źródeł** i kliknij przycisk **z sieci Web**.</span><span class="sxs-lookup"><span data-stu-id="a0dba-189">Click **New Query** on hello toolbar, point too**From Other Sources** and click **From Web**.</span></span>

    ![Power Query menu](./media/data-factory-web-table-connector/PowerQuery-Menu.png)
3. <span data-ttu-id="a0dba-191">W hello **z sieci Web** okna dialogowego wprowadź **adres URL** można skorzystać w połączonej usłudze JSON (na przykład: https://en.wikipedia.org/wiki/) oraz ścieżkę należy określić dla zestawu danych hello (na przykład: AFI % 27s_100_Years... 100_Movies) i kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="a0dba-191">In hello **From Web** dialog box, enter **URL** that you would use in linked service JSON (for example: https://en.wikipedia.org/wiki/) along with path you would specify for hello dataset (for example: AFI%27s_100_Years...100_Movies), and click **OK**.</span></span>

    ![Z okna dialogowego sieci Web](./media/data-factory-web-table-connector/FromWeb-DialogBox.png)

    <span data-ttu-id="a0dba-193">Adres URL używany w tym przykładzie: https://en.wikipedia.org/wiki/AFI%27s_100_Years...100_Movies</span><span class="sxs-lookup"><span data-stu-id="a0dba-193">URL used in this example: https://en.wikipedia.org/wiki/AFI%27s_100_Years...100_Movies</span></span>
4. <span data-ttu-id="a0dba-194">Jeśli widzisz **zawartości sieci Web Access** okno dialogowe, wybierz hello prawo **adres URL**, **uwierzytelniania**i kliknij przycisk **Connect**.</span><span class="sxs-lookup"><span data-stu-id="a0dba-194">If you see **Access Web content** dialog box, select hello right **URL**, **authentication**, and click **Connect**.</span></span>

   ![Okno dialogowe zawartości sieci Web Access](./media/data-factory-web-table-connector/AccessWebContentDialog.png)
5. <span data-ttu-id="a0dba-196">Kliknij przycisk **tabeli** elementu hello drzewa widoku toosee zawartości z hello tabeli, a następnie kliknij przycisk **Edytuj** u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="a0dba-196">Click a **table** item in hello tree view toosee content from hello table and then click **Edit** button at hello bottom.</span></span>  

   ![Nawigator okna dialogowego](./media/data-factory-web-table-connector/Navigator-DialogBox.png)
6. <span data-ttu-id="a0dba-198">W hello **edytora zapytań** okna, kliknij przycisk **Zaawansowany edytor** przycisk na powitania narzędzi.</span><span class="sxs-lookup"><span data-stu-id="a0dba-198">In hello **Query Editor** window, click **Advanced Editor** button on hello toolbar.</span></span>

    ![Przycisk Zaawansowane Edytora](./media/data-factory-web-table-connector/QueryEditor-AdvancedEditorButton.png)
7. <span data-ttu-id="a0dba-200">Okno dialogowe Zaawansowany edytor hello, hello numer obok "Source" jest za hello indeksu.</span><span class="sxs-lookup"><span data-stu-id="a0dba-200">In hello Advanced Editor dialog box, hello number next too"Source" is hello index.</span></span>

    ![Zaawansowany edytor - indeksu](./media/data-factory-web-table-connector/AdvancedEditor-Index.png)

<span data-ttu-id="a0dba-202">Jeśli korzystasz z programu Excel 2013, użyj [Microsoft Power Query dla programu Excel](https://www.microsoft.com/download/details.aspx?id=39379) tooget hello indeksu.</span><span class="sxs-lookup"><span data-stu-id="a0dba-202">If you are using Excel 2013, use [Microsoft Power Query for Excel](https://www.microsoft.com/download/details.aspx?id=39379) tooget hello index.</span></span> <span data-ttu-id="a0dba-203">Zobacz [strony sieci web tooa Połącz](https://support.office.com/article/Connect-to-a-web-page-Power-Query-b2725d67-c9e8-43e6-a590-c0a175bd64d8) artykułu, aby uzyskać szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="a0dba-203">See [Connect tooa web page](https://support.office.com/article/Connect-to-a-web-page-Power-Query-b2725d67-c9e8-43e6-a590-c0a175bd64d8) article for details.</span></span> <span data-ttu-id="a0dba-204">Witaj kroki są podobne, jeśli używasz [Microsoft Power BI Desktop](https://powerbi.microsoft.com/desktop/).</span><span class="sxs-lookup"><span data-stu-id="a0dba-204">hello steps are similar if you are using [Microsoft Power BI for Desktop](https://powerbi.microsoft.com/desktop/).</span></span>

> [!NOTE]
> <span data-ttu-id="a0dba-205">toomap kolumny źródłowej toocolumns zestawu danych z obiektu sink zestawu danych, zobacz [mapowania kolumnach dataset w fabryce danych Azure](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="a0dba-205">toomap columns from source dataset toocolumns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="a0dba-206">Wydajność i dostrajania</span><span class="sxs-lookup"><span data-stu-id="a0dba-206">Performance and Tuning</span></span>
<span data-ttu-id="a0dba-207">Zobacz [wydajności działania kopiowania & dostrajanie przewodnik](data-factory-copy-activity-performance.md) toolearn o kluczu czynniki tego wydajność wpływ przenoszenia danych (działanie kopiowania) w usłudze fabryka danych Azure i różne sposoby toooptimize go.</span><span class="sxs-lookup"><span data-stu-id="a0dba-207">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
