---
title: "Przenoszenie danych do/z bazy danych Azure rozwiązania Cosmos | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 7a11c6ade0325b08ad520448bbf82d64a0a555f3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="move-data-to-and-from-azure-cosmos-db-using-azure-data-factory"></a><span data-ttu-id="18971-103">Przenoszenie danych do i z bazy danych rozwiązania Cosmos Azure przy użyciu fabryki danych Azure</span><span class="sxs-lookup"><span data-stu-id="18971-103">Move data to and from Azure Cosmos DB using Azure Data Factory</span></span>
<span data-ttu-id="18971-104">W tym artykule opisano sposób używania działania kopiowania w fabryce danych Azure do przeniesienia danych z bazy danych Azure rozwiązania Cosmos (interfejsu API usługi DocumentDB).</span><span class="sxs-lookup"><span data-stu-id="18971-104">This article explains how to use the Copy Activity in Azure Data Factory to move data to/from Azure Cosmos DB (DocumentDB API).</span></span> <span data-ttu-id="18971-105">Opiera się na [działań przepływu danych](data-factory-data-movement-activities.md) artykułu, który przedstawia ogólny przegląd przenoszenia danych z działania kopiowania.</span><span class="sxs-lookup"><span data-stu-id="18971-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span> 

<span data-ttu-id="18971-106">Dane należy skopiować z dowolnego źródła obsługiwanych magazynu danych do bazy danych Azure rozwiązania Cosmos lub z bazy danych usługi Azure rozwiązania Cosmos żadnych obsługiwanych ujścia magazynu danych.</span><span class="sxs-lookup"><span data-stu-id="18971-106">You can copy data from any supported source data store to Azure Cosmos DB or from Azure Cosmos DB to any supported sink data store.</span></span> <span data-ttu-id="18971-107">Lista magazynów danych obsługiwane jako źródła lub wychwytywanie przez działanie kopiowania, zobacz [obsługiwane magazyny danych](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabeli.</span><span class="sxs-lookup"><span data-stu-id="18971-107">For a list of data stores supported as sources or sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="18971-108">Łącznik usługi Azure DB rozwiązania Cosmos obsługują tylko interfejsu API usługi DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="18971-108">Azure Cosmos DB connector only support DocumentDB API.</span></span>

<span data-ttu-id="18971-109">Aby skopiować dane jako — jest do/z pliki w formacie JSON lub innej kolekcji rozwiązania Cosmos bazy danych, zobacz [dokumentów JSON importu/eksportu](#importexport-json-documents).</span><span class="sxs-lookup"><span data-stu-id="18971-109">To copy data as-is to/from JSON files or another Cosmos DB collection, see [Import/Export JSON documents](#importexport-json-documents).</span></span>

## <a name="getting-started"></a><span data-ttu-id="18971-110">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="18971-110">Getting started</span></span>
<span data-ttu-id="18971-111">Można utworzyć potoku o działanie kopiowania, który przenosi dane z bazy danych rozwiązania Cosmos Azure przy użyciu różnych narzędzi/interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="18971-111">You can create a pipeline with a copy activity that moves data to/from Azure Cosmos DB by using different tools/APIs.</span></span>

<span data-ttu-id="18971-112">Najprostszym sposobem, aby utworzyć potok jest użycie **kreatora kopiowania**.</span><span class="sxs-lookup"><span data-stu-id="18971-112">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="18971-113">Zobacz [samouczek: tworzenie potoku za pomocą Kreatora kopiowania](data-factory-copy-data-wizard-tutorial.md) szybkie przewodnik dotyczący tworzenia potoku za pomocą Kreatora kopiowania danych.</span><span class="sxs-lookup"><span data-stu-id="18971-113">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="18971-114">Umożliwia także następujące narzędzia do tworzenia potoku: **portalu Azure**, **programu Visual Studio**, **programu Azure PowerShell**, **szablonu usługi Azure Resource Manager**, **interfejs API .NET**, i **interfejsu API REST**.</span><span class="sxs-lookup"><span data-stu-id="18971-114">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="18971-115">Zobacz [samouczek działania kopiowania](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) instrukcje krok po kroku utworzyć potok z działaniem kopiowania.</span><span class="sxs-lookup"><span data-stu-id="18971-115">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="18971-116">Czy można użyć narzędzia i interfejsy API, należy wykonać następujące kroki, aby utworzyć potok, który przenosi dane z magazynu danych źródła do ujścia magazynu danych:</span><span class="sxs-lookup"><span data-stu-id="18971-116">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span> 

1. <span data-ttu-id="18971-117">Utwórz **połączone usługi** Aby połączyć dane wejściowe i wyjściowe są przechowywane w fabryce danych.</span><span class="sxs-lookup"><span data-stu-id="18971-117">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="18971-118">Utwórz **zestawów danych** do reprezentowania danych wejściowych i wyjściowych operacji kopiowania.</span><span class="sxs-lookup"><span data-stu-id="18971-118">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="18971-119">Utwórz **potoku** aktywnością kopiowania zestawu danych jako dane wejściowe i zestawu danych jako dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="18971-119">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="18971-120">Korzystając z kreatora, definicje JSON do tych jednostek fabryki danych (połączone usługi, zestawy danych i potoki) są tworzone automatycznie dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="18971-120">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="18971-121">Korzystając z narzędzi/API (z wyjątkiem interfejs API .NET), należy zdefiniować tych jednostek fabryki danych w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="18971-121">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="18971-122">Dla przykładów z definicji JSON dla jednostek fabryki danych, które służą do kopiowania danych do/z rozwiązania Cosmos bazy danych, zobacz [przykłady JSON](#json-examples) sekcji tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="18971-122">For samples with JSON definitions for Data Factory entities that are used to copy data to/from Cosmos DB, see [JSON examples](#json-examples) section of this article.</span></span> 

<span data-ttu-id="18971-123">Poniższe sekcje zawierają szczegółowe informacje o właściwości JSON, które są używane do definiowania jednostek fabryki danych określonej do rozwiązania Cosmos bazy danych:</span><span class="sxs-lookup"><span data-stu-id="18971-123">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Cosmos DB:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="18971-124">Połączona usługa właściwości</span><span class="sxs-lookup"><span data-stu-id="18971-124">Linked service properties</span></span>
<span data-ttu-id="18971-125">Poniższa tabela zawiera opis specyficzne dla usługi Azure DB rozwiązania Cosmos połączone elementy JSON.</span><span class="sxs-lookup"><span data-stu-id="18971-125">The following table provides description for JSON elements specific to Azure Cosmos DB linked service.</span></span>

| <span data-ttu-id="18971-126">**Właściwość**</span><span class="sxs-lookup"><span data-stu-id="18971-126">**Property**</span></span> | <span data-ttu-id="18971-127">**Opis**</span><span class="sxs-lookup"><span data-stu-id="18971-127">**Description**</span></span> | <span data-ttu-id="18971-128">**Wymagane**</span><span class="sxs-lookup"><span data-stu-id="18971-128">**Required**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="18971-129">type</span><span class="sxs-lookup"><span data-stu-id="18971-129">type</span></span> |<span data-ttu-id="18971-130">Właściwość type musi mieć ustawioną: **usługi DocumentDb**</span><span class="sxs-lookup"><span data-stu-id="18971-130">The type property must be set to: **DocumentDb**</span></span> |<span data-ttu-id="18971-131">Tak</span><span class="sxs-lookup"><span data-stu-id="18971-131">Yes</span></span> |
| <span data-ttu-id="18971-132">Parametry połączenia</span><span class="sxs-lookup"><span data-stu-id="18971-132">connectionString</span></span> |<span data-ttu-id="18971-133">Określ informacje potrzebne do łączenia z bazą danych Azure DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="18971-133">Specify information needed to connect to Azure Cosmos DB database.</span></span> |<span data-ttu-id="18971-134">Tak</span><span class="sxs-lookup"><span data-stu-id="18971-134">Yes</span></span> |

<span data-ttu-id="18971-135">Przykład:</span><span class="sxs-lookup"><span data-stu-id="18971-135">Example:</span></span>

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

## <a name="dataset-properties"></a><span data-ttu-id="18971-136">Właściwości zestawu danych</span><span class="sxs-lookup"><span data-stu-id="18971-136">Dataset properties</span></span>
<span data-ttu-id="18971-137">Pełną listę właściwości dostępne do definiowania zestawów danych & sekcje zapoznaj się [Tworzenie zbiorów danych](data-factory-create-datasets.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="18971-137">For a full list of sections & properties available for defining datasets please refer to the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="18971-138">Jak struktura, dostępności i zasad zestawu danych JSON jest podobna dla wszystkich typów obiektów dataset (Azure SQL, obiektów blob platformy Azure, Azure tabeli itp.).</span><span class="sxs-lookup"><span data-stu-id="18971-138">Sections like structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="18971-139">Sekcja typeProperties jest różne dla każdego typu zestawu danych i zawiera informacje o lokalizacji danych w magazynie danych.</span><span class="sxs-lookup"><span data-stu-id="18971-139">The typeProperties section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="18971-140">TypeProperties sekcja dla zestawu danych typu **DocumentDbCollection** ma następujące właściwości.</span><span class="sxs-lookup"><span data-stu-id="18971-140">The typeProperties section for the dataset of type **DocumentDbCollection** has the following properties.</span></span>

| <span data-ttu-id="18971-141">**Właściwość**</span><span class="sxs-lookup"><span data-stu-id="18971-141">**Property**</span></span> | <span data-ttu-id="18971-142">**Opis**</span><span class="sxs-lookup"><span data-stu-id="18971-142">**Description**</span></span> | <span data-ttu-id="18971-143">**Wymagane**</span><span class="sxs-lookup"><span data-stu-id="18971-143">**Required**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="18971-144">CollectionName</span><span class="sxs-lookup"><span data-stu-id="18971-144">collectionName</span></span> |<span data-ttu-id="18971-145">Nazwa kolekcji dokumentów DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="18971-145">Name of the Cosmos DB document collection.</span></span> |<span data-ttu-id="18971-146">Tak</span><span class="sxs-lookup"><span data-stu-id="18971-146">Yes</span></span> |

<span data-ttu-id="18971-147">Przykład:</span><span class="sxs-lookup"><span data-stu-id="18971-147">Example:</span></span>

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
### <a name="schema-by-data-factory"></a><span data-ttu-id="18971-148">Schemat fabryka danych</span><span class="sxs-lookup"><span data-stu-id="18971-148">Schema by Data Factory</span></span>
<span data-ttu-id="18971-149">W przypadku danych bez schematu sklepów takich jak bazy danych Azure rozwiązania Cosmos usługi fabryka danych z wnioskuje schemat w jednym z następujących sposobów:</span><span class="sxs-lookup"><span data-stu-id="18971-149">For schema-free data stores such as Azure Cosmos DB, the Data Factory service infers the schema in one of the following ways:</span></span>  

1. <span data-ttu-id="18971-150">Jeśli określisz struktury danych za pomocą **struktury** tej struktury Schema honoruje właściwości w definicji zestawu danych, usługi fabryka danych.</span><span class="sxs-lookup"><span data-stu-id="18971-150">If you specify the structure of data by using the **structure** property in the dataset definition, the Data Factory service honors this structure as the schema.</span></span> <span data-ttu-id="18971-151">W takim przypadku wiersza nie zawiera wartości dla kolumny, będzie należy podać dla niego wartość null.</span><span class="sxs-lookup"><span data-stu-id="18971-151">In this case, if a row does not contain a value for a column, a null value will be provided for it.</span></span>
2. <span data-ttu-id="18971-152">Jeśli nie określisz struktury danych za pomocą **struktury** właściwości w definicji zestawu danych, usługi fabryka danych z wnioskuje schemat za pomocą pierwszego wiersza w danych.</span><span class="sxs-lookup"><span data-stu-id="18971-152">If you do not specify the structure of data by using the **structure** property in the dataset definition, the Data Factory service infers the schema by using the first row in the data.</span></span> <span data-ttu-id="18971-153">W takim przypadku jeśli pierwszy wiersz zawiera pełną schematu, niektóre kolumny będą niedostępne w wyniku operacji kopiowania.</span><span class="sxs-lookup"><span data-stu-id="18971-153">In this case, if the first row does not contain the full schema, some columns will be missing in the result of copy operation.</span></span>

<span data-ttu-id="18971-154">W związku z tym dla źródeł danych bez schematu, najlepszym rozwiązaniem jest zdefiniowanie struktury danych przy użyciu **struktury** właściwości.</span><span class="sxs-lookup"><span data-stu-id="18971-154">Therefore, for schema-free data sources, the best practice is to specify the structure of data using the **structure** property.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="18971-155">Właściwości działania kopiowania</span><span class="sxs-lookup"><span data-stu-id="18971-155">Copy activity properties</span></span>
<span data-ttu-id="18971-156">Pełną listę właściwości dostępne do definiowania działań & sekcje zapoznaj się [tworzenie potoków](data-factory-create-pipelines.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="18971-156">For a full list of sections & properties available for defining activities please refer to the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="18971-157">Właściwości, takie jak nazwa, opis, dane wejściowe i wyjściowe tabel i zasady są dostępne dla wszystkich typów działań.</span><span class="sxs-lookup"><span data-stu-id="18971-157">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

> [!NOTE]
> <span data-ttu-id="18971-158">Działanie kopiowania przyjmuje tylko jeden parametr wejściowy i tworzy tylko jedno wyjście.</span><span class="sxs-lookup"><span data-stu-id="18971-158">The Copy Activity takes only one input and produces only one output.</span></span>

<span data-ttu-id="18971-159">Właściwości, które są dostępne w sekcji typeProperties działania z drugiej strony zależą od każdy typ działania, a w przypadku działania kopiowania się różnić w zależności od typów źródeł i sink.</span><span class="sxs-lookup"><span data-stu-id="18971-159">Properties available in the typeProperties section of the activity on the other hand vary with each activity type and in case of Copy activity they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="18971-160">W przypadku działania kopiowania, gdy źródłem jest typu **DocumentDbCollectionSource** następujące właściwości są dostępne w **typeProperties** sekcji:</span><span class="sxs-lookup"><span data-stu-id="18971-160">In case of Copy activity when source is of type **DocumentDbCollectionSource** the following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="18971-161">**Właściwość**</span><span class="sxs-lookup"><span data-stu-id="18971-161">**Property**</span></span> | <span data-ttu-id="18971-162">**Opis**</span><span class="sxs-lookup"><span data-stu-id="18971-162">**Description**</span></span> | <span data-ttu-id="18971-163">**Dozwolone wartości**</span><span class="sxs-lookup"><span data-stu-id="18971-163">**Allowed values**</span></span> | <span data-ttu-id="18971-164">**Wymagane**</span><span class="sxs-lookup"><span data-stu-id="18971-164">**Required**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="18971-165">query</span><span class="sxs-lookup"><span data-stu-id="18971-165">query</span></span> |<span data-ttu-id="18971-166">Określ zapytanie można odczytać danych.</span><span class="sxs-lookup"><span data-stu-id="18971-166">Specify the query to read data.</span></span> |<span data-ttu-id="18971-167">Wyślij zapytanie do ciągu obsługuje bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="18971-167">Query string supported by Azure Cosmos DB.</span></span> <br/><br/><span data-ttu-id="18971-168">Przykład:`SELECT c.BusinessEntityID, c.PersonType, c.NameStyle, c.Title, c.Name.First AS FirstName, c.Name.Last AS LastName, c.Suffix, c.EmailPromotion FROM c WHERE c.ModifiedDate > \"2009-01-01T00:00:00\"`</span><span class="sxs-lookup"><span data-stu-id="18971-168">Example: `SELECT c.BusinessEntityID, c.PersonType, c.NameStyle, c.Title, c.Name.First AS FirstName, c.Name.Last AS LastName, c.Suffix, c.EmailPromotion FROM c WHERE c.ModifiedDate > \"2009-01-01T00:00:00\"`</span></span> |<span data-ttu-id="18971-169">Nie</span><span class="sxs-lookup"><span data-stu-id="18971-169">No</span></span> <br/><br/><span data-ttu-id="18971-170">Jeśli nie zostanie określony, która zostanie wykonana instrukcja SQL:`select <columns defined in structure> from mycollection`</span><span class="sxs-lookup"><span data-stu-id="18971-170">If not specified, the SQL statement that is executed: `select <columns defined in structure> from mycollection`</span></span> |
| <span data-ttu-id="18971-171">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="18971-171">nestingSeparator</span></span> |<span data-ttu-id="18971-172">Znaki specjalne w celu wskazania, że dokument jest zagnieżdżony</span><span class="sxs-lookup"><span data-stu-id="18971-172">Special character to indicate that the document is nested</span></span> |<span data-ttu-id="18971-173">Dowolny znak.</span><span class="sxs-lookup"><span data-stu-id="18971-173">Any character.</span></span> <br/><br/><span data-ttu-id="18971-174">Azure DB rozwiązania Cosmos jest magazynem NoSQL dla dokumentów JSON, których struktury zagnieżdżone są dozwolone.</span><span class="sxs-lookup"><span data-stu-id="18971-174">Azure Cosmos DB is a NoSQL store for JSON documents, where nested structures are allowed.</span></span> <span data-ttu-id="18971-175">Fabryka danych Azure umożliwia użytkownikowi oznaczenia hierarchii za pomocą nestingSeparator, czyli "."</span><span class="sxs-lookup"><span data-stu-id="18971-175">Azure Data Factory enables user to denote hierarchy via nestingSeparator, which is “.”</span></span> <span data-ttu-id="18971-176">w powyższych przykładach.</span><span class="sxs-lookup"><span data-stu-id="18971-176">in the above examples.</span></span> <span data-ttu-id="18971-177">Z separatorem, działanie kopiowania spowoduje wygenerowanie obiektu "Name" o trzy elementy podrzędne elementy najpierw drugie imię i nazwisko, zgodnie z "Name.First", "Name.Middle" i "Name.Last" w definicji tabeli.</span><span class="sxs-lookup"><span data-stu-id="18971-177">With the separator, the copy activity will generate the “Name” object with three children elements First, Middle and Last, according to “Name.First”, “Name.Middle” and “Name.Last” in the table definition.</span></span> |<span data-ttu-id="18971-178">Nie</span><span class="sxs-lookup"><span data-stu-id="18971-178">No</span></span> |

<span data-ttu-id="18971-179">**DocumentDbCollectionSink** obsługuje następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="18971-179">**DocumentDbCollectionSink** supports the following properties:</span></span>

| <span data-ttu-id="18971-180">**Właściwość**</span><span class="sxs-lookup"><span data-stu-id="18971-180">**Property**</span></span> | <span data-ttu-id="18971-181">**Opis**</span><span class="sxs-lookup"><span data-stu-id="18971-181">**Description**</span></span> | <span data-ttu-id="18971-182">**Dozwolone wartości**</span><span class="sxs-lookup"><span data-stu-id="18971-182">**Allowed values**</span></span> | <span data-ttu-id="18971-183">**Wymagane**</span><span class="sxs-lookup"><span data-stu-id="18971-183">**Required**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="18971-184">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="18971-184">nestingSeparator</span></span> |<span data-ttu-id="18971-185">Wymagany jest znak specjalny w nazwa kolumny źródłowej, aby wskazać zagnieżdżonych dokumentu.</span><span class="sxs-lookup"><span data-stu-id="18971-185">A special character in the source column name to indicate that nested document is needed.</span></span> <br/><br/><span data-ttu-id="18971-186">Na przykład powyżej: `Name.First` w danych wyjściowych tabeli tworzy następującą strukturę JSON w dokumencie rozwiązania Cosmos bazy danych:</span><span class="sxs-lookup"><span data-stu-id="18971-186">For example above: `Name.First` in the output table produces the following JSON structure in the Cosmos DB document:</span></span><br/><br/><span data-ttu-id="18971-187">"Nazwa": {</span><span class="sxs-lookup"><span data-stu-id="18971-187">"Name": {</span></span><br/>    <span data-ttu-id="18971-188">"Pierwszy": "Jan"</span><span class="sxs-lookup"><span data-stu-id="18971-188">"First": "John"</span></span><br/><span data-ttu-id="18971-189">},</span><span class="sxs-lookup"><span data-stu-id="18971-189">},</span></span> |<span data-ttu-id="18971-190">Znak używany do rozdzielania poziomów zagnieżdżenia.</span><span class="sxs-lookup"><span data-stu-id="18971-190">Character that is used to separate nesting levels.</span></span><br/><br/><span data-ttu-id="18971-191">Wartość domyślna to `.` (kropką).</span><span class="sxs-lookup"><span data-stu-id="18971-191">Default value is `.` (dot).</span></span> |<span data-ttu-id="18971-192">Znak używany do rozdzielania poziomów zagnieżdżenia.</span><span class="sxs-lookup"><span data-stu-id="18971-192">Character that is used to separate nesting levels.</span></span> <br/><br/><span data-ttu-id="18971-193">Wartość domyślna to `.` (kropką).</span><span class="sxs-lookup"><span data-stu-id="18971-193">Default value is `.` (dot).</span></span> |
| <span data-ttu-id="18971-194">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="18971-194">writeBatchSize</span></span> |<span data-ttu-id="18971-195">Liczba równoległych żądań do usługi Azure DB rozwiązania Cosmos w celu utworzenia dokumentów.</span><span class="sxs-lookup"><span data-stu-id="18971-195">Number of parallel requests to Azure Cosmos DB service to create documents.</span></span><br/><br/><span data-ttu-id="18971-196">Aby precyzyjnie zdefiniować wydajność podczas kopiowania danych z bazy danych usługi rozwiązania Cosmos przy użyciu tej właściwości.</span><span class="sxs-lookup"><span data-stu-id="18971-196">You can fine-tune the performance when copying data to/from Cosmos DB by using this property.</span></span> <span data-ttu-id="18971-197">Wraz ze zwiększeniem writeBatchSize, ponieważ więcej żądań równoległych do rozwiązania Cosmos bazy danych są wysyłane, może spodziewać się lepszą wydajność.</span><span class="sxs-lookup"><span data-stu-id="18971-197">You can expect a better performance when you increase writeBatchSize because more parallel requests to Cosmos DB are sent.</span></span> <span data-ttu-id="18971-198">Jednak należy unikać ograniczania przepustowości, który może zgłaszać komunikat o błędzie: "jest duża szybkość żądania".</span><span class="sxs-lookup"><span data-stu-id="18971-198">However you’ll need to avoid throttling that can throw the error message: "Request rate is large".</span></span><br/><br/><span data-ttu-id="18971-199">Ograniczanie zadecyduje o wiele czynników, w tym rozmiar dokumentów, liczbę dokumentów, indeksowania zasady kolekcji docelowej, itd. Dla operacji kopiowania umożliwiają lepsze kolekcji (np. S3) ma największą przepływność dostępne (2500 żądań jednostek na sekundę).</span><span class="sxs-lookup"><span data-stu-id="18971-199">Throttling is decided by a number of factors, including size of documents, number of terms in documents, indexing policy of target collection, etc. For copy operations, you can use a better collection (e.g. S3) to have the most throughput available (2,500 request units/second).</span></span> |<span data-ttu-id="18971-200">Liczba całkowita</span><span class="sxs-lookup"><span data-stu-id="18971-200">Integer</span></span> |<span data-ttu-id="18971-201">Nie (domyślne: 5)</span><span class="sxs-lookup"><span data-stu-id="18971-201">No (default: 5)</span></span> |
| <span data-ttu-id="18971-202">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="18971-202">writeBatchTimeout</span></span> |<span data-ttu-id="18971-203">Poczekaj na ukończenie upłynie limit czasu operacji.</span><span class="sxs-lookup"><span data-stu-id="18971-203">Wait time for the operation to complete before it times out.</span></span> |<span data-ttu-id="18971-204">Zakres czasu</span><span class="sxs-lookup"><span data-stu-id="18971-204">timespan</span></span><br/><br/> <span data-ttu-id="18971-205">Przykład: "00: 30:00" (30 minut).</span><span class="sxs-lookup"><span data-stu-id="18971-205">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="18971-206">Nie</span><span class="sxs-lookup"><span data-stu-id="18971-206">No</span></span> |

## <a name="importexport-json-documents"></a><span data-ttu-id="18971-207">Dokumentów JSON Import/Eksport</span><span class="sxs-lookup"><span data-stu-id="18971-207">Import/Export JSON documents</span></span>
<span data-ttu-id="18971-208">Korzystając z tego łącznika DB rozwiązania Cosmos, można łatwo</span><span class="sxs-lookup"><span data-stu-id="18971-208">Using this Cosmos DB connector, you can easily</span></span>

* <span data-ttu-id="18971-209">Zaimportuj dokumentów JSON z różnych źródeł do rozwiązania Cosmos bazy danych, w tym obiektów Blob platformy Azure, usługa Azure Data Lake, lokalnego systemu plików lub innych magazynów opartych na plikach obsługiwane przez usługi fabryka danych Azure.</span><span class="sxs-lookup"><span data-stu-id="18971-209">Import JSON documents from various sources into Cosmos DB, including Azure Blob, Azure Data Lake, on-premises File System or other file-based stores supported by Azure Data Factory.</span></span>
* <span data-ttu-id="18971-210">Wyeksportuj dokumentów JSON z collecton rozwiązania Cosmos bazy danych do różnych magazynów opartych na plikach.</span><span class="sxs-lookup"><span data-stu-id="18971-210">Export JSON documents from Cosmos DB collecton into various file-based stores.</span></span>
* <span data-ttu-id="18971-211">Migrowanie danych między dwoma kolekcje DB rozwiązania Cosmos w postaci — jest.</span><span class="sxs-lookup"><span data-stu-id="18971-211">Migrate data between two Cosmos DB collections as-is.</span></span>

<span data-ttu-id="18971-212">Do osiągnięcia tych kopii niezależny od schematu</span><span class="sxs-lookup"><span data-stu-id="18971-212">To achieve such schema-agnostic copy,</span></span> 
* <span data-ttu-id="18971-213">Korzystając z Kreatora kopiowania, sprawdź **"wyeksportować w postaci-ma pliki w formacie JSON lub rozwiązania Cosmos bazy danych kolekcji"** opcji.</span><span class="sxs-lookup"><span data-stu-id="18971-213">When using copy wizard, check the **"Export as-is to JSON files or Cosmos DB collection"** option.</span></span>
* <span data-ttu-id="18971-214">Gdy edycję JSON, nie należy określać w sekcji "structure" w opublikowanych DB rozwiązania Cosmos ani właściwości "nestingSeparator" dla bazy danych rozwiązania Cosmos źródło/ujście w przypadku działania kopiowania.</span><span class="sxs-lookup"><span data-stu-id="18971-214">When using JSON editing, do not specify the "structure" section in Cosmos DB dataset(s) nor "nestingSeparator" property on Cosmos DB source/sink in copy activity.</span></span> <span data-ttu-id="18971-215">Importuj z / Eksportuj do pliki w formacie JSON, w zestawie plików magazynu danych należy określić typ formatu jako "JsonFormat", "filePattern" config i Pomiń pozostałe ustawienia formatu, zobacz [formatu JSON](data-factory-supported-file-and-compression-formats.md#json-format) sekcji Szczegóły.</span><span class="sxs-lookup"><span data-stu-id="18971-215">To import from/export to JSON files, in the file store dataset specify format type as "JsonFormat", config "filePattern" and skip the rest format settings, see [JSON format](data-factory-supported-file-and-compression-formats.md#json-format) section on details.</span></span>

## <a name="json-examples"></a><span data-ttu-id="18971-216">Przykłady JSON</span><span class="sxs-lookup"><span data-stu-id="18971-216">JSON examples</span></span>
<span data-ttu-id="18971-217">Poniższe przykłady zapewniają definicje JSON, których można utworzyć potok przy użyciu [portalu Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) lub [programu Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) lub [programu Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="18971-217">The following examples provide sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="18971-218">Przedstawiają sposób kopiowania danych do i z bazy danych Azure rozwiązania Cosmos i magazynu obiektów Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="18971-218">They show how to copy data to and from Azure Cosmos DB and Azure Blob Storage.</span></span> <span data-ttu-id="18971-219">Jednak dane mogą być kopiowane **bezpośrednio** z dowolnego źródła do dowolnego wychwytywanie podane [tutaj](data-factory-data-movement-activities.md#supported-data-stores-and-formats) za pomocą działania kopiowania w fabryce danych Azure.</span><span class="sxs-lookup"><span data-stu-id="18971-219">However, data can be copied **directly** from any of the sources to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>

## <a name="example-copy-data-from-azure-cosmos-db-to-azure-blob"></a><span data-ttu-id="18971-220">Przykład: Kopiowanie danych z bazy danych Azure rozwiązania Cosmos do obiektów Blob platformy Azure</span><span class="sxs-lookup"><span data-stu-id="18971-220">Example: Copy data from Azure Cosmos DB to Azure Blob</span></span>
<span data-ttu-id="18971-221">Poniższy przykład przedstawia:</span><span class="sxs-lookup"><span data-stu-id="18971-221">The sample below shows:</span></span>

1. <span data-ttu-id="18971-222">Połączonej usługi typu [DocumentDb](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="18971-222">A linked service of type [DocumentDb](#linked-service-properties).</span></span>
2. <span data-ttu-id="18971-223">Połączonej usługi typu [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="18971-223">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="18971-224">Dane wejściowe [dataset](data-factory-create-datasets.md) typu [DocumentDbCollection](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="18971-224">An input [dataset](data-factory-create-datasets.md) of type [DocumentDbCollection](#dataset-properties).</span></span>
4. <span data-ttu-id="18971-225">Dane wyjściowe [dataset](data-factory-create-datasets.md) typu [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="18971-225">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="18971-226">A [potoku](data-factory-create-pipelines.md) z działaniem kopii, która używa [DocumentDbCollectionSource](#copy-activity-properties) i [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="18971-226">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [DocumentDbCollectionSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="18971-227">Przykład kopiuje dane w usłudze Azure DB rozwiązania Cosmos do obiektów Blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="18971-227">The sample copies data in Azure Cosmos DB to Azure Blob.</span></span> <span data-ttu-id="18971-228">Właściwości JSON używane w te przykłady są opisane w sekcjach poniżej próbek.</span><span class="sxs-lookup"><span data-stu-id="18971-228">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="18971-229">**Azure DB rozwiązania Cosmos połączonej usługi:**</span><span class="sxs-lookup"><span data-stu-id="18971-229">**Azure Cosmos DB linked service:**</span></span>

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
<span data-ttu-id="18971-230">**Magazyn obiektów Blob Azure połączonej usługi:**</span><span class="sxs-lookup"><span data-stu-id="18971-230">**Azure Blob storage linked service:**</span></span>

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
<span data-ttu-id="18971-231">**Azure DB dokument wejściowy zestaw danych:**</span><span class="sxs-lookup"><span data-stu-id="18971-231">**Azure Document DB input dataset:**</span></span>

<span data-ttu-id="18971-232">Przykładzie przyjęto założenie, masz kolekcję o nazwie **osoby** w bazie danych bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="18971-232">The sample assumes you have a collection named **Person** in an Azure Cosmos DB database.</span></span>

<span data-ttu-id="18971-233">Ustawienie "external": "prawda", a następnie określając externalData informacje o zasadach usługi fabryka danych Azure czy tabeli zewnętrznej dla fabryki danych i nie są produkowane przez działanie w fabryce danych.</span><span class="sxs-lookup"><span data-stu-id="18971-233">Setting “external”: ”true” and specifying externalData policy information the Azure Data Factory service that the table is external to the data factory and not produced by an activity in the data factory.</span></span>

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

<span data-ttu-id="18971-234">**Azure Blob wyjściowy zestaw danych:**</span><span class="sxs-lookup"><span data-stu-id="18971-234">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="18971-235">Dane zostaną skopiowane do nowego obiektu blob co godzinę o ścieżce dla obiektu blob odzwierciedlające określonej daty/godziny z szczegółowości godzinę.</span><span class="sxs-lookup"><span data-stu-id="18971-235">Data is copied to a new blob every hour with the path for the blob reflecting the specific datetime with hour granularity.</span></span>

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
<span data-ttu-id="18971-236">Przykładowy dokument JSON w kolekcji osoby w bazie danych DB rozwiązania Cosmos:</span><span class="sxs-lookup"><span data-stu-id="18971-236">Sample JSON document in the Person collection in a Cosmos DB database:</span></span>

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
<span data-ttu-id="18971-237">Rozwiązania cosmos bazy danych obsługuje tworzenie zapytań dla dokumentów przy użyciu składni SQL przez hierarchiczna dokumentów JSON.</span><span class="sxs-lookup"><span data-stu-id="18971-237">Cosmos DB supports querying documents using a SQL like syntax over hierarchical JSON documents.</span></span>

<span data-ttu-id="18971-238">Przykład:</span><span class="sxs-lookup"><span data-stu-id="18971-238">Example:</span></span> 

```sql
SELECT Person.PersonId, Person.Name.First AS FirstName, Person.Name.Middle as MiddleName, Person.Name.Last AS LastName FROM Person
```

<span data-ttu-id="18971-239">Następujące potoku kopiuje dane z kolekcji osoby w bazie danych bazy danych Azure rozwiązania Cosmos obiektów blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="18971-239">The following pipeline copies data from the Person collection in the Azure Cosmos DB database to an Azure blob.</span></span> <span data-ttu-id="18971-240">W ramach działania kopiowania danych wejściowych i wyjściowych zestawów danych zostały określone.</span><span class="sxs-lookup"><span data-stu-id="18971-240">As part of the copy activity the input and output datasets have been specified.</span></span>  

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
## <a name="example-copy-data-from-azure-blob-to-azure-cosmos-db"></a><span data-ttu-id="18971-241">Przykład: Kopiowanie danych z obiektu Blob Azure do bazy danych Azure rozwiązania Cosmos</span><span class="sxs-lookup"><span data-stu-id="18971-241">Example: Copy data from Azure Blob to Azure Cosmos DB</span></span> 
<span data-ttu-id="18971-242">Poniższy przykład przedstawia:</span><span class="sxs-lookup"><span data-stu-id="18971-242">The sample below shows:</span></span>

1. <span data-ttu-id="18971-243">Połączonej usługi typu [DocumentDb](#azure-documentdb-linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="18971-243">A linked service of type [DocumentDb](#azure-documentdb-linked-service-properties).</span></span>
2. <span data-ttu-id="18971-244">Połączonej usługi typu [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="18971-244">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="18971-245">Dane wejściowe [dataset](data-factory-create-datasets.md) typu [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="18971-245">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="18971-246">Dane wyjściowe [dataset](data-factory-create-datasets.md) typu [DocumentDbCollection](#azure-documentdb-dataset-type-properties).</span><span class="sxs-lookup"><span data-stu-id="18971-246">An output [dataset](data-factory-create-datasets.md) of type [DocumentDbCollection](#azure-documentdb-dataset-type-properties).</span></span>
5. <span data-ttu-id="18971-247">A [potoku](data-factory-create-pipelines.md) z działaniem kopii, która używa [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) i [DocumentDbCollectionSink](#azure-documentdb-copy-activity-type-properties).</span><span class="sxs-lookup"><span data-stu-id="18971-247">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [DocumentDbCollectionSink](#azure-documentdb-copy-activity-type-properties).</span></span>

<span data-ttu-id="18971-248">Przykład kopiuje dane z usługi Azure blob do bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="18971-248">The sample copies data from Azure blob to Azure Cosmos DB.</span></span> <span data-ttu-id="18971-249">Właściwości JSON używane w te przykłady są opisane w sekcjach poniżej próbek.</span><span class="sxs-lookup"><span data-stu-id="18971-249">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="18971-250">**Magazyn obiektów Blob Azure połączonej usługi:**</span><span class="sxs-lookup"><span data-stu-id="18971-250">**Azure Blob storage linked service:**</span></span>

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
<span data-ttu-id="18971-251">**Azure DB rozwiązania Cosmos połączonej usługi:**</span><span class="sxs-lookup"><span data-stu-id="18971-251">**Azure Cosmos DB linked service:**</span></span>

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
<span data-ttu-id="18971-252">**Azure wejściowego zestawu danych obiektów Blob:**</span><span class="sxs-lookup"><span data-stu-id="18971-252">**Azure Blob input dataset:**</span></span>

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
<span data-ttu-id="18971-253">**Azure DB rozwiązania Cosmos wyjściowy zestaw danych:**</span><span class="sxs-lookup"><span data-stu-id="18971-253">**Azure Cosmos DB output dataset:**</span></span>

<span data-ttu-id="18971-254">Przykład kopiuje dane na kolekcję o nazwie "Osoba".</span><span class="sxs-lookup"><span data-stu-id="18971-254">The sample copies data to a collection named “Person”.</span></span>

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
<span data-ttu-id="18971-255">Następujące potoku kopiuje dane z obiektów Blob platformy Azure do kolekcji osoby w bazie danych rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="18971-255">The following pipeline copies data from Azure Blob to the Person collection in the Cosmos DB.</span></span> <span data-ttu-id="18971-256">W ramach działania kopiowania danych wejściowych i wyjściowych zestawów danych zostały określone.</span><span class="sxs-lookup"><span data-stu-id="18971-256">As part of the copy activity the input and output datasets have been specified.</span></span>

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
              "ColumnMappings": "FirstName: Name.First, MiddleName: Name.Middle, LastName: Name.Last, BusinessEntityID: BusinessEntityID, PersonType: PersonType, NameStyle: NameStyle, Title: Title, Suffix: Suffix, EmailPromotion: EmailPromotion, rowguid: rowguid, ModifiedDate: ModifiedDate"
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
<span data-ttu-id="18971-257">Jeśli przykładowe dane wejściowe obiektu blob jako</span><span class="sxs-lookup"><span data-stu-id="18971-257">If the sample blob input is as</span></span>

```
1,John,,Doe
```
<span data-ttu-id="18971-258">Następnie dane wyjściowe JSON do rozwiązania Cosmos bazy danych będą się jako:</span><span class="sxs-lookup"><span data-stu-id="18971-258">Then the output JSON in Cosmos DB will be as:</span></span>

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
<span data-ttu-id="18971-259">Azure DB rozwiązania Cosmos jest magazynem NoSQL dla dokumentów JSON, których struktury zagnieżdżone są dozwolone.</span><span class="sxs-lookup"><span data-stu-id="18971-259">Azure Cosmos DB is a NoSQL store for JSON documents, where nested structures are allowed.</span></span> <span data-ttu-id="18971-260">Fabryka danych Azure umożliwia użytkownikowi oznaczenia hierarchii za pomocą **nestingSeparator**, czyli "."</span><span class="sxs-lookup"><span data-stu-id="18971-260">Azure Data Factory enables user to denote hierarchy via **nestingSeparator**, which is “.”</span></span> <span data-ttu-id="18971-261">w tym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="18971-261">in this example.</span></span> <span data-ttu-id="18971-262">Z separatorem, działanie kopiowania spowoduje wygenerowanie obiektu "Name" o trzy elementy podrzędne elementy najpierw drugie imię i nazwisko, zgodnie z "Name.First", "Name.Middle" i "Name.Last" w definicji tabeli.</span><span class="sxs-lookup"><span data-stu-id="18971-262">With the separator, the copy activity will generate the “Name” object with three children elements First, Middle and Last, according to “Name.First”, “Name.Middle” and “Name.Last” in the table definition.</span></span>

## <a name="appendix"></a><span data-ttu-id="18971-263">Dodatek</span><span class="sxs-lookup"><span data-stu-id="18971-263">Appendix</span></span>
1. <span data-ttu-id="18971-264">**Pytanie:** jest aktualizacja obsługi działanie kopiowania istniejące rekordy?</span><span class="sxs-lookup"><span data-stu-id="18971-264">**Question:** Does the Copy Activity support update of existing records?</span></span>

    <span data-ttu-id="18971-265">**Odpowiedź:** nie.</span><span class="sxs-lookup"><span data-stu-id="18971-265">**Answer:** No.</span></span>
2. <span data-ttu-id="18971-266">**Pytanie:** jak ponowienie kopię bazy danych Azure rozwiązania Cosmos przeciwdziałania już skopiowane rekordy?</span><span class="sxs-lookup"><span data-stu-id="18971-266">**Question:** How does a retry of a copy to Azure Cosmos DB deal with already copied records?</span></span>

    <span data-ttu-id="18971-267">**Odpowiedź:** rekordów zawiera pola "ID", próbuje operacji kopiowania do wstawienia rekordu o tym samym identyfikatorze operacji kopiowania zgłasza błąd.</span><span class="sxs-lookup"><span data-stu-id="18971-267">**Answer:** If records have an "ID" field and the copy operation tries to insert a record with the same ID, the copy operation throws an error.</span></span>  
3. <span data-ttu-id="18971-268">**Pytanie:** fabryki danych obsługuje [zakres lub partycjonowanie danych opartych na skrót](../documentdb/documentdb-partition-data.md)?</span><span class="sxs-lookup"><span data-stu-id="18971-268">**Question:** Does Data Factory support [range or hash-based data partitioning](../documentdb/documentdb-partition-data.md)?</span></span>

    <span data-ttu-id="18971-269">**Odpowiedź:** nie.</span><span class="sxs-lookup"><span data-stu-id="18971-269">**Answer:** No.</span></span>
4. <span data-ttu-id="18971-270">**Pytanie:** można określić więcej niż jednej bazy danych Azure rozwiązania Cosmos kolekcji dla tabeli?</span><span class="sxs-lookup"><span data-stu-id="18971-270">**Question:** Can I specify more than one Azure Cosmos DB collection for a table?</span></span>

    <span data-ttu-id="18971-271">**Odpowiedź:** nie.</span><span class="sxs-lookup"><span data-stu-id="18971-271">**Answer:** No.</span></span> <span data-ttu-id="18971-272">W tym momencie można określić tylko jedną kolekcję.</span><span class="sxs-lookup"><span data-stu-id="18971-272">Only one collection can be specified at this time.</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="18971-273">Wydajność i dostrajania</span><span class="sxs-lookup"><span data-stu-id="18971-273">Performance and Tuning</span></span>
<span data-ttu-id="18971-274">Zobacz [wydajności działania kopiowania & dostrajanie przewodnik](data-factory-copy-activity-performance.md) Aby dowiedzieć się więcej o kluczowych czynników tego wydajność wpływ przenoszenia danych (działanie kopiowania) w usłudze fabryka danych Azure i zoptymalizować ją na różne sposoby.</span><span class="sxs-lookup"><span data-stu-id="18971-274">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
