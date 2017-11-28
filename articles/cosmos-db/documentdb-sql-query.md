---
title: "aaaSQL zapytania dotyczące interfejsu API Azure rozwiązania Cosmos bazy danych usługi DocumentDB | Dokumentacja firmy Microsoft"
description: "Dowiedz się więcej o składni SQL, pojęcia bazy danych i zapytania SQL dla bazy danych Azure rozwiązania Cosmos. SQL może być używany jako język kwerendy JSON w usłudze Azure DB rozwiązania Cosmos."
keywords: "Składnia SQL, zapytanie sql, zapytania sql, język zapytań json, koncepcje bazy danych i zapytania sql, funkcje agregujące"
services: cosmos-db
documentationcenter: 
author: arramac
manager: jhubbard
editor: monicar
ms.assetid: a73b4ab3-0786-42fd-b59b-555fce09db6e
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: arramac
ms.openlocfilehash: f4db95b87f5796c4e4299aaf016435cb6301bbfe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="sql-queries-for-azure-cosmos-db-documentdb-api"></a><span data-ttu-id="f0070-105">Zapytania SQL dla interfejsu API Azure rozwiązania Cosmos bazy danych usługi DocumentDB</span><span class="sxs-lookup"><span data-stu-id="f0070-105">SQL queries for Azure Cosmos DB DocumentDB API</span></span>
<span data-ttu-id="f0070-106">Bazy danych programu Microsoft Azure rozwiązania Cosmos obsługuje tworzenie zapytań dla dokumentów przy użyciu programu SQL (Structured Query Language) jako język zapytań JSON.</span><span class="sxs-lookup"><span data-stu-id="f0070-106">Microsoft Azure Cosmos DB supports querying documents using SQL (Structured Query Language) as a JSON query language.</span></span> <span data-ttu-id="f0070-107">Rozwiązania cosmos bazy danych jest naprawdę bez schematu.</span><span class="sxs-lookup"><span data-stu-id="f0070-107">Cosmos DB is truly schema-free.</span></span> <span data-ttu-id="f0070-108">Ze względu na jego zobowiązań toohello modelu danych JSON bezpośrednio wewnątrz aparatu bazy danych hello zapewnia automatycznego indeksowania dokumentów JSON bez konieczności jawnego schematu lub tworzenia indeksów pomocniczych.</span><span class="sxs-lookup"><span data-stu-id="f0070-108">By virtue of its commitment toohello JSON data model directly within hello database engine, it provides automatic indexing of JSON documents without requiring explicit schema or creation of secondary indexes.</span></span> 

<span data-ttu-id="f0070-109">Podczas projektowania rozwiązania Cosmos DB język zapytań hello, firma Microsoft ma dwa cele pamiętać:</span><span class="sxs-lookup"><span data-stu-id="f0070-109">While designing hello query language for Cosmos DB, we had two goals in mind:</span></span>

* <span data-ttu-id="f0070-110">Zamiast inventing nowy język zapytań JSON, możemy toosupport SQL.</span><span class="sxs-lookup"><span data-stu-id="f0070-110">Instead of inventing a new JSON query language, we wanted toosupport SQL.</span></span> <span data-ttu-id="f0070-111">SQL jest jednym z hello znanych i najbardziej popularnych języków zapytania.</span><span class="sxs-lookup"><span data-stu-id="f0070-111">SQL is one of hello most familiar and popular query languages.</span></span> <span data-ttu-id="f0070-112">Rozwiązania cosmos bazy danych SQL zapewnia model programowania posiadanie zaawansowane zapytania przez dokumentów JSON.</span><span class="sxs-lookup"><span data-stu-id="f0070-112">Cosmos DB SQL provides a formal programming model for rich queries over JSON documents.</span></span>
* <span data-ttu-id="f0070-113">Jako dokument bazy danych JSON może zostać uruchomiona JavaScript bezpośrednio w aparacie bazy danych hello możemy model programowania toouse JavaScript jako hello foundation dla naszych języka zapytań.</span><span class="sxs-lookup"><span data-stu-id="f0070-113">As a JSON document database capable of executing JavaScript directly in hello database engine, we wanted toouse JavaScript's programming model as hello foundation for our query language.</span></span> <span data-ttu-id="f0070-114">Witaj SQL interfejsu API usługi DocumentDB jest umieszczone w systemie typów języka JavaScript, wyrażenia i wywołania funkcji.</span><span class="sxs-lookup"><span data-stu-id="f0070-114">hello DocumentDB API SQL is rooted in JavaScript's type system, expression evaluation, and function invocation.</span></span> <span data-ttu-id="f0070-115">To w Włącz zapewnia fizyczną model programowania dla projekcje relacyjnych, hierarchicznych nawigacji między dokumentów JSON, self sprzężenia zapytania przestrzenne i wywołania funkcji zdefiniowanej przez użytkownika (UDF) zapisywane w całości w języku JavaScript, między innymi funkcjami.</span><span class="sxs-lookup"><span data-stu-id="f0070-115">This in-turn provides a natural programming model for relational projections, hierarchical navigation across JSON documents, self joins, spatial queries, and invocation of user-defined functions (UDFs) written entirely in JavaScript, among other features.</span></span> 

<span data-ttu-id="f0070-116">Mamy nadzieję, że te możliwości są klucza tooreducing hello tarcia między aplikacji hello i hello baz danych i decydują o produktywność deweloperów.</span><span class="sxs-lookup"><span data-stu-id="f0070-116">We believe that these capabilities are key tooreducing hello friction between hello application and hello database and are crucial for developer productivity.</span></span>

<span data-ttu-id="f0070-117">Zalecamy rozpoczęcie pracy od obejrzenia powitania po wideo, w którym Aravind Ramachandran wyświetlana podczas badania możliwości rozwiązania Cosmos DB i przechodząc naszych [Plac zabaw dla zapytań](http://www.documentdb.com/sql/demo), gdzie możesz wypróbować rozwiązania Cosmos bazy danych i uruchomić zapytań SQL naszym zestawie danych.</span><span class="sxs-lookup"><span data-stu-id="f0070-117">We recommend getting started by watching hello following video, where Aravind Ramachandran shows Cosmos DB's querying capabilities, and by visiting our [Query Playground](http://www.documentdb.com/sql/demo), where you can try out Cosmos DB and run SQL queries against our dataset.</span></span>

> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/DataExposedQueryingDocumentDB/player]
> 
> 

<span data-ttu-id="f0070-118">Zwracany jest toothis artykułu, w którym możemy zaczynać się samouczek zapytania SQL, który przeprowadzi Cię przez niektóre prostych dokumentów JSON i polecenia SQL.</span><span class="sxs-lookup"><span data-stu-id="f0070-118">Then, return toothis article, where we start with a SQL query tutorial that walks you through some simple JSON documents and SQL commands.</span></span>

## <span data-ttu-id="f0070-119"><a id="GettingStarted"></a>Wprowadzenie do poleceń SQL w bazie danych rozwiązania Cosmos</span><span class="sxs-lookup"><span data-stu-id="f0070-119"><a id="GettingStarted"></a>Getting started with SQL commands in Cosmos DB</span></span>
<span data-ttu-id="f0070-120">toosee rozwiązania Cosmos bazy danych SQL w pracy, możemy zaczynać się od kilku prostych dokumentów JSON i zapoznaj się z kilku prostych kwerend na nim.</span><span class="sxs-lookup"><span data-stu-id="f0070-120">toosee Cosmos DB SQL at work, let's begin with a few simple JSON documents and walk through some simple queries against it.</span></span> <span data-ttu-id="f0070-121">Należy wziąć pod uwagę następujące dwa dokumenty JSON o dwie grupy.</span><span class="sxs-lookup"><span data-stu-id="f0070-121">Consider these two JSON documents about two families.</span></span> <span data-ttu-id="f0070-122">Rozwiązania Cosmos DB firma Microsoft nie ma potrzeby toocreate schematy ani indeksów pomocniczych jawnie.</span><span class="sxs-lookup"><span data-stu-id="f0070-122">With Cosmos DB, we do not need toocreate any schemas or secondary indices explicitly.</span></span> <span data-ttu-id="f0070-123">Firma Microsoft po prostu muszą tooinsert hello JSON dokumenty tooa DB rozwiązania Cosmos kolekcji, a następnie zapytania.</span><span class="sxs-lookup"><span data-stu-id="f0070-123">We simply need tooinsert hello JSON documents tooa Cosmos DB collection and subsequently query.</span></span> <span data-ttu-id="f0070-124">W tym miejscu mamy proste JSON dokumentów dla rodziny Andersen hello, hello nadrzędne, podrzędne (i ich zwierząt domowych), adresu i informacji o rejestracji.</span><span class="sxs-lookup"><span data-stu-id="f0070-124">Here we have a simple JSON document for hello Andersen family, hello parents, children (and their pets), address, and registration information.</span></span> <span data-ttu-id="f0070-125">dokument Hello ma ciągów, liczb, wartości logiczne, tablic i właściwości zagnieżdżonych.</span><span class="sxs-lookup"><span data-stu-id="f0070-125">hello document has strings, numbers, Booleans, arrays, and nested properties.</span></span> 

<span data-ttu-id="f0070-126">**Dokument**</span><span class="sxs-lookup"><span data-stu-id="f0070-126">**Document**</span></span>  

```JSON
{
  "id": "AndersenFamily",
  "lastName": "Andersen",
  "parents": [
     { "firstName": "Thomas" },
     { "firstName": "Mary Kay"}
  ],
  "children": [
     {
         "firstName": "Henriette Thaulow", 
         "gender": "female", 
         "grade": 5,
         "pets": [{ "givenName": "Fluffy" }]
     }
  ],
  "address": { "state": "WA", "county": "King", "city": "seattle" },
  "creationDate": 1431620472,
  "isRegistered": true
}
```

<span data-ttu-id="f0070-127">W tym miejscu jest drugi dokument o jedną niewielka różnica — `givenName` i `familyName` są używane zamiast `firstName` i `lastName`.</span><span class="sxs-lookup"><span data-stu-id="f0070-127">Here's a second document with one subtle difference – `givenName` and `familyName` are used instead of `firstName` and `lastName`.</span></span>

<span data-ttu-id="f0070-128">**Dokument**</span><span class="sxs-lookup"><span data-stu-id="f0070-128">**Document**</span></span>  

```json
{
  "id": "WakefieldFamily",
  "parents": [
      { "familyName": "Wakefield", "givenName": "Robin" },
      { "familyName": "Miller", "givenName": "Ben" }
  ],
  "children": [
      {
        "familyName": "Merriam", 
        "givenName": "Jesse", 
        "gender": "female", "grade": 1,
        "pets": [
            { "givenName": "Goofy" },
            { "givenName": "Shadow" }
        ]
      },
      { 
        "familyName": "Miller", 
         "givenName": "Lisa", 
         "gender": "female", 
         "grade": 8 }
  ],
  "address": { "state": "NY", "county": "Manhattan", "city": "NY" },
  "creationDate": 1431620462,
  "isRegistered": false
}
```

<span data-ttu-id="f0070-129">Teraz spróbujmy kilka zapytań względem tego toounderstand danych niektóre hello klucza aspektów SQL interfejsu API usługi DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="f0070-129">Now let's try a few queries against this data toounderstand some of hello key aspects of DocumentDB API SQL.</span></span> <span data-ttu-id="f0070-130">Na przykład hello następujące zapytanie zwraca hello dokumentów, jeśli pole identyfikatora hello odpowiada `AndersenFamily`.</span><span class="sxs-lookup"><span data-stu-id="f0070-130">For example, hello following query returns hello documents where hello id field matches `AndersenFamily`.</span></span> <span data-ttu-id="f0070-131">Ponieważ jest ono `SELECT *`, hello wyników kwerendy hello jest hello pełnego dokumentu JSON:</span><span class="sxs-lookup"><span data-stu-id="f0070-131">Since it's a `SELECT *`, hello output of hello query is hello complete JSON document:</span></span>

<span data-ttu-id="f0070-132">**Zapytanie**</span><span class="sxs-lookup"><span data-stu-id="f0070-132">**Query**</span></span>

    SELECT * 
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="f0070-133">**Wyniki**</span><span class="sxs-lookup"><span data-stu-id="f0070-133">**Results**</span></span>

    [{
        "id": "AndersenFamily",
        "lastName": "Andersen",
        "parents": [
           { "firstName": "Thomas" },
           { "firstName": "Mary Kay"}
        ],
        "children": [
           {
               "firstName": "Henriette Thaulow", "gender": "female", "grade": 5,
               "pets": [{ "givenName": "Fluffy" }]
           }
        ],
        "address": { "state": "WA", "county": "King", "city": "seattle" },
        "creationDate": 1431620472,
        "isRegistered": true
    }]


<span data-ttu-id="f0070-134">Teraz Rozważmy hello potrzebujemy hello tooreformat dane wyjściowe JSON w różnych kształtu.</span><span class="sxs-lookup"><span data-stu-id="f0070-134">Now consider hello case where we need tooreformat hello JSON output in a different shape.</span></span> <span data-ttu-id="f0070-135">To zapytanie, projektów JSON nowy obiekt z dwóch wybranych pól, nazwa i Miasto, podczas miejscowość adresu hello ma hello sama nazwa jak hello stanu.</span><span class="sxs-lookup"><span data-stu-id="f0070-135">This query projects a new JSON object with two selected fields, Name and City, when hello address' city has hello same name as hello state.</span></span> <span data-ttu-id="f0070-136">W takim przypadku "NY, NY" jest zgodny.</span><span class="sxs-lookup"><span data-stu-id="f0070-136">In this case, "NY, NY" matches.</span></span>

<span data-ttu-id="f0070-137">**Zapytanie**</span><span class="sxs-lookup"><span data-stu-id="f0070-137">**Query**</span></span>    

    SELECT {"Name":f.id, "City":f.address.city} AS Family 
    FROM Families f 
    WHERE f.address.city = f.address.state

<span data-ttu-id="f0070-138">**Wyniki**</span><span class="sxs-lookup"><span data-stu-id="f0070-138">**Results**</span></span>

    [{
        "Family": {
            "Name": "WakefieldFamily", 
            "City": "NY"
        }
    }]


<span data-ttu-id="f0070-139">Hello dalej zapytanie zwraca podanymi nazwami hello dzieci w rodzinie hello odpowiada o identyfikatorze `WakefieldFamily` uporządkowanych według miasta hello zamieszkania.</span><span class="sxs-lookup"><span data-stu-id="f0070-139">hello next query returns all hello given names of children in hello family whose id matches `WakefieldFamily` ordered by hello city of residence.</span></span>

<span data-ttu-id="f0070-140">**Zapytanie**</span><span class="sxs-lookup"><span data-stu-id="f0070-140">**Query**</span></span>

    SELECT c.givenName 
    FROM Families f 
    JOIN c IN f.children 
    WHERE f.id = 'WakefieldFamily'
    ORDER BY f.address.city ASC

<span data-ttu-id="f0070-141">**Wyniki**</span><span class="sxs-lookup"><span data-stu-id="f0070-141">**Results**</span></span>

    [
      { "givenName": "Jesse" }, 
      { "givenName": "Lisa"}
    ]


<span data-ttu-id="f0070-142">Chcielibyśmy tooa uwagi toodraw kilka aspektów warte wymienienia hello DB rozwiązania Cosmos zapytania języka za pomocą hello przykłady, które firma Microsoft w tym samouczku wykonanej do tej pory:</span><span class="sxs-lookup"><span data-stu-id="f0070-142">We would like toodraw attention tooa few noteworthy aspects of hello Cosmos DB query language through hello examples we've seen so far:</span></span>  

* <span data-ttu-id="f0070-143">Ponieważ usługa DocumentDB interfejsu API SQL działa na wartości JSON, dotyczy drzewa w kształcie jednostek zamiast wierszy i kolumn.</span><span class="sxs-lookup"><span data-stu-id="f0070-143">Since DocumentDB API SQL works on JSON values, it deals with tree shaped entities instead of rows and columns.</span></span> <span data-ttu-id="f0070-144">W związku z tym hello języka umożliwia tak samo, jak znaleźć toonodes drzewa hello na dowolnej dowolnego głębokości `Node1.Node2.Node3…..Nodem`, podobne toorelational SQL odwołujący się toohello dwie części odwołania `<table>.<column>`.</span><span class="sxs-lookup"><span data-stu-id="f0070-144">Therefore, hello language lets you refer toonodes of hello tree at any arbitrary depth, like `Node1.Node2.Node3…..Nodem`, similar toorelational SQL referring toohello two part reference of `<table>.<column>`.</span></span>   
* <span data-ttu-id="f0070-145">Witaj strukturę zapytania języka współdziała z danych bez schematu.</span><span class="sxs-lookup"><span data-stu-id="f0070-145">hello structured query language works with schema-less data.</span></span> <span data-ttu-id="f0070-146">W związku z tym hello typu systemu potrzeb toobe granica dynamicznie.</span><span class="sxs-lookup"><span data-stu-id="f0070-146">Therefore, hello type system needs toobe bound dynamically.</span></span> <span data-ttu-id="f0070-147">Hello samym wyrażeniu można użyć instrukcji yield różnych typów w różnych dokumentach.</span><span class="sxs-lookup"><span data-stu-id="f0070-147">hello same expression could yield different types on different documents.</span></span> <span data-ttu-id="f0070-148">Witaj wyniku zapytania jest prawidłową wartością JSON, ale nie jest gwarantowana toobe stałego schematu.</span><span class="sxs-lookup"><span data-stu-id="f0070-148">hello result of a query is a valid JSON value, but is not guaranteed toobe of a fixed schema.</span></span>  
* <span data-ttu-id="f0070-149">Rozwiązania cosmos bazy danych obsługuje tylko ścisłe dokumentów JSON.</span><span class="sxs-lookup"><span data-stu-id="f0070-149">Cosmos DB only supports strict JSON documents.</span></span> <span data-ttu-id="f0070-150">Oznacza to, że system typów hello i wyrażenia są ograniczone toodeal tylko z typami JSON.</span><span class="sxs-lookup"><span data-stu-id="f0070-150">This means hello type system and expressions are restricted toodeal only with JSON types.</span></span> <span data-ttu-id="f0070-151">Zobacz toohello [specyfikacji JSON](http://www.json.org/) więcej szczegółów.</span><span class="sxs-lookup"><span data-stu-id="f0070-151">Refer toohello [JSON specification](http://www.json.org/) for more details.</span></span>  
* <span data-ttu-id="f0070-152">Kolekcja DB rozwiązania Cosmos jest kontenerem dokumentów JSON bez schematu.</span><span class="sxs-lookup"><span data-stu-id="f0070-152">A Cosmos DB collection is a schema-free container of JSON documents.</span></span> <span data-ttu-id="f0070-153">Witaj relacji w danych jednostki w obrębie dokumentów w kolekcji oraz niejawnie są przechwytywane przez zamknięcia, a nie przez klucz podstawowy i relacje klucza obcego.</span><span class="sxs-lookup"><span data-stu-id="f0070-153">hello relations in data entities within and across documents in a collection are implicitly captured by containment and not by primary key and foreign key relations.</span></span> <span data-ttu-id="f0070-154">To jest istotnym elementem warto wskazujące świetle sprzężenia wewnątrz dokumentu hello omówiony w dalszej części tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="f0070-154">This is an important aspect worth pointing out in light of hello intra-document joins discussed later in this article.</span></span>

## <span data-ttu-id="f0070-155"><a id="Indexing"></a>Indeksowanie rozwiązania cosmos bazy danych</span><span class="sxs-lookup"><span data-stu-id="f0070-155"><a id="Indexing"></a> Cosmos DB indexing</span></span>
<span data-ttu-id="f0070-156">Przed uzyskujemy do hello składni SQL usługi DocumentDB interfejsu API, warto eksploracji hello indeksowania projektu do rozwiązania Cosmos bazy danych.</span><span class="sxs-lookup"><span data-stu-id="f0070-156">Before we get into hello DocumentDB API SQL syntax, it is worth exploring hello indexing design in Cosmos DB.</span></span> 

<span data-ttu-id="f0070-157">Celem Hello indeksy bazy danych jest tooserve zapytań w swoich różnych formularzach i kształtów za zużycie zasobów minimalną (na przykład procesora CPU i operacjami wejścia/wyjścia) zapewniają dobrą wydajność i małe opóźnienia.</span><span class="sxs-lookup"><span data-stu-id="f0070-157">hello purpose of database indexes is tooserve queries in their various forms and shapes with minimum resource consumption (like CPU and input/output) while providing good throughput and low latency.</span></span> <span data-ttu-id="f0070-158">Często wybór hello hello indeksu prawo do wykonywania zapytań w bazie danych wymaga dużo planowania i eksperymenty.</span><span class="sxs-lookup"><span data-stu-id="f0070-158">Often, hello choice of hello right index for querying a database requires much planning and experimentation.</span></span> <span data-ttu-id="f0070-159">Takie podejście stanowi wyzwanie dla baz danych bez schematu, gdzie hello danych nie jest zgodna z ograniczeniami schematu tooa i rozwoju szybko.</span><span class="sxs-lookup"><span data-stu-id="f0070-159">This approach poses a challenge for schema-less databases where hello data doesn’t conform tooa strict schema and evolves rapidly.</span></span> 

<span data-ttu-id="f0070-160">W związku z tym podczas projektowania firma Microsoft hello DB rozwiązania Cosmos indeksowania podsystemu, możemy ustawić hello następujące cele:</span><span class="sxs-lookup"><span data-stu-id="f0070-160">Therefore, when we designed hello Cosmos DB indexing subsystem, we set hello following goals:</span></span>

* <span data-ttu-id="f0070-161">Indeksować dokumenty bez konieczności schematu: hello indeksowania podsystemu nie wymagają żadnych informacji o schemacie ani nie przyjmuje żadnych założeń dotyczących schematu dokumentów hello.</span><span class="sxs-lookup"><span data-stu-id="f0070-161">Index documents without requiring schema: hello indexing subsystem does not require any schema information or make any assumptions about schema of hello documents.</span></span> 
* <span data-ttu-id="f0070-162">Obsługuje wydajne, zaawansowanych zapytań hierarchicznej i relacyjne: indeks hello obsługuje język kwerendy DB rozwiązania Cosmos hello wydajnie, tym obsługę projekcje hierarchicznej i relacyjne.</span><span class="sxs-lookup"><span data-stu-id="f0070-162">Support for efficient, rich hierarchical, and relational queries: hello index supports hello Cosmos DB query language efficiently, including support for hierarchical and relational projections.</span></span>
* <span data-ttu-id="f0070-163">Obsługa zapytań spójne in face of trwały wolumin zapisów: zapisu wysokiej przepływności obciążeń z zapytaniami spójne hello indeks jest aktualizowany przyrostowo, wydajne i online jest w fazie hello utrzymujących woluminu zapisów.</span><span class="sxs-lookup"><span data-stu-id="f0070-163">Support for consistent queries in face of a sustained volume of writes: For high write throughput workloads with consistent queries, hello index is updated incrementally, efficiently, and online in hello face of a sustained volume of writes.</span></span> <span data-ttu-id="f0070-164">Aktualizacja spójne indeksu Hello jest istotne tooserve hello zapytań na poziomie spójności hello, w których hello skonfigurowany użytkownik hello dokumentu usługi.</span><span class="sxs-lookup"><span data-stu-id="f0070-164">hello consistent index update is crucial tooserve hello queries at hello consistency level in which hello user configured hello document service.</span></span>
* <span data-ttu-id="f0070-165">Obsługa wielu dzierżawców: podana hello oparte na rezerwacjach modelu dla zarządu zasobów między dzierżawcami, indeks aktualizacji są wykonywane w ramach budżetu hello zasobów systemowych (CPU, pamięci i liczby operacji wejścia/wyjścia na sekundę) przydzielone dla replik.</span><span class="sxs-lookup"><span data-stu-id="f0070-165">Support for multi-tenancy: Given hello reservation-based model for resource governance across tenants, index updates are performed within hello budget of system resources (CPU, memory, and input/output operations per second) allocated per replica.</span></span> 
* <span data-ttu-id="f0070-166">Wydajność magazynu: opłacalności, hello na dysku magazynu narzut hello indeksu jest ograniczone i przewidywalne.</span><span class="sxs-lookup"><span data-stu-id="f0070-166">Storage efficiency: For cost effectiveness, hello on-disk storage overhead of hello index is bounded and predictable.</span></span> <span data-ttu-id="f0070-167">Jest to ważne, ponieważ DB rozwiązania Cosmos umożliwia hello developer toomake opartych na kosztach wady i zalety między narzut indeksu w relacji toohello kwerendy wydajności.</span><span class="sxs-lookup"><span data-stu-id="f0070-167">This is crucial because Cosmos DB allows hello developer toomake cost-based tradeoffs between index overhead in relation toohello query performance.</span></span>  

<span data-ttu-id="f0070-168">Zobacz toohello [przykłady Azure DB rozwiązania Cosmos](https://github.com/Azure/azure-documentdb-net) w witrynie MSDN dla przykładów przedstawiający sposób tooconfigure hello zasady indeksowania dla kolekcji.</span><span class="sxs-lookup"><span data-stu-id="f0070-168">Refer toohello [Azure Cosmos DB samples](https://github.com/Azure/azure-documentdb-net) on MSDN for samples showing how tooconfigure hello indexing policy for a collection.</span></span> <span data-ttu-id="f0070-169">Teraz Załóż do szczegółów hello hello składni Azure rozwiązania Cosmos bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="f0070-169">Let’s now get into hello details of hello Azure Cosmos DB SQL syntax.</span></span>

## <span data-ttu-id="f0070-170"><a id="Basics"></a>Podstawowe informacje o kwerendzie Azure rozwiązania Cosmos bazy danych SQL</span><span class="sxs-lookup"><span data-stu-id="f0070-170"><a id="Basics"></a>Basics of an Azure Cosmos DB SQL query</span></span>
<span data-ttu-id="f0070-171">Co kwerenda składa się z klauzuli SELECT i opcjonalnie FROM i klauzulach WHERE w standardach ANSI SQL.</span><span class="sxs-lookup"><span data-stu-id="f0070-171">Every query consists of a SELECT clause and optional FROM and WHERE clauses per ANSI-SQL standards.</span></span> <span data-ttu-id="f0070-172">Zazwyczaj dla każdego zapytania źródła hello w klauzuli FROM hello wyliczeniu.</span><span class="sxs-lookup"><span data-stu-id="f0070-172">Typically, for each query, hello source in hello FROM clause is enumerated.</span></span> <span data-ttu-id="f0070-173">Następnie hello filtrowanie w klauzuli WHERE jest stosowany na powitania źródła tooretrieve hello podzbiór dokumentów JSON.</span><span class="sxs-lookup"><span data-stu-id="f0070-173">Then hello filter in hello WHERE clause is applied on hello source tooretrieve a subset of JSON documents.</span></span> <span data-ttu-id="f0070-174">Na koniec jest używana klauzula SELECT hello tooproject hello żądanej wartości JSON w hello listy wyboru.</span><span class="sxs-lookup"><span data-stu-id="f0070-174">Finally, hello SELECT clause is used tooproject hello requested JSON values in hello select list.</span></span>

    SELECT <select_list> 
    [FROM <from_specification>] 
    [WHERE <filter_condition>]
    [ORDER BY <sort_specification]    


## <span data-ttu-id="f0070-175"><a id="FromClause"></a>Klauzula FROM</span><span class="sxs-lookup"><span data-stu-id="f0070-175"><a id="FromClause"></a>FROM clause</span></span>
<span data-ttu-id="f0070-176">Witaj `FROM <from_specification>` klauzuli jest opcjonalny, jeśli źródło hello jest filtrowana lub przewidywane później w zapytaniu hello.</span><span class="sxs-lookup"><span data-stu-id="f0070-176">hello `FROM <from_specification>` clause is optional unless hello source is filtered or projected later in hello query.</span></span> <span data-ttu-id="f0070-177">Celem Hello klauzulę jest źródło danych hello toospecify na które hello zapytania musi działać.</span><span class="sxs-lookup"><span data-stu-id="f0070-177">hello purpose of this clause is toospecify hello data source upon which hello query must operate.</span></span> <span data-ttu-id="f0070-178">Często całą kolekcję hello jest hello źródła, ale zamiast tego można określić podzbiór hello kolekcji.</span><span class="sxs-lookup"><span data-stu-id="f0070-178">Commonly hello whole collection is hello source, but one can specify a subset of hello collection instead.</span></span> 

<span data-ttu-id="f0070-179">Zapytanie, takich jak `SELECT * FROM Families` oznacza, że hello całą kolekcję rodzin źródła hello za pośrednictwem których tooenumerate.</span><span class="sxs-lookup"><span data-stu-id="f0070-179">A query like `SELECT * FROM Families` indicates that hello entire Families collection is hello source over which tooenumerate.</span></span> <span data-ttu-id="f0070-180">Specjalny identyfikator głównego może być używane toorepresent hello kolekcji zamiast nazwy kolekcji hello.</span><span class="sxs-lookup"><span data-stu-id="f0070-180">A special identifier ROOT can be used toorepresent hello collection instead of using hello collection name.</span></span> <span data-ttu-id="f0070-181">Witaj Poniższa lista zawiera hello reguły, które są wymuszane na zapytanie:</span><span class="sxs-lookup"><span data-stu-id="f0070-181">hello following list contains hello rules that are enforced per query:</span></span>

* <span data-ttu-id="f0070-182">Witaj kolekcji można używać z aliasem, takich jak `SELECT f.id FROM Families AS f` lub po prostu `SELECT f.id FROM Families f`.</span><span class="sxs-lookup"><span data-stu-id="f0070-182">hello collection can be aliased, such as `SELECT f.id FROM Families AS f` or simply `SELECT f.id FROM Families f`.</span></span> <span data-ttu-id="f0070-183">W tym miejscu `f` jest odpowiednikiem hello `Families`.</span><span class="sxs-lookup"><span data-stu-id="f0070-183">Here `f` is hello equivalent of `Families`.</span></span> <span data-ttu-id="f0070-184">`AS`jest to identyfikator hello tooalias optional-słowo kluczowe.</span><span class="sxs-lookup"><span data-stu-id="f0070-184">`AS` is an optional keyword tooalias hello identifier.</span></span>
* <span data-ttu-id="f0070-185">Raz, ponieważ hello oryginalne źródło nie może być powiązany.</span><span class="sxs-lookup"><span data-stu-id="f0070-185">Once aliased, hello original source cannot be bound.</span></span> <span data-ttu-id="f0070-186">Na przykład `SELECT Families.id FROM Families f` ma nieprawidłową składnię, ponieważ już nie można rozpoznać identyfikatora hello "Rodzin".</span><span class="sxs-lookup"><span data-stu-id="f0070-186">For example, `SELECT Families.id FROM Families f` is syntactically invalid since hello identifier "Families" cannot be resolved anymore.</span></span>
* <span data-ttu-id="f0070-187">Wszystkie właściwości, które wymagają toobe odwołuje się do musi być w pełni kwalifikowana.</span><span class="sxs-lookup"><span data-stu-id="f0070-187">All properties that need toobe referenced must be fully qualified.</span></span> <span data-ttu-id="f0070-188">Hello braku schematu ścisłego przestrzegania, jest to wymuszone tooavoid powiązań niejednoznaczne.</span><span class="sxs-lookup"><span data-stu-id="f0070-188">In hello absence of strict schema adherence, this is enforced tooavoid any ambiguous bindings.</span></span> <span data-ttu-id="f0070-189">W związku z tym `SELECT id FROM Families f` ma nieprawidłową składnię od właściwości hello `id` nie jest powiązany.</span><span class="sxs-lookup"><span data-stu-id="f0070-189">Therefore, `SELECT id FROM Families f` is syntactically invalid since hello property `id` is not bound.</span></span>

### <a name="subdocuments"></a><span data-ttu-id="f0070-190">Dokumenty podrzędne</span><span class="sxs-lookup"><span data-stu-id="f0070-190">Subdocuments</span></span>
<span data-ttu-id="f0070-191">Źródło Hello można także mniejszego podzestawu tooa mniejsze.</span><span class="sxs-lookup"><span data-stu-id="f0070-191">hello source can also be reduced tooa smaller subset.</span></span> <span data-ttu-id="f0070-192">Dla wystąpienia tooenumerating tylko poddrzewo do każdego dokumentu, hello subroot może następnie stać się hello źródła, jak pokazano w hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="f0070-192">For instance, tooenumerating only a subtree in each document, hello subroot could then become hello source, as shown in hello following example:</span></span>

<span data-ttu-id="f0070-193">**Zapytanie**</span><span class="sxs-lookup"><span data-stu-id="f0070-193">**Query**</span></span>

    SELECT * 
    FROM Families.children

<span data-ttu-id="f0070-194">**Wyniki**</span><span class="sxs-lookup"><span data-stu-id="f0070-194">**Results**</span></span>  

    [
      [
        {
            "firstName": "Henriette Thaulow",
            "gender": "female",
            "grade": 5,
            "pets": [
              {
                  "givenName": "Fluffy"
              }
            ]
        }
      ],
      [
        {
            "familyName": "Merriam",
            "givenName": "Jesse",
            "gender": "female",
            "grade": 1
        },
        {
            "familyName": "Miller",
            "givenName": "Lisa",
            "gender": "female",
            "grade": 8
        }
      ]
    ]

<span data-ttu-id="f0070-195">Hello powyżej przykład tablicy są używane jako źródło hello, obiektu również mogą być użyte jako źródło hello, w którym jest, co przedstawiono na powitania poniższy przykład: wszelkie prawidłową wartość JSON (nie zdefiniowano), który znajduje się w źródle hello jest uwzględnione w w wyniku hello Witaj zapytania.</span><span class="sxs-lookup"><span data-stu-id="f0070-195">While hello above example used an array as hello source, an object could also be used as hello source, which is what's shown in hello following example: Any valid JSON value (not undefined) that can be found in hello source is considered for inclusion in hello result of hello query.</span></span> <span data-ttu-id="f0070-196">Jeśli nie masz niektórych rodzin `address.state` wartość, są wyłączone w wyniku zapytania hello.</span><span class="sxs-lookup"><span data-stu-id="f0070-196">If some families don’t have an `address.state` value, they are excluded in hello query result.</span></span>

<span data-ttu-id="f0070-197">**Zapytanie**</span><span class="sxs-lookup"><span data-stu-id="f0070-197">**Query**</span></span>

    SELECT * 
    FROM Families.address.state

<span data-ttu-id="f0070-198">**Wyniki**</span><span class="sxs-lookup"><span data-stu-id="f0070-198">**Results**</span></span>

    [
      "WA", 
      "NY"
    ]


## <span data-ttu-id="f0070-199"><a id="WhereClause"></a>Klauzula WHERE</span><span class="sxs-lookup"><span data-stu-id="f0070-199"><a id="WhereClause"></a>WHERE clause</span></span>
<span data-ttu-id="f0070-200">Witaj w klauzuli WHERE (**`WHERE <filter_condition>`**) jest opcjonalna.</span><span class="sxs-lookup"><span data-stu-id="f0070-200">hello WHERE clause (**`WHERE <filter_condition>`**) is optional.</span></span> <span data-ttu-id="f0070-201">Określa się, że warunki hello hello dokumentów JSON podane przez źródło hello powinny spełniać toobe kolejności wchodzącego w skład hello wynik.</span><span class="sxs-lookup"><span data-stu-id="f0070-201">It specifies hello condition(s) that hello JSON documents provided by hello source must satisfy in order toobe included as part of hello result.</span></span> <span data-ttu-id="f0070-202">Należy ocenić dowolnych dokumentów JSON hello określone warunki zbyt "true" toobe brany pod uwagę podczas hello wynik.</span><span class="sxs-lookup"><span data-stu-id="f0070-202">Any JSON document must evaluate hello specified conditions too"true" toobe considered for hello result.</span></span> <span data-ttu-id="f0070-203">Witaj, gdy jest używana klauzula przez warstwę indeksu hello w kolejności toodetermine hello bezwzględną najmniejszą podzbiór dokumentów źródła, które mogą być częścią hello wynik.</span><span class="sxs-lookup"><span data-stu-id="f0070-203">hello WHERE clause is used by hello index layer in order toodetermine hello absolute smallest subset of source documents that can be part of hello result.</span></span> 

<span data-ttu-id="f0070-204">Witaj następujące zapytanie żądań dokumentów, które zawierają właściwość name o wartości `AndersenFamily`.</span><span class="sxs-lookup"><span data-stu-id="f0070-204">hello following query requests documents that contain a name property whose value is `AndersenFamily`.</span></span> <span data-ttu-id="f0070-205">Każdy dokument, który nie ma właściwości name, lub gdy hello wartość nie pasuje do `AndersenFamily` jest wyłączone.</span><span class="sxs-lookup"><span data-stu-id="f0070-205">Any other document that does not have a name property, or where hello value does not match `AndersenFamily` is excluded.</span></span> 

<span data-ttu-id="f0070-206">**Zapytanie**</span><span class="sxs-lookup"><span data-stu-id="f0070-206">**Query**</span></span>

    SELECT f.address
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="f0070-207">**Wyniki**</span><span class="sxs-lookup"><span data-stu-id="f0070-207">**Results**</span></span>

    [{
      "address": {
        "state": "WA", 
        "county": "King", 
        "city": "seattle"
      }
    }]


<span data-ttu-id="f0070-208">Witaj poprzednim przykładzie pokazano zapytania prostego równości.</span><span class="sxs-lookup"><span data-stu-id="f0070-208">hello previous example showed a simple equality query.</span></span> <span data-ttu-id="f0070-209">SQL interfejsu API usługi DocumentDB obsługuje również wiele wyrażeń skalarnych.</span><span class="sxs-lookup"><span data-stu-id="f0070-209">DocumentDB API SQL also supports a variety of scalar expressions.</span></span> <span data-ttu-id="f0070-210">Witaj najczęściej używane są wyrażenia binarne i jednoargumentowy.</span><span class="sxs-lookup"><span data-stu-id="f0070-210">hello most commonly used are binary and unary expressions.</span></span> <span data-ttu-id="f0070-211">Odwołań do właściwości z obiektu JSON źródła hello są również prawidłowe wyrażenia.</span><span class="sxs-lookup"><span data-stu-id="f0070-211">Property references from hello source JSON object are also valid expressions.</span></span> 

<span data-ttu-id="f0070-212">następujące operatory binarne Hello są obecnie obsługiwane i mogą być używane w zapytaniach pokazane na powitania następujące przykłady:</span><span class="sxs-lookup"><span data-stu-id="f0070-212">hello following binary operators are currently supported and can be used in queries as shown in hello following examples:</span></span>  

<table>
<tr>
<td><span data-ttu-id="f0070-213">Operacje arytmetyczne</span><span class="sxs-lookup"><span data-stu-id="f0070-213">Arithmetic</span></span></td>    
<td><span data-ttu-id="f0070-214">+,-,*,/,%</span><span class="sxs-lookup"><span data-stu-id="f0070-214">+,-,*,/,%</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="f0070-215">Alternatywy bitowej</span><span class="sxs-lookup"><span data-stu-id="f0070-215">Bitwise</span></span></td>    
<td><span data-ttu-id="f0070-216">|, &, ^, <<>>,, >>> (zero wypełnienia przesunięcia w prawo)</span><span class="sxs-lookup"><span data-stu-id="f0070-216">|, &, ^, <<, >>, >>> (zero-fill right shift)</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="f0070-217">Logiczne</span><span class="sxs-lookup"><span data-stu-id="f0070-217">Logical</span></span></td>
<td><span data-ttu-id="f0070-218">I, LUB NIE</span><span class="sxs-lookup"><span data-stu-id="f0070-218">AND, OR, NOT</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="f0070-219">Porównanie</span><span class="sxs-lookup"><span data-stu-id="f0070-219">Comparison</span></span></td>    
<td><span data-ttu-id="f0070-220">=, !=, &lt;, &gt;, &lt;=, &gt;=, <></span><span class="sxs-lookup"><span data-stu-id="f0070-220">=, !=, &lt;, &gt;, &lt;=, &gt;=, <></span></span></td>
</tr>
<tr>
<td><span data-ttu-id="f0070-221">Ciąg</span><span class="sxs-lookup"><span data-stu-id="f0070-221">String</span></span></td>    
<td><span data-ttu-id="f0070-222">|| (Połącz)</span><span class="sxs-lookup"><span data-stu-id="f0070-222">|| (concatenate)</span></span></td>
</tr>
</table>  


<span data-ttu-id="f0070-223">Spójrzmy na kilka zapytań przy użyciu operatorów binarnych.</span><span class="sxs-lookup"><span data-stu-id="f0070-223">Let’s take a look at some queries using binary operators.</span></span>

    SELECT * 
    FROM Families.children[0] c
    WHERE c.grade % 2 = 1     -- matching grades == 5, 1

    SELECT * 
    FROM Families.children[0] c
    WHERE c.grade ^ 4 = 1    -- matching grades == 5

    SELECT *
    FROM Families.children[0] c
    WHERE c.grade >= 5     -- matching grades == 5


<span data-ttu-id="f0070-224">Operatory jednoargumentowe Hello +,-, ~ nie są również obsługiwane i może być używany w zapytania, jak pokazano w hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="f0070-224">hello unary operators +,-, ~ and NOT are also supported, and can be used inside queries as shown in hello following example:</span></span>

    SELECT *
    FROM Families.children[0] c
    WHERE NOT(c.grade = 5)  -- matching grades == 1

    SELECT *
    FROM Families.children[0] c
    WHERE (-c.grade = -5)  -- matching grades == 5



<span data-ttu-id="f0070-225">Ponadto toobinary i jednoargumentowe operatory, odwołań do właściwości dozwolone są też.</span><span class="sxs-lookup"><span data-stu-id="f0070-225">In addition toobinary and unary operators, property references are also allowed.</span></span> <span data-ttu-id="f0070-226">Na przykład `SELECT * FROM Families f WHERE f.isRegistered` zwraca hello dokument JSON zawierający właściwości hello `isRegistered` gdy wartość właściwości hello jest równy toohello JSON `true` wartość.</span><span class="sxs-lookup"><span data-stu-id="f0070-226">For example, `SELECT * FROM Families f WHERE f.isRegistered` returns hello JSON document containing hello property `isRegistered` where hello property's value is equal toohello JSON `true` value.</span></span> <span data-ttu-id="f0070-227">Inne wartości (wartość false, wartość null, niezdefiniowane, `<number>`, `<string>`, `<object>`, `<array>`, itd.) prowadzi toohello dokumentu źródłowego są wykluczone z hello wyników.</span><span class="sxs-lookup"><span data-stu-id="f0070-227">Any other values (false, null, Undefined, `<number>`, `<string>`, `<object>`, `<array>`, etc.) leads toohello source document being excluded from hello result.</span></span> 

### <a name="equality-and-comparison-operators"></a><span data-ttu-id="f0070-228">Operatory równości i porównania</span><span class="sxs-lookup"><span data-stu-id="f0070-228">Equality and comparison operators</span></span>
<span data-ttu-id="f0070-229">Hello poniższej tabeli przedstawiono hello wynik porównania równości w usłudze DocumentDB interfejsu API SQL między żadnych dwa typy JSON.</span><span class="sxs-lookup"><span data-stu-id="f0070-229">hello following table shows hello result of equality comparisons in DocumentDB API SQL between any two JSON types.</span></span>

<table style = "width:300px">
   <tbody>
      <tr>
         <td valign="top"><span data-ttu-id="f0070-230">
            <strong>OP</strong>
         </span><span class="sxs-lookup"><span data-stu-id="f0070-230">
            <strong>Op</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="f0070-231">
            <strong>Niezdefiniowana</strong>
         </span><span class="sxs-lookup"><span data-stu-id="f0070-231">
            <strong>Undefined</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="f0070-232">
            <strong>Wartość null</strong>
         </span><span class="sxs-lookup"><span data-stu-id="f0070-232">
            <strong>Null</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="f0070-233">
            <strong>Wartość logiczna</strong>
         </span><span class="sxs-lookup"><span data-stu-id="f0070-233">
            <strong>Boolean</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="f0070-234">
            <strong>Numer</strong>
         </span><span class="sxs-lookup"><span data-stu-id="f0070-234">
            <strong>Number</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="f0070-235">
            <strong>Ciąg</strong>
         </span><span class="sxs-lookup"><span data-stu-id="f0070-235">
            <strong>String</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="f0070-236">
            <strong>Obiekt</strong>
         </span><span class="sxs-lookup"><span data-stu-id="f0070-236">
            <strong>Object</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="f0070-237">
            <strong>Tablica</strong>
         </span><span class="sxs-lookup"><span data-stu-id="f0070-237">
            <strong>Array</strong>
         </span></span></td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="f0070-238">
            <strong>Niezdefiniowana<strong>
         </span><span class="sxs-lookup"><span data-stu-id="f0070-238">
            <strong>Undefined<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="f0070-239">Niezdefiniowana</span><span class="sxs-lookup"><span data-stu-id="f0070-239">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="f0070-240">Niezdefiniowana</span><span class="sxs-lookup"><span data-stu-id="f0070-240">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="f0070-241">Niezdefiniowana</span><span class="sxs-lookup"><span data-stu-id="f0070-241">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="f0070-242">Niezdefiniowana</span><span class="sxs-lookup"><span data-stu-id="f0070-242">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="f0070-243">Niezdefiniowana</span><span class="sxs-lookup"><span data-stu-id="f0070-243">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="f0070-244">Niezdefiniowana</span><span class="sxs-lookup"><span data-stu-id="f0070-244">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="f0070-245">Niezdefiniowana</span><span class="sxs-lookup"><span data-stu-id="f0070-245">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="f0070-246">
            <strong>Wartość null<strong>
         </span><span class="sxs-lookup"><span data-stu-id="f0070-246">
            <strong>Null<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="f0070-247">Niezdefiniowana</span><span class="sxs-lookup"><span data-stu-id="f0070-247">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="f0070-248">
            <strong>OK</strong>
         </span><span class="sxs-lookup"><span data-stu-id="f0070-248">
            <strong>OK</strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="f0070-249">Niezdefiniowana</span><span class="sxs-lookup"><span data-stu-id="f0070-249">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="f0070-250">Niezdefiniowana</span><span class="sxs-lookup"><span data-stu-id="f0070-250">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="f0070-251">Niezdefiniowana</span><span class="sxs-lookup"><span data-stu-id="f0070-251">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="f0070-252">Niezdefiniowana</span><span class="sxs-lookup"><span data-stu-id="f0070-252">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="f0070-253">Niezdefiniowana</span><span class="sxs-lookup"><span data-stu-id="f0070-253">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="f0070-254">
            <strong>Wartość logiczna<strong>
         </span><span class="sxs-lookup"><span data-stu-id="f0070-254">
            <strong>Boolean<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="f0070-255">Niezdefiniowana</span><span class="sxs-lookup"><span data-stu-id="f0070-255">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="f0070-256">Niezdefiniowana</span><span class="sxs-lookup"><span data-stu-id="f0070-256">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="f0070-257">
            <strong>OK</strong>
         </span><span class="sxs-lookup"><span data-stu-id="f0070-257">
            <strong>OK</strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="f0070-258">Niezdefiniowana</span><span class="sxs-lookup"><span data-stu-id="f0070-258">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="f0070-259">Niezdefiniowana</span><span class="sxs-lookup"><span data-stu-id="f0070-259">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="f0070-260">Niezdefiniowana</span><span class="sxs-lookup"><span data-stu-id="f0070-260">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="f0070-261">Niezdefiniowana</span><span class="sxs-lookup"><span data-stu-id="f0070-261">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="f0070-262">
            <strong>Numer<strong>
         </span><span class="sxs-lookup"><span data-stu-id="f0070-262">
            <strong>Number<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="f0070-263">Niezdefiniowana</span><span class="sxs-lookup"><span data-stu-id="f0070-263">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="f0070-264">Niezdefiniowana</span><span class="sxs-lookup"><span data-stu-id="f0070-264">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="f0070-265">Niezdefiniowana</span><span class="sxs-lookup"><span data-stu-id="f0070-265">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="f0070-266">
            <strong>OK</strong>
         </span><span class="sxs-lookup"><span data-stu-id="f0070-266">
            <strong>OK</strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="f0070-267">Niezdefiniowana</span><span class="sxs-lookup"><span data-stu-id="f0070-267">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="f0070-268">Niezdefiniowana</span><span class="sxs-lookup"><span data-stu-id="f0070-268">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="f0070-269">Niezdefiniowana</span><span class="sxs-lookup"><span data-stu-id="f0070-269">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="f0070-270">
            <strong>Ciąg<strong>
         </span><span class="sxs-lookup"><span data-stu-id="f0070-270">
            <strong>String<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="f0070-271">Niezdefiniowana</span><span class="sxs-lookup"><span data-stu-id="f0070-271">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="f0070-272">Niezdefiniowana</span><span class="sxs-lookup"><span data-stu-id="f0070-272">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="f0070-273">Niezdefiniowana</span><span class="sxs-lookup"><span data-stu-id="f0070-273">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="f0070-274">Niezdefiniowana</span><span class="sxs-lookup"><span data-stu-id="f0070-274">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="f0070-275">
            <strong>OK</strong>
         </span><span class="sxs-lookup"><span data-stu-id="f0070-275">
            <strong>OK</strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="f0070-276">Niezdefiniowana</span><span class="sxs-lookup"><span data-stu-id="f0070-276">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="f0070-277">Niezdefiniowana</span><span class="sxs-lookup"><span data-stu-id="f0070-277">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="f0070-278">
            <strong>Obiekt<strong>
         </span><span class="sxs-lookup"><span data-stu-id="f0070-278">
            <strong>Object<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="f0070-279">Niezdefiniowana</span><span class="sxs-lookup"><span data-stu-id="f0070-279">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="f0070-280">Niezdefiniowana</span><span class="sxs-lookup"><span data-stu-id="f0070-280">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="f0070-281">Niezdefiniowana</span><span class="sxs-lookup"><span data-stu-id="f0070-281">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="f0070-282">Niezdefiniowana</span><span class="sxs-lookup"><span data-stu-id="f0070-282">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="f0070-283">Niezdefiniowana</span><span class="sxs-lookup"><span data-stu-id="f0070-283">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="f0070-284">
            <strong>OK</strong>
         </span><span class="sxs-lookup"><span data-stu-id="f0070-284">
            <strong>OK</strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="f0070-285">Niezdefiniowana</span><span class="sxs-lookup"><span data-stu-id="f0070-285">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="f0070-286">
            <strong>Tablica<strong>
         </span><span class="sxs-lookup"><span data-stu-id="f0070-286">
            <strong>Array<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="f0070-287">Niezdefiniowana</span><span class="sxs-lookup"><span data-stu-id="f0070-287">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="f0070-288">Niezdefiniowana</span><span class="sxs-lookup"><span data-stu-id="f0070-288">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="f0070-289">Niezdefiniowana</span><span class="sxs-lookup"><span data-stu-id="f0070-289">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="f0070-290">Niezdefiniowana</span><span class="sxs-lookup"><span data-stu-id="f0070-290">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="f0070-291">Niezdefiniowana</span><span class="sxs-lookup"><span data-stu-id="f0070-291">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="f0070-292">Niezdefiniowana</span><span class="sxs-lookup"><span data-stu-id="f0070-292">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="f0070-293">
            <strong>OK</strong>
         </span><span class="sxs-lookup"><span data-stu-id="f0070-293">
            <strong>OK</strong>
         </span></span></td>
      </tr>
   </tbody>
</table>

<span data-ttu-id="f0070-294">Dla innych operatory porównania, takich jak >, > =,! =, < i < =, hello mają zastosowanie następujące reguły:</span><span class="sxs-lookup"><span data-stu-id="f0070-294">For other comparison operators such as >, >=, !=, < and <=, hello following rules apply:</span></span>   

* <span data-ttu-id="f0070-295">Porównanie różnych typów powoduje Undefined.</span><span class="sxs-lookup"><span data-stu-id="f0070-295">Comparison across types results in Undefined.</span></span>
* <span data-ttu-id="f0070-296">Porównanie między dwoma obiektami lub dwóch stałych powoduje Undefined.</span><span class="sxs-lookup"><span data-stu-id="f0070-296">Comparison between two objects or two arrays results in Undefined.</span></span>   

<span data-ttu-id="f0070-297">Jeśli wynik hello hello wyrażenie skalarne w filtrze hello jest niezdefiniowana, hello odpowiedni dokument nie będzie uwzględniony w wyniku hello, ponieważ niezdefiniowane nie logicznie są zbyt "true" równoważne.</span><span class="sxs-lookup"><span data-stu-id="f0070-297">If hello result of hello scalar expression in hello filter is Undefined, hello corresponding document would not be included in hello result, since Undefined doesn't logically equate too"true".</span></span>

### <a name="between-keyword"></a><span data-ttu-id="f0070-298">MIĘDZY — słowo kluczowe</span><span class="sxs-lookup"><span data-stu-id="f0070-298">BETWEEN keyword</span></span>
<span data-ttu-id="f0070-299">Umożliwia także hello BETWEEN — słowo kluczowe tooexpress zapytań dotyczących zakresów wartości podobnie jak w języku SQL ANSI.</span><span class="sxs-lookup"><span data-stu-id="f0070-299">You can also use hello BETWEEN keyword tooexpress queries against ranges of values like in ANSI SQL.</span></span> <span data-ttu-id="f0070-300">MIĘDZY może służyć przed ciągów lub cyfry.</span><span class="sxs-lookup"><span data-stu-id="f0070-300">BETWEEN can be used against strings or numbers.</span></span>

<span data-ttu-id="f0070-301">Na przykład ta kwerenda zwraca wszystkie dokumenty rodziny, w których hello pierwszy element podrzędny klasy jest między 1-5, (zarówno z wartościami granicznymi).</span><span class="sxs-lookup"><span data-stu-id="f0070-301">For example, this query returns all family documents in which hello first child's grade is between 1-5 (both inclusive).</span></span> 

    SELECT *
    FROM Families.children[0] c
    WHERE c.grade BETWEEN 1 AND 5

<span data-ttu-id="f0070-302">W odróżnieniu od w ANSI SQL umożliwia także klauzuli BETWEEN hello w klauzuli FROM hello podobnie jak w hello poniższy przykład.</span><span class="sxs-lookup"><span data-stu-id="f0070-302">Unlike in ANSI-SQL, you can also use hello BETWEEN clause in hello FROM clause like in hello following example.</span></span>

    SELECT (c.grade BETWEEN 0 AND 10)
    FROM Families.children[0] c

<span data-ttu-id="f0070-303">Dla krótszego czasu wykonywania zapytania Pamiętaj toocreate zasady indeksowania korzysta z typu indeksu zakresu względem dowolnego liczbowego właściwości/ścieżek, które są filtrowane w klauzuli BETWEEN hello.</span><span class="sxs-lookup"><span data-stu-id="f0070-303">For faster query execution times, remember toocreate an indexing policy that uses a range index type against any numeric properties/paths that are filtered in hello BETWEEN clause.</span></span> 

<span data-ttu-id="f0070-304">Witaj podstawowa różnica między przy użyciu BETWEEN interfejsu API usługi DocumentDB i ANSI SQL jest czy można wyrazić zakresu zapytań dotyczących właściwości mieszane typy — na przykład może być "klasy" być liczbą (5) w niektórych dokumentów i ciągi w innych ("grade4").</span><span class="sxs-lookup"><span data-stu-id="f0070-304">hello main difference between using BETWEEN in DocumentDB API and ANSI SQL is that you can express range queries against properties of mixed types – for example, you might have "grade" be a number (5) in some documents and strings in others ("grade4").</span></span> <span data-ttu-id="f0070-305">W takich przypadkach takich jak w języku JavaScript, porównanie dwóch różnych typów wyników w "undefined" i hello dokumentu zostanie pominięte.</span><span class="sxs-lookup"><span data-stu-id="f0070-305">In these cases, like in JavaScript, a comparison between two different types results in "undefined", and hello document will be skipped.</span></span>

### <a name="logical-and-or-and-not-operators"></a><span data-ttu-id="f0070-306">Logiczne (AND, OR i NOT) operatory</span><span class="sxs-lookup"><span data-stu-id="f0070-306">Logical (AND, OR and NOT) operators</span></span>
<span data-ttu-id="f0070-307">Operatory logiczne działają na wartości logiczne.</span><span class="sxs-lookup"><span data-stu-id="f0070-307">Logical operators operate on Boolean values.</span></span> <span data-ttu-id="f0070-308">Hello logicznej prawdy tabele te operatory są wyświetlane w hello następujące tabele.</span><span class="sxs-lookup"><span data-stu-id="f0070-308">hello logical truth tables for these operators are shown in hello following tables.</span></span>

| <span data-ttu-id="f0070-309">LUB</span><span class="sxs-lookup"><span data-stu-id="f0070-309">OR</span></span> | <span data-ttu-id="f0070-310">True</span><span class="sxs-lookup"><span data-stu-id="f0070-310">True</span></span> | <span data-ttu-id="f0070-311">False</span><span class="sxs-lookup"><span data-stu-id="f0070-311">False</span></span> | <span data-ttu-id="f0070-312">Niezdefiniowana</span><span class="sxs-lookup"><span data-stu-id="f0070-312">Undefined</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="f0070-313">True</span><span class="sxs-lookup"><span data-stu-id="f0070-313">True</span></span> |<span data-ttu-id="f0070-314">True</span><span class="sxs-lookup"><span data-stu-id="f0070-314">True</span></span> |<span data-ttu-id="f0070-315">True</span><span class="sxs-lookup"><span data-stu-id="f0070-315">True</span></span> |<span data-ttu-id="f0070-316">True</span><span class="sxs-lookup"><span data-stu-id="f0070-316">True</span></span> |
| <span data-ttu-id="f0070-317">False</span><span class="sxs-lookup"><span data-stu-id="f0070-317">False</span></span> |<span data-ttu-id="f0070-318">True</span><span class="sxs-lookup"><span data-stu-id="f0070-318">True</span></span> |<span data-ttu-id="f0070-319">False</span><span class="sxs-lookup"><span data-stu-id="f0070-319">False</span></span> |<span data-ttu-id="f0070-320">Niezdefiniowana</span><span class="sxs-lookup"><span data-stu-id="f0070-320">Undefined</span></span> |
| <span data-ttu-id="f0070-321">Niezdefiniowana</span><span class="sxs-lookup"><span data-stu-id="f0070-321">Undefined</span></span> |<span data-ttu-id="f0070-322">True</span><span class="sxs-lookup"><span data-stu-id="f0070-322">True</span></span> |<span data-ttu-id="f0070-323">Niezdefiniowana</span><span class="sxs-lookup"><span data-stu-id="f0070-323">Undefined</span></span> |<span data-ttu-id="f0070-324">Niezdefiniowana</span><span class="sxs-lookup"><span data-stu-id="f0070-324">Undefined</span></span> |

| <span data-ttu-id="f0070-325">I</span><span class="sxs-lookup"><span data-stu-id="f0070-325">AND</span></span> | <span data-ttu-id="f0070-326">True</span><span class="sxs-lookup"><span data-stu-id="f0070-326">True</span></span> | <span data-ttu-id="f0070-327">False</span><span class="sxs-lookup"><span data-stu-id="f0070-327">False</span></span> | <span data-ttu-id="f0070-328">Niezdefiniowana</span><span class="sxs-lookup"><span data-stu-id="f0070-328">Undefined</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="f0070-329">True</span><span class="sxs-lookup"><span data-stu-id="f0070-329">True</span></span> |<span data-ttu-id="f0070-330">True</span><span class="sxs-lookup"><span data-stu-id="f0070-330">True</span></span> |<span data-ttu-id="f0070-331">False</span><span class="sxs-lookup"><span data-stu-id="f0070-331">False</span></span> |<span data-ttu-id="f0070-332">Niezdefiniowana</span><span class="sxs-lookup"><span data-stu-id="f0070-332">Undefined</span></span> |
| <span data-ttu-id="f0070-333">False</span><span class="sxs-lookup"><span data-stu-id="f0070-333">False</span></span> |<span data-ttu-id="f0070-334">False</span><span class="sxs-lookup"><span data-stu-id="f0070-334">False</span></span> |<span data-ttu-id="f0070-335">False</span><span class="sxs-lookup"><span data-stu-id="f0070-335">False</span></span> |<span data-ttu-id="f0070-336">False</span><span class="sxs-lookup"><span data-stu-id="f0070-336">False</span></span> |
| <span data-ttu-id="f0070-337">Niezdefiniowana</span><span class="sxs-lookup"><span data-stu-id="f0070-337">Undefined</span></span> |<span data-ttu-id="f0070-338">Niezdefiniowana</span><span class="sxs-lookup"><span data-stu-id="f0070-338">Undefined</span></span> |<span data-ttu-id="f0070-339">False</span><span class="sxs-lookup"><span data-stu-id="f0070-339">False</span></span> |<span data-ttu-id="f0070-340">Niezdefiniowana</span><span class="sxs-lookup"><span data-stu-id="f0070-340">Undefined</span></span> |

| <span data-ttu-id="f0070-341">NIE</span><span class="sxs-lookup"><span data-stu-id="f0070-341">NOT</span></span> |  |
| --- | --- |
| <span data-ttu-id="f0070-342">True</span><span class="sxs-lookup"><span data-stu-id="f0070-342">True</span></span> |<span data-ttu-id="f0070-343">False</span><span class="sxs-lookup"><span data-stu-id="f0070-343">False</span></span> |
| <span data-ttu-id="f0070-344">False</span><span class="sxs-lookup"><span data-stu-id="f0070-344">False</span></span> |<span data-ttu-id="f0070-345">True</span><span class="sxs-lookup"><span data-stu-id="f0070-345">True</span></span> |
| <span data-ttu-id="f0070-346">Niezdefiniowana</span><span class="sxs-lookup"><span data-stu-id="f0070-346">Undefined</span></span> |<span data-ttu-id="f0070-347">Niezdefiniowana</span><span class="sxs-lookup"><span data-stu-id="f0070-347">Undefined</span></span> |

### <a name="in-keyword"></a><span data-ttu-id="f0070-348">IN — słowo kluczowe</span><span class="sxs-lookup"><span data-stu-id="f0070-348">IN keyword</span></span>
<span data-ttu-id="f0070-349">Hello IN — słowo kluczowe może być używane toocheck, czy określona wartość odpowiada wartości na liście.</span><span class="sxs-lookup"><span data-stu-id="f0070-349">hello IN keyword can be used toocheck whether a specified value matches any value in a list.</span></span> <span data-ttu-id="f0070-350">Na przykład ta kwerenda zwraca wszystkie dokumenty rodziny gdzie hello id jest "WakefieldFamily" lub "AndersenFamily".</span><span class="sxs-lookup"><span data-stu-id="f0070-350">For example, this query returns all family documents where hello id is one of "WakefieldFamily" or "AndersenFamily".</span></span> 

    SELECT *
    FROM Families 
    WHERE Families.id IN ('AndersenFamily', 'WakefieldFamily')

<span data-ttu-id="f0070-351">W tym przykładzie zwraca wszystkie dokumenty, w których stan hello jest dowolne hello określone wartości.</span><span class="sxs-lookup"><span data-stu-id="f0070-351">This example returns all documents where hello state is any of hello specified values.</span></span>

    SELECT *
    FROM Families 
    WHERE Families.address.state IN ("NY", "WA", "CA", "PA", "OH", "OR", "MI", "WI", "MN", "FL")

### <a name="ternary--and-coalesce--operators"></a><span data-ttu-id="f0070-352">Operatory łączonej (?) i trójargumentowy (?)</span><span class="sxs-lookup"><span data-stu-id="f0070-352">Ternary (?) and Coalesce (??) operators</span></span>
<span data-ttu-id="f0070-353">Operatory Trzyargumentowe i Coalesce Hello mogą być używane toobuild wyrażenia warunkowe, podobne toopopular Programowanie w językach C# i JavaScript.</span><span class="sxs-lookup"><span data-stu-id="f0070-353">hello Ternary and Coalesce operators can be used toobuild conditional expressions, similar toopopular programming languages like C# and JavaScript.</span></span> 

<span data-ttu-id="f0070-354">operator trójargumentowy (?) Hello może być bardzo przydatne podczas tworzenia nowych właściwości JSON na powitania udać.</span><span class="sxs-lookup"><span data-stu-id="f0070-354">hello Ternary (?) operator can be very handy when constructing new JSON properties on hello fly.</span></span> <span data-ttu-id="f0070-355">Na przykład możesz teraz napisać poziomy klasy hello tooclassify zapytania do człowieka czytelnej postaci jak początkujących/pośredni/zaawansowane jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="f0070-355">For example, now you can write queries tooclassify hello class levels into a human readable form like Beginner/Intermediate/Advanced as shown below.</span></span>

     SELECT (c.grade < 5)? "elementary": "other" AS gradeLevel 
     FROM Families.children[0] c

<span data-ttu-id="f0070-356">Można zagnieżdżać hello wywołania toohello operator podobnie jak w zapytaniu hello poniżej.</span><span class="sxs-lookup"><span data-stu-id="f0070-356">You can also nest hello calls toohello operator like in hello query below.</span></span>

    SELECT (c.grade < 5)? "elementary": ((c.grade < 9)? "junior": "high")  AS gradeLevel 
    FROM Families.children[0] c

<span data-ttu-id="f0070-357">Jako z innymi operatorami zapytania, jeśli hello do którego istnieje odwołanie w wyrażeniu warunkowym hello Brak właściwości dokumentów lub typy hello są porównywane są różne, następnie tych dokumentów są wyłączone w wynikach zapytania hello.</span><span class="sxs-lookup"><span data-stu-id="f0070-357">As with other query operators, if hello referenced properties in hello conditional expression are missing in any document, or if hello types being compared are different, then those documents are excluded in hello query results.</span></span>

<span data-ttu-id="f0070-358">Witaj łączonej (?) operator może być używany wyboru tooefficiently hello obecność właściwości ()</span><span class="sxs-lookup"><span data-stu-id="f0070-358">hello Coalesce (??) operator can be used tooefficiently check for hello presence of a property (a.k.a.</span></span> <span data-ttu-id="f0070-359">zdefiniowano) w dokumencie.</span><span class="sxs-lookup"><span data-stu-id="f0070-359">is defined) in a document.</span></span> <span data-ttu-id="f0070-360">Jest to przydatne podczas wykonywania zapytania względem częściową strukturą lub mieszane typów danych.</span><span class="sxs-lookup"><span data-stu-id="f0070-360">This is useful when querying against semi-structured or data of mixed types.</span></span> <span data-ttu-id="f0070-361">Na przykład ta kwerenda zwraca nazwisko"hello" Jeśli nie istnieje lub hello "nazwisko" Jeśli nie jest obecny.</span><span class="sxs-lookup"><span data-stu-id="f0070-361">For example, this query returns hello "lastName" if present, or hello "surname" if it isn't present.</span></span>

    SELECT f.lastName ?? f.surname AS familyName
    FROM Families f

### <span data-ttu-id="f0070-362"><a id="EscapingReservedKeywords"></a>Metody dostępu właściwości cudzysłowie</span><span class="sxs-lookup"><span data-stu-id="f0070-362"><a id="EscapingReservedKeywords"></a>Quoted property accessor</span></span>
<span data-ttu-id="f0070-363">Można także przejść do właściwości za pomocą operatora właściwość umieszczonej w cudzysłowie hello `[]`.</span><span class="sxs-lookup"><span data-stu-id="f0070-363">You can also access properties using hello quoted property operator `[]`.</span></span> <span data-ttu-id="f0070-364">Na przykład `SELECT c.grade` i `SELECT c["grade"]` są równoważne.</span><span class="sxs-lookup"><span data-stu-id="f0070-364">For example, `SELECT c.grade` and `SELECT c["grade"]` are equivalent.</span></span> <span data-ttu-id="f0070-365">Ta składnia jest przydatne, gdy będziesz potrzebować tooescape właściwości, która zawiera spacje i znaki specjalne lub sytuacji hello tooshare takie same nazwy słowa kluczowego SQL lub zastrzeżony wyraz.</span><span class="sxs-lookup"><span data-stu-id="f0070-365">This syntax is useful when you need tooescape a property that contains spaces, special characters, or happens tooshare hello same name as a SQL keyword or reserved word.</span></span>

    SELECT f["lastName"]
    FROM Families f
    WHERE f["id"] = "AndersenFamily"


## <span data-ttu-id="f0070-366"><a id="SelectClause"></a>Klauzula SELECT</span><span class="sxs-lookup"><span data-stu-id="f0070-366"><a id="SelectClause"></a>SELECT clause</span></span>
<span data-ttu-id="f0070-367">Klauzula SELECT Hello (**`SELECT <select_list>`**) jest obowiązkowy i określa, jakie są one pobierane hello zapytania, tak jak w języku SQL ANSI.</span><span class="sxs-lookup"><span data-stu-id="f0070-367">hello SELECT clause (**`SELECT <select_list>`**) is mandatory and specifies what values are retrieved from hello query, just like in ANSI-SQL.</span></span> <span data-ttu-id="f0070-368">podzbioru Hello, który jest zostały przefiltrowane na podstawie dokumentów źródłowych hello są przekazywane na etapie projekcji hello określoną hello są pobierane wartości JSON i jest tworzony nowy obiekt JSON, dla każdego dane wejściowe przekazane do go.</span><span class="sxs-lookup"><span data-stu-id="f0070-368">hello subset that's been filtered on top of hello source documents are passed onto hello projection phase, where hello specified JSON values are retrieved and a new JSON object is constructed, for each input passed onto it.</span></span> 

<span data-ttu-id="f0070-369">Witaj poniższy przykład pokazuje typowe zapytania SELECT.</span><span class="sxs-lookup"><span data-stu-id="f0070-369">hello following example shows a typical SELECT query.</span></span> 

<span data-ttu-id="f0070-370">**Zapytanie**</span><span class="sxs-lookup"><span data-stu-id="f0070-370">**Query**</span></span>

    SELECT f.address
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="f0070-371">**Wyniki**</span><span class="sxs-lookup"><span data-stu-id="f0070-371">**Results**</span></span>

    [{
      "address": {
        "state": "WA", 
        "county": "King", 
        "city": "seattle"
      }
    }]


### <a name="nested-properties"></a><span data-ttu-id="f0070-372">Właściwości zagnieżdżonych</span><span class="sxs-lookup"><span data-stu-id="f0070-372">Nested properties</span></span>
<span data-ttu-id="f0070-373">W hello poniższy przykład, możemy projekcji dwie właściwości zagnieżdżonych `f.address.state` i `f.address.city`.</span><span class="sxs-lookup"><span data-stu-id="f0070-373">In hello following example, we are projecting two nested properties `f.address.state` and `f.address.city`.</span></span>

<span data-ttu-id="f0070-374">**Zapytanie**</span><span class="sxs-lookup"><span data-stu-id="f0070-374">**Query**</span></span>

    SELECT f.address.state, f.address.city
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="f0070-375">**Wyniki**</span><span class="sxs-lookup"><span data-stu-id="f0070-375">**Results**</span></span>

    [{
      "state": "WA", 
      "city": "seattle"
    }]


<span data-ttu-id="f0070-376">Projekcji obsługuje również wyrażenia JSON, jak pokazano w hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="f0070-376">Projection also supports JSON expressions as shown in hello following example:</span></span>

<span data-ttu-id="f0070-377">**Zapytanie**</span><span class="sxs-lookup"><span data-stu-id="f0070-377">**Query**</span></span>

    SELECT { "state": f.address.state, "city": f.address.city, "name": f.id }
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="f0070-378">**Wyniki**</span><span class="sxs-lookup"><span data-stu-id="f0070-378">**Results**</span></span>

    [{
      "$1": {
        "state": "WA", 
        "city": "seattle", 
        "name": "AndersenFamily"
      }
    }]


<span data-ttu-id="f0070-379">Przyjrzyjmy się rola hello `$1` tutaj.</span><span class="sxs-lookup"><span data-stu-id="f0070-379">Let's look at hello role of `$1` here.</span></span> <span data-ttu-id="f0070-380">Witaj `SELECT` klauzuli wymaga toocreate obiekt JSON, a ponieważ podany żaden klucz, używamy nazwy zmiennych argumentów niejawnego począwszy `$1`.</span><span class="sxs-lookup"><span data-stu-id="f0070-380">hello `SELECT` clause needs toocreate a JSON object and since no key is provided, we use implicit argument variable names starting with `$1`.</span></span> <span data-ttu-id="f0070-381">Na przykład ta kwerenda zwraca dwóch zmiennych argumentów niejawnego etykietą `$1` i `$2`.</span><span class="sxs-lookup"><span data-stu-id="f0070-381">For example, this query returns two implicit argument variables, labeled `$1` and `$2`.</span></span>

<span data-ttu-id="f0070-382">**Zapytanie**</span><span class="sxs-lookup"><span data-stu-id="f0070-382">**Query**</span></span>

    SELECT { "state": f.address.state, "city": f.address.city }, 
           { "name": f.id }
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="f0070-383">**Wyniki**</span><span class="sxs-lookup"><span data-stu-id="f0070-383">**Results**</span></span>

    [{
      "$1": {
        "state": "WA", 
        "city": "seattle"
      }, 
      "$2": {
        "name": "AndersenFamily"
      }
    }]


### <a name="aliasing"></a><span data-ttu-id="f0070-384">Aliasów</span><span class="sxs-lookup"><span data-stu-id="f0070-384">Aliasing</span></span>
<span data-ttu-id="f0070-385">Teraz załóżmy rozszerzenia przykładu hello powyżej z jawnym aliasów wartości.</span><span class="sxs-lookup"><span data-stu-id="f0070-385">Now let's extend hello example above with explicit aliasing of values.</span></span> <span data-ttu-id="f0070-386">Jest to — słowo kluczowe hello używany dla aliasów.</span><span class="sxs-lookup"><span data-stu-id="f0070-386">AS is hello keyword used for aliasing.</span></span> <span data-ttu-id="f0070-387">Jest opcjonalne, jak pokazano podczas projekcji hello drugiej wartości jako `NameInfo`.</span><span class="sxs-lookup"><span data-stu-id="f0070-387">It's optional as shown while projecting hello second value as `NameInfo`.</span></span> 

<span data-ttu-id="f0070-388">W przypadku, gdy zapytanie zawiera dwie właściwości o hello tej samej nazwie, aliasów musi być używane toorename jedno lub oba hello właściwości, dzięki czemu są one rozróżniane w hello przewidywane wynik.</span><span class="sxs-lookup"><span data-stu-id="f0070-388">In case a query has two properties with hello same name, aliasing must be used toorename one or both of hello properties so that they are disambiguated in hello projected result.</span></span>

<span data-ttu-id="f0070-389">**Zapytanie**</span><span class="sxs-lookup"><span data-stu-id="f0070-389">**Query**</span></span>

    SELECT 
           { "state": f.address.state, "city": f.address.city } AS AddressInfo, 
           { "name": f.id } NameInfo
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="f0070-390">**Wyniki**</span><span class="sxs-lookup"><span data-stu-id="f0070-390">**Results**</span></span>

    [{
      "AddressInfo": {
        "state": "WA", 
        "city": "seattle"
      }, 
      "NameInfo": {
        "name": "AndersenFamily"
      }
    }]


### <a name="scalar-expressions"></a><span data-ttu-id="f0070-391">Wyrażenia skalarne</span><span class="sxs-lookup"><span data-stu-id="f0070-391">Scalar expressions</span></span>
<span data-ttu-id="f0070-392">Ponadto tooproperty odwołuje się do, hello klauzuli SELECT obsługuje również wyrażenia skalarne stałe, wyrażenia arytmetyczne, wyrażenie logiczne itd. Na przykład w tym miejscu jest prostego zapytania "Hello World".</span><span class="sxs-lookup"><span data-stu-id="f0070-392">In addition tooproperty references, hello SELECT clause also supports scalar expressions like constants, arithmetic expressions, logical expressions, etc. For example, here's a simple "Hello World" query.</span></span>

<span data-ttu-id="f0070-393">**Zapytanie**</span><span class="sxs-lookup"><span data-stu-id="f0070-393">**Query**</span></span>

    SELECT "Hello World"

<span data-ttu-id="f0070-394">**Wyniki**</span><span class="sxs-lookup"><span data-stu-id="f0070-394">**Results**</span></span>

    [{
      "$1": "Hello World"
    }]


<span data-ttu-id="f0070-395">Oto przykład bardziej złożone wyrażenie skalarne.</span><span class="sxs-lookup"><span data-stu-id="f0070-395">Here's a more complex example that uses a scalar expression.</span></span>

<span data-ttu-id="f0070-396">**Zapytanie**</span><span class="sxs-lookup"><span data-stu-id="f0070-396">**Query**</span></span>

    SELECT ((2 + 11 % 7)-2)/3    

<span data-ttu-id="f0070-397">**Wyniki**</span><span class="sxs-lookup"><span data-stu-id="f0070-397">**Results**</span></span>

    [{
      "$1": 1.33333
    }]


<span data-ttu-id="f0070-398">W hello poniższy przykład hello wynik wyrażenia skalarne hello jest wartością logiczną.</span><span class="sxs-lookup"><span data-stu-id="f0070-398">In hello following example, hello result of hello scalar expression is a Boolean.</span></span>

<span data-ttu-id="f0070-399">**Zapytanie**</span><span class="sxs-lookup"><span data-stu-id="f0070-399">**Query**</span></span>

    SELECT f.address.city = f.address.state AS AreFromSameCityState
    FROM Families f    

<span data-ttu-id="f0070-400">**Wyniki**</span><span class="sxs-lookup"><span data-stu-id="f0070-400">**Results**</span></span>

    [
      {
        "AreFromSameCityState": false
      }, 
      {
        "AreFromSameCityState": true
      }
    ]


### <a name="object-and-array-creation"></a><span data-ttu-id="f0070-401">Tworzenie obiektu i tablicy</span><span class="sxs-lookup"><span data-stu-id="f0070-401">Object and array creation</span></span>
<span data-ttu-id="f0070-402">Inna funkcja klucza SQL interfejsu API usługi DocumentDB jest tworzenie tablicy i obiektów.</span><span class="sxs-lookup"><span data-stu-id="f0070-402">Another key feature of DocumentDB API SQL is array/object creation.</span></span> <span data-ttu-id="f0070-403">W poprzednim przykładzie hello należy pamiętać, że utworzono nowy obiekt JSON.</span><span class="sxs-lookup"><span data-stu-id="f0070-403">In hello previous example, note that we created a new JSON object.</span></span> <span data-ttu-id="f0070-404">Podobnie co także utworzyć tablic pokazane na powitania następujące przykłady:</span><span class="sxs-lookup"><span data-stu-id="f0070-404">Similarly, one can also construct arrays as shown in hello following examples:</span></span>

<span data-ttu-id="f0070-405">**Zapytanie**</span><span class="sxs-lookup"><span data-stu-id="f0070-405">**Query**</span></span>

    SELECT [f.address.city, f.address.state] AS CityState 
    FROM Families f    

<span data-ttu-id="f0070-406">**Wyniki**</span><span class="sxs-lookup"><span data-stu-id="f0070-406">**Results**</span></span>  

    [
      {
        "CityState": [
          "seattle", 
          "WA"
        ]
      }, 
      {
        "CityState": [
          "NY", 
          "NY"
        ]
      }
    ]

### <span data-ttu-id="f0070-407"><a id="ValueKeyword"></a>VALUE — słowo kluczowe</span><span class="sxs-lookup"><span data-stu-id="f0070-407"><a id="ValueKeyword"></a>VALUE keyword</span></span>
<span data-ttu-id="f0070-408">Witaj **wartość** — słowo kluczowe dostarcza wartość sposób tooreturn JSON.</span><span class="sxs-lookup"><span data-stu-id="f0070-408">hello **VALUE** keyword provides a way tooreturn JSON value.</span></span> <span data-ttu-id="f0070-409">Na przykład kwerendy hello pokazano poniżej hello zwraca skalarne `"Hello World"` zamiast `{$1: "Hello World"}`.</span><span class="sxs-lookup"><span data-stu-id="f0070-409">For example, hello query shown below returns hello scalar `"Hello World"` instead of `{$1: "Hello World"}`.</span></span>

<span data-ttu-id="f0070-410">**Zapytanie**</span><span class="sxs-lookup"><span data-stu-id="f0070-410">**Query**</span></span>

    SELECT VALUE "Hello World"

<span data-ttu-id="f0070-411">**Wyniki**</span><span class="sxs-lookup"><span data-stu-id="f0070-411">**Results**</span></span>

    [
      "Hello World"
    ]


<span data-ttu-id="f0070-412">Witaj następujące zapytanie zwraca wartość JSON hello bez hello `"address"` etykiety w wynikach hello.</span><span class="sxs-lookup"><span data-stu-id="f0070-412">hello following query returns hello JSON value without hello `"address"` label in hello results.</span></span>

<span data-ttu-id="f0070-413">**Zapytanie**</span><span class="sxs-lookup"><span data-stu-id="f0070-413">**Query**</span></span>

    SELECT VALUE f.address
    FROM Families f    

<span data-ttu-id="f0070-414">**Wyniki**</span><span class="sxs-lookup"><span data-stu-id="f0070-414">**Results**</span></span>  

    [
      {
        "state": "WA", 
        "county": "King", 
        "city": "seattle"
      }, 
      {
        "state": "NY", 
        "county": "Manhattan", 
        "city": "NY"
      }
    ]

<span data-ttu-id="f0070-415">Witaj poniższy przykład rozszerza to tooshow jak tooreturn JSON pierwotne wartości (hello poziomu liścia hello drzewa JSON).</span><span class="sxs-lookup"><span data-stu-id="f0070-415">hello following example extends this tooshow how tooreturn JSON primitive values (hello leaf level of hello JSON tree).</span></span> 

<span data-ttu-id="f0070-416">**Zapytanie**</span><span class="sxs-lookup"><span data-stu-id="f0070-416">**Query**</span></span>

    SELECT VALUE f.address.state
    FROM Families f    

<span data-ttu-id="f0070-417">**Wyniki**</span><span class="sxs-lookup"><span data-stu-id="f0070-417">**Results**</span></span>

    [
      "WA",
      "NY"
    ]


### <a name="-operator"></a><span data-ttu-id="f0070-418">* — Operator</span><span class="sxs-lookup"><span data-stu-id="f0070-418">* Operator</span></span>
<span data-ttu-id="f0070-419">Hello specjalne — operator (*) jest obsługiwane tooproject hello dokumentu — jest.</span><span class="sxs-lookup"><span data-stu-id="f0070-419">hello special operator (*) is supported tooproject hello document as-is.</span></span> <span data-ttu-id="f0070-420">Gdy jest używany, musi to być hello przewidywane tylko pola.</span><span class="sxs-lookup"><span data-stu-id="f0070-420">When used, it must be hello only projected field.</span></span> <span data-ttu-id="f0070-421">Podczas zapytania, takie jak `SELECT * FROM Families f` jest prawidłowy, `SELECT VALUE * FROM Families f ` i `SELECT *, f.id FROM Families f ` nie są prawidłowe.</span><span class="sxs-lookup"><span data-stu-id="f0070-421">While a query like `SELECT * FROM Families f` is valid, `SELECT VALUE * FROM Families f ` and  `SELECT *, f.id FROM Families f ` are not valid.</span></span>

<span data-ttu-id="f0070-422">**Zapytanie**</span><span class="sxs-lookup"><span data-stu-id="f0070-422">**Query**</span></span>

    SELECT * 
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="f0070-423">**Wyniki**</span><span class="sxs-lookup"><span data-stu-id="f0070-423">**Results**</span></span>

    [{
        "id": "AndersenFamily",
        "lastName": "Andersen",
        "parents": [
           { "firstName": "Thomas" },
           { "firstName": "Mary Kay"}
        ],
        "children": [
           {
               "firstName": "Henriette Thaulow", "gender": "female", "grade": 5,
               "pets": [{ "givenName": "Fluffy" }]
           }
        ],
        "address": { "state": "WA", "county": "King", "city": "seattle" },
        "creationDate": 1431620472,
        "isRegistered": true
    }]

### <span data-ttu-id="f0070-424"><a id="TopKeyword"></a>TOP Operator</span><span class="sxs-lookup"><span data-stu-id="f0070-424"><a id="TopKeyword"></a>TOP Operator</span></span>
<span data-ttu-id="f0070-425">mogą być słowo kluczowe TOP Hello używane toolimit hello liczba wartości z zapytania.</span><span class="sxs-lookup"><span data-stu-id="f0070-425">hello TOP keyword can be used toolimit hello number of values from a query.</span></span> <span data-ttu-id="f0070-426">Po PIERWSZYCH jest używany w połączeniu z hello klauzuli ORDER BY, zestaw wyników hello jest ograniczona toohello pierwsza liczba N uporządkowanej wartości. w przeciwnym razie zwraca hello pierwsze N liczba wyników w kolejności niezdefiniowany.</span><span class="sxs-lookup"><span data-stu-id="f0070-426">When TOP is used in conjunction with hello ORDER BY clause, hello result set is limited toohello first N number of ordered values; otherwise, it returns hello first N number of results in an undefined order.</span></span> <span data-ttu-id="f0070-427">Najlepszym rozwiązaniem w instrukcji SELECT, zawsze za pomocą klauzuli ORDER BY hello klauzuli TOP.</span><span class="sxs-lookup"><span data-stu-id="f0070-427">As a best practice, in a SELECT statement, always use an ORDER BY clause with hello TOP clause.</span></span> <span data-ttu-id="f0070-428">To jest jedynym sposobem hello toopredictably wskazują wiersze, które wpływają na GÓRZE.</span><span class="sxs-lookup"><span data-stu-id="f0070-428">This is hello only way toopredictably indicate which rows are affected by TOP.</span></span> 

<span data-ttu-id="f0070-429">**Zapytanie**</span><span class="sxs-lookup"><span data-stu-id="f0070-429">**Query**</span></span>

    SELECT TOP 1 * 
    FROM Families f 

<span data-ttu-id="f0070-430">**Wyniki**</span><span class="sxs-lookup"><span data-stu-id="f0070-430">**Results**</span></span>

    [{
        "id": "AndersenFamily",
        "lastName": "Andersen",
        "parents": [
           { "firstName": "Thomas" },
           { "firstName": "Mary Kay"}
        ],
        "children": [
           {
               "firstName": "Henriette Thaulow", "gender": "female", "grade": 5,
               "pets": [{ "givenName": "Fluffy" }]
           }
        ],
        "address": { "state": "WA", "county": "King", "city": "seattle" },
        "creationDate": 1431620472,
        "isRegistered": true
    }]

<span data-ttu-id="f0070-431">Z wartością stałą (jak pokazano powyżej) lub wartość zmiennej użycie zapytań sparametryzowanych można TOP.</span><span class="sxs-lookup"><span data-stu-id="f0070-431">TOP can be used with a constant value (as shown above) or with a variable value using parameterized queries.</span></span> <span data-ttu-id="f0070-432">Aby uzyskać więcej informacji zapoznaj się z zapytań sparametryzowanych poniżej.</span><span class="sxs-lookup"><span data-stu-id="f0070-432">For more details, please see parameterized queries below.</span></span>

### <span data-ttu-id="f0070-433"><a id="Aggregates"></a>Funkcje agregujące</span><span class="sxs-lookup"><span data-stu-id="f0070-433"><a id="Aggregates"></a>Aggregate Functions</span></span>
<span data-ttu-id="f0070-434">Można również wykonywać agregacji w hello `SELECT` klauzuli.</span><span class="sxs-lookup"><span data-stu-id="f0070-434">You can also perform aggregations in hello `SELECT` clause.</span></span> <span data-ttu-id="f0070-435">Funkcje agregujące wykonywanie obliczeń na zestaw wartości i zwraca pojedynczą wartość.</span><span class="sxs-lookup"><span data-stu-id="f0070-435">Aggregate functions perform a calculation on a set of values and return a single value.</span></span> <span data-ttu-id="f0070-436">Na przykład hello następujące zapytanie zwraca liczbę hello rodziny dokumentów w kolekcji hello.</span><span class="sxs-lookup"><span data-stu-id="f0070-436">For example, hello following query returns hello count of family documents within hello collection.</span></span>

<span data-ttu-id="f0070-437">**Zapytanie**</span><span class="sxs-lookup"><span data-stu-id="f0070-437">**Query**</span></span>

    SELECT COUNT(1) 
    FROM Families f 

<span data-ttu-id="f0070-438">**Wyniki**</span><span class="sxs-lookup"><span data-stu-id="f0070-438">**Results**</span></span>

    [{
        "$1": 2
    }]

<span data-ttu-id="f0070-439">Można także wrócić hello wartość skalarną hello agregacji przy użyciu hello `VALUE` — słowo kluczowe.</span><span class="sxs-lookup"><span data-stu-id="f0070-439">You can also return hello scalar value of hello aggregate by using hello `VALUE` keyword.</span></span> <span data-ttu-id="f0070-440">Na przykład hello następujące zapytanie zwraca hello liczbę wartości jako jeden numer:</span><span class="sxs-lookup"><span data-stu-id="f0070-440">For example, hello following query returns hello count of values as a single number:</span></span>

<span data-ttu-id="f0070-441">**Zapytanie**</span><span class="sxs-lookup"><span data-stu-id="f0070-441">**Query**</span></span>

    SELECT VALUE COUNT(1) 
    FROM Families f 

<span data-ttu-id="f0070-442">**Wyniki**</span><span class="sxs-lookup"><span data-stu-id="f0070-442">**Results**</span></span>

    [ 2 ]

<span data-ttu-id="f0070-443">Można również wykonywać wartości zagregowanych w połączeniu z filtrami.</span><span class="sxs-lookup"><span data-stu-id="f0070-443">You can also perform aggregates in combination with filters.</span></span> <span data-ttu-id="f0070-444">Na przykład hello następujące zapytanie zwraca hello liczba dokumentów z adresem hello w stanie Waszyngton hello.</span><span class="sxs-lookup"><span data-stu-id="f0070-444">For example, hello following query returns hello count of documents with hello address in hello state of Washington.</span></span>

<span data-ttu-id="f0070-445">**Zapytanie**</span><span class="sxs-lookup"><span data-stu-id="f0070-445">**Query**</span></span>

    SELECT VALUE COUNT(1) 
    FROM Families f
    WHERE f.address.state = "WA" 

<span data-ttu-id="f0070-446">**Wyniki**</span><span class="sxs-lookup"><span data-stu-id="f0070-446">**Results**</span></span>

    [ 1 ]

<span data-ttu-id="f0070-447">Hello poniższej tabeli przedstawiono listę obsługiwanych funkcji agregujących hello w interfejsie API usługi DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="f0070-447">hello following table shows hello list of supported aggregate functions in DocumentDB API.</span></span> <span data-ttu-id="f0070-448">`SUM`i `AVG` są wykonywane za pośrednictwem wartości liczbowe, podczas gdy `COUNT`, `MIN`, i `MAX` mogą być wykonywane za pośrednictwem liczb i ciągów, wartości logiczne oraz wartości null.</span><span class="sxs-lookup"><span data-stu-id="f0070-448">`SUM` and `AVG` are performed over numeric values, whereas `COUNT`, `MIN`, and `MAX` can be performed over numbers, strings, Booleans, and nulls.</span></span> 

| <span data-ttu-id="f0070-449">Sposób użycia</span><span class="sxs-lookup"><span data-stu-id="f0070-449">Usage</span></span> | <span data-ttu-id="f0070-450">Opis</span><span class="sxs-lookup"><span data-stu-id="f0070-450">Description</span></span> |
|-------|-------------|
| <span data-ttu-id="f0070-451">LICZBA</span><span class="sxs-lookup"><span data-stu-id="f0070-451">COUNT</span></span> | <span data-ttu-id="f0070-452">Zwraca hello liczba elementów w wyrażeniu hello.</span><span class="sxs-lookup"><span data-stu-id="f0070-452">Returns hello number of items in hello expression.</span></span> |
| <span data-ttu-id="f0070-453">SUMA</span><span class="sxs-lookup"><span data-stu-id="f0070-453">SUM</span></span>   | <span data-ttu-id="f0070-454">Zwraca hello sumę wszystkich wartości hello w wyrażeniu hello.</span><span class="sxs-lookup"><span data-stu-id="f0070-454">Returns hello sum of all hello values in hello expression.</span></span> |
| <span data-ttu-id="f0070-455">MIN</span><span class="sxs-lookup"><span data-stu-id="f0070-455">MIN</span></span>   | <span data-ttu-id="f0070-456">Zwraca hello minimalną wartość w wyrażeniu hello.</span><span class="sxs-lookup"><span data-stu-id="f0070-456">Returns hello minimum value in hello expression.</span></span> |
| <span data-ttu-id="f0070-457">MAKSYMALNA LICZBA</span><span class="sxs-lookup"><span data-stu-id="f0070-457">MAX</span></span>   | <span data-ttu-id="f0070-458">Zwraca hello maksymalną wartość w wyrażeniu hello.</span><span class="sxs-lookup"><span data-stu-id="f0070-458">Returns hello maximum value in hello expression.</span></span> |
| <span data-ttu-id="f0070-459">ŚR.</span><span class="sxs-lookup"><span data-stu-id="f0070-459">AVG</span></span>   | <span data-ttu-id="f0070-460">Zwraca hello średnią z wartości hello w wyrażeniu hello.</span><span class="sxs-lookup"><span data-stu-id="f0070-460">Returns hello average of hello values in hello expression.</span></span> |

<span data-ttu-id="f0070-461">Agreguje można również przeprowadzić przez hello wyniki iteracji tablicy.</span><span class="sxs-lookup"><span data-stu-id="f0070-461">Aggregates can also be performed over hello results of an array iteration.</span></span> <span data-ttu-id="f0070-462">Aby uzyskać więcej informacji, zobacz [iteracji tablicy w zapytaniach](#Iteration).</span><span class="sxs-lookup"><span data-stu-id="f0070-462">For more information, see [Array Iteration in Queries](#Iteration).</span></span>

> [!NOTE]
> <span data-ttu-id="f0070-463">Przy użyciu hello Eksploratora zapytań w portalu Azure, należy pamiętać, że Agregacja kwerendy mogą zwracać hello wyników zagregowany częściowo za pośrednictwem strony zapytania.</span><span class="sxs-lookup"><span data-stu-id="f0070-463">When using hello Azure portal's Query Explorer, note that aggregation queries may return hello partially aggregated results over a query page.</span></span> <span data-ttu-id="f0070-464">Witaj zestawów SDK tworzy pojedynczej wartości zbiorczej na wszystkich stronach.</span><span class="sxs-lookup"><span data-stu-id="f0070-464">hello SDKs produces a single cumulative value across all pages.</span></span> 
> 
> <span data-ttu-id="f0070-465">W porządku kwerendy agregacji tooperform przy użyciu kodu, należy zestawu .NET SDK 1.12.0, zestawu SDK programu .NET Core 1.1.0 lub zestawu Java SDK 1.9.5 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="f0070-465">In order tooperform aggregation queries using code, you need .NET SDK 1.12.0, .NET Core SDK 1.1.0, or Java SDK 1.9.5 or above.</span></span>    
>

## <span data-ttu-id="f0070-466"><a id="OrderByClause"></a>Klauzula ORDER BY</span><span class="sxs-lookup"><span data-stu-id="f0070-466"><a id="OrderByClause"></a>ORDER BY clause</span></span>
<span data-ttu-id="f0070-467">Podobnie jak w ANSI SQL, można dołączyć opcjonalny klauzuli Order By podczas wykonywania zapytania.</span><span class="sxs-lookup"><span data-stu-id="f0070-467">Like in ANSI-SQL, you can include an optional Order By clause while querying.</span></span> <span data-ttu-id="f0070-468">Klauzula Hello mogą zawierać opcjonalny ASC/DESC toospecify hello Kolejność argumentów w którym można pobrać wyników.</span><span class="sxs-lookup"><span data-stu-id="f0070-468">hello clause can include an optional ASC/DESC argument toospecify hello order in which results must be retrieved.</span></span>

<span data-ttu-id="f0070-469">Na przykład w tym miejscu jest kwerendę, która pobiera rodzin w kolejności nazwę miejscowości rezydentna hello.</span><span class="sxs-lookup"><span data-stu-id="f0070-469">For example, here's a query that retrieves families in order of hello resident city's name.</span></span>

<span data-ttu-id="f0070-470">**Zapytanie**</span><span class="sxs-lookup"><span data-stu-id="f0070-470">**Query**</span></span>

    SELECT f.id, f.address.city
    FROM Families f 
    ORDER BY f.address.city

<span data-ttu-id="f0070-471">**Wyniki**</span><span class="sxs-lookup"><span data-stu-id="f0070-471">**Results**</span></span>

    [
      {
        "id": "WakefieldFamily",
        "city": "NY"
      },
      {
        "id": "AndersenFamily",
        "city": "Seattle"    
      }
    ]

<span data-ttu-id="f0070-472">A Oto kwerendę, która pobiera rodzin w kolejności Data utworzenia, który jest przechowywany jako liczbę reprezentującą hello czas epoki, tj, czas, który upłynął od 1 stycznia 1970 w sekundach.</span><span class="sxs-lookup"><span data-stu-id="f0070-472">And here's a query that retrieves families in order of creation date, which is stored as a number representing hello epoch time, i.e, elapsed time since Jan 1, 1970 in seconds.</span></span>

<span data-ttu-id="f0070-473">**Zapytanie**</span><span class="sxs-lookup"><span data-stu-id="f0070-473">**Query**</span></span>

    SELECT f.id, f.creationDate
    FROM Families f 
    ORDER BY f.creationDate DESC

<span data-ttu-id="f0070-474">**Wyniki**</span><span class="sxs-lookup"><span data-stu-id="f0070-474">**Results**</span></span>

    [
      {
        "id": "WakefieldFamily",
        "creationDate": 1431620462
      },
      {
        "id": "AndersenFamily",
        "creationDate": 1431620472    
      }
    ]

## <span data-ttu-id="f0070-475"><a id="Advanced"></a>Pojęcia zaawansowane bazy danych i zapytania SQL</span><span class="sxs-lookup"><span data-stu-id="f0070-475"><a id="Advanced"></a>Advanced database concepts and SQL queries</span></span>

### <span data-ttu-id="f0070-476"><a id="Iteration"></a>Iteracji</span><span class="sxs-lookup"><span data-stu-id="f0070-476"><a id="Iteration"></a>Iteration</span></span>
<span data-ttu-id="f0070-477">Dodano nową konstrukcję za pośrednictwem hello **IN** — słowo kluczowe w obsłudze tooprovide DocumentDB interfejsu API SQL dla Iterowanie przez tablice notacji JSON.</span><span class="sxs-lookup"><span data-stu-id="f0070-477">A new construct was added via hello **IN** keyword in DocumentDB API SQL tooprovide support for iterating over JSON arrays.</span></span> <span data-ttu-id="f0070-478">Źródło FROM Hello zapewnia obsługę iteracji.</span><span class="sxs-lookup"><span data-stu-id="f0070-478">hello FROM source provides support for iteration.</span></span> <span data-ttu-id="f0070-479">Zacznijmy od hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="f0070-479">Let's start with hello following example:</span></span>

<span data-ttu-id="f0070-480">**Zapytanie**</span><span class="sxs-lookup"><span data-stu-id="f0070-480">**Query**</span></span>

    SELECT * 
    FROM Families.children

<span data-ttu-id="f0070-481">**Wyniki**</span><span class="sxs-lookup"><span data-stu-id="f0070-481">**Results**</span></span>  

    [
      [
        {
          "firstName": "Henriette Thaulow", 
          "gender": "female", 
          "grade": 5, 
          "pets": [{ "givenName": "Fluffy"}]
        }
      ], 
      [
        {
            "familyName": "Merriam", 
            "givenName": "Jesse", 
            "gender": "female", 
            "grade": 1
        }, 
        {
            "familyName": "Miller", 
            "givenName": "Lisa", 
            "gender": "female", 
            "grade": 8
        }
      ]
    ]

<span data-ttu-id="f0070-482">Teraz Przyjrzyjmy się inne zapytanie, który wykonuje iterację na elementy podrzędne w kolekcji hello.</span><span class="sxs-lookup"><span data-stu-id="f0070-482">Now let's look at another query that performs iteration over children in hello collection.</span></span> <span data-ttu-id="f0070-483">Należy zwrócić uwagę hello różnica w tablicy wyjściowej hello.</span><span class="sxs-lookup"><span data-stu-id="f0070-483">Note hello difference in hello output array.</span></span> <span data-ttu-id="f0070-484">W tym przykładzie dzieli `children` i spłaszcza hello wyniki do jednej macierzy.</span><span class="sxs-lookup"><span data-stu-id="f0070-484">This example splits `children` and flattens hello results into a single array.</span></span>  

<span data-ttu-id="f0070-485">**Zapytanie**</span><span class="sxs-lookup"><span data-stu-id="f0070-485">**Query**</span></span>

    SELECT * 
    FROM c IN Families.children

<span data-ttu-id="f0070-486">**Wyniki**</span><span class="sxs-lookup"><span data-stu-id="f0070-486">**Results**</span></span>  

    [
      {
          "firstName": "Henriette Thaulow",
          "gender": "female",
          "grade": 5,
          "pets": [{ "givenName": "Fluffy" }]
      },
      {
          "familyName": "Merriam",
          "givenName": "Jesse",
          "gender": "female",
          "grade": 1
      },
      {
          "familyName": "Miller",
          "givenName": "Lisa",
          "gender": "female",
          "grade": 8
      }
    ]

<span data-ttu-id="f0070-487">Może to być dodatkowo toofilter używanych na każdy wpis poszczególnych tablicy hello, jak pokazano w hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="f0070-487">This can be further used toofilter on each individual entry of hello array as shown in hello following example:</span></span>

<span data-ttu-id="f0070-488">**Zapytanie**</span><span class="sxs-lookup"><span data-stu-id="f0070-488">**Query**</span></span>

    SELECT c.givenName
    FROM c IN Families.children
    WHERE c.grade = 8

<span data-ttu-id="f0070-489">**Wyniki**</span><span class="sxs-lookup"><span data-stu-id="f0070-489">**Results**</span></span>  

    [{
      "givenName": "Lisa"
    }]

<span data-ttu-id="f0070-490">Można również wykonywać agregacji w wyniku hello iteracji tablicy.</span><span class="sxs-lookup"><span data-stu-id="f0070-490">You can also perform aggregation over hello result of array iteration.</span></span> <span data-ttu-id="f0070-491">Na przykład hello następujące zapytanie zlicza hello elementów podrzędnych wśród wszystkich rodzin.</span><span class="sxs-lookup"><span data-stu-id="f0070-491">For example, hello following query counts hello number of children among all families.</span></span>

<span data-ttu-id="f0070-492">**Zapytanie**</span><span class="sxs-lookup"><span data-stu-id="f0070-492">**Query**</span></span>

    SELECT COUNT(child) 
    FROM child IN Families.children

<span data-ttu-id="f0070-493">**Wyniki**</span><span class="sxs-lookup"><span data-stu-id="f0070-493">**Results**</span></span>  

    [
      { 
        "$1": 3
      }
    ]

### <span data-ttu-id="f0070-494"><a id="Joins"></a>Tworzy sprzężenie</span><span class="sxs-lookup"><span data-stu-id="f0070-494"><a id="Joins"></a>Joins</span></span>
<span data-ttu-id="f0070-495">W relacyjnej bazie danych ważne jest toojoin potrzeby hello między tabelami.</span><span class="sxs-lookup"><span data-stu-id="f0070-495">In a relational database, hello need toojoin across tables is important.</span></span> <span data-ttu-id="f0070-496">Jego hello logicznej toodesigning następstwem z znormalizowanych schematów.</span><span class="sxs-lookup"><span data-stu-id="f0070-496">It's hello logical corollary toodesigning normalized schemas.</span></span> <span data-ttu-id="f0070-497">Toothis inaczej, interfejsu API usługi DocumentDB podchodzi do modelu danych nieznormalizowany hello dokumentów bez schematu.</span><span class="sxs-lookup"><span data-stu-id="f0070-497">Contrary toothis, DocumentDB API deals with hello denormalized data model of schema-free documents.</span></span> <span data-ttu-id="f0070-498">Jest to odpowiednik logiczny hello a "samosprzężenie".</span><span class="sxs-lookup"><span data-stu-id="f0070-498">This is hello logical equivalent of a "self-join".</span></span>

<span data-ttu-id="f0070-499">Składnia Hello, obsługujący język hello jest sprzężenia sprzężenia < from_source2 > < from_source1 >... Przyłącz < from_sourceN >.</span><span class="sxs-lookup"><span data-stu-id="f0070-499">hello syntax that hello language supports is <from_source1> JOIN <from_source2> JOIN ... JOIN <from_sourceN>.</span></span> <span data-ttu-id="f0070-500">Ogólne, to zwraca zbiór **N**- krotek (krotki o **N** wartości).</span><span class="sxs-lookup"><span data-stu-id="f0070-500">Overall, this returns a set of **N**-tuples (tuple with **N** values).</span></span> <span data-ttu-id="f0070-501">Każda krotka zawiera wartości utworzonego przez Iterowanie wszystkie aliasy kolekcji po ich odpowiednich zestawów.</span><span class="sxs-lookup"><span data-stu-id="f0070-501">Each tuple has values produced by iterating all collection aliases over their respective sets.</span></span> <span data-ttu-id="f0070-502">Innymi słowy jest to pełny iloczyn wektorowy zestawów hello uczestniczących hello sprzężenia.</span><span class="sxs-lookup"><span data-stu-id="f0070-502">In other words, this is a full cross product of hello sets participating in hello join.</span></span>

<span data-ttu-id="f0070-503">Witaj poniższych przykładach pokazano, jak działa hello klauzuli JOIN.</span><span class="sxs-lookup"><span data-stu-id="f0070-503">hello following examples show how hello JOIN clause works.</span></span> <span data-ttu-id="f0070-504">Poniższy przykład hello, hello wynikiem jest pusty ponieważ hello iloczyn wektorowy każdy dokument z źródła, a pusty zestaw jest pusty.</span><span class="sxs-lookup"><span data-stu-id="f0070-504">In hello following example, hello result is empty since hello cross product of each document from source and an empty set is empty.</span></span>

<span data-ttu-id="f0070-505">**Zapytanie**</span><span class="sxs-lookup"><span data-stu-id="f0070-505">**Query**</span></span>

    SELECT f.id
    FROM Families f
    JOIN f.NonExistent

<span data-ttu-id="f0070-506">**Wyniki**</span><span class="sxs-lookup"><span data-stu-id="f0070-506">**Results**</span></span>  

    [{
    }]


<span data-ttu-id="f0070-507">Poniższy przykład hello, sprzężenia hello jest między hello elementu głównego dokumentu i hello `children` subroot.</span><span class="sxs-lookup"><span data-stu-id="f0070-507">In hello following example, hello join is between hello document root and hello `children` subroot.</span></span> <span data-ttu-id="f0070-508">Jest to produkt między między dwoma obiektami JSON.</span><span class="sxs-lookup"><span data-stu-id="f0070-508">It's a cross product between two JSON objects.</span></span> <span data-ttu-id="f0070-509">Hello fakt, że elementy podrzędne tablicy nie jest aktywne hello sprzężenia, ponieważ firma Microsoft ma do czynienia z jednym elementem głównym będący hello tablicy elementów podrzędnych.</span><span class="sxs-lookup"><span data-stu-id="f0070-509">hello fact that children is an array is not effective in hello JOIN since we are dealing with a single root that is hello children array.</span></span> <span data-ttu-id="f0070-510">Dlatego hello wynik zawiera tylko dwa wyników, ponieważ hello iloczyn wektorowy każdy dokument zawierający tablicę hello daje dokładnie tylko jeden dokument.</span><span class="sxs-lookup"><span data-stu-id="f0070-510">Hence hello result contains only two results, since hello cross product of each document with hello array yields exactly only one document.</span></span>

<span data-ttu-id="f0070-511">**Zapytanie**</span><span class="sxs-lookup"><span data-stu-id="f0070-511">**Query**</span></span>

    SELECT f.id
    FROM Families f
    JOIN f.children

<span data-ttu-id="f0070-512">**Wyniki**</span><span class="sxs-lookup"><span data-stu-id="f0070-512">**Results**</span></span>

    [
      {
        "id": "AndersenFamily"
      }, 
      {
        "id": "WakefieldFamily"
      }
    ]


<span data-ttu-id="f0070-513">Witaj poniższy przykład przedstawia bardziej z konwencjonalnej sprzężenia:</span><span class="sxs-lookup"><span data-stu-id="f0070-513">hello following example shows a more conventional join:</span></span>

<span data-ttu-id="f0070-514">**Zapytanie**</span><span class="sxs-lookup"><span data-stu-id="f0070-514">**Query**</span></span>

    SELECT f.id
    FROM Families f
    JOIN c IN f.children 

<span data-ttu-id="f0070-515">**Wyniki**</span><span class="sxs-lookup"><span data-stu-id="f0070-515">**Results**</span></span>

    [
      {
        "id": "AndersenFamily"
      }, 
      {
        "id": "WakefieldFamily"
      }, 
      {
        "id": "WakefieldFamily"
      }
    ]



<span data-ttu-id="f0070-516">Witaj po pierwsze toonote jest tym hello `from_source` z hello **JOIN** klauzula jest iteratora.</span><span class="sxs-lookup"><span data-stu-id="f0070-516">hello first thing toonote is that hello `from_source` of hello **JOIN** clause is an iterator.</span></span> <span data-ttu-id="f0070-517">Tak, hello przebieg w tym przypadku jest następujący:</span><span class="sxs-lookup"><span data-stu-id="f0070-517">So, hello flow in this case is as follows:</span></span>  

* <span data-ttu-id="f0070-518">Rozwiń węzeł każdego elementu podrzędnego **c** hello tablicy.</span><span class="sxs-lookup"><span data-stu-id="f0070-518">Expand each child element **c** in hello array.</span></span>
* <span data-ttu-id="f0070-519">Zastosuj iloczyn wektorowy z hello elementem głównym dokumentu hello **f** z każdym elementem podrzędnym **c** który został spłaszczone hello pierwszego kroku.</span><span class="sxs-lookup"><span data-stu-id="f0070-519">Apply a cross product with hello root of hello document **f** with each child element **c** that was flattened in hello first step.</span></span>
* <span data-ttu-id="f0070-520">Na koniec projektu obiekt główny hello **f** name — właściwość samodzielnie.</span><span class="sxs-lookup"><span data-stu-id="f0070-520">Finally, project hello root object **f** name property alone.</span></span> 

<span data-ttu-id="f0070-521">pierwszy dokument Hello (`AndersenFamily`) zawiera tylko jeden element podrzędny, w związku z czym hello zestaw wyników zawiera tylko jeden obiekt odpowiedni toothis dokument.</span><span class="sxs-lookup"><span data-stu-id="f0070-521">hello first document (`AndersenFamily`) contains only one child element, so hello result set contains only a single object corresponding toothis document.</span></span> <span data-ttu-id="f0070-522">drugi dokument Hello (`WakefieldFamily`) zawiera dwa elementy podrzędne.</span><span class="sxs-lookup"><span data-stu-id="f0070-522">hello second document (`WakefieldFamily`) contains two children.</span></span> <span data-ttu-id="f0070-523">Tak hello iloczyn wektorowy tworzy oddzielny obiekt dla każdego elementu podrzędnego, powodując dwa obiekty, po jednej dla każdego dokumentu toothis odpowiedniego podrzędnych.</span><span class="sxs-lookup"><span data-stu-id="f0070-523">So, hello cross product produces a separate object for each child, thereby resulting in two objects, one for each child corresponding toothis document.</span></span> <span data-ttu-id="f0070-524">główny Hello pola oba te dokumenty są hello takie same, zgodnie z oczekiwaniami w iloczyn wektorowy.</span><span class="sxs-lookup"><span data-stu-id="f0070-524">hello root fields in both these documents are hello same, just as you would expect in a cross product.</span></span>

<span data-ttu-id="f0070-525">Hello rzeczywistym narzędzie z hello sprzężenia jest krotek tooform z iloczyn wektorowy hello kształtu, który jest tooproject trudne.</span><span class="sxs-lookup"><span data-stu-id="f0070-525">hello real utility of hello JOIN is tooform tuples from hello cross-product in a shape that's otherwise difficult tooproject.</span></span> <span data-ttu-id="f0070-526">Ponadto, jak przedstawiono w poniższym przykładzie hello można filtrować na powitania kombinację krotka hello ten umożliwia użytkownik wybrał warunek spełniać hello spójnych kolekcji ogólnej.</span><span class="sxs-lookup"><span data-stu-id="f0070-526">Furthermore, as we see in hello example below, you could filter on hello combination of a tuple that lets' hello user chose a condition satisfied by hello tuples overall.</span></span>

<span data-ttu-id="f0070-527">**Zapytanie**</span><span class="sxs-lookup"><span data-stu-id="f0070-527">**Query**</span></span>

    SELECT 
        f.id AS familyName,
        c.givenName AS childGivenName,
        c.firstName AS childFirstName,
        p.givenName AS petName 
    FROM Families f 
    JOIN c IN f.children 
    JOIN p IN c.pets

<span data-ttu-id="f0070-528">**Wyniki**</span><span class="sxs-lookup"><span data-stu-id="f0070-528">**Results**</span></span>

    [
      {
        "familyName": "AndersenFamily", 
        "childFirstName": "Henriette Thaulow", 
        "petName": "Fluffy"
      }, 
      {
        "familyName": "WakefieldFamily", 
        "childGivenName": "Jesse", 
        "petName": "Goofy"
      }, 
      {
       "familyName": "WakefieldFamily", 
       "childGivenName": "Jesse", 
       "petName": "Shadow"
      }
    ]



<span data-ttu-id="f0070-529">W tym przykładzie stanowi naturalne rozszerzenie hello poprzedzających przykład i wykonuje sprzężenie dwa razy.</span><span class="sxs-lookup"><span data-stu-id="f0070-529">This example is a natural extension of hello preceding example, and performs a double join.</span></span> <span data-ttu-id="f0070-530">Tak hello iloczyn wektorowy można wyświetlić jako powitania po pseudo-kodu:</span><span class="sxs-lookup"><span data-stu-id="f0070-530">So, hello cross product can be viewed as hello following pseudo-code:</span></span>

    for-each(Family f in Families)
    {    
        for-each(Child c in f.children)
        {
            for-each(Pet p in c.pets)
            {
                return (Tuple(f.id AS familyName, 
                  c.givenName AS childGivenName, 
                  c.firstName AS childFirstName,
                  p.givenName AS petName));
            }
        }
    }

<span data-ttu-id="f0070-531">`AndersenFamily`ma jeden element podrzędny, który ma jedno zwierzę.</span><span class="sxs-lookup"><span data-stu-id="f0070-531">`AndersenFamily` has one child who has one pet.</span></span> <span data-ttu-id="f0070-532">Dlatego hello iloczyn wektorowy zwraca jeden wiersz (1\*1\*1) z tej rodziny.</span><span class="sxs-lookup"><span data-stu-id="f0070-532">So, hello cross product yields one row (1\*1\*1) from this family.</span></span> <span data-ttu-id="f0070-533">WakefieldFamily, ale zawiera dwa elementy podrzędne, ale tylko jeden element podrzędny "Jesse" ma zwierząt domowych.</span><span class="sxs-lookup"><span data-stu-id="f0070-533">WakefieldFamily however has two children, but only one child "Jesse" has pets.</span></span> <span data-ttu-id="f0070-534">Jesse jednak ma dwa zwierząt domowych.</span><span class="sxs-lookup"><span data-stu-id="f0070-534">Jesse has two pets though.</span></span> <span data-ttu-id="f0070-535">Dlatego hello iloczyn wektorowy daje 1\*1\*2 = 2 wierszy z tej rodziny.</span><span class="sxs-lookup"><span data-stu-id="f0070-535">Hence hello cross product yields 1\*1\*2 = 2 rows from this family.</span></span>

<span data-ttu-id="f0070-536">W następnym przykładzie hello na jest dodatkowy filtr `pet`.</span><span class="sxs-lookup"><span data-stu-id="f0070-536">In hello next example, there is an additional filter on `pet`.</span></span> <span data-ttu-id="f0070-537">Obejmuje to wszystkich krotek hello, których nazwa pet hello nie jest "Cienia".</span><span class="sxs-lookup"><span data-stu-id="f0070-537">This excludes all hello tuples where hello pet name is not "Shadow".</span></span> <span data-ttu-id="f0070-538">Zauważyć, że firma Microsoft są w stanie toobuild krotek z tablic, filtr na żadnym z elementów hello hello spójnej kolekcji, a dowolną kombinację hello elementów projektu.</span><span class="sxs-lookup"><span data-stu-id="f0070-538">Notice that we are able toobuild tuples from arrays, filter on any of hello elements of hello tuple, and project any combination of hello elements.</span></span> 

<span data-ttu-id="f0070-539">**Zapytanie**</span><span class="sxs-lookup"><span data-stu-id="f0070-539">**Query**</span></span>

    SELECT 
        f.id AS familyName,
        c.givenName AS childGivenName,
        c.firstName AS childFirstName,
        p.givenName AS petName 
    FROM Families f 
    JOIN c IN f.children 
    JOIN p IN c.pets
    WHERE p.givenName = "Shadow"

<span data-ttu-id="f0070-540">**Wyniki**</span><span class="sxs-lookup"><span data-stu-id="f0070-540">**Results**</span></span>

    [
      {
       "familyName": "WakefieldFamily", 
       "childGivenName": "Jesse", 
       "petName": "Shadow"
      }
    ]


## <span data-ttu-id="f0070-541"><a id="JavaScriptIntegration"></a>Integracja języka JavaScript</span><span class="sxs-lookup"><span data-stu-id="f0070-541"><a id="JavaScriptIntegration"></a>JavaScript integration</span></span>
<span data-ttu-id="f0070-542">Azure DB rozwiązania Cosmos zapewnia model programowania wykonywania logiki aplikacji JavaScript oparty bezpośrednio na kolekcje hello pod względem procedur składowanych i wyzwalaczy.</span><span class="sxs-lookup"><span data-stu-id="f0070-542">Azure Cosmos DB provides a programming model for executing JavaScript based application logic directly on hello collections in terms of stored procedures and triggers.</span></span> <span data-ttu-id="f0070-543">Dzięki temu zarówno dla:</span><span class="sxs-lookup"><span data-stu-id="f0070-543">This allows for both:</span></span>

* <span data-ttu-id="f0070-544">Możliwość toodo wysokiej wydajności transakcyjnych operacji CRUD i zapytań dotyczących dokumentów w kolekcji na podstawie hello głęboka Integracja środowiska wykonawczego języka JavaScript bezpośrednio wewnątrz aparatu bazy danych hello.</span><span class="sxs-lookup"><span data-stu-id="f0070-544">Ability toodo high-performance transactional CRUD operations and queries against documents in a collection by virtue of hello deep integration of JavaScript runtime directly within hello database engine.</span></span> 
* <span data-ttu-id="f0070-545">Fizyczne modelowania przepływu sterowania, zmiennej zakresu i przypisania i integracja z transakcji bazy danych w nim elementów podstawowych obsługi wyjątków.</span><span class="sxs-lookup"><span data-stu-id="f0070-545">A natural modeling of control flow, variable scoping, and assignment and integration of exception handling primitives with database transactions.</span></span> <span data-ttu-id="f0070-546">Aby uzyskać więcej informacji na temat bazy danych Azure rozwiązania Cosmos obsługę języka JavaScript integracji można znaleźć w dokumentacji programowania po stronie serwera JavaScript toohello.</span><span class="sxs-lookup"><span data-stu-id="f0070-546">For more details about Azure Cosmos DB support for JavaScript integration, please refer toohello JavaScript server-side programmability documentation.</span></span>

### <span data-ttu-id="f0070-547"><a id="UserDefinedFunctions"></a>Funkcje zdefiniowane przez użytkownika (UDF)</span><span class="sxs-lookup"><span data-stu-id="f0070-547"><a id="UserDefinedFunctions"></a>User-Defined Functions (UDFs)</span></span>
<span data-ttu-id="f0070-548">Wraz z typów hello już zdefiniowany w tym artykule SQL interfejsu API usługi DocumentDB zapewnia obsługę dla użytkownika określone funkcje (UDF).</span><span class="sxs-lookup"><span data-stu-id="f0070-548">Along with hello types already defined in this article, DocumentDB API SQL provides support for User Defined Functions (UDF).</span></span> <span data-ttu-id="f0070-549">W szczególności skalarne funkcji UDF są obsługiwane, której deweloperzy hello można przekazywać zero lub wiele argumentów i zwracanie wyniku pojedynczy argument ponownie.</span><span class="sxs-lookup"><span data-stu-id="f0070-549">In particular, scalar UDFs are supported where hello developers can pass in zero or many arguments and return a single argument result back.</span></span> <span data-ttu-id="f0070-550">Każdy z tych argumentów jest sprawdzany pod kątem trwa wartości JSON.</span><span class="sxs-lookup"><span data-stu-id="f0070-550">Each of these arguments is checked for being legal JSON values.</span></span>  

<span data-ttu-id="f0070-551">Witaj składni SQL usługi DocumentDB interfejsu API jest rozszerzony toosupport niestandardowej logiki aplikacji przy użyciu tych funkcji zdefiniowanych przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="f0070-551">hello DocumentDB API SQL syntax is extended toosupport custom application logic using these User-Defined Functions.</span></span> <span data-ttu-id="f0070-552">Funkcje UDF może być zarejestrowane przy użyciu interfejsu API usługi DocumentDB i odwoływać jako część zapytania SQL.</span><span class="sxs-lookup"><span data-stu-id="f0070-552">UDFs can be registered with DocumentDB API and then be referenced as part of a SQL query.</span></span> <span data-ttu-id="f0070-553">W rzeczywistości hello, funkcje UDF exquisitely są zaprojektowane toobe wywoływane przez zapytania.</span><span class="sxs-lookup"><span data-stu-id="f0070-553">In fact, hello UDFs are exquisitely designed toobe invoked by queries.</span></span> <span data-ttu-id="f0070-554">Jako opcja toothis następstwem funkcji UDF nie mają dostępu toohello kontekstu obiektu którego hello JavaScript innych typów (procedury składowane i wyzwalaczy).</span><span class="sxs-lookup"><span data-stu-id="f0070-554">As a corollary toothis choice, UDFs do not have access toohello context object which hello other JavaScript types (stored procedures and triggers) have.</span></span> <span data-ttu-id="f0070-555">Od czasu wykonania zapytania jako tylko do odczytu, można uruchomić na podstawowym lub w replikach pomocniczych.</span><span class="sxs-lookup"><span data-stu-id="f0070-555">Since queries execute as read-only, they can run either on primary or on secondary replicas.</span></span> <span data-ttu-id="f0070-556">W związku z tym funkcje UDF są zaprojektowane toorun w replikach pomocniczych, w odróżnieniu od innych typów języka JavaScript.</span><span class="sxs-lookup"><span data-stu-id="f0070-556">Therefore, UDFs are designed toorun on secondary replicas unlike other JavaScript types.</span></span>

<span data-ttu-id="f0070-557">Poniżej przedstawiono przykładowy sposób funkcji zdefiniowanej przez użytkownika może być zarejestrowany w bazy danych DB rozwiązania Cosmos hello, w szczególności w kolekcji dokumentów.</span><span class="sxs-lookup"><span data-stu-id="f0070-557">Below is an example of how a UDF can be registered at hello Cosmos DB database, specifically under a document collection.</span></span>

       UserDefinedFunction regexMatchUdf = new UserDefinedFunction
       {
           Id = "REGEX_MATCH",
           Body = @"function (input, pattern) { 
                       return input.match(pattern) !== null;
                   };",
       };

       UserDefinedFunction createdUdf = client.CreateUserDefinedFunctionAsync(
           UriFactory.CreateDocumentCollectionUri("testdb", "families"), 
           regexMatchUdf).Result;  

<span data-ttu-id="f0070-558">Witaj poprzednim przykładzie jest tworzony UDF, którego nazwa jest `REGEX_MATCH`.</span><span class="sxs-lookup"><span data-stu-id="f0070-558">hello preceding example creates a UDF whose name is `REGEX_MATCH`.</span></span> <span data-ttu-id="f0070-559">Akceptuje dwóch wartości ciągu JSON `input` i `pattern` i sprawdza, czy hello dopasowań pierwszy wzorzec hello określone w drugi hello przy użyciu funkcji string.match() języka JavaScript.</span><span class="sxs-lookup"><span data-stu-id="f0070-559">It accepts two JSON string values `input` and `pattern` and checks if hello first matches hello pattern specified in hello second using JavaScript's string.match() function.</span></span>

<span data-ttu-id="f0070-560">Firma Microsoft mogą teraz używać tej funkcji w zapytaniu w projekcji.</span><span class="sxs-lookup"><span data-stu-id="f0070-560">We can now use this UDF in a query in a projection.</span></span> <span data-ttu-id="f0070-561">Funkcje UDF musi być kwalifikowana za hello z uwzględnieniem wielkości liter prefiks "udf."</span><span class="sxs-lookup"><span data-stu-id="f0070-561">UDFs must be qualified with hello case-sensitive prefix "udf."</span></span> <span data-ttu-id="f0070-562">Po wywołaniu z wewnątrz zapytania.</span><span class="sxs-lookup"><span data-stu-id="f0070-562">when called from within queries.</span></span> 

> [!NOTE]
> <span data-ttu-id="f0070-563">Wcześniejsze too3 17 2015-, rozwiązania Cosmos DB obsługiwane wywołania funkcji zdefiniowanej przez użytkownika bez hello "udf."</span><span class="sxs-lookup"><span data-stu-id="f0070-563">Prior too3/17/2015, Cosmos DB supported UDF calls without hello "udf."</span></span> <span data-ttu-id="f0070-564">Prefiks, takich jak REGEX_MATCH() wybierz.</span><span class="sxs-lookup"><span data-stu-id="f0070-564">prefix like SELECT REGEX_MATCH().</span></span> <span data-ttu-id="f0070-565">Ten wzorzec wywołującego jest przestarzała.</span><span class="sxs-lookup"><span data-stu-id="f0070-565">This calling pattern has been deprecated.</span></span>  
> 
> 

<span data-ttu-id="f0070-566">**Zapytanie**</span><span class="sxs-lookup"><span data-stu-id="f0070-566">**Query**</span></span>

    SELECT udf.REGEX_MATCH(Families.address.city, ".*eattle")
    FROM Families

<span data-ttu-id="f0070-567">**Wyniki**</span><span class="sxs-lookup"><span data-stu-id="f0070-567">**Results**</span></span>

    [
      {
        "$1": true
      }, 
      {
        "$1": false
      }
    ]

<span data-ttu-id="f0070-568">Hello UDF również może być używany w filtrze, jak pokazano w przykładzie hello poniżej, również kwalifikowany za pomocą hello "udf."</span><span class="sxs-lookup"><span data-stu-id="f0070-568">hello UDF can also be used inside a filter as shown in hello example below, also qualified with hello "udf."</span></span> <span data-ttu-id="f0070-569">Prefiks:</span><span class="sxs-lookup"><span data-stu-id="f0070-569">prefix:</span></span>

<span data-ttu-id="f0070-570">**Zapytanie**</span><span class="sxs-lookup"><span data-stu-id="f0070-570">**Query**</span></span>

    SELECT Families.id, Families.address.city
    FROM Families
    WHERE udf.REGEX_MATCH(Families.address.city, ".*eattle")

<span data-ttu-id="f0070-571">**Wyniki**</span><span class="sxs-lookup"><span data-stu-id="f0070-571">**Results**</span></span>

    [{
        "id": "AndersenFamily",
        "city": "Seattle"
    }]


<span data-ttu-id="f0070-572">W zasadzie funkcje UDF są prawidłowe wyrażenia skalarne i mogą być używane w zarówno projekcje i filtry.</span><span class="sxs-lookup"><span data-stu-id="f0070-572">In essence, UDFs are valid scalar expressions and can be used in both projections and filters.</span></span> 

<span data-ttu-id="f0070-573">tooexpand zasilania hello funkcji UDF, Przyjrzyjmy się innym przykładem w logice warunkowego:</span><span class="sxs-lookup"><span data-stu-id="f0070-573">tooexpand on hello power of UDFs, let's look at another example with conditional logic:</span></span>

       UserDefinedFunction seaLevelUdf = new UserDefinedFunction()
       {
           Id = "SEALEVEL",
           Body = @"function(city) {
                   switch (city) {
                       case 'seattle':
                           return 520;
                       case 'NY':
                           return 410;
                       case 'Chicago':
                           return 673;
                       default:
                           return -1;
                    }"
            };

            UserDefinedFunction createdUdf = await client.CreateUserDefinedFunctionAsync(
                UriFactory.CreateDocumentCollectionUri("testdb", "families"), 
                seaLevelUdf);


<span data-ttu-id="f0070-574">Poniżej znajduje się przykład czy ćwiczeń hello funkcji zdefiniowanej przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="f0070-574">Below is an example that exercises hello UDF.</span></span>

<span data-ttu-id="f0070-575">**Zapytanie**</span><span class="sxs-lookup"><span data-stu-id="f0070-575">**Query**</span></span>

    SELECT f.address.city, udf.SEALEVEL(f.address.city) AS seaLevel
    FROM Families f    

<span data-ttu-id="f0070-576">**Wyniki**</span><span class="sxs-lookup"><span data-stu-id="f0070-576">**Results**</span></span>

     [
      {
        "city": "seattle", 
        "seaLevel": 520
      }, 
      {
        "city": "NY", 
        "seaLevel": 410
      }
    ]


<span data-ttu-id="f0070-577">Jak hello poprzedniego pokazy przykłady, funkcji UDF integracji zasilania hello języka JavaScript z tooprovide SQL interfejsu API usługi DocumentDB hello sformatowanego programowalny toodo złożonych procedurach, warunkowego logikę interfejsu za pomocą hello wbudowanych środowiska wykonawczego języka JavaScript możliwości.</span><span class="sxs-lookup"><span data-stu-id="f0070-577">As hello preceding examples showcase, UDFs integrate hello power of JavaScript language with hello DocumentDB API SQL tooprovide a rich programmable interface toodo complex procedural, conditional logic with hello help of inbuilt JavaScript runtime capabilities.</span></span>

<span data-ttu-id="f0070-578">SQL interfejsu API usługi DocumentDB zawiera argumenty hello toohello funkcji UDF dla każdego dokumentu w źródle hello etapu hello bieżący (w klauzuli WHERE lub w klauzuli SELECT) hello przetwarzania UDF.</span><span class="sxs-lookup"><span data-stu-id="f0070-578">DocumentDB API SQL provides hello arguments toohello UDFs for each document in hello source at hello current stage (WHERE clause or SELECT clause) of processing hello UDF.</span></span> <span data-ttu-id="f0070-579">Witaj wynik jest włączona w bezproblemowo hello ogólną wykonywania potoku.</span><span class="sxs-lookup"><span data-stu-id="f0070-579">hello result is incorporated in hello overall execution pipeline seamlessly.</span></span> <span data-ttu-id="f0070-580">Jeśli właściwości hello tooby określonego hello UDF parametry nie są dostępne w hello wartość JSON hello się, że parametr jest uznawany za niezdefiniowane i dlatego hello wywołania funkcji zdefiniowanej przez użytkownika jest całkowicie pomijane.</span><span class="sxs-lookup"><span data-stu-id="f0070-580">If hello properties referred tooby hello UDF parameters are not available in hello JSON value, hello parameter is considered as undefined and hence hello UDF invocation is entirely skipped.</span></span> <span data-ttu-id="f0070-581">Podobnie jeśli zdefiniowano hello wynik hello UDF go nie jest uwzględniony w wyniku hello.</span><span class="sxs-lookup"><span data-stu-id="f0070-581">Similarly if hello result of hello UDF is undefined, it's not included in hello result.</span></span> 

<span data-ttu-id="f0070-582">Podsumowując funkcje UDF są doskonałe narzędzia toodo złożonej logiki biznesowej w ramach zapytania hello.</span><span class="sxs-lookup"><span data-stu-id="f0070-582">In summary, UDFs are great tools toodo complex business logic as part of hello query.</span></span>

### <a name="operator-evaluation"></a><span data-ttu-id="f0070-583">Ocena — operator</span><span class="sxs-lookup"><span data-stu-id="f0070-583">Operator evaluation</span></span>
<span data-ttu-id="f0070-584">Rozwiązania cosmos bazy danych, na mocy hello jest bazą danych JSON, rysuje równoleżników JavaScript — operatory i jego semantyki oceny.</span><span class="sxs-lookup"><span data-stu-id="f0070-584">Cosmos DB, by hello virtue of being a JSON database, draws parallels with JavaScript operators and its evaluation semantics.</span></span> <span data-ttu-id="f0070-585">Gdy DB rozwiązania Cosmos podejmie próbę semantyki JavaScript toopreserve pod względem obsługi JSON, oceny operacji hello odbiega w niektórych przypadkach.</span><span class="sxs-lookup"><span data-stu-id="f0070-585">While Cosmos DB tries toopreserve JavaScript semantics in terms of JSON support, hello operation evaluation deviates in some instances.</span></span>

<span data-ttu-id="f0070-586">W programie SQL usługi DocumentDB interfejsu API w przeciwieństwie do tradycyjnych SQL hello typy wartości często nie są znane aż do wartości hello są pobierane z bazy danych.</span><span class="sxs-lookup"><span data-stu-id="f0070-586">In DocumentDB API SQL, unlike in traditional SQL, hello types of values are often not known until hello values are retrieved from database.</span></span> <span data-ttu-id="f0070-587">W kolejności tooefficiently wykonywanie zapytań, większość operatorów hello ma wymagania typu strict.</span><span class="sxs-lookup"><span data-stu-id="f0070-587">In order tooefficiently execute queries, most of hello operators have strict type requirements.</span></span> 

<span data-ttu-id="f0070-588">Usługa DocumentDB interfejsu API SQL nie działa niejawne konwersje, w przeciwieństwie do języka JavaScript.</span><span class="sxs-lookup"><span data-stu-id="f0070-588">DocumentDB API SQL doesn't perform implicit conversions, unlike JavaScript.</span></span> <span data-ttu-id="f0070-589">Na przykład, takich jak kwerendy `SELECT * FROM Person p WHERE p.Age = 21` odpowiada dokumentów, które zawierają właściwość wieku, którego wartość to 21.</span><span class="sxs-lookup"><span data-stu-id="f0070-589">For instance, a query like `SELECT * FROM Person p WHERE p.Age = 21` matches documents that contain an Age property whose value is 21.</span></span> <span data-ttu-id="f0070-590">Innych dokumentów, których właściwość wieku odpowiada ciągu "21" lub innych zmian prawdopodobnie nieskończone, takich jak "021", "21.0", "0021", "00021", nie będzie można dopasować itp.</span><span class="sxs-lookup"><span data-stu-id="f0070-590">Any other document whose Age property matches string "21", or other possibly infinite variations like "021", "21.0", "0021", "00021", etc. will not be matched.</span></span> <span data-ttu-id="f0070-591">Jest to z kolei toohello JavaScript, w których toonumbers niejawnie rzutować wartości ciągu hello (na podstawie operatora, np: ==).</span><span class="sxs-lookup"><span data-stu-id="f0070-591">This is in contrast toohello JavaScript where hello string values are implicitly casted toonumbers (based on operator, ex: ==).</span></span> <span data-ttu-id="f0070-592">Ten wybór jest kluczowe znaczenie dla efektywnego indeksu pasujące SQL interfejsu API usługi DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="f0070-592">This choice is crucial for efficient index matching in DocumentDB API SQL.</span></span> 

## <a name="parameterized-sql-queries"></a><span data-ttu-id="f0070-593">Sparametryzowane zapytania SQL</span><span class="sxs-lookup"><span data-stu-id="f0070-593">Parameterized SQL queries</span></span>
<span data-ttu-id="f0070-594">Rozwiązania cosmos bazy danych obsługuje zapytania z parametrami wyrażone z hello znanych @ notacji.</span><span class="sxs-lookup"><span data-stu-id="f0070-594">Cosmos DB supports queries with parameters expressed with hello familiar @ notation.</span></span> <span data-ttu-id="f0070-595">Sparametryzowane SQL zapewnia niezawodne obsługi i anulowanie z danych wprowadzonych przez użytkownika, uniemożliwia przypadkowe ujawnienie danych za pomocą iniekcji kodu SQL.</span><span class="sxs-lookup"><span data-stu-id="f0070-595">Parameterized SQL provides robust handling and escaping of user input, preventing accidental exposure of data through SQL injection.</span></span> 

<span data-ttu-id="f0070-596">Można na przykład napisz zapytanie, które przyjmuje jako parametry nazwisko i adres Stan i wykonaj go dla różnych wartości nazwisko i adres Stan oparte na danych wejściowych użytkownika.</span><span class="sxs-lookup"><span data-stu-id="f0070-596">For example, you can write a query that takes last name and address state as parameters, and then execute it for various values of last name and address state based on user input.</span></span>

    SELECT * 
    FROM Families f
    WHERE f.lastName = @lastName AND f.address.state = @addressState

<span data-ttu-id="f0070-597">To żądanie można następnie wysłać tooCosmos bazy danych jako zapytania parametrycznego JSON, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="f0070-597">This request can then be sent tooCosmos DB as a parameterized JSON query like shown below.</span></span>

    {      
        "query": "SELECT * FROM Families f WHERE f.lastName = @lastName AND f.address.state = @addressState",     
        "parameters": [          
            {"name": "@lastName", "value": "Wakefield"},         
            {"name": "@addressState", "value": "NY"},           
        ] 
    }

<span data-ttu-id="f0070-598">Hello argument tooTOP można ustawić użycie zapytań sparametryzowanych, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="f0070-598">hello argument tooTOP can be set using parameterized queries like shown below.</span></span>

    {      
        "query": "SELECT TOP @n * FROM Families",     
        "parameters": [          
            {"name": "@n", "value": 10},         
        ] 
    }

<span data-ttu-id="f0070-599">Wartości parametru może być dowolnym poprawne dane JSON (ciągów, liczb, wartości logiczne, null, nawet tablice lub zagnieżdżone JSON).</span><span class="sxs-lookup"><span data-stu-id="f0070-599">Parameter values can be any valid JSON (strings, numbers, Booleans, null, even arrays or nested JSON).</span></span> <span data-ttu-id="f0070-600">Również DB rozwiązania Cosmos jest bez schematu, parametry nie są weryfikowane względem dowolnego typu.</span><span class="sxs-lookup"><span data-stu-id="f0070-600">Also since Cosmos DB is schema-less, parameters are not validated against any type.</span></span>

## <span data-ttu-id="f0070-601"><a id="BuiltinFunctions"></a>Funkcje wbudowane</span><span class="sxs-lookup"><span data-stu-id="f0070-601"><a id="BuiltinFunctions"></a>Built-in functions</span></span>
<span data-ttu-id="f0070-602">Rozwiązania cosmos bazy danych obsługuje również kilka wbudowanych funkcji typowych operacji, które mogą być używane wewnątrz zapytań, takich jak funkcje zdefiniowane przez użytkownika (UDF).</span><span class="sxs-lookup"><span data-stu-id="f0070-602">Cosmos DB also supports a number of built-in functions for common operations, that can be used inside queries like user-defined functions (UDFs).</span></span>

| <span data-ttu-id="f0070-603">Grupy — funkcja</span><span class="sxs-lookup"><span data-stu-id="f0070-603">Function group</span></span>          | <span data-ttu-id="f0070-604">Operacje</span><span class="sxs-lookup"><span data-stu-id="f0070-604">Operations</span></span>                                                                                                                                          |
|-------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="f0070-605">Funkcje matematyczne</span><span class="sxs-lookup"><span data-stu-id="f0070-605">Mathematical functions</span></span>  | <span data-ttu-id="f0070-606">ABS, limitu, EXP, FLOOR, dziennika, LOG10, zasilania, ROUND, logowania, SQRT, KWADRATOWYCH, TRUNC, ACOS, ASIN, ATAN, ATN2, COS, KOT, stopni PI, wartość w RADIANACH, SIN i TAN</span><span class="sxs-lookup"><span data-stu-id="f0070-606">ABS, CEILING, EXP, FLOOR, LOG, LOG10, POWER, ROUND, SIGN, SQRT, SQUARE, TRUNC, ACOS, ASIN, ATAN, ATN2, COS, COT, DEGREES, PI, RADIANS, SIN, and TAN</span></span> |
| <span data-ttu-id="f0070-607">Typ funkcji sprawdzania</span><span class="sxs-lookup"><span data-stu-id="f0070-607">Type checking functions</span></span> | <span data-ttu-id="f0070-608">Is_array —, IS_BOOL IS_NULL, IS_NUMBER, is_object —, IS_STRING, IS_DEFINED i IS_PRIMITIVE</span><span class="sxs-lookup"><span data-stu-id="f0070-608">IS_ARRAY, IS_BOOL, IS_NULL, IS_NUMBER, IS_OBJECT, IS_STRING, IS_DEFINED, and IS_PRIMITIVE</span></span>                                                           |
| <span data-ttu-id="f0070-609">Funkcje ciągów</span><span class="sxs-lookup"><span data-stu-id="f0070-609">String functions</span></span>        | <span data-ttu-id="f0070-610">CONCAT, zawiera ENDSWITH, INDEX_OF, po lewej, długość, małe, LTRIM, ZAMIEŃ, REPLIKACJA, ODWROTNIE, prawo, RTRIM, STARTSWITH, PODCIĄG i górna</span><span class="sxs-lookup"><span data-stu-id="f0070-610">CONCAT, CONTAINS, ENDSWITH, INDEX_OF, LEFT, LENGTH, LOWER, LTRIM, REPLACE, REPLICATE, REVERSE, RIGHT, RTRIM, STARTSWITH, SUBSTRING, and UPPER</span></span>       |
| <span data-ttu-id="f0070-611">Funkcje tablicy</span><span class="sxs-lookup"><span data-stu-id="f0070-611">Array functions</span></span>         | <span data-ttu-id="f0070-612">ARRAY_CONCAT, ARRAY_CONTAINS ARRAY_LENGTH i ARRAY_SLICE</span><span class="sxs-lookup"><span data-stu-id="f0070-612">ARRAY_CONCAT, ARRAY_CONTAINS, ARRAY_LENGTH, and ARRAY_SLICE</span></span>                                                                                         |
| <span data-ttu-id="f0070-613">Funkcje przestrzenne</span><span class="sxs-lookup"><span data-stu-id="f0070-613">Spatial functions</span></span>       | <span data-ttu-id="f0070-614">ST_DISTANCE, ST_WITHIN ST_INTERSECTS, ST_ISVALID i ST_ISVALIDDETAILED</span><span class="sxs-lookup"><span data-stu-id="f0070-614">ST_DISTANCE, ST_WITHIN, ST_INTERSECTS, ST_ISVALID, and ST_ISVALIDDETAILED</span></span>                                                                           | 

<span data-ttu-id="f0070-615">Jeśli obecnie używasz — funkcja zdefiniowana przez użytkownika (UDF) dla której wbudowana funkcja jest teraz dostępna, należy używać hello odpowiedniego wbudowanych funkcji, ponieważ będzie toobe toorun szybsze i inne wydajnie.</span><span class="sxs-lookup"><span data-stu-id="f0070-615">If you’re currently using a user-defined function (UDF) for which a built-in function is now available, you should use hello corresponding built-in function as it is going toobe quicker toorun and more efficiently.</span></span> 

### <a name="mathematical-functions"></a><span data-ttu-id="f0070-616">Funkcje matematyczne</span><span class="sxs-lookup"><span data-stu-id="f0070-616">Mathematical functions</span></span>
<span data-ttu-id="f0070-617">Witaj funkcje matematyczne każdego wykonywanie obliczeń, na podstawie wartości wejściowych, które są przekazywane jako argumenty i zwracać wartość liczbową.</span><span class="sxs-lookup"><span data-stu-id="f0070-617">hello mathematical functions each perform a calculation, based on input values that are provided as arguments, and return a numeric value.</span></span> <span data-ttu-id="f0070-618">W tym miejscu znajduje się tabela obsługiwanych wbudowanych funkcji matematycznych.</span><span class="sxs-lookup"><span data-stu-id="f0070-618">Here’s a table of supported built-in mathematical functions.</span></span>


| <span data-ttu-id="f0070-619">Sposób użycia</span><span class="sxs-lookup"><span data-stu-id="f0070-619">Usage</span></span> | <span data-ttu-id="f0070-620">Opis</span><span class="sxs-lookup"><span data-stu-id="f0070-620">Description</span></span> |
|----------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="f0070-621">[[ABS (num_expr)](#bk_abs)</span><span class="sxs-lookup"><span data-stu-id="f0070-621">[[ABS (num_expr)](#bk_abs)</span></span> | <span data-ttu-id="f0070-622">Zwraca hello bezwzględną () wartości dodatniej hello określone wyrażenie liczbowe.</span><span class="sxs-lookup"><span data-stu-id="f0070-622">Returns hello absolute (positive) value of hello specified numeric expression.</span></span> |
| [<span data-ttu-id="f0070-623">CEILING (num_expr)</span><span class="sxs-lookup"><span data-stu-id="f0070-623">CEILING (num_expr)</span></span>](#bk_ceiling) | <span data-ttu-id="f0070-624">Zwraca hello najmniejszą liczbę całkowitą większą niż lub równa, hello określonego wyrażenia liczbowego.</span><span class="sxs-lookup"><span data-stu-id="f0070-624">Returns hello smallest integer value greater than, or equal to, hello specified numeric expression.</span></span> |
| [<span data-ttu-id="f0070-625">FLOOR (num_expr)</span><span class="sxs-lookup"><span data-stu-id="f0070-625">FLOOR (num_expr)</span></span>](#bk_floor) | <span data-ttu-id="f0070-626">Zwraca hello największa liczba całkowita mniejsza lub równa toohello określone wyrażenie liczbowe.</span><span class="sxs-lookup"><span data-stu-id="f0070-626">Returns hello largest integer less than or equal toohello specified numeric expression.</span></span> |
| [<span data-ttu-id="f0070-627">EXP (num_expr)</span><span class="sxs-lookup"><span data-stu-id="f0070-627">EXP (num_expr)</span></span>](#bk_exp) | <span data-ttu-id="f0070-628">Zwraca wykładnik hello hello określone wyrażenie liczbowe.</span><span class="sxs-lookup"><span data-stu-id="f0070-628">Returns hello exponent of hello specified numeric expression.</span></span> |
| <span data-ttu-id="f0070-629">[Dziennik (num_expr [, base])](#bk_log)</span><span class="sxs-lookup"><span data-stu-id="f0070-629">[LOG (num_expr [,base])](#bk_log)</span></span> | <span data-ttu-id="f0070-630">Zwraca logarytm naturalny hello hello określony wyrażenia liczbowego, lub za pomocą hello logarytm hello określony podstawowy</span><span class="sxs-lookup"><span data-stu-id="f0070-630">Returns hello natural logarithm of hello specified numeric expression, or hello logarithm using hello specified base</span></span> |
| [<span data-ttu-id="f0070-631">LOG10 (num_expr)</span><span class="sxs-lookup"><span data-stu-id="f0070-631">LOG10 (num_expr)</span></span>](#bk_log10) | <span data-ttu-id="f0070-632">Zwraca hello base 10 logarytmicznej wartość hello określona wyrażenia liczbowego.</span><span class="sxs-lookup"><span data-stu-id="f0070-632">Returns hello base-10 logarithmic value of hello specified numeric expression.</span></span> |
| [<span data-ttu-id="f0070-633">ZAOKRĄGLIJ (num_expr)</span><span class="sxs-lookup"><span data-stu-id="f0070-633">ROUND (num_expr)</span></span>](#bk_round) | <span data-ttu-id="f0070-634">Zwraca wartość liczbową zaokrąglony toohello najbliższej liczby całkowitej wartości.</span><span class="sxs-lookup"><span data-stu-id="f0070-634">Returns a numeric value, rounded toohello closest integer value.</span></span> |
| [<span data-ttu-id="f0070-635">TRUNC (num_expr)</span><span class="sxs-lookup"><span data-stu-id="f0070-635">TRUNC (num_expr)</span></span>](#bk_trunc) | <span data-ttu-id="f0070-636">Zwraca wartość liczbową skróconą toohello najbliższą wartość całkowitą.</span><span class="sxs-lookup"><span data-stu-id="f0070-636">Returns a numeric value, truncated toohello closest integer value.</span></span> |
| [<span data-ttu-id="f0070-637">SQRT (num_expr)</span><span class="sxs-lookup"><span data-stu-id="f0070-637">SQRT (num_expr)</span></span>](#bk_sqrt) | <span data-ttu-id="f0070-638">Zwraca pierwiastek kwadratowy hello hello określone wyrażenie liczbowe.</span><span class="sxs-lookup"><span data-stu-id="f0070-638">Returns hello square root of hello specified numeric expression.</span></span> |
| [<span data-ttu-id="f0070-639">(Num_expr) KWADRATU</span><span class="sxs-lookup"><span data-stu-id="f0070-639">SQUARE (num_expr)</span></span>](#bk_square) | <span data-ttu-id="f0070-640">Zwraca hello kwadratowy z hello określone wyrażenie liczbowe.</span><span class="sxs-lookup"><span data-stu-id="f0070-640">Returns hello square of hello specified numeric expression.</span></span> |
| [<span data-ttu-id="f0070-641">ZASILANIA (num_expr, num_expr)</span><span class="sxs-lookup"><span data-stu-id="f0070-641">POWER (num_expr, num_expr)</span></span>](#bk_power) | <span data-ttu-id="f0070-642">Zwraca możliwości hello hello podać wartość toohello wyrażenia liczbowego.</span><span class="sxs-lookup"><span data-stu-id="f0070-642">Returns hello power of hello specified numeric expression toohello value specified.</span></span> |
| [<span data-ttu-id="f0070-643">ZNAK (num_expr)</span><span class="sxs-lookup"><span data-stu-id="f0070-643">SIGN (num_expr)</span></span>](#bk_sign) | <span data-ttu-id="f0070-644">Zwraca hello logowania (-1, 0, 1) z hello podać wartość wyrażenia liczbowego.</span><span class="sxs-lookup"><span data-stu-id="f0070-644">Returns hello sign value (-1, 0, 1) of hello specified numeric expression.</span></span> |
| [<span data-ttu-id="f0070-645">ACOS (num_expr)</span><span class="sxs-lookup"><span data-stu-id="f0070-645">ACOS (num_expr)</span></span>](#bk_acos) | <span data-ttu-id="f0070-646">Zwraca hello kąt w radianach, którego cosinus jest hello określonego wyrażenia liczbowego. Skrót cosinus.</span><span class="sxs-lookup"><span data-stu-id="f0070-646">Returns hello angle, in radians, whose cosine is hello specified numeric expression; also called arccosine.</span></span> |
| [<span data-ttu-id="f0070-647">ASIN (num_expr)</span><span class="sxs-lookup"><span data-stu-id="f0070-647">ASIN (num_expr)</span></span>](#bk_asin) | <span data-ttu-id="f0070-648">Zwraca hello kąt w radianach, którego sinusem jest dana hello określony wyrażenia liczbowego.</span><span class="sxs-lookup"><span data-stu-id="f0070-648">Returns hello angle, in radians, whose sine is hello specified numeric expression.</span></span> <span data-ttu-id="f0070-649">Jest to również sinus.</span><span class="sxs-lookup"><span data-stu-id="f0070-649">This is also called arcsine.</span></span> |
| [<span data-ttu-id="f0070-650">ATAN (num_expr)</span><span class="sxs-lookup"><span data-stu-id="f0070-650">ATAN (num_expr)</span></span>](#bk_atan) | <span data-ttu-id="f0070-651">Zwraca hello kąt w radianach, którego tangens jest hello określony wyrażenia liczbowego.</span><span class="sxs-lookup"><span data-stu-id="f0070-651">Returns hello angle, in radians, whose tangent is hello specified numeric expression.</span></span> <span data-ttu-id="f0070-652">Jest to również tangens.</span><span class="sxs-lookup"><span data-stu-id="f0070-652">This is also called arctangent.</span></span> |
| [<span data-ttu-id="f0070-653">ATN2 (num_expr)</span><span class="sxs-lookup"><span data-stu-id="f0070-653">ATN2 (num_expr)</span></span>](#bk_atn2) | <span data-ttu-id="f0070-654">Zwraca hello kąt w radianach, między hello dodatnią osi x i promień powitania od hello pochodzenia toohello punkt (y, x), gdzie x i y są wartości hello hello dwóch wyrażeń określonego typu float.</span><span class="sxs-lookup"><span data-stu-id="f0070-654">Returns hello angle, in radians, between hello positive x-axis and hello ray from hello origin toohello point (y, x), where x and y are hello values of hello two specified float expressions.</span></span> |
| [<span data-ttu-id="f0070-655">COS (num_expr)</span><span class="sxs-lookup"><span data-stu-id="f0070-655">COS (num_expr)</span></span>](#bk_cos) | <span data-ttu-id="f0070-656">Zwraca hello trygonometryczne cosinus hello określony kąt w radianach, w hello określone wyrażenie.</span><span class="sxs-lookup"><span data-stu-id="f0070-656">Returns hello trigonometric cosine of hello specified angle, in radians, in hello specified expression.</span></span> |
| [<span data-ttu-id="f0070-657">KOT (num_expr)</span><span class="sxs-lookup"><span data-stu-id="f0070-657">COT (num_expr)</span></span>](#bk_cot) | <span data-ttu-id="f0070-658">Zwraca hello trygonometryczne cotangens hello określony kąt w radianach, w hello określonego wyrażenia liczbowego.</span><span class="sxs-lookup"><span data-stu-id="f0070-658">Returns hello trigonometric cotangent of hello specified angle, in radians, in hello specified numeric expression.</span></span> |
| [<span data-ttu-id="f0070-659">STOPNI (num_expr)</span><span class="sxs-lookup"><span data-stu-id="f0070-659">DEGREES (num_expr)</span></span>](#bk_degrees) | <span data-ttu-id="f0070-660">Zwraca hello odpowiadający mu kąt w stopniach dla kąta określonego w radianach.</span><span class="sxs-lookup"><span data-stu-id="f0070-660">Returns hello corresponding angle in degrees for an angle specified in radians.</span></span> |
| [<span data-ttu-id="f0070-661">PI)</span><span class="sxs-lookup"><span data-stu-id="f0070-661">PI ()</span></span>](#bk_pi) | <span data-ttu-id="f0070-662">Zwraca hello stałą wartość PI.</span><span class="sxs-lookup"><span data-stu-id="f0070-662">Returns hello constant value of PI.</span></span> |
| [<span data-ttu-id="f0070-663">Wartość w RADIANACH (num_expr)</span><span class="sxs-lookup"><span data-stu-id="f0070-663">RADIANS (num_expr)</span></span>](#bk_radians) | <span data-ttu-id="f0070-664">Zwraca wartość w radianach, po wprowadzeniu w stopniach, wyrażenia liczbowego.</span><span class="sxs-lookup"><span data-stu-id="f0070-664">Returns radians when a numeric expression, in degrees, is entered.</span></span> |
| [<span data-ttu-id="f0070-665">SIN (num_expr)</span><span class="sxs-lookup"><span data-stu-id="f0070-665">SIN (num_expr)</span></span>](#bk_sin) | <span data-ttu-id="f0070-666">Zwraca hello trygonometryczne sinus hello określony kąt w radianach, w hello określone wyrażenie.</span><span class="sxs-lookup"><span data-stu-id="f0070-666">Returns hello trigonometric sine of hello specified angle, in radians, in hello specified expression.</span></span> |
| [<span data-ttu-id="f0070-667">TAN (num_expr)</span><span class="sxs-lookup"><span data-stu-id="f0070-667">TAN (num_expr)</span></span>](#bk_tan) | <span data-ttu-id="f0070-668">Zwraca tangens hello hello wyrażenie wejściowe w hello określone wyrażenie.</span><span class="sxs-lookup"><span data-stu-id="f0070-668">Returns hello tangent of hello input expression, in hello specified expression.</span></span> |

<span data-ttu-id="f0070-669">Na przykład można teraz uruchomić zapytania, takie jak następujące hello:</span><span class="sxs-lookup"><span data-stu-id="f0070-669">For example, you can now run queries like hello following:</span></span>

<span data-ttu-id="f0070-670">**Zapytanie**</span><span class="sxs-lookup"><span data-stu-id="f0070-670">**Query**</span></span>

    SELECT VALUE ABS(-4)

<span data-ttu-id="f0070-671">**Wyniki**</span><span class="sxs-lookup"><span data-stu-id="f0070-671">**Results**</span></span>

    [4]

<span data-ttu-id="f0070-672">Hello podstawowa różnica między tooANSI funkcji w porównaniu rozwiązania Cosmos bazy danych SQL polega na tym, że są one przeznaczone toowork prawidłowo w przypadku danych bez schematu i mieszanych schematu.</span><span class="sxs-lookup"><span data-stu-id="f0070-672">hello main difference between Cosmos DB’s functions compared tooANSI SQL is that they are designed toowork well with schema-less and mixed schema data.</span></span> <span data-ttu-id="f0070-673">Na przykład jeśli dokument, w którym brakuje właściwości Size hello, lub ma wartości nieliczbowe, takich jak "Nieznane", a następnie dokumentu hello jest pominięty, zamiast zwróciła błąd.</span><span class="sxs-lookup"><span data-stu-id="f0070-673">For example, if you have a document where hello Size property is missing, or has a non-numeric value like “unknown”, then hello document is skipped over, instead of returning an error.</span></span>

### <a name="type-checking-functions"></a><span data-ttu-id="f0070-674">Typ funkcji sprawdzania</span><span class="sxs-lookup"><span data-stu-id="f0070-674">Type checking functions</span></span>
<span data-ttu-id="f0070-675">Sprawdzanie, czy funkcje typu Hello pozwalają toocheck hello typ wyrażenia w obrębie zapytania SQL.</span><span class="sxs-lookup"><span data-stu-id="f0070-675">hello type checking functions allow you toocheck hello type of an expression within SQL queries.</span></span> <span data-ttu-id="f0070-676">Typ funkcji sprawdzania może być używany typ hello toodetermine właściwości w dokumentach na bieżąco hello, gdy jest zmienna lub nieznany.</span><span class="sxs-lookup"><span data-stu-id="f0070-676">Type checking functions can be used toodetermine hello type of properties within documents on hello fly when it is variable or unknown.</span></span> <span data-ttu-id="f0070-677">W tym miejscu znajduje się tabela obsługiwanym typem wbudowane funkcje kontroli.</span><span class="sxs-lookup"><span data-stu-id="f0070-677">Here’s a table of supported built-in type checking functions.</span></span>

<table>
<tr>
  <td><span data-ttu-id="f0070-678"><strong>Użycie</strong></span><span class="sxs-lookup"><span data-stu-id="f0070-678"><strong>Usage</strong></span></span></td>
  <td><span data-ttu-id="f0070-679"><strong>Opis</strong></span><span class="sxs-lookup"><span data-stu-id="f0070-679"><strong>Description</strong></span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="f0070-680"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_array">Is_array — (wyrażenie)</a></span><span class="sxs-lookup"><span data-stu-id="f0070-680"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_array">IS_ARRAY (expr)</a></span></span></td>
  <td><span data-ttu-id="f0070-681">Zwraca wartość Boolean wskazującą, czy hello typ wartości hello jest tablicą.</span><span class="sxs-lookup"><span data-stu-id="f0070-681">Returns a Boolean indicating if hello type of hello value is an array.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="f0070-682"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_bool">IS_BOOL (wyrażenie)</a></span><span class="sxs-lookup"><span data-stu-id="f0070-682"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_bool">IS_BOOL (expr)</a></span></span></td>
  <td><span data-ttu-id="f0070-683">Zwraca wartość Boolean wskazującą, czy typ hello wartości hello jest wartością logiczną.</span><span class="sxs-lookup"><span data-stu-id="f0070-683">Returns a Boolean indicating if hello type of hello value is a Boolean.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="f0070-684"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_null">IS_NULL (wyrażenie)</a></span><span class="sxs-lookup"><span data-stu-id="f0070-684"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_null">IS_NULL (expr)</a></span></span></td>
  <td><span data-ttu-id="f0070-685">Zwraca wartość Boolean wskazującą, czy typ hello hello wartości ma wartość null.</span><span class="sxs-lookup"><span data-stu-id="f0070-685">Returns a Boolean indicating if hello type of hello value is null.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="f0070-686"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_number">IS_NUMBER (wyrażenie)</a></span><span class="sxs-lookup"><span data-stu-id="f0070-686"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_number">IS_NUMBER (expr)</a></span></span></td>
  <td><span data-ttu-id="f0070-687">Zwraca wartość Boolean wskazującą, czy typ hello wartości hello jest liczbą.</span><span class="sxs-lookup"><span data-stu-id="f0070-687">Returns a Boolean indicating if hello type of hello value is a number.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="f0070-688"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_object">Is_object — (wyrażenie)</a></span><span class="sxs-lookup"><span data-stu-id="f0070-688"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_object">IS_OBJECT (expr)</a></span></span></td>
  <td><span data-ttu-id="f0070-689">Zwraca wartość Boolean wskazującą, czy typ hello wartości hello jest obiekt JSON.</span><span class="sxs-lookup"><span data-stu-id="f0070-689">Returns a Boolean indicating if hello type of hello value is a JSON object.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="f0070-690"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_string">IS_STRING (wyrażenie)</a></span><span class="sxs-lookup"><span data-stu-id="f0070-690"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_string">IS_STRING (expr)</a></span></span></td>
  <td><span data-ttu-id="f0070-691">Zwraca wartość Boolean wskazującą, czy hello typ wartości hello jest ciąg.</span><span class="sxs-lookup"><span data-stu-id="f0070-691">Returns a Boolean indicating if hello type of hello value is a string.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="f0070-692"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_defined">IS_DEFINED (wyrażenie)</a></span><span class="sxs-lookup"><span data-stu-id="f0070-692"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_defined">IS_DEFINED (expr)</a></span></span></td>
  <td><span data-ttu-id="f0070-693">Zwraca wartość Boolean wskazującą, czy właściwość hello zostanie przypisana wartość.</span><span class="sxs-lookup"><span data-stu-id="f0070-693">Returns a Boolean indicating if hello property has been assigned a value.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="f0070-694"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_primitive">IS_PRIMITIVE (wyrażenie)</a></span><span class="sxs-lookup"><span data-stu-id="f0070-694"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_primitive">IS_PRIMITIVE (expr)</a></span></span></td>
  <td><span data-ttu-id="f0070-695">Zwraca wartość Boolean wskazującą, czy typ hello wartości hello jest ciąg, liczbę, Boolean lub wartość null.</span><span class="sxs-lookup"><span data-stu-id="f0070-695">Returns a Boolean indicating if hello type of hello value is a string, number, Boolean or null.</span></span></td>
</tr>

</table>

<span data-ttu-id="f0070-696">Przy użyciu tych funkcji, można teraz uruchomić zapytania, takie jak następujące hello:</span><span class="sxs-lookup"><span data-stu-id="f0070-696">Using these functions, you can now run queries like hello following:</span></span>

<span data-ttu-id="f0070-697">**Zapytanie**</span><span class="sxs-lookup"><span data-stu-id="f0070-697">**Query**</span></span>

    SELECT VALUE IS_NUMBER(-4)

<span data-ttu-id="f0070-698">**Wyniki**</span><span class="sxs-lookup"><span data-stu-id="f0070-698">**Results**</span></span>

    [true]

### <a name="string-functions"></a><span data-ttu-id="f0070-699">Funkcje ciągów</span><span class="sxs-lookup"><span data-stu-id="f0070-699">String functions</span></span>
<span data-ttu-id="f0070-700">Witaj następujące funkcje skalarne wykonania operacji w ciągu wartości wejściowej i zwraca ciąg, wartość liczbowa lub wartość logiczna.</span><span class="sxs-lookup"><span data-stu-id="f0070-700">hello following scalar functions perform an operation on a string input value and return a string, numeric or Boolean value.</span></span> <span data-ttu-id="f0070-701">W tym miejscu jest tabela funkcji wbudowanych ciągu:</span><span class="sxs-lookup"><span data-stu-id="f0070-701">Here's a table of built-in string functions:</span></span>

| <span data-ttu-id="f0070-702">Sposób użycia</span><span class="sxs-lookup"><span data-stu-id="f0070-702">Usage</span></span> | <span data-ttu-id="f0070-703">Opis</span><span class="sxs-lookup"><span data-stu-id="f0070-703">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="f0070-704">DŁUGOŚĆ (str_expr)</span><span class="sxs-lookup"><span data-stu-id="f0070-704">LENGTH (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_length) |<span data-ttu-id="f0070-705">Witaj zwraca liczbę znaków hello określone wyrażenie ciągu</span><span class="sxs-lookup"><span data-stu-id="f0070-705">Returns hello number of characters of hello specified string expression</span></span> |
| <span data-ttu-id="f0070-706">[CONCAT (str_expr, str_expr [, str_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_concat)</span><span class="sxs-lookup"><span data-stu-id="f0070-706">[CONCAT (str_expr, str_expr [, str_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_concat)</span></span> |<span data-ttu-id="f0070-707">Zwraca ciąg, który jest wynikiem hello łączenie dwóch lub więcej wartości ciągu.</span><span class="sxs-lookup"><span data-stu-id="f0070-707">Returns a string that is hello result of concatenating two or more string values.</span></span> |
| [<span data-ttu-id="f0070-708">SUBSTRING (str_expr, num_expr, num_expr)</span><span class="sxs-lookup"><span data-stu-id="f0070-708">SUBSTRING (str_expr, num_expr, num_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_substring) |<span data-ttu-id="f0070-709">Zwraca część wyrażenia ciągu.</span><span class="sxs-lookup"><span data-stu-id="f0070-709">Returns part of a string expression.</span></span> |
| [<span data-ttu-id="f0070-710">STARTSWITH (str_expr, str_expr)</span><span class="sxs-lookup"><span data-stu-id="f0070-710">STARTSWITH (str_expr, str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_startswith) |<span data-ttu-id="f0070-711">Zwraca wartość Boolean wskazującą, czy pierwsze wyrażenie ciąg hello kończy hello drugi</span><span class="sxs-lookup"><span data-stu-id="f0070-711">Returns a Boolean indicating whether hello first string expression ends with hello second</span></span> |
| [<span data-ttu-id="f0070-712">ENDSWITH (str_expr, str_expr)</span><span class="sxs-lookup"><span data-stu-id="f0070-712">ENDSWITH (str_expr, str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_endswith) |<span data-ttu-id="f0070-713">Zwraca wartość Boolean wskazującą, czy pierwsze wyrażenie ciąg hello kończy hello drugi</span><span class="sxs-lookup"><span data-stu-id="f0070-713">Returns a Boolean indicating whether hello first string expression ends with hello second</span></span> |
| [<span data-ttu-id="f0070-714">ZAWIERA (str_expr, str_expr)</span><span class="sxs-lookup"><span data-stu-id="f0070-714">CONTAINS (str_expr, str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_contains) |<span data-ttu-id="f0070-715">Zwraca wartość Boolean wskazującą, czy pierwsze wyrażenie ciąg hello drugi zawiera hello.</span><span class="sxs-lookup"><span data-stu-id="f0070-715">Returns a Boolean indicating whether hello first string expression contains hello second.</span></span> |
| [<span data-ttu-id="f0070-716">INDEX_OF (str_expr, str_expr)</span><span class="sxs-lookup"><span data-stu-id="f0070-716">INDEX_OF (str_expr, str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_index_of) |<span data-ttu-id="f0070-717">Zwraca hello uruchamianie pozycję pierwszego wystąpienia hello hello drugiego wyrażenia ciągu w obrębie hello pierwszy określonego wyrażenia ciągu lub wartość -1, jeśli nie zostanie znaleziony ciąg hello.</span><span class="sxs-lookup"><span data-stu-id="f0070-717">Returns hello starting position of hello first occurrence of hello second string expression within hello first specified string expression, or -1 if hello string is not found.</span></span> |
| [<span data-ttu-id="f0070-718">LEFT (str_expr, num_expr)</span><span class="sxs-lookup"><span data-stu-id="f0070-718">LEFT (str_expr, num_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_left) |<span data-ttu-id="f0070-719">Zwraca hello lewej części ciągu z hello określona liczba znaków.</span><span class="sxs-lookup"><span data-stu-id="f0070-719">Returns hello left part of a string with hello specified number of characters.</span></span> |
| [<span data-ttu-id="f0070-720">RIGHT (str_expr, num_expr)</span><span class="sxs-lookup"><span data-stu-id="f0070-720">RIGHT (str_expr, num_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_right) |<span data-ttu-id="f0070-721">Zwraca hello prawej części ciągu z hello określona liczba znaków.</span><span class="sxs-lookup"><span data-stu-id="f0070-721">Returns hello right part of a string with hello specified number of characters.</span></span> |
| [<span data-ttu-id="f0070-722">PRZYTP (str_expr)</span><span class="sxs-lookup"><span data-stu-id="f0070-722">LTRIM (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_ltrim) |<span data-ttu-id="f0070-723">Zwraca wyrażenie ciągu, po usuwa spacje wiodące.</span><span class="sxs-lookup"><span data-stu-id="f0070-723">Returns a string expression after it removes leading blanks.</span></span> |
| [<span data-ttu-id="f0070-724">PRZYTK (str_expr)</span><span class="sxs-lookup"><span data-stu-id="f0070-724">RTRIM (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_rtrim) |<span data-ttu-id="f0070-725">Zwraca wyrażenie ciągu po obcinanie wszystkie spacje końcowe.</span><span class="sxs-lookup"><span data-stu-id="f0070-725">Returns a string expression after truncating all trailing blanks.</span></span> |
| [<span data-ttu-id="f0070-726">MAŁE (str_expr)</span><span class="sxs-lookup"><span data-stu-id="f0070-726">LOWER (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_lower) |<span data-ttu-id="f0070-727">Zwraca wyrażenie ciągu po przekonwertowaniu toolowercase danych wielką literę.</span><span class="sxs-lookup"><span data-stu-id="f0070-727">Returns a string expression after converting uppercase character data toolowercase.</span></span> |
| [<span data-ttu-id="f0070-728">Górna (str_expr)</span><span class="sxs-lookup"><span data-stu-id="f0070-728">UPPER (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_upper) |<span data-ttu-id="f0070-729">Zwraca wyrażenie ciągu po przekonwertowaniu toouppercase danych małą literę.</span><span class="sxs-lookup"><span data-stu-id="f0070-729">Returns a string expression after converting lowercase character data toouppercase.</span></span> |
| [<span data-ttu-id="f0070-730">Zastąp (str_expr, str_expr, str_expr)</span><span class="sxs-lookup"><span data-stu-id="f0070-730">REPLACE (str_expr, str_expr, str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_replace) |<span data-ttu-id="f0070-731">Zamienia wszystkie wystąpienia określonej wartości ciągu na inną wartość ciągu.</span><span class="sxs-lookup"><span data-stu-id="f0070-731">Replaces all occurrences of a specified string value with another string value.</span></span> |
| [<span data-ttu-id="f0070-732">REPLIKACJA (str_expr, num_expr)</span><span class="sxs-lookup"><span data-stu-id="f0070-732">REPLICATE (str_expr, num_expr)</span></span>](https://docs.microsoft.com/azure/cosmos-db/documentdb-sql-query-reference#bk_replicate) |<span data-ttu-id="f0070-733">Wartość ciągu jest powtarzany określoną liczbę razy.</span><span class="sxs-lookup"><span data-stu-id="f0070-733">Repeats a string value a specified number of times.</span></span> |
| [<span data-ttu-id="f0070-734">REVERSE (str_expr)</span><span class="sxs-lookup"><span data-stu-id="f0070-734">REVERSE (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_reverse) |<span data-ttu-id="f0070-735">Zwraca hello odwrotna kolejność wartość ciągu.</span><span class="sxs-lookup"><span data-stu-id="f0070-735">Returns hello reverse order of a string value.</span></span> |

<span data-ttu-id="f0070-736">Przy użyciu tych funkcji, można teraz uruchomić zapytania, takie jak następujące hello.</span><span class="sxs-lookup"><span data-stu-id="f0070-736">Using these functions, you can now run queries like hello following.</span></span> <span data-ttu-id="f0070-737">Na przykład można zwrócić nazwę rodziny hello pisane wielkimi literami w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="f0070-737">For example, you can return hello family name in uppercase as follows:</span></span>

<span data-ttu-id="f0070-738">**Zapytanie**</span><span class="sxs-lookup"><span data-stu-id="f0070-738">**Query**</span></span>

    SELECT VALUE UPPER(Families.id)
    FROM Families

<span data-ttu-id="f0070-739">**Wyniki**</span><span class="sxs-lookup"><span data-stu-id="f0070-739">**Results**</span></span>

    [
        "WAKEFIELDFAMILY", 
        "ANDERSENFAMILY"
    ]

<span data-ttu-id="f0070-740">Lub ciągów podobnie jak w tym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="f0070-740">Or concatenate strings like in this example:</span></span>

<span data-ttu-id="f0070-741">**Zapytanie**</span><span class="sxs-lookup"><span data-stu-id="f0070-741">**Query**</span></span>

    SELECT Families.id, CONCAT(Families.address.city, ",", Families.address.state) AS location
    FROM Families

<span data-ttu-id="f0070-742">**Wyniki**</span><span class="sxs-lookup"><span data-stu-id="f0070-742">**Results**</span></span>

    [{
      "id": "WakefieldFamily",
      "location": "NY,NY"
    },
    {
      "id": "AndersenFamily",
      "location": "seattle,WA"
    }]


<span data-ttu-id="f0070-743">Funkcje ciągów można również w hello gdzie klauzuli toofilter wyników, podobnie jak w hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="f0070-743">String functions can also be used in hello WHERE clause toofilter results, like in hello following example:</span></span>

<span data-ttu-id="f0070-744">**Zapytanie**</span><span class="sxs-lookup"><span data-stu-id="f0070-744">**Query**</span></span>

    SELECT Families.id, Families.address.city
    FROM Families
    WHERE STARTSWITH(Families.id, "Wakefield")

<span data-ttu-id="f0070-745">**Wyniki**</span><span class="sxs-lookup"><span data-stu-id="f0070-745">**Results**</span></span>

    [{
      "id": "WakefieldFamily",
      "city": "NY"
    }]

### <a name="array-functions"></a><span data-ttu-id="f0070-746">Funkcje tablicy</span><span class="sxs-lookup"><span data-stu-id="f0070-746">Array functions</span></span>
<span data-ttu-id="f0070-747">następujące funkcje skalarne Hello wykonania operacji na tablicy wartości wejściowej i powrotu liczbowego, wartość logiczną lub tablicy.</span><span class="sxs-lookup"><span data-stu-id="f0070-747">hello following scalar functions perform an operation on an array input value and return numeric, Boolean or array value.</span></span> <span data-ttu-id="f0070-748">W tym miejscu jest tabela funkcji wbudowanej tablicy:</span><span class="sxs-lookup"><span data-stu-id="f0070-748">Here's a table of built-in array functions:</span></span>

| <span data-ttu-id="f0070-749">Sposób użycia</span><span class="sxs-lookup"><span data-stu-id="f0070-749">Usage</span></span> | <span data-ttu-id="f0070-750">Opis</span><span class="sxs-lookup"><span data-stu-id="f0070-750">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="f0070-751">ARRAY_LENGTH (arr_expr)</span><span class="sxs-lookup"><span data-stu-id="f0070-751">ARRAY_LENGTH (arr_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_length) |<span data-ttu-id="f0070-752">Zwraca numer hello elementów hello określone wyrażenie tablicy.</span><span class="sxs-lookup"><span data-stu-id="f0070-752">Returns hello number of elements of hello specified array expression.</span></span> |
| <span data-ttu-id="f0070-753">[ARRAY_CONCAT (arr_expr, arr_expr [, arr_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_concat)</span><span class="sxs-lookup"><span data-stu-id="f0070-753">[ARRAY_CONCAT (arr_expr, arr_expr [, arr_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_concat)</span></span> |<span data-ttu-id="f0070-754">Zwraca tablicę, która jest wynikiem hello łączenie dwóch lub więcej wartości tablicy.</span><span class="sxs-lookup"><span data-stu-id="f0070-754">Returns an array that is hello result of concatenating two or more array values.</span></span> |
| <span data-ttu-id="f0070-755">[ARRAY_CONTAINS (arr_expr, wyrażenie [, bool_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_contains)</span><span class="sxs-lookup"><span data-stu-id="f0070-755">[ARRAY_CONTAINS (arr_expr, expr [, bool_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_contains)</span></span> |<span data-ttu-id="f0070-756">Zwraca wartość typu Boolean wskazującą, czy tablica hello zawiera hello określona wartość.</span><span class="sxs-lookup"><span data-stu-id="f0070-756">Returns a Boolean indicating whether hello array contains hello specified value.</span></span> <span data-ttu-id="f0070-757">Można określić, czy dopasowanie hello jest pełnej lub częściowej.</span><span class="sxs-lookup"><span data-stu-id="f0070-757">Can specify if hello match is full or partial.</span></span> |
| <span data-ttu-id="f0070-758">[ARRAY_SLICE (arr_expr, num_expr [, num_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_slice)</span><span class="sxs-lookup"><span data-stu-id="f0070-758">[ARRAY_SLICE (arr_expr, num_expr [, num_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_slice)</span></span> |<span data-ttu-id="f0070-759">Zwraca część wyrażenie tablicy.</span><span class="sxs-lookup"><span data-stu-id="f0070-759">Returns part of an array expression.</span></span> |

<span data-ttu-id="f0070-760">Funkcje tablicy mogą być używane toomanipulate tablice w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="f0070-760">Array functions can be used toomanipulate arrays within JSON.</span></span> <span data-ttu-id="f0070-761">Na przykład w tym miejscu jest kwerendę, która zwraca wszystkie dokumenty, gdy jeden z elementów nadrzędnych hello jest "Działania okrężnego Wakefield".</span><span class="sxs-lookup"><span data-stu-id="f0070-761">For example, here's a query that returns all documents where one of hello parents is "Robin Wakefield".</span></span> 

<span data-ttu-id="f0070-762">**Zapytanie**</span><span class="sxs-lookup"><span data-stu-id="f0070-762">**Query**</span></span>

    SELECT Families.id 
    FROM Families 
    WHERE ARRAY_CONTAINS(Families.parents, { givenName: "Robin", familyName: "Wakefield" })

<span data-ttu-id="f0070-763">**Wyniki**</span><span class="sxs-lookup"><span data-stu-id="f0070-763">**Results**</span></span>

    [{
      "id": "WakefieldFamily"
    }]

<span data-ttu-id="f0070-764">Można określić częściowego fragmentu dla zgodnych elementów w tablicy hello.</span><span class="sxs-lookup"><span data-stu-id="f0070-764">You can specify a partial fragment for matching elements within hello array.</span></span> <span data-ttu-id="f0070-765">Witaj następujące zapytanie znajdzie wszystkich elementów nadrzędnych z hello `givenName` z `Robin`.</span><span class="sxs-lookup"><span data-stu-id="f0070-765">hello following query finds all parents with hello `givenName` of `Robin`.</span></span>

<span data-ttu-id="f0070-766">**Zapytanie**</span><span class="sxs-lookup"><span data-stu-id="f0070-766">**Query**</span></span>

    SELECT Families.id 
    FROM Families 
    WHERE ARRAY_CONTAINS(Families.parents, { givenName: "Robin" }, true)

<span data-ttu-id="f0070-767">**Wyniki**</span><span class="sxs-lookup"><span data-stu-id="f0070-767">**Results**</span></span>

    [{
      "id": "WakefieldFamily"
    }]


<span data-ttu-id="f0070-768">Oto przykład innego, który używa ARRAY_LENGTH tooget hello liczbę elementów podrzędnych na rodzinę.</span><span class="sxs-lookup"><span data-stu-id="f0070-768">Here's another example that uses ARRAY_LENGTH tooget hello number of children per family.</span></span>

<span data-ttu-id="f0070-769">**Zapytanie**</span><span class="sxs-lookup"><span data-stu-id="f0070-769">**Query**</span></span>

    SELECT Families.id, ARRAY_LENGTH(Families.children) AS numberOfChildren
    FROM Families 

<span data-ttu-id="f0070-770">**Wyniki**</span><span class="sxs-lookup"><span data-stu-id="f0070-770">**Results**</span></span>

    [{
      "id": "WakefieldFamily",
      "numberOfChildren": 2
    },
    {
      "id": "AndersenFamily",
      "numberOfChildren": 1
    }]

### <a name="spatial-functions"></a><span data-ttu-id="f0070-771">Funkcje przestrzenne</span><span class="sxs-lookup"><span data-stu-id="f0070-771">Spatial functions</span></span>
<span data-ttu-id="f0070-772">Rozwiązania cosmos bazy danych obsługuje następujące funkcje wbudowane Otwórz geograficzne konsorcjum (OGC) na potrzeby zapytań o dane geograficzne hello.</span><span class="sxs-lookup"><span data-stu-id="f0070-772">Cosmos DB supports hello following Open Geospatial Consortium (OGC) built-in functions for geospatial querying.</span></span> 

<table>
<tr>
  <td><span data-ttu-id="f0070-773"><strong>Użycie</strong></span><span class="sxs-lookup"><span data-stu-id="f0070-773"><strong>Usage</strong></span></span></td>
  <td><span data-ttu-id="f0070-774"><strong>Opis</strong></span><span class="sxs-lookup"><span data-stu-id="f0070-774"><strong>Description</strong></span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="f0070-775">ST_DISTANCE (point_expr, point_expr)</span><span class="sxs-lookup"><span data-stu-id="f0070-775">ST_DISTANCE (point_expr, point_expr)</span></span></td>
  <td><span data-ttu-id="f0070-776">Zwraca hello odległość między hello dwóch wyrażeń GeoJSON punktu wielokąta i LineString.</span><span class="sxs-lookup"><span data-stu-id="f0070-776">Returns hello distance between hello two GeoJSON Point, Polygon, or LineString expressions.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="f0070-777">ST_WITHIN (point_expr, polygon_expr)</span><span class="sxs-lookup"><span data-stu-id="f0070-777">ST_WITHIN (point_expr, polygon_expr)</span></span></td>
  <td><span data-ttu-id="f0070-778">Zwraca wyrażenie logiczne, wskazującą, czy hello pierwszego obiektu GeoJSON (punkt, wielokąta lub LineString) jest w obrębie hello drugiego obiektu GeoJSON (punkt, wielokąta lub LineString).</span><span class="sxs-lookup"><span data-stu-id="f0070-778">Returns a Boolean expression indicating whether hello first GeoJSON object (Point, Polygon, or LineString) is within hello second GeoJSON object (Point, Polygon, or LineString).</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="f0070-779">ST_INTERSECTS (spatial_expr, spatial_expr)</span><span class="sxs-lookup"><span data-stu-id="f0070-779">ST_INTERSECTS (spatial_expr, spatial_expr)</span></span></td>
  <td><span data-ttu-id="f0070-780">Zwraca wyrażenie logiczne, wskazującą, czy intersect hello dwóch określonych GeoJSON obiektów (punkt, wielokąta lub LineString).</span><span class="sxs-lookup"><span data-stu-id="f0070-780">Returns a Boolean expression indicating whether hello two specified GeoJSON objects (Point, Polygon, or LineString) intersect.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="f0070-781">ST_ISVALID</span><span class="sxs-lookup"><span data-stu-id="f0070-781">ST_ISVALID</span></span></td>
  <td><span data-ttu-id="f0070-782">Zwraca wartość logiczną wskazującą, czy określono hello wyrażenie GeoJSON punktu wielokąta i LineString jest nieprawidłowy.</span><span class="sxs-lookup"><span data-stu-id="f0070-782">Returns a Boolean value indicating whether hello specified GeoJSON Point, Polygon, or LineString expression is valid.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="f0070-783">ST_ISVALIDDETAILED</span><span class="sxs-lookup"><span data-stu-id="f0070-783">ST_ISVALIDDETAILED</span></span></td>
  <td><span data-ttu-id="f0070-784">Zwraca wartość JSON zawierający wartość logiczna, jeśli hello określone wyrażenie GeoJSON punktu wielokąta i LineString jest prawidłowy, a jeśli jest nieprawidłowy, ponadto hello Przyczyna jako wartość typu ciąg.</span><span class="sxs-lookup"><span data-stu-id="f0070-784">Returns a JSON value containing a Boolean value if hello specified GeoJSON Point, Polygon, or LineString expression is valid, and if invalid, additionally hello reason as a string value.</span></span></td>
</tr>
</table>

<span data-ttu-id="f0070-785">Funkcje przestrzenne mogą być używane tooperform zbliżeniowe zapytań dotyczących danych przestrzennych.</span><span class="sxs-lookup"><span data-stu-id="f0070-785">Spatial functions can be used tooperform proximity queries against spatial data.</span></span> <span data-ttu-id="f0070-786">Na przykład w tym miejscu jest kwerendę, która zwraca rodziny wszystkie dokumenty, czy są w ciągu 30 km hello określonej lokalizacji przy użyciu wbudowanych funkcji ST_DISTANCE hello.</span><span class="sxs-lookup"><span data-stu-id="f0070-786">For example, here's a query that returns all family documents that are within 30 km of hello specified location using hello ST_DISTANCE built-in function.</span></span> 

<span data-ttu-id="f0070-787">**Zapytanie**</span><span class="sxs-lookup"><span data-stu-id="f0070-787">**Query**</span></span>

    SELECT f.id 
    FROM Families f 
    WHERE ST_DISTANCE(f.location, {'type': 'Point', 'coordinates':[31.9, -4.8]}) < 30000

<span data-ttu-id="f0070-788">**Wyniki**</span><span class="sxs-lookup"><span data-stu-id="f0070-788">**Results**</span></span>

    [{
      "id": "WakefieldFamily"
    }]

<span data-ttu-id="f0070-789">Aby uzyskać więcej informacji dotyczących obsługi dane geograficzne do rozwiązania Cosmos bazy danych, zobacz [Praca z dane geograficzne w usłudze Azure DB rozwiązania Cosmos](geospatial.md).</span><span class="sxs-lookup"><span data-stu-id="f0070-789">For more details on geospatial support in Cosmos DB, please see [Working with geospatial data in Azure Cosmos DB](geospatial.md).</span></span> <span data-ttu-id="f0070-790">Który koduje funkcje przestrzenne i hello składni SQL DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="f0070-790">That wraps up spatial functions, and hello SQL syntax for Cosmos DB.</span></span> <span data-ttu-id="f0070-791">Teraz Spójrzmy na jak LINQ zapytań działa i jak współdziała ze składnią hello możemy w tym samouczku wykonanej do tej pory.</span><span class="sxs-lookup"><span data-stu-id="f0070-791">Now let's take a look at how LINQ querying works and how it interacts with hello syntax we've seen so far.</span></span>

## <span data-ttu-id="f0070-792"><a id="Linq"></a>LINQ tooDocumentDB interfejsu API SQL</span><span class="sxs-lookup"><span data-stu-id="f0070-792"><a id="Linq"></a>LINQ tooDocumentDB API SQL</span></span>
<span data-ttu-id="f0070-793">LINQ jest model programowania .NET określającym obliczeń jako kwerendy dla strumieni obiektów.</span><span class="sxs-lookup"><span data-stu-id="f0070-793">LINQ is a .NET programming model that expresses computation as queries on streams of objects.</span></span> <span data-ttu-id="f0070-794">Rozwiązania cosmos DB zapewnia toointerface biblioteki po stronie klienta, za pomocą LINQ ułatwiając konwersji między obiektami JSON i .NET i mapowanie z podzbioru LINQ kwerendy kwerendy tooCosmos bazy danych.</span><span class="sxs-lookup"><span data-stu-id="f0070-794">Cosmos DB provides a client-side library toointerface with LINQ by facilitating a conversion between JSON and .NET objects and a mapping from a subset of LINQ queries tooCosmos DB queries.</span></span> 

<span data-ttu-id="f0070-795">Obraz powitania poniżej przedstawiono architekturę hello obsługi zapytań LINQ przy użyciu rozwiązania Cosmos bazy danych.</span><span class="sxs-lookup"><span data-stu-id="f0070-795">hello picture below shows hello architecture of supporting LINQ queries using Cosmos DB.</span></span>  <span data-ttu-id="f0070-796">Za pomocą powitania klienta rozwiązania Cosmos bazy danych, deweloperzy mogą tworzyć **IQueryable** obiektów, że bezpośrednio zapytania hello DB rozwiązania Cosmos zapytanie do dostawcy, który następnie tłumaczy zapytania LINQ hello na zapytanie DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="f0070-796">Using hello Cosmos DB client, developers can create an **IQueryable** object that directly queries hello Cosmos DB query provider, which then translates hello LINQ query into a Cosmos DB query.</span></span> <span data-ttu-id="f0070-797">Zapytanie Hello są następnie przekazywane toohello tooretrieve serwera bazy danych rozwiązania Cosmos zestaw wyników w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="f0070-797">hello query is then passed toohello Cosmos DB server tooretrieve a set of results in JSON format.</span></span> <span data-ttu-id="f0070-798">Witaj zwracane wyniki są zdeserializowany do strumienia obiektów .NET na powitania po stronie klienta.</span><span class="sxs-lookup"><span data-stu-id="f0070-798">hello returned results are deserialized into a stream of .NET objects on hello client side.</span></span>

![Architektura obsługi zapytań LINQ przy użyciu interfejsu API usługi DocumentDB — składnia SQL, język zapytań JSON pojęcia bazy danych i zapytania SQL][1]

### <a name="net-and-json-mapping"></a><span data-ttu-id="f0070-800">Mapowanie JSON i .NET</span><span class="sxs-lookup"><span data-stu-id="f0070-800">.NET and JSON mapping</span></span>
<span data-ttu-id="f0070-801">Hello mapowania między obiektami .NET i dokumentów JSON jest naturalna — każdego pola elementu członkowskiego danych jest mapowany tooa obiekt JSON, których nazwa pola hello jest zamapowany toohello "klucz" część obiektu hello i części "value" hello jest zamapowany rekursywnie toohello wartość częścią hello obiektu.</span><span class="sxs-lookup"><span data-stu-id="f0070-801">hello mapping between .NET objects and JSON documents is natural - each data member field is mapped tooa JSON object, where hello field name is mapped toohello "key" part of hello object and hello "value" part is recursively mapped toohello value part of hello object.</span></span> <span data-ttu-id="f0070-802">Należy wziąć pod uwagę hello poniższy przykład: hello rodziny obiektu utworzonego jest mapowane toohello dokument JSON w sposób przedstawiony poniżej.</span><span class="sxs-lookup"><span data-stu-id="f0070-802">Consider hello following example: hello Family object created is mapped toohello JSON document as shown below.</span></span> <span data-ttu-id="f0070-803">I odwrotnie, hello dokumentu JSON jest mapowane tooa zapasowego obiektu .NET.</span><span class="sxs-lookup"><span data-stu-id="f0070-803">And vice versa, hello JSON document is mapped back tooa .NET object.</span></span>

<span data-ttu-id="f0070-804">**Klasa C#**</span><span class="sxs-lookup"><span data-stu-id="f0070-804">**C# Class**</span></span>

    public class Family
    {
        [JsonProperty(PropertyName="id")]
        public string Id;
        public Parent[] parents;
        public Child[] children;
        public bool isRegistered;
    };

    public struct Parent
    {
        public string familyName;
        public string givenName;
    };

    public class Child
    {
        public string familyName;
        public string givenName;
        public string gender;
        public int grade;
        public List<Pet> pets;
    };

    public class Pet
    {
        public string givenName;
    };

    public class Address
    {
        public string state;
        public string county;
        public string city;
    };

    // Create a Family object.
    Parent mother = new Parent { familyName= "Wakefield", givenName="Robin" };
    Parent father = new Parent { familyName = "Miller", givenName = "Ben" };
    Child child = new Child { familyName="Merriam", givenName="Jesse", gender="female", grade=1 };
    Pet pet = new Pet { givenName = "Fluffy" };
    Address address = new Address { state = "NY", county = "Manhattan", city = "NY" };
    Family family = new Family { Id = "WakefieldFamily", parents = new Parent [] { mother, father}, children = new Child[] { child }, isRegistered = false };


<span data-ttu-id="f0070-805">**JSON**</span><span class="sxs-lookup"><span data-stu-id="f0070-805">**JSON**</span></span>  

    {
        "id": "WakefieldFamily",
        "parents": [
            { "familyName": "Wakefield", "givenName": "Robin" },
            { "familyName": "Miller", "givenName": "Ben" }
        ],
        "children": [
            {
                "familyName": "Merriam", 
                "givenName": "Jesse", 
                "gender": "female", 
                "grade": 1,
                "pets": [
                    { "givenName": "Goofy" },
                    { "givenName": "Shadow" }
                ]
            },
            { 
              "familyName": "Miller", 
              "givenName": "Lisa", 
              "gender": "female", 
              "grade": 8 
            }
        ],
        "address": { "state": "NY", "county": "Manhattan", "city": "NY" },
        "isRegistered": false
    };



### <a name="linq-toosql-translation"></a><span data-ttu-id="f0070-806">Tłumaczenie tooSQL LINQ</span><span class="sxs-lookup"><span data-stu-id="f0070-806">LINQ tooSQL translation</span></span>
<span data-ttu-id="f0070-807">Hello DB rozwiązania Cosmos zapytanie do dostawcy wykonuje najlepsze mapowania nakładu pracy w wyniku zapytania LINQ do zapytania rozwiązania Cosmos bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="f0070-807">hello Cosmos DB query provider performs a best effort mapping from a LINQ query into a Cosmos DB SQL query.</span></span> <span data-ttu-id="f0070-808">W następujących opis hello przyjęto założenie, że czytnik hello ma podstawowe znajomości LINQ.</span><span class="sxs-lookup"><span data-stu-id="f0070-808">In hello following description, we assume hello reader has a basic familiarity of LINQ.</span></span>

<span data-ttu-id="f0070-809">Najpierw hello typu systemu obsługujemy JSON pierwotne typy — typy liczbowe, boolean, typ string i wartości null.</span><span class="sxs-lookup"><span data-stu-id="f0070-809">First, for hello type system, we support all JSON primitive types – numeric types, boolean, string, and null.</span></span> <span data-ttu-id="f0070-810">Obsługiwane są tylko te typy JSON.</span><span class="sxs-lookup"><span data-stu-id="f0070-810">Only these JSON types are supported.</span></span> <span data-ttu-id="f0070-811">Witaj następującego wyrażenia skalarne są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="f0070-811">hello following scalar expressions are supported.</span></span>

* <span data-ttu-id="f0070-812">Wartości stałe — należą do stałej wartości typów pierwotnych danych hello w czasie hello hello zapytania.</span><span class="sxs-lookup"><span data-stu-id="f0070-812">Constant values – these include constant values of hello primitive data types at hello time hello query is evaluated.</span></span>
* <span data-ttu-id="f0070-813">Wyrażenia indeksu tablicy/właściwości — tych wyrażeń odwołuje się właściwość toohello obiektu lub elementu tablicy.</span><span class="sxs-lookup"><span data-stu-id="f0070-813">Property/array index expressions – these expressions refer toohello property of an object or an array element.</span></span>
  
     <span data-ttu-id="f0070-814">rodziny. Identyfikator;    Family.Children[0].familyName;    Family.Children[0].Grade;    Family.Children[n].Grade; n jest zmienną int</span><span class="sxs-lookup"><span data-stu-id="f0070-814">family.Id;    family.children[0].familyName;    family.children[0].grade;    family.children[n].grade; //n is an int variable</span></span>
* <span data-ttu-id="f0070-815">Wyrażenia arytmetyczne - obejmują one wspólnych wyrażeniach arytmetycznych na wartościach wartości liczbowych i logicznych.</span><span class="sxs-lookup"><span data-stu-id="f0070-815">Arithmetic expressions - These include common arithmetic expressions on numerical and boolean values.</span></span> <span data-ttu-id="f0070-816">Hello pełną listę można znaleźć w specyfikacji SQL toohello.</span><span class="sxs-lookup"><span data-stu-id="f0070-816">For hello complete list, refer toohello SQL specification.</span></span>
  
     <span data-ttu-id="f0070-817">2 * family.children[0].grade;    x + y;</span><span class="sxs-lookup"><span data-stu-id="f0070-817">2 * family.children[0].grade;    x + y;</span></span>
* <span data-ttu-id="f0070-818">Wyrażenia porównanie ciągu - należą do porównywania wartości stałej ciągu toosome wartość ciągu.</span><span class="sxs-lookup"><span data-stu-id="f0070-818">String comparison expression - these include comparing a string value toosome constant string value.</span></span>  
  
     <span data-ttu-id="f0070-819">mother.familyName == "Smith";    child.givenName == s; s jest zmienną ciągu</span><span class="sxs-lookup"><span data-stu-id="f0070-819">mother.familyName == "Smith";    child.givenName == s; //s is a string variable</span></span>
* <span data-ttu-id="f0070-820">/ Tablicę obiektów wyrażeniem tworzenia - tych wyrażeń zwracanego obiektu złożonego wartość lub anonimowy typ lub tablicę takie obiekty.</span><span class="sxs-lookup"><span data-stu-id="f0070-820">Object/array creation expression - these expressions return an object of compound value type or anonymous type or an array of such objects.</span></span> <span data-ttu-id="f0070-821">Te wartości mogą być zagnieżdżone.</span><span class="sxs-lookup"><span data-stu-id="f0070-821">These values can be nested.</span></span>
  
     <span data-ttu-id="f0070-822">nadrzędną {familyName = "Smith" givenName = "Jan"}; New {najpierw = 1, drugi = 2;} Typ anonimowy z dwóch pól</span><span class="sxs-lookup"><span data-stu-id="f0070-822">new Parent { familyName = "Smith", givenName = "Joe" }; new { first = 1, second = 2 }; //an anonymous type with two fields</span></span>              
     <span data-ttu-id="f0070-823">Nowy int [] {3, child.grade, 5};</span><span class="sxs-lookup"><span data-stu-id="f0070-823">new int[] { 3, child.grade, 5 };</span></span>

### <span data-ttu-id="f0070-824"><a id="SupportedLinqOperators"></a>Lista obsługiwanych operatorów LINQ</span><span class="sxs-lookup"><span data-stu-id="f0070-824"><a id="SupportedLinqOperators"></a>List of supported LINQ operators</span></span>
<span data-ttu-id="f0070-825">Poniżej przedstawiono listę obsługiwanych operatorów LINQ hello LINQ dostawcy dołączonego hello zestawu SDK .NET usługi DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="f0070-825">Here is a list of supported LINQ operators in hello LINQ provider included with hello DocumentDB .NET SDK.</span></span>

* <span data-ttu-id="f0070-826">**Wybierz**: projekcje tłumaczenie toohello SQL SELECT, łącznie z konstrukcji obiektów</span><span class="sxs-lookup"><span data-stu-id="f0070-826">**Select**: Projections translate toohello SQL SELECT including object construction</span></span>
* <span data-ttu-id="f0070-827">**Gdzie**: filtry Przetłumacz toohello SQL WHERE i translacja między obsługuje & &, || i!</span><span class="sxs-lookup"><span data-stu-id="f0070-827">**Where**: Filters translate toohello SQL WHERE, and support translation between && , || and !</span></span> <span data-ttu-id="f0070-828">Operatory SQL toohello</span><span class="sxs-lookup"><span data-stu-id="f0070-828">toohello SQL operators</span></span>
* <span data-ttu-id="f0070-829">**Operacja SelectMany**: umożliwia rozwinięcia klauzuli SQL JOIN toohello tablic.</span><span class="sxs-lookup"><span data-stu-id="f0070-829">**SelectMany**: Allows unwinding of arrays toohello SQL JOIN clause.</span></span> <span data-ttu-id="f0070-830">Może być używane toochain/zagnieżdżania toofilter wyrażenia na elementów tablicy</span><span class="sxs-lookup"><span data-stu-id="f0070-830">Can be used toochain/nest expressions toofilter on array elements</span></span>
* <span data-ttu-id="f0070-831">**OrderBy i OrderByDescending**: tłumaczy tooORDER BY rosnąco/malejąco</span><span class="sxs-lookup"><span data-stu-id="f0070-831">**OrderBy and OrderByDescending**: Translates tooORDER BY ascending/descending</span></span>
* <span data-ttu-id="f0070-832">**Liczba**, **suma**, **Min**, **Max**, i **średni** operatory do agregacji i ich odpowiedniki async **CountAsync**, **SumAsync**, **MinAsync**, **MaxAsync**, i **AverageAsync**.</span><span class="sxs-lookup"><span data-stu-id="f0070-832">**Count**, **Sum**, **Min**, **Max**, and **Average** operators for aggregation, and their async equivalents **CountAsync**, **SumAsync**, **MinAsync**, **MaxAsync**, and **AverageAsync**.</span></span>
* <span data-ttu-id="f0070-833">**Wykonanie funkcji CompareTo**: tłumaczy toorange porównania.</span><span class="sxs-lookup"><span data-stu-id="f0070-833">**CompareTo**: Translates toorange comparisons.</span></span> <span data-ttu-id="f0070-834">Często używane dla ciągów, ponieważ nie są one porównywalne w .NET</span><span class="sxs-lookup"><span data-stu-id="f0070-834">Commonly used for strings since they’re not comparable in .NET</span></span>
* <span data-ttu-id="f0070-835">**Podejmij**: tłumaczy toohello GÓRNEJ SQL ograniczania wyników kwerendy</span><span class="sxs-lookup"><span data-stu-id="f0070-835">**Take**: Translates toohello SQL TOP for limiting results from a query</span></span>
* <span data-ttu-id="f0070-836">**Funkcje matematyczne**: obsługuje translację. Asin Abs, Acos, przez sieć, Atan Ceiling Cos Exp, Floor, Log10, Pow, Round, logowania, Sin, dziennika Sqrt, Tan, Truncate równoważne funkcje wbudowane toohello SQL.</span><span class="sxs-lookup"><span data-stu-id="f0070-836">**Math Functions**: Supports translation from .NET’s Abs, Acos, Asin, Atan, Ceiling, Cos, Exp, Floor, Log, Log10, Pow, Round, Sign, Sin, Sqrt, Tan, Truncate toohello equivalent SQL built-in functions.</span></span>
* <span data-ttu-id="f0070-837">**Ciąg funkcji**: obsługuje translację. EndsWith Concat, zawiera, w sieci, IndexOf, Count, ToLower, TrimStart, Zamień, wstecznego, TrimEnd, StartsWith, SubString, ToUpper toohello równoważne SQL funkcji wbudowanych.</span><span class="sxs-lookup"><span data-stu-id="f0070-837">**String Functions**: Supports translation from .NET’s Concat, Contains, EndsWith, IndexOf, Count, ToLower, TrimStart, Replace, Reverse, TrimEnd, StartsWith, SubString, ToUpper toohello equivalent SQL built-in functions.</span></span>
* <span data-ttu-id="f0070-838">**Tablica funkcji**: obsługuje translację. W sieci Concat, zawierający i liczba toohello równoważne SQL funkcji wbudowanych.</span><span class="sxs-lookup"><span data-stu-id="f0070-838">**Array Functions**: Supports translation from .NET’s Concat, Contains, and Count toohello equivalent SQL built-in functions.</span></span>
* <span data-ttu-id="f0070-839">**Funkcje rozszerzeń dane geograficzne**: obsługuje translację szkieletu metody odległości w IsValid i IsValidDetailed toohello równoważne wbudowanych funkcji SQL.</span><span class="sxs-lookup"><span data-stu-id="f0070-839">**Geospatial Extension Functions**: Supports translation from stub methods Distance, Within, IsValid, and IsValidDetailed toohello equivalent SQL built-in functions.</span></span>
* <span data-ttu-id="f0070-840">**Zdefiniowane przez użytkownika funkcji rozszerzenia funkcji**: obsługuje translację hello stub metody UserDefinedFunctionProvider.Invoke toohello odpowiedni zdefiniowanej przez użytkownika funkcji.</span><span class="sxs-lookup"><span data-stu-id="f0070-840">**User-Defined Function Extension Function**: Supports translation from hello stub method UserDefinedFunctionProvider.Invoke toohello corresponding user-defined function.</span></span>
* <span data-ttu-id="f0070-841">**Różne**: obsługuje łączonych tłumaczenia hello i operatory warunkowe.</span><span class="sxs-lookup"><span data-stu-id="f0070-841">**Miscellaneous**: Supports translation of hello coalesce and conditional operators.</span></span> <span data-ttu-id="f0070-842">Może dokonywać translacji tooString zawiera CONTAINS, ARRAY_CONTAINS lub hello SQL IN, w zależności od kontekstu.</span><span class="sxs-lookup"><span data-stu-id="f0070-842">Can translate Contains tooString CONTAINS, ARRAY_CONTAINS, or hello SQL IN depending on context.</span></span>

### <a name="sql-query-operators"></a><span data-ttu-id="f0070-843">Operatory kwerend SQL</span><span class="sxs-lookup"><span data-stu-id="f0070-843">SQL query operators</span></span>
<span data-ttu-id="f0070-844">Oto przykłady ilustrujące sposobu niektóre hello standardowych operatorów zapytań LINQ przekształcania dół tooCosmos kwerendy bazy danych.</span><span class="sxs-lookup"><span data-stu-id="f0070-844">Here are some examples that illustrate how some of hello standard LINQ query operators are translated down tooCosmos DB queries.</span></span>

#### <a name="select-operator"></a><span data-ttu-id="f0070-845">SELECT — Operator</span><span class="sxs-lookup"><span data-stu-id="f0070-845">Select Operator</span></span>
<span data-ttu-id="f0070-846">Składnia Hello jest `input.Select(x => f(x))`, gdzie `f` jest wyrażenie skalarne.</span><span class="sxs-lookup"><span data-stu-id="f0070-846">hello syntax is `input.Select(x => f(x))`, where `f` is a scalar expression.</span></span>

<span data-ttu-id="f0070-847">**Wyrażenie lambda LINQ**</span><span class="sxs-lookup"><span data-stu-id="f0070-847">**LINQ lambda expression**</span></span>

    input.Select(family => family.parents[0].familyName);

<span data-ttu-id="f0070-848">**SQL**</span><span class="sxs-lookup"><span data-stu-id="f0070-848">**SQL**</span></span> 

    SELECT VALUE f.parents[0].familyName
    FROM Families f



<span data-ttu-id="f0070-849">**Wyrażenie lambda LINQ**</span><span class="sxs-lookup"><span data-stu-id="f0070-849">**LINQ lambda expression**</span></span>

    input.Select(family => family.children[0].grade + c); // c is an int variable


<span data-ttu-id="f0070-850">**SQL**</span><span class="sxs-lookup"><span data-stu-id="f0070-850">**SQL**</span></span> 

    SELECT VALUE f.children[0].grade + c
    FROM Families f 



<span data-ttu-id="f0070-851">**Wyrażenie lambda LINQ**</span><span class="sxs-lookup"><span data-stu-id="f0070-851">**LINQ lambda expression**</span></span>

    input.Select(family => new
    {
        name = family.children[0].familyName,
        grade = family.children[0].grade + 3
    });


<span data-ttu-id="f0070-852">**SQL**</span><span class="sxs-lookup"><span data-stu-id="f0070-852">**SQL**</span></span> 

    SELECT VALUE {"name":f.children[0].familyName, 
                  "grade": f.children[0].grade + 3 }
    FROM Families f



#### <a name="selectmany-operator"></a><span data-ttu-id="f0070-853">Operacja SelectMany — operator</span><span class="sxs-lookup"><span data-stu-id="f0070-853">SelectMany operator</span></span>
<span data-ttu-id="f0070-854">Składnia Hello jest `input.SelectMany(x => f(x))`, gdzie `f` jest wyrażenie skalarne, który zwraca typ kolekcji.</span><span class="sxs-lookup"><span data-stu-id="f0070-854">hello syntax is `input.SelectMany(x => f(x))`, where `f` is a scalar expression that returns a collection type.</span></span>

<span data-ttu-id="f0070-855">**Wyrażenie lambda LINQ**</span><span class="sxs-lookup"><span data-stu-id="f0070-855">**LINQ lambda expression**</span></span>

    input.SelectMany(family => family.children);

<span data-ttu-id="f0070-856">**SQL**</span><span class="sxs-lookup"><span data-stu-id="f0070-856">**SQL**</span></span> 

    SELECT VALUE child
    FROM child IN Families.children



#### <a name="where-operator"></a><span data-ttu-id="f0070-857">Gdy operator</span><span class="sxs-lookup"><span data-stu-id="f0070-857">Where operator</span></span>
<span data-ttu-id="f0070-858">Składnia Hello jest `input.Where(x => f(x))`, gdzie `f` jest wyrażenie skalarne, która zwraca wartość logiczną.</span><span class="sxs-lookup"><span data-stu-id="f0070-858">hello syntax is `input.Where(x => f(x))`, where `f` is a scalar expression, which returns a Boolean value.</span></span>

<span data-ttu-id="f0070-859">**Wyrażenie lambda LINQ**</span><span class="sxs-lookup"><span data-stu-id="f0070-859">**LINQ lambda expression**</span></span>

    input.Where(family=> family.parents[0].familyName == "Smith");

<span data-ttu-id="f0070-860">**SQL**</span><span class="sxs-lookup"><span data-stu-id="f0070-860">**SQL**</span></span> 

    SELECT *
    FROM Families f
    WHERE f.parents[0].familyName = "Smith" 



<span data-ttu-id="f0070-861">**Wyrażenie lambda LINQ**</span><span class="sxs-lookup"><span data-stu-id="f0070-861">**LINQ lambda expression**</span></span>

    input.Where(
        family => family.parents[0].familyName == "Smith" && 
        family.children[0].grade < 3);

<span data-ttu-id="f0070-862">**SQL**</span><span class="sxs-lookup"><span data-stu-id="f0070-862">**SQL**</span></span> 

    SELECT *
    FROM Families f
    WHERE f.parents[0].familyName = "Smith"
    AND f.children[0].grade < 3


### <a name="composite-sql-queries"></a><span data-ttu-id="f0070-863">Złożonego zapytania SQL</span><span class="sxs-lookup"><span data-stu-id="f0070-863">Composite SQL queries</span></span>
<span data-ttu-id="f0070-864">Witaj powyżej operatory tooform złożona, może być bardziej zaawansowanych zapytań.</span><span class="sxs-lookup"><span data-stu-id="f0070-864">hello above operators can be composed tooform more powerful queries.</span></span> <span data-ttu-id="f0070-865">Ponieważ DB rozwiązania Cosmos obsługuje zagnieżdżonych kolekcje, hello kompozycji można być połączonych lub zagnieżdżone.</span><span class="sxs-lookup"><span data-stu-id="f0070-865">Since Cosmos DB supports nested collections, hello composition can either be concatenated or nested.</span></span>

#### <a name="concatenation"></a><span data-ttu-id="f0070-866">Łączenie</span><span class="sxs-lookup"><span data-stu-id="f0070-866">Concatenation</span></span>
<span data-ttu-id="f0070-867">Składnia Hello jest `input(.|.SelectMany())(.Select()|.Where())*`.</span><span class="sxs-lookup"><span data-stu-id="f0070-867">hello syntax is `input(.|.SelectMany())(.Select()|.Where())*`.</span></span> <span data-ttu-id="f0070-868">Połączonych zapytanie można uruchomić z opcjonalną `SelectMany` query następuje wielu `Select` lub `Where` operatorów.</span><span class="sxs-lookup"><span data-stu-id="f0070-868">A concatenated query can start with an optional `SelectMany` query followed by multiple `Select` or `Where` operators.</span></span>

<span data-ttu-id="f0070-869">**Wyrażenie lambda LINQ**</span><span class="sxs-lookup"><span data-stu-id="f0070-869">**LINQ lambda expression**</span></span>

    input.Select(family=>family.parents[0])
        .Where(familyName == "Smith");

<span data-ttu-id="f0070-870">**SQL**</span><span class="sxs-lookup"><span data-stu-id="f0070-870">**SQL**</span></span>

    SELECT *
    FROM Families f
    WHERE f.parents[0].familyName = "Smith"



<span data-ttu-id="f0070-871">**Wyrażenie lambda LINQ**</span><span class="sxs-lookup"><span data-stu-id="f0070-871">**LINQ lambda expression**</span></span>

    input.Where(family => family.children[0].grade > 3)
        .Select(family => family.parents[0].familyName);

<span data-ttu-id="f0070-872">**SQL**</span><span class="sxs-lookup"><span data-stu-id="f0070-872">**SQL**</span></span> 

    SELECT VALUE f.parents[0].familyName
    FROM Families f
    WHERE f.children[0].grade > 3



<span data-ttu-id="f0070-873">**Wyrażenie lambda LINQ**</span><span class="sxs-lookup"><span data-stu-id="f0070-873">**LINQ lambda expression**</span></span>

    input.Select(family => new { grade=family.children[0].grade}).
        Where(anon=> anon.grade < 3);

<span data-ttu-id="f0070-874">**SQL**</span><span class="sxs-lookup"><span data-stu-id="f0070-874">**SQL**</span></span> 

    SELECT *
    FROM Families f
    WHERE ({grade: f.children[0].grade}.grade > 3)



<span data-ttu-id="f0070-875">**Wyrażenie lambda LINQ**</span><span class="sxs-lookup"><span data-stu-id="f0070-875">**LINQ lambda expression**</span></span>

    input.SelectMany(family => family.parents)
        .Where(parent => parents.familyName == "Smith");

<span data-ttu-id="f0070-876">**SQL**</span><span class="sxs-lookup"><span data-stu-id="f0070-876">**SQL**</span></span> 

    SELECT *
    FROM p IN Families.parents
    WHERE p.familyName = "Smith"



#### <a name="nesting"></a><span data-ttu-id="f0070-877">Zagnieżdżania</span><span class="sxs-lookup"><span data-stu-id="f0070-877">Nesting</span></span>
<span data-ttu-id="f0070-878">Składnia Hello jest `input.SelectMany(x=>x.Q())` w przypadku pytań `Select`, `SelectMany`, lub `Where` operatora.</span><span class="sxs-lookup"><span data-stu-id="f0070-878">hello syntax is `input.SelectMany(x=>x.Q())` where Q is a `Select`, `SelectMany`, or `Where` operator.</span></span>

<span data-ttu-id="f0070-879">W zapytaniu zagnieżdżonym zapytanie wewnętrzny hello jest zastosowane tooeach elementu hello zewnętrzne kolekcji.</span><span class="sxs-lookup"><span data-stu-id="f0070-879">In a nested query, hello inner query is applied tooeach element of hello outer collection.</span></span> <span data-ttu-id="f0070-880">Jeden wewnętrzny zapytania hello mogą odwoływać się pola toohello hello elementów w kolekcji zewnętrzne hello, takich jak jest ważna cecha samosprzężenia.</span><span class="sxs-lookup"><span data-stu-id="f0070-880">One important feature is that hello inner query can refer toohello fields of hello elements in hello outer collection like self-joins.</span></span>

<span data-ttu-id="f0070-881">**Wyrażenie lambda LINQ**</span><span class="sxs-lookup"><span data-stu-id="f0070-881">**LINQ lambda expression**</span></span>

    input.SelectMany(family=> 
        family.parents.Select(p => p.familyName));

<span data-ttu-id="f0070-882">**SQL**</span><span class="sxs-lookup"><span data-stu-id="f0070-882">**SQL**</span></span> 

    SELECT VALUE p.familyName
    FROM Families f
    JOIN p IN f.parents


<span data-ttu-id="f0070-883">**Wyrażenie lambda LINQ**</span><span class="sxs-lookup"><span data-stu-id="f0070-883">**LINQ lambda expression**</span></span>

    input.SelectMany(family => 
        family.children.Where(child => child.familyName == "Jeff"));

<span data-ttu-id="f0070-884">**SQL**</span><span class="sxs-lookup"><span data-stu-id="f0070-884">**SQL**</span></span> 

    SELECT *
    FROM Families f
    JOIN c IN f.children
    WHERE c.familyName = "Jeff"



<span data-ttu-id="f0070-885">**Wyrażenie lambda LINQ**</span><span class="sxs-lookup"><span data-stu-id="f0070-885">**LINQ lambda expression**</span></span>

    input.SelectMany(family => family.children.Where(
        child => child.familyName == family.parents[0].familyName));

<span data-ttu-id="f0070-886">**SQL**</span><span class="sxs-lookup"><span data-stu-id="f0070-886">**SQL**</span></span> 

    SELECT *
    FROM Families f
    JOIN c IN f.children
    WHERE c.familyName = f.parents[0].familyName


## <span data-ttu-id="f0070-887"><a id="ExecutingSqlQueries"></a>Wykonywanie kwerend SQL</span><span class="sxs-lookup"><span data-stu-id="f0070-887"><a id="ExecutingSqlQueries"></a>Executing SQL queries</span></span>
<span data-ttu-id="f0070-888">Rozwiązania cosmos DB udostępnia zasoby za pośrednictwem interfejsu API REST, który można wywołać za pomocą dowolnego języka realizującego żądania HTTP i HTTPS.</span><span class="sxs-lookup"><span data-stu-id="f0070-888">Cosmos DB exposes resources through a REST API that can be called by any language capable of making HTTP/HTTPS requests.</span></span> <span data-ttu-id="f0070-889">Ponadto DB rozwiązania Cosmos oferuje biblioteki programistyczne dla kilku popularnych języków, takich jak .NET, Node.js, JavaScript i Python.</span><span class="sxs-lookup"><span data-stu-id="f0070-889">Additionally, Cosmos DB offers programming libraries for several popular languages like .NET, Node.js, JavaScript, and Python.</span></span> <span data-ttu-id="f0070-890">Hello interfejsu API REST i hello różnych bibliotek wszystkich obsługuje zapytań za pomocą programu SQL.</span><span class="sxs-lookup"><span data-stu-id="f0070-890">hello REST API and hello various libraries all support querying through SQL.</span></span> <span data-ttu-id="f0070-891">Hello zestawu .NET SDK obsługuje dodatkowo badania tooSQL LINQ.</span><span class="sxs-lookup"><span data-stu-id="f0070-891">hello .NET SDK supports LINQ querying in addition tooSQL.</span></span>

<span data-ttu-id="f0070-892">Witaj w następujących przykładach pokazano, jak toocreate kwerendy i przesłać je do konta bazy danych DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="f0070-892">hello following examples show how toocreate a query and submit it against a Cosmos DB database account.</span></span>

### <span data-ttu-id="f0070-893"><a id="RestAPI"></a>INTERFEJS API REST</span><span class="sxs-lookup"><span data-stu-id="f0070-893"><a id="RestAPI"></a>REST API</span></span>
<span data-ttu-id="f0070-894">Rozwiązania cosmos DB oferuje Otwórz model programowania RESTful za pośrednictwem protokołu HTTP.</span><span class="sxs-lookup"><span data-stu-id="f0070-894">Cosmos DB offers an open RESTful programming model over HTTP.</span></span> <span data-ttu-id="f0070-895">Konta bazy danych można alokować przy użyciu subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f0070-895">Database accounts can be provisioned using an Azure subscription.</span></span> <span data-ttu-id="f0070-896">model zasobów bazy danych rozwiązania Cosmos Hello zawiera zestaw zasobów w ramach konta bazy danych, z których każdy jest mogą być adresowane za pomocą logicznych i stabilny identyfikator URI.</span><span class="sxs-lookup"><span data-stu-id="f0070-896">hello Cosmos DB resource model consists of a set of resources under a database account, each  of which is addressable using a logical and stable URI.</span></span> <span data-ttu-id="f0070-897">Zestaw zasobów jest tooas określonego źródła danych w tym dokumencie.</span><span class="sxs-lookup"><span data-stu-id="f0070-897">A set of resources is referred tooas a feed in this document.</span></span> <span data-ttu-id="f0070-898">Konto bazy danych zawiera zestaw baz danych, każda z nich zawiera wiele kolekcji, a każdy z których w Włącz zawierają dokumentów, funkcje UDF i innych typów zasobów.</span><span class="sxs-lookup"><span data-stu-id="f0070-898">A database account consists of a set of databases, each containing multiple collections, each of which in-turn contain documents, UDFs, and other resource types.</span></span>

<span data-ttu-id="f0070-899">Hello podstawowe interakcji model przy użyciu tych zasobów jest za pośrednictwem zleceń hello HTTP GET, PUT, POST i DELETE z ich interpretacji standardowa.</span><span class="sxs-lookup"><span data-stu-id="f0070-899">hello basic interaction model with these resources is through hello HTTP verbs GET, PUT, POST, and DELETE with their standard interpretation.</span></span> <span data-ttu-id="f0070-900">zlecenie POST Hello jest używany w celu utworzenia nowego zasobu, wykonywania procedury składowanej lub zapytania DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="f0070-900">hello POST verb is used for creation of a new resource, for executing a stored procedure or for issuing a Cosmos DB query.</span></span> <span data-ttu-id="f0070-901">Zapytania są zawsze operacji tylko do odczytu z żadnych efektów ubocznych.</span><span class="sxs-lookup"><span data-stu-id="f0070-901">Queries are always read-only operations with no side-effects.</span></span>

<span data-ttu-id="f0070-902">Witaj poniższe przykłady przedstawiają POST dla zapytania interfejsu API usługi DocumentDB wykonane w stosunku do kolekcji zawierającej dwa dokumenty przykładowe hello się, że firma Microsoft zostało sprawdzone wykonanej do tej pory.</span><span class="sxs-lookup"><span data-stu-id="f0070-902">hello following examples show a POST for a DocumentDB API query made against a collection containing hello two sample documents we've reviewed so far.</span></span> <span data-ttu-id="f0070-903">Zapytanie Hello ma filtr prosty na powitania JSON nazwę właściwości.</span><span class="sxs-lookup"><span data-stu-id="f0070-903">hello query has a simple filter on hello JSON name property.</span></span> <span data-ttu-id="f0070-904">Należy zwrócić uwagę użycie hello hello `x-ms-documentdb-isquery` i Content-Type: `application/query+json` toodenote nagłówki, które hello operacji jest zapytaniem.</span><span class="sxs-lookup"><span data-stu-id="f0070-904">Note hello use of hello `x-ms-documentdb-isquery` and Content-Type: `application/query+json` headers toodenote that hello operation is a query.</span></span>

<span data-ttu-id="f0070-905">**Żądanie**</span><span class="sxs-lookup"><span data-stu-id="f0070-905">**Request**</span></span>

    POST https://<REST URI>/docs HTTP/1.1
    ...
    x-ms-documentdb-isquery: True
    Content-Type: application/query+json

    {      
        "query": "SELECT * FROM Families f WHERE f.id = @familyId",     
        "parameters": [          
            {"name": "@familyId", "value": "AndersenFamily"}         
        ] 
    }


<span data-ttu-id="f0070-906">**Wyniki**</span><span class="sxs-lookup"><span data-stu-id="f0070-906">**Results**</span></span>

    HTTP/1.1 200 Ok
    x-ms-activity-id: 8b4678fa-a947-47d3-8dd3-549a40da6eed
    x-ms-item-count: 1
    x-ms-request-charge: 0.32

    <indented for readability, results highlighted>

    {  
       "_rid":"u1NXANcKogE=",
       "Documents":[  
          {  
             "id":"AndersenFamily",
             "lastName":"Andersen",
             "parents":[  
                {  
                   "firstName":"Thomas"
                },
                {  
                   "firstName":"Mary Kay"
                }
             ],
             "children":[  
                {  
                   "firstName":"Henriette Thaulow",
                   "gender":"female",
                   "grade":5,
                   "pets":[  
                      {  
                         "givenName":"Fluffy"
                      }
                   ]
                }
             ],
             "address":{  
                "state":"WA",
                "county":"King",
                "city":"seattle"
             },
             "_rid":"u1NXANcKogEcAAAAAAAAAA==",
             "_ts":1407691744,
             "_self":"dbs\/u1NXAA==\/colls\/u1NXANcKogE=\/docs\/u1NXANcKogEcAAAAAAAAAA==\/",
             "_etag":"00002b00-0000-0000-0000-53e7abe00000",
             "_attachments":"_attachments\/"
          }
       ],
       "count":1
    }


<span data-ttu-id="f0070-907">drugi przykład Witaj zawiera bardziej złożoną kwerendę, która zwraca wiele wyników z hello sprzężenia.</span><span class="sxs-lookup"><span data-stu-id="f0070-907">hello second example shows a more complex query that returns multiple results from hello join.</span></span>

<span data-ttu-id="f0070-908">**Żądanie**</span><span class="sxs-lookup"><span data-stu-id="f0070-908">**Request**</span></span>

    POST https://<REST URI>/docs HTTP/1.1
    ...
    x-ms-documentdb-isquery: True
    Content-Type: application/query+json

    {      
        "query": "SELECT 
                     f.id AS familyName, 
                     c.givenName AS childGivenName, 
                     c.firstName AS childFirstName, 
                     p.givenName AS petName 
                  FROM Families f 
                  JOIN c IN f.children 
                  JOIN p in c.pets",     
        "parameters": [] 
    }


<span data-ttu-id="f0070-909">**Wyniki**</span><span class="sxs-lookup"><span data-stu-id="f0070-909">**Results**</span></span>

    HTTP/1.1 200 Ok
    x-ms-activity-id: 568f34e3-5695-44d3-9b7d-62f8b83e509d
    x-ms-item-count: 1
    x-ms-request-charge: 7.84

    <indented for readability, results highlighted>

    {  
       "_rid":"u1NXANcKogE=",
       "Documents":[  
          {  
             "familyName":"AndersenFamily",
             "childFirstName":"Henriette Thaulow",
             "petName":"Fluffy"
          },
          {  
             "familyName":"WakefieldFamily",
             "childGivenName":"Jesse",
             "petName":"Goofy"
          },
          {  
             "familyName":"WakefieldFamily",
             "childGivenName":"Jesse",
             "petName":"Shadow"
          }
       ],
       "count":3
    }


<span data-ttu-id="f0070-910">Jeśli wyników zapytania nie mieści się w obrębie jednej strony wyników, a następnie hello interfejsu API REST zwraca token kontynuacji za pośrednictwem hello `x-ms-continuation-token` nagłówka odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="f0070-910">If a query's results cannot fit within a single page of results, then hello REST API returns a continuation token through hello `x-ms-continuation-token` response header.</span></span> <span data-ttu-id="f0070-911">Klienci mogą z podziałem na strony wyników przez dołączenie nagłówka hello w kolejnych wyników.</span><span class="sxs-lookup"><span data-stu-id="f0070-911">Clients can paginate results by including hello header in subsequent results.</span></span> <span data-ttu-id="f0070-912">Witaj liczba wyników na stronie również mogą być kontrolowane za pośrednictwem hello `x-ms-max-item-count` numer nagłówka.</span><span class="sxs-lookup"><span data-stu-id="f0070-912">hello number of results per page can also be controlled through hello `x-ms-max-item-count` number header.</span></span> <span data-ttu-id="f0070-913">Jeśli określone zapytanie hello ma funkcję agregacji, takie jak `COUNT`, następnie hello zapytania strony może zwracać wartości zagregowane częściowo za pośrednictwem hello strony wyników.</span><span class="sxs-lookup"><span data-stu-id="f0070-913">If hello specified query has an aggregation function like `COUNT`, then hello query page may return a partially aggregated value over hello page of results.</span></span> <span data-ttu-id="f0070-914">klientom Witaj musi wykonać agregacji drugiego poziomu przez te wyniki tooproduce hello wyników końcowych, na przykład, Suma za pośrednictwem liczby hello zwracane w hello poszczególnych stron tooreturn hello łączna liczba.</span><span class="sxs-lookup"><span data-stu-id="f0070-914">hello clients must perform a second-level aggregation over these results tooproduce hello final results, for example, sum over hello counts returned in hello individual pages tooreturn hello total count.</span></span>

<span data-ttu-id="f0070-915">zasady spójności danych hello toomanage dla zapytań, użyj hello `x-ms-consistency-level` nagłówka, takie jak wszystkie żądania interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="f0070-915">toomanage hello data consistency policy for queries, use hello `x-ms-consistency-level` header like all REST API requests.</span></span> <span data-ttu-id="f0070-916">Spójność sesji jest wymagana tooalso echo hello najnowszych `x-ms-session-token` nagłówka pliku Cookie w żądaniu zapytania hello.</span><span class="sxs-lookup"><span data-stu-id="f0070-916">For session consistency, it is required tooalso echo hello latest `x-ms-session-token` Cookie header in hello query request.</span></span> <span data-ttu-id="f0070-917">Witaj zasady indeksowania, którego dotyczy kwerenda kolekcji można również wpływ spójności hello wyników zapytania.</span><span class="sxs-lookup"><span data-stu-id="f0070-917">hello queried collection's indexing policy can also influence hello consistency of query results.</span></span> <span data-ttu-id="f0070-918">Z hello domyślne ustawienia zasad indeksowania kolekcje indeksu hello jest zawsze hello zawartości dokumentu i zapytań wyników spełniających spójności hello wybrany dla danych.</span><span class="sxs-lookup"><span data-stu-id="f0070-918">With hello default indexing policy settings, for collections hello index is always current with hello document contents and query results match hello consistency chosen for data.</span></span> <span data-ttu-id="f0070-919">Jeśli hello indeksowania zasad swobodnej tooLazy, zapytania mogą zwracać starych wyników.</span><span class="sxs-lookup"><span data-stu-id="f0070-919">If hello indexing policy is relaxed tooLazy, then queries can return stale results.</span></span> <span data-ttu-id="f0070-920">Aby uzyskać więcej informacji, zobacz [poziomy spójności bazy danych rozwiązania Cosmos Azure][consistency-levels].</span><span class="sxs-lookup"><span data-stu-id="f0070-920">For more information, see [Azure Cosmos DB Consistency Levels][consistency-levels].</span></span>

<span data-ttu-id="f0070-921">Jeśli hello skonfigurowane zasady indeksowania w kolekcji hello nie obsługuje określonego zapytania hello, serwera bazy danych Azure rozwiązania Cosmos hello zwraca 400 "złe żądanie".</span><span class="sxs-lookup"><span data-stu-id="f0070-921">If hello configured indexing policy on hello collection cannot support hello specified query, hello Azure Cosmos DB server returns 400 "Bad Request".</span></span> <span data-ttu-id="f0070-922">Ten błąd jest zwracany dla zakresu zapytania względem ścieżki skonfigurowane dla wyszukiwań wyznaczania wartości skrótu (równości) i ścieżek jawnie wykluczona z indeksowania.</span><span class="sxs-lookup"><span data-stu-id="f0070-922">This is returned for range queries against paths configured for hash (equality) lookups, and for paths explicitly excluded from indexing.</span></span> <span data-ttu-id="f0070-923">Witaj `x-ms-documentdb-query-enable-scan` nagłówek może być określony tooallow hello zapytania tooperform skanowanie, gdy indeks nie jest dostępna.</span><span class="sxs-lookup"><span data-stu-id="f0070-923">hello `x-ms-documentdb-query-enable-scan` header can be specified tooallow hello query tooperform a scan when an index is not available.</span></span>

<span data-ttu-id="f0070-924">Szczegółowe metryki na wykonanie kwerendy można uzyskać przez ustawienie `x-ms-documentdb-populatequerymetrics` nagłówka zbyt`True`.</span><span class="sxs-lookup"><span data-stu-id="f0070-924">You can get detailed metrics on query execution by setting `x-ms-documentdb-populatequerymetrics` header too`True`.</span></span> <span data-ttu-id="f0070-925">Aby uzyskać więcej informacji, zobacz [metryki kwerendy SQL dla interfejsu API Azure rozwiązania Cosmos bazy danych usługi DocumentDB](documentdb-sql-query-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="f0070-925">For more information, see [SQL query metrics for Azure Cosmos DB DocumentDB API](documentdb-sql-query-metrics.md).</span></span>

### <span data-ttu-id="f0070-926"><a id="DotNetSdk"></a>C# (.NET) ZESTAWU SDK</span><span class="sxs-lookup"><span data-stu-id="f0070-926"><a id="DotNetSdk"></a>C# (.NET) SDK</span></span>
<span data-ttu-id="f0070-927">Witaj zestawu .NET SDK obsługuje zarówno LINQ, jak i SQL zapytań.</span><span class="sxs-lookup"><span data-stu-id="f0070-927">hello .NET SDK supports both LINQ and SQL querying.</span></span> <span data-ttu-id="f0070-928">Witaj poniższy przykład przedstawia sposób zapytanie filtru prostego powitania tooperform wprowadzone wcześniej w tym dokumencie.</span><span class="sxs-lookup"><span data-stu-id="f0070-928">hello following example shows how tooperform hello simple filter query introduced earlier in this document.</span></span>

    foreach (var family in client.CreateDocumentQuery(collectionLink, 
        "SELECT * FROM Families f WHERE f.id = \"AndersenFamily\""))
    {
        Console.WriteLine("\tRead {0} from SQL", family);
    }

    SqlQuerySpec query = new SqlQuerySpec("SELECT * FROM Families f WHERE f.id = @familyId");
    query.Parameters = new SqlParameterCollection();
    query.Parameters.Add(new SqlParameter("@familyId", "AndersenFamily"));

    foreach (var family in client.CreateDocumentQuery(collectionLink, query))
    {
        Console.WriteLine("\tRead {0} from parameterized SQL", family);
    }

    foreach (var family in (
        from f in client.CreateDocumentQuery(collectionLink)
        where f.Id == "AndersenFamily"
        select f))
    {
        Console.WriteLine("\tRead {0} from LINQ query", family);
    }

    foreach (var family in client.CreateDocumentQuery(collectionLink)
        .Where(f => f.Id == "AndersenFamily")
        .Select(f => f))
    {
        Console.WriteLine("\tRead {0} from LINQ lambda", family);
    }


<span data-ttu-id="f0070-929">W tym przykładzie porównanie dwóch właściwości równości w ramach każdego dokumentu i używa projekcje anonimowy.</span><span class="sxs-lookup"><span data-stu-id="f0070-929">This sample compares two properties for equality within each document and uses anonymous projections.</span></span> 

    foreach (var family in client.CreateDocumentQuery(collectionLink,
        @"SELECT {""Name"": f.id, ""City"":f.address.city} AS Family 
        FROM Families f 
        WHERE f.address.city = f.address.state"))
    {
        Console.WriteLine("\tRead {0} from SQL", family);
    }

    foreach (var family in (
        from f in client.CreateDocumentQuery<Family>(collectionLink)
        where f.address.city == f.address.state
        select new { Name = f.Id, City = f.address.city }))
    {
        Console.WriteLine("\tRead {0} from LINQ query", family);
    }

    foreach (var family in
        client.CreateDocumentQuery<Family>(collectionLink)
        .Where(f => f.address.city == f.address.state)
        .Select(f => new { Name = f.Id, City = f.address.city }))
    {
        Console.WriteLine("\tRead {0} from LINQ lambda", family);
    }


<span data-ttu-id="f0070-930">Następna próbka Hello pokazuje sprzężenia, wyrazić za pomocą operacja SelectMany LINQ.</span><span class="sxs-lookup"><span data-stu-id="f0070-930">hello next sample shows joins, expressed through LINQ SelectMany.</span></span>

    foreach (var pet in client.CreateDocumentQuery(collectionLink,
          @"SELECT p
            FROM Families f 
                 JOIN c IN f.children 
                 JOIN p in c.pets 
            WHERE p.givenName = ""Shadow"""))
    {
        Console.WriteLine("\tRead {0} from SQL", pet);
    }

    // Equivalent in Lambda expressions
    foreach (var pet in
        client.CreateDocumentQuery<Family>(collectionLink)
        .SelectMany(f => f.children)
        .SelectMany(c => c.pets)
        .Where(p => p.givenName == "Shadow"))
    {
        Console.WriteLine("\tRead {0} from LINQ lambda", pet);
    }



<span data-ttu-id="f0070-931">powitania klienta .NET automatycznie iterację wszystkich stron hello wyników kwerendy w blokach foreach hello, jak pokazano powyżej.</span><span class="sxs-lookup"><span data-stu-id="f0070-931">hello .NET client automatically iterates through all hello pages of query results in hello foreach blocks as shown above.</span></span> <span data-ttu-id="f0070-932">zapytania Hello wprowadzono w sekcji interfejsu API REST hello opcje są także dostępne w hello zestawu SDK .NET przy użyciu hello `FeedOptions` i `FeedResponse` klas w hello CreateDocumentQuery metody.</span><span class="sxs-lookup"><span data-stu-id="f0070-932">hello query options introduced in hello REST API section are also available in hello .NET SDK using hello `FeedOptions` and `FeedResponse` classes in hello CreateDocumentQuery method.</span></span> <span data-ttu-id="f0070-933">Hello liczbę stron, które mogą być kontrolowane za pomocą hello `MaxItemCount` ustawienie.</span><span class="sxs-lookup"><span data-stu-id="f0070-933">hello number of pages can be controlled using hello `MaxItemCount` setting.</span></span> 

<span data-ttu-id="f0070-934">Można również jawnie kontrolować stronicowania, tworząc `IDocumentQueryable` przy użyciu hello `IQueryable` obiektu, a następnie odczytując` ResponseContinuationToken` wartości i przekazywanie ich ponownie jako `RequestContinuationToken` w `FeedOptions`.</span><span class="sxs-lookup"><span data-stu-id="f0070-934">You can also explicitly control paging by creating `IDocumentQueryable` using hello `IQueryable` object, then by reading the` ResponseContinuationToken` values and passing them back as `RequestContinuationToken` in `FeedOptions`.</span></span> <span data-ttu-id="f0070-935">`EnableScanInQuery`może być zestaw tooenable skanowanie, gdy hello zapytania nie może być obsługiwana przez hello skonfigurowane zasady indeksowania.</span><span class="sxs-lookup"><span data-stu-id="f0070-935">`EnableScanInQuery` can be set tooenable scans when hello query cannot be supported by hello configured indexing policy.</span></span> <span data-ttu-id="f0070-936">Dla kolekcji partycjonowanych, można użyć `PartitionKey` toorun hello zapytanie pojedynczej partycji (chociaż DB rozwiązania Cosmos można automatycznie wyodrębniania to tekst zapytania hello), i `EnableCrossPartitionQuery` toorun zapytania, które mogą wymagać toobe uruchomienia wielu partycji.</span><span class="sxs-lookup"><span data-stu-id="f0070-936">For partitioned collections, you can use `PartitionKey` toorun hello query against a single partition (though Cosmos DB can automatically extract this from hello query text), and `EnableCrossPartitionQuery` toorun queries that may need toobe run against multiple partitions.</span></span> 

<span data-ttu-id="f0070-937">Odwołuje się zbyt[przykłady Azure rozwiązania Cosmos DB .NET](https://github.com/Azure/azure-documentdb-net) dla większej liczby próbek zawierający zapytania.</span><span class="sxs-lookup"><span data-stu-id="f0070-937">Refer too[Azure Cosmos DB .NET samples](https://github.com/Azure/azure-documentdb-net) for more samples containing queries.</span></span> 

### <span data-ttu-id="f0070-938"><a id="JavaScriptServerSideApi"></a>Interfejs API programu JavaScript po stronie serwera</span><span class="sxs-lookup"><span data-stu-id="f0070-938"><a id="JavaScriptServerSideApi"></a>JavaScript server-side API</span></span>
<span data-ttu-id="f0070-939">Rozwiązania cosmos DB zapewnia model programowania do wykonywania logiki aplikacji JavaScript oparty bezpośrednio na powitania kolekcji przy użyciu procedur składowanych i wyzwalaczy.</span><span class="sxs-lookup"><span data-stu-id="f0070-939">Cosmos DB provides a programming model for executing JavaScript based application logic directly on hello collections using stored procedures and triggers.</span></span> <span data-ttu-id="f0070-940">Logika JavaScript Hello zarejestrowany na poziomie zbioru następnie mogą wyzwalać operacje bazy danych na operacje hello w dokumentach hello hello podane kolekcji.</span><span class="sxs-lookup"><span data-stu-id="f0070-940">hello JavaScript logic registered at a collection level can then issue database operations on hello operations on hello documents of hello given collection.</span></span> <span data-ttu-id="f0070-941">Operacje te są ujęte w transakcji ACID otoczenia.</span><span class="sxs-lookup"><span data-stu-id="f0070-941">These operations are wrapped in ambient ACID transactions.</span></span>

<span data-ttu-id="f0070-942">Witaj poniższy przykład przedstawia sposób queryDocuments hello toouse w toomake hello JavaScript API serwera zapytania z wewnątrz procedury składowane i wyzwalaczy.</span><span class="sxs-lookup"><span data-stu-id="f0070-942">hello following example shows how toouse hello queryDocuments in hello JavaScript server API toomake queries from inside stored procedures and triggers.</span></span>

    function businessLogic(name, author) {
        var context = getContext();
        var collectionManager = context.getCollection();
        var collectionLink = collectionManager.getSelfLink()

        // create a new document.
        collectionManager.createDocument(collectionLink,
            { name: name, author: author },
            function (err, documentCreated) {
                if (err) throw new Error(err.message);

                // filter documents by author
                var filterQuery = "SELECT * from root r WHERE r.author = 'George R.'";
                collectionManager.queryDocuments(collectionLink,
                    filterQuery,
                    function (err, matchingDocuments) {
                        if (err) throw new Error(err.message);
    context.getResponse().setBody(matchingDocuments.length);

                        // Replace hello author name for all documents that satisfied hello query.
                        for (var i = 0; i < matchingDocuments.length; i++) {
                            matchingDocuments[i].author = "George R. R. Martin";
                            // we don't need tooexecute a callback because they are in parallel
                            collectionManager.replaceDocument(matchingDocuments[i]._self,
                                matchingDocuments[i]);
                        }
                    })
            });
    }

## <span data-ttu-id="f0070-943"><a id="References"></a>Odwołania</span><span class="sxs-lookup"><span data-stu-id="f0070-943"><a id="References"></a>References</span></span>
1. <span data-ttu-id="f0070-944">[Wprowadzenie tooAzure DB rozwiązania Cosmos][introduction]</span><span class="sxs-lookup"><span data-stu-id="f0070-944">[Introduction tooAzure Cosmos DB][introduction]</span></span>
2. [<span data-ttu-id="f0070-945">Specyfikacja rozwiązania Cosmos bazy danych SQL Azure</span><span class="sxs-lookup"><span data-stu-id="f0070-945">Azure Cosmos DB SQL specification</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=510612)
3. [<span data-ttu-id="f0070-946">Przykładów dla platformy Azure .NET DB rozwiązania Cosmos</span><span class="sxs-lookup"><span data-stu-id="f0070-946">Azure Cosmos DB .NET samples</span></span>](https://github.com/Azure/azure-documentdb-net)
4. <span data-ttu-id="f0070-947">[Poziomy spójności bazy danych Azure rozwiązania Cosmos][consistency-levels]</span><span class="sxs-lookup"><span data-stu-id="f0070-947">[Azure Cosmos DB Consistency Levels][consistency-levels]</span></span>
5. <span data-ttu-id="f0070-948">ANSI SQL 2011 [http://www.iso.org/iso/iso_catalogue/catalogue_tc/catalogue_detail.htm?csnumber=53681](http://www.iso.org/iso/iso_catalogue/catalogue_tc/catalogue_detail.htm?csnumber=53681)</span><span class="sxs-lookup"><span data-stu-id="f0070-948">ANSI SQL 2011 [http://www.iso.org/iso/iso_catalogue/catalogue_tc/catalogue_detail.htm?csnumber=53681](http://www.iso.org/iso/iso_catalogue/catalogue_tc/catalogue_detail.htm?csnumber=53681)</span></span>
6. <span data-ttu-id="f0070-949">JSON [http://json.org/](http://json.org/)</span><span class="sxs-lookup"><span data-stu-id="f0070-949">JSON [http://json.org/](http://json.org/)</span></span>
7. <span data-ttu-id="f0070-950">Specyfikacja języka JavaScript [http://www.ecma-international.org/publications/standards/Ecma-262.htm](http://www.ecma-international.org/publications/standards/Ecma-262.htm)</span><span class="sxs-lookup"><span data-stu-id="f0070-950">Javascript Specification [http://www.ecma-international.org/publications/standards/Ecma-262.htm](http://www.ecma-international.org/publications/standards/Ecma-262.htm)</span></span> 
8. <span data-ttu-id="f0070-951">LINQ [http://msdn.microsoft.com/library/bb308959.aspx](http://msdn.microsoft.com/library/bb308959.aspx)</span><span class="sxs-lookup"><span data-stu-id="f0070-951">LINQ [http://msdn.microsoft.com/library/bb308959.aspx](http://msdn.microsoft.com/library/bb308959.aspx)</span></span> 
9. <span data-ttu-id="f0070-952">Zapytanie techniki oceny dla dużych baz danych [http://dl.acm.org/citation.cfm?id=152611](http://dl.acm.org/citation.cfm?id=152611)</span><span class="sxs-lookup"><span data-stu-id="f0070-952">Query evaluation techniques for large databases [http://dl.acm.org/citation.cfm?id=152611](http://dl.acm.org/citation.cfm?id=152611)</span></span>
10. <span data-ttu-id="f0070-953">Przetwarzania zapytań w systemach równoległych relacyjnych baz danych, naciśnij społeczeństwa IEEE komputera, 1994 r.</span><span class="sxs-lookup"><span data-stu-id="f0070-953">Query Processing in Parallel Relational Database Systems, IEEE Computer Society Press, 1994</span></span>
11. <span data-ttu-id="f0070-954">Tan lu, Ooi, Wyślij zapytanie do przetwarzania w systemach równoległych relacyjnej bazy danych, naciśnij klawisz społeczeństwa IEEE komputera, 1994.</span><span class="sxs-lookup"><span data-stu-id="f0070-954">Lu, Ooi, Tan, Query Processing in Parallel Relational Database Systems, IEEE Computer Society Press, 1994.</span></span>
12. <span data-ttu-id="f0070-955">Christopher Olston, Reed Benjaminowi Utkarsh Srivastava, Kumar Ravi, Andrew Tomkins: Pig Latin: nie tak obcego języka do przetwarzania danych, SIGMOD 2008.</span><span class="sxs-lookup"><span data-stu-id="f0070-955">Christopher Olston, Benjamin Reed, Utkarsh Srivastava, Ravi Kumar, Andrew Tomkins: Pig Latin: A Not-So-Foreign Language for Data Processing, SIGMOD 2008.</span></span>
13. <span data-ttu-id="f0070-956">G.</span><span class="sxs-lookup"><span data-stu-id="f0070-956">G.</span></span> <span data-ttu-id="f0070-957">Graefe.</span><span class="sxs-lookup"><span data-stu-id="f0070-957">Graefe.</span></span> <span data-ttu-id="f0070-958">Struktura kaskady Hello na optymalizację zapytania.</span><span class="sxs-lookup"><span data-stu-id="f0070-958">hello Cascades framework for query optimization.</span></span> <span data-ttu-id="f0070-959">Eng. IEEE danych</span><span class="sxs-lookup"><span data-stu-id="f0070-959">IEEE Data Eng.</span></span> <span data-ttu-id="f0070-960">Bull., 18(3): 1995.</span><span class="sxs-lookup"><span data-stu-id="f0070-960">Bull., 18(3): 1995.</span></span>

[1]: ./media/documentdb-sql-query/sql-query1.png
[introduction]: introduction.md
[consistency-levels]: consistency-levels.md