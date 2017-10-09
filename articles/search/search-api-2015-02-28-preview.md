---
title: "aaaAzure 2015 wersja interfejsu API REST usługi wyszukiwania-02-28-Preview | Dokumentacja firmy Microsoft"
description: "Azure Search usługi REST interfejsu API w wersji 2015-02-28-Preview obejmuje eksperymentalne funkcje, takie jak analizatorów języka naturalnego i moreLikeThis wyszukiwania."
services: search
documentationcenter: na
author: brjohnstmsft
manager: pablocas
editor: 
ms.assetid: 3dba3bf8-9c83-42f6-82bc-04727bd11037
ms.service: search
ms.devlang: rest-api
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: search
ms.date: 05/01/2017
ms.author: brjohnst
ms.openlocfilehash: 63cb30b7f43a42552c6744ea087afea947857224
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-search-service-rest-api-version-2015-02-28-preview"></a><span data-ttu-id="633c8-103">Interfejs API REST usługi wyszukiwanie Azure: Wersja 2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="633c8-103">Azure Search Service REST API: Version 2015-02-28-Preview</span></span>
<span data-ttu-id="633c8-104">W tym artykule jest hello dokumentacji dla `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="633c8-104">This article is hello reference documentation for `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="633c8-105">Ta wersja zapoznawcza rozszerza hello bieżącej wersji ogólnie dostępna, [interfejsu api-version = 2015-02-28](https://msdn.microsoft.com/library/dn798935.aspx), podając następujące eksperymentalną hello:</span><span class="sxs-lookup"><span data-stu-id="633c8-105">This preview extends hello current generally available version, [api-version=2015-02-28](https://msdn.microsoft.com/library/dn798935.aspx), by providing hello following experimental features:</span></span>

* <span data-ttu-id="633c8-106">`moreLikeThis`parametr w hello zapytania [dokumenty wyszukiwania](#SearchDocs) interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="633c8-106">`moreLikeThis` query parameter in hello [Search Documents](#SearchDocs) API.</span></span> <span data-ttu-id="633c8-107">Znajdzie inne dokumenty, które są odpowiednie tooanother określonego dokumentu.</span><span class="sxs-lookup"><span data-stu-id="633c8-107">It finds other documents that are relevant tooanother specific document.</span></span>

<span data-ttu-id="633c8-108">Kilka dodatkowych części hello `2015-02-28-Preview` interfejsu API REST są udokumentowane oddzielnie.</span><span class="sxs-lookup"><span data-stu-id="633c8-108">A few additional parts of hello `2015-02-28-Preview` REST API are documented separately.</span></span> <span data-ttu-id="633c8-109">Należą do nich:</span><span class="sxs-lookup"><span data-stu-id="633c8-109">These include:</span></span>

* [<span data-ttu-id="633c8-110">Profile oceniania</span><span class="sxs-lookup"><span data-stu-id="633c8-110">Scoring Profiles</span></span>](search-api-scoring-profiles-2015-02-28-preview.md)
* <span data-ttu-id="633c8-111">[Indexers](search-api-indexers-2015-02-28-preview.md) (Indeksatory)</span><span class="sxs-lookup"><span data-stu-id="633c8-111">[Indexers](search-api-indexers-2015-02-28-preview.md)</span></span>

<span data-ttu-id="633c8-112">Usługa Azure Search jest dostępna w różnych wersjach.</span><span class="sxs-lookup"><span data-stu-id="633c8-112">Azure Search service is available in multiple versions.</span></span> <span data-ttu-id="633c8-113">Zobacz zbyt[przechowywanie wersji usługi wyszukiwania](http://msdn.microsoft.com/library/azure/dn864560.aspx) szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="633c8-113">Please refer too[Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details.</span></span>

## <a name="apis-in-this-document"></a><span data-ttu-id="633c8-114">Interfejsy API w tym dokumencie</span><span class="sxs-lookup"><span data-stu-id="633c8-114">APIs in this document</span></span>
<span data-ttu-id="633c8-115">Interfejs API usługi Azure Search obsługuje dwa składni adresu URL dla operacji interfejsu API: proste i OData (zobacz [obsługę OData (interfejsu API usługi Azure Search)](http://msdn.microsoft.com/library/azure/dn798932.aspx) szczegółowe informacje).</span><span class="sxs-lookup"><span data-stu-id="633c8-115">Azure Search service API supports two URL syntaxes for API operations: simple and OData (see [Support for OData (Azure Search API)](http://msdn.microsoft.com/library/azure/dn798932.aspx) for details).</span></span> <span data-ttu-id="633c8-116">Witaj poniższej liście przedstawiono składnię prostego powitania.</span><span class="sxs-lookup"><span data-stu-id="633c8-116">hello following list shows hello simple syntax.</span></span>

[<span data-ttu-id="633c8-117">Tworzenie indeksu</span><span class="sxs-lookup"><span data-stu-id="633c8-117">Create Index</span></span>](#CreateIndex)

    POST /indexes?api-version=2015-02-28-Preview

[<span data-ttu-id="633c8-118">Aktualizuj indeks</span><span class="sxs-lookup"><span data-stu-id="633c8-118">Update Index</span></span>](#UpdateIndex)

    PUT /indexes/[index name]?api-version=2015-02-28-Preview

[<span data-ttu-id="633c8-119">Pobierz indeksu</span><span class="sxs-lookup"><span data-stu-id="633c8-119">Get Index</span></span>](#GetIndex)

    GET /indexes/[index name]?api-version=2015-02-28-Preview

[<span data-ttu-id="633c8-120">Wyświetlanie listy indeksów</span><span class="sxs-lookup"><span data-stu-id="633c8-120">Listing Indexes</span></span>](#ListIndexes)

    GET /indexes?api-version=2015-02-28-Preview

[<span data-ttu-id="633c8-121">Uzyskać statystyki indeksu</span><span class="sxs-lookup"><span data-stu-id="633c8-121">Get Index Statistics</span></span>](#GetIndexStats)

    GET /indexes/[index name]/stats?api-version=2015-02-28-Preview

[<span data-ttu-id="633c8-122">Analizator testów</span><span class="sxs-lookup"><span data-stu-id="633c8-122">Test Analyzer</span></span>](#TestAnalyzer)

    POST /indexes/[index name]/analyze?api-version=2015-02-28-Preview

[<span data-ttu-id="633c8-123">Usuwanie indeksu</span><span class="sxs-lookup"><span data-stu-id="633c8-123">Delete an Index</span></span>](#DeleteIndex)

    DELETE /indexes/[index name]?api-version=2015-02-28-Preview

[<span data-ttu-id="633c8-124">Dodawanie, usuwanie i aktualizowanie danych w indeksie</span><span class="sxs-lookup"><span data-stu-id="633c8-124">Add, Delete, and Update Data within an Index</span></span>](#AddOrUpdateDocuments)

    POST /indexes/[index name]/docs/index?api-version=2015-02-28-Preview

[<span data-ttu-id="633c8-125">Przeszukaj dokumenty</span><span class="sxs-lookup"><span data-stu-id="633c8-125">Search Documents</span></span>](#SearchDocs)

    GET /indexes/[index name]/docs?[query parameters]
    POST /indexes/[index name]/docs/search?api-version=2015-02-28-Preview

[<span data-ttu-id="633c8-126">Dokument wyszukiwania</span><span class="sxs-lookup"><span data-stu-id="633c8-126">Lookup Document</span></span>](#LookupAPI)

     GET /indexes/[index name]/docs/[key]?[query parameters]

[<span data-ttu-id="633c8-127">Liczba dokumentów</span><span class="sxs-lookup"><span data-stu-id="633c8-127">Count Documents</span></span>](#CountDocs)

    GET /indexes/[index name]/docs/$count?api-version=2015-02-28-Preview

[<span data-ttu-id="633c8-128">Sugestie</span><span class="sxs-lookup"><span data-stu-id="633c8-128">Suggestions</span></span>](#Suggestions)

    GET /indexes/[index name]/docs/suggest?[query parameters]
    POST /indexes/[index name]/docs/suggest?api-version=2015-02-28-Preview

- - -
<a name="IndexOps"></a>

## <a name="index-operations"></a><span data-ttu-id="633c8-129">Operacje na indeksie</span><span class="sxs-lookup"><span data-stu-id="633c8-129">Index Operations</span></span>
<span data-ttu-id="633c8-130">Można tworzyć i Zarządzaj indeksami w usłudze Azure Search za pomocą prostego żądania HTTP (POST, GET, PUT, DELETE) względem zasobów danego indeksu.</span><span class="sxs-lookup"><span data-stu-id="633c8-130">You can create and manage indexes in Azure Search service via simple HTTP requests (POST, GET, PUT, DELETE) against a given index resource.</span></span> <span data-ttu-id="633c8-131">toocreate jako indeks, najpierw po dokument JSON, który opisuje hello schematu indeksu.</span><span class="sxs-lookup"><span data-stu-id="633c8-131">toocreate an index, you first POST a JSON document that describes hello index schema.</span></span> <span data-ttu-id="633c8-132">Schemat Hello definiuje pola hello hello indeksu, ich typy danych i jak mogą być używane (na przykład w wyszukiwania pełnotekstowego, filtry, sortowania i tworzenie aspektów).</span><span class="sxs-lookup"><span data-stu-id="633c8-132">hello schema defines hello fields of hello index, their data types, and how they can be used (for example, in full-text searches, filters, sorting, or faceting).</span></span> <span data-ttu-id="633c8-133">Definiuje również oceniania profile, sugestorów i inne atrybuty tooconfigure hello zachowanie hello indeksu.</span><span class="sxs-lookup"><span data-stu-id="633c8-133">It also defines scoring profiles, suggesters and other attributes tooconfigure hello behavior of hello index.</span></span>

<span data-ttu-id="633c8-134">Witaj poniższym przykładzie przedstawiono ilustrację Schemat używany do wyszukiwania w hotelach informacji z pola Opis hello zdefiniowane w dwóch języków.</span><span class="sxs-lookup"><span data-stu-id="633c8-134">hello following example provides an illustration of a schema used for searching on hotel information with hello Description field defined in two languages.</span></span> <span data-ttu-id="633c8-135">Zwróć uwagę, jak atrybuty kontrolować sposób używania pola hello.</span><span class="sxs-lookup"><span data-stu-id="633c8-135">Notice how attributes control how hello field is used.</span></span> <span data-ttu-id="633c8-136">Na przykład Witaj `hotelId` jest używany jako klucz dokumentu hello (`"key": true`) i jest on wykluczony z wyszukiwania pełnotekstowego (`"searchable": false`).</span><span class="sxs-lookup"><span data-stu-id="633c8-136">For example hello `hotelId` is used as hello document key (`"key": true`) and is excluded from full-text searches (`"searchable": false`).</span></span>

    {
    "name": "hotels",  
    "fields": [
      {"name": "hotelId", "type": "Edm.String", "key": true, "searchable": false},
      {"name": "baseRate", "type": "Edm.Double"},
      {"name": "description", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false},
      {"name": "description_fr", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false, "analyzer": "fr.lucene"},
      {"name": "hotelName", "type": "Edm.String"},
      {"name": "category", "type": "Edm.String"},
      {"name": "tags", "type": "Collection(Edm.String)"},
      {"name": "parkingIncluded", "type": "Edm.Boolean"},
      {"name": "smokingAllowed", "type": "Edm.Boolean"},
      {"name": "lastRenovationDate", "type": "Edm.DateTimeOffset"},
      {"name": "rating", "type": "Edm.Int32"},
      {"name": "location", "type": "Edm.GeographyPoint"}
     ],
     "suggesters": [
      {
       "name": "sg",
       "searchMode": "analyzingInfixMatching",
       "sourceFields": ["hotelName"]
      }
     ]
    }

<span data-ttu-id="633c8-137">Po utworzeniu indeksu hello będzie przekazywanie dokumentów, które wypełniania indeksu hello.</span><span class="sxs-lookup"><span data-stu-id="633c8-137">After hello index is created, you'll upload documents that populate hello index.</span></span> <span data-ttu-id="633c8-138">Zobacz [Dodaj lub dokumenty aktualizacji](#AddOrUpdateDocuments) tego następnego kroku.</span><span class="sxs-lookup"><span data-stu-id="633c8-138">See [Add or Update Documents](#AddOrUpdateDocuments) for this next step.</span></span>

<span data-ttu-id="633c8-139">Aby tooindexing wprowadzenie wideo w usłudze Azure Search, zobacz hello [Channel 9 chmury obejmują epizodu w usłudze Azure Search](http://go.microsoft.com/fwlink/p/?LinkId=511509).</span><span class="sxs-lookup"><span data-stu-id="633c8-139">For a video introduction tooindexing in Azure Search, see hello [Channel 9 Cloud Cover episode on Azure Search](http://go.microsoft.com/fwlink/p/?LinkId=511509).</span></span>

<a name="CreateIndex"></a>

## <a name="create-index"></a><span data-ttu-id="633c8-140">Tworzenie indeksu</span><span class="sxs-lookup"><span data-stu-id="633c8-140">Create Index</span></span>
<span data-ttu-id="633c8-141">Indeks jest hello podstawowy sposób organizowania i wyszukiwanie dokumentów w usłudze Azure Search, podobne toohow tabeli organizuje rekordów w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="633c8-141">An index is hello primary means of organizing and searching documents in Azure Search, similar toohow a table organizes records in a database.</span></span> <span data-ttu-id="633c8-142">Każdy indeks ma kolekcję dokumentów wszystkie zgodne toohello schematu indeksu (nazw pól, typy danych i właściwości), że indeksy także określić dodatkowych konstrukcje (sugestorów oceniania profile i opcje mechanizmu CORS) definiujące innych zachowań wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="633c8-142">Each index has a collection of documents that all conform toohello index schema (field names, data types, and properties), but indexes also specify additional constructs (suggesters, scoring profiles, and CORS options) that define other search behaviors.</span></span>

<span data-ttu-id="633c8-143">Można utworzyć nowego indeksu w ramach usługi Azure Search za pomocą żądania HTTP POST i PUT.</span><span class="sxs-lookup"><span data-stu-id="633c8-143">You can create a new index within an Azure Search service using an HTTP POST or PUT request.</span></span> <span data-ttu-id="633c8-144">Witaj treści żądania hello jest schemat JSON, który określa hello indeksu i informacje o konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="633c8-144">hello body of hello request is a JSON schema that specifies hello index and configuration information.</span></span>

    POST https://[service name].search.windows.net/indexes?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

<span data-ttu-id="633c8-145">Alternatywnie można użyć PUT i określ nazwę indeksu hello na powitania identyfikatora URI.</span><span class="sxs-lookup"><span data-stu-id="633c8-145">Alternatively, you can use PUT and specify hello index name on hello URI.</span></span> <span data-ttu-id="633c8-146">Witaj indeks nie istnieje, zostanie utworzona.</span><span class="sxs-lookup"><span data-stu-id="633c8-146">If hello index does not exist, it will be created.</span></span>

    PUT https://[search service url]/indexes/[index name]?api-version=[api-version]

<span data-ttu-id="633c8-147">Tworzenie indeksu określa hello struktury dokumentów hello przechowywane i używane w operacji wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="633c8-147">Creating an index determines hello structure of hello documents stored and used in search operations.</span></span> <span data-ttu-id="633c8-148">Wypełnianie indeksu hello jest osobnym operacji.</span><span class="sxs-lookup"><span data-stu-id="633c8-148">Populating hello index is a separate operation.</span></span> <span data-ttu-id="633c8-149">W tym kroku użyjesz [indeksatora](https://msdn.microsoft.com/library/azure/mt183328.aspx) (dostępne dla obsługiwanych źródeł danych) lub [Add, Update lub usuwanie dokumentów](https://msdn.microsoft.com/library/azure/dn798930.aspx) operacji.</span><span class="sxs-lookup"><span data-stu-id="633c8-149">For this step, you can use an [indexer](https://msdn.microsoft.com/library/azure/mt183328.aspx) (available for supported data sources) or an [Add, Update, or Delete Documents](https://msdn.microsoft.com/library/azure/dn798930.aspx) operation.</span></span> <span data-ttu-id="633c8-150">Indeks Hello odwrócony jest generowany, gdy ogłoszeniem hello dokumentów.</span><span class="sxs-lookup"><span data-stu-id="633c8-150">hello inverted index is generated when hello documents are posted.</span></span>

<span data-ttu-id="633c8-151">**Uwaga**: Maksymalna liczba indeksów dozwolone hello jest zależna od warstwy cenowej.</span><span class="sxs-lookup"><span data-stu-id="633c8-151">**Note**: hello maximum number of indexes allowed varies by pricing tier.</span></span> <span data-ttu-id="633c8-152">Usługa wolnego Hello umożliwia się too3 indeksów.</span><span class="sxs-lookup"><span data-stu-id="633c8-152">hello free service allows up too3 indexes.</span></span> <span data-ttu-id="633c8-153">Standardowa usługa umożliwia 50 indeksy na usługę wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="633c8-153">Standard service allows 50 indexes per Search service.</span></span> <span data-ttu-id="633c8-154">Zobacz [limity i ograniczenia](http://msdn.microsoft.com/library/azure/dn798934.aspx) szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="633c8-154">See [Limits and constraints](http://msdn.microsoft.com/library/azure/dn798934.aspx) for details.</span></span>

<span data-ttu-id="633c8-155">**Żądanie**</span><span class="sxs-lookup"><span data-stu-id="633c8-155">**Request**</span></span>

<span data-ttu-id="633c8-156">HTTPS jest wymagana dla wszystkich żądań obsługi.</span><span class="sxs-lookup"><span data-stu-id="633c8-156">HTTPS is required for all service requests.</span></span> <span data-ttu-id="633c8-157">Witaj **Create Index** żądania może być skonstruowany przy użyciu metody POST i PUT.</span><span class="sxs-lookup"><span data-stu-id="633c8-157">hello **Create Index** request can be constructed using either a POST or PUT method.</span></span> <span data-ttu-id="633c8-158">Korzystając z POST, należy podać nazwę indeksu w treści żądania hello wraz z definicji schematu indeksu hello.</span><span class="sxs-lookup"><span data-stu-id="633c8-158">When using POST, you must provide an index name in hello request body along with hello index schema definition.</span></span> <span data-ttu-id="633c8-159">Z PUT nazwę indeksu hello jest częścią hello adresu URL.</span><span class="sxs-lookup"><span data-stu-id="633c8-159">With PUT, hello index name is part of hello URL.</span></span> <span data-ttu-id="633c8-160">Jeśli indeks hello nie istnieje, jest tworzony.</span><span class="sxs-lookup"><span data-stu-id="633c8-160">If hello index doesn't exist, it is created.</span></span> <span data-ttu-id="633c8-161">Jeśli już istnieje, jest nowa definicja toohello zaktualizowane.</span><span class="sxs-lookup"><span data-stu-id="633c8-161">If it already exists, it is updated toohello new definition.</span></span>

<span data-ttu-id="633c8-162">Nazwa indeksu Hello musi zawierać małe litery, zaczynać się literą lub cyfrą nie ukośniki lub kropki i mniej niż 128 znaków.</span><span class="sxs-lookup"><span data-stu-id="633c8-162">hello index name must be lower case, start with a letter or number, have no slashes or dots, and be less than 128 characters.</span></span> <span data-ttu-id="633c8-163">Po uruchomieniu nazwę indeksu hello literą lub cyfrą hello reszty hello nazwa może zawierać żadnych list, numer i kreski, tak długo, jak hello łączniki nie są kolejne.</span><span class="sxs-lookup"><span data-stu-id="633c8-163">After starting hello index name with a letter or number, hello rest of hello name can include any letter, number and dashes, as long as hello dashes are not consecutive.</span></span>

<span data-ttu-id="633c8-164">Witaj `api-version` jest wymagana.</span><span class="sxs-lookup"><span data-stu-id="633c8-164">hello `api-version` is required.</span></span> <span data-ttu-id="633c8-165">Zobacz [przechowywanie wersji usługi wyszukiwania](http://msdn.microsoft.com/library/azure/dn864560.aspx) listę dostępnych wersji.</span><span class="sxs-lookup"><span data-stu-id="633c8-165">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for a list of available versions.</span></span>

<span data-ttu-id="633c8-166">**Nagłówki żądania**</span><span class="sxs-lookup"><span data-stu-id="633c8-166">**Request Headers**</span></span>

<span data-ttu-id="633c8-167">powitania po liście opisano hello wymagane i opcjonalne żądania nagłówków.</span><span class="sxs-lookup"><span data-stu-id="633c8-167">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="633c8-168">`Content-Type`: Wymagane.</span><span class="sxs-lookup"><span data-stu-id="633c8-168">`Content-Type`: Required.</span></span> <span data-ttu-id="633c8-169">Ustaw tę wartość za`application/json`</span><span class="sxs-lookup"><span data-stu-id="633c8-169">Set this too`application/json`</span></span>
* <span data-ttu-id="633c8-170">`api-key`: Wymagane.</span><span class="sxs-lookup"><span data-stu-id="633c8-170">`api-key`: Required.</span></span> <span data-ttu-id="633c8-171">Witaj `api-key` służy do</span><span class="sxs-lookup"><span data-stu-id="633c8-171">hello `api-key` is used to</span></span>
* <span data-ttu-id="633c8-172">Uwierzytelnianie usługi wyszukiwania tooyour żądania hello.</span><span class="sxs-lookup"><span data-stu-id="633c8-172">authenticate hello request tooyour Search service.</span></span> <span data-ttu-id="633c8-173">Jest to wartość ciągu, usługa tooyour unikatowy.</span><span class="sxs-lookup"><span data-stu-id="633c8-173">It is a string value, unique tooyour service.</span></span> <span data-ttu-id="633c8-174">Witaj **Create Index** żądanie musi zawierać `api-key` nagłówka ustawić tooyour klucza administratora (jako klucz zapytania min. tooa).</span><span class="sxs-lookup"><span data-stu-id="633c8-174">hello **Create Index** request must include an `api-key` header set tooyour admin key (as opposed tooa query key).</span></span>

<span data-ttu-id="633c8-175">Należy również adres URL hello usługi nazwa tooconstruct hello żądania.</span><span class="sxs-lookup"><span data-stu-id="633c8-175">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="633c8-176">Możesz uzyskać zarówno hello nazwy usługi i `api-key` z pulpitu nawigacyjnego usługi w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="633c8-176">You can get both hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="633c8-177">Zobacz [Tworzenie usługi Azure Search w portalu hello](search-create-service-portal.md) dla pomocy nawigacji strony.</span><span class="sxs-lookup"><span data-stu-id="633c8-177">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="633c8-178"><a name="RequestData"></a>
**Składnia treść żądania**</span><span class="sxs-lookup"><span data-stu-id="633c8-178"><a name="RequestData"></a>
**Request Body Syntax**</span></span>

<span data-ttu-id="633c8-179">Witaj treści żądania hello zawiera definicji schematu, w tym hello listy pól danych w dokumentach, którzy będą przekazywani do tego indeksu, typy danych, atrybutów, a także opcjonalną listę oceniania profilów, które są używane tooscore pasujących dokumentów w Czas kwerendy.</span><span class="sxs-lookup"><span data-stu-id="633c8-179">hello body of hello request contains a schema definition, which includes hello list of data fields within documents that will be fed into this index, data types, attributes, as well as an optional list of scoring profiles that are used tooscore matching documents at query time.</span></span>

<span data-ttu-id="633c8-180">Należy pamiętać, że dla żądania POST, należy określić nazwę indeksu hello w treści żądania hello.</span><span class="sxs-lookup"><span data-stu-id="633c8-180">Note that for a POST request, you must specify hello index name in hello request body.</span></span>

<span data-ttu-id="633c8-181">Może istnieć tylko jedno pole klucza w indeksie hello.</span><span class="sxs-lookup"><span data-stu-id="633c8-181">There can only be one key field in hello index.</span></span> <span data-ttu-id="633c8-182">Posiada toobe polem ciągu.</span><span class="sxs-lookup"><span data-stu-id="633c8-182">It has toobe a string field.</span></span> <span data-ttu-id="633c8-183">To pole reprezentuje unikatowy identyfikator każdego dokumentu przechowywanego w indeksie hello hello.</span><span class="sxs-lookup"><span data-stu-id="633c8-183">This field represents hello unique identifier for each document stored within hello index.</span></span>

<span data-ttu-id="633c8-184">główne części Hello indeksu Uwzględnij hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="633c8-184">hello main parts of an index include hello following:</span></span>

* `name`
* <span data-ttu-id="633c8-185">`fields`który będą przekazywani do tego indeksu, w tym nazwę, typ danych i właściwości, które definiują akcje dozwolone dla tego pola.</span><span class="sxs-lookup"><span data-stu-id="633c8-185">`fields` that will be fed into this index, including name, data type, and properties that define allowable actions on that field.</span></span>
* <span data-ttu-id="633c8-186">`suggesters`używany do wpisywaniu lub Autouzupełnianie zapytań.</span><span class="sxs-lookup"><span data-stu-id="633c8-186">`suggesters` used for auto-complete or type-ahead queries.</span></span>
* <span data-ttu-id="633c8-187">`scoringProfiles`używany do klasyfikacji wynik wyszukiwania niestandardowego.</span><span class="sxs-lookup"><span data-stu-id="633c8-187">`scoringProfiles` used for custom search score ranking.</span></span> <span data-ttu-id="633c8-188">Zobacz [Dodaj oceniania profile](https://msdn.microsoft.com/library/azure/dn798928.aspx) szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="633c8-188">See [Add scoring profiles](https://msdn.microsoft.com/library/azure/dn798928.aspx) for details.</span></span>
* <span data-ttu-id="633c8-189">`analyzers`, `charFilters`, `tokenizers`, `tokenFilters` używane toodefine jak dokumenty/kwerendy są podzielone na indeksowalnych/wyszukiwanie tokenów.</span><span class="sxs-lookup"><span data-stu-id="633c8-189">`analyzers`, `charFilters`, `tokenizers`, `tokenFilters` used toodefine how your documents/queries are broken into indexable/searchable tokens.</span></span> <span data-ttu-id="633c8-190">Zobacz [analizy w usłudze Azure Search](https://aka.ms//azsanalysis) szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="633c8-190">See [Analysis in Azure Search](https://aka.ms//azsanalysis) for details.</span></span>
* <span data-ttu-id="633c8-191">`defaultScoringProfile`użyć domyślnej hello toooverwrite oceniania zachowania.</span><span class="sxs-lookup"><span data-stu-id="633c8-191">`defaultScoringProfile` used toooverwrite hello default scoring behaviors.</span></span>
* <span data-ttu-id="633c8-192">`corsOptions`tooallow cross-origin zapytań względem indeksu.</span><span class="sxs-lookup"><span data-stu-id="633c8-192">`corsOptions` tooallow cross-origin queries against your index.</span></span>

<span data-ttu-id="633c8-193">Witaj dla struktury ładunku żądania hello ma następującą składnię.</span><span class="sxs-lookup"><span data-stu-id="633c8-193">hello syntax for structuring hello request payload is as follows.</span></span> <span data-ttu-id="633c8-194">Przykładowe żądanie znajduje się bardziej szczegółowo na, w tym temacie.</span><span class="sxs-lookup"><span data-stu-id="633c8-194">A sample request is provided further on in this topic.</span></span>

    {
      "name": (optional on PUT; required on POST) "name_of_index",
      "fields": [
        {
          "name": "name_of_field",
          "type": "Edm.String | Collection(Edm.String) | Edm.Int32 | Edm.Int64 | Edm.Double | Edm.Boolean | Edm.DateTimeOffset | Edm.GeographyPoint",
          "searchable": true (default where applicable) | false (only Edm.String and Collection(Edm.String) fields can be searchable),
          "filterable": true (default) | false,
          "sortable": true (default where applicable) | false (Collection(Edm.String) fields cannot be sortable),
          "facetable": true (default where applicable) | false (Edm.GeographyPoint fields cannot be facetable),
          "key": true | false (default, only Edm.String fields can be keys),
          "retrievable": true (default) | false,              
          "analyzer": "name of hello analyzer used for search and indexing", (only if 'searchAnalyzer' and 'indexAnalyzer' are not set)
          "searchAnalyzer": "name of hello search analyzer", (only if 'indexAnalyzer' is set and 'analyzer' is not set)
          "indexAnalyzer": "name of hello indexing analyzer" (only if 'searchAnalyzer' is set and 'analyzer' is not set)
        }
      ],
      "suggesters": [
        {
          "name": "name of suggester",
          "searchMode": "analyzingInfixMatching" (other modes may be added in hello future),
          "sourceFields": ["field1", "field2", ...]
        }
      ],
      "scoringProfiles": [
        {
          "name": "name of scoring profile",
          "text": (optional, only applies toosearchable fields) {
            "weights": {
              "searchable_field_name": relative_weight_value (positive numbers),
              ...
            }
          },
          "functions": (optional) [
            {
              "type": "magnitude | freshness | distance | tag",
              "boost": # (positive number used as multiplier for raw score != 1),
              "fieldName": "...",
              "interpolation": "constant | linear (default) | quadratic | logarithmic",
              "magnitude": {
                "boostingRangeStart": #,
                "boostingRangeEnd": #,
                "constantBoostBeyondRange": true | false (default)
              },
              "freshness": {
                "boostingDuration": "..." (value representing timespan leading toonow over which boosting occurs)
              },
              "distance": {
                "referencePointParameter": "...", (parameter toobe passed in queries toouse as reference location, see "scoringParameter" for syntax details)
                "boostingDistance": # (hello distance in kilometers from hello reference location where hello boosting range ends)
              },
              "tag": {
                "tagsParameter": "..." (parameter toobe passed in queries toospecify list of tags toocompare against target field, see "scoringParameter" for syntax details)
              }
            }
          ],
          "functionAggregation": (optional, applies only when functions are specified)
            "sum (default) | average | minimum | maximum | firstMatching"
        }
      ],
      "analyzers":(optional)[ ... ],
      "charFilters":(optional)[ ... ],
      "tokenizers":(optional)[ ... ],
      "tokenFilters":(optional)[ ... ],
      "defaultScoringProfile": (optional) "...",
      "corsOptions": (optional) {
        "allowedOrigins": ["*"] | ["origin_1", "origin_2", ...],
        "maxAgeInSeconds": (optional) max_age_in_seconds (non-negative integer)
      }
    }

<span data-ttu-id="633c8-195">**Atrybuty indeksu**</span><span class="sxs-lookup"><span data-stu-id="633c8-195">**Index Attributes**</span></span>

<span data-ttu-id="633c8-196">Witaj następujące atrybuty mogą zostać ustawione podczas tworzenia indeksu.</span><span class="sxs-lookup"><span data-stu-id="633c8-196">hello following attributes can be set when creating an index.</span></span> <span data-ttu-id="633c8-197">Aby uzyskać więcej informacji o oceniania i oceniania profilów, zobacz [dodać oceniania profile](https://msdn.microsoft.com/library/azure/dn798928.aspx).</span><span class="sxs-lookup"><span data-stu-id="633c8-197">For details about scoring and scoring profiles, see [Add scoring Profiles](https://msdn.microsoft.com/library/azure/dn798928.aspx).</span></span>

<span data-ttu-id="633c8-198">`name`— Ustawia hello nazwę pola hello.</span><span class="sxs-lookup"><span data-stu-id="633c8-198">`name` - Sets hello name of hello field.</span></span>

<span data-ttu-id="633c8-199">`type`— Ustawia hello typ danych pola hello.</span><span class="sxs-lookup"><span data-stu-id="633c8-199">`type` - Sets hello data type for hello field.</span></span>

<span data-ttu-id="633c8-200">`searchable`-Oznacza pole hello jako pełnotekstowego stanie wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="633c8-200">`searchable` - Marks hello field as full-text search-able.</span></span> <span data-ttu-id="633c8-201">Oznacza to, że zostaną poddane analizy, takich jak dzielenia wyrazów podczas indeksowania.</span><span class="sxs-lookup"><span data-stu-id="633c8-201">This means it will undergo analysis such as word-breaking during indexing.</span></span> <span data-ttu-id="633c8-202">Jeśli ustawisz `searchable` wartość tooa pola, takie jak "słoneczna day", wewnętrznie będzie podzielić na tokeny poszczególnych hello "Słoneczna" i "dzień".</span><span class="sxs-lookup"><span data-stu-id="633c8-202">If you set a `searchable` field tooa value like "sunny day", internally it will be split into hello individual tokens "sunny" and "day".</span></span> <span data-ttu-id="633c8-203">Dzięki temu wyszukiwania pełnotekstowego dla tych warunków.</span><span class="sxs-lookup"><span data-stu-id="633c8-203">This enables full-text searches for these terms.</span></span> <span data-ttu-id="633c8-204">Pola typu `Edm.String` lub `Collection(Edm.String)` są `searchable` domyślnie.</span><span class="sxs-lookup"><span data-stu-id="633c8-204">Fields of type `Edm.String` or `Collection(Edm.String)` are `searchable` by default.</span></span> <span data-ttu-id="633c8-205">Pola innych typów nie może być `searchable`.</span><span class="sxs-lookup"><span data-stu-id="633c8-205">Fields of other types cannot be `searchable`.</span></span>

* <span data-ttu-id="633c8-206">**Uwaga**: `searchable` pola korzystać dodatkowe miejsce w indeksie, ponieważ usługi Azure Search zapisze dodatkową wersję tokenami hello wartości pola dla wyszukiwania pełnotekstowego.</span><span class="sxs-lookup"><span data-stu-id="633c8-206">**Note**: `searchable` fields consume extra space in your index since Azure Search will store an additional tokenized version of hello field value for full-text searches.</span></span> <span data-ttu-id="633c8-207">Jeśli chcesz toosave miejsca indeksie i nie potrzebujesz toobe pola, uwzględniane podczas wyszukiwania, ustaw `searchable` zbyt`false`.</span><span class="sxs-lookup"><span data-stu-id="633c8-207">If you want toosave space in your index and you don't need a field toobe included in searches, set `searchable` too`false`.</span></span>

<span data-ttu-id="633c8-208">`filterable`— Umożliwia hello toobe pola, do którego odwołuje się `$filter` zapytania.</span><span class="sxs-lookup"><span data-stu-id="633c8-208">`filterable` - Allows hello field toobe referenced in `$filter` queries.</span></span> <span data-ttu-id="633c8-209">`filterable`różni się od `searchable` w sposób obsługi ciągów.</span><span class="sxs-lookup"><span data-stu-id="633c8-209">`filterable` differs from `searchable` in how strings are handled.</span></span> <span data-ttu-id="633c8-210">Pola typu `Edm.String` lub `Collection(Edm.String)` , które są `filterable` nie zostały poddane dzielenia wyrazów, więc porównania dla tylko dokładne dopasowania.</span><span class="sxs-lookup"><span data-stu-id="633c8-210">Fields of type `Edm.String` or `Collection(Edm.String)` that are `filterable` do not undergo word-breaking, so comparisons are for exact matches only.</span></span> <span data-ttu-id="633c8-211">Na przykład jeśli ustawisz takiego pola `f` zbyt "słoneczna day" `$filter=f eq 'sunny'` znajdziesz żadnych wyników, ale `$filter=f eq 'sunny day'` będzie.</span><span class="sxs-lookup"><span data-stu-id="633c8-211">For example, if you set such a field `f` too"sunny day", `$filter=f eq 'sunny'` will find no matches, but `$filter=f eq 'sunny day'` will.</span></span> <span data-ttu-id="633c8-212">Wszystkie pola są `filterable` domyślnie.</span><span class="sxs-lookup"><span data-stu-id="633c8-212">All fields are `filterable` by default.</span></span>

<span data-ttu-id="633c8-213">`sortable`-, Domyślnie hello system sortujące wyniki według wyników, ale w ramach wielu użytkownicy będą toosort według pól w dokumentach hello.</span><span class="sxs-lookup"><span data-stu-id="633c8-213">`sortable` - By default hello system sorts results by score, but in many experiences users will want toosort by fields in hello documents.</span></span> <span data-ttu-id="633c8-214">Pola typu `Collection(Edm.String)` nie może być `sortable`.</span><span class="sxs-lookup"><span data-stu-id="633c8-214">Fields of type `Collection(Edm.String)` cannot be `sortable`.</span></span> <span data-ttu-id="633c8-215">Wszystkie pozostałe pola są `sortable` domyślnie.</span><span class="sxs-lookup"><span data-stu-id="633c8-215">All other fields are `sortable` by default.</span></span>

<span data-ttu-id="633c8-216">`facetable`-Zazwyczaj używane w prezentacji wyników wyszukiwania, która zawiera liczby trafień według kategorii (na przykład, wyszukaj cyfrowe aparaty fotograficzne i trafień Zobacz przez marki, przez milionów pikseli, ceny, itp.).</span><span class="sxs-lookup"><span data-stu-id="633c8-216">`facetable`- Typically used in a presentation of search results that includes hit count by category (for example, search for digital cameras and see hits by brand, by megapixels, by price, etc.).</span></span> <span data-ttu-id="633c8-217">Nie można użyć tej opcji z polami typu `Edm.GeographyPoint`.</span><span class="sxs-lookup"><span data-stu-id="633c8-217">This option cannot be used with fields of type `Edm.GeographyPoint`.</span></span> <span data-ttu-id="633c8-218">Wszystkie pozostałe pola są `facetable` domyślnie.</span><span class="sxs-lookup"><span data-stu-id="633c8-218">All other fields are `facetable` by default.</span></span>

* <span data-ttu-id="633c8-219">**Uwaga**: pola typu `Edm.String` , które są `filterable`, `sortable`, lub `facetable` może mieć maksymalnie 32 KB długości.</span><span class="sxs-lookup"><span data-stu-id="633c8-219">**Note**: Fields of type `Edm.String` that are `filterable`, `sortable`, or `facetable` can be at most 32KB in length.</span></span> <span data-ttu-id="633c8-220">Jest tak, ponieważ takie pola są traktowane jako pojedynczy wyszukiwany termin, a maksymalna długość termin w usłudze Azure Search hello wynosi 32KB.</span><span class="sxs-lookup"><span data-stu-id="633c8-220">This is because such fields are treated as a single search term, and hello maximum length of a term in Azure Search is 32KB.</span></span> <span data-ttu-id="633c8-221">Jeśli potrzebujesz toostore tekstu więcej niż to pole będący pojedynczym ciągiem, konieczne będzie tooexplicitly ustawić `filterable`, `sortable`, i `facetable` zbyt`false` w definicji indeksu.</span><span class="sxs-lookup"><span data-stu-id="633c8-221">If you need toostore more text than this in a single string field, you will need tooexplicitly set `filterable`, `sortable`, and `facetable` too`false` in your index definition.</span></span>
* <span data-ttu-id="633c8-222">**Uwaga**: Jeśli pole ma żaden z powyższych hello atrybuty ustawić także`true` (`searchable`, `filterable`, `sortable`, lub`facetable`) pole hello skutecznie jest wykluczony z indeksu hello odwrócony.</span><span class="sxs-lookup"><span data-stu-id="633c8-222">**Note**: If a field has none of hello above attributes set too`true` (`searchable`, `filterable`, `sortable`,  or`facetable`) hello field is effectively excluded from hello inverted index.</span></span> <span data-ttu-id="633c8-223">Ta opcja przydaje się do pola, które nie są używane w zapytaniach, ale są wymagane w wynikach wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="633c8-223">This option is useful for fields that are not used in queries, but are needed in search results.</span></span> <span data-ttu-id="633c8-224">Z wyjątkiem tych pól z indeksu hello poprawia wydajność.</span><span class="sxs-lookup"><span data-stu-id="633c8-224">Excluding such fields from hello index improves performance.</span></span>

<span data-ttu-id="633c8-225">`key`— Znaczniki Witaj pole jako zawierające unikatowych identyfikatorów dla dokumentów w indeksie hello.</span><span class="sxs-lookup"><span data-stu-id="633c8-225">`key` - Marks hello field as containing unique identifiers for documents within hello index.</span></span> <span data-ttu-id="633c8-226">Należy wybrać dokładnie jedno pole jako hello `key` pola, a musi być typu `Edm.String`.</span><span class="sxs-lookup"><span data-stu-id="633c8-226">Exactly one field must be chosen as hello `key` field and it must be of type `Edm.String`.</span></span> <span data-ttu-id="633c8-227">Pola klucza może być używane toolook dokumentów bezpośrednio za pomocą hello [wyszukiwania API](#LookupAPI).</span><span class="sxs-lookup"><span data-stu-id="633c8-227">Key fields can be used toolook up documents directly via hello [Lookup API](#LookupAPI).</span></span>

<span data-ttu-id="633c8-228">`retrievable`— Ustawia, czy pole hello może być zwracany w wynikach wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="633c8-228">`retrievable` - Sets whether hello field can be returned in a search result.</span></span>  <span data-ttu-id="633c8-229">Jest to przydatne, gdy chcesz toouse pola (na przykład marginesu) jako filtru, sortowania, lub oceniania mechanizmu, ale nie chcesz, aby użytkownik końcowy hello pola toobe toohello widoczne.</span><span class="sxs-lookup"><span data-stu-id="633c8-229">This is useful when you want toouse a field (for example, margin) as a filter, sorting, or scoring mechanism but do not want hello field toobe visible toohello end user.</span></span> <span data-ttu-id="633c8-230">Ten atrybut musi być `true` dla `key` pola.</span><span class="sxs-lookup"><span data-stu-id="633c8-230">This attribute must be `true` for `key` fields.</span></span>

<span data-ttu-id="633c8-231">`analyzer`-Zestawy hello nazwa toouse analizator hello hello pola w czasie wyszukiwania i czas indeksowania.</span><span class="sxs-lookup"><span data-stu-id="633c8-231">`analyzer` - Sets hello name of hello analyzer toouse for hello field at search time and indexing time.</span></span> <span data-ttu-id="633c8-232">Witaj dozwolone zestaw wartości dla [analizatorów](https://msdn.microsoft.com/library/mt605304.aspx).</span><span class="sxs-lookup"><span data-stu-id="633c8-232">For hello allowed set of values see [Analyzers](https://msdn.microsoft.com/library/mt605304.aspx).</span></span> <span data-ttu-id="633c8-233">Ta opcja może być używana tylko z `searchable` pól i nie można ustawić razem albo `searchAnalyzer` lub `indexAnalyzer`.</span><span class="sxs-lookup"><span data-stu-id="633c8-233">This option can be used only with `searchable` fields and it can't be set together with either `searchAnalyzer` or `indexAnalyzer`.</span></span>  <span data-ttu-id="633c8-234">Po analizatora hello jest wybrana, nie można zmienić pola hello.</span><span class="sxs-lookup"><span data-stu-id="633c8-234">Once hello analyzer is chosen, it cannot be changed for hello field.</span></span>

<span data-ttu-id="633c8-235">`searchAnalyzer`— Ustawia hello nazwa używana w czasie wyszukiwania dla pola hello analizatora hello.</span><span class="sxs-lookup"><span data-stu-id="633c8-235">`searchAnalyzer` - Sets hello name of hello analyzer used at search time for hello field.</span></span> <span data-ttu-id="633c8-236">Witaj dozwolone zestaw wartości dla [analizatorów](https://msdn.microsoft.com/library/mt605304.aspx).</span><span class="sxs-lookup"><span data-stu-id="633c8-236">For hello allowed set of values see [Analyzers](https://msdn.microsoft.com/library/mt605304.aspx).</span></span> <span data-ttu-id="633c8-237">Ta opcja może być używana tylko z `searchable` pól.</span><span class="sxs-lookup"><span data-stu-id="633c8-237">This option can be used only with `searchable` fields.</span></span> <span data-ttu-id="633c8-238">Należy wybrać razem z `indexAnalyzer` i nie można ustawić wraz z hello `analyzer` opcji.</span><span class="sxs-lookup"><span data-stu-id="633c8-238">It must be set together with `indexAnalyzer` and it cannot be set together with hello `analyzer` option.</span></span> <span data-ttu-id="633c8-239">Analizator ten może zostać zaktualizowana na istniejącym polem.</span><span class="sxs-lookup"><span data-stu-id="633c8-239">This analyzer can be updated on an existing field.</span></span>

<span data-ttu-id="633c8-240">`indexAnalyzer`— Ustawia hello nazwa używana podczas indeksowania pola hello analizatora hello.</span><span class="sxs-lookup"><span data-stu-id="633c8-240">`indexAnalyzer` - Sets hello name of hello analyzer used at indexing time for hello field.</span></span> <span data-ttu-id="633c8-241">Witaj dozwolone zestaw wartości dla [analizatorów](https://msdn.microsoft.com/library/mt605304.aspx).</span><span class="sxs-lookup"><span data-stu-id="633c8-241">For hello allowed set of values see [Analyzers](https://msdn.microsoft.com/library/mt605304.aspx).</span></span> <span data-ttu-id="633c8-242">Ta opcja może być używana tylko z `searchable` pól.</span><span class="sxs-lookup"><span data-stu-id="633c8-242">This option can be used only with `searchable` fields.</span></span> <span data-ttu-id="633c8-243">Należy wybrać razem z `searchAnalyzer` i nie można ustawić wraz z hello `analyzer` opcji.</span><span class="sxs-lookup"><span data-stu-id="633c8-243">It must be set together with `searchAnalyzer` and it cannot be set together with hello `analyzer` option.</span></span> <span data-ttu-id="633c8-244">Po analizatora hello jest wybrana, nie można zmienić pola hello.</span><span class="sxs-lookup"><span data-stu-id="633c8-244">Once hello analyzer is chosen, it cannot be changed for hello field.</span></span>

<span data-ttu-id="633c8-245">`suggesters`— Ustawia hello tryb wyszukiwania i pola, które są hello źródło zawartości hello sugestie.</span><span class="sxs-lookup"><span data-stu-id="633c8-245">`suggesters` - Sets hello search mode and fields that are hello source of hello content for suggestions.</span></span> <span data-ttu-id="633c8-246">Zobacz [Sugestorów](#Suggesters) szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="633c8-246">See [Suggesters](#Suggesters) for details.</span></span>

<span data-ttu-id="633c8-247">`scoringProfiles`-Definiuje oceniania zachowań niestandardowych umożliwiające wpływ elementy, które są wyświetlane w wynikach wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="633c8-247">`scoringProfiles` - Defines custom scoring behaviors that let you influence which items appear higher in search results.</span></span> <span data-ttu-id="633c8-248">Profile oceniania składają się z wag pól i funkcji.</span><span class="sxs-lookup"><span data-stu-id="633c8-248">Scoring profiles are made up of field weights and functions.</span></span> <span data-ttu-id="633c8-249">Zobacz [dodać oceniania profile](https://msdn.microsoft.com/library/azure/dn798928.aspx) uzyskać więcej informacji dotyczących atrybutów hello używanych w profilu oceniania.</span><span class="sxs-lookup"><span data-stu-id="633c8-249">See [Add scoring Profiles](https://msdn.microsoft.com/library/azure/dn798928.aspx) for more information about hello attributes used in a scoring profile.</span></span>

<span data-ttu-id="633c8-250"><!-- This is a standalone topic in MSDN -->
<a name="LanguageSupport"></a>
**Obsługa języków**</span><span class="sxs-lookup"><span data-stu-id="633c8-250"><!-- This is a standalone topic in MSDN -->
<a name="LanguageSupport"></a>
**Language support**</span></span>

<span data-ttu-id="633c8-251">Pól z możliwością wyszukiwania przechodzą analizy najlepiej odpowiadającej często pociąga za sobą dzielenia wyrazów, normalizacji tekstu i filtrowanie warunki.</span><span class="sxs-lookup"><span data-stu-id="633c8-251">Searchable fields undergo analysis that most frequently involves word-breaking, text normalization, and filtering out terms.</span></span> <span data-ttu-id="633c8-252">Domyślnie pól z możliwością wyszukiwania w usłudze Azure Search są analizowane za pomocą hello [Apache Lucene standardowe analizator](http://lucene.apache.org/core/4_9_0/analyzers-common/index.html) który dzieli tekst na następujące elementy["Segmentacji tekst Unicode"](http://unicode.org/reports/tr29/) reguły.</span><span class="sxs-lookup"><span data-stu-id="633c8-252">By default, searchable fields in Azure Search are analyzed with hello [Apache Lucene Standard analyzer](http://lucene.apache.org/core/4_9_0/analyzers-common/index.html) which breaks text into elements following the["Unicode Text Segmentation"](http://unicode.org/reports/tr29/) rules.</span></span> <span data-ttu-id="633c8-253">Ponadto analizatora standardowe hello konwertuje wszystkie znaki tootheir małe litery formularza.</span><span class="sxs-lookup"><span data-stu-id="633c8-253">Additionally, hello standard analyzer converts all characters tootheir lower case form.</span></span> <span data-ttu-id="633c8-254">Zarówno indeksowanych dokumentów, jak i terminy wyszukiwania przechodzą przez analizy hello podczas indeksowania i przetwarzania kwerend.</span><span class="sxs-lookup"><span data-stu-id="633c8-254">Both indexed documents and search terms go through hello analysis during indexing and query processing.</span></span>

<span data-ttu-id="633c8-255">Usługa Azure Search obsługuje wiele języków.</span><span class="sxs-lookup"><span data-stu-id="633c8-255">Azure Search supports a variety of languages.</span></span> <span data-ttu-id="633c8-256">Każdego języka wymaga analyzer niestandardowy tekst, który konta dla właściwości danego języka.</span><span class="sxs-lookup"><span data-stu-id="633c8-256">Each language requires a non-standard text analyzer which accounts for characteristics of a given language.</span></span> <span data-ttu-id="633c8-257">Usługa Azure Search udostępnia dwa typy analizatorów:</span><span class="sxs-lookup"><span data-stu-id="633c8-257">Azure Search offers two types of analyzers:</span></span>

* <span data-ttu-id="633c8-258">obsługiwana przez Lucene 35 analizatorów.</span><span class="sxs-lookup"><span data-stu-id="633c8-258">35 analyzers backed by Lucene.</span></span>
* <span data-ttu-id="633c8-259">50 analizatorów obsługiwanej przez zastrzeżonych języka naturalnego Microsoft przetwarzania technologii używanej do pakietu Office i usługi Bing.</span><span class="sxs-lookup"><span data-stu-id="633c8-259">50 analyzers backed by proprietary Microsoft natural language processing technology used in Office and Bing.</span></span>

<span data-ttu-id="633c8-260">Niektórzy deweloperzy mogą preferować hello więcej znanego, prostego, open source rozwiązań związanych z Lucene.</span><span class="sxs-lookup"><span data-stu-id="633c8-260">Some developers might prefer hello more familiar, simple, open-source solution of Lucene.</span></span> <span data-ttu-id="633c8-261">Analizatory Lucene są szybsze, ale analizatorów Microsoft hello ma zaawansowane funkcje, takie jak Lematyzacja, decompounding (w językach takich jak niemiecki, duński, holenderski, szwedzki, norweski, estoński, Zakończ, węgierski, słowacki) i rozpoznawanie jednostek (adresów URL programu word wiadomości e-mail, dat, liczb).</span><span class="sxs-lookup"><span data-stu-id="633c8-261">Lucene analyzers are faster, but hello Microsoft analyzers have advanced capabilities, such as lemmatization, word decompounding (in languages like German, Danish, Dutch, Swedish, Norwegian, Estonian, Finish, Hungarian, Slovak) and entity recognition (URLs, emails, dates, numbers).</span></span> <span data-ttu-id="633c8-262">Jeśli to możliwe należy uruchomić porównania obu hello firmy Microsoft i Lucene analizatorów toodecide które z nich jest lepszym rozwiązaniem.</span><span class="sxs-lookup"><span data-stu-id="633c8-262">If possible, you should run comparisons of both hello Microsoft and Lucene analyzers toodecide which one is a better fit.</span></span>

<span data-ttu-id="633c8-263">***Ich porównanie***</span><span class="sxs-lookup"><span data-stu-id="633c8-263">***How they compare***</span></span>

<span data-ttu-id="633c8-264">Analizator Lucene powitania dla języka angielskiego rozszerza hello standardowe analizatora.</span><span class="sxs-lookup"><span data-stu-id="633c8-264">hello Lucene analyzer for English extends hello standard analyzer.</span></span> <span data-ttu-id="633c8-265">Usuwa Zaimki dzierżawcze (końcowe firmy) z wyrazy, dotyczy danych zgodnie [wynikające Porter algorytmu](http://tartarus.org/~martin/PorterStemmer/)i usuwa angielski [zatrzymać słowa](http://en.wikipedia.org/wiki/Stop_words).</span><span class="sxs-lookup"><span data-stu-id="633c8-265">It removes possessives (trailing 's) from words, applies stemming as per [Porter Stemming algorithm](http://tartarus.org/~martin/PorterStemmer/), and removes English [stop words](http://en.wikipedia.org/wiki/Stop_words).</span></span>

<span data-ttu-id="633c8-266">Z kolei analizatora Microsoft hello wykonuje Lematyzacja zamiast danych.</span><span class="sxs-lookup"><span data-stu-id="633c8-266">In comparison, hello Microsoft analyzer performs lemmatization instead of stemming.</span></span> <span data-ttu-id="633c8-267">Oznacza to, co powoduje dokładniejsze wyniki wyszukiwania może obsługiwać znacznie poprawia formularze word na przykład jeśli modulowany i nieregularne (czujki Moduł 7 [prezentacji MVA wyszukiwanie Azure](http://www.microsoftvirtualacademy.com/training-courses/adding-microsoft-azure-search-to-your-websites-and-apps) więcej szczegółów).</span><span class="sxs-lookup"><span data-stu-id="633c8-267">It means it can handle inflected and irregular word forms much better what results in more relevant search results (watch module 7 of [Azure Search MVA presentation](http://www.microsoftvirtualacademy.com/training-courses/adding-microsoft-azure-search-to-your-websites-and-apps) for more details).</span></span>

<span data-ttu-id="633c8-268">Indeksowanie z analizatorów firmy Microsoft jest średnio dwa razy toothree wolniej niż ich odpowiedniki Lucene, w zależności od języka hello.</span><span class="sxs-lookup"><span data-stu-id="633c8-268">Indexing with Microsoft analyzers is on average two toothree times slower than their Lucene equivalents, depending on hello language.</span></span> <span data-ttu-id="633c8-269">Wydajność wyszukiwania nie może znacząco kolidować średni rozmiar zapytań.</span><span class="sxs-lookup"><span data-stu-id="633c8-269">Search performance should not be significantly affected for average size queries.</span></span>

<span data-ttu-id="633c8-270">***Konfiguracja***</span><span class="sxs-lookup"><span data-stu-id="633c8-270">***Configuration***</span></span>

<span data-ttu-id="633c8-271">Dla każdego pola w definicji indeksu hello można ustawić hello `analyzer` nazwy analizator tooan właściwości, która określa, które języka i dostawcy.</span><span class="sxs-lookup"><span data-stu-id="633c8-271">For each field in hello index definition, you can set hello `analyzer` property tooan analyzer name that specifies which language and vendor.</span></span> <span data-ttu-id="633c8-272">Witaj, analizator tego samego zostaną zastosowane podczas indeksowania i wyszukiwania dla tego pola.</span><span class="sxs-lookup"><span data-stu-id="633c8-272">hello same analyzer will be applied when indexing and searching for that field.</span></span>
<span data-ttu-id="633c8-273">Na przykład można mieć oddzielne pola angielskim, francuskim i hiszpańskim opisy hoteli, które istnieją side-by-side w hello sam indeks.</span><span class="sxs-lookup"><span data-stu-id="633c8-273">For example, you can have separate fields for English, French, and Spanish hotel descriptions that exist side-by-side in hello same index.</span></span> <span data-ttu-id="633c8-274">Użyj hello [parametr zapytania "searchFields"](#SearchQueryParameters) toospecify które toosearch pola specyficzny dla języka dla zapytania.</span><span class="sxs-lookup"><span data-stu-id="633c8-274">Use hello ['searchFields' query parameter](#SearchQueryParameters) toospecify which language-specific field toosearch against in your queries.</span></span> <span data-ttu-id="633c8-275">Możesz przejrzeć przykłady zapytania, które zawierają hello `analyzer` właściwości w [dokumenty wyszukiwania](#SearchDocs).</span><span class="sxs-lookup"><span data-stu-id="633c8-275">You can review query examples that include hello `analyzer` property in [Search Documents](#SearchDocs).</span></span> 

<span data-ttu-id="633c8-276">***Lista analizatora***</span><span class="sxs-lookup"><span data-stu-id="633c8-276">***Analyzer list***</span></span>

<span data-ttu-id="633c8-277">Poniżej znajduje się hello listę obsługiwanych języków oraz nazw analizator Lucene i firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="633c8-277">Below is hello list of supported languages together with Lucene and Microsoft analyzer names.</span></span>

<table style="font-size:12">
    <tr>
        <th><span data-ttu-id="633c8-278">Język</span><span class="sxs-lookup"><span data-stu-id="633c8-278">Language</span></span></th>
        <th><span data-ttu-id="633c8-279">Analizator firmy Microsoft o nazwie</span><span class="sxs-lookup"><span data-stu-id="633c8-279">Microsoft analyzer name</span></span></th>
        <th><span data-ttu-id="633c8-280">Nazwa analizator Lucene</span><span class="sxs-lookup"><span data-stu-id="633c8-280">Lucene analyzer name</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="633c8-281">Arabski</span><span class="sxs-lookup"><span data-stu-id="633c8-281">Arabic</span></span></td>
        <td><span data-ttu-id="633c8-282">ar.Microsoft</span><span class="sxs-lookup"><span data-stu-id="633c8-282">ar.microsoft</span></span></td>
        <td><span data-ttu-id="633c8-283">ar.lucene</span><span class="sxs-lookup"><span data-stu-id="633c8-283">ar.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="633c8-284">Armeński</span><span class="sxs-lookup"><span data-stu-id="633c8-284">Armenian</span></span></td>
        <td></td>
        <td><span data-ttu-id="633c8-285">HY.lucene</span><span class="sxs-lookup"><span data-stu-id="633c8-285">hy.lucene</span></span></td>
      </tr>
    <tr>
        <td><span data-ttu-id="633c8-286">Bengalski</span><span class="sxs-lookup"><span data-stu-id="633c8-286">Bangla</span></span></td>
        <td><span data-ttu-id="633c8-287">BN.Microsoft</span><span class="sxs-lookup"><span data-stu-id="633c8-287">bn.microsoft</span></span></td>
        <td></td>
    </tr>
      <tr>
        <td><span data-ttu-id="633c8-288">Baskijski</span><span class="sxs-lookup"><span data-stu-id="633c8-288">Basque</span></span></td>
        <td></td>
        <td><span data-ttu-id="633c8-289">EU.lucene</span><span class="sxs-lookup"><span data-stu-id="633c8-289">eu.lucene</span></span></td>
    </tr>
      <tr>
         <td><span data-ttu-id="633c8-290">Bułgarski</span><span class="sxs-lookup"><span data-stu-id="633c8-290">Bulgarian</span></span></td>
        <td><span data-ttu-id="633c8-291">BG.Microsoft</span><span class="sxs-lookup"><span data-stu-id="633c8-291">bg.microsoft</span></span></td>
        <td><span data-ttu-id="633c8-292">BG.lucene</span><span class="sxs-lookup"><span data-stu-id="633c8-292">bg.lucene</span></span></td>
      </tr>
      <tr>
        <td><span data-ttu-id="633c8-293">Kataloński</span><span class="sxs-lookup"><span data-stu-id="633c8-293">Catalan</span></span></td>
        <td><span data-ttu-id="633c8-294">CA.Microsoft</span><span class="sxs-lookup"><span data-stu-id="633c8-294">ca.microsoft</span></span></td>
        <td><span data-ttu-id="633c8-295">CA.lucene</span><span class="sxs-lookup"><span data-stu-id="633c8-295">ca.lucene</span></span></td>          
      </tr>
    <tr>
        <td><span data-ttu-id="633c8-296">Chiński uproszczony</span><span class="sxs-lookup"><span data-stu-id="633c8-296">Chinese Simplified</span></span></td>
        <td><span data-ttu-id="633c8-297">zh-Hans.microsoft</span><span class="sxs-lookup"><span data-stu-id="633c8-297">zh-Hans.microsoft</span></span></td>
        <td><span data-ttu-id="633c8-298">zh-Hans.lucene</span><span class="sxs-lookup"><span data-stu-id="633c8-298">zh-Hans.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="633c8-299">Chiński tradycyjny</span><span class="sxs-lookup"><span data-stu-id="633c8-299">Chinese Traditional</span></span></td>
        <td><span data-ttu-id="633c8-300">zh-Hant.microsoft</span><span class="sxs-lookup"><span data-stu-id="633c8-300">zh-Hant.microsoft</span></span></td>
        <td><span data-ttu-id="633c8-301">zh-Hant.lucene</span><span class="sxs-lookup"><span data-stu-id="633c8-301">zh-Hant.lucene</span></span></td>        
    <tr>
    <tr>
        <td><span data-ttu-id="633c8-302">Chorwacki</span><span class="sxs-lookup"><span data-stu-id="633c8-302">Croatian</span></span></td>
        <td><span data-ttu-id="633c8-303">hr.Microsoft</span><span class="sxs-lookup"><span data-stu-id="633c8-303">hr.microsoft</span></span></td>
        <td/></td>
    </tr>
    <tr>
        <td><span data-ttu-id="633c8-304">Czeski</span><span class="sxs-lookup"><span data-stu-id="633c8-304">Czech</span></span></td>
        <td><span data-ttu-id="633c8-305">CS.Microsoft</span><span class="sxs-lookup"><span data-stu-id="633c8-305">cs.microsoft</span></span></td>
        <td><span data-ttu-id="633c8-306">CS.lucene</span><span class="sxs-lookup"><span data-stu-id="633c8-306">cs.lucene</span></span></td>        
    </tr>    
    <tr>
        <td><span data-ttu-id="633c8-307">Duński</span><span class="sxs-lookup"><span data-stu-id="633c8-307">Danish</span></span></td>
        <td><span data-ttu-id="633c8-308">da.Microsoft</span><span class="sxs-lookup"><span data-stu-id="633c8-308">da.microsoft</span></span></td>
        <td><span data-ttu-id="633c8-309">da.lucene</span><span class="sxs-lookup"><span data-stu-id="633c8-309">da.lucene</span></span></td>        
    </tr>    
    <tr>
        <td><span data-ttu-id="633c8-310">Holenderski</span><span class="sxs-lookup"><span data-stu-id="633c8-310">Dutch</span></span></td>
        <td><span data-ttu-id="633c8-311">NL.Microsoft</span><span class="sxs-lookup"><span data-stu-id="633c8-311">nl.microsoft</span></span></td>
        <td><span data-ttu-id="633c8-312">NL.lucene</span><span class="sxs-lookup"><span data-stu-id="633c8-312">nl.lucene</span></span></td>    
    </tr>    
    <tr>
        <td><span data-ttu-id="633c8-313">Polski</span><span class="sxs-lookup"><span data-stu-id="633c8-313">English</span></span></td>        
        <td><span data-ttu-id="633c8-314">EN.Microsoft</span><span class="sxs-lookup"><span data-stu-id="633c8-314">en.microsoft</span></span></td>
        <td><span data-ttu-id="633c8-315">EN.lucene</span><span class="sxs-lookup"><span data-stu-id="633c8-315">en.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="633c8-316">Estoński</span><span class="sxs-lookup"><span data-stu-id="633c8-316">Estonian</span></span></td>
        <td><span data-ttu-id="633c8-317">et.Microsoft</span><span class="sxs-lookup"><span data-stu-id="633c8-317">et.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="633c8-318">Fiński</span><span class="sxs-lookup"><span data-stu-id="633c8-318">Finnish</span></span></td>
        <td><span data-ttu-id="633c8-319">Fi.Microsoft</span><span class="sxs-lookup"><span data-stu-id="633c8-319">fi.microsoft</span></span></td>
        <td><span data-ttu-id="633c8-320">Fi.lucene</span><span class="sxs-lookup"><span data-stu-id="633c8-320">fi.lucene</span></span></td>        
    </tr>    
    <tr>
        <td><span data-ttu-id="633c8-321">Francuski</span><span class="sxs-lookup"><span data-stu-id="633c8-321">French</span></span></td>
        <td><span data-ttu-id="633c8-322">FR.Microsoft</span><span class="sxs-lookup"><span data-stu-id="633c8-322">fr.microsoft</span></span></td>
        <td><span data-ttu-id="633c8-323">FR.lucene</span><span class="sxs-lookup"><span data-stu-id="633c8-323">fr.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="633c8-324">Galicyjski</span><span class="sxs-lookup"><span data-stu-id="633c8-324">Galician</span></span></td>
        <td></td>
        <td><span data-ttu-id="633c8-325">GL.lucene</span><span class="sxs-lookup"><span data-stu-id="633c8-325">gl.lucene</span></span></td>        
      </tr>
    <tr>
        <td><span data-ttu-id="633c8-326">Niemiecki</span><span class="sxs-lookup"><span data-stu-id="633c8-326">German</span></span></td>
        <td><span data-ttu-id="633c8-327">de.Microsoft</span><span class="sxs-lookup"><span data-stu-id="633c8-327">de.microsoft</span></span></td>
        <td><span data-ttu-id="633c8-328">de.lucene</span><span class="sxs-lookup"><span data-stu-id="633c8-328">de.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="633c8-329">Grecki</span><span class="sxs-lookup"><span data-stu-id="633c8-329">Greek</span></span></td>
        <td><span data-ttu-id="633c8-330">el.Microsoft</span><span class="sxs-lookup"><span data-stu-id="633c8-330">el.microsoft</span></span></td>
        <td><span data-ttu-id="633c8-331">el.lucene</span><span class="sxs-lookup"><span data-stu-id="633c8-331">el.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="633c8-332">Gudżarati</span><span class="sxs-lookup"><span data-stu-id="633c8-332">Gujarati</span></span></td>
        <td><span data-ttu-id="633c8-333">gu.Microsoft</span><span class="sxs-lookup"><span data-stu-id="633c8-333">gu.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="633c8-334">Hebrajski</span><span class="sxs-lookup"><span data-stu-id="633c8-334">Hebrew</span></span></td>
        <td><span data-ttu-id="633c8-335">HE.Microsoft</span><span class="sxs-lookup"><span data-stu-id="633c8-335">he.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="633c8-336">Hindi</span><span class="sxs-lookup"><span data-stu-id="633c8-336">Hindi</span></span></td>
        <td><span data-ttu-id="633c8-337">Hi.Microsoft</span><span class="sxs-lookup"><span data-stu-id="633c8-337">hi.microsoft</span></span></td>
        <td><span data-ttu-id="633c8-338">Hi.lucene</span><span class="sxs-lookup"><span data-stu-id="633c8-338">hi.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="633c8-339">Węgierski</span><span class="sxs-lookup"><span data-stu-id="633c8-339">Hungarian</span></span></td>        
        <td><span data-ttu-id="633c8-340">HU.Microsoft</span><span class="sxs-lookup"><span data-stu-id="633c8-340">hu.microsoft</span></span></td>
        <td><span data-ttu-id="633c8-341">HU.lucene</span><span class="sxs-lookup"><span data-stu-id="633c8-341">hu.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="633c8-342">Islandzki</span><span class="sxs-lookup"><span data-stu-id="633c8-342">Icelandic</span></span></td>
        <td><span data-ttu-id="633c8-343">is.Microsoft</span><span class="sxs-lookup"><span data-stu-id="633c8-343">is.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="633c8-344">Indonezyjski (Bahasa)</span><span class="sxs-lookup"><span data-stu-id="633c8-344">Indonesian (Bahasa)</span></span></td>
        <td><span data-ttu-id="633c8-345">ID.Microsoft</span><span class="sxs-lookup"><span data-stu-id="633c8-345">id.microsoft</span></span></td>
        <td><span data-ttu-id="633c8-346">ID.lucene</span><span class="sxs-lookup"><span data-stu-id="633c8-346">id.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="633c8-347">Irlandzki</span><span class="sxs-lookup"><span data-stu-id="633c8-347">Irish</span></span></td>
        <td></td>
          <td><span data-ttu-id="633c8-348">GA.lucene</span><span class="sxs-lookup"><span data-stu-id="633c8-348">ga.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="633c8-349">Włoski</span><span class="sxs-lookup"><span data-stu-id="633c8-349">Italian</span></span></td>
        <td><span data-ttu-id="633c8-350">IT.Microsoft</span><span class="sxs-lookup"><span data-stu-id="633c8-350">it.microsoft</span></span></td>
        <td><span data-ttu-id="633c8-351">IT.lucene</span><span class="sxs-lookup"><span data-stu-id="633c8-351">it.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="633c8-352">Japoński</span><span class="sxs-lookup"><span data-stu-id="633c8-352">Japanese</span></span></td>
        <td><span data-ttu-id="633c8-353">ja.Microsoft</span><span class="sxs-lookup"><span data-stu-id="633c8-353">ja.microsoft</span></span></td>
        <td><span data-ttu-id="633c8-354">ja.lucene</span><span class="sxs-lookup"><span data-stu-id="633c8-354">ja.lucene</span></span></td>

    </tr>
    <tr>
        <td><span data-ttu-id="633c8-355">Kannada</span><span class="sxs-lookup"><span data-stu-id="633c8-355">Kannada</span></span></td>
        <td><span data-ttu-id="633c8-356">Ka.Microsoft</span><span class="sxs-lookup"><span data-stu-id="633c8-356">ka.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="633c8-357">Koreański</span><span class="sxs-lookup"><span data-stu-id="633c8-357">Korean</span></span></td>
        <td><span data-ttu-id="633c8-358">Ko.Microsoft</span><span class="sxs-lookup"><span data-stu-id="633c8-358">ko.microsoft</span></span></td>
        <td><span data-ttu-id="633c8-359">Ko.lucene</span><span class="sxs-lookup"><span data-stu-id="633c8-359">ko.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="633c8-360">Łotewski</span><span class="sxs-lookup"><span data-stu-id="633c8-360">Latvian</span></span></td>        
        <td><span data-ttu-id="633c8-361">LV.Microsoft</span><span class="sxs-lookup"><span data-stu-id="633c8-361">lv.microsoft</span></span></td>
        <td><span data-ttu-id="633c8-362">LV.lucene</span><span class="sxs-lookup"><span data-stu-id="633c8-362">lv.lucene</span></span></td>    
    </tr>
    <tr>
        <td><span data-ttu-id="633c8-363">Litewski</span><span class="sxs-lookup"><span data-stu-id="633c8-363">Lithuanian</span></span></td>
        <td><span data-ttu-id="633c8-364">lt.Microsoft</span><span class="sxs-lookup"><span data-stu-id="633c8-364">lt.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="633c8-365">Malayalam</span><span class="sxs-lookup"><span data-stu-id="633c8-365">Malayalam</span></span></td>
        <td><span data-ttu-id="633c8-366">ml.Microsoft</span><span class="sxs-lookup"><span data-stu-id="633c8-366">ml.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="633c8-367">Malajski (łaciński)</span><span class="sxs-lookup"><span data-stu-id="633c8-367">Malay (Latin)</span></span></td>
        <td><span data-ttu-id="633c8-368">MS.Microsoft</span><span class="sxs-lookup"><span data-stu-id="633c8-368">ms.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="633c8-369">Marathi</span><span class="sxs-lookup"><span data-stu-id="633c8-369">Marathi</span></span></td>
        <td><span data-ttu-id="633c8-370">MR.Microsoft</span><span class="sxs-lookup"><span data-stu-id="633c8-370">mr.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="633c8-371">Norweski</span><span class="sxs-lookup"><span data-stu-id="633c8-371">Norwegian</span></span></td>
        <td><span data-ttu-id="633c8-372">NB.Microsoft</span><span class="sxs-lookup"><span data-stu-id="633c8-372">nb.microsoft</span></span></td>
        <td><span data-ttu-id="633c8-373">No.lucene</span><span class="sxs-lookup"><span data-stu-id="633c8-373">no.lucene</span></span></td>        
    </tr>
      <tr>
        <td><span data-ttu-id="633c8-374">Perski</span><span class="sxs-lookup"><span data-stu-id="633c8-374">Persian</span></span></td>
        <td></td>
        <td><span data-ttu-id="633c8-375">fa.lucene</span><span class="sxs-lookup"><span data-stu-id="633c8-375">fa.lucene</span></span></td>        
      </tr>
    <tr>
        <td><span data-ttu-id="633c8-376">Polski</span><span class="sxs-lookup"><span data-stu-id="633c8-376">Polish</span></span></td>
        <td><span data-ttu-id="633c8-377">pl.Microsoft</span><span class="sxs-lookup"><span data-stu-id="633c8-377">pl.microsoft</span></span></td>
        <td><span data-ttu-id="633c8-378">pl.lucene</span><span class="sxs-lookup"><span data-stu-id="633c8-378">pl.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="633c8-379">Portugalski (Brazylia)</span><span class="sxs-lookup"><span data-stu-id="633c8-379">Portuguese (Brazil)</span></span></td>
        <td><span data-ttu-id="633c8-380">PT Br.microsoft</span><span class="sxs-lookup"><span data-stu-id="633c8-380">pt-Br.microsoft</span></span></td>
        <td><span data-ttu-id="633c8-381">PT Br.lucene</span><span class="sxs-lookup"><span data-stu-id="633c8-381">pt-Br.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="633c8-382">Portugalski (Portugalia)</span><span class="sxs-lookup"><span data-stu-id="633c8-382">Portuguese (Portugal)</span></span></td>
        <td><span data-ttu-id="633c8-383">PT Pt.microsoft</span><span class="sxs-lookup"><span data-stu-id="633c8-383">pt-Pt.microsoft</span></span></td>        
        <td><span data-ttu-id="633c8-384">PT Pt.lucene</span><span class="sxs-lookup"><span data-stu-id="633c8-384">pt-Pt.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="633c8-385">Pendżabski</span><span class="sxs-lookup"><span data-stu-id="633c8-385">Punjabi</span></span></td>
        <td><span data-ttu-id="633c8-386">Pa.Microsoft</span><span class="sxs-lookup"><span data-stu-id="633c8-386">pa.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="633c8-387">Rumuński</span><span class="sxs-lookup"><span data-stu-id="633c8-387">Romanian</span></span></td>
        <td><span data-ttu-id="633c8-388">ro.Microsoft</span><span class="sxs-lookup"><span data-stu-id="633c8-388">ro.microsoft</span></span></td>
        <td><span data-ttu-id="633c8-389">ro.lucene</span><span class="sxs-lookup"><span data-stu-id="633c8-389">ro.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="633c8-390">Rosyjski</span><span class="sxs-lookup"><span data-stu-id="633c8-390">Russian</span></span></td>
        <td><span data-ttu-id="633c8-391">RU.Microsoft</span><span class="sxs-lookup"><span data-stu-id="633c8-391">ru.microsoft</span></span></td>
        <td><span data-ttu-id="633c8-392">RU.lucene</span><span class="sxs-lookup"><span data-stu-id="633c8-392">ru.lucene</span></span></td>    
    </tr>
    <tr>
        <td><span data-ttu-id="633c8-393">Serbski (Cyrylica)</span><span class="sxs-lookup"><span data-stu-id="633c8-393">Serbian (Cyrillic)</span></span></td>
        <td><span data-ttu-id="633c8-394">SR-cyrillic.microsoft</span><span class="sxs-lookup"><span data-stu-id="633c8-394">sr-cyrillic.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="633c8-395">Serbski (łaciński)</span><span class="sxs-lookup"><span data-stu-id="633c8-395">Serbian (Latin)</span></span></td>
        <td><span data-ttu-id="633c8-396">SR-latin.microsoft</span><span class="sxs-lookup"><span data-stu-id="633c8-396">sr-latin.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="633c8-397">Słowacki</span><span class="sxs-lookup"><span data-stu-id="633c8-397">Slovak</span></span></td>
        <td><span data-ttu-id="633c8-398">SK.Microsoft</span><span class="sxs-lookup"><span data-stu-id="633c8-398">sk.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="633c8-399">Słoweński</span><span class="sxs-lookup"><span data-stu-id="633c8-399">Slovenian</span></span></td>
        <td><span data-ttu-id="633c8-400">SL.Microsoft</span><span class="sxs-lookup"><span data-stu-id="633c8-400">sl.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="633c8-401">Hiszpański</span><span class="sxs-lookup"><span data-stu-id="633c8-401">Spanish</span></span></td>
        <td><span data-ttu-id="633c8-402">ES.Microsoft</span><span class="sxs-lookup"><span data-stu-id="633c8-402">es.microsoft</span></span></td>
        <td><span data-ttu-id="633c8-403">ES.lucene</span><span class="sxs-lookup"><span data-stu-id="633c8-403">es.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="633c8-404">Szwedzki</span><span class="sxs-lookup"><span data-stu-id="633c8-404">Swedish</span></span></td>
        <td><span data-ttu-id="633c8-405">SV.Microsoft</span><span class="sxs-lookup"><span data-stu-id="633c8-405">sv.microsoft</span></span></td>
        <td><span data-ttu-id="633c8-406">SV.lucene</span><span class="sxs-lookup"><span data-stu-id="633c8-406">sv.lucene</span></span></td>
    </tr>

    <tr>
        <td><span data-ttu-id="633c8-407">Tamilski</span><span class="sxs-lookup"><span data-stu-id="633c8-407">Tamil</span></span></td>
        <td><span data-ttu-id="633c8-408">Ta.Microsoft</span><span class="sxs-lookup"><span data-stu-id="633c8-408">ta.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="633c8-409">Telugu</span><span class="sxs-lookup"><span data-stu-id="633c8-409">Telugu</span></span></td>
        <td><span data-ttu-id="633c8-410">te.Microsoft</span><span class="sxs-lookup"><span data-stu-id="633c8-410">te.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="633c8-411">Tajski</span><span class="sxs-lookup"><span data-stu-id="633c8-411">Thai</span></span></td>
        <td><span data-ttu-id="633c8-412">TH.Microsoft</span><span class="sxs-lookup"><span data-stu-id="633c8-412">th.microsoft</span></span></td>
        <td><span data-ttu-id="633c8-413">TH.lucene</span><span class="sxs-lookup"><span data-stu-id="633c8-413">th.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="633c8-414">Turecki</span><span class="sxs-lookup"><span data-stu-id="633c8-414">Turkish</span></span></td>
        <td><span data-ttu-id="633c8-415">TR.Microsoft</span><span class="sxs-lookup"><span data-stu-id="633c8-415">tr.microsoft</span></span></td>
        <td><span data-ttu-id="633c8-416">TR.lucene</span><span class="sxs-lookup"><span data-stu-id="633c8-416">tr.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="633c8-417">Ukraiński</span><span class="sxs-lookup"><span data-stu-id="633c8-417">Ukrainian</span></span></td>
        <td><span data-ttu-id="633c8-418">UK.Microsoft</span><span class="sxs-lookup"><span data-stu-id="633c8-418">uk.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="633c8-419">Urdu</span><span class="sxs-lookup"><span data-stu-id="633c8-419">Urdu</span></span></td>
        <td><span data-ttu-id="633c8-420">Your.Microsoft</span><span class="sxs-lookup"><span data-stu-id="633c8-420">ur.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="633c8-421">Wietnamski</span><span class="sxs-lookup"><span data-stu-id="633c8-421">Vietnamese</span></span></td>
        <td><span data-ttu-id="633c8-422">VI.Microsoft</span><span class="sxs-lookup"><span data-stu-id="633c8-422">vi.microsoft</span></span></td>
        <td></td>
    </tr>
    <td colspan="3"><span data-ttu-id="633c8-423">Ponadto usługi Azure Search udostępnia konfiguracje analizatora niezależny od języka</span><span class="sxs-lookup"><span data-stu-id="633c8-423">Additionally Azure Search provides language-agnostic analyzer configurations</span></span></td>
    <tr>
        <td><span data-ttu-id="633c8-424">ASCII standardowa składanie</span><span class="sxs-lookup"><span data-stu-id="633c8-424">Standard ASCII Folding</span></span></td>
        <td><span data-ttu-id="633c8-425">standardasciifolding.lucene</span><span class="sxs-lookup"><span data-stu-id="633c8-425">standardasciifolding.lucene</span></span></td>
        <td>
        <ul>
            <li><span data-ttu-id="633c8-426">Segmentacja tekst Unicode (Tokenizatora standardowy)</span><span class="sxs-lookup"><span data-stu-id="633c8-426">Unicode text segmentation (Standard Tokenizer)</span></span></li>
            <li><span data-ttu-id="633c8-427">Filtr składania ASCII — konwertuje znaki Unicode, które należą do ich odpowiedniki ASCII zestawu toohello najpierw 127 znaków ASCII.</span><span class="sxs-lookup"><span data-stu-id="633c8-427">ASCII folding filter - converts Unicode characters that don't belong toohello set of first 127 ASCII characters into their ASCII equivalents.</span></span> <span data-ttu-id="633c8-428">Jest to przydatne w celu usunięcia znaków diakrytycznych.</span><span class="sxs-lookup"><span data-stu-id="633c8-428">This is useful for removing diacritics.</span></span></li>
        </ul>
        </td>
    </tr>
</table>

<span data-ttu-id="633c8-429">Wszystkie analizatory z nazwami opatrzoną <i>lucene</i> są obsługiwane przez [analizatorów języka Apache Lucene](http://lucene.apache.org/core/4_9_0/analyzers-common/overview-summary.html).</span><span class="sxs-lookup"><span data-stu-id="633c8-429">All analyzers with names annotated with <i>lucene</i> are powered by [Apache Lucene's language analyzers](http://lucene.apache.org/core/4_9_0/analyzers-common/overview-summary.html).</span></span> <span data-ttu-id="633c8-430">Więcej informacji na temat ASCII hello składania filtru można znaleźć [tutaj](http://lucene.apache.org/core/4_9_0/analyzers-common/org/apache/lucene/analysis/miscellaneous/ASCIIFoldingFilter.html).</span><span class="sxs-lookup"><span data-stu-id="633c8-430">More information about hello ASCII folding filter can be found [here](http://lucene.apache.org/core/4_9_0/analyzers-common/org/apache/lucene/analysis/miscellaneous/ASCIIFoldingFilter.html).</span></span>

<span data-ttu-id="633c8-431">**Funkcje sugestii**</span><span class="sxs-lookup"><span data-stu-id="633c8-431">**Suggesters**</span></span>

<span data-ttu-id="633c8-432">A `suggester` definiuje pola w indeksie, które są używane toosupport funkcja automatycznego uzupełniania w wynikach wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="633c8-432">A `suggester` defines which fields in an index are used toosupport auto-complete in searches.</span></span> <span data-ttu-id="633c8-433">Zwykle ciągi częściowe wyszukiwania są wysyłane toohello [API sugestie](#Suggestions) użytkownika hello pisze zapytania wyszukiwania i hello interfejsu API zwraca zestaw sugerowane wyrażeń.</span><span class="sxs-lookup"><span data-stu-id="633c8-433">Typically partial search strings are sent toohello [Suggestions API](#Suggestions) while hello user is typing a search query, and hello API returns a set of suggested phrases.</span></span> <span data-ttu-id="633c8-434">Sugestora, zdefiniowanego w indeksie hello określa pola, które są używane toobuild hello wpisywaniu wyszukiwania terminów.</span><span class="sxs-lookup"><span data-stu-id="633c8-434">A suggester that you define in hello index determines which fields are used toobuild hello type-ahead search terms.</span></span> <span data-ttu-id="633c8-435">Zobacz [Sugestorów](#Suggesters) szczegółowe informacje dotyczące konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="633c8-435">See [Suggesters](#Suggesters) for configuration details.</span></span>

<span data-ttu-id="633c8-436">**Profile oceniania**</span><span class="sxs-lookup"><span data-stu-id="633c8-436">**Scoring profiles**</span></span>

<span data-ttu-id="633c8-437">A `scoringProfile` definiuje oceniania zachowań niestandardowych umożliwiające wpływ elementy, które są wyświetlane w wynikach wyszukiwania hello wyższy.</span><span class="sxs-lookup"><span data-stu-id="633c8-437">A `scoringProfile` defines custom scoring behaviors that let you influence which items appear higher in hello search results.</span></span> <span data-ttu-id="633c8-438">Profile oceniania składają się z wag pól i funkcji.</span><span class="sxs-lookup"><span data-stu-id="633c8-438">Scoring profiles are made up of field weights and functions.</span></span> <span data-ttu-id="633c8-439">toouse ich, określ profil według nazwy na powitania ciągu zapytania.</span><span class="sxs-lookup"><span data-stu-id="633c8-439">toouse them, you specify a profile by name on hello query string.</span></span>

<span data-ttu-id="633c8-440">Domyślny profil oceniania działa za toocompute sceny hello wynik wyszukiwania dla każdego elementu w zestawie wyników.</span><span class="sxs-lookup"><span data-stu-id="633c8-440">A default scoring profile operates behind hello scenes toocompute a search score for every item in a result set.</span></span> <span data-ttu-id="633c8-441">Możesz użyć hello wewnętrzne, bez nazwy profilu oceniania.</span><span class="sxs-lookup"><span data-stu-id="633c8-441">You can use hello internal, unnamed scoring profile.</span></span> <span data-ttu-id="633c8-442">Możesz również ustawić `defaultScoringProfile` toouse niestandardowy profil jako domyślny hello, wywoływane zawsze, gdy nie określono niestandardowego profilu na ciąg zapytania hello.</span><span class="sxs-lookup"><span data-stu-id="633c8-442">Alternatively, set `defaultScoringProfile` toouse a custom profile as hello default, invoked whenever a custom profile is not specified on hello query string.</span></span>

<span data-ttu-id="633c8-443">Zobacz [oceniania Dodaj profile tooa wyszukiwania indeksu (wyszukiwania usługi interfejsu API REST Azure)](search-api-scoring-profiles-2015-02-28-preview.md) szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="633c8-443">See [Add scoring profiles tooa search index (Azure Search Service REST API)](search-api-scoring-profiles-2015-02-28-preview.md) for details.</span></span>

<span data-ttu-id="633c8-444">**Opcje mechanizmu CORS**</span><span class="sxs-lookup"><span data-stu-id="633c8-444">**CORS Options**</span></span>

<span data-ttu-id="633c8-445">Javascript po stronie klienta nie można wywołać wszystkie interfejsy API domyślnie, ponieważ przeglądarka hello uniemożliwi wszystkich żądań cross-origin.</span><span class="sxs-lookup"><span data-stu-id="633c8-445">Client-side Javascript cannot call any APIs by default since hello browser will prevent all cross-origin requests.</span></span> <span data-ttu-id="633c8-446">Włączanie mechanizmu CORS (Cross-Origin Resource Sharing) przez ustawienie hello `corsOptions` atrybutu tooallow zapytania cross-origin tooyour indeksu.</span><span class="sxs-lookup"><span data-stu-id="633c8-446">Enable CORS (Cross-Origin Resource Sharing) by setting hello `corsOptions` attribute tooallow cross-origin queries tooyour index.</span></span> <span data-ttu-id="633c8-447">Pamiętaj tylko kwerendy interfejsów API obsługi mechanizmu CORS ze względów bezpieczeństwa.</span><span class="sxs-lookup"><span data-stu-id="633c8-447">Note that only query APIs support CORS for security reasons.</span></span> <span data-ttu-id="633c8-448">dla mechanizmu CORS można ustawić Hello następujące opcje:</span><span class="sxs-lookup"><span data-stu-id="633c8-448">hello following options can be set for CORS:</span></span>

* <span data-ttu-id="633c8-449">`allowedOrigins`(wymagane): jest to lista źródeł, które będą mieć dostępu tooyour indeksu.</span><span class="sxs-lookup"><span data-stu-id="633c8-449">`allowedOrigins` (required): This is a list of origins that will be granted access tooyour index.</span></span> <span data-ttu-id="633c8-450">To oznacza, że każdy kod Javascript pochodzący z tych źródeł będzie dozwolone tooquery indeksie (przy założeniu, zapewnia hello poprawny klucz interfejsu API).</span><span class="sxs-lookup"><span data-stu-id="633c8-450">This means that any Javascript code served from those origins will be allowed tooquery your index (assuming it provides hello correct API key).</span></span> <span data-ttu-id="633c8-451">Każde źródło ma zazwyczaj formę hello `protocol://fully-qualified-domain-name:port` mimo, że hello port jest często pomijany.</span><span class="sxs-lookup"><span data-stu-id="633c8-451">Each origin is typically of hello form `protocol://fully-qualified-domain-name:port` although hello port is often omitted.</span></span> <span data-ttu-id="633c8-452">Zobacz [w tym artykule](http://go.microsoft.com/fwlink/?LinkId=330822) więcej szczegółów.</span><span class="sxs-lookup"><span data-stu-id="633c8-452">See [this article](http://go.microsoft.com/fwlink/?LinkId=330822) for more details.</span></span>
  * <span data-ttu-id="633c8-453">Tooallow dostępu tooall źródeł, należy włączyć `*` jako pojedynczy element w hello `allowedOrigins` tablicy.</span><span class="sxs-lookup"><span data-stu-id="633c8-453">If you want tooallow access tooall origins, include `*` as a single item in hello `allowedOrigins` array.</span></span> <span data-ttu-id="633c8-454">Należy pamiętać, że **nie jest to zalecane rozwiązanie dla usługi wyszukiwania w środowisku produkcyjnym.**</span><span class="sxs-lookup"><span data-stu-id="633c8-454">Note that **this is not recommended practice for production search services.**</span></span> <span data-ttu-id="633c8-455">Jednak może być przydatne w przypadku rozwoju lub debugowania.</span><span class="sxs-lookup"><span data-stu-id="633c8-455">However, it may be useful for development or debugging purposes.</span></span>
* <span data-ttu-id="633c8-456">`maxAgeInSeconds`(opcjonalnie): przeglądarki używają tej wartości toodetermine hello czas trwania (w sekundach) toocache CORS wstępnej odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="633c8-456">`maxAgeInSeconds` (optional): Browsers use this value toodetermine hello duration (in seconds) toocache CORS preflight responses.</span></span> <span data-ttu-id="633c8-457">To musi być nieujemną liczbą całkowitą.</span><span class="sxs-lookup"><span data-stu-id="633c8-457">This must be a non-negative integer.</span></span> <span data-ttu-id="633c8-458">większe Hello jest ta wartość będzie hello lepszą wydajność, ale hello dłużej potrwa dla efektu tootake zmian zasad CORS.</span><span class="sxs-lookup"><span data-stu-id="633c8-458">hello larger this value is, hello better performance will be, but hello longer it will take for CORS policy changes tootake effect.</span></span> <span data-ttu-id="633c8-459">Jeśli nie jest ustawiona, będzie używany domyślny okres 5 minut.</span><span class="sxs-lookup"><span data-stu-id="633c8-459">If it is not set, a default duration of 5 minutes will be used.</span></span>

<span data-ttu-id="633c8-460"><a name="CreateUpdateIndexExample"></a>
**Przykład treść żądania**</span><span class="sxs-lookup"><span data-stu-id="633c8-460"><a name="CreateUpdateIndexExample"></a>
**Request Body Example**</span></span>

    {
      "name": "hotels",  
      "fields": [
        {"name": "hotelId", "type": "Edm.String", "key": true, "searchable": false},
        {"name": "baseRate", "type": "Edm.Double"},
        {"name": "description", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false},
        {"name": "description_fr", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false, "analyzer": "fr.lucene"},
        {"name": "hotelName", "type": "Edm.String"},
        {"name": "category", "type": "Edm.String"},
        {"name": "tags", "type": "Collection(Edm.String)"},
        {"name": "parkingIncluded", "type": "Edm.Boolean"},
        {"name": "smokingAllowed", "type": "Edm.Boolean"},
        {"name": "lastRenovationDate", "type": "Edm.DateTimeOffset"},
        {"name": "rating", "type": "Edm.Int32"},
        {"name": "location", "type": "Edm.GeographyPoint"}
      ],
      "suggesters": [
        {
          "name": "sg",
          "searchMode": "analyzingInfixMatching",
          "sourceFields": ["hotelName"]
        }
      ]
    }

<span data-ttu-id="633c8-461">**Odpowiedź**</span><span class="sxs-lookup"><span data-stu-id="633c8-461">**Response**</span></span>

<span data-ttu-id="633c8-462">Żądanie powiodło się: "201 utworzono".</span><span class="sxs-lookup"><span data-stu-id="633c8-462">For a successful request: "201 Created".</span></span>

<span data-ttu-id="633c8-463">Domyślnie treść odpowiedzi hello będzie zawierać hello JSON dla hello definicji indeksu, który został utworzony.</span><span class="sxs-lookup"><span data-stu-id="633c8-463">By default hello response body will contain hello JSON for hello index definition that was created.</span></span> <span data-ttu-id="633c8-464">Jeśli hello `Prefer` nagłówek żądania jest ustawiona zbyt`return=minimal`, treść odpowiedzi hello będzie pusty i będzie kod stanu Powodzenie hello "204 żadnej zawartości" zamiast "201 utworzono".</span><span class="sxs-lookup"><span data-stu-id="633c8-464">If hello `Prefer` request header is set too`return=minimal`, hello response body will be empty and hello success status code will be "204 No Content" instead of "201 Created".</span></span> <span data-ttu-id="633c8-465">Dotyczy to niezależnie od tego, czy PUT lub POST była używana toocreate hello indeksu.</span><span class="sxs-lookup"><span data-stu-id="633c8-465">This is true regardless of whether PUT or POST was used toocreate hello index.</span></span>

<span data-ttu-id="633c8-466">**Uwagi**</span><span class="sxs-lookup"><span data-stu-id="633c8-466">**Remarks**</span></span>

<span data-ttu-id="633c8-467">Obecnie jest ograniczona obsługa aktualizacji schematu indeksu.</span><span class="sxs-lookup"><span data-stu-id="633c8-467">Currently, there is limited support for index schema updates.</span></span> <span data-ttu-id="633c8-468">Obecnie nie są obsługiwane żadne aktualizacje schematu, które wymagają ponownego indeksowania, np. zmiany typów pól.</span><span class="sxs-lookup"><span data-stu-id="633c8-468">Any schema updates that would require re-indexing such as changing field types are not currently supported.</span></span> <span data-ttu-id="633c8-469">Mimo że istniejących pól nie można zmienić ani usunąć, dodawać nowe pola można tooan istniejący indeks w dowolnym momencie.</span><span class="sxs-lookup"><span data-stu-id="633c8-469">Although existing fields cannot be changed or deleted, new fields can be added tooan existing index at any time.</span></span> <span data-ttu-id="633c8-470">Po dodaniu nowego pola, wszystkie istniejące dokumenty w indeksie hello automatycznie ma wartość null dla tego pola.</span><span class="sxs-lookup"><span data-stu-id="633c8-470">When a new field is added, all existing documents in hello index will automatically have a null value for that field.</span></span> <span data-ttu-id="633c8-471">Nie dodatkowego miejsca będą działały dopóki indeks toohello dodaniu nowych dokumentów.</span><span class="sxs-lookup"><span data-stu-id="633c8-471">No additional storage space will be consumed until new documents are added toohello index.</span></span>

<a name="Suggesters"></a>

## <a name="suggesters"></a><span data-ttu-id="633c8-472">Funkcje sugestii</span><span class="sxs-lookup"><span data-stu-id="633c8-472">Suggesters</span></span>
<span data-ttu-id="633c8-473">Funkcja sugestie Hello w usłudze Azure Search jest możliwość wpisywaniu lub Autouzupełnianie zapytań, podając listę potencjalnych terminy wyszukiwania w odpowiedzi toopartial ciągu dane wejściowe wprowadzona w polu wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="633c8-473">hello suggestions feature in Azure Search is a type-ahead or auto-complete query capability, providing a list of potential search terms in response toopartial string inputs entered into a search box.</span></span> <span data-ttu-id="633c8-474">Można zauważyć zapytań korzystając z wyszukiwarki komercyjnych sieci web: wpisz ".NET" w usłudze Bing tworzy listę terminologii ".NET 4.5", ".NET Framework 3,5" itd.</span><span class="sxs-lookup"><span data-stu-id="633c8-474">You've probably noticed query suggestions when using commercial web search engines: typing ".NET" in Bing produces a list of terms for ".NET 4.5", ".NET Framework 3.5", and so forth.</span></span> <span data-ttu-id="633c8-475">Korzystając z interfejsu API REST usługi wyszukiwania hello, implementacja sugestie w niestandardowych aplikacji usługi Azure Search wymaga następujących hello:</span><span class="sxs-lookup"><span data-stu-id="633c8-475">When using hello Search service REST API, implementing suggestions in a custom Azure Search application requires hello following:</span></span>

* <span data-ttu-id="633c8-476">Włączanie sugestie przez dodanie **sugestora** konstrukcji w indeksie, podając nazwę hello, tryb wyszukiwania i Lista pól, dla którego wpisywaniu jest wywoływany.</span><span class="sxs-lookup"><span data-stu-id="633c8-476">Enable suggestions by adding a **suggester** construction in your index, giving hello name, search mode, and a list of fields for which type-ahead is invoked.</span></span> <span data-ttu-id="633c8-477">Na przykład jeśli określisz "Nazwa_miasta" jako pola źródłowego, wpisując ciąg wyszukiwania częściowej "Sea" spowoduje "Seattle", "Bocznej" i "Seatac" (wszystkie trzy nazwy miast rzeczywiste) oferowane jako użytkownik toohello sugestie dotyczące zapytań.</span><span class="sxs-lookup"><span data-stu-id="633c8-477">For example, if you specify "cityName" as a source field, typing a partial search string of "Sea" will result in "Seattle", "Seaside", and "Seatac" (all three are actual city names) offered up as query suggestions toohello user.</span></span>
* <span data-ttu-id="633c8-478">Wywołanie przez wywołanie hello sugestie [API sugestie](#Suggestions) w kodzie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="633c8-478">Invoke suggestions by calling hello [Suggestions API](#Suggestions) in your application code.</span></span> <span data-ttu-id="633c8-479">Zwykle ciągi częściowe wyszukiwania są wysyłane toohello usługi podczas użytkownika hello pisze zapytania wyszukiwania, a ten interfejs API zwraca zestaw sugerowane wyrażeń.</span><span class="sxs-lookup"><span data-stu-id="633c8-479">Typically partial search strings are sent toohello service while hello user is typing a search query, and this API returns a set of suggested phrases.</span></span>

<span data-ttu-id="633c8-480">W tym artykule opisano sposób tooconfigure **sugestora**.</span><span class="sxs-lookup"><span data-stu-id="633c8-480">This article explains how tooconfigure a **suggester**.</span></span> <span data-ttu-id="633c8-481">Należy także przejrzeć hello [API sugestie](#Suggestions) szczegółowe informacje dotyczące sposobu używania sugestora.</span><span class="sxs-lookup"><span data-stu-id="633c8-481">You should also review hello [Suggestions API](#Suggestions) for details on how a suggester is used.</span></span>

<span data-ttu-id="633c8-482">**Użycie**</span><span class="sxs-lookup"><span data-stu-id="633c8-482">**Usage**</span></span>

<span data-ttu-id="633c8-483">`Suggesters`są tworzone w indeksie hello i działają najlepiej, gdy używane toosuggest określonych dokumentów zamiast utracić warunki ani fraz.</span><span class="sxs-lookup"><span data-stu-id="633c8-483">`Suggesters` are created in hello index and work best when used toosuggest specific documents rather than loose terms or phrases.</span></span> <span data-ttu-id="633c8-484">najlepsze pola candidate Hello są tytuły, nazwy i inne stosunkowo zwroty identyfikujące element.</span><span class="sxs-lookup"><span data-stu-id="633c8-484">hello best candidate fields are titles, names, and other relatively short phrases that can identify an item.</span></span> <span data-ttu-id="633c8-485">Są mniej skuteczne powtarzających się pola, takie jak kategorie i tagi, lub bardzo dużo pól, np. pola opisy lub komentarzy.</span><span class="sxs-lookup"><span data-stu-id="633c8-485">Less effective are repetitive fields, such as categories and tags, or very long fields such as descriptions or comments fields.</span></span>

<span data-ttu-id="633c8-486">W ramach definicji indeksu hello, możesz dodać toohello pojedynczego sugestora `suggesters` kolekcji.</span><span class="sxs-lookup"><span data-stu-id="633c8-486">As part of hello index definition, you can add a single suggester toohello `suggesters` collection.</span></span> <span data-ttu-id="633c8-487">Właściwości, które definiują sugestora Uwzględnij hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="633c8-487">Properties that define a suggester include hello following:</span></span>

* <span data-ttu-id="633c8-488">`name`: hello nazwę sugestora hello.</span><span class="sxs-lookup"><span data-stu-id="633c8-488">`name`: hello name of hello suggester.</span></span> <span data-ttu-id="633c8-489">Użyj hello nazwę sugestora hello podczas wywoływania metody hello `suggest` interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="633c8-489">You use hello name of hello suggester when calling hello `suggest` API.</span></span>
* <span data-ttu-id="633c8-490">`searchMode`: hello toosearch strategia używana do fraz kandydujących.</span><span class="sxs-lookup"><span data-stu-id="633c8-490">`searchMode`: hello strategy used toosearch for candidate phrases.</span></span> <span data-ttu-id="633c8-491">Witaj jedyny obecnie obsługiwany tryb to `analyzingInfixMatching`, który przeprowadza elastyczne dopasowywanie fraz na początku hello lub w środku zdań hello.</span><span class="sxs-lookup"><span data-stu-id="633c8-491">hello only mode currently supported is `analyzingInfixMatching`, which performs flexible matching of phrases at hello beginning or in hello middle of sentences.</span></span>
* <span data-ttu-id="633c8-492">`sourceFields`: Lista jednego lub więcej pól, które są hello źródło zawartości hello sugestie.</span><span class="sxs-lookup"><span data-stu-id="633c8-492">`sourceFields`: A list of one or more fields that are hello source of hello content for suggestions.</span></span> <span data-ttu-id="633c8-493">Tylko pola typu `Edm.String` i `Collection(Edm.String)` mogą być sugestie dotyczące źródeł.</span><span class="sxs-lookup"><span data-stu-id="633c8-493">Only fields of type `Edm.String` and `Collection(Edm.String)` may be sources for suggestions.</span></span> <span data-ttu-id="633c8-494">Można tylko pola, które nie mają niestandardowego analizatora języków ustawić.</span><span class="sxs-lookup"><span data-stu-id="633c8-494">Only fields that don't have a custom language analyzer set can be used.</span></span>

<span data-ttu-id="633c8-495">**Przykład sugestora**</span><span class="sxs-lookup"><span data-stu-id="633c8-495">**Suggester Example**</span></span>

<span data-ttu-id="633c8-496">Sugestora jest częścią indeksu hello.</span><span class="sxs-lookup"><span data-stu-id="633c8-496">A suggester is part of hello index.</span></span> <span data-ttu-id="633c8-497">Może istnieć tylko jeden sugestora hello `suggesters` kolekcji w bieżącej wersji hello obok hello pola kolekcji i `scoringProfiles`.</span><span class="sxs-lookup"><span data-stu-id="633c8-497">Only one suggester can exist in hello `suggesters` collection in hello current version, alongside hello fields collection and `scoringProfiles`.</span></span>

        {
          "name": "hotels",
          "fields": [
             . . .
           ],
          "suggesters": [
            {
            "name": "sg",
            "searchMode": "analyzingInfixMatching",
            "sourceFields: ["hotelName", "category"]
            }
          ],
          "scoringProfiles": [
             . . .
          ]
        }

> [!NOTE]
> <span data-ttu-id="633c8-498">Jeśli używana wersja hello publicznej wersji zapoznawczej usługi Azure Search `suggesters` zastępuje starsze właściwości typu boolean (`"suggestions": false`) sugestie prefiks która obsługiwana tylko dla ciągów krótkich (3-25 znaków).</span><span class="sxs-lookup"><span data-stu-id="633c8-498">If you used hello public preview version of Azure Search, `suggesters` replaces an older boolean property (`"suggestions": false`) that only supported prefix suggestions for short strings (3-25 characters).</span></span> <span data-ttu-id="633c8-499">Jego zastąpienia `suggesters`, obsługuje element infiksu wyszukującą pasujących terminów hello początku lub w środku hello zawartość pola z lepszą tolerancji błędów w ciągów wyszukiwania dopasowania.</span><span class="sxs-lookup"><span data-stu-id="633c8-499">Its replacement, `suggesters`, supports infix matching that finds matching terms at hello beginning or in hello middle of field content, with better tolerance for mistakes in search strings.</span></span> <span data-ttu-id="633c8-500">Począwszy od wersji ogólnie dostępna hello, jest teraz hello tylko implementacja sugestie hello interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="633c8-500">Starting with hello generally available release, this is now hello only implementation of hello suggestions API.</span></span> <span data-ttu-id="633c8-501">Witaj starsze `suggestions` właściwość, która została wprowadzona w systemie `api-version=2014-07-31-Preview` nadal toowork w tej wersji, ale nie działa w hello `2015-02-28` lub nowsze wersje usługi Azure Search.</span><span class="sxs-lookup"><span data-stu-id="633c8-501">hello older `suggestions` property that was introduced in `api-version=2014-07-31-Preview` continues toowork in that version, but is not operational in hello `2015-02-28` or later versions of Azure Search.</span></span>
> 
> 

<a name="UpdateIndex"></a>

## <a name="update-index"></a><span data-ttu-id="633c8-502">Aktualizuj indeks</span><span class="sxs-lookup"><span data-stu-id="633c8-502">Update Index</span></span>
<span data-ttu-id="633c8-503">Możesz zaktualizować istniejący indeks w usłudze Azure Search za pomocą żądania HTTP PUT.</span><span class="sxs-lookup"><span data-stu-id="633c8-503">You can update an existing index within Azure Search using an HTTP PUT request.</span></span> <span data-ttu-id="633c8-504">Aktualizacje mogą obejmować dodawanie nowych pól toohello istniejącego schematu, modyfikowanie opcji mechanizmu CORS i modyfikowanie oceniania profile.</span><span class="sxs-lookup"><span data-stu-id="633c8-504">Updates can include adding new fields toohello existing schema, modifying CORS options, and modifying scoring profiles.</span></span> <span data-ttu-id="633c8-505">Zobacz [dodać oceniania profile](https://msdn.microsoft.com/library/azure/dn798928.aspx) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="633c8-505">See [Add scoring Profiles](https://msdn.microsoft.com/library/azure/dn798928.aspx) for more information.</span></span> <span data-ttu-id="633c8-506">Należy określić nazwę hello tooupdate indeksu hello na powitania identyfikatora URI żądania:</span><span class="sxs-lookup"><span data-stu-id="633c8-506">You specify hello name of hello index tooupdate on hello request URI:</span></span>

    PUT https://[search service url]/indexes/[index name]?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

<span data-ttu-id="633c8-507">**Ważne:** toooperations ograniczone, które nie wymagają odbudowanie indeksu wyszukiwania hello jest obsługa aktualizacji schematu indeksu.</span><span class="sxs-lookup"><span data-stu-id="633c8-507">**Important:** Support for index schema updates is limited toooperations that don't require rebuilding hello search index.</span></span> <span data-ttu-id="633c8-508">Obecnie nie są obsługiwane żadne aktualizacje schematu, które wymagają ponownego indeksowania, np. zmiany typów pól.</span><span class="sxs-lookup"><span data-stu-id="633c8-508">Any schema updates that would require re-indexing, such as changing field types, are not currently supported.</span></span> <span data-ttu-id="633c8-509">W dowolnym momencie można dodawać nowe pola, mimo że nie należy modyfikować ani usuwać istniejących pól.</span><span class="sxs-lookup"><span data-stu-id="633c8-509">New fields can be added at any time, although existing fields cannot be changed or deleted.</span></span> <span data-ttu-id="633c8-510">Witaj dotyczy to również zbyt`suggesters`.</span><span class="sxs-lookup"><span data-stu-id="633c8-510">hello same applies too`suggesters`.</span></span> <span data-ttu-id="633c8-511">Można dodawać nowe pola, sugestora tooa w polach hello czasu hello zostaną dodane, ale nie można usunąć pola z `suggesters` i nie można dodać pól istniejących zbyt`suggesters`.</span><span class="sxs-lookup"><span data-stu-id="633c8-511">New fields may be added tooa suggester at hello time hello fields are added, but fields cannot be removed from `suggesters` and existing fields cannot be added too`suggesters`.</span></span>

<span data-ttu-id="633c8-512">Podczas dodawania nowego indeksu tooan pola, wszystkie istniejące dokumenty w indeksie hello automatycznie ma wartość null dla tego pola.</span><span class="sxs-lookup"><span data-stu-id="633c8-512">When adding a new field tooan index, all existing documents in hello index will automatically have a null value for that field.</span></span> <span data-ttu-id="633c8-513">Nie dodatkowego miejsca będą działały dopóki indeks toohello dodaniu nowych dokumentów.</span><span class="sxs-lookup"><span data-stu-id="633c8-513">No additional storage space will be consumed until new documents are added toohello index.</span></span>

<span data-ttu-id="633c8-514">**Żądanie**</span><span class="sxs-lookup"><span data-stu-id="633c8-514">**Request**</span></span>

<span data-ttu-id="633c8-515">HTTPS jest wymagana dla wszystkich żądań obsługi.</span><span class="sxs-lookup"><span data-stu-id="633c8-515">HTTPS is required for all service requests.</span></span> <span data-ttu-id="633c8-516">Witaj **Aktualizuj indeks** żądania jest tworzony przy użyciu HTTP PUT.</span><span class="sxs-lookup"><span data-stu-id="633c8-516">hello **Update Index** request is constructed using HTTP PUT.</span></span> <span data-ttu-id="633c8-517">Z PUT nazwę indeksu hello jest częścią hello adresu URL.</span><span class="sxs-lookup"><span data-stu-id="633c8-517">With PUT, hello index name is part of hello URL.</span></span> <span data-ttu-id="633c8-518">Jeśli indeks hello nie istnieje, jest tworzony.</span><span class="sxs-lookup"><span data-stu-id="633c8-518">If hello index doesn't exist, it is created.</span></span> <span data-ttu-id="633c8-519">Jeśli istnieje już indeks hello, jest nowa definicja toohello zaktualizowane.</span><span class="sxs-lookup"><span data-stu-id="633c8-519">If hello index already exists, it is updated toohello new definition.</span></span>

<span data-ttu-id="633c8-520">Nazwa indeksu Hello musi zawierać małe litery, zaczynać się literą lub cyfrą nie ukośniki lub kropki i mniej niż 128 znaków.</span><span class="sxs-lookup"><span data-stu-id="633c8-520">hello index name must be lower case, start with a letter or number, have no slashes or dots, and be less than 128 characters.</span></span> <span data-ttu-id="633c8-521">Po uruchomieniu nazwę indeksu hello literą lub cyfrą hello reszty hello nazwa może zawierać żadnych list, numer i kreski, tak długo, jak hello łączniki nie są kolejne.</span><span class="sxs-lookup"><span data-stu-id="633c8-521">After starting hello index name with a letter or number, hello rest of hello name can include any letter, number and dashes, as long as hello dashes are not consecutive.</span></span>

<span data-ttu-id="633c8-522">`api-version=[string]`(wymagane).</span><span class="sxs-lookup"><span data-stu-id="633c8-522">`api-version=[string]` (required).</span></span> <span data-ttu-id="633c8-523">Wersja zapoznawcza Hello jest `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="633c8-523">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="633c8-524">Zobacz [przechowywanie wersji usługi wyszukiwania](http://msdn.microsoft.com/library/azure/dn864560.aspx) szczegółowe informacje i alternatywne wersje.</span><span class="sxs-lookup"><span data-stu-id="633c8-524">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="633c8-525">**Nagłówki żądania**</span><span class="sxs-lookup"><span data-stu-id="633c8-525">**Request Headers**</span></span>

<span data-ttu-id="633c8-526">powitania po liście opisano hello wymagane i opcjonalne żądania nagłówków.</span><span class="sxs-lookup"><span data-stu-id="633c8-526">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="633c8-527">`Content-Type`: Wymagane.</span><span class="sxs-lookup"><span data-stu-id="633c8-527">`Content-Type`: Required.</span></span> <span data-ttu-id="633c8-528">Ustaw tę wartość za`application/json`</span><span class="sxs-lookup"><span data-stu-id="633c8-528">Set this too`application/json`</span></span>
* <span data-ttu-id="633c8-529">`api-key`: Wymagane.</span><span class="sxs-lookup"><span data-stu-id="633c8-529">`api-key`: Required.</span></span> <span data-ttu-id="633c8-530">Witaj `api-key` jest używane tooauthenticate hello żądania tooyour usługi wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="633c8-530">hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="633c8-531">Jest to wartość ciągu, usługa tooyour unikatowy.</span><span class="sxs-lookup"><span data-stu-id="633c8-531">It is a string value, unique tooyour service.</span></span> <span data-ttu-id="633c8-532">Witaj **Aktualizuj indeks** żądanie musi zawierać `api-key` nagłówka ustawić tooyour klucza administratora (jako klucz zapytania tooa min.).</span><span class="sxs-lookup"><span data-stu-id="633c8-532">hello **Update Index** request must include an `api-key` header set tooyour admin key (as opposed tooa query key).</span></span>

<span data-ttu-id="633c8-533">Należy również adres URL hello usługi nazwa tooconstruct hello żądania.</span><span class="sxs-lookup"><span data-stu-id="633c8-533">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="633c8-534">Można uzyskać nazwy usługi hello i `api-key` z pulpitu nawigacyjnego usługi w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="633c8-534">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="633c8-535">Zobacz [Tworzenie usługi Azure Search w portalu hello](search-create-service-portal.md) dla pomocy nawigacji strony.</span><span class="sxs-lookup"><span data-stu-id="633c8-535">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="633c8-536">**Składnia treść żądania**</span><span class="sxs-lookup"><span data-stu-id="633c8-536">**Request Body Syntax**</span></span>

<span data-ttu-id="633c8-537">Podczas aktualizowania istniejący indeks, treści hello musi zawierać hello oryginalnej definicji schematu, a także hello nowe pola, które dodajesz, a także hello zmodyfikowane oceniania profile, sugestorów i opcje CORS, ile.</span><span class="sxs-lookup"><span data-stu-id="633c8-537">When updating an existing index, hello body must include hello original schema definition, plus hello new fields you are adding, as well as hello modified scoring profiles, suggesters and CORS options, if any.</span></span> <span data-ttu-id="633c8-538">W przypadku modyfikowania nie hello oceniania profilów i opcji CORS, musi zawierać oryginału powitania od utworzenia indeksu hello.</span><span class="sxs-lookup"><span data-stu-id="633c8-538">If you are not modifying hello scoring profiles and CORS options, you must include hello originals from when hello index was created.</span></span> <span data-ttu-id="633c8-539">Ogólnie rzecz biorąc hello najlepsze wzorzec toouse aktualizacji jest definicja indeksu hello tooretrieve pobieranie, zmodyfikuj go, a następnie go zaktualizować z użyciem PUT.</span><span class="sxs-lookup"><span data-stu-id="633c8-539">In general hello best pattern toouse for updates is tooretrieve hello index definition with a GET, modify it, then update it with PUT.</span></span>

<span data-ttu-id="633c8-540">Składnia schematu Hello używana toocreate, który indeks jest przedstawiony tutaj dla wygody.</span><span class="sxs-lookup"><span data-stu-id="633c8-540">hello schema syntax used toocreate an index is reproduced here for convenience.</span></span> <span data-ttu-id="633c8-541">Zobacz [Create Index](#CreateIndex) więcej szczegółów.</span><span class="sxs-lookup"><span data-stu-id="633c8-541">See [Create Index](#CreateIndex) for more details.</span></span>

    {
      "name": (optional) "name_of_index",
      "fields": [
        {
          "name": "name_of_field",
          "type": "Edm.String | Collection(Edm.String) | Edm.Int32 | Edm.Int64 | Edm.Double | Edm.Boolean | Edm.DateTimeOffset | Edm.GeographyPoint",
          "searchable": true (default where applicable) | false (only Edm.String and Collection(Edm.String) fields can be searchable),
          "filterable": true (default) | false,
          "sortable": true (default where applicable) | false (Collection(Edm.String) fields cannot be sortable),
          "facetable": true (default where applicable) | false (Edm.GeographyPoint fields cannot be facetable),
          "key": true | false (default, only Edm.String fields can be keys),
          "retrievable": true (default) | false, 
          "analyzer": "name of hello analyzer used for search and indexing", (only if 'searchAnalyzer' and 'indexAnalyzer' are not set)
          "searchAnalyzer": "name of hello search analyzer", (only if 'indexAnalyzer' is set and 'analyzer' is not set)
          "indexAnalyzer": "name of hello indexing analyzer" (only if 'searchAnalyzer' is set and 'analyzer' is not set)
        }
      ],
      "suggesters": [
        {
          "name": "name of suggester",
          "searchMode": "analyzingInfixMatching" (other modes may be added in hello future),
          "sourceFields": ["field1", "field2", ...]
        }
      ],
      "scoringProfiles": [
        {
          "name": "name of scoring profile",
          "text": (optional, only applies toosearchable fields) {
            "weights": {
              "searchable_field_name": relative_weight_value (positive numbers),
              ...
            }
          },
          "functions": (optional) [
            {
              "type": "magnitude | freshness | distance | tag",
              "boost": # (positive number used as multiplier for raw score != 1),
              "fieldName": "...",
              "interpolation": "constant | linear (default) | quadratic | logarithmic",
              "magnitude": {
                "boostingRangeStart": #,
                "boostingRangeEnd": #,
                "constantBoostBeyondRange": true | false (default)
              },
              "freshness": {
                "boostingDuration": "..." (value representing timespan leading toonow over which boosting occurs)
              },
              "distance": {
                "referencePointParameter": "...", (parameter toobe passed in queries toouse as reference location, see "scoringParameter" for syntax details)
                "boostingDistance": # (hello distance in kilometers from hello reference location where hello boosting range ends)
              },
              "tag": {
                "tagsParameter": "..." (parameter toobe passed in queries toospecify list of tags toocompare against target field, see "scoringParameter" for syntax details)
              }
            }
          ],
          "functionAggregation": (optional, applies only when functions are specified)
            "sum (default) | average | minimum | maximum | firstMatching"
        }
      ],
      "analyzers":(optional)[ ... ],
      "charFilters":(optional)[ ... ],
      "tokenizers":(optional)[ ... ],
      "tokenFilters":(optional)[ ... ],
      "defaultScoringProfile": (optional) "...",
      "corsOptions": (optional) {
        "allowedOrigins": ["*"] | ["origin_1", "origin_2", ...],
        "maxAgeInSeconds": (optional) max_age_in_seconds (non-negative integer)
      }
    }


<span data-ttu-id="633c8-542">**Odpowiedź**</span><span class="sxs-lookup"><span data-stu-id="633c8-542">**Response**</span></span>

<span data-ttu-id="633c8-543">Żądanie powiodło się: "204 żadna zawartość".</span><span class="sxs-lookup"><span data-stu-id="633c8-543">For a successful request: "204 No Content".</span></span>

<span data-ttu-id="633c8-544">Domyślnie hello treść odpowiedzi jest pusta.</span><span class="sxs-lookup"><span data-stu-id="633c8-544">By default hello response body will be empty.</span></span> <span data-ttu-id="633c8-545">Jednakże, jeżeli hello `Prefer` nagłówek żądania jest ustawiona zbyt`return=representation`, treść odpowiedzi hello będzie zawierać hello JSON dla hello definicji indeksu, który został zaktualizowany.</span><span class="sxs-lookup"><span data-stu-id="633c8-545">However, if hello `Prefer` request header is set too`return=representation`, hello response body will contain hello JSON for hello index definition that was updated.</span></span> <span data-ttu-id="633c8-546">W takim przypadku zostanie kod stanu Powodzenie hello "200 OK".</span><span class="sxs-lookup"><span data-stu-id="633c8-546">In this case, hello success status code will be "200 OK".</span></span>

<span data-ttu-id="633c8-547">**Aktualizowanie definicji indeksu za pomocą analizatorów niestandardowych**</span><span class="sxs-lookup"><span data-stu-id="633c8-547">**Updating index definition with custom analyzers**</span></span>

<span data-ttu-id="633c8-548">Po zdefiniowaniu jest analyzer, tokenizatora, token filtr lub filtr char, nie można modyfikować.</span><span class="sxs-lookup"><span data-stu-id="633c8-548">Once an analyzer, a tokenizer, a token filter or a char filter is defined, it cannot be modified.</span></span> <span data-ttu-id="633c8-549">Nowe można dodać istniejący indeks tooan tylko wtedy, gdy hello `allowIndexDowntime` flagę tootrue w żądaniu aktualizacji indeksu hello:</span><span class="sxs-lookup"><span data-stu-id="633c8-549">New ones can be added tooan existing index only if hello `allowIndexDowntime` flag is set tootrue in hello index update request:</span></span> 

`PUT https://[search service name].search.windows.net/indexes/[index name]?api-version=[api-version]&allowIndexDowntime=true`

<span data-ttu-id="633c8-550">Uwaga tej operacji zostanie umieszczone indeksu w trybie offline dla co najmniej kilka sekund, powodując Twojej indeksowanie i zapytania żądania toofail.</span><span class="sxs-lookup"><span data-stu-id="633c8-550">Note that this operation will put your index offline for at least a few seconds, causing your indexing and query requests toofail.</span></span> <span data-ttu-id="633c8-551">Wydajność i zapisu dostępności indeksu hello może być ograniczony na kilka minut po zaktualizowaniu indeksu hello lub dłużej dla bardzo dużych indeksów.</span><span class="sxs-lookup"><span data-stu-id="633c8-551">Performance and write availability of hello index can be impaired for several minutes after hello index is updated, or longer for very large indexes.</span></span>

<a name="ListIndexes"></a>

## <a name="list-indexes"></a><span data-ttu-id="633c8-552">Listy indeksów</span><span class="sxs-lookup"><span data-stu-id="633c8-552">List Indexes</span></span>
<span data-ttu-id="633c8-553">Witaj **listy indeksów** operacji zwraca listę indeksów hello obecnie w usłudze Azure Search.</span><span class="sxs-lookup"><span data-stu-id="633c8-553">hello **List Indexes** operation returns a list of hello indexes currently in your Azure Search service.</span></span>

    GET https://[service name].search.windows.net/indexes?api-version=[api-version]
    api-key: [admin key]

<span data-ttu-id="633c8-554">**Żądanie**</span><span class="sxs-lookup"><span data-stu-id="633c8-554">**Request**</span></span>

<span data-ttu-id="633c8-555">HTTPS jest wymagana dla wszystkich żądań obsługi.</span><span class="sxs-lookup"><span data-stu-id="633c8-555">HTTPS is required for all service requests.</span></span> <span data-ttu-id="633c8-556">Witaj **listy indeksów** żądania można skonstruować przy użyciu metody GET hello.</span><span class="sxs-lookup"><span data-stu-id="633c8-556">hello **List Indexes** request can be constructed using hello GET method.</span></span>

<span data-ttu-id="633c8-557">`api-version=[string]`(wymagane).</span><span class="sxs-lookup"><span data-stu-id="633c8-557">`api-version=[string]` (required).</span></span> <span data-ttu-id="633c8-558">Wersja zapoznawcza Hello jest `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="633c8-558">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="633c8-559">Zobacz [przechowywanie wersji usługi wyszukiwania](http://msdn.microsoft.com/library/azure/dn864560.aspx) szczegółowe informacje i alternatywne wersje.</span><span class="sxs-lookup"><span data-stu-id="633c8-559">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="633c8-560">**Nagłówki żądania**</span><span class="sxs-lookup"><span data-stu-id="633c8-560">**Request Headers**</span></span>

<span data-ttu-id="633c8-561">powitania po liście opisano hello wymagane i opcjonalne żądania nagłówków.</span><span class="sxs-lookup"><span data-stu-id="633c8-561">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="633c8-562">`api-key`: Wymagane.</span><span class="sxs-lookup"><span data-stu-id="633c8-562">`api-key`: Required.</span></span> <span data-ttu-id="633c8-563">Witaj `api-key` jest używane tooauthenticate hello żądania tooyour usługi wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="633c8-563">hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="633c8-564">Jest to wartość ciągu, usługa tooyour unikatowy.</span><span class="sxs-lookup"><span data-stu-id="633c8-564">It is a string value, unique tooyour service.</span></span> <span data-ttu-id="633c8-565">Witaj **listy indeksów** żądanie musi zawierać `api-key` klucz administratora tooan zestawu (jako klucz zapytania min. tooa).</span><span class="sxs-lookup"><span data-stu-id="633c8-565">hello **List Indexes** request must include an `api-key` set tooan admin key (as opposed tooa query key).</span></span>

<span data-ttu-id="633c8-566">Należy również adres URL hello usługi nazwa tooconstruct hello żądania.</span><span class="sxs-lookup"><span data-stu-id="633c8-566">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="633c8-567">Można uzyskać nazwy usługi hello i `api-key` z pulpitu nawigacyjnego usługi w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="633c8-567">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="633c8-568">Zobacz [Tworzenie usługi Azure Search w portalu hello](search-create-service-portal.md) dla pomocy nawigacji strony.</span><span class="sxs-lookup"><span data-stu-id="633c8-568">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="633c8-569">**Treść żądania**</span><span class="sxs-lookup"><span data-stu-id="633c8-569">**Request Body**</span></span>

<span data-ttu-id="633c8-570">Brak.</span><span class="sxs-lookup"><span data-stu-id="633c8-570">None.</span></span>

<span data-ttu-id="633c8-571">**Odpowiedź**</span><span class="sxs-lookup"><span data-stu-id="633c8-571">**Response**</span></span>

<span data-ttu-id="633c8-572">Kod stanu: 200 OK jest zwracana dla pomyślnej odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="633c8-572">Status Code: 200 OK is returned for a successful response.</span></span>

<span data-ttu-id="633c8-573">Oto przykład treści odpowiedzi:</span><span class="sxs-lookup"><span data-stu-id="633c8-573">Here is an example response body:</span></span>

    {
      "value": [
        {
          "name": "Books",
          "fields": [
            {"name": "ISBN", ...},
            ...
          ]
        },
        {
          "name": "Games",
          ...
        },
        ...
      ]
    }

<span data-ttu-id="633c8-574">Należy pamiętać, filtrować odpowiedź hello toojust hello właściwości, które interesują Cię w dół.</span><span class="sxs-lookup"><span data-stu-id="633c8-574">Note that you can filter hello response down toojust hello properties you're interested in.</span></span> <span data-ttu-id="633c8-575">Na przykład, jeśli chcesz tylko listę nazw indeksów, użyj hello OData `$select` opcji zapytania:</span><span class="sxs-lookup"><span data-stu-id="633c8-575">For example, if you want only a list of index names, use hello OData `$select` query option:</span></span>

    GET /indexes?api-version=2015-02-28-Preview&$select=name

<span data-ttu-id="633c8-576">W takim przypadku hello odpowiedzi z hello powyżej przykład będzie wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="633c8-576">In this case, hello response from hello above example would appear as follows:</span></span>

    {
      "value": [
        {"name": "Books"},
        {"name": "Games"},
        ...
      ]
    }

<span data-ttu-id="633c8-577">Jest przepustowości toosave technika przydatne, jeśli masz wiele indeksów w swojej usłudze wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="633c8-577">This is a useful technique toosave bandwidth if you have a lot of indexes in your Search service.</span></span>

<a name="GetIndex"></a>

## <a name="get-index"></a><span data-ttu-id="633c8-578">Pobierz indeksu</span><span class="sxs-lookup"><span data-stu-id="633c8-578">Get Index</span></span>
<span data-ttu-id="633c8-579">Witaj **uzyskać indeks** operacji definicji indeksu hello są pobierane z usługi Azure Search.</span><span class="sxs-lookup"><span data-stu-id="633c8-579">hello **Get Index** operation gets hello index definition from Azure Search.</span></span>

    GET https://[service name].search.windows.net/indexes/[index name]?api-version=[api-version]
    api-key: [admin key]

<span data-ttu-id="633c8-580">**Żądanie**</span><span class="sxs-lookup"><span data-stu-id="633c8-580">**Request**</span></span>

<span data-ttu-id="633c8-581">HTTPS jest wymagana dla żądań obsługi.</span><span class="sxs-lookup"><span data-stu-id="633c8-581">HTTPS is required for service requests.</span></span> <span data-ttu-id="633c8-582">Witaj **uzyskać indeks** żądania można skonstruować przy użyciu metody GET hello.</span><span class="sxs-lookup"><span data-stu-id="633c8-582">hello **Get Index** request can be constructed using hello GET method.</span></span>

<span data-ttu-id="633c8-583">hello [Nazwa indeksu] w identyfikatorze URI żądania hello Określa, które tooreturn indeksu z kolekcji indeksów hello.</span><span class="sxs-lookup"><span data-stu-id="633c8-583">hello [index name] in hello request URI specifies which index tooreturn from hello indexes collection.</span></span>

<span data-ttu-id="633c8-584">`api-version=[string]`(wymagane).</span><span class="sxs-lookup"><span data-stu-id="633c8-584">`api-version=[string]` (required).</span></span> <span data-ttu-id="633c8-585">Wersja zapoznawcza Hello jest `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="633c8-585">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="633c8-586">Zobacz [przechowywanie wersji usługi wyszukiwania](http://msdn.microsoft.com/library/azure/dn864560.aspx) szczegółowe informacje i alternatywne wersje.</span><span class="sxs-lookup"><span data-stu-id="633c8-586">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="633c8-587">**Nagłówki żądania**</span><span class="sxs-lookup"><span data-stu-id="633c8-587">**Request Headers**</span></span>

<span data-ttu-id="633c8-588">powitania po liście opisano hello wymagane i opcjonalne żądania nagłówków.</span><span class="sxs-lookup"><span data-stu-id="633c8-588">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="633c8-589">`api-key`: hello `api-key` jest używane tooauthenticate hello żądania tooyour usługi wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="633c8-589">`api-key`: hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="633c8-590">Jest to wartość ciągu, usługa tooyour unikatowy.</span><span class="sxs-lookup"><span data-stu-id="633c8-590">It is a string value, unique tooyour service.</span></span> <span data-ttu-id="633c8-591">Witaj **uzyskać indeks** żądanie musi zawierać `api-key` klucz administratora tooan zestawu (jako klucz zapytania min. tooa).</span><span class="sxs-lookup"><span data-stu-id="633c8-591">hello **Get Index** request must include an `api-key` set tooan admin key (as opposed tooa query key).</span></span>

<span data-ttu-id="633c8-592">Należy również adres URL hello usługi nazwa tooconstruct hello żądania.</span><span class="sxs-lookup"><span data-stu-id="633c8-592">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="633c8-593">Można uzyskać nazwy usługi hello i `api-key` z pulpitu nawigacyjnego usługi w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="633c8-593">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="633c8-594">Zobacz [Tworzenie usługi Azure Search w portalu hello](search-create-service-portal.md) dla pomocy nawigacji strony.</span><span class="sxs-lookup"><span data-stu-id="633c8-594">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="633c8-595">**Treść żądania**</span><span class="sxs-lookup"><span data-stu-id="633c8-595">**Request Body**</span></span>

<span data-ttu-id="633c8-596">Brak.</span><span class="sxs-lookup"><span data-stu-id="633c8-596">None.</span></span>

<span data-ttu-id="633c8-597">**Odpowiedź**</span><span class="sxs-lookup"><span data-stu-id="633c8-597">**Response**</span></span>

<span data-ttu-id="633c8-598">Kod stanu: 200 OK jest zwracana dla pomyślnej odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="633c8-598">Status Code: 200 OK is returned for a successful response.</span></span>

<span data-ttu-id="633c8-599">Zobacz przykład Witaj JSON w [tworzenie i aktualizowanie indeksu](#CreateUpdateIndexExample) przykład hello ładunku odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="633c8-599">See hello example JSON in [Creating and Updating an Index](#CreateUpdateIndexExample) for an example of hello response payload.</span></span>

<a name="DeleteIndex"></a>

## <a name="delete-index"></a><span data-ttu-id="633c8-600">Usuwanie indeksu</span><span class="sxs-lookup"><span data-stu-id="633c8-600">Delete Index</span></span>
<span data-ttu-id="633c8-601">Witaj **Usuń indeks** operacji usuwa indeks i dokumenty skojarzone z usługi Azure Search.</span><span class="sxs-lookup"><span data-stu-id="633c8-601">hello **Delete Index** operation removes an index and associated documents from your Azure Search service.</span></span> <span data-ttu-id="633c8-602">Nazwa indeksu hello można uzyskać z pulpitu nawigacyjnego usługi hello w portalu Azure hello lub hello interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="633c8-602">You can get hello index name from hello service dashboard in hello Azure portal, or from hello API.</span></span> <span data-ttu-id="633c8-603">Zobacz [listy indeksów](#ListIndexes) szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="633c8-603">See [List Indexes](#ListIndexes) for details.</span></span>

    DELETE https://[service name].search.windows.net/indexes/[index name]?api-version=[api-version]
    api-key: [admin key]

<span data-ttu-id="633c8-604">**Żądanie**</span><span class="sxs-lookup"><span data-stu-id="633c8-604">**Request**</span></span>

<span data-ttu-id="633c8-605">HTTPS jest wymagana dla żądań obsługi.</span><span class="sxs-lookup"><span data-stu-id="633c8-605">HTTPS is required for service requests.</span></span> <span data-ttu-id="633c8-606">Witaj **Usuń indeks** żądania może być skonstruowany przy użyciu metody DELETE hello.</span><span class="sxs-lookup"><span data-stu-id="633c8-606">hello **Delete Index** request can be constructed using hello DELETE method.</span></span>

<span data-ttu-id="633c8-607">hello [Nazwa indeksu] w identyfikatorze URI żądania hello Określa, które toodelete indeksu z kolekcji indeksów hello.</span><span class="sxs-lookup"><span data-stu-id="633c8-607">hello [index name] in hello request URI specifies which index toodelete from hello indexes collection.</span></span>

<span data-ttu-id="633c8-608">`api-version=[string]`(wymagane).</span><span class="sxs-lookup"><span data-stu-id="633c8-608">`api-version=[string]` (required).</span></span> <span data-ttu-id="633c8-609">Wersja zapoznawcza Hello jest `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="633c8-609">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="633c8-610">Zobacz [przechowywanie wersji usługi wyszukiwania](http://msdn.microsoft.com/library/azure/dn864560.aspx) szczegółowe informacje i alternatywne wersje.</span><span class="sxs-lookup"><span data-stu-id="633c8-610">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="633c8-611">**Nagłówki żądania**</span><span class="sxs-lookup"><span data-stu-id="633c8-611">**Request Headers**</span></span>

<span data-ttu-id="633c8-612">powitania po liście opisano hello wymagane i opcjonalne żądania nagłówków.</span><span class="sxs-lookup"><span data-stu-id="633c8-612">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="633c8-613">`api-key`: Wymagane.</span><span class="sxs-lookup"><span data-stu-id="633c8-613">`api-key`: Required.</span></span> <span data-ttu-id="633c8-614">Witaj `api-key` jest używane tooauthenticate hello żądania tooyour usługi wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="633c8-614">hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="633c8-615">Jest to wartość ciągu tooyour unikatowy adres URL usługi.</span><span class="sxs-lookup"><span data-stu-id="633c8-615">It is a string value, unique tooyour service URL.</span></span> <span data-ttu-id="633c8-616">Witaj **usunąć indeksu** żądanie musi zawierać `api-key` nagłówka ustawić tooyour klucza administratora (jako klucz zapytania min. tooa).</span><span class="sxs-lookup"><span data-stu-id="633c8-616">hello **Delete Index** request must include an `api-key` header set tooyour admin key (as opposed tooa query key).</span></span>

<span data-ttu-id="633c8-617">Należy również adres URL hello usługi nazwa tooconstruct hello żądania.</span><span class="sxs-lookup"><span data-stu-id="633c8-617">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="633c8-618">Można uzyskać nazwy usługi hello i `api-key` z pulpitu nawigacyjnego usługi w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="633c8-618">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="633c8-619">Zobacz [Tworzenie usługi Azure Search w portalu hello](search-create-service-portal.md) dla pomocy nawigacji strony.</span><span class="sxs-lookup"><span data-stu-id="633c8-619">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="633c8-620">**Treść żądania**</span><span class="sxs-lookup"><span data-stu-id="633c8-620">**Request Body**</span></span>

<span data-ttu-id="633c8-621">Brak.</span><span class="sxs-lookup"><span data-stu-id="633c8-621">None.</span></span>

<span data-ttu-id="633c8-622">**Odpowiedź**</span><span class="sxs-lookup"><span data-stu-id="633c8-622">**Response**</span></span>

<span data-ttu-id="633c8-623">Kod stanu: 204 nr zawartości jest zwracana dla pomyślnej odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="633c8-623">Status Code: 204 No Content is returned for a successful response.</span></span>

<a name="GetIndexStats"></a>

## <a name="get-index-statistics"></a><span data-ttu-id="633c8-624">Uzyskać statystyki indeksu</span><span class="sxs-lookup"><span data-stu-id="633c8-624">Get Index Statistics</span></span>
<span data-ttu-id="633c8-625">Witaj **uzyskać statystyki indeksu** operacja zwraca z usługi Azure Search o liczbie dokumentów hello bieżącego indeksu, a także wykorzystanie magazynu.</span><span class="sxs-lookup"><span data-stu-id="633c8-625">hello **Get Index Statistics** operation returns from Azure Search a document count for hello current index, plus storage usage.</span></span>

    GET https://[service name].search.windows.net/indexes/[index name]/stats?api-version=[api-version]
    api-key: [admin key]

> [!NOTE]
> <span data-ttu-id="633c8-626">Statystyki na dokument liczby i rozmiaru magazynu są gromadzone co kilka minut, nie znajduje się w czasie rzeczywistym.</span><span class="sxs-lookup"><span data-stu-id="633c8-626">Statistics on document count and storage size are collected every few minutes, not in real time.</span></span> <span data-ttu-id="633c8-627">W związku z tym statystyki hello zwróconych przez ten interfejs API może nie odzwierciedlać, zmiany spowodowane przez ostatnie operacje indeksowania.</span><span class="sxs-lookup"><span data-stu-id="633c8-627">Therefore, hello statistics returned by this API may not reflect changes caused by recent indexing operations.</span></span>
> 
> 

<span data-ttu-id="633c8-628">**Żądanie**</span><span class="sxs-lookup"><span data-stu-id="633c8-628">**Request**</span></span>

<span data-ttu-id="633c8-629">HTTPS jest wymagana dla wszystkich żądań usług.</span><span class="sxs-lookup"><span data-stu-id="633c8-629">HTTPS is required for all services requests.</span></span> <span data-ttu-id="633c8-630">Witaj **uzyskać statystyki indeksu** żądania można skonstruować przy użyciu metody GET hello.</span><span class="sxs-lookup"><span data-stu-id="633c8-630">hello **Get Index Statistics** request can be constructed using hello GET method.</span></span>

<span data-ttu-id="633c8-631">hello [Nazwa indeksu] w identyfikatorze URI żądania hello informuje hello usługi tooreturn indeksu statystyki dotyczące hello określonego indeksu.</span><span class="sxs-lookup"><span data-stu-id="633c8-631">hello [index name] in hello request URI tells hello service tooreturn index statistics for hello specified index.</span></span>

<span data-ttu-id="633c8-632">`api-version=[string]`(wymagane).</span><span class="sxs-lookup"><span data-stu-id="633c8-632">`api-version=[string]` (required).</span></span> <span data-ttu-id="633c8-633">Wersja zapoznawcza Hello jest `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="633c8-633">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="633c8-634">Zobacz [przechowywanie wersji usługi wyszukiwania](http://msdn.microsoft.com/library/azure/dn864560.aspx) szczegółowe informacje i alternatywne wersje.</span><span class="sxs-lookup"><span data-stu-id="633c8-634">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="633c8-635">**Nagłówki żądania**</span><span class="sxs-lookup"><span data-stu-id="633c8-635">**Request Headers**</span></span>

<span data-ttu-id="633c8-636">powitania po liście opisano hello wymagane i opcjonalne żądania nagłówków.</span><span class="sxs-lookup"><span data-stu-id="633c8-636">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="633c8-637">`api-key`: hello `api-key` jest używane tooauthenticate hello żądania tooyour usługi wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="633c8-637">`api-key`: hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="633c8-638">Jest to wartość ciągu, usługa tooyour unikatowy.</span><span class="sxs-lookup"><span data-stu-id="633c8-638">It is a string value, unique tooyour service.</span></span> <span data-ttu-id="633c8-639">Witaj **uzyskać statystyki indeksu** żądanie musi zawierać `api-key` klucz administratora tooan zestawu (jako klucz zapytania min. tooa).</span><span class="sxs-lookup"><span data-stu-id="633c8-639">hello **Get Index Statistics** request must include an `api-key` set tooan admin key (as opposed tooa query key).</span></span>

<span data-ttu-id="633c8-640">Należy również adres URL hello usługi nazwa tooconstruct hello żądania.</span><span class="sxs-lookup"><span data-stu-id="633c8-640">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="633c8-641">Można uzyskać nazwy usługi hello i `api-key` z pulpitu nawigacyjnego usługi w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="633c8-641">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="633c8-642">Zobacz [Tworzenie usługi Azure Search w portalu hello](search-create-service-portal.md) dla pomocy nawigacji strony.</span><span class="sxs-lookup"><span data-stu-id="633c8-642">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="633c8-643">**Treść żądania**</span><span class="sxs-lookup"><span data-stu-id="633c8-643">**Request Body**</span></span>

<span data-ttu-id="633c8-644">Brak.</span><span class="sxs-lookup"><span data-stu-id="633c8-644">None.</span></span>

<span data-ttu-id="633c8-645">**Odpowiedź**</span><span class="sxs-lookup"><span data-stu-id="633c8-645">**Response**</span></span>

<span data-ttu-id="633c8-646">Kod stanu: 200 OK jest zwracana dla pomyślnej odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="633c8-646">Status Code: 200 OK is returned for a successful response.</span></span>

<span data-ttu-id="633c8-647">Witaj treść odpowiedzi znajduje się w hello następującego formatu:</span><span class="sxs-lookup"><span data-stu-id="633c8-647">hello response body is in hello following format:</span></span>

    {
      "documentCount": number,
      "storageSize": number (size of hello index in bytes)
    }

<a name="TestAnalyzer"></a>

## <a name="test-analyzer"></a><span data-ttu-id="633c8-648">Analizator testów</span><span class="sxs-lookup"><span data-stu-id="633c8-648">Test Analyzer</span></span>
<span data-ttu-id="633c8-649">Witaj **analizowanie interfejsu API** pokazuje, jak analizator dzieli tekst na tokeny.</span><span class="sxs-lookup"><span data-stu-id="633c8-649">hello **Analyze API** shows how an analyzer breaks text into tokens.</span></span>

    POST https://[service name].search.windows.net/indexes/[index name]/analyze?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

<span data-ttu-id="633c8-650">**Żądanie**</span><span class="sxs-lookup"><span data-stu-id="633c8-650">**Request**</span></span>

<span data-ttu-id="633c8-651">HTTPS jest wymagana dla wszystkich żądań usług.</span><span class="sxs-lookup"><span data-stu-id="633c8-651">HTTPS is required for all services requests.</span></span> <span data-ttu-id="633c8-652">Witaj **analizowanie interfejsu API** żądania może być skonstruowany przy użyciu metody POST hello.</span><span class="sxs-lookup"><span data-stu-id="633c8-652">hello **Analyze API** request can be constructed using hello POST method.</span></span>

<span data-ttu-id="633c8-653">`api-version=[string]`(wymagane).</span><span class="sxs-lookup"><span data-stu-id="633c8-653">`api-version=[string]` (required).</span></span> <span data-ttu-id="633c8-654">Wersja zapoznawcza Hello jest `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="633c8-654">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="633c8-655">Zobacz [przechowywanie wersji usługi wyszukiwania](http://msdn.microsoft.com/library/azure/dn864560.aspx) szczegółowe informacje i alternatywne wersje.</span><span class="sxs-lookup"><span data-stu-id="633c8-655">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="633c8-656">**Nagłówki żądania**</span><span class="sxs-lookup"><span data-stu-id="633c8-656">**Request Headers**</span></span>

<span data-ttu-id="633c8-657">powitania po liście opisano hello wymagane i opcjonalne żądania nagłówków.</span><span class="sxs-lookup"><span data-stu-id="633c8-657">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="633c8-658">`api-key`: hello `api-key` jest używane tooauthenticate hello żądania tooyour usługi wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="633c8-658">`api-key`: hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="633c8-659">Jest to wartość ciągu, usługa tooyour unikatowy.</span><span class="sxs-lookup"><span data-stu-id="633c8-659">It is a string value, unique tooyour service.</span></span> <span data-ttu-id="633c8-660">Witaj **analizowanie interfejsu API** żądanie musi zawierać `api-key` klucz administratora tooan zestawu (jako klucz zapytania min. tooa).</span><span class="sxs-lookup"><span data-stu-id="633c8-660">hello **Analyze API** request must include an `api-key` set tooan admin key (as opposed tooa query key).</span></span>

<span data-ttu-id="633c8-661">Należy również hello indeksu nazwę i adres URL hello usługi nazwa tooconstruct hello żądania.</span><span class="sxs-lookup"><span data-stu-id="633c8-661">You will also need hello index name and hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="633c8-662">Można uzyskać nazwy usługi hello i `api-key` z pulpitu nawigacyjnego usługi w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="633c8-662">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="633c8-663">Zobacz [Tworzenie usługi Azure Search w portalu hello](search-create-service-portal.md) dla pomocy nawigacji strony.</span><span class="sxs-lookup"><span data-stu-id="633c8-663">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="633c8-664">**Treść żądania**</span><span class="sxs-lookup"><span data-stu-id="633c8-664">**Request Body**</span></span>

    {
      "text": "Text tooanalyze",
      "analyzer": "analyzer_name"
    }

<span data-ttu-id="633c8-665">lub</span><span class="sxs-lookup"><span data-stu-id="633c8-665">or</span></span>

    {
      "text": "Text tooanalyze",
      "tokenizer": "tokenizer_name",
      "tokenFilters": (optional) [ "token_filter_name" ],
      "charFilters": (optional) [ "char_filter_name" ]
    }

<span data-ttu-id="633c8-666">Witaj `analyzer_name`, `tokenizer_name`, `token_filter_name` i `char_filter_name` muszą toobe prawidłowe nazwy analizatorów wstępnie zdefiniowanych lub niestandardowych, tokenizatory, token filtry i filtry char hello indeksu.</span><span class="sxs-lookup"><span data-stu-id="633c8-666">hello `analyzer_name`, `tokenizer_name`, `token_filter_name` and `char_filter_name` need toobe valid names of predefined or custom analyzers, tokenizers, token filters and char filters for hello index.</span></span> <span data-ttu-id="633c8-667">toolearn Zobacz więcej informacji na temat procesu hello leksykalne analizy [analizy w usłudze Azure Search](https://aka.ms/azsanalysis).</span><span class="sxs-lookup"><span data-stu-id="633c8-667">toolearn more about hello process of lexical analysis see [Analysis in Azure Search](https://aka.ms/azsanalysis).</span></span>

<span data-ttu-id="633c8-668">**Odpowiedź**</span><span class="sxs-lookup"><span data-stu-id="633c8-668">**Response**</span></span>

<span data-ttu-id="633c8-669">Kod stanu: 200 OK jest zwracana dla pomyślnej odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="633c8-669">Status Code: 200 OK is returned for a successful response.</span></span>

<span data-ttu-id="633c8-670">Witaj treść odpowiedzi znajduje się w hello następującego formatu:</span><span class="sxs-lookup"><span data-stu-id="633c8-670">hello response body is in hello following format:</span></span>

    {
      "tokens": [
        {
          "token": string (token),
          "startOffset": number (index of hello first character of hello token),
          "endOffset": number (index of hello last character of hello token),
          "position": number (position of hello token in hello input text)
        },
        ...
      ]
    }

<span data-ttu-id="633c8-671">**Analizowanie przykładowy interfejs API**</span><span class="sxs-lookup"><span data-stu-id="633c8-671">**Analyze API example**</span></span>

<span data-ttu-id="633c8-672">**Żądanie**</span><span class="sxs-lookup"><span data-stu-id="633c8-672">**Request**</span></span>

    {
      "text": "Text tooanalyze",
      "analyzer": "standard"
    }

<span data-ttu-id="633c8-673">**Odpowiedź**</span><span class="sxs-lookup"><span data-stu-id="633c8-673">**Response**</span></span>

    {
      "tokens": [
        {
          "token": "text",
          "startOffset": 0,
          "endOffset": 4,
          "position": 0
        },
        {
          "token": "to",
          "startOffset": 5,
          "endOffset": 7,
          "position": 1
        },
        {
          "token": "analyze",
          "startOffset": 8,
          "endOffset": 15,
          "position": 2
        }
      ]
    }

- - -
<a name="DocOps"></a>

## <a name="document-operations"></a><span data-ttu-id="633c8-674">Operacje dokumentu</span><span class="sxs-lookup"><span data-stu-id="633c8-674">Document Operations</span></span>
<span data-ttu-id="633c8-675">W usłudze Azure Search indeksu są przechowywane w chmurze hello i wypełniane przy użyciu przekazanie usługi toohello dokumentów JSON.</span><span class="sxs-lookup"><span data-stu-id="633c8-675">In Azure Search, an index is stored in hello cloud and populated using JSON documents that you upload toohello service.</span></span> <span data-ttu-id="633c8-676">Wszystkie dokumenty hello, które można przekazać obejmują Boże hello wyszukiwania danych.</span><span class="sxs-lookup"><span data-stu-id="633c8-676">All hello documents that you upload comprise hello corpus of your search data.</span></span> <span data-ttu-id="633c8-677">Dokumenty zawierają pól, niektóre z nich stokenizowanego do terminy wyszukiwania, ponieważ są one przekazywane.</span><span class="sxs-lookup"><span data-stu-id="633c8-677">Documents contain fields, some of which are tokenized into search terms as they are uploaded.</span></span> <span data-ttu-id="633c8-678">Witaj `/docs` segment adresu URL w hello interfejsu API usługi Azure Search reprezentuje kolekcję hello dokumenty do indeksu.</span><span class="sxs-lookup"><span data-stu-id="633c8-678">hello `/docs` URL segment in hello Azure Search API represents hello collection of documents in an index.</span></span> <span data-ttu-id="633c8-679">Wszystkie operacje wykonywane na powitania kolekcji, takie jak przekazywanie, scalanie, usuwanie i badania dokumentów została wykonana w kontekście hello jeden indeks tak hello adresów URL dla tych operacji zawsze rozpoczynają się `/indexes/[index name]/docs` nazwy danego indeksu.</span><span class="sxs-lookup"><span data-stu-id="633c8-679">All operations performed on hello collection such as uploading, merging, deleting, or querying documents take place in hello context of a single index, so hello URLs for these operations will always start with `/indexes/[index name]/docs` for a given index name.</span></span>

<span data-ttu-id="633c8-680">Kod aplikacji należy wygenerować tooAzure tooupload dokumentów JSON wyszukiwania lub użyć [indeksatora](https://msdn.microsoft.com/library/dn946891.aspx) tooload dokumentów, jeśli źródło danych hello jest baza danych SQL Azure lub bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="633c8-680">Your application code must either generate JSON documents tooupload tooAzure Search or you can use an [indexer](https://msdn.microsoft.com/library/dn946891.aspx) tooload documents if hello data source is either Azure SQL Database or Azure Cosmos DB.</span></span> <span data-ttu-id="633c8-681">Zazwyczaj indeksy są wypełnione z jednego zestawu danych, który podasz.</span><span class="sxs-lookup"><span data-stu-id="633c8-681">Typically, indexes are populated from a single dataset that you provide.</span></span>

<span data-ttu-id="633c8-682">Należy zaplanować na o jeden dokument dla każdego elementu, które mają toosearch.</span><span class="sxs-lookup"><span data-stu-id="633c8-682">You should plan on having one document for each item that you want toosearch.</span></span> <span data-ttu-id="633c8-683">Aplikacja wynajem filmu może mieć jeden dokument na film, sklepu aplikacje mogą mieć jeden dokument dla jednostki SKU, aplikacji online opracowanie oprogramowania edukacyjnego mogą mieć jeden dokument dla porach, badań firmy mogą mieć jeden dokument dla każdego academic papieru w ich repozytorium i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="633c8-683">A movie rental application might have one document per movie, a storefront application might have one document per SKU, an online courseware application might have one document per course, a research firm might have one document for each academic paper in their repository, and so on.</span></span>

<span data-ttu-id="633c8-684">Dokumenty składają się z co najmniej jedno pole.</span><span class="sxs-lookup"><span data-stu-id="633c8-684">Documents consist of one or more fields.</span></span> <span data-ttu-id="633c8-685">Pola mogą zawierać tekst, który jest stokenizowana przez usługi Azure Search w terminy wyszukiwania, a także z systemem innym niż stokenizowanego lub wartości nietekstowych, które mogą być używane w filtry lub oceniania profile.</span><span class="sxs-lookup"><span data-stu-id="633c8-685">Fields can contain text that is tokenized by Azure Search into search terms, as well as non-tokenized or non-text values that can be used in filters or scoring profiles.</span></span> <span data-ttu-id="633c8-686">Witaj nazwy, typy danych i funkcji wyszukiwania są obsługiwane dla każdego pola są określane przez hello schematu indeksu.</span><span class="sxs-lookup"><span data-stu-id="633c8-686">hello names, data types, and search features supported for each field are determined by hello index schema.</span></span> <span data-ttu-id="633c8-687">Jedno z pól hello schematu indeksu muszą być wyznaczone jako identyfikator, a każdy dokument musi mieć wartość pola Identyfikatora hello, który unikatowo identyfikuje ten dokument w indeksie hello.</span><span class="sxs-lookup"><span data-stu-id="633c8-687">One of hello fields in each index schema must be designated as an ID, and each document must have a value for hello ID field that uniquely identifies that document in hello index.</span></span> <span data-ttu-id="633c8-688">Wszystkie pola dokumentu są opcjonalne i domyślne tooa wartość null, jeśli nie zostanie podany.</span><span class="sxs-lookup"><span data-stu-id="633c8-688">All other document fields are optional and will default tooa null value if left unspecified.</span></span> <span data-ttu-id="633c8-689">Należy pamiętać, że miejsca w indeksie wyszukiwania hello nie przyjmują wartości null.</span><span class="sxs-lookup"><span data-stu-id="633c8-689">Note that null values do not take up space in hello search index.</span></span>

<span data-ttu-id="633c8-690">Zanim można przekazywać dokumenty, musi utworzono już indeks hello na powitania usługi.</span><span class="sxs-lookup"><span data-stu-id="633c8-690">Before you can upload documents, you must have already created hello index on hello service.</span></span> <span data-ttu-id="633c8-691">Zobacz [Create Index](#CreateIndex) szczegółowe informacje o tym pierwszym krokiem.</span><span class="sxs-lookup"><span data-stu-id="633c8-691">See [Create Index](#CreateIndex) for details about this first step.</span></span>

<a name="AddOrUpdateDocuments"></a>

## <a name="add-update-or-delete-documents"></a><span data-ttu-id="633c8-692">Dodawanie, aktualizowanie lub usuwanie dokumentów</span><span class="sxs-lookup"><span data-stu-id="633c8-692">Add, Update, or Delete Documents</span></span>
<span data-ttu-id="633c8-693">Możesz przekazać, scalania, merge lub przekazanie pliku lub Usuń dokumenty od określonego indeksu przy użyciu metody POST protokołu HTTP.</span><span class="sxs-lookup"><span data-stu-id="633c8-693">You can upload, merge, merge-or-upload or delete documents from a specified index using HTTP POST.</span></span> <span data-ttu-id="633c8-694">Duża liczba aktualizacji zaleca się przetwarzanie wsadowe dokumentów (too1000 dokumentów na partię) lub wkrótce 16 MB na partię.</span><span class="sxs-lookup"><span data-stu-id="633c8-694">For large numbers of updates, batching of documents (up too1000 documents per batch or about 16 MB per batch) is recommended.</span></span>

    POST https://[service name].search.windows.net/indexes/[index name]/docs/index?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

<span data-ttu-id="633c8-695">**Żądanie**</span><span class="sxs-lookup"><span data-stu-id="633c8-695">**Request**</span></span>

<span data-ttu-id="633c8-696">HTTPS jest wymagana dla wszystkich żądań obsługi.</span><span class="sxs-lookup"><span data-stu-id="633c8-696">HTTPS is required for all service requests.</span></span> <span data-ttu-id="633c8-697">Możesz przekazać, scalania, merge lub przekazanie pliku lub Usuń dokumenty od określonego indeksu przy użyciu metody POST protokołu HTTP.</span><span class="sxs-lookup"><span data-stu-id="633c8-697">You can upload, merge, merge-or-upload or delete documents from a specified index using HTTP POST.</span></span>

<span data-ttu-id="633c8-698">[Nazwa indeksu] zawiera identyfikator URI żądania Hello określania dokumentów toopost indeksu.</span><span class="sxs-lookup"><span data-stu-id="633c8-698">hello request URI includes [index name], specifying which index toopost documents.</span></span> <span data-ttu-id="633c8-699">Można tylko po indeksie tooone dokumentów w czasie.</span><span class="sxs-lookup"><span data-stu-id="633c8-699">You can only post documents tooone index at a time.</span></span>

<span data-ttu-id="633c8-700">`api-version=[string]`(wymagane).</span><span class="sxs-lookup"><span data-stu-id="633c8-700">`api-version=[string]` (required).</span></span> <span data-ttu-id="633c8-701">Wersja zapoznawcza Hello jest `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="633c8-701">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="633c8-702">Zobacz [przechowywanie wersji usługi wyszukiwania](http://msdn.microsoft.com/library/azure/dn864560.aspx) szczegółowe informacje i alternatywne wersje.</span><span class="sxs-lookup"><span data-stu-id="633c8-702">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="633c8-703">**Nagłówki żądania**</span><span class="sxs-lookup"><span data-stu-id="633c8-703">**Request Headers**</span></span>

<span data-ttu-id="633c8-704">powitania po liście opisano hello wymagane i opcjonalne żądania nagłówków.</span><span class="sxs-lookup"><span data-stu-id="633c8-704">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="633c8-705">`Content-Type`: Wymagane.</span><span class="sxs-lookup"><span data-stu-id="633c8-705">`Content-Type`: Required.</span></span> <span data-ttu-id="633c8-706">Ustaw tę wartość za`application/json`</span><span class="sxs-lookup"><span data-stu-id="633c8-706">Set this too`application/json`</span></span>
* <span data-ttu-id="633c8-707">`api-key`: Wymagane.</span><span class="sxs-lookup"><span data-stu-id="633c8-707">`api-key`: Required.</span></span> <span data-ttu-id="633c8-708">Witaj `api-key` jest używane tooauthenticate hello żądania tooyour usługi wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="633c8-708">hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="633c8-709">Jest to wartość ciągu, usługa tooyour unikatowy.</span><span class="sxs-lookup"><span data-stu-id="633c8-709">It is a string value, unique tooyour service.</span></span> <span data-ttu-id="633c8-710">Witaj **Dodawanie dokumentów** żądanie musi zawierać `api-key` nagłówka ustawić tooyour klucza administratora (jako klucz zapytania min. tooa).</span><span class="sxs-lookup"><span data-stu-id="633c8-710">hello **Add Documents** request must include an `api-key` header set tooyour admin key (as opposed tooa query key).</span></span>

<span data-ttu-id="633c8-711">Należy również adres URL hello usługi nazwa tooconstruct hello żądania.</span><span class="sxs-lookup"><span data-stu-id="633c8-711">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="633c8-712">Można uzyskać nazwy usługi hello i `api-key` z pulpitu nawigacyjnego usługi w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="633c8-712">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="633c8-713">Zobacz [Tworzenie usługi Azure Search w portalu hello](search-create-service-portal.md) dla pomocy nawigacji strony.</span><span class="sxs-lookup"><span data-stu-id="633c8-713">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="633c8-714">**Treść żądania**</span><span class="sxs-lookup"><span data-stu-id="633c8-714">**Request Body**</span></span>

<span data-ttu-id="633c8-715">Witaj treści żądania hello zawiera jeden lub więcej dokumentów toobe indeksowanym.</span><span class="sxs-lookup"><span data-stu-id="633c8-715">hello body of hello request contains one or more documents toobe indexed.</span></span> <span data-ttu-id="633c8-716">Dokumenty są identyfikowane przez unikatowy klucz.</span><span class="sxs-lookup"><span data-stu-id="633c8-716">Documents are identified by a unique key.</span></span> <span data-ttu-id="633c8-717">Każdy dokument jest skojarzony z akcją: przekazywanie, scalania, mergeOrUpload lub delete.</span><span class="sxs-lookup"><span data-stu-id="633c8-717">Each document is associated with an action: upload, merge, mergeOrUpload or delete.</span></span> <span data-ttu-id="633c8-718">Przekaż żądania musi zawierać dane dokumentu hello jako zestaw par klucz/wartość.</span><span class="sxs-lookup"><span data-stu-id="633c8-718">Upload requests must include hello document data as a set of key/value pairs.</span></span>

    {
      "value": [
        {
          "@search.action": "upload (default) | merge | mergeOrUpload | delete",
          "key_field_name": "unique_key_of_document", (key/value pair for key field from index schema)
          "field_name": field_value (key/value pairs matching index schema)
            ...
        },
        ...
      ]
    }

> [!NOTE]
> <span data-ttu-id="633c8-719">Klucze dokumentu może zawierać tylko litery, cyfry, łączniki ("-"), znaki podkreślenia ("_") i znaku równości ("=").</span><span class="sxs-lookup"><span data-stu-id="633c8-719">Document keys can only contain letters, numbers, dashes ("-"), underscores ("_"), and equal signs ("=").</span></span> <span data-ttu-id="633c8-720">Aby uzyskać więcej informacji, zobacz [reguły nazewnictwa](https://msdn.microsoft.com/library/azure/dn857353.aspx).</span><span class="sxs-lookup"><span data-stu-id="633c8-720">For more details, see [Naming rules](https://msdn.microsoft.com/library/azure/dn857353.aspx).</span></span>
> 
> 

<span data-ttu-id="633c8-721">**Akcje dokumentu**</span><span class="sxs-lookup"><span data-stu-id="633c8-721">**Document Actions**</span></span>

* <span data-ttu-id="633c8-722">`upload`: Akcja przekazywanie jest podobne tooan "upsert", gdzie hello dokument zostanie wstawiony, jeśli jest nowy albo zaktualizowany/zastąpiony, jeśli istnieje.</span><span class="sxs-lookup"><span data-stu-id="633c8-722">`upload`: An upload action is similar tooan "upsert" where hello document will be inserted if it is new and updated/replaced if it exists.</span></span> <span data-ttu-id="633c8-723">Należy pamiętać, że wszystkie pola są zamieniane w przypadku aktualizacji hello.</span><span class="sxs-lookup"><span data-stu-id="633c8-723">Note that all fields are replaced in hello update case.</span></span>
* <span data-ttu-id="633c8-724">`merge`: Aktualizacje scalanie istniejący dokument o hello określone pola.</span><span class="sxs-lookup"><span data-stu-id="633c8-724">`merge`: Merge updates an existing document with hello specified fields.</span></span> <span data-ttu-id="633c8-725">Jeśli dokument hello nie istnieje, hello scalanie zakończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="633c8-725">If hello document doesn't exist, hello merge will fail.</span></span> <span data-ttu-id="633c8-726">Wszystkie pola, które określisz w żądaniu scalania zastąpi istniejące pole hello w dokumencie hello.</span><span class="sxs-lookup"><span data-stu-id="633c8-726">Any field you specify in a merge will replace hello existing field in hello document.</span></span> <span data-ttu-id="633c8-727">Obejmuje to również pola typu `Collection(Edm.String)`.</span><span class="sxs-lookup"><span data-stu-id="633c8-727">This includes fields of type `Collection(Edm.String)`.</span></span> <span data-ttu-id="633c8-728">Na przykład, jeśli hello dokument zawiera pole "tagi" o wartości `["budget"]` i wykonywane jest scalanie z wartością `["economy", "pool"]` "tagów" będzie końcowa wartość pola tagi"hello" hello `["economy", "pool"]`.</span><span class="sxs-lookup"><span data-stu-id="633c8-728">For example, if hello document contains a field "tags" with value `["budget"]` and you execute a merge with value `["economy", "pool"]` for "tags", hello final value of hello "tags" field will be `["economy", "pool"]`.</span></span> <span data-ttu-id="633c8-729">Będzie on **nie** można `["budget", "economy", "pool"]`.</span><span class="sxs-lookup"><span data-stu-id="633c8-729">It will **not** be `["budget", "economy", "pool"]`.</span></span>
* <span data-ttu-id="633c8-730">`mergeOrUpload`: zachowuje się jak `merge` Jeśli dokument o hello podany klucz już istnieje w indeksie hello.</span><span class="sxs-lookup"><span data-stu-id="633c8-730">`mergeOrUpload`: behaves like `merge` if a document with hello given key already exists in hello index.</span></span> <span data-ttu-id="633c8-731">Jeśli dokument hello nie istnieje zachowuje się jak `upload` dla nowego dokumentu.</span><span class="sxs-lookup"><span data-stu-id="633c8-731">If hello document does not exist it behaves like `upload` with a new document.</span></span>
* <span data-ttu-id="633c8-732">`delete`: Delete Usuwa hello określony dokument z indeksu hello.</span><span class="sxs-lookup"><span data-stu-id="633c8-732">`delete`: Delete removes hello specified document from hello index.</span></span> <span data-ttu-id="633c8-733">Należy pamiętać, że wszystkie pola, które określisz w `delete` operacji innego niż pole klucza hello zostaną zignorowane.</span><span class="sxs-lookup"><span data-stu-id="633c8-733">Note that any fields you specify in a `delete` operation other than hello key field will be ignored.</span></span> <span data-ttu-id="633c8-734">Tooremove pojedyncze pole z dokumentu, należy użyć `merge` zamiast i po prostu hello jawnie ustaw pola zbyt`null`.</span><span class="sxs-lookup"><span data-stu-id="633c8-734">If you want tooremove an individual field from a document, use `merge` instead and simply set hello field explicitly too`null`.</span></span>

<span data-ttu-id="633c8-735">**Odpowiedź**</span><span class="sxs-lookup"><span data-stu-id="633c8-735">**Response**</span></span>

<span data-ttu-id="633c8-736">Dla pomyślnej odpowiedzi, co oznacza, że wszystkie elementy zostały pomyślnie zindeksowane zwracany jest kod stanu 200 (OK).</span><span class="sxs-lookup"><span data-stu-id="633c8-736">Status code 200 (OK) is returned for a successful response, meaning that all items have been successfully indexed.</span></span> <span data-ttu-id="633c8-737">Jest to określane przez hello `status` ustawienia właściwości tootrue dla wszystkich elementów, jak również hello `statusCode` ustawienia właściwości tooeither 201 (dla nowo przesłanym dokumenty) lub 200 (w przypadku scalonych lub usunięto dokumenty):</span><span class="sxs-lookup"><span data-stu-id="633c8-737">This is indicated by hello `status` property being set tootrue for all items, as well as hello `statusCode` property being set tooeither 201 (for newly uploaded documents) or 200 (for merged or deleted documents):</span></span>

    {
      "value": [
        {
          "key": "unique_key_of_new_document",
          "status": true,
          "errorMessage": null,
          "statusCode": 201
        },
        {
          "key": "unique_key_of_merged_document",
          "status": true,
          "errorMessage": null,
          "statusCode": 200
        },
        {
          "key": "unique_key_of_deleted_document",
          "status": true,
          "errorMessage": null,
          "statusCode": 200
        }
      ]
    }  

<span data-ttu-id="633c8-738">Kod stanu 207 (wiele stanów) jest zwracany, gdy co najmniej jeden element nie został pomyślnie indeksowane.</span><span class="sxs-lookup"><span data-stu-id="633c8-738">Status code 207 (Multi-Status) is returned when at least one item was not successfully indexed.</span></span> <span data-ttu-id="633c8-739">Elementy, które nie zostały zaindeksowane mają hello `status` toofalse zestawu pól.</span><span class="sxs-lookup"><span data-stu-id="633c8-739">Items that have not been indexed have hello `status` field set toofalse.</span></span> <span data-ttu-id="633c8-740">Witaj `errorMessage` i `statusCode` właściwości będzie wskazywać przyczynę hello hello indeksowania błąd:</span><span class="sxs-lookup"><span data-stu-id="633c8-740">hello `errorMessage` and `statusCode` properties will indicate hello reason for hello indexing error:</span></span>

    {
      "value": [
        {
          "key": "unique_key_of_document_1",
          "status": false,
          "errorMessage": "hello search service is too busy tooprocess this document. Please try again later.",
          "statusCode": 503
        },
        {
          "key": "unique_key_of_document_2",
          "status": false,
          "errorMessage": "Document not found.",
          "statusCode": 404
        },
        {
          "key": "unique_key_of_document_3",
          "status": false,
          "errorMessage": "Index is temporarily unavailable because it was updated with hello 'allowIndexDowntime' flag set too'true'. Please try again later.",
          "statusCode": 422
        }
      ]
    }  

<span data-ttu-id="633c8-741">Witaj w poniższej tabeli opisano hello różnych powiązany z dokumentem kodów stanu, które może być zwracany w odpowiedzi hello.</span><span class="sxs-lookup"><span data-stu-id="633c8-741">hello following table explains hello various per-document status codes that can be returned in hello response.</span></span> <span data-ttu-id="633c8-742">Należy pamiętać, że niektóre wskazują na problemy z hello żądania, podczas gdy inne wskazać warunki tymczasowy błąd.</span><span class="sxs-lookup"><span data-stu-id="633c8-742">Note that some indicate problems with hello request itself, while others indicate temporary error conditions.</span></span> <span data-ttu-id="633c8-743">ostatnie Hello powinna ponowić z opóźnieniem.</span><span class="sxs-lookup"><span data-stu-id="633c8-743">hello latter you should retry after a delay.</span></span>

<table style="font-size:12">
    <tr>
        <th><span data-ttu-id="633c8-744">Kod stanu</span><span class="sxs-lookup"><span data-stu-id="633c8-744">Status code</span></span></th>
        <th><span data-ttu-id="633c8-745">Znaczenie</span><span class="sxs-lookup"><span data-stu-id="633c8-745">Meaning</span></span></th>
        <th><span data-ttu-id="633c8-746">Powtarzający operację</span><span class="sxs-lookup"><span data-stu-id="633c8-746">Retryable</span></span></th>
        <th><span data-ttu-id="633c8-747">Uwagi</span><span class="sxs-lookup"><span data-stu-id="633c8-747">Notes</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="633c8-748">200</span><span class="sxs-lookup"><span data-stu-id="633c8-748">200</span></span></td>
        <td><span data-ttu-id="633c8-749">Dokument został pomyślnie zmodyfikowany lub usunięty.</span><span class="sxs-lookup"><span data-stu-id="633c8-749">Document was successfully modified or deleted.</span></span></td>
        <td><span data-ttu-id="633c8-750">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="633c8-750">n/a</span></span></td>
        <td><span data-ttu-id="633c8-751">Usuwanie operacji są <a href="https://en.wikipedia.org/wiki/Idempotence">idempotentności</a>.</span><span class="sxs-lookup"><span data-stu-id="633c8-751">Delete operations are <a href="https://en.wikipedia.org/wiki/Idempotence">idempotent</a>.</span></span> <span data-ttu-id="633c8-752">Oznacza to nawet jeśli klucz dokumentu nie istnieje w indeksie hello, próbę wykonania operacji usuwania z tego klucza spowoduje kod stanu 200.</span><span class="sxs-lookup"><span data-stu-id="633c8-752">That is, even if a document key does not exist in hello index, attempting a delete operation with that key will result in a 200 status code.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="633c8-753">201</span><span class="sxs-lookup"><span data-stu-id="633c8-753">201</span></span></td>
        <td><span data-ttu-id="633c8-754">Dokument został pomyślnie utworzony.</span><span class="sxs-lookup"><span data-stu-id="633c8-754">Document was successfully created.</span></span></td>
        <td><span data-ttu-id="633c8-755">Nie dotyczy</span><span class="sxs-lookup"><span data-stu-id="633c8-755">n/a</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="633c8-756">400</span><span class="sxs-lookup"><span data-stu-id="633c8-756">400</span></span></td>
        <td><span data-ttu-id="633c8-757">Wystąpił błąd w dokumencie hello, który uniemożliwił indeksowany.</span><span class="sxs-lookup"><span data-stu-id="633c8-757">There was an error in hello document that prevented it from being indexed.</span></span></td>
        <td><span data-ttu-id="633c8-758">Nie</span><span class="sxs-lookup"><span data-stu-id="633c8-758">No</span></span></td>
        <td><span data-ttu-id="633c8-759">komunikat o błędzie Hello w odpowiedzi hello wskaże, co to jest problem z hello dokumentu.</span><span class="sxs-lookup"><span data-stu-id="633c8-759">hello error message in hello response will indicate what is wrong with hello document.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="633c8-760">404</span><span class="sxs-lookup"><span data-stu-id="633c8-760">404</span></span></td>
        <td><span data-ttu-id="633c8-761">Nie można scalić Hello dokumentu, ponieważ hello podany klucz nie istnieje w indeksie hello.</span><span class="sxs-lookup"><span data-stu-id="633c8-761">hello document could not be merged because hello given key doesn't exist in hello index.</span></span></td>
        <td><span data-ttu-id="633c8-762">Nie</span><span class="sxs-lookup"><span data-stu-id="633c8-762">No</span></span></td>
        <td><span data-ttu-id="633c8-763">Ten błąd nie występuje przekazywania, ponieważ ich tworzenie nowych dokumentów, a nie występuje dla usunięć ponieważ są one <a href="https://en.wikipedia.org/wiki/Idempotence">idempotentności</a>.</span><span class="sxs-lookup"><span data-stu-id="633c8-763">This error does not occur for uploads since they create new documents, and it does not occur for deletes because they are <a href="https://en.wikipedia.org/wiki/Idempotence">idempotent</a>.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="633c8-764">409</span><span class="sxs-lookup"><span data-stu-id="633c8-764">409</span></span></td>
        <td><span data-ttu-id="633c8-765">Wykryto konflikt wersji podczas próby tooindex dokumentu.</span><span class="sxs-lookup"><span data-stu-id="633c8-765">A version conflict was detected when attempting tooindex a document.</span></span></td>
        <td><span data-ttu-id="633c8-766">Tak</span><span class="sxs-lookup"><span data-stu-id="633c8-766">Yes</span></span></td>
        <td><span data-ttu-id="633c8-767">Może to nastąpić, jeśli próbujesz hello tooindex sam dokumentu więcej niż raz jednocześnie.</span><span class="sxs-lookup"><span data-stu-id="633c8-767">This can happen when you're trying tooindex hello same document more than once concurrently.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="633c8-768">422</span><span class="sxs-lookup"><span data-stu-id="633c8-768">422</span></span></td>
        <td><span data-ttu-id="633c8-769">Indeks Hello jest tymczasowo niedostępny, ponieważ został zaktualizowany o too'true Ustaw flagi "allowIndexDowntime" hello ".</span><span class="sxs-lookup"><span data-stu-id="633c8-769">hello index is temporarily unavailable because it was updated with hello 'allowIndexDowntime' flag set too'true'.</span></span></td>
        <td><span data-ttu-id="633c8-770">Tak</span><span class="sxs-lookup"><span data-stu-id="633c8-770">Yes</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="633c8-771">503</span><span class="sxs-lookup"><span data-stu-id="633c8-771">503</span></span></td>
        <td><span data-ttu-id="633c8-772">Usługi wyszukiwania jest tymczasowo niedostępny, prawdopodobnie powodu tooheavy obciążenia.</span><span class="sxs-lookup"><span data-stu-id="633c8-772">Your search service is temporarily unavailable, possibly due tooheavy load.</span></span></td>
        <td><span data-ttu-id="633c8-773">Tak</span><span class="sxs-lookup"><span data-stu-id="633c8-773">Yes</span></span></td>
        <td><span data-ttu-id="633c8-774">Kod ma odczekać przed ponowną próbą w takim przypadku lub istnieje ryzyko, przedłużenie hello niedostępności usługi.</span><span class="sxs-lookup"><span data-stu-id="633c8-774">Your code should wait before retrying in this case or you risk prolonging hello service unavailability.</span></span></td>
    </tr>
</table> 

<span data-ttu-id="633c8-775">**Uwaga**: Jeśli kod klienta często napotka odpowiedź 207, jedną z możliwych przyczyn jest hello system pod obciążeniem.</span><span class="sxs-lookup"><span data-stu-id="633c8-775">**Note**: If your client code frequently encounters a 207 response, one possible reason is that hello system is under load.</span></span> <span data-ttu-id="633c8-776">Można to potwierdzić, sprawdzając hello `statusCode` właściwość 503.</span><span class="sxs-lookup"><span data-stu-id="633c8-776">You can confirm this by checking hello `statusCode` property for 503.</span></span> <span data-ttu-id="633c8-777">Jeśli hello tak jest, zalecamy ***ograniczania żądania indeksowania***.</span><span class="sxs-lookup"><span data-stu-id="633c8-777">If this is hello case, we recommend ***throttling indexing requests***.</span></span> <span data-ttu-id="633c8-778">W przeciwnym razie jeśli ruch indeksowania nie subside, hello system można uruchomić odrzuca wszystkie żądania z błędami 503.</span><span class="sxs-lookup"><span data-stu-id="633c8-778">Otherwise, if indexing traffic doesn't subside, hello system could start rejecting all requests with 503 errors.</span></span>

<span data-ttu-id="633c8-779">Kod stanu 429 wskazuje, że przekroczono limitu przydziału na powitania liczby dokumentów w indeksie.</span><span class="sxs-lookup"><span data-stu-id="633c8-779">Status code 429 indicates that you have exceeded your quota on hello number of documents per index.</span></span> <span data-ttu-id="633c8-780">Należy utworzyć nowy indeks lub uaktualnienia wyższe limity pojemności.</span><span class="sxs-lookup"><span data-stu-id="633c8-780">You must either create a new index or upgrade for higher capacity limits.</span></span>

<span data-ttu-id="633c8-781">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="633c8-781">**Example:**</span></span>

    {
      "value": [
        {
          "@search.action": "upload",
          "hotelId": "1",
          "baseRate": 199.0,
          "description": "Best hotel in town",
          "description_fr": "Meilleur hôtel en ville",
          "hotelName": "Fancy Stay",
          "category": "Luxury",
          "tags": ["pool", "view", "wifi", "concierge"],
          "parkingIncluded": false,
          "smokingAllowed": false,
          "lastRenovationDate": "2010-06-27T00:00:00Z",
          "rating": 5,
          "location": { "type": "Point", "coordinates": [-122.131577, 47.678581] }
        },
        {
          "@search.action": "upload",
          "hotelId": "2",
          "baseRate": 79.99,
          "description": "Cheapest hotel in town",
          "description_fr": "Hôtel le moins cher en ville",
          "hotelName": "Roach Motel",
          "category": "Budget",
          "tags": ["motel", "budget"],
          "parkingIncluded": true,
          "smokingAllowed": true,
          "lastRenovationDate": "1982-04-28T00:00:00Z",
          "rating": 1,
          "location": { "type": "Point", "coordinates": [-122.131577, 49.678581] }
        },
        {
          "@search.action": "merge",
          "hotelId": "3",
          "baseRate": 279.99,
          "description": "Surprisingly expensive",
          "lastRenovationDate": null
        },
        {
          "@search.action": "delete",
          "hotelId": "4"
        }
      ]
    }
- - -
<a name="SearchDocs"></a>

## <a name="search-documents"></a><span data-ttu-id="633c8-782">Przeszukaj dokumenty</span><span class="sxs-lookup"><span data-stu-id="633c8-782">Search Documents</span></span>
<span data-ttu-id="633c8-783">A **wyszukiwania** operacji wydawane jako żądania GET lub POST, określa parametry, które zapewniają hello kryteria wyboru pasujących dokumentów.</span><span class="sxs-lookup"><span data-stu-id="633c8-783">A **Search** operation is issued as a GET or POST request and specifies parameters that give hello criteria for selecting matching documents.</span></span>

    GET https://[service name].search.windows.net/indexes/[index name]/docs?[query parameters]
    api-key: [admin or query key]

    POST https://[service name].search.windows.net/indexes/[index name]/docs/search?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin or query key]

<span data-ttu-id="633c8-784">**Podczas publikowania toouse zamiast GET**</span><span class="sxs-lookup"><span data-stu-id="633c8-784">**When toouse POST instead of GET**</span></span>

<span data-ttu-id="633c8-785">Jeśli używasz HTTP GET hello toocall **wyszukiwania** interfejsu API, należy pamiętać, że hello długość adresu URL żądania hello nie może przekraczać 8 KB toobe.</span><span class="sxs-lookup"><span data-stu-id="633c8-785">When you use HTTP GET toocall hello **Search** API, you need toobe aware that hello length of hello request URL cannot exceed 8 KB.</span></span> <span data-ttu-id="633c8-786">Jest to zwykle wystarczająco dla większości aplikacji.</span><span class="sxs-lookup"><span data-stu-id="633c8-786">This is usually enough for most applications.</span></span> <span data-ttu-id="633c8-787">Jednak niektóre aplikacje powodują bardzo dużych kwerend lub wyrażeniach filtru OData.</span><span class="sxs-lookup"><span data-stu-id="633c8-787">However, some applications produce very large queries or OData filter expressions.</span></span> <span data-ttu-id="633c8-788">W przypadku tych aplikacji przy użyciu metody POST protokołu HTTP jest lepszym rozwiązaniem, ponieważ umożliwia on większy filtry i zapytania niż GET.</span><span class="sxs-lookup"><span data-stu-id="633c8-788">For these applications, using HTTP POST is a better choice because it allows larger filters and queries than GET.</span></span> <span data-ttu-id="633c8-789">POST, liczba hello warunków lub klauzul w zapytaniu hello jest ograniczanie współczynnik, nie hello rozmiar hello raw zapytania, ponieważ limit rozmiaru hello żądania POST wynosi około 16 MB.</span><span class="sxs-lookup"><span data-stu-id="633c8-789">With POST, hello number of terms or clauses in a query is hello limiting factor, not hello size of hello raw query since hello request size limit for POST is approximately 16 MB.</span></span>

> [!NOTE]
> <span data-ttu-id="633c8-790">Mimo że limit rozmiaru żądania POST hello jest bardzo duży, zapytania wyszukiwania i wyrażenia filtru nie może być arbitralnie złożonych.</span><span class="sxs-lookup"><span data-stu-id="633c8-790">Even though hello POST request size limit is very large, search queries and filter expressions cannot be arbitrarily complex.</span></span> <span data-ttu-id="633c8-791">Zobacz [składnia zapytań Lucene](https://msdn.microsoft.com/library/mt589323.aspx) i [składni wyrażeń OData](https://msdn.microsoft.com/library/dn798921.aspx) uzyskać więcej informacji o ograniczeniach złożoności zapytań i filtr wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="633c8-791">See [Lucene query syntax](https://msdn.microsoft.com/library/mt589323.aspx) and [OData expression syntax](https://msdn.microsoft.com/library/dn798921.aspx) for more information about search query and filter complexity limitations.</span></span>
> 
> 

<span data-ttu-id="633c8-792">**Żądanie**</span><span class="sxs-lookup"><span data-stu-id="633c8-792">**Request**</span></span>

<span data-ttu-id="633c8-793">HTTPS jest wymagana dla żądań obsługi.</span><span class="sxs-lookup"><span data-stu-id="633c8-793">HTTPS is required for service requests.</span></span> <span data-ttu-id="633c8-794">Witaj **wyszukiwania** żądania można skonstruować przy użyciu hello GET lub POST metody.</span><span class="sxs-lookup"><span data-stu-id="633c8-794">hello **Search** request can be constructed using hello GET or POST methods.</span></span>

<span data-ttu-id="633c8-795">Identyfikator URI żądania Hello Określa, które tooquery indeksu, dla wszystkich dokumentów zgodnych parametrów hello.</span><span class="sxs-lookup"><span data-stu-id="633c8-795">hello request URI specifies which index tooquery, for all documents that match hello parameters.</span></span> <span data-ttu-id="633c8-796">Parametry są określone na ciąg zapytania hello w przypadku żądania GET hello, a w żądaniu hello żądań treści w przypadku hello POST.</span><span class="sxs-lookup"><span data-stu-id="633c8-796">Parameters are specified on hello query string in hello case of GET requests, and in hello request body in hello case of POST requests.</span></span>

<span data-ttu-id="633c8-797">Najlepszym rozwiązaniem podczas tworzenia żądania GET, pamiętaj zbyt[kodowania adresu URL](https://msdn.microsoft.com/library/system.uri.escapedatastring.aspx) określonej kwerendy bezpośrednio hello parametrów podczas wywoływania metody interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="633c8-797">As a best practice when creating GET requests, remember too[URL-encode](https://msdn.microsoft.com/library/system.uri.escapedatastring.aspx) specific query parameters when calling hello REST API directly.</span></span> <span data-ttu-id="633c8-798">Aby uzyskać **wyszukiwania** operacje, w tym:</span><span class="sxs-lookup"><span data-stu-id="633c8-798">For **Search** operations, this includes:</span></span>

* `$filter`
* `facet`
* `highlightPreTag`
* `highlightPostTag`
* `search`
* `moreLikeThis`

<span data-ttu-id="633c8-799">Kodowanie adresu URL zaleca się tylko na powitania powyżej parametry zapytania.</span><span class="sxs-lookup"><span data-stu-id="633c8-799">URL encoding is only recommended on hello above query parameters.</span></span> <span data-ttu-id="633c8-800">Jeśli użytkownik przypadkowo kodowania adresu URL hello ciągu zapytania całego, (wszystko po hello?), spowoduje przerwanie żądania.</span><span class="sxs-lookup"><span data-stu-id="633c8-800">If you inadvertently URL-encode hello entire query string (everything after hello ?), requests will break.</span></span>

<span data-ttu-id="633c8-801">Ponadto podczas kodowania adresu URL jest wymagane tylko podczas wywoływania metody hello UZYSKAĆ bezpośrednio przy użyciu interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="633c8-801">Also, URL encoding is only necessary when calling hello REST API directly using GET.</span></span> <span data-ttu-id="633c8-802">Bez kodowania adresu URL jest niezbędne, jeśli wywołanie **wyszukiwania** używanie żądania POST, lub w przypadku używania hello [biblioteki klienta .NET](https://msdn.microsoft.com/library/dn951165.aspx), który obsługuje kodowanie adresu URL.</span><span class="sxs-lookup"><span data-stu-id="633c8-802">No URL encoding is necessary when calling **Search** using POST, or when using hello [.NET client library](https://msdn.microsoft.com/library/dn951165.aspx), which handles URL encoding for you.</span></span>

<span data-ttu-id="633c8-803"><a name="SearchQueryParameters"></a>
**Parametry zapytań**</span><span class="sxs-lookup"><span data-stu-id="633c8-803"><a name="SearchQueryParameters"></a>
**Query Parameters**</span></span>

<span data-ttu-id="633c8-804">**Wyszukiwanie** przyjmuje kilka parametrów, które zapewniają kryteria, a także określić sposób wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="633c8-804">**Search** accepts several parameters that provide query criteria and also specify search behavior.</span></span> <span data-ttu-id="633c8-805">Należy podać długość ciągu zapytania tych parametrów w adresie URL hello podczas wywoływania metody **wyszukiwania** alerty, a także jako właściwości JSON w treści żądania hello podczas wywoływania metody **wyszukiwania** za pośrednictwem POST.</span><span class="sxs-lookup"><span data-stu-id="633c8-805">You provide these parameters in hello URL query string when calling **Search** via GET, and as JSON properties in hello request body when calling **Search** via POST.</span></span> <span data-ttu-id="633c8-806">Składnia Hello niektórych parametrów różni się nieco między GET i POST.</span><span class="sxs-lookup"><span data-stu-id="633c8-806">hello syntax for some parameters is slightly different between GET and POST.</span></span> <span data-ttu-id="633c8-807">Różnice te odnotowano odpowiednio poniżej:</span><span class="sxs-lookup"><span data-stu-id="633c8-807">These differences are noted as applicable below:</span></span>

<span data-ttu-id="633c8-808">`search=[string]`(opcjonalnie) — Witaj toosearch tekstu dla.</span><span class="sxs-lookup"><span data-stu-id="633c8-808">`search=[string]` (optional) - hello text toosearch for.</span></span> <span data-ttu-id="633c8-809">Wszystkie `searchable` pola są przeszukiwane domyślnie, chyba że `searchFields` jest określona.</span><span class="sxs-lookup"><span data-stu-id="633c8-809">All `searchable` fields are searched by default unless `searchFields` is specified.</span></span> <span data-ttu-id="633c8-810">Podczas wyszukiwania `searchable` stokenizowanego pól, sam tekst wyszukiwania hello tak wielu warunki mogą być oddzielone biały znak (na przykład: `search=hello world`).</span><span class="sxs-lookup"><span data-stu-id="633c8-810">When searching `searchable` fields, hello search text itself is tokenized, so multiple terms can be separated by white space (for example: `search=hello world`).</span></span> <span data-ttu-id="633c8-811">Użyj dowolnej termin toomatch `*` (może to być przydatne dla zapytań filtr wartości logicznych).</span><span class="sxs-lookup"><span data-stu-id="633c8-811">toomatch any term, use `*` (this can be useful for boolean filter queries).</span></span> <span data-ttu-id="633c8-812">Pominięcie tego parametru jest hello efektu takie same jak opcja zbyt`*`.</span><span class="sxs-lookup"><span data-stu-id="633c8-812">Omitting this parameter has hello same effect as setting it too`*`.</span></span> <span data-ttu-id="633c8-813">Zobacz [proste składnia zapytania](https://msdn.microsoft.com/library/dn798920.aspx) kątem specyfiki na powitania składni wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="633c8-813">See [Simple Query Syntax](https://msdn.microsoft.com/library/dn798920.aspx) for specifics on hello search syntax.</span></span>

* <span data-ttu-id="633c8-814">**Uwaga**: hello wyniki mogą być czasem zaskakująco podczas wykonywania zapytania za pośrednictwem `searchable` pola.</span><span class="sxs-lookup"><span data-stu-id="633c8-814">**Note**: hello results can sometimes be surprising when querying over `searchable` fields.</span></span> <span data-ttu-id="633c8-815">tokenizator Hello zawiera logikę toohandle przypadków wspólnej tooEnglish tekst apostrofy, przecinki w numery itp. Na przykład `search=123,456` będzie odpowiadała pojedynczy termin 123,456 zamiast poszczególnych warunków hello 123 i 456, ponieważ przecinki są używane jako separatory tysięcy dużą liczbą w języku angielskim.</span><span class="sxs-lookup"><span data-stu-id="633c8-815">hello tokenizer includes logic toohandle cases common tooEnglish text like apostrophes, commas in numbers, etc. For example, `search=123,456` will match a single term 123,456 rather than hello individual terms 123 and 456, since commas are used as thousand-separators for large numbers in English.</span></span> <span data-ttu-id="633c8-816">Z tego powodu zaleca się używanie zamiast znaków interpunkcyjnych tooseparate warunki biały znak w hello `search` parametru.</span><span class="sxs-lookup"><span data-stu-id="633c8-816">For this reason, we recommend using white space rather than punctuation tooseparate terms in hello `search` parameter.</span></span>

<span data-ttu-id="633c8-817">`searchMode=any|all`(opcjonalne, domyślnie przyjmowana jest zbyt`any`) — czy niektóre lub wszystkie z warunkami wyszukiwania hello muszą być zgodne w kolejności toocount hello dokumentu jako dopasowanie.</span><span class="sxs-lookup"><span data-stu-id="633c8-817">`searchMode=any|all` (optional, defaults too`any`) - whether any or all of hello search terms must be matched in order toocount hello document as a match.</span></span>

<span data-ttu-id="633c8-818">`searchFields=[string]`(opcjonalnie) - hello lista toosearch nazw pól rozdzielonych przecinkami dla hello określony tekst.</span><span class="sxs-lookup"><span data-stu-id="633c8-818">`searchFields=[string]` (optional) - hello list of comma-separated field names toosearch for hello specified text.</span></span> <span data-ttu-id="633c8-819">Pola docelowe muszą być oznaczone jako `searchable`.</span><span class="sxs-lookup"><span data-stu-id="633c8-819">Target fields must be marked as `searchable`.</span></span>

<span data-ttu-id="633c8-820">`queryType=simple|full`(opcjonalne, domyślnie przyjmowana jest zbyt`simple`) — w przypadku zestawu zbyt "prosta" wyszukiwany tekst jest interpretowana przy użyciu języka prostego zapytania, który zezwala na symbole, takich jak +, * oraz "".</span><span class="sxs-lookup"><span data-stu-id="633c8-820">`queryType=simple|full` (optional, defaults too`simple`) - when set too"simple" search text is interpreted using a simple query language that allows for symbols such as +, * and "".</span></span> <span data-ttu-id="633c8-821">Zapytania są oceniane przez wszystkie pola z możliwością przeszukiwania (lub pól wskazaną w `searchFields`) do każdego dokumentu domyślnie.</span><span class="sxs-lookup"><span data-stu-id="633c8-821">Queries are evaluated across all searchable fields (or fields indicated in `searchFields`) in each document by default.</span></span> <span data-ttu-id="633c8-822">Gdy typ zapytania hello ustawiono zbyt`full` przy użyciu języka zapytań Lucene hello, który umożliwia wyszukiwanie określonego pola i ważoną interpretowany tekst do wyszukania.</span><span class="sxs-lookup"><span data-stu-id="633c8-822">When hello query type is set too`full` search text is interpreted using hello Lucene query language which allows field-specific and weighted searches.</span></span> <span data-ttu-id="633c8-823">Zobacz [proste składnia zapytania](https://msdn.microsoft.com/library/dn798920.aspx) i [składnia zapytań Lucene](https://msdn.microsoft.com/library/mt589323.aspx) kątem specyfiki na powitania składni wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="633c8-823">See [Simple Query Syntax](https://msdn.microsoft.com/library/dn798920.aspx) and [Lucene Query Syntax](https://msdn.microsoft.com/library/mt589323.aspx) for specifics on hello search syntaxes.</span></span> 

> [!NOTE]
> <span data-ttu-id="633c8-824">Zakres wyszukiwania w hello Lucene język kwerendy nie jest obsługiwany na rzecz $filter, która oferuje podobne funkcje.</span><span class="sxs-lookup"><span data-stu-id="633c8-824">Range search in hello Lucene query language is not supported in favor of $filter which offers similar functionality.</span></span>
> 
> 

<span data-ttu-id="633c8-825">`moreLikeThis=[key]`(opcjonalnie) **Ważne:** ta funkcja jest dostępna tylko w `2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="633c8-825">`moreLikeThis=[key]` (optional) **Important:** This feature is only available in `2015-02-28-Preview`.</span></span> <span data-ttu-id="633c8-826">Ta opcja nie można użyć w zapytaniu, które zawiera parametr wyszukiwania tekstu hello, `search=[string]`.</span><span class="sxs-lookup"><span data-stu-id="633c8-826">This option cannot be used in a query that contains hello text search parameter, `search=[string]`.</span></span> <span data-ttu-id="633c8-827">Witaj `moreLikeThis` parametru znajduje dokumenty, które są podobne dokument toohello określony przez klucz dokumentu hello.</span><span class="sxs-lookup"><span data-stu-id="633c8-827">hello `moreLikeThis` parameter finds documents that are similar toohello document specified by hello document key.</span></span> <span data-ttu-id="633c8-828">Po wysłaniu żądania wyszukiwania z `moreLikeThis`, listę terminy wyszukiwania jest generowany na podstawie częstotliwości hello i rzadkość terminów w dokumencie źródłowym hello.</span><span class="sxs-lookup"><span data-stu-id="633c8-828">When a search request is made with `moreLikeThis`, a list of search terms is generated based on hello frequency and rarity of terms in hello source document.</span></span> <span data-ttu-id="633c8-829">Te warunki są następnie używane toomake hello żądania.</span><span class="sxs-lookup"><span data-stu-id="633c8-829">Those terms are then used toomake hello request.</span></span> <span data-ttu-id="633c8-830">Domyślnie program hello zawartość wszystkich `searchable` pola są traktowane jako, chyba że `searchFields` jest używane toorestrict pola, które będą wyszukiwane.</span><span class="sxs-lookup"><span data-stu-id="633c8-830">By default, hello contents of all `searchable` fields are considered unless `searchFields` is used toorestrict which fields are searched.</span></span>  

<span data-ttu-id="633c8-831">`$skip=#`(opcjonalnie) — liczba hello wyszukiwania powoduje tooskip; Nie może być większa niż 100 000.</span><span class="sxs-lookup"><span data-stu-id="633c8-831">`$skip=#` (optional) - hello number of search results tooskip; Cannot be greater than 100,000.</span></span> <span data-ttu-id="633c8-832">Jeśli konieczne tooscan dokumentów w sekwencji, ale nie można użyć `$skip` ze względu na ograniczenia toothis należy rozważyć użycie `$orderby` na kluczu całkowicie uporządkowane i `$filter` zakres zamiast tego zapytania.</span><span class="sxs-lookup"><span data-stu-id="633c8-832">If you need tooscan documents in sequence but cannot use `$skip` due toothis limitation, consider using `$orderby` on a totally-ordered key and `$filter` with a range query instead.</span></span>

> [!NOTE]
> <span data-ttu-id="633c8-833">Podczas wywoływania metody **wyszukiwania** używanie żądania POST, ten parametr nosi nazwę `skip` zamiast `$skip`.</span><span class="sxs-lookup"><span data-stu-id="633c8-833">When calling **Search** using POST, this parameter is named `skip` instead of `$skip`.</span></span>
> 
> 

<span data-ttu-id="633c8-834">`$top=#`(opcjonalnie) - tooretrieve powoduje hello liczba wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="633c8-834">`$top=#` (optional) - hello number of search results tooretrieve.</span></span> <span data-ttu-id="633c8-835">Może być używany w połączeniu z `$skip` tooimplement po stronie klienta stronicowania wyników wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="633c8-835">This can be used in conjunction with `$skip` tooimplement client-side paging of search results.</span></span>

> [!NOTE]
> <span data-ttu-id="633c8-836">Podczas wywoływania metody **wyszukiwania** używanie żądania POST, ten parametr nosi nazwę `top` zamiast `$top`.</span><span class="sxs-lookup"><span data-stu-id="633c8-836">When calling **Search** using POST, this parameter is named `top` instead of `$top`.</span></span>
> 
> 

<span data-ttu-id="633c8-837">`$count=true|false`(opcjonalne, domyślnie przyjmowana jest zbyt`false`) — określa, czy toofetch hello łącznej liczby wyników.</span><span class="sxs-lookup"><span data-stu-id="633c8-837">`$count=true|false` (optional, defaults too`false`) - Specifies whether toofetch hello total count of results.</span></span> <span data-ttu-id="633c8-838">Jest to liczba hello wszystkie dokumenty, które odpowiadają hello `search` i `$filter` parametrów, ignorowanie `$top` i `$skip`.</span><span class="sxs-lookup"><span data-stu-id="633c8-838">This is hello count of all documents that match hello `search` and `$filter` parameters, ignoring `$top` and `$skip`.</span></span> <span data-ttu-id="633c8-839">Ustawienie tej wartości zbyt`true` może mieć negatywny wpływ na wydajność.</span><span class="sxs-lookup"><span data-stu-id="633c8-839">Setting this value too`true` may have a performance impact.</span></span> <span data-ttu-id="633c8-840">Należy pamiętać, że liczba hello zwracane wartości.</span><span class="sxs-lookup"><span data-stu-id="633c8-840">Note that hello count returned is an approximation.</span></span>

> [!NOTE]
> <span data-ttu-id="633c8-841">Podczas wywoływania metody **wyszukiwania** używanie żądania POST, ten parametr nosi nazwę `count` zamiast `$count`.</span><span class="sxs-lookup"><span data-stu-id="633c8-841">When calling **Search** using POST, this parameter is named `count` instead of `$count`.</span></span>
> 
> 

<span data-ttu-id="633c8-842">`$orderby=[string]`(opcjonalnie) — lista wyrażeń oddzielonych przecinkami toosort hello wyniki według.</span><span class="sxs-lookup"><span data-stu-id="633c8-842">`$orderby=[string]` (optional) - A list of comma-separated expressions toosort hello results by.</span></span> <span data-ttu-id="633c8-843">Każde wyrażenie może być nazwą pola lub toohello wywołania `geo.distance()` funkcji.</span><span class="sxs-lookup"><span data-stu-id="633c8-843">Each expression can be either a field name or a call toohello `geo.distance()` function.</span></span> <span data-ttu-id="633c8-844">Każde wyrażenie może następować `asc` tooindicated rosnącej, i `desc` tooindicate malejąco.</span><span class="sxs-lookup"><span data-stu-id="633c8-844">Each expression can be followed by `asc` tooindicated ascending, and `desc` tooindicate descending.</span></span> <span data-ttu-id="633c8-845">domyślne Hello jest rosnącą.</span><span class="sxs-lookup"><span data-stu-id="633c8-845">hello default is ascending order.</span></span> <span data-ttu-id="633c8-846">Grup równych wartości będą podziałem hello dopasowania wyników dokumentów.</span><span class="sxs-lookup"><span data-stu-id="633c8-846">Ties will be broken by hello match scores of documents.</span></span> <span data-ttu-id="633c8-847">Jeśli nie `$orderby` określono hello domyślną kolejność sortowania jest malejąco według dokumentu dopasowania wyników.</span><span class="sxs-lookup"><span data-stu-id="633c8-847">If no `$orderby` is specified, hello default sort order is descending by document match score.</span></span> <span data-ttu-id="633c8-848">Istnieje limit 32 klauzule dotyczące `$orderby`.</span><span class="sxs-lookup"><span data-stu-id="633c8-848">There is a limit of 32 clauses for `$orderby`.</span></span>

> [!NOTE]
> <span data-ttu-id="633c8-849">Podczas wywoływania metody **wyszukiwania** używanie żądania POST, ten parametr nosi nazwę `orderby` zamiast `$orderby`.</span><span class="sxs-lookup"><span data-stu-id="633c8-849">When calling **Search** using POST, this parameter is named `orderby` instead of `$orderby`.</span></span>
> 
> 

<span data-ttu-id="633c8-850">`$select=[string]`(opcjonalnie) — lista tooretrieve pól rozdzielonych przecinkami.</span><span class="sxs-lookup"><span data-stu-id="633c8-850">`$select=[string]` (optional) - A list of comma-separated fields tooretrieve.</span></span> <span data-ttu-id="633c8-851">Jeśli zostanie określona, wszystkie pola oznaczone jako pobieranie w schemacie hello są dołączone.</span><span class="sxs-lookup"><span data-stu-id="633c8-851">If unspecified, all fields marked as retrievable in hello schema are included.</span></span> <span data-ttu-id="633c8-852">Można również jawnie żądania wszystkie pola przez ustawienie tego parametru zbyt`*`.</span><span class="sxs-lookup"><span data-stu-id="633c8-852">You can also explicitly request all fields by setting this parameter too`*`.</span></span>

> [!NOTE]
> <span data-ttu-id="633c8-853">Podczas wywoływania metody **wyszukiwania** używanie żądania POST, ten parametr nosi nazwę `select` zamiast `$select`.</span><span class="sxs-lookup"><span data-stu-id="633c8-853">When calling **Search** using POST, this parameter is named `select` instead of `$select`.</span></span>
> 
> 

<span data-ttu-id="633c8-854">`facet=[string]`(zero lub więcej) - toofacet pole, według.</span><span class="sxs-lookup"><span data-stu-id="633c8-854">`facet=[string]` (zero or more) - A field toofacet by.</span></span> <span data-ttu-id="633c8-855">Opcjonalnie ciąg hello mogą zawierać parametrów toocustomize hello tworzenie aspektów wyrażonej w postaci rozdzielanej przecinkami `name:value` pary.</span><span class="sxs-lookup"><span data-stu-id="633c8-855">Optionally hello string may contain parameters toocustomize hello faceting expressed as comma-separated `name:value` pairs.</span></span> <span data-ttu-id="633c8-856">Prawidłowe parametry to:</span><span class="sxs-lookup"><span data-stu-id="633c8-856">Valid parameters are:</span></span>

* <span data-ttu-id="633c8-857">`count`(maksymalna liczba warunki aspektu; domyślna wynosi 10).</span><span class="sxs-lookup"><span data-stu-id="633c8-857">`count` (max number of facet terms; default is 10).</span></span> <span data-ttu-id="633c8-858">Nie jest brak maksimum, ale wyższe wartości pociągnąć za sobą odpowiednie spadek wydajności, szczególnie w przypadku, gdy pole aspektowej hello zawiera dużą liczbę unikatowych warunki.</span><span class="sxs-lookup"><span data-stu-id="633c8-858">There is no maximum, but higher values incur a corresponding performance penalty, especially if hello faceted field contains a large number of unique terms.</span></span>
  * <span data-ttu-id="633c8-859">Na przykład: `facet=category,count:5` pobiera hello top pięć kategorii w wynikach zestawu reguł.</span><span class="sxs-lookup"><span data-stu-id="633c8-859">For example: `facet=category,count:5` gets hello top five categories in facet results.</span></span>  
  * <span data-ttu-id="633c8-860">**Uwaga**: Jeśli hello `count` parametrów jest mniejsza niż liczba hello unikatowy warunków, hello wyniki mogą być niedokładne.</span><span class="sxs-lookup"><span data-stu-id="633c8-860">**Note**: If hello `count` parameter is less than hello number of unique terms, hello results may not be accurate.</span></span> <span data-ttu-id="633c8-861">Jest to ze względu na sposób toohello tworzenie aspektów zapytania rozproszone na fragmentów.</span><span class="sxs-lookup"><span data-stu-id="633c8-861">This is due toohello way faceting queries are distributed across shards.</span></span> <span data-ttu-id="633c8-862">Zwiększenie `count` zwykle zwiększa hello dokładność hello określenie liczby, ale na zmniejszenie wydajności.</span><span class="sxs-lookup"><span data-stu-id="633c8-862">Increasing `count` generally increases hello accuracy of hello term counts, but at a performance cost.</span></span>
* <span data-ttu-id="633c8-863">`sort`(jeden z `count` toosort *malejąco* według liczby, `-count` toosort *rosnącej* według liczby, `value` toosort *rosnącej* wg wartości, lub `-value` toosort *malejąco* przez wartość)</span><span class="sxs-lookup"><span data-stu-id="633c8-863">`sort` (one of `count` toosort *descending* by count, `-count` toosort *ascending* by count, `value` toosort *ascending* by value, or `-value` toosort *descending* by value)</span></span>
  * <span data-ttu-id="633c8-864">Na przykład: `facet=category,count:3,sort:count` pobiera hello top trzy kategorie w wynikach aspektu w kolejności malejącej według hello liczba dokumentów z każdym nazwę miejscowości.</span><span class="sxs-lookup"><span data-stu-id="633c8-864">For example: `facet=category,count:3,sort:count` gets hello top three categories in facet results in descending order by hello number of documents with each city name.</span></span> <span data-ttu-id="633c8-865">Na przykład hello top trzy kategorie są budżetu, Motel i możliwość zaprojektowania kątem zabezpieczeń i budżetu ma 5 trafień Motel ma 6, przez co 4 ma możliwość zaprojektowania kątem zabezpieczeń, hello pakiety zostaną w kolejności hello Motel, budżetu, możliwość zaprojektowania kątem zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="633c8-865">For example, if hello top three categories are Budget, Motel, and Luxury, and Budget has 5 hits, Motel has 6, and Luxury has 4, then hello buckets will be in hello order Motel, Budget, Luxury.</span></span>
  * <span data-ttu-id="633c8-866">Na przykład: `facet=rating,sort:-value` tworzy zasobników dla wszystkich możliwych klasyfikacje, w kolejności malejącej według wartości.</span><span class="sxs-lookup"><span data-stu-id="633c8-866">For example: `facet=rating,sort:-value` produces buckets for all possible ratings, in descending order by value.</span></span> <span data-ttu-id="633c8-867">Na przykład w przypadku klasyfikacji hello z 1 too5, zasobników hello będzie można porządkować 5, 4, 3, 2, 1, niezależnie od liczby dokumentów odpowiada każdej klasyfikacji.</span><span class="sxs-lookup"><span data-stu-id="633c8-867">For example, if hello ratings are from 1 too5, hello buckets will be ordered 5, 4, 3, 2, 1, irrespective of how many documents match each rating.</span></span>
* <span data-ttu-id="633c8-868">`values`(rozdzielany potoku liczbowe lub `Edm.DateTimeOffset` wartości określających zestawu dynamicznego aspektu wpis wartości)</span><span class="sxs-lookup"><span data-stu-id="633c8-868">`values` (pipe-delimited numeric or `Edm.DateTimeOffset` values specifying a dynamic set of facet entry values)</span></span>
  * <span data-ttu-id="633c8-869">Na przykład: `facet=baseRate,values:10|20` tworzy trzech zasobników: jeden dla podstawowej szybkość 0 się toobut wyłączeniem 10, co 10 się toobut bez uwzględniania 20 i jeden dla 20 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="633c8-869">For example: `facet=baseRate,values:10|20` produces three buckets: One for base rate 0 up toobut not including 10, one for 10 up toobut not including 20, and one for 20 or higher.</span></span>
  * <span data-ttu-id="633c8-870">Na przykład: `facet=lastRenovationDate,values:2010-02-01T00:00:00Z` tworzy dwa zasobników: jeden dla hotele renovated przed lutego 2010 i drugi dla hotele renovated lutego 1, 2010 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="633c8-870">For example: `facet=lastRenovationDate,values:2010-02-01T00:00:00Z` produces two buckets: One for hotels renovated before February 2010, and one for hotels renovated February 1st, 2010 or later.</span></span>
* <span data-ttu-id="633c8-871">`interval`(interwał liczbą całkowitą większą niż 0 w przypadku numerów lub `minute`, `hour`, `day`, `week`, `month`, `quarter`, `year` dla wartości czasu Data)</span><span class="sxs-lookup"><span data-stu-id="633c8-871">`interval` (integer interval greater than 0 for numbers, or `minute`, `hour`, `day`, `week`, `month`, `quarter`, `year` for date time values)</span></span>
  * <span data-ttu-id="633c8-872">Na przykład: `facet=baseRate,interval:100` tworzy pakiety na podstawie współczynnika podstawowej zakresów rozmiaru 100.</span><span class="sxs-lookup"><span data-stu-id="633c8-872">For example: `facet=baseRate,interval:100` produces buckets based on base rate ranges of size 100.</span></span> <span data-ttu-id="633c8-873">Na przykład jeżeli stawki podstawowe są wszystkie między 60 $ i $600, będzie zasobników 0-100, 100 – 200, 200 300, 300 400, 400 500 i 500 600.</span><span class="sxs-lookup"><span data-stu-id="633c8-873">For example, if base rates are all between $60 and $600, there will be buckets for 0-100, 100-200, 200-300, 300-400, 400-500, and 500-600.</span></span>
  * <span data-ttu-id="633c8-874">Na przykład: `facet=lastRenovationDate,interval:year` tworzy jeden zasobnik dla każdego roku po zostały renovated hotels.</span><span class="sxs-lookup"><span data-stu-id="633c8-874">For example: `facet=lastRenovationDate,interval:year` produces one bucket for each year when hotels were renovated.</span></span>
* <span data-ttu-id="633c8-875">`timeoffset`([+-] hh: mm, [+-] hh: mm, lub [+-] hh) `timeoffset` jest opcjonalna.</span><span class="sxs-lookup"><span data-stu-id="633c8-875">`timeoffset` ([+-]hh:mm, [+-]hhmm, or [+-]hh) `timeoffset` is optional.</span></span> <span data-ttu-id="633c8-876">Można połączyć tylko z hello `interval` opcja i tylko wtedy, gdy zastosowane tooa pola typu `Edm.DateTimeOffset`.</span><span class="sxs-lookup"><span data-stu-id="633c8-876">It can only be combined with hello `interval` option, and only when applied tooa field of type `Edm.DateTimeOffset`.</span></span> <span data-ttu-id="633c8-877">wartość Hello określa tooaccount przesunięcia czasu hello UTC dla podczas ustawiania granic godziny.</span><span class="sxs-lookup"><span data-stu-id="633c8-877">hello value specifies hello UTC time offset tooaccount for in setting time boundaries.</span></span>
  * <span data-ttu-id="633c8-878">Na przykład: `facet=lastRenovationDate,interval:day,timeoffset:-01:00` używa hello granic dzień, która rozpoczyna się od 01:00:00 czasu UTC (północ w strefie czasowej hello docelowych)</span><span class="sxs-lookup"><span data-stu-id="633c8-878">For example: `facet=lastRenovationDate,interval:day,timeoffset:-01:00` uses hello day boundary that starts at 01:00:00 UTC (midnight in hello target time zone)</span></span>
* <span data-ttu-id="633c8-879">**Uwaga**: `count` i `sort` mogą być łączone w hello sam specyfikacji zestawu reguł, ale nie można połączyć z `interval` lub `values`, i `interval` i `values` nie można łączyć ze sobą.</span><span class="sxs-lookup"><span data-stu-id="633c8-879">**Note**: `count` and `sort` can be combined in hello same facet specification, but they cannot be combined with `interval` or `values`, and `interval` and `values` cannot be combined together.</span></span>
* <span data-ttu-id="633c8-880">**Uwaga**: interwał zestawów reguł Data i godzina są obliczane na podstawie czasu UTC, jeśli `timeoffset` nie jest określona.</span><span class="sxs-lookup"><span data-stu-id="633c8-880">**Note**: Interval facets on date time are computed based on UTC time if `timeoffset` is not specified.</span></span> <span data-ttu-id="633c8-881">Na przykład: dla `facet=lastRenovationDate,interval:day`, granic dzień hello rozpoczyna się od 00:00:00 czasu UTC.</span><span class="sxs-lookup"><span data-stu-id="633c8-881">For example: for `facet=lastRenovationDate,interval:day`, hello day boundary starts at 00:00:00 UTC.</span></span> 

> [!NOTE]
> <span data-ttu-id="633c8-882">Podczas wywoływania metody **wyszukiwania** używanie żądania POST, ten parametr nosi nazwę `facets` zamiast `facet`.</span><span class="sxs-lookup"><span data-stu-id="633c8-882">When calling **Search** using POST, this parameter is named `facets` instead of `facet`.</span></span> <span data-ttu-id="633c8-883">Ponadto można określić go jako tablica JSON ciągów, gdzie każdy ciąg jest wyrażenie oddzielne aspekt.</span><span class="sxs-lookup"><span data-stu-id="633c8-883">Also, you specify it as a JSON array of strings where each string is a separate facet expression.</span></span>
> 
> 

<span data-ttu-id="633c8-884">`$filter=[string]`(opcjonalnie) - strukturalnych wyrażenia w standardowej składni OData.</span><span class="sxs-lookup"><span data-stu-id="633c8-884">`$filter=[string]` (optional) - A structured search expression in standard OData syntax.</span></span>

> [!NOTE]
> <span data-ttu-id="633c8-885">Podczas wywoływania metody **wyszukiwania** używanie żądania POST, ten parametr nosi nazwę `filter` zamiast `$filter`.</span><span class="sxs-lookup"><span data-stu-id="633c8-885">When calling **Search** using POST, this parameter is named `filter` instead of `$filter`.</span></span>
> 
> 

<span data-ttu-id="633c8-886">`highlight=[string]`(opcjonalnie) - prezentuje zestaw stosowania trafień nazw pól rozdzielonych przecinkami.</span><span class="sxs-lookup"><span data-stu-id="633c8-886">`highlight=[string]` (optional) - A set of comma-separated field names used for hit highlights.</span></span> <span data-ttu-id="633c8-887">Tylko `searchable` pola mogą być używane dla wyróżnianie trafień.</span><span class="sxs-lookup"><span data-stu-id="633c8-887">Only `searchable` fields can be used for hit highlighting.</span></span>

<span data-ttu-id="633c8-888">`highlightPreTag=[string]`(opcjonalne, domyślnie przyjmowana jest zbyt`<em>`) — ciągu znaczników, które dołącza toohit najważniejsze funkcje.</span><span class="sxs-lookup"><span data-stu-id="633c8-888">`highlightPreTag=[string]` (optional, defaults too`<em>`) - A string tag that prepends toohit highlights.</span></span> <span data-ttu-id="633c8-889">Musi być ustawiona z `highlightPostTag`.</span><span class="sxs-lookup"><span data-stu-id="633c8-889">Must be set with `highlightPostTag`.</span></span>

> [!NOTE]
> <span data-ttu-id="633c8-890">Podczas wywoływania metody **wyszukiwania** przy użyciu GET, zarezerwowanych znaków w adresie URL hello musi być zakodowany procent (na przykład zamiast #, % 23).</span><span class="sxs-lookup"><span data-stu-id="633c8-890">When calling **Search** using GET, reserved characters in hello URL must be percent-encoded (for example, %23 instead of #).</span></span>
> 
> 

<span data-ttu-id="633c8-891">`highlightPostTag=[string]`(opcjonalne, domyślnie przyjmowana jest zbyt`</em>`)-tag ciąg, który dołącza toohit najważniejsze funkcje.</span><span class="sxs-lookup"><span data-stu-id="633c8-891">`highlightPostTag=[string]` (optional, defaults too`</em>`) - a string tag that appends toohit highlights.</span></span> <span data-ttu-id="633c8-892">Musi być ustawiona z `highlightPreTag`.</span><span class="sxs-lookup"><span data-stu-id="633c8-892">Must be set with `highlightPreTag`.</span></span>

> [!NOTE]
> <span data-ttu-id="633c8-893">Podczas wywoływania metody **wyszukiwania** przy użyciu GET, zarezerwowanych znaków w adresie URL hello musi być zakodowany procent (na przykład zamiast #, % 23).</span><span class="sxs-lookup"><span data-stu-id="633c8-893">When calling **Search** using GET, reserved characters in hello URL must be percent-encoded (for example, %23 instead of #).</span></span>
> 
> 

<span data-ttu-id="633c8-894">`scoringProfile=[string]`(opcjonalnie) — nazwa hello oceniania tooevaluate profilu odpowiadać wyniki pasujące dokumenty w kolejności toosort hello wyników.</span><span class="sxs-lookup"><span data-stu-id="633c8-894">`scoringProfile=[string]` (optional) - hello name of a scoring profile tooevaluate match scores for matching documents in order toosort hello results.</span></span>

<span data-ttu-id="633c8-895">`scoringParameter=[string]`(zero lub więcej) — wskazuje hello wartości dla każdego parametru zdefiniowanego w funkcji oceniania (na przykład `referencePointParameter`) przy użyciu formatu hello `name-value1,value2,...`.</span><span class="sxs-lookup"><span data-stu-id="633c8-895">`scoringParameter=[string]` (zero or more) - Indicates hello values for each parameter defined in a scoring function (for example, `referencePointParameter`) using hello format `name-value1,value2,...`.</span></span>

* <span data-ttu-id="633c8-896">Na przykład jeśli hello profilu oceniania definiuje funkcję z parametr o nazwie opcja ciągu zapytania hello "mylocation" będzie `&scoringParameter=mylocation--122.2,44.8`.</span><span class="sxs-lookup"><span data-stu-id="633c8-896">For example, if hello scoring profile defines a function with a parameter called "mylocation" hello query string option would be `&scoringParameter=mylocation--122.2,44.8`.</span></span> <span data-ttu-id="633c8-897">dash pierwszy Hello oddziela hello nazwę z listy wartość hello podczas drugiego dash hello jest częścią hello pierwsza wartość (długości geograficznej, w tym przykładzie).</span><span class="sxs-lookup"><span data-stu-id="633c8-897">hello first dash separates hello name from hello value list, while hello second dash is part of hello first value (longitude in this example).</span></span>
* <span data-ttu-id="633c8-898">Oceniania parametrów, takich jak tagu zwiększanie wyniku, który może zawierać przecinków, można escape takie wartości, na liście hello przy użyciu apostrofy.</span><span class="sxs-lookup"><span data-stu-id="633c8-898">For scoring parameters such as for tag boosting that can contain commas, you can escape any such values in hello list using single quotes.</span></span> <span data-ttu-id="633c8-899">Jeśli same wartości hello zawierać pojedynczych cudzysłowów, możesz je escape przez wpisanie dwóch znaków.</span><span class="sxs-lookup"><span data-stu-id="633c8-899">If hello values themselves contain single quotes, you can escape them by doubling.</span></span>
  * <span data-ttu-id="633c8-900">Na przykład, jeśli masz tag zwiększania parametr o nazwie "mytag" i ma tooboost w tagu hello wartości "Hello, O'Brien" i "Smith", zapytanie hello będzie opcja ciągu `&scoringParameter=mytag-'Hello, O''Brien',Smith`.</span><span class="sxs-lookup"><span data-stu-id="633c8-900">For example, if you have a tag boosting parameter called "mytag" and you want tooboost on hello tag values "Hello, O'Brien" and "Smith", hello query string option would be `&scoringParameter=mytag-'Hello, O''Brien',Smith`.</span></span> <span data-ttu-id="633c8-901">Należy pamiętać, że cudzysłowy są tylko wartości zawierające przecinki wymagane.</span><span class="sxs-lookup"><span data-stu-id="633c8-901">Note that quotes are only required for values that contain commas.</span></span>

> [!NOTE]
> <span data-ttu-id="633c8-902">Podczas wywoływania metody **wyszukiwania** używanie żądania POST, ten parametr nosi nazwę `scoringParameters` zamiast `scoringParameter`.</span><span class="sxs-lookup"><span data-stu-id="633c8-902">When calling **Search** using POST, this parameter is named `scoringParameters` instead of `scoringParameter`.</span></span> <span data-ttu-id="633c8-903">Ponadto określić go jako tablica JSON ciągów, których każdy ciąg jest osobny `name-values` pary.</span><span class="sxs-lookup"><span data-stu-id="633c8-903">Also, you specify it as a JSON array of strings where each string is a separate `name-values` pair.</span></span>
> 
> 

<span data-ttu-id="633c8-904">`minimumCoverage`(opcjonalne, domyślnie przyjmowana jest too100) - liczbą z zakresu od 0 do 100 wskazujący procent hello hello indeksu, który musi być objęta zapytania wyszukiwania, aby toobe zapytania hello raportowane klientowi jako sukcesu.</span><span class="sxs-lookup"><span data-stu-id="633c8-904">`minimumCoverage` (optional, defaults too100) - a number between 0 and 100 indicating hello percentage of hello index that must be covered by a search query in order for hello query toobe reported as a success.</span></span> <span data-ttu-id="633c8-905">Domyślnie program hello całego indeksu musi być dostępny lub `Search` zwróci kod stanu HTTP 503.</span><span class="sxs-lookup"><span data-stu-id="633c8-905">By default, hello entire index must be available or `Search` will return HTTP status code 503.</span></span> <span data-ttu-id="633c8-906">Jeśli ustawisz `minimumCoverage` i `Search` zakończy się pomyślnie, zostanie zwrócić 200 protokołu HTTP i obejmują `@search.coverage` wartości w odpowiedzi hello wskazujący procent hello hello indeksu, który został uwzględniony w zapytaniu hello.</span><span class="sxs-lookup"><span data-stu-id="633c8-906">If you set `minimumCoverage` and `Search` succeeds, it will return HTTP 200 and include a `@search.coverage` value in hello response indicating hello percentage of hello index that was included in hello query.</span></span>

> [!NOTE]
> <span data-ttu-id="633c8-907">Ustawienie tej wartości tooa parametru mniejsze niż 100 mogą być przydatne dla zapewnienia dostępności wyszukiwania nawet w przypadku usług z tylko jedną replikę.</span><span class="sxs-lookup"><span data-stu-id="633c8-907">Setting this parameter tooa value lower than 100 can be useful for ensuring search availability even for services with only one replica.</span></span> <span data-ttu-id="633c8-908">Jednak nie wszystkie dokumenty pasujące dotrą toobe obecne w wynikach wyszukiwania hello.</span><span class="sxs-lookup"><span data-stu-id="633c8-908">However, not all matching documents are guaranteed toobe present in hello search results.</span></span> <span data-ttu-id="633c8-909">Jeśli odwołanie wyszukiwania jest ważniejsze aplikacja tooyour od dostępności, a następnie jest najlepszym tooleave `minimumCoverage` przy domyślnej wartości 100.</span><span class="sxs-lookup"><span data-stu-id="633c8-909">If search recall is more important tooyour application than availability, then it's best tooleave `minimumCoverage` at its default value of 100.</span></span>
> 
> 

<span data-ttu-id="633c8-910">`api-version=[string]`(wymagane).</span><span class="sxs-lookup"><span data-stu-id="633c8-910">`api-version=[string]` (required).</span></span> <span data-ttu-id="633c8-911">Wersja zapoznawcza Hello jest `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="633c8-911">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="633c8-912">Zobacz [przechowywanie wersji usługi wyszukiwania](http://msdn.microsoft.com/library/azure/dn864560.aspx) szczegółowe informacje i alternatywne wersje.</span><span class="sxs-lookup"><span data-stu-id="633c8-912">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="633c8-913">Uwaga: Ta operacja hello `api-version` jest określony jako parametr zapytania w adresie URL hello niezależnie od tego, czy wywołać **wyszukiwania** z GET lub POST.</span><span class="sxs-lookup"><span data-stu-id="633c8-913">Note: For this operation, hello `api-version` is specified as a query parameter in hello URL regardless of whether you call **Search** with GET or POST.</span></span>

<span data-ttu-id="633c8-914">**Nagłówki żądania**</span><span class="sxs-lookup"><span data-stu-id="633c8-914">**Request Headers**</span></span>

<span data-ttu-id="633c8-915">powitania po liście opisano hello wymagane i opcjonalne żądania nagłówków.</span><span class="sxs-lookup"><span data-stu-id="633c8-915">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="633c8-916">`api-key`: hello `api-key` jest używane tooauthenticate hello żądania tooyour usługi wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="633c8-916">`api-key`: hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="633c8-917">Jest to wartość ciągu tooyour unikatowy adres URL usługi.</span><span class="sxs-lookup"><span data-stu-id="633c8-917">It is a string value, unique tooyour service URL.</span></span> <span data-ttu-id="633c8-918">Witaj **wyszukiwania** żądania można podać klucz administratora lub klucz zapytania dla `api-key`.</span><span class="sxs-lookup"><span data-stu-id="633c8-918">hello **Search** request can specify either an admin key or query key for `api-key`.</span></span>

<span data-ttu-id="633c8-919">Należy również adres URL hello usługi nazwa tooconstruct hello żądania.</span><span class="sxs-lookup"><span data-stu-id="633c8-919">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="633c8-920">Można uzyskać nazwy usługi hello i `api-key` z pulpitu nawigacyjnego usługi w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="633c8-920">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="633c8-921">Zobacz [Tworzenie usługi Azure Search w portalu hello](search-create-service-portal.md) dla pomocy nawigacji strony.</span><span class="sxs-lookup"><span data-stu-id="633c8-921">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="633c8-922">**Treść żądania**</span><span class="sxs-lookup"><span data-stu-id="633c8-922">**Request Body**</span></span>

<span data-ttu-id="633c8-923">Get: Brak.</span><span class="sxs-lookup"><span data-stu-id="633c8-923">For GET: None.</span></span>

<span data-ttu-id="633c8-924">W przypadku żądania POST:</span><span class="sxs-lookup"><span data-stu-id="633c8-924">For POST:</span></span>

    {
      "count": true | false (default),
      "facets": [ "facet_expression_1", "facet_expression_2", ... ],
      "filter": "odata_filter_expression",
      "highlight": "highlight_field_1, highlight_field_2, ...",
      "highlightPreTag": "pre_tag",
      "highlightPostTag": "post_tag",
      "minimumCoverage": # (% of index that must be covered toodeclare query successful; default 100),
      "moreLikeThis": "document_key" (mutually exclusive with "search" parameter),
      "orderby": "orderby_expression",
      "scoringParameters": [ "scoring_parameter_1", "scoring_parameter_2", ... ],
      "scoringProfile": "scoring_profile_name",
      "search": "simple_query_expression",
      "searchFields": "field_name_1, field_name_2, ...",
      "searchMode": "any" (default) | "all",
      "select": "field_name_1, field_name_2, ...",
      "skip": # (default 0),
      "top": #
    }

<span data-ttu-id="633c8-925">**Kontynuacji Search częściowej odpowiedzi**</span><span class="sxs-lookup"><span data-stu-id="633c8-925">**Continuation of Partial Search Responses**</span></span>

<span data-ttu-id="633c8-926">Czasami usługi Azure Search nie może zwracać wszystkie hello żądanych wyników w jednej odpowiedzi wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="633c8-926">Sometimes Azure Search can't return all hello requested results in a single Search response.</span></span> <span data-ttu-id="633c8-927">Możliwe są różne przyczyny, na przykład gdy zapytanie hello żąda zbyt wiele dokumentów, nie określając `$top` lub podanie wartości `$top` jest zbyt duży.</span><span class="sxs-lookup"><span data-stu-id="633c8-927">This can happen for different reasons, such as when hello query requests too many documents by not specifying `$top` or specifying a value for `$top` that is too large.</span></span> <span data-ttu-id="633c8-928">W takich przypadkach usługi Azure Search uwzględni hello `@odata.nextLink` adnotacji w treści odpowiedzi hello, a także `@search.nextPageParameters` Jeśli był to wysłanie żądania POST.</span><span class="sxs-lookup"><span data-stu-id="633c8-928">In such cases, Azure Search will include hello `@odata.nextLink` annotation in hello response body, and also `@search.nextPageParameters` if it was a POST request.</span></span> <span data-ttu-id="633c8-929">Hello wartości tych tooformulate adnotacje można użyć innego wyszukiwania żądania tooget hello następnej części hello odpowiedzi wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="633c8-929">You can use hello values of these annotations tooformulate another Search request tooget hello next part of hello search response.</span></span> <span data-ttu-id="633c8-930">Ta metoda jest wywoływana ***kontynuacji*** hello oryginalnego żądania wyszukiwania i hello adnotacje są zwykle nazywane ***tokeny kontynuacji***.</span><span class="sxs-lookup"><span data-stu-id="633c8-930">This is called a ***continuation*** of hello original Search request, and hello annotations are generally called ***continuation tokens***.</span></span> <span data-ttu-id="633c8-931">Zobacz [w poniższym przykładzie hello](#SearchResponse) szczegółowe informacje na temat składni hello adnotacje i gdy pojawią się one w treści odpowiedzi na powitania.</span><span class="sxs-lookup"><span data-stu-id="633c8-931">See [hello example below](#SearchResponse) for details on hello syntax of these annotations and where they appear in hello response body.</span></span> 

<span data-ttu-id="633c8-932">Dlaczego usługi Azure Search może zwrócić tokeny kontynuacji powodów Hello są toochange konkretnej implementacji i temat.</span><span class="sxs-lookup"><span data-stu-id="633c8-932">hello reasons why Azure Search might return continuation tokens are implementation-specific and subject toochange.</span></span> <span data-ttu-id="633c8-933">Niezawodne klientów należy zawsze toohandle gotowy przypadki są zwracane dokumenty mniej niż oczekiwany token kontynuacji jest dołączony toocontinue pobierania dokumentów.</span><span class="sxs-lookup"><span data-stu-id="633c8-933">Robust clients should always be ready toohandle cases where fewer documents than expected are returned and a continuation token is included toocontinue retrieving documents.</span></span> <span data-ttu-id="633c8-934">Ponadto należy pamiętać, że należy użyć hello tej samej metody HTTP jako hello oryginalnego żądania w kolejności toocontinue.</span><span class="sxs-lookup"><span data-stu-id="633c8-934">Also note that you must use hello same HTTP method as hello original request in order toocontinue.</span></span> <span data-ttu-id="633c8-935">Na przykład, jeśli wysłano żądanie GET żądań kontynuacji wysyłania należy również użyć GET (i podobnie w przypadku żądania POST).</span><span class="sxs-lookup"><span data-stu-id="633c8-935">For example, if you sent a GET request, any continuation requests you send must also use GET (and likewise for POST).</span></span>

<span data-ttu-id="633c8-936"><a name="SearchResponse"></a>
**Odpowiedź**</span><span class="sxs-lookup"><span data-stu-id="633c8-936"><a name="SearchResponse"></a>
**Response**</span></span>

<span data-ttu-id="633c8-937">Kod stanu: 200 OK jest zwracana dla pomyślnej odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="633c8-937">Status Code: 200 OK is returned for a successful response.</span></span>

    {
      "@odata.count": # (if $count=true was provided in hello query),
      "@search.coverage": # (if minimumCoverage was provided in hello query),
      "@search.facets": { (if faceting was specified in hello query)
        "facet_field": [
          {
            "value": facet_entry_value (for non-range facets),
            "from": facet_entry_value (for range facets),
            "to": facet_entry_value (for range facets),
            "count": number_of_documents
          }
        ],
        ...
      },
      "@search.nextPageParameters": { (request body toofetch hello next page of results if not all results could be returned in this response and Search was called with POST)
        "count": ... (value from request body if present),
        "facets": ... (value from request body if present),
        "filter": ... (value from request body if present),
        "highlight": ... (value from request body if present),
        "highlightPreTag": ... (value from request body if present),
        "highlightPostTag": ... (value from request body if present),
        "minimumCoverage": ... (value from request body if present),
        "moreLikeThis": ... (value from request body if present),
        "orderby": ... (value from request body if present),
        "scoringParameters": ... (value from request body if present),
        "scoringProfile": ... (value from request body if present),
        "search": ... (value from request body if present),
        "searchFields": ... (value from request body if present),
        "searchMode": ... (value from request body if present),
        "select": ... (value from request body if present),
        "skip": ... (page size plus value from request body if present),
        "top": ... (value from request body if present minus page size),
      },
      "value": [
        {
          "@search.score": document_score (if a text query was provided),
          "@search.highlights": {
            field_name: [ subset of text, ... ],
            ...
          },
          key_field_name: document_key,
          field_name: field_value (retrievable fields or specified projection),
          ...
        },
        ...
      ],
      "@odata.nextLink": (URL toofetch hello next page of results if not all results could be returned in this response; Applies tooboth GET and POST)
    }

<span data-ttu-id="633c8-938">**Przykłady:**</span><span class="sxs-lookup"><span data-stu-id="633c8-938">**Examples:**</span></span>

<span data-ttu-id="633c8-939">Dodatkowe przykłady można znaleźć na powitania [OData składnia wyrażeń dla usługi Azure Search](https://msdn.microsoft.com/library/azure/dn798921.aspx) strony.</span><span class="sxs-lookup"><span data-stu-id="633c8-939">You can find additional examples on hello [OData Expression Syntax for Azure Search](https://msdn.microsoft.com/library/azure/dn798921.aspx) page.</span></span>

1)    <span data-ttu-id="633c8-940">Witaj wyszukiwania indeksu posortowanych malejąco według daty.</span><span class="sxs-lookup"><span data-stu-id="633c8-940">Search hello Index sorted descending by date.</span></span>

    <span data-ttu-id="633c8-941">GET /indexes/hotels/docs? wyszukiwania = * & $orderby = lastRenovationDate desc & api-version = 2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="633c8-941">GET /indexes/hotels/docs?search=*&$orderby=lastRenovationDate desc&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="633c8-942">POST /indexes/hotels/docs/search? api-version = 2015-02-28-Preview {"wyszukiwanie": "*", "orderby": "lastRenovationDate desc"}</span><span class="sxs-lookup"><span data-stu-id="633c8-942">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "orderby": "lastRenovationDate desc" }</span></span>

2)    <span data-ttu-id="633c8-943">W wyszukiwaniu aspektowej hello w indeksie i pobrać aspektów dla kategorii, klasyfikacji, tagi, a także elementy baseRate w określonych zakresach:</span><span class="sxs-lookup"><span data-stu-id="633c8-943">In a faceted search, search hello index and retrieve facets for categories, rating, tags, as well as items with baseRate in specific ranges:</span></span>

    <span data-ttu-id="633c8-944">GET /indexes/hotels/docs? wyszukiwania = test & aspektu = kategorii & aspektu = klasyfikacji & aspektu = tagi & aspektu = baseRate, wartości: 80 | 150 | 220 & api-version = 2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="633c8-944">GET /indexes/hotels/docs?search=test&facet=category&facet=rating&facet=tags&facet=baseRate,values:80|150|220&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="633c8-945">POST /indexes/hotels/docs/search? api-version = 2015-02-28-Preview {"wyszukiwanie": "test", "aspekty": ["kategorii", "klasyfikacji", "tagi", "baseRate, wartości: 80 | 150 | 220"]}</span><span class="sxs-lookup"><span data-stu-id="633c8-945">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "test", "facets": [ "category", "rating", "tags", "baseRate,values:80|150|220" ] }</span></span>

3)    <span data-ttu-id="633c8-946">Przy użyciu filtru, zawęzić wyniki zapytania aspektowej poprzedniego hello, po kliknięciu hello na ocena 3 kategorii "Motel":</span><span class="sxs-lookup"><span data-stu-id="633c8-946">Using a filter, narrow down hello previous faceted query results after hello user clicks on rating 3 and category "Motel":</span></span>

    <span data-ttu-id="633c8-947">GET /indexes/hotels/docs? wyszukiwania = test & aspektu = tagi & aspektu = baseRate, wartości: 80 | 150 | 220 & $filter = eq klasyfikacji 3 i eq kategorii "Motel" & api-version = 2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="633c8-947">GET /indexes/hotels/docs?search=test&facet=tags&facet=baseRate,values:80|150|220&$filter=rating eq 3 and category eq 'Motel'&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="633c8-948">POST /indexes/hotels/docs/search? api-version = 2015-02-28-Preview {"wyszukiwanie": "test", "aspekty": ["tagi", "baseRate, wartości: 80 | 150 | 220"], "filter": "eq klasyfikacji 3 i eq kategorii"Motel""}</span><span class="sxs-lookup"><span data-stu-id="633c8-948">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "test", "facets": [ "tags", "baseRate,values:80|150|220" ], "filter": "rating eq 3 and category eq 'Motel'" }</span></span>

4) <span data-ttu-id="633c8-949">W wyszukiwaniu aspektowej należy ustawić górny limit na warunkach unikatowy zwracane w kwerendzie.</span><span class="sxs-lookup"><span data-stu-id="633c8-949">In a faceted search, set an upper limit on unique terms returned in a query.</span></span> <span data-ttu-id="633c8-950">Witaj domyślna to 10, ale można zwiększyć lub zmniejszyć tę wartość przy użyciu hello `count` parametru na powitania `facet` atrybutu:</span><span class="sxs-lookup"><span data-stu-id="633c8-950">hello default is 10, but you can increase or decrease this value using hello `count` parameter on hello `facet` attribute:</span></span>

    <span data-ttu-id="633c8-951">GET /indexes/hotels/docs? wyszukiwania = test & aspektu = Miasto, liczba: 5 & api-version = 2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="633c8-951">GET /indexes/hotels/docs?search=test&facet=city,count:5&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="633c8-952">POST /indexes/hotels/docs/search? api-version = 2015-02-28-Preview {"wyszukiwanie": "test", "aspekty": ["Miasto, liczba: 5"]}</span><span class="sxs-lookup"><span data-stu-id="633c8-952">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview  {    "search": "test",    "facets": [ "city,count:5" ]  }</span></span>

5)    <span data-ttu-id="633c8-953">Witaj wyszukiwania indeksu w określonych pól; Na przykład pole specyficzny dla języka:</span><span class="sxs-lookup"><span data-stu-id="633c8-953">Search hello Index within specific fields; For example, a language-specific field:</span></span>

    <span data-ttu-id="633c8-954">GET /indexes/hotels/docs? wyszukiwania = hôtel & searchFields = description_fr & api-version = 2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="633c8-954">GET /indexes/hotels/docs?search=hôtel&searchFields=description_fr&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="633c8-955">POST /indexes/hotels/docs/search? api-version = 2015-02-28-Preview {"wyszukiwanie": "hôtel", "searchFields": "description_fr"}</span><span class="sxs-lookup"><span data-stu-id="633c8-955">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "hôtel", "searchFields": "description_fr" }</span></span>

6) <span data-ttu-id="633c8-956">Wyszukaj hello indeksu w wielu pól.</span><span class="sxs-lookup"><span data-stu-id="633c8-956">Search hello Index across multiple fields.</span></span> <span data-ttu-id="633c8-957">Na przykład można przechowywać i pola, w których kwerendy w wielu językach w ramach hello sam indeks.</span><span class="sxs-lookup"><span data-stu-id="633c8-957">For example, you can store and query searchable fields in multiple languages, all within hello same index.</span></span>  <span data-ttu-id="633c8-958">Jeśli opisy angielskim i francuskim współistnieć w hello sam dokumentu, można powrócić hello w dowolnych lub wszystkich wyników zapytania:</span><span class="sxs-lookup"><span data-stu-id="633c8-958">If English and French descriptions co-exist in hello same document, you can return any or all in hello query results:</span></span>

    <span data-ttu-id="633c8-959">GET /indexes/hotels/docs? wyszukiwania = hoteli & searchFields = opis, description_fr & api-version = 2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="633c8-959">GET /indexes/hotels/docs?search=hotel&searchFields=description,description_fr&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="633c8-960">POST /indexes/hotels/docs/search? api-version = 2015-02-28-Preview {"wyszukiwanie": "hoteli", "searchFields": "opis, description_fr"}</span><span class="sxs-lookup"><span data-stu-id="633c8-960">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview  {    "search": "hotel",    "searchFields": "description, description_fr"  }</span></span>

<span data-ttu-id="633c8-961">Należy pamiętać, można tylko kwerendę jeden indeks naraz.</span><span class="sxs-lookup"><span data-stu-id="633c8-961">Note that you can only query one index at a time.</span></span> <span data-ttu-id="633c8-962">Jeśli nie planujesz tooquery jednym naraz, nie należy tworzyć wiele indeksów dla każdego języka.</span><span class="sxs-lookup"><span data-stu-id="633c8-962">Do not create multiple indexes for each language unless you plan tooquery one at a time.</span></span>

7)    <span data-ttu-id="633c8-963">Stronicowanie - Get hello 1 strony elementów (rozmiar strony jest 10):</span><span class="sxs-lookup"><span data-stu-id="633c8-963">Paging - Get hello 1st page of items (page size is 10):</span></span>

    <span data-ttu-id="633c8-964">GET /indexes/hotels/docs? wyszukiwania = * & $skip = 0 & $top = 10 & api-version = 2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="633c8-964">GET /indexes/hotels/docs?search=*&$skip=0&$top=10&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="633c8-965">POST /indexes/hotels/docs/search? api-version = 2015-02-28-Preview {"wyszukiwanie": "*", "Pomiń": 0, "top": 10}</span><span class="sxs-lookup"><span data-stu-id="633c8-965">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "skip": 0, "top": 10 }</span></span>

8)    <span data-ttu-id="633c8-966">Stronicowanie - Get hello 2 strony elementów (rozmiar strony jest 10):</span><span class="sxs-lookup"><span data-stu-id="633c8-966">Paging - Get hello 2nd page of items (page size is 10):</span></span>

    <span data-ttu-id="633c8-967">GET /indexes/hotels/docs? wyszukiwania = * & $skip = 10 & $top = 10 & api-version = 2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="633c8-967">GET /indexes/hotels/docs?search=*&$skip=10&$top=10&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="633c8-968">POST /indexes/hotels/docs/search? api-version = 2015-02-28-Preview {"wyszukiwanie": "*", "Pomiń": "top", 10: 10}</span><span class="sxs-lookup"><span data-stu-id="633c8-968">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "skip": 10, "top": 10 }</span></span>

9)    <span data-ttu-id="633c8-969">Pobierz zestaw określonych pól:</span><span class="sxs-lookup"><span data-stu-id="633c8-969">Retrieve a specific set of fields:</span></span>

    <span data-ttu-id="633c8-970">GET /indexes/hotels/docs? wyszukiwania = * & $select = hotelName, opis i interfejsu api-version = 2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="633c8-970">GET /indexes/hotels/docs?search=*&$select=hotelName,description&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="633c8-971">POST /indexes/hotels/docs/search? api-version = 2015-02-28-Preview {"wyszukiwanie": "*", "select": "hotelName, opis"}</span><span class="sxs-lookup"><span data-stu-id="633c8-971">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "select": "hotelName, description" }</span></span>

10)  <span data-ttu-id="633c8-972">Pobrać dokumentów zgodnego z wyrażeniem określony filtr:</span><span class="sxs-lookup"><span data-stu-id="633c8-972">Retrieve documents matching a specific filter expression:</span></span>

    <span data-ttu-id="633c8-973">GET /indexes/hotels/docs? $filter = (baseRate ge 60 i baseRate lt 300) lub hotelName eq "Pozostać ozdobne" & api-version = 2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="633c8-973">GET /indexes/hotels/docs?$filter=(baseRate ge 60 and baseRate lt 300) or hotelName eq 'Fancy Stay'&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="633c8-974">POST /indexes/hotels/docs/search? api-version = 2015-02-28-Preview {"filter": "(baseRate ge 60 i baseRate lt 300) lub hotelName eq"Pozostań ozdobne""}</span><span class="sxs-lookup"><span data-stu-id="633c8-974">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {  "filter": "(baseRate ge 60 and baseRate lt 300) or hotelName eq 'Fancy Stay'" }</span></span>

11) <span data-ttu-id="633c8-975">Witaj w indeksie i zwracać fragmenty o trafień najważniejsze funkcje</span><span class="sxs-lookup"><span data-stu-id="633c8-975">Search hello index and return fragments with hit highlights</span></span>

    <span data-ttu-id="633c8-976">GET /indexes/hotels/docs? wyszukiwania = coś & Wyróżnij = opis & api-version = 2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="633c8-976">GET /indexes/hotels/docs?search=something&highlight=description&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="633c8-977">POST /indexes/hotels/docs/search? api-version = 2015-02-28-Preview {"wyszukiwanie": coś, co","highlight":"opis"}</span><span class="sxs-lookup"><span data-stu-id="633c8-977">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "something",   "highlight": "description" }</span></span>

12) <span data-ttu-id="633c8-978">Witaj w indeksie i zwracają dokumenty sortowane od bliżej toofarther poza lokalizacją referencyjną</span><span class="sxs-lookup"><span data-stu-id="633c8-978">Search hello index and return documents sorted from closer toofarther away from a reference location</span></span>

    <span data-ttu-id="633c8-979">GET /indexes/hotels/docs? wyszukiwania = coś & $orderby=geo.distance (lokalizacji, geography'POINT(-122.12315 47.88121) ") & api-version = 2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="633c8-979">GET /indexes/hotels/docs?search=something&$orderby=geo.distance(location, geography'POINT(-122.12315 47.88121)')&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="633c8-980">POST /indexes/hotels/docs/search? api-version = 2015-02-28-Preview {"wyszukiwanie": coś, co","orderby":" geo.distance (lokalizacji, geography'POINT(-122.12315 47.88121) ")"}</span><span class="sxs-lookup"><span data-stu-id="633c8-980">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "something",   "orderby": "geo.distance(location, geography'POINT(-122.12315 47.88121)')" }</span></span>

13) <span data-ttu-id="633c8-981">Wyszukiwania hello indeksu zakładając, że jest profil oceniania o nazwie "geo" z dwóch funkcji oceniania odległość, definiujący jeden parametr o nazwie "currentLocation" i jednym definiujący parametr o nazwie "lastLocation"</span><span class="sxs-lookup"><span data-stu-id="633c8-981">Search hello index assuming there's a scoring profile called "geo" with two distance scoring functions, one defining a parameter called "currentLocation" and one defining a parameter called "lastLocation"</span></span>

    <span data-ttu-id="633c8-982">GET /indexes/hotels/docs? wyszukiwania coś = & scoringProfile = geograficznie & scoringParameter = currentLocation — 122.123,44.77233 & scoringParameter = lastLocation — 121.499,44.2113 & api-version = 2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="633c8-982">GET /indexes/hotels/docs?search=something&scoringProfile=geo&scoringParameter=currentLocation--122.123,44.77233&scoringParameter=lastLocation--121.499,44.2113&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="633c8-983">POST /indexes/hotels/docs/search? api-version = 2015-02-28-Preview {"wyszukiwanie": coś, co","scoringProfile":"geo","scoringParameters": [" currentLocation — 122.123,44.77233 "," lastLocation — 121.499,44.2113 "]}</span><span class="sxs-lookup"><span data-stu-id="633c8-983">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "something",   "scoringProfile": "geo",   "scoringParameters": [ "currentLocation--122.123,44.77233", "lastLocation--121.499,44.2113" ] }</span></span>

14) <span data-ttu-id="633c8-984">Znajdowanie dokumentów w hello indeks, używając [prosta składnia zapytań](https://msdn.microsoft.com/library/dn798920.aspx).</span><span class="sxs-lookup"><span data-stu-id="633c8-984">Find documents in hello index using [simple query syntax](https://msdn.microsoft.com/library/dn798920.aspx).</span></span> <span data-ttu-id="633c8-985">Ta kwerenda zwraca hotele, w którym pól z możliwością wyszukiwania zawierają hello warunki "komfort" i "Lokalizacja", ale nie "motel":</span><span class="sxs-lookup"><span data-stu-id="633c8-985">This query returns hotels where searchable fields contain hello terms "comfort" and "location" but not "motel":</span></span>

    <span data-ttu-id="633c8-986">GET /indexes/hotels/docs? wyszukiwania = komfort + lokalizacji-motel & searchMode = all & api-version = 2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="633c8-986">GET /indexes/hotels/docs?search=comfort +location -motel&searchMode=all&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="633c8-987">POST /indexes/hotels/docs/search? api-version = 2015-02-28-Preview {"wyszukiwanie": "komfort + lokalizacji-motel", "searchMode": "wszystkie"}</span><span class="sxs-lookup"><span data-stu-id="633c8-987">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "comfort +location -motel",   "searchMode": "all" }</span></span>

<span data-ttu-id="633c8-988">Należy zwrócić uwagę użycie hello `searchMode=all` powyżej.</span><span class="sxs-lookup"><span data-stu-id="633c8-988">Note hello use of `searchMode=all` above.</span></span> <span data-ttu-id="633c8-989">W tym ten parametr zastępuje domyślną hello `searchMode=any`, zapewnienie który `-motel` oznacza ", a nie" zamiast "Lub nie".</span><span class="sxs-lookup"><span data-stu-id="633c8-989">Including this parameter overrides hello default of `searchMode=any`, ensuring that `-motel` means "AND NOT" instead of "OR NOT".</span></span> <span data-ttu-id="633c8-990">Bez `searchMode=all`, możesz uzyskać "Lub nie", która rozszerza, a nie ogranicza wyniki wyszukiwania i może to być counter-intuitive toosome użytkowników.</span><span class="sxs-lookup"><span data-stu-id="633c8-990">Without `searchMode=all`, you get "OR NOT" which expands rather than restricts search results, and this can be counter-intuitive toosome users.</span></span>

15) <span data-ttu-id="633c8-991">Znajdowanie dokumentów w hello indeks, używając [składnia zapytań lucene](https://msdn.microsoft.com/library/mt589323.aspx).</span><span class="sxs-lookup"><span data-stu-id="633c8-991">Find documents in hello index using [lucene query syntax](https://msdn.microsoft.com/library/mt589323.aspx).</span></span> <span data-ttu-id="633c8-992">Ta kwerenda zwraca hotele, w którym hello pole kategorii zawiera hello termin "budget" i wyszukiwanie wszystkich pól zawierających hello frazy "ostatnio renovated".</span><span class="sxs-lookup"><span data-stu-id="633c8-992">This query returns hotels where hello category field contains hello term "budget" and all searchable fields containing hello phrase "recently renovated".</span></span> <span data-ttu-id="633c8-993">Dokumenty zawierające hello frazy "ostatnio renovated" są wyżej w wyniku wartość zwiększanie wyniku terminu hello (3)</span><span class="sxs-lookup"><span data-stu-id="633c8-993">Documents containing hello phrase "recently renovated" are ranked higher as a result of hello term boost value (3)</span></span>

    <span data-ttu-id="633c8-994">GET /indexes/hotels/docs? wyszukiwania = kategorii: budżetu i \"ostatnio renovated\"^ 3 & searchMode = all & api-version = 2015-02-28-Preview & kwerendami typu = pełny</span><span class="sxs-lookup"><span data-stu-id="633c8-994">GET /indexes/hotels/docs?search=category:budget AND \"recently renovated\"^3&searchMode=all&api-version=2015-02-28-Preview&querytype=full</span></span>

    <span data-ttu-id="633c8-995">POST /indexes/hotels/docs/search? api-version = 2015-02-28-Preview {"wyszukiwanie": "kategorii: budżetu i \"ostatnio renovated\"^ 3", "kwerendami typu": "pełnej", "searchMode": "wszystkie"}</span><span class="sxs-lookup"><span data-stu-id="633c8-995">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "category:budget AND \"recently renovated\"^3",   "queryType": "full",   "searchMode": "all" }</span></span>

<a name="LookupAPI"></a>

## <a name="lookup-document"></a><span data-ttu-id="633c8-996">Dokument wyszukiwania</span><span class="sxs-lookup"><span data-stu-id="633c8-996">Lookup Document</span></span>
<span data-ttu-id="633c8-997">Witaj **wyszukiwania dokumentu** operacji pobiera dokument z usługi Azure Search.</span><span class="sxs-lookup"><span data-stu-id="633c8-997">hello **Lookup Document** operation retrieves a document from Azure Search.</span></span> <span data-ttu-id="633c8-998">Jest to przydatne, gdy użytkownik kliknie wynik wyszukiwania określonych i ma toolook się szczegółowe informacje na temat tego dokumentu.</span><span class="sxs-lookup"><span data-stu-id="633c8-998">This is useful when a user clicks on a specific search result, and you want toolook up specific details about that document.</span></span>

    GET https://[service name].search.windows.net/indexes/[index name]/docs/[key]?[query parameters]
    api-key: [admin or query key]

<span data-ttu-id="633c8-999">**Żądanie**</span><span class="sxs-lookup"><span data-stu-id="633c8-999">**Request**</span></span>

<span data-ttu-id="633c8-1000">HTTPS jest wymagana dla żądań obsługi.</span><span class="sxs-lookup"><span data-stu-id="633c8-1000">HTTPS is required for service requests.</span></span> <span data-ttu-id="633c8-1001">Witaj **wyszukiwania dokumentu** żądania może być skonstruowany w następujący sposób.</span><span class="sxs-lookup"><span data-stu-id="633c8-1001">hello **Lookup Document** request can be constructed as follows.</span></span>

    GET /indexes/[index name]/docs/key?[query parameters]

<span data-ttu-id="633c8-1002">Alternatywnie program hello tradycyjnych składni OData dla klucza wyszukiwania:</span><span class="sxs-lookup"><span data-stu-id="633c8-1002">Alternatively, you can use hello traditional OData syntax for key lookup:</span></span>

    GET /indexes('[index name]')/docs('[key]')?[query parameters]

<span data-ttu-id="633c8-1003">Żądanie hello identyfikator URI zawiera [Nazwa indeksu] i [klucz], określania, które tooretrieve dokument z indeksu, który.</span><span class="sxs-lookup"><span data-stu-id="633c8-1003">hello request URI includes an [index name] and [key], specifying which document tooretrieve from which index.</span></span> <span data-ttu-id="633c8-1004">Wystarczy tylko jeden dokument naraz.</span><span class="sxs-lookup"><span data-stu-id="633c8-1004">You can only get one document at a time.</span></span> <span data-ttu-id="633c8-1005">Użyj **wyszukiwania** tooget wielu dokumentów w ramach pojedynczego żądania.</span><span class="sxs-lookup"><span data-stu-id="633c8-1005">Use **Search** tooget multiple documents in a single request.</span></span>

<span data-ttu-id="633c8-1006">**Parametry zapytań**</span><span class="sxs-lookup"><span data-stu-id="633c8-1006">**Query Parameters**</span></span>

<span data-ttu-id="633c8-1007">`$select=[string]`(opcjonalnie) — lista tooretrieve pól rozdzielonych przecinkami.</span><span class="sxs-lookup"><span data-stu-id="633c8-1007">`$select=[string]` (optional) - a list of comma-separated fields tooretrieve.</span></span> <span data-ttu-id="633c8-1008">Jeśli nie określono tego parametru lub zbyt`*`, wszystkie pola oznaczone jako pobieranie w schemacie hello są objęte hello projekcji.</span><span class="sxs-lookup"><span data-stu-id="633c8-1008">If unspecified or set too`*`, all fields marked as retrievable in hello schema are included in hello projection.</span></span>

<span data-ttu-id="633c8-1009">`api-version=[string]`(wymagane).</span><span class="sxs-lookup"><span data-stu-id="633c8-1009">`api-version=[string]` (required).</span></span> <span data-ttu-id="633c8-1010">Wersja zapoznawcza Hello jest `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="633c8-1010">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="633c8-1011">Zobacz [przechowywanie wersji usługi wyszukiwania](http://msdn.microsoft.com/library/azure/dn864560.aspx) szczegółowe informacje i alternatywne wersje.</span><span class="sxs-lookup"><span data-stu-id="633c8-1011">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="633c8-1012">Uwaga: Ta operacja hello `api-version` jest określony jako parametr zapytania.</span><span class="sxs-lookup"><span data-stu-id="633c8-1012">Note: For this operation, hello `api-version` is specified as a query parameter.</span></span>

<span data-ttu-id="633c8-1013">**Nagłówki żądania**</span><span class="sxs-lookup"><span data-stu-id="633c8-1013">**Request Headers**</span></span>

<span data-ttu-id="633c8-1014">powitania po liście opisano hello wymagane i opcjonalne żądania nagłówków.</span><span class="sxs-lookup"><span data-stu-id="633c8-1014">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="633c8-1015">`api-key`: hello `api-key` jest używane tooauthenticate hello żądania tooyour usługi wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="633c8-1015">`api-key`: hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="633c8-1016">Jest to wartość ciągu tooyour unikatowy adres URL usługi.</span><span class="sxs-lookup"><span data-stu-id="633c8-1016">It is a string value, unique tooyour service URL.</span></span> <span data-ttu-id="633c8-1017">Witaj **wyszukiwania dokumentu** żądania można podać klucz administratora lub klucz zapytania dla `api-key`.</span><span class="sxs-lookup"><span data-stu-id="633c8-1017">hello **Lookup Document** request can specify either an admin key or query key for `api-key`.</span></span>

<span data-ttu-id="633c8-1018">Należy również adres URL hello usługi nazwa tooconstruct hello żądania.</span><span class="sxs-lookup"><span data-stu-id="633c8-1018">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="633c8-1019">Można uzyskać nazwy usługi hello i `api-key` z pulpitu nawigacyjnego usługi w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="633c8-1019">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="633c8-1020">Zobacz [Tworzenie usługi Azure Search w portalu hello](search-create-service-portal.md) dla pomocy nawigacji strony.</span><span class="sxs-lookup"><span data-stu-id="633c8-1020">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="633c8-1021">**Treść żądania**</span><span class="sxs-lookup"><span data-stu-id="633c8-1021">**Request Body**</span></span>

<span data-ttu-id="633c8-1022">Brak.</span><span class="sxs-lookup"><span data-stu-id="633c8-1022">None.</span></span>

<span data-ttu-id="633c8-1023">**Odpowiedź**</span><span class="sxs-lookup"><span data-stu-id="633c8-1023">**Response**</span></span>

<span data-ttu-id="633c8-1024">Kod stanu: 200 OK jest zwracana dla pomyślnej odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="633c8-1024">Status Code: 200 OK is returned for a successful response.</span></span>

    {
      field_name: field_value (fields matching hello default or specified projection)
    }

<span data-ttu-id="633c8-1025">**Przykład**</span><span class="sxs-lookup"><span data-stu-id="633c8-1025">**Example**</span></span>

<span data-ttu-id="633c8-1026">Wyszukiwanie hello dokument, który ma klucz "2"</span><span class="sxs-lookup"><span data-stu-id="633c8-1026">Lookup hello document that has key '2'</span></span>

    GET /indexes/hotels/docs/2?api-version=2015-02-28-Preview

<span data-ttu-id="633c8-1027">Wyszukiwanie hello dokument, który ma klucz "3" przy użyciu składni OData:</span><span class="sxs-lookup"><span data-stu-id="633c8-1027">Lookup hello document that has key '3' using OData syntax:</span></span>

    GET /indexes('hotels')/docs('3')?api-version=2015-02-28-Preview

<a name="CountDocs"></a>

## <a name="count-documents"></a><span data-ttu-id="633c8-1028">Liczba dokumentów</span><span class="sxs-lookup"><span data-stu-id="633c8-1028">Count Documents</span></span>
<span data-ttu-id="633c8-1029">Witaj **liczba dokumentów** operacji pobiera liczbę hello liczby dokumentów w indeksie wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="633c8-1029">hello **Count Documents** operation retrieves a count of hello number of documents in a search index.</span></span> <span data-ttu-id="633c8-1030">Witaj `$count` składni jest częścią hello protokołu OData.</span><span class="sxs-lookup"><span data-stu-id="633c8-1030">hello `$count` syntax is part of hello OData protocol.</span></span>

    GET https://[service name].search.windows.net/indexes/[index name]/docs/$count?api-version=[api-version]
    Accept: text/plain
    api-key: [admin or query key]

<span data-ttu-id="633c8-1031">**Żądanie**</span><span class="sxs-lookup"><span data-stu-id="633c8-1031">**Request**</span></span>

<span data-ttu-id="633c8-1032">HTTPS jest wymagana dla żądań obsługi.</span><span class="sxs-lookup"><span data-stu-id="633c8-1032">HTTPS is required for service requests.</span></span> <span data-ttu-id="633c8-1033">Witaj **liczba dokumentów** żądania można skonstruować przy użyciu metody GET hello.</span><span class="sxs-lookup"><span data-stu-id="633c8-1033">hello **Count Documents** request can be constructed using hello GET method.</span></span>

<span data-ttu-id="633c8-1034">hello [Nazwa indeksu] w identyfikatorze URI żądania hello informuje tooreturn usługi hello liczbę wszystkich elementów w kolekcji dokumentów hello hello określonego indeksu.</span><span class="sxs-lookup"><span data-stu-id="633c8-1034">hello [index name] in hello request URI tells hello service tooreturn a count of all items in hello docs collection of hello specified index.</span></span>

<span data-ttu-id="633c8-1035">`api-version=[string]`(wymagane).</span><span class="sxs-lookup"><span data-stu-id="633c8-1035">`api-version=[string]` (required).</span></span> <span data-ttu-id="633c8-1036">Wersja zapoznawcza Hello jest `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="633c8-1036">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="633c8-1037">Zobacz [przechowywanie wersji usługi wyszukiwania](http://msdn.microsoft.com/library/azure/dn864560.aspx) szczegółowe informacje i alternatywne wersje.</span><span class="sxs-lookup"><span data-stu-id="633c8-1037">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="633c8-1038">**Nagłówki żądania**</span><span class="sxs-lookup"><span data-stu-id="633c8-1038">**Request Headers**</span></span>

<span data-ttu-id="633c8-1039">powitania po liście opisano hello wymagane i opcjonalne żądania nagłówków.</span><span class="sxs-lookup"><span data-stu-id="633c8-1039">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="633c8-1040">`Accept`: Ta wartość musi być ustawiona zbyt`text/plain`.</span><span class="sxs-lookup"><span data-stu-id="633c8-1040">`Accept`: This value must be set too`text/plain`.</span></span>
* <span data-ttu-id="633c8-1041">`api-key`: hello `api-key` jest używane tooauthenticate hello żądania tooyour usługi wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="633c8-1041">`api-key`: hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="633c8-1042">Jest to wartość ciągu tooyour unikatowy adres URL usługi.</span><span class="sxs-lookup"><span data-stu-id="633c8-1042">It is a string value, unique tooyour service URL.</span></span> <span data-ttu-id="633c8-1043">Witaj **liczba dokumentów** żądania można podać klucz administratora lub klucz zapytania dla `api-key`.</span><span class="sxs-lookup"><span data-stu-id="633c8-1043">hello **Count Documents** request can specify either an admin key or query key for `api-key`.</span></span>

<span data-ttu-id="633c8-1044">Należy również adres URL hello usługi nazwa tooconstruct hello żądania.</span><span class="sxs-lookup"><span data-stu-id="633c8-1044">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="633c8-1045">Można uzyskać nazwy usługi hello i `api-key` z pulpitu nawigacyjnego usługi w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="633c8-1045">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="633c8-1046">Zobacz [Tworzenie usługi Azure Search w portalu hello](search-create-service-portal.md) dla pomocy nawigacji strony.</span><span class="sxs-lookup"><span data-stu-id="633c8-1046">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="633c8-1047">**Treść żądania**</span><span class="sxs-lookup"><span data-stu-id="633c8-1047">**Request Body**</span></span>

<span data-ttu-id="633c8-1048">Brak.</span><span class="sxs-lookup"><span data-stu-id="633c8-1048">None.</span></span>

<span data-ttu-id="633c8-1049">**Odpowiedź**</span><span class="sxs-lookup"><span data-stu-id="633c8-1049">**Response**</span></span>

<span data-ttu-id="633c8-1050">Kod stanu: 200 OK jest zwracana dla pomyślnej odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="633c8-1050">Status Code: 200 OK is returned for a successful response.</span></span>

<span data-ttu-id="633c8-1051">treść odpowiedzi Hello zawiera wartość licznika hello jako liczba całkowita sformatowany w postaci zwykłego tekstu.</span><span class="sxs-lookup"><span data-stu-id="633c8-1051">hello response body contains hello count value as an integer formatted in plain text.</span></span>

<a name="Suggestions"></a>

## <a name="suggestions"></a><span data-ttu-id="633c8-1052">Propozycje</span><span class="sxs-lookup"><span data-stu-id="633c8-1052">Suggestions</span></span>
<span data-ttu-id="633c8-1053">Witaj **sugestie** operacji pobiera sugestie na podstawie danych wprowadzonych z częściowa wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="633c8-1053">hello **Suggestions** operation retrieves suggestions based on partial search input.</span></span> <span data-ttu-id="633c8-1054">Zazwyczaj jest używany w wpisywaniu sugestie dotyczące wyszukiwania pola tooprovide jako użytkowników wprowadza terminy wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="633c8-1054">It's typically used in search boxes tooprovide type-ahead suggestions as users are entering search terms.</span></span>

<span data-ttu-id="633c8-1055">Wnioski sugestię celem sugerowanie dokumentach docelowych, więc hello sugerowane się, że tekst może się powtarzać, jeśli wiele dokumentów candidate zgodne hello same wyszukiwania danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="633c8-1055">Suggestion requests aim at suggesting target documents, so hello suggested text may be repeated if multiple candidate documents match hello same search input.</span></span> <span data-ttu-id="633c8-1056">Można użyć `$select` tooretrieve innych dokumentów pola (w tym hello klucz dokumentu), dzięki czemu można określić, który dokument jest hello źródła dla każdej sugestii.</span><span class="sxs-lookup"><span data-stu-id="633c8-1056">You can use `$select` tooretrieve other document fields (including hello document key) so that you can tell which document is hello source for each suggestion.</span></span>

<span data-ttu-id="633c8-1057">A **sugestie** operacji jest wystawione jako żądania GET lub POST.</span><span class="sxs-lookup"><span data-stu-id="633c8-1057">A **Suggestions** operation is issued as a GET or POST request.</span></span>

    GET https://[service name].search.windows.net/indexes/[index name]/docs/suggest?[query parameters]
    api-key: [admin or query key]

    POST https://[service name].search.windows.net/indexes/[index name]/docs/suggest?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin or query key]

<span data-ttu-id="633c8-1058">**Podczas publikowania toouse zamiast GET**</span><span class="sxs-lookup"><span data-stu-id="633c8-1058">**When toouse POST instead of GET**</span></span>

<span data-ttu-id="633c8-1059">Jeśli używasz HTTP GET hello toocall **sugestie** interfejsu API, należy pamiętać, że hello długość adresu URL żądania hello nie może przekraczać 8 KB toobe.</span><span class="sxs-lookup"><span data-stu-id="633c8-1059">When you use HTTP GET toocall hello **Suggestions** API, you need toobe aware that hello length of hello request URL cannot exceed 8 KB.</span></span> <span data-ttu-id="633c8-1060">Jest to zwykle wystarczająco dla większości aplikacji.</span><span class="sxs-lookup"><span data-stu-id="633c8-1060">This is usually enough for most applications.</span></span> <span data-ttu-id="633c8-1061">Jednak niektóre aplikacje powodują bardzo dużych zapytań, w szczególności wyrażeniach filtru OData.</span><span class="sxs-lookup"><span data-stu-id="633c8-1061">However, some applications produce very large queries, specifically OData filter expressions.</span></span> <span data-ttu-id="633c8-1062">W przypadku tych aplikacji przy użyciu metody POST protokołu HTTP jest lepszym rozwiązaniem, ponieważ umożliwia filtry większych niż GET.</span><span class="sxs-lookup"><span data-stu-id="633c8-1062">For these applications, using HTTP POST is a better choice because it allows larger filters than GET.</span></span> <span data-ttu-id="633c8-1063">Przy użyciu metody POST hello liczba klauzul w filtrze jest czynnikiem ograniczającym hello, nie hello rozmiar hello ciąg filtru raw, ponieważ limit rozmiaru hello żądania POST wynosi około 16 MB.</span><span class="sxs-lookup"><span data-stu-id="633c8-1063">With POST, hello number of clauses in a filter is hello limiting factor, not hello size of hello raw filter string since hello request size limit for POST is approximately 16 MB.</span></span>

> [!NOTE]
> <span data-ttu-id="633c8-1064">Mimo że limit rozmiaru żądania POST hello jest bardzo duży, wyrażeniach filtru nie może być arbitralnie złożonych.</span><span class="sxs-lookup"><span data-stu-id="633c8-1064">Even though hello POST request size limit is very large, filter expressions cannot be arbitrarily complex.</span></span> <span data-ttu-id="633c8-1065">Zobacz [składni wyrażeń OData](https://msdn.microsoft.com/library/dn798921.aspx) uzyskać więcej informacji o ograniczeniach złożoności filtru.</span><span class="sxs-lookup"><span data-stu-id="633c8-1065">See [OData expression syntax](https://msdn.microsoft.com/library/dn798921.aspx) for more information about filter complexity limitations.</span></span>
> 
> 

<span data-ttu-id="633c8-1066">**Żądanie**</span><span class="sxs-lookup"><span data-stu-id="633c8-1066">**Request**</span></span>

<span data-ttu-id="633c8-1067">HTTPS jest wymagana dla żądań obsługi.</span><span class="sxs-lookup"><span data-stu-id="633c8-1067">HTTPS is required for service requests.</span></span> <span data-ttu-id="633c8-1068">Witaj **sugestie** żądania można skonstruować przy użyciu hello GET lub POST metody.</span><span class="sxs-lookup"><span data-stu-id="633c8-1068">hello **Suggestions** request can be constructed using hello GET or POST methods.</span></span>

<span data-ttu-id="633c8-1069">Identyfikator URI żądania Hello nazwa hello hello tooquery indeksu.</span><span class="sxs-lookup"><span data-stu-id="633c8-1069">hello request URI specifies hello name of hello index tooquery.</span></span> <span data-ttu-id="633c8-1070">Parametry, takie jak hello częściowo wejściowych wyszukiwany termin, są określone w ciągu kwerendy hello w przypadku żądania GET hello, a w żądaniu hello żądań treści w przypadku hello POST.</span><span class="sxs-lookup"><span data-stu-id="633c8-1070">Parameters, such as hello partially input search term, are specified on hello query string in hello case of GET requests, and in hello request body in hello case of POST requests.</span></span>

<span data-ttu-id="633c8-1071">Najlepszym rozwiązaniem podczas tworzenia żądania GET, pamiętaj zbyt[kodowania adresu URL](https://msdn.microsoft.com/library/system.uri.escapedatastring.aspx) określonej kwerendy bezpośrednio hello parametrów podczas wywoływania metody interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="633c8-1071">As a best practice when creating GET requests, remember too[URL-encode](https://msdn.microsoft.com/library/system.uri.escapedatastring.aspx) specific query parameters when calling hello REST API directly.</span></span> <span data-ttu-id="633c8-1072">Aby uzyskać **sugestie** operacje, w tym:</span><span class="sxs-lookup"><span data-stu-id="633c8-1072">For **Suggestions** operations, this includes:</span></span>

* `$filter`
* `highlightPreTag`
* `highlightPostTag`
* `search`

<span data-ttu-id="633c8-1073">Kodowanie adresu URL zaleca się tylko na powitania powyżej parametry zapytania.</span><span class="sxs-lookup"><span data-stu-id="633c8-1073">URL encoding is only recommended on hello above query parameters.</span></span> <span data-ttu-id="633c8-1074">Jeśli użytkownik przypadkowo kodowania adresu URL hello ciągu zapytania całego, (wszystko po hello?), spowoduje przerwanie żądania.</span><span class="sxs-lookup"><span data-stu-id="633c8-1074">If you inadvertently URL-encode hello entire query string (everything after hello ?), requests will break.</span></span>

<span data-ttu-id="633c8-1075">Ponadto podczas kodowania adresu URL jest wymagane tylko podczas wywoływania metody hello UZYSKAĆ bezpośrednio przy użyciu interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="633c8-1075">Also, URL encoding is only necessary when calling hello REST API directly using GET.</span></span> <span data-ttu-id="633c8-1076">Bez kodowania adresu URL jest niezbędne, jeśli wywołanie **sugestie** używanie żądania POST, lub w przypadku używania hello [biblioteki klienta .NET](https://msdn.microsoft.com/library/dn951165.aspx), który obsługuje kodowanie adresu URL.</span><span class="sxs-lookup"><span data-stu-id="633c8-1076">No URL encoding is necessary when calling **Suggestions** using POST, or when using hello [.NET client library](https://msdn.microsoft.com/library/dn951165.aspx), which handles URL encoding for you.</span></span>

<span data-ttu-id="633c8-1077">**Parametry zapytań**</span><span class="sxs-lookup"><span data-stu-id="633c8-1077">**Query Parameters**</span></span>

<span data-ttu-id="633c8-1078">**Sugestie** przyjmuje kilka parametrów, które zapewniają kryteria, a także określić sposób wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="633c8-1078">**Suggestions** accepts several parameters that provide query criteria and also specify search behavior.</span></span> <span data-ttu-id="633c8-1079">Należy podać długość ciągu zapytania tych parametrów w adresie URL hello podczas wywoływania metody **sugestie** alerty, a także jako właściwości JSON w treści żądania hello podczas wywoływania metody **sugestie** za pośrednictwem POST.</span><span class="sxs-lookup"><span data-stu-id="633c8-1079">You provide these parameters in hello URL query string when calling **Suggestions** via GET, and as JSON properties in hello request body when calling **Suggestions** via POST.</span></span> <span data-ttu-id="633c8-1080">Składnia Hello niektórych parametrów różni się nieco między GET i POST.</span><span class="sxs-lookup"><span data-stu-id="633c8-1080">hello syntax for some parameters is slightly different between GET and POST.</span></span> <span data-ttu-id="633c8-1081">Różnice te odnotowano odpowiednio poniżej:</span><span class="sxs-lookup"><span data-stu-id="633c8-1081">These differences are noted as applicable below:</span></span>

<span data-ttu-id="633c8-1082">`search=[string]`-hello zapytania toosuggest toouse tekst wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="633c8-1082">`search=[string]` - hello search text toouse toosuggest queries.</span></span> <span data-ttu-id="633c8-1083">Musi być co najmniej 1 znak i nie może przekraczać 100 znaków.</span><span class="sxs-lookup"><span data-stu-id="633c8-1083">Must be at least 1 character, and no more than 100 characters.</span></span>

<span data-ttu-id="633c8-1084">`highlightPreTag=[string]`(opcjonalnie) - tag ciąg, który dołącza toosearch trafień.</span><span class="sxs-lookup"><span data-stu-id="633c8-1084">`highlightPreTag=[string]` (optional) - a string tag that prepends toosearch hits.</span></span> <span data-ttu-id="633c8-1085">Musi być ustawiona z `highlightPostTag`.</span><span class="sxs-lookup"><span data-stu-id="633c8-1085">Must be set with `highlightPostTag`.</span></span>

> [!NOTE]
> <span data-ttu-id="633c8-1086">Podczas wywoływania metody **sugestie** przy użyciu GET, zarezerwowanych znaków w adresie URL hello musi być zakodowany procent (na przykład zamiast #, % 23).</span><span class="sxs-lookup"><span data-stu-id="633c8-1086">When calling **Suggestions** using GET, reserved characters in hello URL must be percent-encoded (for example, %23 instead of #).</span></span>
> 
> 

<span data-ttu-id="633c8-1087">`highlightPostTag=[string]`(opcjonalnie) - tag ciąg, który dołącza toosearch trafień.</span><span class="sxs-lookup"><span data-stu-id="633c8-1087">`highlightPostTag=[string]` (optional) - a string tag that appends toosearch hits.</span></span> <span data-ttu-id="633c8-1088">Musi być ustawiona z `highlightPreTag`.</span><span class="sxs-lookup"><span data-stu-id="633c8-1088">Must be set with `highlightPreTag`.</span></span>

> [!NOTE]
> <span data-ttu-id="633c8-1089">Podczas wywoływania metody **sugestie** przy użyciu GET, zarezerwowanych znaków w adresie URL hello musi być zakodowany procent (na przykład zamiast #, % 23).</span><span class="sxs-lookup"><span data-stu-id="633c8-1089">When calling **Suggestions** using GET, reserved characters in hello URL must be percent-encoded (for example, %23 instead of #).</span></span>
> 
> 

<span data-ttu-id="633c8-1090">`suggesterName=[string]`-hello nazwę sugestora hello jako określone w hello `suggesters` kolekcji, która jest częścią definicji indeksu hello.</span><span class="sxs-lookup"><span data-stu-id="633c8-1090">`suggesterName=[string]` - hello name of hello suggester as specified in hello `suggesters` collection that's part of hello index definition.</span></span> <span data-ttu-id="633c8-1091">A `suggester` określa pola, które są skanowane pod kątem warunków sugerowane zapytania.</span><span class="sxs-lookup"><span data-stu-id="633c8-1091">A `suggester` determines which fields are scanned for suggested query terms.</span></span> <span data-ttu-id="633c8-1092">Zobacz [Sugestorów](#Suggesters) szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="633c8-1092">See [Suggesters](#Suggesters) for details.</span></span>

<span data-ttu-id="633c8-1093">`fuzzy=[boolean]`(opcjonalne, domyślne = false) — wartość tootrue to interfejsu API będzie sugestie nawet, jeśli występuje znak podstawione lub brak w hello szukany tekst.</span><span class="sxs-lookup"><span data-stu-id="633c8-1093">`fuzzy=[boolean]` (optional, default = false) - when set tootrue this API will find suggestions even if there's a substituted or missing character in hello search text.</span></span> <span data-ttu-id="633c8-1094">Gdy zapewnia lepsze środowisko pracy w niektórych scenariuszach pochodzi z wydajnością, kosztów rozmytego sugestii wyszukiwania są wolniejszej i zużywać więcej zasobów.</span><span class="sxs-lookup"><span data-stu-id="633c8-1094">While this provides a better experience in some scenarios it comes at a performance cost as fuzzy suggestion searches are slower and consume more resources.</span></span>

<span data-ttu-id="633c8-1095">`searchFields=[string]`(opcjonalnie) - hello lista toosearch nazw pól rozdzielonych przecinkami dla hello określony tekst wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="633c8-1095">`searchFields=[string]` (optional) - hello list of comma-separated field names toosearch for hello specified search text.</span></span> <span data-ttu-id="633c8-1096">Sugestie, można włączyć pól docelowych.</span><span class="sxs-lookup"><span data-stu-id="633c8-1096">Target fields must be enabled for suggestions.</span></span>

<span data-ttu-id="633c8-1097">`$top=#`(opcjonalne, domyślne = 5) — Witaj liczba tooretrieve sugestie.</span><span class="sxs-lookup"><span data-stu-id="633c8-1097">`$top=#` (optional, default = 5) - hello number of suggestions tooretrieve.</span></span> <span data-ttu-id="633c8-1098">Musi być liczbą z zakresu od 1 do 100.</span><span class="sxs-lookup"><span data-stu-id="633c8-1098">Must be a number between 1 and 100.</span></span>

> [!NOTE]
> <span data-ttu-id="633c8-1099">Podczas wywoływania metody **sugestie** używanie żądania POST, ten parametr nosi nazwę `top` zamiast `$top`.</span><span class="sxs-lookup"><span data-stu-id="633c8-1099">When calling **Suggestions** using POST, this parameter is named `top` instead of `$top`.</span></span>
> 
> 

<span data-ttu-id="633c8-1100">`$filter=[string]`(opcjonalnie) - wyrażenia filtrujące dokumenty hello rozważyć sugestie.</span><span class="sxs-lookup"><span data-stu-id="633c8-1100">`$filter=[string]` (optional) - an expression that filters hello documents considered for suggestions.</span></span>

> [!NOTE]
> <span data-ttu-id="633c8-1101">Podczas wywoływania metody **sugestie** używanie żądania POST, ten parametr nosi nazwę `filter` zamiast `$filter`.</span><span class="sxs-lookup"><span data-stu-id="633c8-1101">When calling **Suggestions** using POST, this parameter is named `filter` instead of `$filter`.</span></span>
> 
> 

<span data-ttu-id="633c8-1102">`$orderby=[string]`(opcjonalnie) — lista wyrażeń oddzielonych przecinkami toosort hello wyniki według.</span><span class="sxs-lookup"><span data-stu-id="633c8-1102">`$orderby=[string]` (optional) - a list of comma-separated expressions toosort hello results by.</span></span> <span data-ttu-id="633c8-1103">Każde wyrażenie może być nazwą pola lub toohello wywołania `geo.distance()` funkcji.</span><span class="sxs-lookup"><span data-stu-id="633c8-1103">Each expression can be either a field name or a call toohello `geo.distance()` function.</span></span> <span data-ttu-id="633c8-1104">Każde wyrażenie może następować `asc` tooindicated rosnącej, i `desc` tooindicate malejąco.</span><span class="sxs-lookup"><span data-stu-id="633c8-1104">Each expression can be followed by `asc` tooindicated ascending, and `desc` tooindicate descending.</span></span> <span data-ttu-id="633c8-1105">domyślne Hello jest rosnącą.</span><span class="sxs-lookup"><span data-stu-id="633c8-1105">hello default is ascending order.</span></span> <span data-ttu-id="633c8-1106">Istnieje limit 32 klauzule dotyczące `$orderby`.</span><span class="sxs-lookup"><span data-stu-id="633c8-1106">There is a limit of 32 clauses for `$orderby`.</span></span>

> [!NOTE]
> <span data-ttu-id="633c8-1107">Podczas wywoływania metody **sugestie** używanie żądania POST, ten parametr nosi nazwę `orderby` zamiast `$orderby`.</span><span class="sxs-lookup"><span data-stu-id="633c8-1107">When calling **Suggestions** using POST, this parameter is named `orderby` instead of `$orderby`.</span></span>
> 
> 

<span data-ttu-id="633c8-1108">`$select=[string]`(opcjonalnie) — lista tooretrieve pól rozdzielonych przecinkami.</span><span class="sxs-lookup"><span data-stu-id="633c8-1108">`$select=[string]` (optional) - a list of comma-separated fields tooretrieve.</span></span> <span data-ttu-id="633c8-1109">Jeśli zostanie określona, tylko hello klucz dokumentu i zwracany jest tekst uwag.</span><span class="sxs-lookup"><span data-stu-id="633c8-1109">If unspecified, only hello document key and suggestion text is returned.</span></span> <span data-ttu-id="633c8-1110">Można jawnie żądania wszystkie pola przez ustawienie tego parametru zbyt`*`.</span><span class="sxs-lookup"><span data-stu-id="633c8-1110">You can explicitly request all fields by setting this parameter too`*`.</span></span>

> [!NOTE]
> <span data-ttu-id="633c8-1111">Podczas wywoływania metody **sugestie** używanie żądania POST, ten parametr nosi nazwę `select` zamiast `$select`.</span><span class="sxs-lookup"><span data-stu-id="633c8-1111">When calling **Suggestions** using POST, this parameter is named `select` instead of `$select`.</span></span>
> 
> 

<span data-ttu-id="633c8-1112">`minimumCoverage`(opcjonalne, domyślnie przyjmowana jest too80) - liczbą z zakresu od 0 do 100 wskazujący procent hello hello indeksu, który musi być objęta sugestie zapytanie aby toobe zapytania hello raportowane klientowi jako sukcesu.</span><span class="sxs-lookup"><span data-stu-id="633c8-1112">`minimumCoverage` (optional, defaults too80) - a number between 0 and 100 indicating hello percentage of hello index that must be covered by a suggestions query in order for hello query toobe reported as a success.</span></span> <span data-ttu-id="633c8-1113">Domyślnie, muszą być dostępne co najmniej 80% hello indeksu lub `Suggest` zwróci kod stanu HTTP 503.</span><span class="sxs-lookup"><span data-stu-id="633c8-1113">By default, at least 80% of hello index must be available or `Suggest` will return HTTP status code 503.</span></span> <span data-ttu-id="633c8-1114">Jeśli ustawisz `minimumCoverage` i `Suggest` zakończy się pomyślnie, zostanie zwrócić 200 protokołu HTTP i obejmują `@search.coverage` wartości w odpowiedzi hello wskazujący procent hello hello indeksu, który został uwzględniony w zapytaniu hello.</span><span class="sxs-lookup"><span data-stu-id="633c8-1114">If you set `minimumCoverage` and `Suggest` succeeds, it will return HTTP 200 and include a `@search.coverage` value in hello response indicating hello percentage of hello index that was included in hello query.</span></span>

> [!NOTE]
> <span data-ttu-id="633c8-1115">Ustawienie tej wartości tooa parametru mniejsze niż 100 mogą być przydatne dla zapewnienia dostępności wyszukiwania nawet w przypadku usług z tylko jedną replikę.</span><span class="sxs-lookup"><span data-stu-id="633c8-1115">Setting this parameter tooa value lower than 100 can be useful for ensuring search availability even for services with only one replica.</span></span> <span data-ttu-id="633c8-1116">Jednak nie wszystkie pasujących propozycji dotrą toobe obecne w wynikach hello.</span><span class="sxs-lookup"><span data-stu-id="633c8-1116">However, not all matching suggestions are guaranteed toobe present in hello results.</span></span> <span data-ttu-id="633c8-1117">Jeśli odwołania jest ważniejsze aplikacji tooyour niż dostępności, a następnie jego najlepszych nie toolower `minimumCoverage` poniżej jego domyślna wartość 80.</span><span class="sxs-lookup"><span data-stu-id="633c8-1117">If recall is more important tooyour application than availability, then it's best not toolower `minimumCoverage` below its default value of 80.</span></span>
> 
> 

<span data-ttu-id="633c8-1118">`api-version=[string]`(wymagane).</span><span class="sxs-lookup"><span data-stu-id="633c8-1118">`api-version=[string]` (required).</span></span> <span data-ttu-id="633c8-1119">Wersja zapoznawcza Hello jest `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="633c8-1119">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="633c8-1120">Zobacz [przechowywanie wersji usługi wyszukiwania](http://msdn.microsoft.com/library/azure/dn864560.aspx) szczegółowe informacje i alternatywne wersje.</span><span class="sxs-lookup"><span data-stu-id="633c8-1120">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="633c8-1121">Uwaga: Ta operacja hello `api-version` jest określony jako parametr zapytania w adresie URL hello niezależnie od tego, czy wywołać **sugestie** z GET lub POST.</span><span class="sxs-lookup"><span data-stu-id="633c8-1121">Note: For this operation, hello `api-version` is specified as a query parameter in hello URL regardless of whether you call **Suggestions** with GET or POST.</span></span>

<span data-ttu-id="633c8-1122">**Nagłówki żądania**</span><span class="sxs-lookup"><span data-stu-id="633c8-1122">**Request Headers**</span></span>

<span data-ttu-id="633c8-1123">następujące listy Hello opisano hello wymagane i opcjonalne żądania nagłówków</span><span class="sxs-lookup"><span data-stu-id="633c8-1123">hello following list describes hello required and optional request headers</span></span>

* <span data-ttu-id="633c8-1124">`api-key`: hello `api-key` jest używane tooauthenticate hello żądania tooyour usługi wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="633c8-1124">`api-key`: hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="633c8-1125">Jest to wartość ciągu tooyour unikatowy adres URL usługi.</span><span class="sxs-lookup"><span data-stu-id="633c8-1125">It is a string value, unique tooyour service URL.</span></span> <span data-ttu-id="633c8-1126">Witaj **sugestie** żądania można podać klucz administratora lub klucz zapytania jako hello `api-key`.</span><span class="sxs-lookup"><span data-stu-id="633c8-1126">hello **Suggestions** request can specify either an admin key or query key as hello `api-key`.</span></span>

<span data-ttu-id="633c8-1127">Należy również adres URL hello usługi nazwa tooconstruct hello żądania.</span><span class="sxs-lookup"><span data-stu-id="633c8-1127">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="633c8-1128">Można uzyskać nazwy usługi hello i `api-key` z pulpitu nawigacyjnego usługi w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="633c8-1128">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="633c8-1129">Zobacz [Tworzenie usługi Azure Search w portalu hello](search-create-service-portal.md) dla pomocy nawigacji strony.</span><span class="sxs-lookup"><span data-stu-id="633c8-1129">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="633c8-1130">**Treść żądania**</span><span class="sxs-lookup"><span data-stu-id="633c8-1130">**Request Body**</span></span>

<span data-ttu-id="633c8-1131">Get: Brak.</span><span class="sxs-lookup"><span data-stu-id="633c8-1131">For GET: None.</span></span>

<span data-ttu-id="633c8-1132">W przypadku żądania POST:</span><span class="sxs-lookup"><span data-stu-id="633c8-1132">For POST:</span></span>

    {
      "filter": "odata_filter_expression",
      "fuzzy": true | false (default),
      "highlightPreTag": "pre_tag",
      "highlightPostTag": "post_tag",
      "minimumCoverage": # (% of index that must be covered toodeclare query successful; default 80),
      "orderby": "orderby_expression",
      "search": "partial_search_input",
      "searchFields": "field_name_1, field_name_2, ...",
      "select": "field_name_1, field_name_2, ...",
      "suggesterName": "suggester_name",
      "top": # (default 5)
    }

<span data-ttu-id="633c8-1133">**Odpowiedź**</span><span class="sxs-lookup"><span data-stu-id="633c8-1133">**Response**</span></span>

<span data-ttu-id="633c8-1134">Kod stanu: 200 OK jest zwracana dla pomyślnej odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="633c8-1134">Status Code: 200 OK is returned for a successful response.</span></span>

    {
      "@search.coverage": # (if minimumCoverage was provided in hello query),
      "value": [
        {
          "@search.text": "...",
          "<key field>": "..."
        },
        ...
      ]
    }

<span data-ttu-id="633c8-1135">Jeśli opcja projekcji hello jest używany tooretrieve pola są uwzględnione na liście każdy element tablicy hello:</span><span class="sxs-lookup"><span data-stu-id="633c8-1135">If hello projection option is used tooretrieve fields they are included in each element of hello array:</span></span>

    {
      "@search.coverage": # (if minimumCoverage was provided in hello query),
      "value": [
        {
          "@search.text": "...",
          "<key field>": "..."
          <other projected data fields>
        },
        ...
      ]
    }

<span data-ttu-id="633c8-1136">**Przykład**</span><span class="sxs-lookup"><span data-stu-id="633c8-1136">**Example**</span></span>

<span data-ttu-id="633c8-1137">Pobierz 5 sugestie gdzie danych wejściowych z częściowa wyszukiwania hello jest "lux"</span><span class="sxs-lookup"><span data-stu-id="633c8-1137">Retrieve 5 suggestions where hello partial search input is 'lux'</span></span>

    GET /indexes/hotels/docs/suggest?search=lux&$top=5&suggesterName=sg&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/suggest?api-version=2015-02-28-Preview
    {
      "search": "lux",
      "top": 5,
      "suggesterName": "sg"
    }
