---
title: "aaaMove danych do/z bazy danych Azure rozwiązania Cosmos | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak przenieść dane do/z bazy danych Azure rozwiązania Cosmos kolekcji przy użyciu fabryki danych Azure"
services: data-factory, cosmosdb
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: c9297b71-1bb4-4b29-ba3c-4cf1f5575fac
ms.service: multiple
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: bd23ce4e004a972ce6f3e4165cfdea4f0c18fecc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooand-from-azure-cosmos-db-using-azure-data-factory"></a><span data-ttu-id="bf95f-103">Przenieś tooand danych z bazy danych rozwiązania Cosmos Azure przy użyciu fabryki danych Azure</span><span class="sxs-lookup"><span data-stu-id="bf95f-103">Move data tooand from Azure Cosmos DB using Azure Data Factory</span></span>
<span data-ttu-id="bf95f-104">W tym artykule opisano, jak toouse hello działanie kopiowania w fabryce danych Azure toomove danych z bazy danych Azure rozwiązania Cosmos (interfejsu API usługi DocumentDB).</span><span class="sxs-lookup"><span data-stu-id="bf95f-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data to/from Azure Cosmos DB (DocumentDB API).</span></span> <span data-ttu-id="bf95f-105">Opiera się na powitania [działań przepływu danych](data-factory-data-movement-activities.md) artykułu, który przedstawia ogólny przegląd przenoszenia danych z hello działanie kopiowania.</span><span class="sxs-lookup"><span data-stu-id="bf95f-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span> 

<span data-ttu-id="bf95f-106">Możesz skopiować dane z dowolnych obsługiwanych źródeł danych magazynu tooAzure rozwiązania Cosmos bazy danych lub z bazy danych Azure rozwiązania Cosmos tooany obsługiwane ujścia danych.</span><span class="sxs-lookup"><span data-stu-id="bf95f-106">You can copy data from any supported source data store tooAzure Cosmos DB or from Azure Cosmos DB tooany supported sink data store.</span></span> <span data-ttu-id="bf95f-107">Lista magazynów danych obsługiwane jako źródła lub wychwytywanie przez działanie kopiowania hello, zobacz hello [obsługiwane magazyny danych](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabeli.</span><span class="sxs-lookup"><span data-stu-id="bf95f-107">For a list of data stores supported as sources or sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="bf95f-108">Łącznik usługi Azure DB rozwiązania Cosmos obsługują tylko interfejsu API usługi DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="bf95f-108">Azure Cosmos DB connector only support DocumentDB API.</span></span>

<span data-ttu-id="bf95f-109">dane toocopy jako — jest do/z pliki w formacie JSON lub innej kolekcji rozwiązania Cosmos bazy danych, zobacz [dokumentów JSON importu/eksportu](#importexport-json-documents).</span><span class="sxs-lookup"><span data-stu-id="bf95f-109">toocopy data as-is to/from JSON files or another Cosmos DB collection, see [Import/Export JSON documents](#importexport-json-documents).</span></span>

## <a name="getting-started"></a><span data-ttu-id="bf95f-110">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="bf95f-110">Getting started</span></span>
<span data-ttu-id="bf95f-111">Można utworzyć potoku o działanie kopiowania, który przenosi dane z bazy danych rozwiązania Cosmos Azure przy użyciu różnych narzędzi/interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="bf95f-111">You can create a pipeline with a copy activity that moves data to/from Azure Cosmos DB by using different tools/APIs.</span></span>

<span data-ttu-id="bf95f-112">Witaj Najprostszym sposobem toocreate potoku jest toouse hello **kreatora kopiowania**.</span><span class="sxs-lookup"><span data-stu-id="bf95f-112">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="bf95f-113">Zobacz [samouczek: tworzenie potoku za pomocą Kreatora kopiowania](data-factory-copy-data-wizard-tutorial.md) szybkie przewodnik dotyczący tworzenia potoku za pomocą Kreatora dane Kopiuj hello.</span><span class="sxs-lookup"><span data-stu-id="bf95f-113">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="bf95f-114">Można również użyć hello następujące narzędzia toocreate potoku: **portalu Azure**, **programu Visual Studio**, **programu Azure PowerShell**, **szablonu usługi Azure Resource Manager** , **Interfejs API .NET**, i **interfejsu API REST**.</span><span class="sxs-lookup"><span data-stu-id="bf95f-114">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="bf95f-115">Zobacz [samouczek działania kopiowania](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) dla toocreate instrukcje krok po kroku potoku z działaniem kopiowania.</span><span class="sxs-lookup"><span data-stu-id="bf95f-115">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="bf95f-116">Czy za pomocą narzędzia hello lub interfejsów API, należy wykonać następujące kroki toocreate potok, który przenosi się, że magazyn danych ze źródła danych magazynu danych zbiornika tooa hello:</span><span class="sxs-lookup"><span data-stu-id="bf95f-116">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span> 

1. <span data-ttu-id="bf95f-117">Utwórz **połączone usługi** toolink usługi fabryka danych tooyour magazynów danych wejściowych i wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="bf95f-117">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="bf95f-118">Utwórz **zestawów danych** toorepresent wejściowe i wyjściowe dane hello operacji kopiowania.</span><span class="sxs-lookup"><span data-stu-id="bf95f-118">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="bf95f-119">Utwórz **potoku** aktywnością kopiowania zestawu danych jako dane wejściowe i zestawu danych jako dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="bf95f-119">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="bf95f-120">Korzystając z Kreatora hello, definicje JSON do tych jednostek fabryki danych (połączone usługi, zestawy danych i potoku hello) są tworzone automatycznie dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="bf95f-120">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="bf95f-121">Korzystając z narzędzi/API (z wyjątkiem interfejs API .NET), należy zdefiniować za pomocą formatu JSON hello tych jednostek fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="bf95f-121">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="bf95f-122">Dla przykładów z definicji JSON dla jednostek fabryki danych, które są używane toocopy danych do/z rozwiązania Cosmos bazy danych, zobacz [przykłady JSON](#json-examples) sekcji tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="bf95f-122">For samples with JSON definitions for Data Factory entities that are used toocopy data to/from Cosmos DB, see [JSON examples](#json-examples) section of this article.</span></span> 

<span data-ttu-id="bf95f-123">Witaj następujące sekcje zawierają szczegółowe informacje o właściwości JSON, które są używane toodefine fabryki danych jednostek określonych tooCosmos bazy danych:</span><span class="sxs-lookup"><span data-stu-id="bf95f-123">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooCosmos DB:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="bf95f-124">Połączona usługa właściwości</span><span class="sxs-lookup"><span data-stu-id="bf95f-124">Linked service properties</span></span>
<span data-ttu-id="bf95f-125">Witaj w poniższej tabeli przedstawiono opis dla określonych tooAzure elementów JSON DB rozwiązania Cosmos połączone usługi.</span><span class="sxs-lookup"><span data-stu-id="bf95f-125">hello following table provides description for JSON elements specific tooAzure Cosmos DB linked service.</span></span>

| <span data-ttu-id="bf95f-126">**Właściwość**</span><span class="sxs-lookup"><span data-stu-id="bf95f-126">**Property**</span></span> | <span data-ttu-id="bf95f-127">**Opis**</span><span class="sxs-lookup"><span data-stu-id="bf95f-127">**Description**</span></span> | <span data-ttu-id="bf95f-128">**Wymagane**</span><span class="sxs-lookup"><span data-stu-id="bf95f-128">**Required**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="bf95f-129">type</span><span class="sxs-lookup"><span data-stu-id="bf95f-129">type</span></span> |<span data-ttu-id="bf95f-130">musi mieć ustawioną właściwość type Hello: **usługi DocumentDb**</span><span class="sxs-lookup"><span data-stu-id="bf95f-130">hello type property must be set to: **DocumentDb**</span></span> |<span data-ttu-id="bf95f-131">Tak</span><span class="sxs-lookup"><span data-stu-id="bf95f-131">Yes</span></span> |
| <span data-ttu-id="bf95f-132">Parametry połączenia</span><span class="sxs-lookup"><span data-stu-id="bf95f-132">connectionString</span></span> |<span data-ttu-id="bf95f-133">Określ informacje niezbędne tooconnect tooAzure DB rozwiązania Cosmos w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="bf95f-133">Specify information needed tooconnect tooAzure Cosmos DB database.</span></span> |<span data-ttu-id="bf95f-134">Tak</span><span class="sxs-lookup"><span data-stu-id="bf95f-134">Yes</span></span> |

<span data-ttu-id="bf95f-135">Przykład:</span><span class="sxs-lookup"><span data-stu-id="bf95f-135">Example:</span></span>

```JSON
{
  "name": "CosmosDbLinkedService",
  "properties": {
    "type": "DocumentDb",
    "typeProperties": {
      "connectionString": "AccountEndpoint=<EndpointUrl>;AccountKey=<AccessKey>;Database=<Database>"
    }
  }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="bf95f-136">Właściwości zestawu danych</span><span class="sxs-lookup"><span data-stu-id="bf95f-136">Dataset properties</span></span>
<span data-ttu-id="bf95f-137">Pełną listę sekcje & właściwości dostępne do definiowania zestawów danych można znaleźć toohello [Tworzenie zbiorów danych](data-factory-create-datasets.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="bf95f-137">For a full list of sections & properties available for defining datasets please refer toohello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="bf95f-138">Jak struktura, dostępności i zasad zestawu danych JSON jest podobna dla wszystkich typów obiektów dataset (Azure SQL, obiektów blob platformy Azure, Azure tabeli itp.).</span><span class="sxs-lookup"><span data-stu-id="bf95f-138">Sections like structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="bf95f-139">sekcja typeProperties Hello jest różne dla każdego typu zestawu danych i zawiera informacje o lokalizacji hello hello danych w magazynie danych hello.</span><span class="sxs-lookup"><span data-stu-id="bf95f-139">hello typeProperties section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="bf95f-140">Witaj typeProperties sekcja dla zestawu danych hello typu **DocumentDbCollection** ma hello następujące właściwości.</span><span class="sxs-lookup"><span data-stu-id="bf95f-140">hello typeProperties section for hello dataset of type **DocumentDbCollection** has hello following properties.</span></span>

| <span data-ttu-id="bf95f-141">**Właściwość**</span><span class="sxs-lookup"><span data-stu-id="bf95f-141">**Property**</span></span> | <span data-ttu-id="bf95f-142">**Opis**</span><span class="sxs-lookup"><span data-stu-id="bf95f-142">**Description**</span></span> | <span data-ttu-id="bf95f-143">**Wymagane**</span><span class="sxs-lookup"><span data-stu-id="bf95f-143">**Required**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="bf95f-144">CollectionName</span><span class="sxs-lookup"><span data-stu-id="bf95f-144">collectionName</span></span> |<span data-ttu-id="bf95f-145">Nazwa hello kolekcji dokumentów DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="bf95f-145">Name of hello Cosmos DB document collection.</span></span> |<span data-ttu-id="bf95f-146">Tak</span><span class="sxs-lookup"><span data-stu-id="bf95f-146">Yes</span></span> |

<span data-ttu-id="bf95f-147">Przykład:</span><span class="sxs-lookup"><span data-stu-id="bf95f-147">Example:</span></span>

```JSON
{
  "name": "PersonCosmosDbTable",
  "properties": {
    "type": "DocumentDbCollection",
    "linkedServiceName": "CosmosDbLinkedService",
    "typeProperties": {
      "collectionName": "Person"
    },
    "external": true,
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```
### <a name="schema-by-data-factory"></a><span data-ttu-id="bf95f-148">Schemat fabryka danych</span><span class="sxs-lookup"><span data-stu-id="bf95f-148">Schema by Data Factory</span></span>
<span data-ttu-id="bf95f-149">Dla magazynów danych bez schematu, takie jak bazy danych Azure rozwiązania Cosmos hello usługi fabryka danych wnioskuje schemat hello w jednym z hello następujące sposoby:</span><span class="sxs-lookup"><span data-stu-id="bf95f-149">For schema-free data stores such as Azure Cosmos DB, hello Data Factory service infers hello schema in one of hello following ways:</span></span>  

1. <span data-ttu-id="bf95f-150">Jeśli określisz hello struktury danych za pomocą hello **struktury** tej struktury Schema hello honoruje właściwości w definicji zestawu danych hello, hello usługi fabryka danych.</span><span class="sxs-lookup"><span data-stu-id="bf95f-150">If you specify hello structure of data by using hello **structure** property in hello dataset definition, hello Data Factory service honors this structure as hello schema.</span></span> <span data-ttu-id="bf95f-151">W takim przypadku wiersza nie zawiera wartości dla kolumny, będzie należy podać dla niego wartość null.</span><span class="sxs-lookup"><span data-stu-id="bf95f-151">In this case, if a row does not contain a value for a column, a null value will be provided for it.</span></span>
2. <span data-ttu-id="bf95f-152">Jeśli nie określisz hello struktury danych za pomocą hello **struktury** właściwości w definicji zestawu danych hello, hello usługi fabryka danych wnioskuje schemat hello przy użyciu danych hello hello pierwszego wiersza.</span><span class="sxs-lookup"><span data-stu-id="bf95f-152">If you do not specify hello structure of data by using hello **structure** property in hello dataset definition, hello Data Factory service infers hello schema by using hello first row in hello data.</span></span> <span data-ttu-id="bf95f-153">W takim przypadku jeśli pierwszy wiersz hello nie zawiera pełnej schematu hello, niektóre kolumny będą niedostępne w hello wynik operacji kopiowania.</span><span class="sxs-lookup"><span data-stu-id="bf95f-153">In this case, if hello first row does not contain hello full schema, some columns will be missing in hello result of copy operation.</span></span>

<span data-ttu-id="bf95f-154">W związku z tym dla źródeł danych bez schematu hello najlepszym rozwiązaniem jest toospecify hello struktury danych za pomocą hello **struktury** właściwości.</span><span class="sxs-lookup"><span data-stu-id="bf95f-154">Therefore, for schema-free data sources, hello best practice is toospecify hello structure of data using hello **structure** property.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="bf95f-155">Właściwości działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="bf95f-155">Copy activity properties</span></span>
<span data-ttu-id="bf95f-156">Pełną listę sekcje & właściwości dostępne do definiowania działań można znaleźć toohello [tworzenie potoków](data-factory-create-pipelines.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="bf95f-156">For a full list of sections & properties available for defining activities please refer toohello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="bf95f-157">Właściwości, takie jak nazwa, opis, dane wejściowe i wyjściowe tabel i zasady są dostępne dla wszystkich typów działań.</span><span class="sxs-lookup"><span data-stu-id="bf95f-157">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

> [!NOTE]
> <span data-ttu-id="bf95f-158">Witaj działanie kopiowania przyjmuje tylko jeden parametr wejściowy i tworzy tylko jedno wyjście.</span><span class="sxs-lookup"><span data-stu-id="bf95f-158">hello Copy Activity takes only one input and produces only one output.</span></span>

<span data-ttu-id="bf95f-159">Właściwości dostępne w sekcji typeProperties hello aktywności hello na powitania drugiej różnią się każdy typ działania, a w przypadku działania kopiowania różnią się w zależności od typów hello źródeł i sink.</span><span class="sxs-lookup"><span data-stu-id="bf95f-159">Properties available in hello typeProperties section of hello activity on hello other hand vary with each activity type and in case of Copy activity they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="bf95f-160">W przypadku działania kopiowania, gdy źródłem jest typu **DocumentDbCollectionSource** hello następujące właściwości są dostępne w **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="bf95f-160">In case of Copy activity when source is of type **DocumentDbCollectionSource** hello following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="bf95f-161">**Właściwość**</span><span class="sxs-lookup"><span data-stu-id="bf95f-161">**Property**</span></span> | <span data-ttu-id="bf95f-162">**Opis**</span><span class="sxs-lookup"><span data-stu-id="bf95f-162">**Description**</span></span> | <span data-ttu-id="bf95f-163">**Dozwolone wartości**</span><span class="sxs-lookup"><span data-stu-id="bf95f-163">**Allowed values**</span></span> | <span data-ttu-id="bf95f-164">**Wymagane**</span><span class="sxs-lookup"><span data-stu-id="bf95f-164">**Required**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="bf95f-165">query</span><span class="sxs-lookup"><span data-stu-id="bf95f-165">query</span></span> |<span data-ttu-id="bf95f-166">Określ hello zapytania tooread dane.</span><span class="sxs-lookup"><span data-stu-id="bf95f-166">Specify hello query tooread data.</span></span> |<span data-ttu-id="bf95f-167">Wyślij zapytanie do ciągu obsługuje bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="bf95f-167">Query string supported by Azure Cosmos DB.</span></span> <br/><br/><span data-ttu-id="bf95f-168">Przykład:`SELECT c.BusinessEntityID, c.PersonType, c.NameStyle, c.Title, c.Name.First AS FirstName, c.Name.Last AS LastName, c.Suffix, c.EmailPromotion FROM c WHERE c.ModifiedDate > \"2009-01-01T00:00:00\"`</span><span class="sxs-lookup"><span data-stu-id="bf95f-168">Example: `SELECT c.BusinessEntityID, c.PersonType, c.NameStyle, c.Title, c.Name.First AS FirstName, c.Name.Last AS LastName, c.Suffix, c.EmailPromotion FROM c WHERE c.ModifiedDate > \"2009-01-01T00:00:00\"`</span></span> |<span data-ttu-id="bf95f-169">Nie</span><span class="sxs-lookup"><span data-stu-id="bf95f-169">No</span></span> <br/><br/><span data-ttu-id="bf95f-170">Jeśli nie zostanie określony, hello instrukcji SQL, która jest wykonywana:`select <columns defined in structure> from mycollection`</span><span class="sxs-lookup"><span data-stu-id="bf95f-170">If not specified, hello SQL statement that is executed: `select <columns defined in structure> from mycollection`</span></span> |
| <span data-ttu-id="bf95f-171">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="bf95f-171">nestingSeparator</span></span> |<span data-ttu-id="bf95f-172">Tooindicate znak specjalny, który hello dokumentu jest zagnieżdżony.</span><span class="sxs-lookup"><span data-stu-id="bf95f-172">Special character tooindicate that hello document is nested</span></span> |<span data-ttu-id="bf95f-173">Dowolny znak.</span><span class="sxs-lookup"><span data-stu-id="bf95f-173">Any character.</span></span> <br/><br/><span data-ttu-id="bf95f-174">Azure DB rozwiązania Cosmos jest magazynem NoSQL dla dokumentów JSON, których struktury zagnieżdżone są dozwolone.</span><span class="sxs-lookup"><span data-stu-id="bf95f-174">Azure Cosmos DB is a NoSQL store for JSON documents, where nested structures are allowed.</span></span> <span data-ttu-id="bf95f-175">Fabryka danych Azure umożliwia hierarchii toodenote użytkownika za pośrednictwem nestingSeparator, czyli "."</span><span class="sxs-lookup"><span data-stu-id="bf95f-175">Azure Data Factory enables user toodenote hierarchy via nestingSeparator, which is “.”</span></span> <span data-ttu-id="bf95f-176">w hello powyżej przykłady.</span><span class="sxs-lookup"><span data-stu-id="bf95f-176">in hello above examples.</span></span> <span data-ttu-id="bf95f-177">Z separatorem hello działanie kopiowania hello wygeneruje obiektu "Name" hello z trzech elementów podrzędnych elementów pierwszy, środkowy i ostatnich, zgodnie z too"Name.First", "Name.Middle" i "Name.Last" w hello definicja tabeli.</span><span class="sxs-lookup"><span data-stu-id="bf95f-177">With hello separator, hello copy activity will generate hello “Name” object with three children elements First, Middle and Last, according too“Name.First”, “Name.Middle” and “Name.Last” in hello table definition.</span></span> |<span data-ttu-id="bf95f-178">Nie</span><span class="sxs-lookup"><span data-stu-id="bf95f-178">No</span></span> |

<span data-ttu-id="bf95f-179">**DocumentDbCollectionSink** obsługuje hello następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="bf95f-179">**DocumentDbCollectionSink** supports hello following properties:</span></span>

| <span data-ttu-id="bf95f-180">**Właściwość**</span><span class="sxs-lookup"><span data-stu-id="bf95f-180">**Property**</span></span> | <span data-ttu-id="bf95f-181">**Opis**</span><span class="sxs-lookup"><span data-stu-id="bf95f-181">**Description**</span></span> | <span data-ttu-id="bf95f-182">**Dozwolone wartości**</span><span class="sxs-lookup"><span data-stu-id="bf95f-182">**Allowed values**</span></span> | <span data-ttu-id="bf95f-183">**Wymagane**</span><span class="sxs-lookup"><span data-stu-id="bf95f-183">**Required**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="bf95f-184">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="bf95f-184">nestingSeparator</span></span> |<span data-ttu-id="bf95f-185">Wymagany jest znak specjalny w tooindicate nazwa kolumny źródła hello, który zagnieżdżone dokumentu.</span><span class="sxs-lookup"><span data-stu-id="bf95f-185">A special character in hello source column name tooindicate that nested document is needed.</span></span> <br/><br/><span data-ttu-id="bf95f-186">Na przykład powyżej: `Name.First` w danych wyjściowych hello tabeli tworzy hello następującej strukturze JSON w dokumencie DB rozwiązania Cosmos hello:</span><span class="sxs-lookup"><span data-stu-id="bf95f-186">For example above: `Name.First` in hello output table produces hello following JSON structure in hello Cosmos DB document:</span></span><br/><br/><span data-ttu-id="bf95f-187">"Nazwa": {</span><span class="sxs-lookup"><span data-stu-id="bf95f-187">"Name": {</span></span><br/>    <span data-ttu-id="bf95f-188">"Pierwszy": "Jan"</span><span class="sxs-lookup"><span data-stu-id="bf95f-188">"First": "John"</span></span><br/><span data-ttu-id="bf95f-189">},</span><span class="sxs-lookup"><span data-stu-id="bf95f-189">},</span></span> |<span data-ttu-id="bf95f-190">Znak, który jest używany tooseparate poziomów zagnieżdżenia.</span><span class="sxs-lookup"><span data-stu-id="bf95f-190">Character that is used tooseparate nesting levels.</span></span><br/><br/><span data-ttu-id="bf95f-191">Wartość domyślna to `.` (kropką).</span><span class="sxs-lookup"><span data-stu-id="bf95f-191">Default value is `.` (dot).</span></span> |<span data-ttu-id="bf95f-192">Znak, który jest używany tooseparate poziomów zagnieżdżenia.</span><span class="sxs-lookup"><span data-stu-id="bf95f-192">Character that is used tooseparate nesting levels.</span></span> <br/><br/><span data-ttu-id="bf95f-193">Wartość domyślna to `.` (kropką).</span><span class="sxs-lookup"><span data-stu-id="bf95f-193">Default value is `.` (dot).</span></span> |
| <span data-ttu-id="bf95f-194">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="bf95f-194">writeBatchSize</span></span> |<span data-ttu-id="bf95f-195">Liczba równoległe żądań tooAzure DB rozwiązania Cosmos usługi toocreate dokumentów.</span><span class="sxs-lookup"><span data-stu-id="bf95f-195">Number of parallel requests tooAzure Cosmos DB service toocreate documents.</span></span><br/><br/><span data-ttu-id="bf95f-196">Aby precyzyjnie zdefiniować hello wydajności podczas kopiowania danych z bazy danych usługi rozwiązania Cosmos przy użyciu tej właściwości.</span><span class="sxs-lookup"><span data-stu-id="bf95f-196">You can fine-tune hello performance when copying data to/from Cosmos DB by using this property.</span></span> <span data-ttu-id="bf95f-197">Wraz ze zwiększeniem writeBatchSize, ponieważ więcej tooCosmos równoległych żądań bazy danych są wysyłane, może spodziewać się lepszą wydajność.</span><span class="sxs-lookup"><span data-stu-id="bf95f-197">You can expect a better performance when you increase writeBatchSize because more parallel requests tooCosmos DB are sent.</span></span> <span data-ttu-id="bf95f-198">Jednak potrzebny tooavoid ograniczania przepustowości, który może zgłaszać komunikat o błędzie hello: "jest duża szybkość żądania".</span><span class="sxs-lookup"><span data-stu-id="bf95f-198">However you’ll need tooavoid throttling that can throw hello error message: "Request rate is large".</span></span><br/><br/><span data-ttu-id="bf95f-199">Ograniczanie zadecyduje o wiele czynników, w tym rozmiar dokumentów, liczbę dokumentów, indeksowania zasady kolekcji docelowej, itd. Operacje kopiowania, można użyć lepsze hello toohave kolekcji (np. S3) większości dostępna przepustowość (2500 żądań jednostek na sekundę).</span><span class="sxs-lookup"><span data-stu-id="bf95f-199">Throttling is decided by a number of factors, including size of documents, number of terms in documents, indexing policy of target collection, etc. For copy operations, you can use a better collection (e.g. S3) toohave hello most throughput available (2,500 request units/second).</span></span> |<span data-ttu-id="bf95f-200">Liczba całkowita</span><span class="sxs-lookup"><span data-stu-id="bf95f-200">Integer</span></span> |<span data-ttu-id="bf95f-201">Nie (domyślne: 5)</span><span class="sxs-lookup"><span data-stu-id="bf95f-201">No (default: 5)</span></span> |
| <span data-ttu-id="bf95f-202">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="bf95f-202">writeBatchTimeout</span></span> |<span data-ttu-id="bf95f-203">Czas toocomplete operacji hello oczekiwania, zanim upłynie limit czasu.</span><span class="sxs-lookup"><span data-stu-id="bf95f-203">Wait time for hello operation toocomplete before it times out.</span></span> |<span data-ttu-id="bf95f-204">Zakres czasu</span><span class="sxs-lookup"><span data-stu-id="bf95f-204">timespan</span></span><br/><br/> <span data-ttu-id="bf95f-205">Przykład: "00: 30:00" (30 minut).</span><span class="sxs-lookup"><span data-stu-id="bf95f-205">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="bf95f-206">Nie</span><span class="sxs-lookup"><span data-stu-id="bf95f-206">No</span></span> |

## <a name="importexport-json-documents"></a><span data-ttu-id="bf95f-207">Dokumentów JSON Import/Eksport</span><span class="sxs-lookup"><span data-stu-id="bf95f-207">Import/Export JSON documents</span></span>
<span data-ttu-id="bf95f-208">Korzystając z tego łącznika DB rozwiązania Cosmos, można łatwo</span><span class="sxs-lookup"><span data-stu-id="bf95f-208">Using this Cosmos DB connector, you can easily</span></span>

* <span data-ttu-id="bf95f-209">Zaimportuj dokumentów JSON z różnych źródeł do rozwiązania Cosmos bazy danych, w tym obiektów Blob platformy Azure, usługa Azure Data Lake, lokalnego systemu plików lub innych magazynów opartych na plikach obsługiwane przez usługi fabryka danych Azure.</span><span class="sxs-lookup"><span data-stu-id="bf95f-209">Import JSON documents from various sources into Cosmos DB, including Azure Blob, Azure Data Lake, on-premises File System or other file-based stores supported by Azure Data Factory.</span></span>
* <span data-ttu-id="bf95f-210">Wyeksportuj dokumentów JSON z collecton rozwiązania Cosmos bazy danych do różnych magazynów opartych na plikach.</span><span class="sxs-lookup"><span data-stu-id="bf95f-210">Export JSON documents from Cosmos DB collecton into various file-based stores.</span></span>
* <span data-ttu-id="bf95f-211">Migrowanie danych między dwoma kolekcje DB rozwiązania Cosmos w postaci — jest.</span><span class="sxs-lookup"><span data-stu-id="bf95f-211">Migrate data between two Cosmos DB collections as-is.</span></span>

<span data-ttu-id="bf95f-212">Skopiuj takiego schematu niezależny od tooachieve</span><span class="sxs-lookup"><span data-stu-id="bf95f-212">tooachieve such schema-agnostic copy,</span></span> 
* <span data-ttu-id="bf95f-213">Korzystając z Kreatora kopiowania, sprawdź hello **"wyeksportować w postaci — jest tooJSON plików lub rozwiązania Cosmos bazy danych kolekcji"** opcji.</span><span class="sxs-lookup"><span data-stu-id="bf95f-213">When using copy wizard, check hello **"Export as-is tooJSON files or Cosmos DB collection"** option.</span></span>
* <span data-ttu-id="bf95f-214">Gdy edycję JSON, nie należy określać sekcji "structure" hello w opublikowanych DB rozwiązania Cosmos ani właściwości "nestingSeparator" dla bazy danych rozwiązania Cosmos źródło/ujście w przypadku działania kopiowania.</span><span class="sxs-lookup"><span data-stu-id="bf95f-214">When using JSON editing, do not specify hello "structure" section in Cosmos DB dataset(s) nor "nestingSeparator" property on Cosmos DB source/sink in copy activity.</span></span> <span data-ttu-id="bf95f-215">tooimport z / tooJSON pliki eksportu, hello pliku magazynu danych należy określić typ formatu jako "JsonFormat", "filePattern" config i Pomiń hello rest format ustawień, zobacz [formatu JSON](data-factory-supported-file-and-compression-formats.md#json-format) sekcji Szczegóły.</span><span class="sxs-lookup"><span data-stu-id="bf95f-215">tooimport from/export tooJSON files, in hello file store dataset specify format type as "JsonFormat", config "filePattern" and skip hello rest format settings, see [JSON format](data-factory-supported-file-and-compression-formats.md#json-format) section on details.</span></span>

## <a name="json-examples"></a><span data-ttu-id="bf95f-216">Przykłady JSON</span><span class="sxs-lookup"><span data-stu-id="bf95f-216">JSON examples</span></span>
<span data-ttu-id="bf95f-217">Witaj poniższe przykłady zapewniają definicje JSON przy użyciu można toocreate potoku [portalu Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) lub [programu Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) lub [programu Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="bf95f-217">hello following examples provide sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="bf95f-218">Przedstawiają sposób toocopy tooand danych z bazy danych Azure rozwiązania Cosmos i magazynu obiektów Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="bf95f-218">They show how toocopy data tooand from Azure Cosmos DB and Azure Blob Storage.</span></span> <span data-ttu-id="bf95f-219">Jednak dane mogą być kopiowane **bezpośrednio** za pomocą dowolnego hello tooany źródeł z wychwytywanie hello podane [tutaj](data-factory-data-movement-activities.md#supported-data-stores-and-formats) przy użyciu hello działanie kopiowania w fabryce danych Azure.</span><span class="sxs-lookup"><span data-stu-id="bf95f-219">However, data can be copied **directly** from any of hello sources tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>

## <a name="example-copy-data-from-azure-cosmos-db-tooazure-blob"></a><span data-ttu-id="bf95f-220">Przykład: Kopiowanie danych z bazy danych Azure rozwiązania Cosmos tooAzure obiektów Blob</span><span class="sxs-lookup"><span data-stu-id="bf95f-220">Example: Copy data from Azure Cosmos DB tooAzure Blob</span></span>
<span data-ttu-id="bf95f-221">Poniższy przykład Hello zawiera:</span><span class="sxs-lookup"><span data-stu-id="bf95f-221">hello sample below shows:</span></span>

1. <span data-ttu-id="bf95f-222">Połączonej usługi typu [DocumentDb](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="bf95f-222">A linked service of type [DocumentDb](#linked-service-properties).</span></span>
2. <span data-ttu-id="bf95f-223">Połączonej usługi typu [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="bf95f-223">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="bf95f-224">Dane wejściowe [dataset](data-factory-create-datasets.md) typu [DocumentDbCollection](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="bf95f-224">An input [dataset](data-factory-create-datasets.md) of type [DocumentDbCollection](#dataset-properties).</span></span>
4. <span data-ttu-id="bf95f-225">Dane wyjściowe [dataset](data-factory-create-datasets.md) typu [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="bf95f-225">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="bf95f-226">A [potoku](data-factory-create-pipelines.md) z działaniem kopii, która używa [DocumentDbCollectionSource](#copy-activity-properties) i [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="bf95f-226">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [DocumentDbCollectionSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="bf95f-227">przykład Witaj kopiuje dane w tooAzure bazy danych rozwiązania Cosmos Azure Blob.</span><span class="sxs-lookup"><span data-stu-id="bf95f-227">hello sample copies data in Azure Cosmos DB tooAzure Blob.</span></span> <span data-ttu-id="bf95f-228">właściwości JSON Hello używane w te przykłady są opisane w sekcjach poniżej hello próbek.</span><span class="sxs-lookup"><span data-stu-id="bf95f-228">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="bf95f-229">**Azure DB rozwiązania Cosmos połączonej usługi:**</span><span class="sxs-lookup"><span data-stu-id="bf95f-229">**Azure Cosmos DB linked service:**</span></span>

```JSON
{
  "name": "CosmosDbLinkedService",
  "properties": {
    "type": "DocumentDb",
    "typeProperties": {
      "connectionString": "AccountEndpoint=<EndpointUrl>;AccountKey=<AccessKey>;Database=<Database>"
    }
  }
}
```
<span data-ttu-id="bf95f-230">**Magazyn obiektów Blob Azure połączonej usługi:**</span><span class="sxs-lookup"><span data-stu-id="bf95f-230">**Azure Blob storage linked service:**</span></span>

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
<span data-ttu-id="bf95f-231">**Azure DB dokument wejściowy zestaw danych:**</span><span class="sxs-lookup"><span data-stu-id="bf95f-231">**Azure Document DB input dataset:**</span></span>

<span data-ttu-id="bf95f-232">Przykładowe Hello zakłada istnieje kolekcja o nazwie **osoby** w bazie danych bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="bf95f-232">hello sample assumes you have a collection named **Person** in an Azure Cosmos DB database.</span></span>

<span data-ttu-id="bf95f-233">Ustawienie "external": "true" i określenie externalData informacje o zasadach hello fabryki danych Azure Usługa tabeli hello zewnętrznych toohello fabryki danych i nie są produkowane przez działanie w fabryce danych hello.</span><span class="sxs-lookup"><span data-stu-id="bf95f-233">Setting “external”: ”true” and specifying externalData policy information hello Azure Data Factory service that hello table is external toohello data factory and not produced by an activity in hello data factory.</span></span>

```JSON
{
  "name": "PersonCosmosDbTable",
  "properties": {
    "type": "DocumentDbCollection",
    "linkedServiceName": "CosmosDbLinkedService",
    "typeProperties": {
      "collectionName": "Person"
    },
    "external": true,
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```

<span data-ttu-id="bf95f-234">**Azure Blob wyjściowy zestaw danych:**</span><span class="sxs-lookup"><span data-stu-id="bf95f-234">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="bf95f-235">Dane są skopiowanych tooa nowego obiektu blob co godzinę o ścieżce hello obiektu blob hello odzwierciedlające hello określonej daty/godziny z szczegółowości godzinę.</span><span class="sxs-lookup"><span data-stu-id="bf95f-235">Data is copied tooa new blob every hour with hello path for hello blob reflecting hello specific datetime with hour granularity.</span></span>

```JSON
{
  "name": "PersonBlobTableOut",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "docdb",
      "format": {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "nullValue": "NULL"
      }
    },
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```
<span data-ttu-id="bf95f-236">Przykładowy dokument JSON w hello osoby kolekcji w bazie danych DB rozwiązania Cosmos:</span><span class="sxs-lookup"><span data-stu-id="bf95f-236">Sample JSON document in hello Person collection in a Cosmos DB database:</span></span>

```JSON
{
  "PersonId": 2,
  "Name": {
    "First": "Jane",
    "Middle": "",
    "Last": "Doe"
  }
}
```
<span data-ttu-id="bf95f-237">Rozwiązania cosmos bazy danych obsługuje tworzenie zapytań dla dokumentów przy użyciu składni SQL przez hierarchiczna dokumentów JSON.</span><span class="sxs-lookup"><span data-stu-id="bf95f-237">Cosmos DB supports querying documents using a SQL like syntax over hierarchical JSON documents.</span></span>

<span data-ttu-id="bf95f-238">Przykład:</span><span class="sxs-lookup"><span data-stu-id="bf95f-238">Example:</span></span> 

```sql
SELECT Person.PersonId, Person.Name.First AS FirstName, Person.Name.Middle as MiddleName, Person.Name.Last AS LastName FROM Person
```

<span data-ttu-id="bf95f-239">następujące Hello potoku kopie danych z hello kolekcji osoby w hello Azure DB rozwiązania Cosmos tooan bazy danych obiektów blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="bf95f-239">hello following pipeline copies data from hello Person collection in hello Azure Cosmos DB database tooan Azure blob.</span></span> <span data-ttu-id="bf95f-240">W ramach hello działania kopiowania hello określono wejściowych i wyjściowych zestawów danych.</span><span class="sxs-lookup"><span data-stu-id="bf95f-240">As part of hello copy activity hello input and output datasets have been specified.</span></span>  

```JSON
{
  "name": "DocDbToBlobPipeline",
  "properties": {
    "activities": [
      {
        "type": "Copy",
        "typeProperties": {
          "source": {
            "type": "DocumentDbCollectionSource",
            "query": "SELECT Person.Id, Person.Name.First AS FirstName, Person.Name.Middle as MiddleName, Person.Name.Last AS LastName FROM Person",
            "nestingSeparator": "."
          },
          "sink": {
            "type": "BlobSink",
            "blobWriterAddHeader": true,
            "writeBatchSize": 1000,
            "writeBatchTimeout": "00:00:59"
          }
        },
        "inputs": [
          {
            "name": "PersonCosmosDbTable"
          }
        ],
        "outputs": [
          {
            "name": "PersonBlobTableOut"
          }
        ],
        "policy": {
          "concurrency": 1
        },
        "name": "CopyFromDocDbToBlob"
      }
    ],
    "start": "2015-04-01T00:00:00Z",
    "end": "2015-04-02T00:00:00Z"
  }
}
```
## <a name="example-copy-data-from-azure-blob-tooazure-cosmos-db"></a><span data-ttu-id="bf95f-241">Przykład: Kopiowanie danych z obiektu Blob Azure tooAzure DB rozwiązania Cosmos</span><span class="sxs-lookup"><span data-stu-id="bf95f-241">Example: Copy data from Azure Blob tooAzure Cosmos DB</span></span> 
<span data-ttu-id="bf95f-242">Poniższy przykład Hello zawiera:</span><span class="sxs-lookup"><span data-stu-id="bf95f-242">hello sample below shows:</span></span>

1. <span data-ttu-id="bf95f-243">Połączonej usługi typu [DocumentDb](#azure-documentdb-linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="bf95f-243">A linked service of type [DocumentDb](#azure-documentdb-linked-service-properties).</span></span>
2. <span data-ttu-id="bf95f-244">Połączonej usługi typu [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="bf95f-244">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="bf95f-245">Dane wejściowe [dataset](data-factory-create-datasets.md) typu [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="bf95f-245">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="bf95f-246">Dane wyjściowe [dataset](data-factory-create-datasets.md) typu [DocumentDbCollection](#azure-documentdb-dataset-type-properties).</span><span class="sxs-lookup"><span data-stu-id="bf95f-246">An output [dataset](data-factory-create-datasets.md) of type [DocumentDbCollection](#azure-documentdb-dataset-type-properties).</span></span>
5. <span data-ttu-id="bf95f-247">A [potoku](data-factory-create-pipelines.md) z działaniem kopii, która używa [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) i [DocumentDbCollectionSink](#azure-documentdb-copy-activity-type-properties).</span><span class="sxs-lookup"><span data-stu-id="bf95f-247">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [DocumentDbCollectionSink](#azure-documentdb-copy-activity-type-properties).</span></span>

<span data-ttu-id="bf95f-248">przykład Witaj kopiuje dane z tooAzure obiektów blob platformy Azure DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="bf95f-248">hello sample copies data from Azure blob tooAzure Cosmos DB.</span></span> <span data-ttu-id="bf95f-249">właściwości JSON Hello używane w te przykłady są opisane w sekcjach poniżej hello próbek.</span><span class="sxs-lookup"><span data-stu-id="bf95f-249">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="bf95f-250">**Magazyn obiektów Blob Azure połączonej usługi:**</span><span class="sxs-lookup"><span data-stu-id="bf95f-250">**Azure Blob storage linked service:**</span></span>

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
<span data-ttu-id="bf95f-251">**Azure DB rozwiązania Cosmos połączonej usługi:**</span><span class="sxs-lookup"><span data-stu-id="bf95f-251">**Azure Cosmos DB linked service:**</span></span>

```JSON
{
  "name": "CosmosDbLinkedService",
  "properties": {
    "type": "DocumentDb",
    "typeProperties": {
      "connectionString": "AccountEndpoint=<EndpointUrl>;AccountKey=<AccessKey>;Database=<Database>"
    }
  }
}
```
<span data-ttu-id="bf95f-252">**Azure wejściowego zestawu danych obiektów Blob:**</span><span class="sxs-lookup"><span data-stu-id="bf95f-252">**Azure Blob input dataset:**</span></span>

```JSON
{
  "name": "PersonBlobTableIn",
  "properties": {
    "structure": [
      {
        "name": "Id",
        "type": "Int"
      },
      {
        "name": "FirstName",
        "type": "String"
      },
      {
        "name": "MiddleName",
        "type": "String"
      },
      {
        "name": "LastName",
        "type": "String"
      }
    ],
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "fileName": "input.csv",
      "folderPath": "docdb",
      "format": {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "nullValue": "NULL"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```
<span data-ttu-id="bf95f-253">**Azure DB rozwiązania Cosmos wyjściowy zestaw danych:**</span><span class="sxs-lookup"><span data-stu-id="bf95f-253">**Azure Cosmos DB output dataset:**</span></span>

<span data-ttu-id="bf95f-254">przykład Witaj kopiuje kolekcję tooa danych o nazwie "Osoba".</span><span class="sxs-lookup"><span data-stu-id="bf95f-254">hello sample copies data tooa collection named “Person”.</span></span>

```JSON
{
  "name": "PersonCosmosDbTableOut",
  "properties": {
    "structure": [
      {
        "name": "Id",
        "type": "Int"
      },
      {
        "name": "Name.First",
        "type": "String"
      },
      {
        "name": "Name.Middle",
        "type": "String"
      },
      {
        "name": "Name.Last",
        "type": "String"
      }
    ],
    "type": "DocumentDbCollection",
    "linkedServiceName": "CosmosDbLinkedService",
    "typeProperties": {
      "collectionName": "Person"
    },
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```
<span data-ttu-id="bf95f-255">następujące Hello potoku kopie danych z obiektu Blob Azure toohello kolekcji osoby w hello DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="bf95f-255">hello following pipeline copies data from Azure Blob toohello Person collection in hello Cosmos DB.</span></span> <span data-ttu-id="bf95f-256">W ramach hello działania kopiowania hello określono wejściowych i wyjściowych zestawów danych.</span><span class="sxs-lookup"><span data-stu-id="bf95f-256">As part of hello copy activity hello input and output datasets have been specified.</span></span>

```JSON
{
  "name": "BlobToDocDbPipeline",
  "properties": {
    "activities": [
      {
        "type": "Copy",
        "typeProperties": {
          "source": {
            "type": "BlobSource"
          },
          "sink": {
            "type": "DocumentDbCollectionSink",
            "nestingSeparator": ".",
            "writeBatchSize": 2,
            "writeBatchTimeout": "00:00:00"
          }
          "translator": {
              "type": "TabularTranslator",
              "ColumnMappings": "FirstName: Name.First, MiddleName: Name.Middle, LastName: Name.Last, BusinessEntityID: BusinessEntityID, PersonType: PersonType, NameStyle: NameStyle, title: aaaTitle, Suffix: Suffix, EmailPromotion: EmailPromotion, rowguid: rowguid, ModifiedDate: ModifiedDate"
          }
        },
        "inputs": [
          {
            "name": "PersonBlobTableIn"
          }
        ],
        "outputs": [
          {
            "name": "PersonCosmosDbTableOut"
          }
        ],
        "policy": {
          "concurrency": 1
        },
        "name": "CopyFromBlobToDocDb"
      }
    ],
    "start": "2015-04-14T00:00:00Z",
    "end": "2015-04-15T00:00:00Z"
  }
}
```
<span data-ttu-id="bf95f-257">Jeśli hello przykładowe dane wejściowe obiektu blob jest jako</span><span class="sxs-lookup"><span data-stu-id="bf95f-257">If hello sample blob input is as</span></span>

```
1,John,,Doe
```
<span data-ttu-id="bf95f-258">Następnie będzie hello dane wyjściowe JSON do rozwiązania Cosmos bazy danych jako:</span><span class="sxs-lookup"><span data-stu-id="bf95f-258">Then hello output JSON in Cosmos DB will be as:</span></span>

```JSON
{
  "Id": 1,
  "Name": {
    "First": "John",
    "Middle": null,
    "Last": "Doe"
  },
  "id": "a5e8595c-62ec-4554-a118-3940f4ff70b6"
}
```
<span data-ttu-id="bf95f-259">Azure DB rozwiązania Cosmos jest magazynem NoSQL dla dokumentów JSON, których struktury zagnieżdżone są dozwolone.</span><span class="sxs-lookup"><span data-stu-id="bf95f-259">Azure Cosmos DB is a NoSQL store for JSON documents, where nested structures are allowed.</span></span> <span data-ttu-id="bf95f-260">Fabryka danych Azure umożliwia hierarchii toodenote użytkownika za pośrednictwem **nestingSeparator**, czyli "."</span><span class="sxs-lookup"><span data-stu-id="bf95f-260">Azure Data Factory enables user toodenote hierarchy via **nestingSeparator**, which is “.”</span></span> <span data-ttu-id="bf95f-261">w tym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="bf95f-261">in this example.</span></span> <span data-ttu-id="bf95f-262">Z separatorem hello działanie kopiowania hello wygeneruje obiektu "Name" hello z trzech elementów podrzędnych elementów pierwszy, środkowy i ostatnich, zgodnie z too"Name.First", "Name.Middle" i "Name.Last" w hello definicja tabeli.</span><span class="sxs-lookup"><span data-stu-id="bf95f-262">With hello separator, hello copy activity will generate hello “Name” object with three children elements First, Middle and Last, according too“Name.First”, “Name.Middle” and “Name.Last” in hello table definition.</span></span>

## <a name="appendix"></a><span data-ttu-id="bf95f-263">Dodatek</span><span class="sxs-lookup"><span data-stu-id="bf95f-263">Appendix</span></span>
1. <span data-ttu-id="bf95f-264">**Pytanie:** hello aktualizacja obsługi działania kopiowania istniejących rekordów?</span><span class="sxs-lookup"><span data-stu-id="bf95f-264">**Question:** Does hello Copy Activity support update of existing records?</span></span>

    <span data-ttu-id="bf95f-265">**Odpowiedź:** nie.</span><span class="sxs-lookup"><span data-stu-id="bf95f-265">**Answer:** No.</span></span>
2. <span data-ttu-id="bf95f-266">**Pytanie:** jak ponowną próbę kopiowania tooAzure DB rozwiązania Cosmos dotyczą już skopiowane rekordy?</span><span class="sxs-lookup"><span data-stu-id="bf95f-266">**Question:** How does a retry of a copy tooAzure Cosmos DB deal with already copied records?</span></span>

    <span data-ttu-id="bf95f-267">**Odpowiedź:** Jeśli rekordy ma pole "ID" i operacji kopiowania hello próbuje tooinsert rekord z hello sam identyfikator operacji kopiowania hello zgłasza błąd.</span><span class="sxs-lookup"><span data-stu-id="bf95f-267">**Answer:** If records have an "ID" field and hello copy operation tries tooinsert a record with hello same ID, hello copy operation throws an error.</span></span>  
3. <span data-ttu-id="bf95f-268">**Pytanie:** fabryki danych obsługuje [zakres lub partycjonowanie danych opartych na skrót](../documentdb/documentdb-partition-data.md)?</span><span class="sxs-lookup"><span data-stu-id="bf95f-268">**Question:** Does Data Factory support [range or hash-based data partitioning](../documentdb/documentdb-partition-data.md)?</span></span>

    <span data-ttu-id="bf95f-269">**Odpowiedź:** nie.</span><span class="sxs-lookup"><span data-stu-id="bf95f-269">**Answer:** No.</span></span>
4. <span data-ttu-id="bf95f-270">**Pytanie:** można określić więcej niż jednej bazy danych Azure rozwiązania Cosmos kolekcji dla tabeli?</span><span class="sxs-lookup"><span data-stu-id="bf95f-270">**Question:** Can I specify more than one Azure Cosmos DB collection for a table?</span></span>

    <span data-ttu-id="bf95f-271">**Odpowiedź:** nie.</span><span class="sxs-lookup"><span data-stu-id="bf95f-271">**Answer:** No.</span></span> <span data-ttu-id="bf95f-272">W tym momencie można określić tylko jedną kolekcję.</span><span class="sxs-lookup"><span data-stu-id="bf95f-272">Only one collection can be specified at this time.</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="bf95f-273">Wydajność i dostrajania</span><span class="sxs-lookup"><span data-stu-id="bf95f-273">Performance and Tuning</span></span>
<span data-ttu-id="bf95f-274">Zobacz [wydajności działania kopiowania & dostrajanie przewodnik](data-factory-copy-activity-performance.md) toolearn o kluczu czynniki tego wydajność wpływ przenoszenia danych (działanie kopiowania) w usłudze fabryka danych Azure i różne sposoby toooptimize go.</span><span class="sxs-lookup"><span data-stu-id="bf95f-274">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
