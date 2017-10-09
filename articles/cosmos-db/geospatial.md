---
title: "aaaWorking z dane geograficzne w usłudze Azure DB rozwiązania Cosmos | Dokumentacja firmy Microsoft"
description: "Zrozumieć, jak toocreate, indeksu i przestrzennych obiektów z bazy danych Azure rozwiązania Cosmos zapytania i hello interfejsu API usługi DocumentDB."
services: cosmos-db
documentationcenter: 
author: arramac
manager: jhubbard
editor: monicar
ms.assetid: 82ce2898-a9f9-4acf-af4d-8ca4ba9c7b8f
ms.service: cosmos-db
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 05/22/2017
ms.author: arramac
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a1e40b78cb4595631d845d46c21d07a30c8b972f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-geospatial-and-geojson-location-data-in-azure-cosmos-db"></a><span data-ttu-id="513b7-103">Praca z dane geograficzne i danych lokalizacji GeoJSON w usłudze Azure DB rozwiązania Cosmos</span><span class="sxs-lookup"><span data-stu-id="513b7-103">Working with geospatial and GeoJSON location data in Azure Cosmos DB</span></span>
<span data-ttu-id="513b7-104">Ten artykuł obejmuje wprowadzenie toohello dane geograficzne funkcji [bazy danych Azure rozwiązania Cosmos](https://azure.microsoft.com/services/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="513b7-104">This article is an introduction toohello geospatial functionality in [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span></span> <span data-ttu-id="513b7-105">Po przeczytaniu tego, będą mogli tooanswer hello następujące pytania:</span><span class="sxs-lookup"><span data-stu-id="513b7-105">After reading this, you will be able tooanswer hello following questions:</span></span>

* <span data-ttu-id="513b7-106">Sposób przechowywania danych przestrzennych w usłudze Azure DB rozwiązania Cosmos?</span><span class="sxs-lookup"><span data-stu-id="513b7-106">How do I store spatial data in Azure Cosmos DB?</span></span>
* <span data-ttu-id="513b7-107">Jak wykonać zapytanie dane geograficzne w usłudze Azure DB rozwiązania Cosmos w SQL i LINQ</span><span class="sxs-lookup"><span data-stu-id="513b7-107">How can I query geospatial data in Azure Cosmos DB in SQL and LINQ?</span></span>
* <span data-ttu-id="513b7-108">Jak włączyć lub wyłączyć indeksowanie przestrzenne w usłudze Azure DB rozwiązania Cosmos</span><span class="sxs-lookup"><span data-stu-id="513b7-108">How do I enable or disable spatial indexing in Azure Cosmos DB?</span></span>

<span data-ttu-id="513b7-109">W tym artykule opisano, jak toowork z danych przestrzennych z hello interfejsu API usługi DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="513b7-109">This article shows how toowork with spatial data with hello DocumentDB API.</span></span> <span data-ttu-id="513b7-110">Zobacz to [projektu GitHub](https://github.com/Azure/azure-documentdb-dotnet/blob/master/samples/code-samples/Geospatial/Program.cs) dla przykładów kodu.</span><span class="sxs-lookup"><span data-stu-id="513b7-110">Please see this [GitHub project](https://github.com/Azure/azure-documentdb-dotnet/blob/master/samples/code-samples/Geospatial/Program.cs) for code samples.</span></span>

## <a name="introduction-toospatial-data"></a><span data-ttu-id="513b7-111">Wprowadzenie toospatial danych</span><span class="sxs-lookup"><span data-stu-id="513b7-111">Introduction toospatial data</span></span>
<span data-ttu-id="513b7-112">Dane przestrzenne opisano hello pozycji i kształt obiektów w przestrzeni.</span><span class="sxs-lookup"><span data-stu-id="513b7-112">Spatial data describes hello position and shape of objects in space.</span></span> <span data-ttu-id="513b7-113">W większości aplikacji one odpowiadać tooobjects na powitania ziemi, tj. dane geograficzne.</span><span class="sxs-lookup"><span data-stu-id="513b7-113">In most applications, these correspond tooobjects on hello earth, i.e. geospatial data.</span></span> <span data-ttu-id="513b7-114">Dane przestrzenne może być używane toorepresent hello lokalizacji osoby, miejsca lub granic hello miejscowości lub jeziora.</span><span class="sxs-lookup"><span data-stu-id="513b7-114">Spatial data can be used toorepresent hello location of a person, a place of interest, or hello boundary of a city, or a lake.</span></span> <span data-ttu-id="513b7-115">Typowe przypadki użycia obejmują często zbliżeniowe zapytań, dotyczących np. "Znajdź wszystkie kawiarniach niemal mojej bieżącej lokalizacji".</span><span class="sxs-lookup"><span data-stu-id="513b7-115">Common use cases often involve proximity queries, for e.g., "find all coffee shops near my current location".</span></span> 

### <a name="geojson"></a><span data-ttu-id="513b7-116">GeoJSON</span><span class="sxs-lookup"><span data-stu-id="513b7-116">GeoJSON</span></span>
<span data-ttu-id="513b7-117">Azure DB rozwiązania Cosmos obsługuje indeksowanie i wyszukiwanie danych punktu geograficznych reprezentowanej przy użyciu hello [specyfikacji GeoJSON](https://tools.ietf.org/html/rfc7946).</span><span class="sxs-lookup"><span data-stu-id="513b7-117">Azure Cosmos DB supports indexing and querying of geospatial point data that's represented using hello [GeoJSON specification](https://tools.ietf.org/html/rfc7946).</span></span> <span data-ttu-id="513b7-118">Struktury danych GeoJSON są zawsze prawidłowych obiektów JSON, dzięki czemu mogą być przechowywane i wyświetlić przy użyciu bazy danych Azure rozwiązania Cosmos bez żadnych specjalnych narzędzi i bibliotek.</span><span class="sxs-lookup"><span data-stu-id="513b7-118">GeoJSON data structures are always valid JSON objects, so they can be stored and queried using Azure Cosmos DB without any specialized tools or libraries.</span></span> <span data-ttu-id="513b7-119">Hello Azure rozwiązania Cosmos DB SDK zapewniają pomocnika klasy i metody, dzięki któremu można łatwo toowork z danymi przestrzennymi.</span><span class="sxs-lookup"><span data-stu-id="513b7-119">hello Azure Cosmos DB SDKs provide helper classes and methods that make it easy toowork with spatial data.</span></span> 

### <a name="points-linestrings-and-polygons"></a><span data-ttu-id="513b7-120">Punkty, LineStrings i wielokątów</span><span class="sxs-lookup"><span data-stu-id="513b7-120">Points, LineStrings and Polygons</span></span>
<span data-ttu-id="513b7-121">A **punktu** oznacza pojedynczego pozycję w przestrzeni.</span><span class="sxs-lookup"><span data-stu-id="513b7-121">A **Point** denotes a single position in space.</span></span> <span data-ttu-id="513b7-122">W danych geograficznych punkt reprezentuje hello dokładnej lokalizacji, która może być ulicę sklepów spożywczych, kiosku, samochodu lub miejscowości.</span><span class="sxs-lookup"><span data-stu-id="513b7-122">In geospatial data, a Point represents hello exact location, which could be a street address of a grocery store, a kiosk, an automobile or a city.</span></span>  <span data-ttu-id="513b7-123">Punkt jest reprezentowana w pary GeoJSON (i bazy danych Azure rozwiązania Cosmos) przy użyciu jego współrzędnych lub długości i szerokości geograficznej.</span><span class="sxs-lookup"><span data-stu-id="513b7-123">A point is represented in GeoJSON (and Azure Cosmos DB) using its coordinate pair or longitude and latitude.</span></span> <span data-ttu-id="513b7-124">Oto przykład JSON dla punktu.</span><span class="sxs-lookup"><span data-stu-id="513b7-124">Here's an example JSON for a point.</span></span>

<span data-ttu-id="513b7-125">**Punkty Azure rozwiązania Cosmos bazy danych**</span><span class="sxs-lookup"><span data-stu-id="513b7-125">**Points in Azure Cosmos DB**</span></span>

```json
{
    "type":"Point",
    "coordinates":[ 31.9, -4.8 ]
}
```

> [!NOTE]
> <span data-ttu-id="513b7-126">Hello specyfikacji GeoJSON określa długość pierwszy i szerokości geograficznej drugiego.</span><span class="sxs-lookup"><span data-stu-id="513b7-126">hello GeoJSON specification specifies longitude first and latitude second.</span></span> <span data-ttu-id="513b7-127">Podobnie jak w innych aplikacjach mapowania długości i szerokości geograficznej są kąty i wyświetlany w postaci stopni.</span><span class="sxs-lookup"><span data-stu-id="513b7-127">Like in other mapping applications, longitude and latitude are angles and represented in terms of degrees.</span></span> <span data-ttu-id="513b7-128">Wartości długości geograficznej są mierzone od głównego południka hello i należą do zakresu od- i 180.0 stopni, 180 do szerokości geograficznej wartości są mierzone od równika hello i należą do zakresu od-90.0 i 90.0 stopni.</span><span class="sxs-lookup"><span data-stu-id="513b7-128">Longitude values are measured from hello Prime Meridian and are between -180 and 180.0 degrees, and latitude values are measured from hello equator and are between -90.0 and 90.0 degrees.</span></span> 
> 
> <span data-ttu-id="513b7-129">Azure DB rozwiązania Cosmos interpretuje współrzędne reprezentowane na powitania WGS 84 odwołanie systemu.</span><span class="sxs-lookup"><span data-stu-id="513b7-129">Azure Cosmos DB interprets coordinates as represented per hello WGS-84 reference system.</span></span> <span data-ttu-id="513b7-130">Zobacz poniżej więcej szczegółów dotyczących systemów współrzędnych odwołania.</span><span class="sxs-lookup"><span data-stu-id="513b7-130">Please see below for more details about coordinate reference systems.</span></span>
> 
> 

<span data-ttu-id="513b7-131">Można ją osadzić w dokumencie bazy danych Azure rozwiązania Cosmos opisane w tym przykładzie profilu użytkownika zawierającego dane dotyczące lokalizacji:</span><span class="sxs-lookup"><span data-stu-id="513b7-131">This can be embedded in an Azure Cosmos DB document as shown in this example of a user profile containing location data:</span></span>

<span data-ttu-id="513b7-132">**Użyj profilu z lokalizacją przechowywane w usłudze Azure DB rozwiązania Cosmos**</span><span class="sxs-lookup"><span data-stu-id="513b7-132">**Use Profile with Location stored in Azure Cosmos DB**</span></span>

```json
{
    "id":"documentdb-profile",
    "screen_name":"@CosmosDB",
    "city":"Redmond",
    "topics":[ "global", "distributed" ],
    "location":{
        "type":"Point",
        "coordinates":[ 31.9, -4.8 ]
    }
}
```

<span data-ttu-id="513b7-133">Ponadto toopoints, GeoJSON obsługuje również LineStrings i wielokątów.</span><span class="sxs-lookup"><span data-stu-id="513b7-133">In addition toopoints, GeoJSON also supports LineStrings and Polygons.</span></span> <span data-ttu-id="513b7-134">**LineStrings** reprezentują dwa lub więcej punktów w miejscu i hello segmenty linii, które łączą te elementy.</span><span class="sxs-lookup"><span data-stu-id="513b7-134">**LineStrings** represent a series of two or more points in space and hello line segments that connect them.</span></span> <span data-ttu-id="513b7-135">W danych geograficznych LineStrings są często używane toorepresent drogami lub rzek.</span><span class="sxs-lookup"><span data-stu-id="513b7-135">In geospatial data, LineStrings are commonly used toorepresent highways or rivers.</span></span> <span data-ttu-id="513b7-136">A **wielokąta** jest granicę punktów połączonych formularzy LineString zamknięte.</span><span class="sxs-lookup"><span data-stu-id="513b7-136">A **Polygon** is a boundary of connected points that forms a closed LineString.</span></span> <span data-ttu-id="513b7-137">Wielokąty są często używane toorepresent tworzenie fizyczne jak jeziora lub polityczną jurysdykcjach przykład miast i stanów.</span><span class="sxs-lookup"><span data-stu-id="513b7-137">Polygons are commonly used toorepresent natural formations like lakes or political jurisdictions like cities and states.</span></span> <span data-ttu-id="513b7-138">Oto przykład wielokąta w usłudze Azure DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="513b7-138">Here's an example of a Polygon in Azure Cosmos DB.</span></span> 

<span data-ttu-id="513b7-139">**Wielokąty w GeoJSON**</span><span class="sxs-lookup"><span data-stu-id="513b7-139">**Polygons in GeoJSON**</span></span>

```json
{
    "type":"Polygon",
    "coordinates":[
        [ 31.8, -5 ],
        [ 31.8, -4.7 ],
        [ 32, -4.7 ],
        [ 32, -5 ],
        [ 31.8, -5 ]
    ]
}
```

> [!NOTE]
> <span data-ttu-id="513b7-140">Hello GeoJSON specyfikacji wymaga, aby uzyskać prawidłową wielokątów hello ostatnią parę współrzędnych podane powinien hello sam toocreate najpierw hello zamknięty kształt.</span><span class="sxs-lookup"><span data-stu-id="513b7-140">hello GeoJSON specification requires that for valid Polygons, hello last coordinate pair provided should be hello same as hello first, toocreate a closed shape.</span></span>
> 
> <span data-ttu-id="513b7-141">Punktów w wielokąta muszą być określone w kolejności przeciwnie do ruchu wskazówek zegara.</span><span class="sxs-lookup"><span data-stu-id="513b7-141">Points within a Polygon must be specified in counter-clockwise order.</span></span> <span data-ttu-id="513b7-142">Wielokąt określony w kolejności zegara reprezentuje odwrotność hello hello regionu w niej.</span><span class="sxs-lookup"><span data-stu-id="513b7-142">A Polygon specified in clockwise order represents hello inverse of hello region within it.</span></span>
> 
> 

<span data-ttu-id="513b7-143">W dodatku tooPoint, LineString, Polygon, a GeoJSON określa również hello reprezentację jak toogroup wielu lokalizacji geograficznych, oraz dowolne właściwości tooassociate z używanie funkcji geolokalizacji jako **funkcji**.</span><span class="sxs-lookup"><span data-stu-id="513b7-143">In addition tooPoint, LineString and Polygon, GeoJSON also specifies hello representation for how toogroup multiple geospatial locations, as well as how tooassociate arbitrary properties with geolocation as a **Feature**.</span></span> <span data-ttu-id="513b7-144">Ponieważ te obiekty są poprawne dane JSON, ich można wszystkie przechowywane i przetwarzane w usłudze Azure DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="513b7-144">Since these objects are valid JSON, they can all be stored and processed in Azure Cosmos DB.</span></span> <span data-ttu-id="513b7-145">Niemniej jednak bazy danych Azure rozwiązania Cosmos obsługuje tylko, automatycznego indeksowania punktów.</span><span class="sxs-lookup"><span data-stu-id="513b7-145">However Azure Cosmos DB only supports automatic indexing of points.</span></span>

### <a name="coordinate-reference-systems"></a><span data-ttu-id="513b7-146">Koordynacji systemów odniesienia</span><span class="sxs-lookup"><span data-stu-id="513b7-146">Coordinate reference systems</span></span>
<span data-ttu-id="513b7-147">Ponieważ kształtu hello ziemi hello jest nieprawidłowa, współrzędne geograficzne danych jest reprezentowana w wielu systemach współrzędnych odwołania (znaki CR), każdy z ramek odniesienia i jednostki miary.</span><span class="sxs-lookup"><span data-stu-id="513b7-147">Since hello shape of hello earth is irregular, coordinates of geospatial data is represented in many coordinate reference systems (CRS), each with their own frames of reference and units of measurement.</span></span> <span data-ttu-id="513b7-148">Na przykład "National siatki Brytania" hello jest systemu odniesienia są bardzo dokładne na brytyjski hello, ale nie poza nią.</span><span class="sxs-lookup"><span data-stu-id="513b7-148">For example, hello "National Grid of Britain" is a reference system is very accurate for hello United Kingdom, but not outside it.</span></span> 

<span data-ttu-id="513b7-149">Witaj najpopularniejszych używany obecnie jest hello World geodezyjnej systemu [WGS 84](http://earth-info.nga.mil/GandG/wgs84/).</span><span class="sxs-lookup"><span data-stu-id="513b7-149">hello most popular CRS in use today is hello World Geodetic System  [WGS-84](http://earth-info.nga.mil/GandG/wgs84/).</span></span> <span data-ttu-id="513b7-150">Urządzenia GPS, a wiele usług mapowania tym map programu Google i interfejsów API map Bing Użyj WGS 84.</span><span class="sxs-lookup"><span data-stu-id="513b7-150">GPS devices, and many mapping services including Google Maps and Bing Maps APIs use WGS-84.</span></span> <span data-ttu-id="513b7-151">Azure DB rozwiązania Cosmos obsługuje indeksowanie i wyszukiwanie przy użyciu hello CRS WGS 84 tylko dane geograficzne.</span><span class="sxs-lookup"><span data-stu-id="513b7-151">Azure Cosmos DB supports indexing and querying of geospatial data using hello WGS-84 CRS only.</span></span> 

## <a name="creating-documents-with-spatial-data"></a><span data-ttu-id="513b7-152">Tworzenie dokumentów z danymi przestrzennymi</span><span class="sxs-lookup"><span data-stu-id="513b7-152">Creating documents with spatial data</span></span>
<span data-ttu-id="513b7-153">Podczas tworzenia dokumentów, które zawierają wartości GeoJSON, są one automatycznie indeksowane z indeksu przestrzennego w zasadach indeksowania toohello zgodnie z kolekcji hello.</span><span class="sxs-lookup"><span data-stu-id="513b7-153">When you create documents that contain GeoJSON values, they are automatically indexed with a spatial index in accordance toohello indexing policy of hello collection.</span></span> <span data-ttu-id="513b7-154">Podczas pracy z zestawem Azure rozwiązania Cosmos DB SDK w typach określanych dynamicznie języka Python lub Node.js, należy utworzyć prawidłowy GeoJSON.</span><span class="sxs-lookup"><span data-stu-id="513b7-154">If you're working with an Azure Cosmos DB SDK in a dynamically typed language like Python or Node.js, you must create valid GeoJSON.</span></span>

<span data-ttu-id="513b7-155">**Utwórz dokument z dane geograficzne w środowisku Node.js**</span><span class="sxs-lookup"><span data-stu-id="513b7-155">**Create Document with Geospatial data in Node.js**</span></span>

```json
var userProfileDocument = {
    "name":"documentdb",
    "location":{
        "type":"Point",
        "coordinates":[ -122.12, 47.66 ]
    }
};

client.createDocument(`dbs/${databaseName}/colls/${collectionName}`, userProfileDocument, (err, created) => {
    // additional code within hello callback
});
```

<span data-ttu-id="513b7-156">Jeśli pracujesz z hello interfejsów API usługi DocumentDB, można użyć hello `Point` i `Polygon` klas w ramach hello `Microsoft.Azure.Documents.Spatial` informacji o lokalizacji tooembed przestrzeni nazw w obrębie obiektów aplikacji.</span><span class="sxs-lookup"><span data-stu-id="513b7-156">If you're working with hello DocumentDB APIs, you can use hello `Point` and `Polygon` classes within hello `Microsoft.Azure.Documents.Spatial` namespace tooembed location information within your application objects.</span></span> <span data-ttu-id="513b7-157">Te klasy ułatwić hello serializacji i deserializacji danych przestrzennych w GeoJSON.</span><span class="sxs-lookup"><span data-stu-id="513b7-157">These classes help simplify hello serialization and deserialization of spatial data into GeoJSON.</span></span>

<span data-ttu-id="513b7-158">**Utwórz dokument z dane geograficzne w .NET**</span><span class="sxs-lookup"><span data-stu-id="513b7-158">**Create Document with Geospatial data in .NET**</span></span>

```json
using Microsoft.Azure.Documents.Spatial;

public class UserProfile
{
    [JsonProperty("name")]
    public string Name { get; set; }

    [JsonProperty("location")]
    public Point Location { get; set; }

    // More properties
}

await client.CreateDocumentAsync(
    UriFactory.CreateDocumentCollectionUri("db", "profiles"), 
    new UserProfile 
    { 
        Name = "documentdb", 
        Location = new Point (-122.12, 47.66) 
    });
```

<span data-ttu-id="513b7-159">Jeśli nie ma informacji hello współrzędne geograficzne, ale ma hello adresów fizycznych ani nazwy lokalizacji, takiej jak nazwa miejscowości lub kraj, rzeczywiste współrzędne hello można wyszukiwać za pomocą usług geokodowanie, takich jak usługi REST mapy Bing.</span><span class="sxs-lookup"><span data-stu-id="513b7-159">If you don't have hello latitude and longitude information, but have hello physical addresses or location name like city or country, you can look up hello actual coordinates by using a geocoding service like Bing Maps REST Services.</span></span> <span data-ttu-id="513b7-160">Więcej informacji na temat usługi mapy Bing geokodowanie [tutaj](https://msdn.microsoft.com/library/ff701713.aspx).</span><span class="sxs-lookup"><span data-stu-id="513b7-160">Learn more about Bing Maps geocoding [here](https://msdn.microsoft.com/library/ff701713.aspx).</span></span>

## <a name="querying-spatial-types"></a><span data-ttu-id="513b7-161">Wykonywanie zapytania typów przestrzennych</span><span class="sxs-lookup"><span data-stu-id="513b7-161">Querying spatial types</span></span>
<span data-ttu-id="513b7-162">Teraz, gdy firma Microsoft zajęło przyjrzeć się jak dane geograficzne tooinsert, Spójrzmy na jak tooquery te dane przy użyciu bazy danych rozwiązania Cosmos Azure przy użyciu programu SQL i LINQ.</span><span class="sxs-lookup"><span data-stu-id="513b7-162">Now that we've taken a look at how tooinsert geospatial data, let's take a look at how tooquery this data using Azure Cosmos DB using SQL and LINQ.</span></span>

### <a name="spatial-sql-built-in-functions"></a><span data-ttu-id="513b7-163">Przestrzenne wbudowanych funkcji SQL</span><span class="sxs-lookup"><span data-stu-id="513b7-163">Spatial SQL built-in functions</span></span>
<span data-ttu-id="513b7-164">Azure DB rozwiązania Cosmos obsługuje hello następujące funkcje wbudowane Otwórz geograficzne konsorcjum (OGC) na potrzeby zapytań o dane geograficzne.</span><span class="sxs-lookup"><span data-stu-id="513b7-164">Azure Cosmos DB supports hello following Open Geospatial Consortium (OGC) built-in functions for geospatial querying.</span></span> <span data-ttu-id="513b7-165">Więcej szczegółów na powitania pełnego zestawu funkcji wbudowanych hello języka SQL, zobacz zbyt[kwerendy bazy danych z rozwiązania Cosmos Azure](documentdb-sql-query.md).</span><span class="sxs-lookup"><span data-stu-id="513b7-165">For more details on hello complete set of built-in functions in hello SQL language, please refer too[Query Azure Cosmos DB](documentdb-sql-query.md).</span></span>

<table>
<tr>
  <td><span data-ttu-id="513b7-166"><strong>Użycie</strong></span><span class="sxs-lookup"><span data-stu-id="513b7-166"><strong>Usage</strong></span></span></td>
  <td><span data-ttu-id="513b7-167"><strong>Opis</strong></span><span class="sxs-lookup"><span data-stu-id="513b7-167"><strong>Description</strong></span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="513b7-168">ST_DISTANCE (spatial_expr, spatial_expr)</span><span class="sxs-lookup"><span data-stu-id="513b7-168">ST_DISTANCE (spatial_expr, spatial_expr)</span></span></td>
  <td><span data-ttu-id="513b7-169">Zwraca hello odległość między hello dwóch wyrażeń GeoJSON punktu wielokąta i LineString.</span><span class="sxs-lookup"><span data-stu-id="513b7-169">Returns hello distance between hello two GeoJSON Point, Polygon, or LineString expressions.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="513b7-170">ST_WITHIN (spatial_expr, spatial_expr)</span><span class="sxs-lookup"><span data-stu-id="513b7-170">ST_WITHIN (spatial_expr, spatial_expr)</span></span></td>
  <td><span data-ttu-id="513b7-171">Zwraca wyrażenie logiczne, wskazującą, czy hello pierwszego obiektu GeoJSON (punkt, wielokąta lub LineString) jest w obrębie hello drugiego obiektu GeoJSON (punkt, wielokąta lub LineString).</span><span class="sxs-lookup"><span data-stu-id="513b7-171">Returns a Boolean expression indicating whether hello first GeoJSON object (Point, Polygon, or LineString) is within hello second GeoJSON object (Point, Polygon, or LineString).</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="513b7-172">ST_INTERSECTS (spatial_expr, spatial_expr)</span><span class="sxs-lookup"><span data-stu-id="513b7-172">ST_INTERSECTS (spatial_expr, spatial_expr)</span></span></td>
  <td><span data-ttu-id="513b7-173">Zwraca wyrażenie logiczne, wskazującą, czy intersect hello dwóch określonych GeoJSON obiektów (punkt, wielokąta lub LineString).</span><span class="sxs-lookup"><span data-stu-id="513b7-173">Returns a Boolean expression indicating whether hello two specified GeoJSON objects (Point, Polygon, or LineString) intersect.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="513b7-174">ST_ISVALID</span><span class="sxs-lookup"><span data-stu-id="513b7-174">ST_ISVALID</span></span></td>
  <td><span data-ttu-id="513b7-175">Zwraca wartość logiczną wskazującą, czy określono hello wyrażenie GeoJSON punktu wielokąta i LineString jest nieprawidłowy.</span><span class="sxs-lookup"><span data-stu-id="513b7-175">Returns a Boolean value indicating whether hello specified GeoJSON Point, Polygon, or LineString expression is valid.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="513b7-176">ST_ISVALIDDETAILED</span><span class="sxs-lookup"><span data-stu-id="513b7-176">ST_ISVALIDDETAILED</span></span></td>
  <td><span data-ttu-id="513b7-177">Zwraca wartość JSON zawierający wartość logiczna, jeśli hello określone wyrażenie GeoJSON punktu wielokąta i LineString jest prawidłowy, a jeśli jest nieprawidłowy, ponadto hello Przyczyna jako wartość typu ciąg.</span><span class="sxs-lookup"><span data-stu-id="513b7-177">Returns a JSON value containing a Boolean value if hello specified GeoJSON Point, Polygon, or LineString expression is valid, and if invalid, additionally hello reason as a string value.</span></span></td>
</tr>
</table>

<span data-ttu-id="513b7-178">Funkcje przestrzenne mogą być używane tooperform zbliżeniowe zapytań dotyczących danych przestrzennych.</span><span class="sxs-lookup"><span data-stu-id="513b7-178">Spatial functions can be used tooperform proximity queries against spatial data.</span></span> <span data-ttu-id="513b7-179">Na przykład w tym miejscu jest kwerendę, która zwraca rodziny wszystkie dokumenty, czy są w ciągu 30 km hello określonej lokalizacji przy użyciu wbudowanych funkcji ST_DISTANCE hello.</span><span class="sxs-lookup"><span data-stu-id="513b7-179">For example, here's a query that returns all family documents that are within 30 km of hello specified location using hello ST_DISTANCE built-in function.</span></span> 

<span data-ttu-id="513b7-180">**Zapytanie**</span><span class="sxs-lookup"><span data-stu-id="513b7-180">**Query**</span></span>

    SELECT f.id 
    FROM Families f 
    WHERE ST_DISTANCE(f.location, {'type': 'Point', 'coordinates':[31.9, -4.8]}) < 30000

<span data-ttu-id="513b7-181">**Wyniki**</span><span class="sxs-lookup"><span data-stu-id="513b7-181">**Results**</span></span>

    [{
      "id": "WakefieldFamily"
    }]

<span data-ttu-id="513b7-182">Jeśli dołączysz przestrzennych indeksowania w zasady indeksowania, następnie "odległość zapytania" zostanie obsłużona wydajnie za pomocą hello indeksu.</span><span class="sxs-lookup"><span data-stu-id="513b7-182">If you include spatial indexing in your indexing policy, then "distance queries" will be served efficiently through hello index.</span></span> <span data-ttu-id="513b7-183">Więcej szczegółów na indeksowanie przestrzennych zobacz sekcję hello poniżej.</span><span class="sxs-lookup"><span data-stu-id="513b7-183">For more details on spatial indexing, please see hello section below.</span></span> <span data-ttu-id="513b7-184">Jeśli nie masz przestrzennych indeks hello określonych ścieżek, można wykonywać zapytania przestrzennych, określając `x-ms-documentdb-query-enable-scan` nagłówek żądania z hello wartość ustawiona zbyt "true".</span><span class="sxs-lookup"><span data-stu-id="513b7-184">If you don't have a spatial index for hello specified paths, you can still perform spatial queries by specifying `x-ms-documentdb-query-enable-scan` request header with hello value set too"true".</span></span> <span data-ttu-id="513b7-185">W środowisku .NET, można to zrobić przez przekazanie hello opcjonalne **FeedOptions** tooqueries argumentu z [EnableScanInQuery](https://msdn.microsoft.com/library/microsoft.azure.documents.client.feedoptions.enablescaninquery.aspx#P:Microsoft.Azure.Documents.Client.FeedOptions.EnableScanInQuery) ustawić tootrue.</span><span class="sxs-lookup"><span data-stu-id="513b7-185">In .NET, this can be done by passing hello optional **FeedOptions** argument tooqueries with [EnableScanInQuery](https://msdn.microsoft.com/library/microsoft.azure.documents.client.feedoptions.enablescaninquery.aspx#P:Microsoft.Azure.Documents.Client.FeedOptions.EnableScanInQuery) set tootrue.</span></span> 

<span data-ttu-id="513b7-186">ST_WITHIN mogą być używane toocheck punkt znajduje się wewnątrz wielokąta.</span><span class="sxs-lookup"><span data-stu-id="513b7-186">ST_WITHIN can be used toocheck if a point lies within a Polygon.</span></span> <span data-ttu-id="513b7-187">Często wielokątów są granicami toorepresent używanych kodów pocztowych, stan granice lub tworzenie fizycznych.</span><span class="sxs-lookup"><span data-stu-id="513b7-187">Commonly Polygons are used toorepresent boundaries like zip codes, state boundaries, or natural formations.</span></span> <span data-ttu-id="513b7-188">Ponownie Jeśli przestrzennych indeksowania w zasady indeksowania, następnie "w" zapytania zostanie obsłużona wydajnie za pomocą hello indeksu.</span><span class="sxs-lookup"><span data-stu-id="513b7-188">Again if you include spatial indexing in your indexing policy, then "within" queries will be served efficiently through hello index.</span></span> 

<span data-ttu-id="513b7-189">Argumenty wielokąta ST_WITHIN może zawierać tylko jeden pierścień, tj. hello wielokątów nie może zawierać luk w nich.</span><span class="sxs-lookup"><span data-stu-id="513b7-189">Polygon arguments in ST_WITHIN can contain only a single ring, i.e. hello Polygons must not contain holes in them.</span></span> 

<span data-ttu-id="513b7-190">**Zapytanie**</span><span class="sxs-lookup"><span data-stu-id="513b7-190">**Query**</span></span>

    SELECT * 
    FROM Families f 
    WHERE ST_WITHIN(f.location, {
        'type':'Polygon', 
        'coordinates': [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]
    })

<span data-ttu-id="513b7-191">**Wyniki**</span><span class="sxs-lookup"><span data-stu-id="513b7-191">**Results**</span></span>

    [{
      "id": "WakefieldFamily",
    }]

> [!NOTE]
> <span data-ttu-id="513b7-192">Podobnych typów toohow niezgodne działa w zapytaniu bazy danych rozwiązania Cosmos Azure, jeśli wartość lokalizacji hello określony w albo argument jest źle sformułowany lub nieprawidłowy, a następnie będą oceniać za**Niezdefiniowany** i toobe dokumentu hello obliczone pominięte z hello wyniki zapytania.</span><span class="sxs-lookup"><span data-stu-id="513b7-192">Similar toohow mismatched types works in Azure Cosmos DB query, if hello location value specified in either argument is malformed or invalid, then it will evaluate too**undefined** and hello evaluated document toobe skipped from hello query results.</span></span> <span data-ttu-id="513b7-193">Jeśli zapytanie nie przynosi efektów, uruchom toodebug ST_ISVALIDDETAILED Dlaczego hello spatail typ jest nieprawidłowy.</span><span class="sxs-lookup"><span data-stu-id="513b7-193">If your query returns no results, run ST_ISVALIDDETAILED toodebug why hello spatail type is invalid.</span></span>     
> 
> 

<span data-ttu-id="513b7-194">Azure DB rozwiązania Cosmos obsługuje również wykonywania kwerend odwrotny, tj. Możesz indeksu wierszy w usłudze Azure DB rozwiązania Cosmos lub wielokątów, a następnie wyszukać hello obszarów, które zawierają określony punkt.</span><span class="sxs-lookup"><span data-stu-id="513b7-194">Azure Cosmos DB also supports performing inverse queries, i.e. you can index Polygons or lines in Azure Cosmos DB, then query for hello areas that contain a specified point.</span></span> <span data-ttu-id="513b7-195">Ten wzorzec jest często używana w tooidentify logistyki np. podczas ciężarówka wprowadza lub pozostawia wyznaczonego obszaru.</span><span class="sxs-lookup"><span data-stu-id="513b7-195">This pattern is commonly used in logistics tooidentify e.g. when a truck enters or leaves a designated area.</span></span> 

<span data-ttu-id="513b7-196">**Zapytanie**</span><span class="sxs-lookup"><span data-stu-id="513b7-196">**Query**</span></span>

    SELECT * 
    FROM Areas a 
    WHERE ST_WITHIN({'type': 'Point', 'coordinates':[31.9, -4.8]}, a.location)


<span data-ttu-id="513b7-197">**Wyniki**</span><span class="sxs-lookup"><span data-stu-id="513b7-197">**Results**</span></span>

    [{
      "id": "MyDesignatedLocation",
      "location": {
        "type":"Polygon", 
        "coordinates": [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]
      }
    }]

<span data-ttu-id="513b7-198">ST_ISVALID i ST_ISVALIDDETAILED mogą być toocheck używane, jeśli obiektu przestrzennego jest prawidłowy.</span><span class="sxs-lookup"><span data-stu-id="513b7-198">ST_ISVALID and ST_ISVALIDDETAILED can be used toocheck if a spatial object is valid.</span></span> <span data-ttu-id="513b7-199">Na przykład hello następującego zapytania sprawdza ważność hello punktu z poza zakresu wartości szerokości geograficznej (-132.8).</span><span class="sxs-lookup"><span data-stu-id="513b7-199">For example, hello following query checks hello validity of a point with an out of range latitude value (-132.8).</span></span> <span data-ttu-id="513b7-200">ST_ISVALID zwraca wartość logiczną, a zwraca ST_ISVALIDDETAILED hello logicznych i ciąg zawierający Przyczyna hello dlaczego jest uznawane za nieprawidłowe.</span><span class="sxs-lookup"><span data-stu-id="513b7-200">ST_ISVALID returns just a Boolean value, and ST_ISVALIDDETAILED returns hello Boolean and a string containing hello reason why it is considered invalid.</span></span>

<span data-ttu-id="513b7-201">** Zapytania **</span><span class="sxs-lookup"><span data-stu-id="513b7-201">** Query **</span></span>

    SELECT ST_ISVALID({ "type": "Point", "coordinates": [31.9, -132.8] })

<span data-ttu-id="513b7-202">**Wyniki**</span><span class="sxs-lookup"><span data-stu-id="513b7-202">**Results**</span></span>

    [{
      "$1": false
    }]

<span data-ttu-id="513b7-203">Te funkcje mogą być również używane toovalidate wielokątów.</span><span class="sxs-lookup"><span data-stu-id="513b7-203">These functions can also be used toovalidate Polygons.</span></span> <span data-ttu-id="513b7-204">Na przykład w tym miejscu używamy toovalidate ST_ISVALIDDETAILED wielokąta, który nie jest zamknięty.</span><span class="sxs-lookup"><span data-stu-id="513b7-204">For example, here we use ST_ISVALIDDETAILED toovalidate a Polygon that is not closed.</span></span> 

<span data-ttu-id="513b7-205">**Zapytanie**</span><span class="sxs-lookup"><span data-stu-id="513b7-205">**Query**</span></span>

    SELECT ST_ISVALIDDETAILED({ "type": "Polygon", "coordinates": [[ 
        [ 31.8, -5 ], [ 31.8, -4.7 ], [ 32, -4.7 ], [ 32, -5 ] 
        ]]})

<span data-ttu-id="513b7-206">**Wyniki**</span><span class="sxs-lookup"><span data-stu-id="513b7-206">**Results**</span></span>

    [{
       "$1": { 
            "valid": false, 
            "reason": "hello Polygon input is not valid because hello start and end points of hello ring number 1 are not hello same. Each ring of a Polygon must have hello same start and end points." 
          }
    }]

### <a name="linq-querying-in-hello-net-sdk"></a><span data-ttu-id="513b7-207">W hello zestawu .NET SDK zapytań LINQ</span><span class="sxs-lookup"><span data-stu-id="513b7-207">LINQ Querying in hello .NET SDK</span></span>
<span data-ttu-id="513b7-208">Witaj zestawu SDK .NET usługi DocumentDB również dostawców stub metody `Distance()` i `Within()` do użytku w wyrażenia LINQ.</span><span class="sxs-lookup"><span data-stu-id="513b7-208">hello DocumentDB .NET SDK also providers stub methods `Distance()` and `Within()` for use within LINQ expressions.</span></span> <span data-ttu-id="513b7-209">Witaj dostawcy DocumentDB LINQ tłumaczy tych wywołań toohello równoważne SQL wbudowanych funkcji wywołania metody (ST_DISTANCE i ST_WITHIN odpowiednio).</span><span class="sxs-lookup"><span data-stu-id="513b7-209">hello DocumentDB LINQ provider translates these method calls toohello equivalent SQL built-in function calls (ST_DISTANCE and ST_WITHIN respectively).</span></span> 

<span data-ttu-id="513b7-210">Oto przykład kwerendy LINQ znajduje wszystkie dokumenty w hello Azure DB rozwiązania Cosmos kolekcji o wartości "Lokalizacja" w ramach usługi radius 30 km hello określono punktu, przy użyciu LINQ.</span><span class="sxs-lookup"><span data-stu-id="513b7-210">Here's an example of a LINQ query that finds all documents in hello Azure Cosmos DB collection whose "location" value is within a radius of 30km of hello specified point using LINQ.</span></span>

<span data-ttu-id="513b7-211">**Zapytania LINQ odległość**</span><span class="sxs-lookup"><span data-stu-id="513b7-211">**LINQ query for Distance**</span></span>

    foreach (UserProfile user in client.CreateDocumentQuery<UserProfile>(UriFactory.CreateDocumentCollectionUri("db", "profiles"))
        .Where(u => u.ProfileType == "Public" && a.Location.Distance(new Point(32.33, -4.66)) < 30000))
    {
        Console.WriteLine("\t" + user);
    }

<span data-ttu-id="513b7-212">Podobnie w tym miejscu jest zapytania do znajdowania się, że wszystkie dokumenty hello, w których "Lokalizacja" znajduje się w hello określone pole/wielokąta.</span><span class="sxs-lookup"><span data-stu-id="513b7-212">Similarly, here's a query for finding all hello documents whose "location" is within hello specified box/Polygon.</span></span> 

<span data-ttu-id="513b7-213">**W ramach kwerendy LINQ**</span><span class="sxs-lookup"><span data-stu-id="513b7-213">**LINQ query for Within**</span></span>

    Polygon rectangularArea = new Polygon(
        new[]
        {
            new LinearRing(new [] {
                new Position(31.8, -5),
                new Position(32, -5),
                new Position(32, -4.7),
                new Position(31.8, -4.7),
                new Position(31.8, -5)
            })
        });

    foreach (UserProfile user in client.CreateDocumentQuery<UserProfile>(UriFactory.CreateDocumentCollectionUri("db", "profiles"))
        .Where(a => a.Location.Within(rectangularArea)))
    {
        Console.WriteLine("\t" + user);
    }


<span data-ttu-id="513b7-214">Teraz, gdy firma Microsoft zajęło przyjrzeć się jak tooquery dokumentów za pomocą LINQ i SQL, Spójrzmy na jak tooconfigure bazy danych Azure rozwiązania Cosmos przestrzennych indeksowania.</span><span class="sxs-lookup"><span data-stu-id="513b7-214">Now that we've taken a look at how tooquery documents using LINQ and SQL, let's take a look at how tooconfigure Azure Cosmos DB for spatial indexing.</span></span>

## <a name="indexing"></a><span data-ttu-id="513b7-215">Indeksowanie</span><span class="sxs-lookup"><span data-stu-id="513b7-215">Indexing</span></span>
<span data-ttu-id="513b7-216">Zgodnie z opisem możemy w hello [schematu niezależny od indeksowanie z bazy danych Azure rozwiązania Cosmos](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf) papier, możemy zaprojektowane toobe aparatu bazy danych DB rozwiązania Cosmos Azure rzeczywiście niezależny od schematu oraz zapewnić wsparcie pierwszej klasie dla formatu JSON.</span><span class="sxs-lookup"><span data-stu-id="513b7-216">As we described in hello [Schema Agnostic Indexing with Azure Cosmos DB](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf) paper, we designed Azure Cosmos DB’s database engine toobe truly schema agnostic and provide first class support for JSON.</span></span> <span data-ttu-id="513b7-217">Aparat bazy danych zoptymalizowanych pod kątem zapisu Hello Azure DB rozwiązania Cosmos rozumie natywnie danych przestrzennych (punkty, wielokątów i linii) reprezentowany w standardzie GeoJSON hello.</span><span class="sxs-lookup"><span data-stu-id="513b7-217">hello write optimized database engine of Azure Cosmos DB natively understands spatial data (points, Polygons and lines) represented in hello GeoJSON standard.</span></span>

<span data-ttu-id="513b7-218">Mówiąc, geometrii hello jest zaprojektowana geodezyjnej współrzędne na płaszczyźnie 2D, a następnie stopniowo podzielone komórki za pomocą **quadtree**.</span><span class="sxs-lookup"><span data-stu-id="513b7-218">In a nutshell, hello geometry is projected from geodetic coordinates onto a 2D plane then divided progressively into cells using a **quadtree**.</span></span> <span data-ttu-id="513b7-219">Te komórki są mapowane too1D na podstawie lokalizacji hello hello komórki znajdującej się w **Hilberta miejsca wypełnianie krzywej**, który zachowuje lokalizację punktów.</span><span class="sxs-lookup"><span data-stu-id="513b7-219">These cells are mapped too1D based on hello location of hello cell within a **Hilbert space filling curve**, which preserves locality of points.</span></span> <span data-ttu-id="513b7-220">Ponadto gdy danych lokalizacji jest indeksowany, przechodzi ona przez proces znany jako **tworzenia mozaiki**, tj. wszystkie komórki hello, przecinających lokalizacji są zidentyfikowane i przechowywane jako klucze hello Azure DB rozwiązania Cosmos indeksu.</span><span class="sxs-lookup"><span data-stu-id="513b7-220">Additionally when location data is indexed, it goes through a process known as **tessellation**, i.e. all hello cells that intersect a location are identified and stored as keys in hello Azure Cosmos DB index.</span></span> <span data-ttu-id="513b7-221">Podczas przeszukiwania argumenty, np. punkty i wielokątów są również tesselowaną tooextract hello zakresów identyfikator odpowiedniego komórek, a następnie użyć danych tooretrieve z indeksu hello.</span><span class="sxs-lookup"><span data-stu-id="513b7-221">At query time, arguments like points and Polygons are also tessellated tooextract hello relevant cell ID ranges, then used tooretrieve data from hello index.</span></span>

<span data-ttu-id="513b7-222">Jeśli można określić zasady indeksowania, który zawiera indeks przestrzenny dla / * (wszystkie ścieżki), a następnie wszystkie punkty znaleziony w kolekcji hello są indeksowane wydajnych zapytań przestrzennych (ST_WITHIN i ST_DISTANCE).</span><span class="sxs-lookup"><span data-stu-id="513b7-222">If you specify an indexing policy that includes spatial index for /* (all paths), then all points found within hello collection are indexed for efficient spatial queries (ST_WITHIN and ST_DISTANCE).</span></span> <span data-ttu-id="513b7-223">Indeksy przestrzenne nie ma wartość precyzji i zawsze używaj domyślną wartość precyzji.</span><span class="sxs-lookup"><span data-stu-id="513b7-223">Spatial indexes do not have a precision value, and always use a default precision value.</span></span>

> [!NOTE]
> <span data-ttu-id="513b7-224">Obsługuje bazę danych systemu Azure rozwiązania Cosmos automatycznego indeksowania punktów, wielokątów i LineStrings</span><span class="sxs-lookup"><span data-stu-id="513b7-224">Azure Cosmos DB supports automatic indexing of Points, Polygons, and LineStrings</span></span>
> 
> 

<span data-ttu-id="513b7-225">Hello następujący fragment kodu JSON przedstawia zasady indeksowania z włączone indeksowanie przestrzennych, tj. indeks dowolnego punktu GeoJSON znaleziono w dokumentach do wykonywania zapytań przestrzennych.</span><span class="sxs-lookup"><span data-stu-id="513b7-225">hello following JSON snippet shows an indexing policy with spatial indexing enabled, i.e. index any GeoJSON point found within documents for spatial querying.</span></span> <span data-ttu-id="513b7-226">W przypadku modyfikowania hello indeksowania zasady za pomocą hello portalu Azure, można określić powitania po JSON do indeksowania tooenable zasad przestrzennych indeksowania w kolekcji.</span><span class="sxs-lookup"><span data-stu-id="513b7-226">If you are modifying hello indexing policy using hello Azure Portal, you can specify hello following JSON for indexing policy tooenable spatial indexing on your collection.</span></span>

<span data-ttu-id="513b7-227">**Kolekcja indeksowania zasad JSON z przestrzennym włączone punktów i wielokątów**</span><span class="sxs-lookup"><span data-stu-id="513b7-227">**Collection Indexing Policy JSON with Spatial enabled for points and Polygons**</span></span>

    {
       "automatic":true,
       "indexingMode":"Consistent",
       "includedPaths":[
          {
             "path":"/*",
             "indexes":[
                {
                   "kind":"Range",
                   "dataType":"String",
                   "precision":-1
                },
                {
                   "kind":"Range",
                   "dataType":"Number",
                   "precision":-1
                },
                {
                   "kind":"Spatial",
                   "dataType":"Point"
                },
                {
                   "kind":"Spatial",
                   "dataType":"Polygon"
                }                
             ]
          }
       ],
       "excludedPaths":[
       ]
    }

<span data-ttu-id="513b7-228">Oto fragment kodu w programie .NET, który pokazuje, jak toocreate kolekcji z przestrzennego indeksowania włączona dla wszystkich ścieżek zawierających punkty.</span><span class="sxs-lookup"><span data-stu-id="513b7-228">Here's a code snippet in .NET that shows how toocreate a collection with spatial indexing turned on for all paths containing points.</span></span> 

<span data-ttu-id="513b7-229">**Utwórz kolekcję z przestrzennego indeksowania**</span><span class="sxs-lookup"><span data-stu-id="513b7-229">**Create a collection with spatial indexing**</span></span>

    DocumentCollection spatialData = new DocumentCollection()
    spatialData.IndexingPolicy = new IndexingPolicy(new SpatialIndex(DataType.Point)); //override tooturn spatial on by default
    collection = await client.CreateDocumentCollectionAsync(UriFactory.CreateDatabaseUri("db"), spatialData);

<span data-ttu-id="513b7-230">A Oto, jak można zmodyfikować istniejący kolekcji tootake zaletą przestrzennych indeksowania za pośrednictwem punktów, które są przechowywane w dokumentach.</span><span class="sxs-lookup"><span data-stu-id="513b7-230">And here's how you can modify an existing collection tootake advantage of spatial indexing over any points that are stored within documents.</span></span>

<span data-ttu-id="513b7-231">**Zmodyfikuj istniejącą kolekcję z przestrzennego indeksowania**</span><span class="sxs-lookup"><span data-stu-id="513b7-231">**Modify an existing collection with spatial indexing**</span></span>

    Console.WriteLine("Updating collection with spatial indexing enabled in indexing policy...");
    collection.IndexingPolicy = new IndexingPolicy(new SpatialIndex(DataType.Point));
    await client.ReplaceDocumentCollectionAsync(collection);

    Console.WriteLine("Waiting for indexing toocomplete...");
    long indexTransformationProgress = 0;
    while (indexTransformationProgress < 100)
    {
        ResourceResponse<DocumentCollection> response = await client.ReadDocumentCollectionAsync(UriFactory.CreateDocumentCollectionUri("db", "coll"));
        indexTransformationProgress = response.IndexTransformationProgress;

        await Task.Delay(TimeSpan.FromSeconds(1));
    }

> [!NOTE]
> <span data-ttu-id="513b7-232">Jeśli lokalizacja hello GeoJSON wartość w dokumencie hello jest źle sformułowany lub nieprawidłowy, następnie go zostanie nie indeksowanie przestrzennych zapytań.</span><span class="sxs-lookup"><span data-stu-id="513b7-232">If hello location GeoJSON value within hello document is malformed or invalid, then it will not get indexed for spatial querying.</span></span> <span data-ttu-id="513b7-233">Można sprawdzić za pomocą ST_ISVALID i ST_ISVALIDDETAILED wartości lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="513b7-233">You can validate location values using ST_ISVALID and ST_ISVALIDDETAILED.</span></span>
> 
> <span data-ttu-id="513b7-234">Jeśli definicja kolekcja zawiera klucz partycji, indeksowania postępu przekształcenie nie został zgłoszony.</span><span class="sxs-lookup"><span data-stu-id="513b7-234">If your collection definition includes a partition key, indexing transformation progress is not reported.</span></span> 
> 
> 

## <a name="next-steps"></a><span data-ttu-id="513b7-235">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="513b7-235">Next steps</span></span>
<span data-ttu-id="513b7-236">Teraz, gdy zostały wcześniej o jak tooget pracę z obsługą dane geograficzne w usłudze Azure DB rozwiązania Cosmos, można wykonywać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="513b7-236">Now that you've learnt about how tooget started with geospatial support in Azure Cosmos DB, you can:</span></span>

* <span data-ttu-id="513b7-237">Rozpoczęcie kodowania z hello [przykłady kodu .NET dane geograficzne w witrynie GitHub](https://github.com/Azure/azure-documentdb-dotnet/blob/fcf23d134fc5019397dcf7ab97d8d6456cd94820/samples/code-samples/Geospatial/Program.cs)</span><span class="sxs-lookup"><span data-stu-id="513b7-237">Start coding with hello [Geospatial .NET code samples on GitHub](https://github.com/Azure/azure-documentdb-dotnet/blob/fcf23d134fc5019397dcf7ab97d8d6456cd94820/samples/code-samples/Geospatial/Program.cs)</span></span>
* <span data-ttu-id="513b7-238">Uzyskać ręce na z geograficzne zapytań na powitania [Plac zabaw dla Azure rozwiązania Cosmos DB zapytań](http://www.documentdb.com/sql/demo#geospatial)</span><span class="sxs-lookup"><span data-stu-id="513b7-238">Get hands on with geospatial querying at hello [Azure Cosmos DB Query Playground](http://www.documentdb.com/sql/demo#geospatial)</span></span>
* <span data-ttu-id="513b7-239">Dowiedz się więcej o [kwerendy bazy danych Azure rozwiązania Cosmos](documentdb-sql-query.md)</span><span class="sxs-lookup"><span data-stu-id="513b7-239">Learn more about [Azure Cosmos DB Query](documentdb-sql-query.md)</span></span>
* <span data-ttu-id="513b7-240">Dowiedz się więcej o [zasady indeksowania bazy danych Azure rozwiązania Cosmos](indexing-policies.md)</span><span class="sxs-lookup"><span data-stu-id="513b7-240">Learn more about [Azure Cosmos DB Indexing Policies](indexing-policies.md)</span></span>

