---
title: "Indeks tooSearch danych aaaPush przy użyciu fabryki danych | Dokumentacja firmy Microsoft"
description: "Dowiedz się więcej o toopush danych tooAzure indeksu wyszukiwania przy użyciu fabryki danych Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: f8d46e1e-5c37-4408-80fb-c54be532a4ab
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: f2d973d0a2c24d6448e2d59e37e24503aa433018
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="push-data-tooan-azure-search-index-by-using-azure-data-factory"></a><span data-ttu-id="2bbf6-103">Wypychanie indeksu usługi Azure Search tooan danych przy użyciu fabryki danych Azure</span><span class="sxs-lookup"><span data-stu-id="2bbf6-103">Push data tooan Azure Search index by using Azure Data Factory</span></span>
<span data-ttu-id="2bbf6-104">W tym artykule opisano, jak indeks wyszukiwania tooAzure magazynu toouse hello działanie kopiowania toopush danych z obsługiwanych źródła danych.</span><span class="sxs-lookup"><span data-stu-id="2bbf6-104">This article describes how toouse hello Copy Activity toopush data from a supported source data store tooAzure Search index.</span></span> <span data-ttu-id="2bbf6-105">Magazyny danych obsługiwanych źródłowych są wymienione w kolumnie źródła hello hello [obsługiwanych źródeł i wychwytywanie](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabeli.</span><span class="sxs-lookup"><span data-stu-id="2bbf6-105">Supported source data stores are listed in hello Source column of hello [supported sources and sinks](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="2bbf6-106">W tym artykule opiera się na powitania [działań przepływu danych](data-factory-data-movement-activities.md) artykułu, który przedstawia ogólny przegląd przenoszenia danych z kombinacji magazynu obsługiwane dane i działanie kopiowania.</span><span class="sxs-lookup"><span data-stu-id="2bbf6-106">This article builds on hello [data movement activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with Copy Activity and supported data store combinations.</span></span>

## <a name="enabling-connectivity"></a><span data-ttu-id="2bbf6-107">Włączenie łączności</span><span class="sxs-lookup"><span data-stu-id="2bbf6-107">Enabling connectivity</span></span>
<span data-ttu-id="2bbf6-108">tooallow usługi fabryka danych połączenia tooan z lokalnym magazynem danych, zainstalować bramę zarządzania danymi w środowisku lokalnym.</span><span class="sxs-lookup"><span data-stu-id="2bbf6-108">tooallow Data Factory service connect tooan on-premises data store, you install Data Management Gateway in your on-premises environment.</span></span> <span data-ttu-id="2bbf6-109">Możesz zainstalować bramę na hello na tym samym komputerze obsługującym hello źródła danych magazynu lub na tooavoid osobnym komputerze fizycznym, konkurowanie o zasoby z hello danych.</span><span class="sxs-lookup"><span data-stu-id="2bbf6-109">You can install gateway on hello same machine that hosts hello source data store or on a separate machine tooavoid competing for resources with hello data store.</span></span>

<span data-ttu-id="2bbf6-110">Brama zarządzania danymi nawiązuje połączenie usługi toocloud źródeł danych lokalnych w sposób bezpieczny i zarządzanie nimi.</span><span class="sxs-lookup"><span data-stu-id="2bbf6-110">Data Management Gateway connects on-premises data sources toocloud services in a secure and managed way.</span></span> <span data-ttu-id="2bbf6-111">Zobacz [przenoszenie danych między lokalnymi i w chmurze](data-factory-move-data-between-onprem-and-cloud.md) artykułu, aby uzyskać więcej informacji dotyczących bramy zarządzania danymi.</span><span class="sxs-lookup"><span data-stu-id="2bbf6-111">See [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for details about Data Management Gateway.</span></span>

## <a name="getting-started"></a><span data-ttu-id="2bbf6-112">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="2bbf6-112">Getting started</span></span>
<span data-ttu-id="2bbf6-113">Można utworzyć potoku o działanie kopiowania, który wypycha dane z indeksem wyszukiwania tooAzure źródła danych magazynu przy użyciu różnych narzędzi/interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="2bbf6-113">You can create a pipeline with a copy activity that pushes data from a source data store tooAzure Search index by using different tools/APIs.</span></span>

<span data-ttu-id="2bbf6-114">Witaj Najprostszym sposobem toocreate potoku jest toouse hello **kreatora kopiowania**.</span><span class="sxs-lookup"><span data-stu-id="2bbf6-114">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="2bbf6-115">Zobacz [samouczek: tworzenie potoku za pomocą Kreatora kopiowania](data-factory-copy-data-wizard-tutorial.md) szybkie przewodnik dotyczący tworzenia potoku za pomocą Kreatora dane Kopiuj hello.</span><span class="sxs-lookup"><span data-stu-id="2bbf6-115">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="2bbf6-116">Można również użyć hello następujące narzędzia toocreate potoku: **portalu Azure**, **programu Visual Studio**, **programu Azure PowerShell**, **szablonu usługi Azure Resource Manager** , **Interfejs API .NET**, i **interfejsu API REST**.</span><span class="sxs-lookup"><span data-stu-id="2bbf6-116">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="2bbf6-117">Zobacz [samouczek działania kopiowania](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) dla toocreate instrukcje krok po kroku potoku z działaniem kopiowania.</span><span class="sxs-lookup"><span data-stu-id="2bbf6-117">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="2bbf6-118">Czy za pomocą narzędzia hello lub interfejsów API, należy wykonać następujące kroki toocreate potok, który przenosi się, że magazyn danych ze źródła danych magazynu danych zbiornika tooa hello:</span><span class="sxs-lookup"><span data-stu-id="2bbf6-118">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span> 

1. <span data-ttu-id="2bbf6-119">Utwórz **połączone usługi** toolink usługi fabryka danych tooyour magazynów danych wejściowych i wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="2bbf6-119">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="2bbf6-120">Utwórz **zestawów danych** toorepresent wejściowe i wyjściowe dane hello operacji kopiowania.</span><span class="sxs-lookup"><span data-stu-id="2bbf6-120">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="2bbf6-121">Utwórz **potoku** aktywnością kopiowania zestawu danych jako dane wejściowe i zestawu danych jako dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="2bbf6-121">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="2bbf6-122">Korzystając z Kreatora hello, definicje JSON do tych jednostek fabryki danych (połączone usługi, zestawy danych i potoku hello) są tworzone automatycznie dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="2bbf6-122">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="2bbf6-123">Korzystając z narzędzi/API (z wyjątkiem interfejs API .NET), należy zdefiniować za pomocą formatu JSON hello tych jednostek fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="2bbf6-123">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="2bbf6-124">Dla przykładu z definicji JSON dla jednostek fabryki danych, które są używane toocopy danych tooAzure indeks, zobacz [przykład JSON: kopiowanie danych z lokalnego programu SQL Server tooAzure indeks](#json-example-copy-data-from-on-premises-sql-server-to-azure-search-index) sekcji tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="2bbf6-124">For a sample with JSON definitions for Data Factory entities that are used toocopy data tooAzure Search index, see [JSON example: Copy data from on-premises SQL Server tooAzure Search index](#json-example-copy-data-from-on-premises-sql-server-to-azure-search-index) section of this article.</span></span> 

<span data-ttu-id="2bbf6-125">Witaj następujące sekcje zawierają szczegółowe informacje o właściwości JSON, które są używane toodefine fabryki danych jednostek określonych tooAzure indeksu wyszukiwania:</span><span class="sxs-lookup"><span data-stu-id="2bbf6-125">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooAzure Search Index:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="2bbf6-126">Połączona usługa właściwości</span><span class="sxs-lookup"><span data-stu-id="2bbf6-126">Linked service properties</span></span>

<span data-ttu-id="2bbf6-127">Witaj w poniższej tabeli zawiera opisy elementów JSON usługi Azure Search połączone toohello określone.</span><span class="sxs-lookup"><span data-stu-id="2bbf6-127">hello following table provides descriptions for JSON elements that are specific toohello Azure Search linked service.</span></span>

| <span data-ttu-id="2bbf6-128">Właściwość</span><span class="sxs-lookup"><span data-stu-id="2bbf6-128">Property</span></span> | <span data-ttu-id="2bbf6-129">Opis</span><span class="sxs-lookup"><span data-stu-id="2bbf6-129">Description</span></span> | <span data-ttu-id="2bbf6-130">Wymagane</span><span class="sxs-lookup"><span data-stu-id="2bbf6-130">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="2bbf6-131">type</span><span class="sxs-lookup"><span data-stu-id="2bbf6-131">type</span></span> | <span data-ttu-id="2bbf6-132">musi mieć ustawioną właściwość type Hello: **AzureSearch**.</span><span class="sxs-lookup"><span data-stu-id="2bbf6-132">hello type property must be set to: **AzureSearch**.</span></span> | <span data-ttu-id="2bbf6-133">Tak</span><span class="sxs-lookup"><span data-stu-id="2bbf6-133">Yes</span></span> |
| <span data-ttu-id="2bbf6-134">adres URL</span><span class="sxs-lookup"><span data-stu-id="2bbf6-134">url</span></span> | <span data-ttu-id="2bbf6-135">Adres URL hello usługi Azure Search.</span><span class="sxs-lookup"><span data-stu-id="2bbf6-135">URL for hello Azure Search service.</span></span> | <span data-ttu-id="2bbf6-136">Tak</span><span class="sxs-lookup"><span data-stu-id="2bbf6-136">Yes</span></span> |
| <span data-ttu-id="2bbf6-137">key</span><span class="sxs-lookup"><span data-stu-id="2bbf6-137">key</span></span> | <span data-ttu-id="2bbf6-138">Klucz administratora dla hello usługi Azure Search.</span><span class="sxs-lookup"><span data-stu-id="2bbf6-138">Admin key for hello Azure Search service.</span></span> | <span data-ttu-id="2bbf6-139">Tak</span><span class="sxs-lookup"><span data-stu-id="2bbf6-139">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="2bbf6-140">Właściwości zestawu danych</span><span class="sxs-lookup"><span data-stu-id="2bbf6-140">Dataset properties</span></span>

<span data-ttu-id="2bbf6-141">Aby uzyskać pełną listę sekcje i właściwości, które są dostępne do definiowania zestawów danych, zobacz hello [Tworzenie zbiorów danych](data-factory-create-datasets.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="2bbf6-141">For a full list of sections and properties that are available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="2bbf6-142">Sekcje zawierają informacje, takie jak struktury, dostępności i zasad zestawu danych JSON są podobne dla wszystkich typów w zestawie danych.</span><span class="sxs-lookup"><span data-stu-id="2bbf6-142">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types.</span></span> <span data-ttu-id="2bbf6-143">Witaj **typeProperties** sekcja jest różne dla każdego typu zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="2bbf6-143">hello **typeProperties** section is different for each type of dataset.</span></span> <span data-ttu-id="2bbf6-144">Witaj typeProperties sekcja dla zestawu danych typu hello **AzureSearchIndex** ma hello następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="2bbf6-144">hello typeProperties section for a dataset of hello type **AzureSearchIndex** has hello following properties:</span></span>

| <span data-ttu-id="2bbf6-145">Właściwość</span><span class="sxs-lookup"><span data-stu-id="2bbf6-145">Property</span></span> | <span data-ttu-id="2bbf6-146">Opis</span><span class="sxs-lookup"><span data-stu-id="2bbf6-146">Description</span></span> | <span data-ttu-id="2bbf6-147">Wymagane</span><span class="sxs-lookup"><span data-stu-id="2bbf6-147">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="2bbf6-148">type</span><span class="sxs-lookup"><span data-stu-id="2bbf6-148">type</span></span> | <span data-ttu-id="2bbf6-149">zbyt należy ustawić właściwość typu Hello**AzureSearchIndex**.</span><span class="sxs-lookup"><span data-stu-id="2bbf6-149">hello type property must be set too**AzureSearchIndex**.</span></span>| <span data-ttu-id="2bbf6-150">Tak</span><span class="sxs-lookup"><span data-stu-id="2bbf6-150">Yes</span></span> |
| <span data-ttu-id="2bbf6-151">indexName</span><span class="sxs-lookup"><span data-stu-id="2bbf6-151">indexName</span></span> | <span data-ttu-id="2bbf6-152">Nazwa indeksu usługi Azure Search hello.</span><span class="sxs-lookup"><span data-stu-id="2bbf6-152">Name of hello Azure Search index.</span></span> <span data-ttu-id="2bbf6-153">Fabryki danych nie powoduje utworzenia hello indeksu.</span><span class="sxs-lookup"><span data-stu-id="2bbf6-153">Data Factory does not create hello index.</span></span> <span data-ttu-id="2bbf6-154">Indeks Hello musi istnieć w usłudze Azure Search.</span><span class="sxs-lookup"><span data-stu-id="2bbf6-154">hello index must exist in Azure Search.</span></span> | <span data-ttu-id="2bbf6-155">Tak</span><span class="sxs-lookup"><span data-stu-id="2bbf6-155">Yes</span></span> |


## <a name="copy-activity-properties"></a><span data-ttu-id="2bbf6-156">Właściwości działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="2bbf6-156">Copy activity properties</span></span>
<span data-ttu-id="2bbf6-157">Aby uzyskać pełną listę sekcje i właściwości, które są dostępne do definiowania działań, zobacz hello [tworzenie potoków](data-factory-create-pipelines.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="2bbf6-157">For a full list of sections and properties that are available for defining activities, see hello [Creating pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="2bbf6-158">Właściwości, takie jak nazwa, opis, dane wejściowe i tabele wyjściowe i różnych zasad są dostępne dla wszystkich typów działań.</span><span class="sxs-lookup"><span data-stu-id="2bbf6-158">Properties such as name, description, input and output tables, and various policies are available for all types of activities.</span></span> <span data-ttu-id="2bbf6-159">Właściwości, które są dostępne w sekcji typeProperties hello różnić się z każdym typem działania.</span><span class="sxs-lookup"><span data-stu-id="2bbf6-159">Whereas, properties available in hello typeProperties section vary with each activity type.</span></span> <span data-ttu-id="2bbf6-160">Dla działania kopiowania różnią się w zależności od typów hello źródeł i sink.</span><span class="sxs-lookup"><span data-stu-id="2bbf6-160">For Copy Activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="2bbf6-161">Dla działania kopiowania, gdy zbiornika hello jest typu hello **AzureSearchIndexSink**, hello następujące właściwości są dostępne w sekcji typeProperties:</span><span class="sxs-lookup"><span data-stu-id="2bbf6-161">For Copy Activity, when hello sink is of hello type **AzureSearchIndexSink**, hello following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="2bbf6-162">Właściwość</span><span class="sxs-lookup"><span data-stu-id="2bbf6-162">Property</span></span> | <span data-ttu-id="2bbf6-163">Opis</span><span class="sxs-lookup"><span data-stu-id="2bbf6-163">Description</span></span> | <span data-ttu-id="2bbf6-164">Dozwolone wartości</span><span class="sxs-lookup"><span data-stu-id="2bbf6-164">Allowed values</span></span> | <span data-ttu-id="2bbf6-165">Wymagane</span><span class="sxs-lookup"><span data-stu-id="2bbf6-165">Required</span></span> |
| -------- | ----------- | -------------- | -------- |
| <span data-ttu-id="2bbf6-166">WriteBehavior</span><span class="sxs-lookup"><span data-stu-id="2bbf6-166">WriteBehavior</span></span> | <span data-ttu-id="2bbf6-167">Określa, czy toomerge lub Zastąp, gdy dokument już istnieje w indeksie hello.</span><span class="sxs-lookup"><span data-stu-id="2bbf6-167">Specifies whether toomerge or replace when a document already exists in hello index.</span></span> <span data-ttu-id="2bbf6-168">Zobacz hello [WriteBehavior właściwości](#writebehavior-property).</span><span class="sxs-lookup"><span data-stu-id="2bbf6-168">See hello [WriteBehavior property](#writebehavior-property).</span></span>| <span data-ttu-id="2bbf6-169">Merge (ustawienie domyślne)</span><span class="sxs-lookup"><span data-stu-id="2bbf6-169">Merge (default)</span></span><br/><span data-ttu-id="2bbf6-170">Upload</span><span class="sxs-lookup"><span data-stu-id="2bbf6-170">Upload</span></span>| <span data-ttu-id="2bbf6-171">Nie</span><span class="sxs-lookup"><span data-stu-id="2bbf6-171">No</span></span> |
| <span data-ttu-id="2bbf6-172">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="2bbf6-172">WriteBatchSize</span></span> | <span data-ttu-id="2bbf6-173">Przekazywanie danych do indeksu usługi Azure Search hello, gdy osiągnie rozmiar buforu hello writeBatchSize.</span><span class="sxs-lookup"><span data-stu-id="2bbf6-173">Uploads data into hello Azure Search index when hello buffer size reaches writeBatchSize.</span></span> <span data-ttu-id="2bbf6-174">Zobacz hello [właściwości WriteBatchSize](#writebatchsize-property) szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="2bbf6-174">See hello [WriteBatchSize property](#writebatchsize-property) for details.</span></span> | <span data-ttu-id="2bbf6-175">1 too1 000.</span><span class="sxs-lookup"><span data-stu-id="2bbf6-175">1 too1,000.</span></span> <span data-ttu-id="2bbf6-176">Wartość domyślna to 1000.</span><span class="sxs-lookup"><span data-stu-id="2bbf6-176">Default value is 1000.</span></span> | <span data-ttu-id="2bbf6-177">Nie</span><span class="sxs-lookup"><span data-stu-id="2bbf6-177">No</span></span> |

### <a name="writebehavior-property"></a><span data-ttu-id="2bbf6-178">Właściwość WriteBehavior</span><span class="sxs-lookup"><span data-stu-id="2bbf6-178">WriteBehavior property</span></span>
<span data-ttu-id="2bbf6-179">Upserts AzureSearchSink podczas zapisywania danych.</span><span class="sxs-lookup"><span data-stu-id="2bbf6-179">AzureSearchSink upserts when writing data.</span></span> <span data-ttu-id="2bbf6-180">Innymi słowy podczas zapisywania dokumentu, jeśli klucz dokumentu hello już istnieje w indeksie usługi Azure Search hello, usługi Azure Search aktualizuje hello istniejącego dokumentu, zamiast zgłaszanie wyjątków konflikt.</span><span class="sxs-lookup"><span data-stu-id="2bbf6-180">In other words, when writing a document, if hello document key already exists in hello Azure Search index, Azure Search updates hello existing document rather than throwing a conflict exception.</span></span>

<span data-ttu-id="2bbf6-181">Witaj AzureSearchSink zapewnia hello następujące dwa zachowania upsert (przy użyciu zestawu SDK AzureSearch):</span><span class="sxs-lookup"><span data-stu-id="2bbf6-181">hello AzureSearchSink provides hello following two upsert behaviors (by using AzureSearch SDK):</span></span>

- <span data-ttu-id="2bbf6-182">**Scal**: łączenie wszystkich kolumn hello hello nowy dokument z hello jedną istniejącą.</span><span class="sxs-lookup"><span data-stu-id="2bbf6-182">**Merge**: combine all hello columns in hello new document with hello existing one.</span></span> <span data-ttu-id="2bbf6-183">Dla kolumn o wartości null w hello nowy dokument wartość hello w hello jedną istniejącą zostanie zachowana.</span><span class="sxs-lookup"><span data-stu-id="2bbf6-183">For columns with null value in hello new document, hello value in hello existing one is preserved.</span></span>
- <span data-ttu-id="2bbf6-184">**Przekaż**: hello nowy dokument zastępuje hello istniejący.</span><span class="sxs-lookup"><span data-stu-id="2bbf6-184">**Upload**: hello new document replaces hello existing one.</span></span> <span data-ttu-id="2bbf6-185">Dla kolumn nie jest określona w hello nowy dokument hello wartość jest ustawiana toonull, czy istnieje wartość inną niż null w hello istniejącego dokumentu lub nie.</span><span class="sxs-lookup"><span data-stu-id="2bbf6-185">For columns not specified in hello new document, hello value is set toonull whether there is a non-null value in hello existing document or not.</span></span>

<span data-ttu-id="2bbf6-186">Witaj domyślne zachowanie to **scalania**.</span><span class="sxs-lookup"><span data-stu-id="2bbf6-186">hello default behavior is **Merge**.</span></span>

### <a name="writebatchsize-property"></a><span data-ttu-id="2bbf6-187">Właściwość WriteBatchSize</span><span class="sxs-lookup"><span data-stu-id="2bbf6-187">WriteBatchSize Property</span></span>
<span data-ttu-id="2bbf6-188">Usługa Azure Search obsługuje dokumenty Zapisywanie jako zadanie wsadowe.</span><span class="sxs-lookup"><span data-stu-id="2bbf6-188">Azure Search service supports writing documents as a batch.</span></span> <span data-ttu-id="2bbf6-189">Plik wsadowy może zawierać too1 1, 000 akcje.</span><span class="sxs-lookup"><span data-stu-id="2bbf6-189">A batch can contain 1 too1,000 Actions.</span></span> <span data-ttu-id="2bbf6-190">Akcja obsługuje jednej operacji przekazywania/merge hello tooperform dokumentu.</span><span class="sxs-lookup"><span data-stu-id="2bbf6-190">An action handles one document tooperform hello upload/merge operation.</span></span>

### <a name="data-type-support"></a><span data-ttu-id="2bbf6-191">Obsługa typu danych</span><span class="sxs-lookup"><span data-stu-id="2bbf6-191">Data type support</span></span>
<span data-ttu-id="2bbf6-192">Witaj Poniższa tabela określa, czy lub nie obsługuje typu danych usługi Azure Search.</span><span class="sxs-lookup"><span data-stu-id="2bbf6-192">hello following table specifies whether an Azure Search data type is supported or not.</span></span>

| <span data-ttu-id="2bbf6-193">Typ danych w usłudze Azure wyszukiwania</span><span class="sxs-lookup"><span data-stu-id="2bbf6-193">Azure Search data type</span></span> | <span data-ttu-id="2bbf6-194">Obsługiwane w ujściu usługi Azure Search</span><span class="sxs-lookup"><span data-stu-id="2bbf6-194">Supported in Azure Search Sink</span></span> |
| ---------------------- | ------------------------------ |
| <span data-ttu-id="2bbf6-195">Ciąg</span><span class="sxs-lookup"><span data-stu-id="2bbf6-195">String</span></span> | <span data-ttu-id="2bbf6-196">Tak</span><span class="sxs-lookup"><span data-stu-id="2bbf6-196">Y</span></span> |
| <span data-ttu-id="2bbf6-197">Int32</span><span class="sxs-lookup"><span data-stu-id="2bbf6-197">Int32</span></span> | <span data-ttu-id="2bbf6-198">Tak</span><span class="sxs-lookup"><span data-stu-id="2bbf6-198">Y</span></span> |
| <span data-ttu-id="2bbf6-199">Int64</span><span class="sxs-lookup"><span data-stu-id="2bbf6-199">Int64</span></span> | <span data-ttu-id="2bbf6-200">Tak</span><span class="sxs-lookup"><span data-stu-id="2bbf6-200">Y</span></span> |
| <span data-ttu-id="2bbf6-201">O podwójnej precyzji</span><span class="sxs-lookup"><span data-stu-id="2bbf6-201">Double</span></span> | <span data-ttu-id="2bbf6-202">Tak</span><span class="sxs-lookup"><span data-stu-id="2bbf6-202">Y</span></span> |
| <span data-ttu-id="2bbf6-203">Wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="2bbf6-203">Boolean</span></span> | <span data-ttu-id="2bbf6-204">Tak</span><span class="sxs-lookup"><span data-stu-id="2bbf6-204">Y</span></span> |
| <span data-ttu-id="2bbf6-205">DataTimeOffset</span><span class="sxs-lookup"><span data-stu-id="2bbf6-205">DataTimeOffset</span></span> | <span data-ttu-id="2bbf6-206">Tak</span><span class="sxs-lookup"><span data-stu-id="2bbf6-206">Y</span></span> |
| <span data-ttu-id="2bbf6-207">Tablica ciągów</span><span class="sxs-lookup"><span data-stu-id="2bbf6-207">String Array</span></span> | <span data-ttu-id="2bbf6-208">N</span><span class="sxs-lookup"><span data-stu-id="2bbf6-208">N</span></span> |
| <span data-ttu-id="2bbf6-209">GeographyPoint</span><span class="sxs-lookup"><span data-stu-id="2bbf6-209">GeographyPoint</span></span> | <span data-ttu-id="2bbf6-210">N</span><span class="sxs-lookup"><span data-stu-id="2bbf6-210">N</span></span> |

## <a name="json-example-copy-data-from-on-premises-sql-server-tooazure-search-index"></a><span data-ttu-id="2bbf6-211">Przykład JSON: kopiowanie danych z lokalnego programu SQL Server tooAzure wyszukiwania indeksu</span><span class="sxs-lookup"><span data-stu-id="2bbf6-211">JSON example: Copy data from on-premises SQL Server tooAzure Search index</span></span>

<span data-ttu-id="2bbf6-212">następujące przykładowe pokazuje Hello:</span><span class="sxs-lookup"><span data-stu-id="2bbf6-212">hello following sample shows:</span></span>

1.  <span data-ttu-id="2bbf6-213">Połączonej usługi typu [AzureSearch](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="2bbf6-213">A linked service of type [AzureSearch](#linked-service-properties).</span></span>
2.  <span data-ttu-id="2bbf6-214">Połączonej usługi typu [OnPremisesSqlServer](data-factory-sqlserver-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="2bbf6-214">A linked service of type [OnPremisesSqlServer](data-factory-sqlserver-connector.md#linked-service-properties).</span></span>
3.  <span data-ttu-id="2bbf6-215">Dane wejściowe [dataset](data-factory-create-datasets.md) typu [SqlServerTable](data-factory-sqlserver-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="2bbf6-215">An input [dataset](data-factory-create-datasets.md) of type [SqlServerTable](data-factory-sqlserver-connector.md#dataset-properties).</span></span>
4.  <span data-ttu-id="2bbf6-216">Dane wyjściowe [dataset](data-factory-create-datasets.md) typu [AzureSearchIndex](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="2bbf6-216">An output [dataset](data-factory-create-datasets.md) of type [AzureSearchIndex](#dataset-properties).</span></span>
4.  <span data-ttu-id="2bbf6-217">A [potoku](data-factory-create-pipelines.md) z działania kopiowania, która używa [SqlSource](data-factory-sqlserver-connector.md#copy-activity-properties) i [AzureSearchIndexSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="2bbf6-217">A [pipeline](data-factory-create-pipelines.md) with a Copy activity that uses [SqlSource](data-factory-sqlserver-connector.md#copy-activity-properties) and [AzureSearchIndexSink](#copy-activity-properties).</span></span>

<span data-ttu-id="2bbf6-218">Przykładowe Hello kopiuje dane szeregów czasowych co godzinę z lokalnymi indeksu usługi Azure Search tooan bazy danych programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="2bbf6-218">hello sample copies time-series data from an on-premises SQL Server database tooan Azure Search index hourly.</span></span> <span data-ttu-id="2bbf6-219">właściwości JSON Hello używane w tym przykładzie są opisane w sekcjach poniżej hello próbek.</span><span class="sxs-lookup"><span data-stu-id="2bbf6-219">hello JSON properties used in this sample are described in sections following hello samples.</span></span>

<span data-ttu-id="2bbf6-220">Pierwszym krokiem konfiguracji bramy zarządzania danymi hello na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="2bbf6-220">As a first step, setup hello data management gateway on your on-premises machine.</span></span> <span data-ttu-id="2bbf6-221">Witaj instrukcje znajdują się w hello [przenoszenie danych między lokalizacji lokalnej i w chmurze](data-factory-move-data-between-onprem-and-cloud.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="2bbf6-221">hello instructions are in hello [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="2bbf6-222">**Usługa Azure Search połączone:**</span><span class="sxs-lookup"><span data-stu-id="2bbf6-222">**Azure Search linked service:**</span></span>

```JSON
{
    "name": "AzureSearchLinkedService",
    "properties": {
        "type": "AzureSearch",
        "typeProperties": {
            "url": "https://<service>.search.windows.net",
            "key": "<AdminKey>"
        }
    }
}
```

<span data-ttu-id="2bbf6-223">**Usługi SQL Server połączone**</span><span class="sxs-lookup"><span data-stu-id="2bbf6-223">**SQL Server linked service**</span></span>

```JSON
{
  "Name": "SqlServerLinkedService",
  "properties": {
    "type": "OnPremisesSqlServer",
    "typeProperties": {
      "connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=False;User ID=<username>;Password=<password>;",
      "gatewayName": "<gatewayname>"
    }
  }
}
```

<span data-ttu-id="2bbf6-224">**Wejściowy zestaw danych programu SQL Server**</span><span class="sxs-lookup"><span data-stu-id="2bbf6-224">**SQL Server input dataset**</span></span>

<span data-ttu-id="2bbf6-225">przykład Witaj przyjęto założenie, utworzono tabelę "MyTable" w programie SQL Server i zawiera kolumnę o nazwie "timestampcolumn" dla czasu serii danych.</span><span class="sxs-lookup"><span data-stu-id="2bbf6-225">hello sample assumes you have created a table “MyTable” in SQL Server and it contains a column called “timestampcolumn” for time series data.</span></span> <span data-ttu-id="2bbf6-226">Umożliwia wysyłanie zapytań przez wiele tabel w ramach tej samej bazy danych za pomocą jednego zestawu danych, ale pojedynczej tabeli muszą być używane do hello dataset tableName typeProperty powitalne.</span><span class="sxs-lookup"><span data-stu-id="2bbf6-226">You can query over multiple tables within hello same database using a single dataset, but a single table must be used for hello dataset's tableName typeProperty.</span></span>

<span data-ttu-id="2bbf6-227">Ustawienie "external": "prawda" informuje usługi fabryka danych tego elementu dataset hello zewnętrznych toohello fabryki danych i nie jest generowany przez działanie w fabryce danych hello.</span><span class="sxs-lookup"><span data-stu-id="2bbf6-227">Setting “external”: ”true” informs Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```JSON
{
  "name": "SqlServerDataset",
  "properties": {
    "type": "SqlServerTable",
    "linkedServiceName": "SqlServerLinkedService",
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

<span data-ttu-id="2bbf6-228">**Usługa Azure Search wyjściowy zestaw danych:**</span><span class="sxs-lookup"><span data-stu-id="2bbf6-228">**Azure Search output dataset:**</span></span>

<span data-ttu-id="2bbf6-229">Hello próbki kopii danych tooan indeksu usługi Azure Search o nazwie **produkty**.</span><span class="sxs-lookup"><span data-stu-id="2bbf6-229">hello sample copies data tooan Azure Search index named **products**.</span></span> <span data-ttu-id="2bbf6-230">Fabryki danych nie powoduje utworzenia hello indeksu.</span><span class="sxs-lookup"><span data-stu-id="2bbf6-230">Data Factory does not create hello index.</span></span> <span data-ttu-id="2bbf6-231">Witaj tootest przykładowe, Utwórz indeks o tej nazwie.</span><span class="sxs-lookup"><span data-stu-id="2bbf6-231">tootest hello sample, create an index with this name.</span></span> <span data-ttu-id="2bbf6-232">Tworzenie indeksu usługi Azure Search hello z hello taką samą liczbę kolumn, tak jak hello wejściowy zestaw danych.</span><span class="sxs-lookup"><span data-stu-id="2bbf6-232">Create hello Azure Search index with hello same number of columns as in hello input dataset.</span></span> <span data-ttu-id="2bbf6-233">Nowe wpisy są dodawane indeksu usługi Azure Search toohello co godzinę.</span><span class="sxs-lookup"><span data-stu-id="2bbf6-233">New entries are added toohello Azure Search index every hour.</span></span>

```JSON
{
    "name": "AzureSearchIndexDataset",
    "properties": {
        "type": "AzureSearchIndex",
        "linkedServiceName": "AzureSearchLinkedService",
        "typeProperties" : {
            "indexName": "products",
        },
        "availability": {
            "frequency": "Minute",
            "interval": 15
        }
   }
}
```

<span data-ttu-id="2bbf6-234">**Działanie kopiowania w potoku z SQL źródłowy i odbiorczy indeksu usługi Azure Search:**</span><span class="sxs-lookup"><span data-stu-id="2bbf6-234">**Copy activity in a pipeline with SQL source and Azure Search Index sink:**</span></span>

<span data-ttu-id="2bbf6-235">Witaj potoku zawiera działanie kopiowania, który jest skonfigurowany toouse hello wejściowych i wyjściowych zestawów danych i jest toorun zaplanowane co godzinę.</span><span class="sxs-lookup"><span data-stu-id="2bbf6-235">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="2bbf6-236">W potoku hello definicji JSON, hello **źródła** typu ustawiono zbyt**SqlSource** i **zbiornika** typu ustawiono zbyt**AzureSearchIndexSink**.</span><span class="sxs-lookup"><span data-stu-id="2bbf6-236">In hello pipeline JSON definition, hello **source** type is set too**SqlSource** and **sink** type is set too**AzureSearchIndexSink**.</span></span> <span data-ttu-id="2bbf6-237">Zapytanie SQL Hello określone dla hello **SqlReaderQuery** właściwości zaznacza danych hello hello poza toocopy godzinę.</span><span class="sxs-lookup"><span data-stu-id="2bbf6-237">hello SQL query specified for hello **SqlReaderQuery** property selects hello data in hello past hour toocopy.</span></span>

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline for copy activity",
    "activities":[  
      {
        "name": "SqlServertoAzureSearchIndex",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": " SqlServerInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureSearchIndexDataset"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "SqlSource",
            "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
          },
          "sink": {
            "type": "AzureSearchIndexSink"
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

<span data-ttu-id="2bbf6-238">Jeśli kopiujesz danych z magazynu danych chmury do usługi Azure Search `executionLocation` właściwość jest wymagana.</span><span class="sxs-lookup"><span data-stu-id="2bbf6-238">If you are copying data from a cloud data store into Azure Search, `executionLocation` property is required.</span></span> <span data-ttu-id="2bbf6-239">Witaj następujący fragment kodu JSON zawiera hello zmiany wymagane w obszarze działania kopiowania `typeProperties` jako przykład.</span><span class="sxs-lookup"><span data-stu-id="2bbf6-239">hello following JSON snippet shows hello change needed under Copy Activity `typeProperties` as an example.</span></span> <span data-ttu-id="2bbf6-240">Sprawdź [kopiowanie danych między magazyny danych w chmurze](data-factory-data-movement-activities.md#global) sekcji obsługiwane wartości i więcej szczegółów.</span><span class="sxs-lookup"><span data-stu-id="2bbf6-240">Check [Copy data between cloud data stores](data-factory-data-movement-activities.md#global) section for supported values and more details.</span></span>

```JSON
"typeProperties": {
  "source": {
    "type": "BlobSource"
  },
  "sink": {
    "type": "AzureSearchIndexSink"
  },
  "executionLocation": "West US"
}
```


## <a name="copy-from-a-cloud-source"></a><span data-ttu-id="2bbf6-241">Skopiuj ze źródłowej chmurze</span><span class="sxs-lookup"><span data-stu-id="2bbf6-241">Copy from a cloud source</span></span>
<span data-ttu-id="2bbf6-242">Jeśli kopiujesz danych z magazynu danych chmury do usługi Azure Search `executionLocation` właściwość jest wymagana.</span><span class="sxs-lookup"><span data-stu-id="2bbf6-242">If you are copying data from a cloud data store into Azure Search, `executionLocation` property is required.</span></span> <span data-ttu-id="2bbf6-243">Witaj następujący fragment kodu JSON zawiera hello zmiany wymagane w obszarze działania kopiowania `typeProperties` jako przykład.</span><span class="sxs-lookup"><span data-stu-id="2bbf6-243">hello following JSON snippet shows hello change needed under Copy Activity `typeProperties` as an example.</span></span> <span data-ttu-id="2bbf6-244">Sprawdź [kopiowanie danych między magazyny danych w chmurze](data-factory-data-movement-activities.md#global) sekcji obsługiwane wartości i więcej szczegółów.</span><span class="sxs-lookup"><span data-stu-id="2bbf6-244">Check [Copy data between cloud data stores](data-factory-data-movement-activities.md#global) section for supported values and more details.</span></span>

```JSON
"typeProperties": {
  "source": {
    "type": "BlobSource"
  },
  "sink": {
    "type": "AzureSearchIndexSink"
  },
  "executionLocation": "West US"
}
```

<span data-ttu-id="2bbf6-245">Można również mapować kolumn z źródła toocolumns zestawu danych z zestawu danych zbiornika w definicji działania kopiowania hello.</span><span class="sxs-lookup"><span data-stu-id="2bbf6-245">You can also map columns from source dataset toocolumns from sink dataset in hello copy activity definition.</span></span> <span data-ttu-id="2bbf6-246">Aby uzyskać więcej informacji, zobacz [mapowania kolumnach dataset w fabryce danych Azure](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="2bbf6-246">For details, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="2bbf6-247">Wydajności i dostosowywanie</span><span class="sxs-lookup"><span data-stu-id="2bbf6-247">Performance and tuning</span></span>  
<span data-ttu-id="2bbf6-248">Zobacz hello [wydajności działania kopiowania i dostrajania przewodnik](data-factory-copy-activity-performance.md) toolearn o kluczu czynniki tego wydajności wpływ przenoszenia danych (działanie kopiowania) oraz różne sposoby toooptimize go.</span><span class="sxs-lookup"><span data-stu-id="2bbf6-248">See hello [Copy Activity performance and tuning guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) and various ways toooptimize it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2bbf6-249">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="2bbf6-249">Next steps</span></span>
<span data-ttu-id="2bbf6-250">Zobacz następujące artykuły hello:</span><span class="sxs-lookup"><span data-stu-id="2bbf6-250">See hello following articles:</span></span>

* <span data-ttu-id="2bbf6-251">[Samouczek działania kopiowania](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) instrukcje krok po kroku do tworzenia potoku z działania kopiowania.</span><span class="sxs-lookup"><span data-stu-id="2bbf6-251">[Copy Activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions for creating a pipeline with a Copy Activity.</span></span>
