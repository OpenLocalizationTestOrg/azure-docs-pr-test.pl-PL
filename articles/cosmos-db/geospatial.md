---
title: "Praca z danymi dane geograficzne w usłudze Azure DB rozwiązania Cosmos | Dokumentacja firmy Microsoft"
description: "Zrozumienie sposobu tworzenia, indeksu i zapytania przestrzennych obiektów z bazy danych rozwiązania Cosmos Azure i interfejsu API usługi DocumentDB."
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
ms.openlocfilehash: d5785c81fb597e7d30eb7d3a880e7194d8358ed5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="working-with-geospatial-and-geojson-location-data-in-azure-cosmos-db"></a><span data-ttu-id="08ab0-103">Praca z dane geograficzne i danych lokalizacji GeoJSON w usłudze Azure DB rozwiązania Cosmos</span><span class="sxs-lookup"><span data-stu-id="08ab0-103">Working with geospatial and GeoJSON location data in Azure Cosmos DB</span></span>
<span data-ttu-id="08ab0-104">Ten artykuł obejmuje wprowadzenie do funkcji geograficzne w [bazy danych Azure rozwiązania Cosmos](https://azure.microsoft.com/services/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="08ab0-104">This article is an introduction to the geospatial functionality in [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span></span> <span data-ttu-id="08ab0-105">Po przeczytaniu tego, będzie mógł odpowiedzieć na następujące pytania:</span><span class="sxs-lookup"><span data-stu-id="08ab0-105">After reading this, you will be able to answer the following questions:</span></span>

* <span data-ttu-id="08ab0-106">Sposób przechowywania danych przestrzennych w usłudze Azure DB rozwiązania Cosmos?</span><span class="sxs-lookup"><span data-stu-id="08ab0-106">How do I store spatial data in Azure Cosmos DB?</span></span>
* <span data-ttu-id="08ab0-107">Jak wykonać zapytanie dane geograficzne w usłudze Azure DB rozwiązania Cosmos w SQL i LINQ</span><span class="sxs-lookup"><span data-stu-id="08ab0-107">How can I query geospatial data in Azure Cosmos DB in SQL and LINQ?</span></span>
* <span data-ttu-id="08ab0-108">Jak włączyć lub wyłączyć indeksowanie przestrzenne w usłudze Azure DB rozwiązania Cosmos</span><span class="sxs-lookup"><span data-stu-id="08ab0-108">How do I enable or disable spatial indexing in Azure Cosmos DB?</span></span>

<span data-ttu-id="08ab0-109">W tym artykule przedstawiono sposób pracy z danymi przestrzennymi przy użyciu interfejsu API usługi DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="08ab0-109">This article shows how to work with spatial data with the DocumentDB API.</span></span> <span data-ttu-id="08ab0-110">Zobacz to [projektu GitHub](https://github.com/Azure/azure-documentdb-dotnet/blob/master/samples/code-samples/Geospatial/Program.cs) dla przykładów kodu.</span><span class="sxs-lookup"><span data-stu-id="08ab0-110">Please see this [GitHub project](https://github.com/Azure/azure-documentdb-dotnet/blob/master/samples/code-samples/Geospatial/Program.cs) for code samples.</span></span>

## <a name="introduction-to-spatial-data"></a><span data-ttu-id="08ab0-111">Wprowadzenie do danych przestrzennych</span><span class="sxs-lookup"><span data-stu-id="08ab0-111">Introduction to spatial data</span></span>
<span data-ttu-id="08ab0-112">Dane przestrzenne opisano pozycji i kształt obiektów w przestrzeni.</span><span class="sxs-lookup"><span data-stu-id="08ab0-112">Spatial data describes the position and shape of objects in space.</span></span> <span data-ttu-id="08ab0-113">W większości aplikacji odpowiadają one obiekty powierzchni ziemi, tj. dane geograficzne.</span><span class="sxs-lookup"><span data-stu-id="08ab0-113">In most applications, these correspond to objects on the earth, i.e. geospatial data.</span></span> <span data-ttu-id="08ab0-114">Dane przestrzenne może służyć do reprezentowania lokalizacji osoby, miejsca lub granic miejscowości lub jeziora.</span><span class="sxs-lookup"><span data-stu-id="08ab0-114">Spatial data can be used to represent the location of a person, a place of interest, or the boundary of a city, or a lake.</span></span> <span data-ttu-id="08ab0-115">Typowe przypadki użycia obejmują często zbliżeniowe zapytań, dotyczących np. "Znajdź wszystkie kawiarniach niemal mojej bieżącej lokalizacji".</span><span class="sxs-lookup"><span data-stu-id="08ab0-115">Common use cases often involve proximity queries, for e.g., "find all coffee shops near my current location".</span></span> 

### <a name="geojson"></a><span data-ttu-id="08ab0-116">GeoJSON</span><span class="sxs-lookup"><span data-stu-id="08ab0-116">GeoJSON</span></span>
<span data-ttu-id="08ab0-117">Azure DB rozwiązania Cosmos obsługuje indeksowanie i badania dane geograficzne punktu danych, które ma reprezentowanej przy użyciu [specyfikacji GeoJSON](https://tools.ietf.org/html/rfc7946).</span><span class="sxs-lookup"><span data-stu-id="08ab0-117">Azure Cosmos DB supports indexing and querying of geospatial point data that's represented using the [GeoJSON specification](https://tools.ietf.org/html/rfc7946).</span></span> <span data-ttu-id="08ab0-118">Struktury danych GeoJSON są zawsze prawidłowych obiektów JSON, dzięki czemu mogą być przechowywane i wyświetlić przy użyciu bazy danych Azure rozwiązania Cosmos bez żadnych specjalnych narzędzi i bibliotek.</span><span class="sxs-lookup"><span data-stu-id="08ab0-118">GeoJSON data structures are always valid JSON objects, so they can be stored and queried using Azure Cosmos DB without any specialized tools or libraries.</span></span> <span data-ttu-id="08ab0-119">Zestawy SDK Azure rozwiązania Cosmos DB Podaj pomocnika klasy i metody, które ułatwiają pracę z danymi przestrzennymi.</span><span class="sxs-lookup"><span data-stu-id="08ab0-119">The Azure Cosmos DB SDKs provide helper classes and methods that make it easy to work with spatial data.</span></span> 

### <a name="points-linestrings-and-polygons"></a><span data-ttu-id="08ab0-120">Punkty, LineStrings i wielokątów</span><span class="sxs-lookup"><span data-stu-id="08ab0-120">Points, LineStrings and Polygons</span></span>
<span data-ttu-id="08ab0-121">A **punktu** oznacza pojedynczego pozycję w przestrzeni.</span><span class="sxs-lookup"><span data-stu-id="08ab0-121">A **Point** denotes a single position in space.</span></span> <span data-ttu-id="08ab0-122">W danych geograficznych punkt reprezentuje dokładnej lokalizacji, która może być ulicę sklepów spożywczych, kiosku, samochodu lub miejscowości.</span><span class="sxs-lookup"><span data-stu-id="08ab0-122">In geospatial data, a Point represents the exact location, which could be a street address of a grocery store, a kiosk, an automobile or a city.</span></span>  <span data-ttu-id="08ab0-123">Punkt jest reprezentowana w pary GeoJSON (i bazy danych Azure rozwiązania Cosmos) przy użyciu jego współrzędnych lub długości i szerokości geograficznej.</span><span class="sxs-lookup"><span data-stu-id="08ab0-123">A point is represented in GeoJSON (and Azure Cosmos DB) using its coordinate pair or longitude and latitude.</span></span> <span data-ttu-id="08ab0-124">Oto przykład JSON dla punktu.</span><span class="sxs-lookup"><span data-stu-id="08ab0-124">Here's an example JSON for a point.</span></span>

<span data-ttu-id="08ab0-125">**Punkty Azure rozwiązania Cosmos bazy danych**</span><span class="sxs-lookup"><span data-stu-id="08ab0-125">**Points in Azure Cosmos DB**</span></span>

```json
{
    "type":"Point",
    "coordinates":[ 31.9, -4.8 ]
}
```

> [!NOTE]
> <span data-ttu-id="08ab0-126">Specyfikacja GeoJSON określa długość pierwszy i szerokości geograficznej drugiego.</span><span class="sxs-lookup"><span data-stu-id="08ab0-126">The GeoJSON specification specifies longitude first and latitude second.</span></span> <span data-ttu-id="08ab0-127">Podobnie jak w innych aplikacjach mapowania długości i szerokości geograficznej są kąty i wyświetlany w postaci stopni.</span><span class="sxs-lookup"><span data-stu-id="08ab0-127">Like in other mapping applications, longitude and latitude are angles and represented in terms of degrees.</span></span> <span data-ttu-id="08ab0-128">Wartości długości geograficznej są mierzone od głównego południka i należą do zakresu od- i 180.0 stopni, 180 do szerokości geograficznej wartości są mierzone od równika i należą do zakresu od-90.0 i 90.0 stopni.</span><span class="sxs-lookup"><span data-stu-id="08ab0-128">Longitude values are measured from the Prime Meridian and are between -180 and 180.0 degrees, and latitude values are measured from the equator and are between -90.0 and 90.0 degrees.</span></span> 
> 
> <span data-ttu-id="08ab0-129">Azure DB rozwiązania Cosmos interpretuje współrzędne reprezentowane na WGS 84 systemu odniesienia.</span><span class="sxs-lookup"><span data-stu-id="08ab0-129">Azure Cosmos DB interprets coordinates as represented per the WGS-84 reference system.</span></span> <span data-ttu-id="08ab0-130">Zobacz poniżej więcej szczegółów dotyczących systemów współrzędnych odwołania.</span><span class="sxs-lookup"><span data-stu-id="08ab0-130">Please see below for more details about coordinate reference systems.</span></span>
> 
> 

<span data-ttu-id="08ab0-131">Można ją osadzić w dokumencie bazy danych Azure rozwiązania Cosmos opisane w tym przykładzie profilu użytkownika zawierającego dane dotyczące lokalizacji:</span><span class="sxs-lookup"><span data-stu-id="08ab0-131">This can be embedded in an Azure Cosmos DB document as shown in this example of a user profile containing location data:</span></span>

<span data-ttu-id="08ab0-132">**Użyj profilu z lokalizacją przechowywane w usłudze Azure DB rozwiązania Cosmos**</span><span class="sxs-lookup"><span data-stu-id="08ab0-132">**Use Profile with Location stored in Azure Cosmos DB**</span></span>

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

<span data-ttu-id="08ab0-133">Oprócz punktów GeoJSON obsługuje również LineStrings i wielokątów.</span><span class="sxs-lookup"><span data-stu-id="08ab0-133">In addition to points, GeoJSON also supports LineStrings and Polygons.</span></span> <span data-ttu-id="08ab0-134">**LineStrings** reprezentują dwa lub więcej punktów w miejsce i segmentów, które łączą te elementy.</span><span class="sxs-lookup"><span data-stu-id="08ab0-134">**LineStrings** represent a series of two or more points in space and the line segments that connect them.</span></span> <span data-ttu-id="08ab0-135">W polu dane geograficzne LineStrings często są używane do reprezentowania drogami lub rzek.</span><span class="sxs-lookup"><span data-stu-id="08ab0-135">In geospatial data, LineStrings are commonly used to represent highways or rivers.</span></span> <span data-ttu-id="08ab0-136">A **wielokąta** jest granicę punktów połączonych formularzy LineString zamknięte.</span><span class="sxs-lookup"><span data-stu-id="08ab0-136">A **Polygon** is a boundary of connected points that forms a closed LineString.</span></span> <span data-ttu-id="08ab0-137">Wielokąty często są używane do reprezentowania tworzenie fizycznych, takich jak jeziora lub polityczną jurysdykcjach przykład miast i stanów.</span><span class="sxs-lookup"><span data-stu-id="08ab0-137">Polygons are commonly used to represent natural formations like lakes or political jurisdictions like cities and states.</span></span> <span data-ttu-id="08ab0-138">Oto przykład wielokąta w usłudze Azure DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="08ab0-138">Here's an example of a Polygon in Azure Cosmos DB.</span></span> 

<span data-ttu-id="08ab0-139">**Wielokąty w GeoJSON**</span><span class="sxs-lookup"><span data-stu-id="08ab0-139">**Polygons in GeoJSON**</span></span>

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
> <span data-ttu-id="08ab0-140">Specyfikacja GeoJSON wymaga, aby uzyskać prawidłowy wielokątów ostatnią parę współrzędnych podane powinien taka sama jak pierwsza strona, aby utworzyć zamknięty kształt.</span><span class="sxs-lookup"><span data-stu-id="08ab0-140">The GeoJSON specification requires that for valid Polygons, the last coordinate pair provided should be the same as the first, to create a closed shape.</span></span>
> 
> <span data-ttu-id="08ab0-141">Punktów w wielokąta muszą być określone w kolejności przeciwnie do ruchu wskazówek zegara.</span><span class="sxs-lookup"><span data-stu-id="08ab0-141">Points within a Polygon must be specified in counter-clockwise order.</span></span> <span data-ttu-id="08ab0-142">Wielokąt określony w kolejności zegara reprezentuje odwrotność regionu w niej.</span><span class="sxs-lookup"><span data-stu-id="08ab0-142">A Polygon specified in clockwise order represents the inverse of the region within it.</span></span>
> 
> 

<span data-ttu-id="08ab0-143">Oprócz i wielokąta punktu, LineString, GeoJSON określa również reprezentację sposób grupowania wielu lokalizacji geograficznych, a także sposobu kojarzenia dowolne właściwości z używanie funkcji geolokalizacji jako **funkcji**.</span><span class="sxs-lookup"><span data-stu-id="08ab0-143">In addition to Point, LineString and Polygon, GeoJSON also specifies the representation for how to group multiple geospatial locations, as well as how to associate arbitrary properties with geolocation as a **Feature**.</span></span> <span data-ttu-id="08ab0-144">Ponieważ te obiekty są poprawne dane JSON, ich można wszystkie przechowywane i przetwarzane w usłudze Azure DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="08ab0-144">Since these objects are valid JSON, they can all be stored and processed in Azure Cosmos DB.</span></span> <span data-ttu-id="08ab0-145">Niemniej jednak bazy danych Azure rozwiązania Cosmos obsługuje tylko, automatycznego indeksowania punktów.</span><span class="sxs-lookup"><span data-stu-id="08ab0-145">However Azure Cosmos DB only supports automatic indexing of points.</span></span>

### <a name="coordinate-reference-systems"></a><span data-ttu-id="08ab0-146">Koordynacji systemów odniesienia</span><span class="sxs-lookup"><span data-stu-id="08ab0-146">Coordinate reference systems</span></span>
<span data-ttu-id="08ab0-147">Ponieważ kształtu ziemi jest nieprawidłowa, współrzędne geograficzne danych jest reprezentowana w wielu systemach współrzędnych odwołania (znaki CR), każdy z ramek odniesienia i jednostki miary.</span><span class="sxs-lookup"><span data-stu-id="08ab0-147">Since the shape of the earth is irregular, coordinates of geospatial data is represented in many coordinate reference systems (CRS), each with their own frames of reference and units of measurement.</span></span> <span data-ttu-id="08ab0-148">Na przykład "National siatki z Brytania" jest systemu odniesienia są bardzo dokładne Zjednoczone Królestwo, ale nie poza nią.</span><span class="sxs-lookup"><span data-stu-id="08ab0-148">For example, the "National Grid of Britain" is a reference system is very accurate for the United Kingdom, but not outside it.</span></span> 

<span data-ttu-id="08ab0-149">Najbardziej popularnym używany obecnie jest System geodezyjny World [WGS 84](http://earth-info.nga.mil/GandG/wgs84/).</span><span class="sxs-lookup"><span data-stu-id="08ab0-149">The most popular CRS in use today is the World Geodetic System  [WGS-84](http://earth-info.nga.mil/GandG/wgs84/).</span></span> <span data-ttu-id="08ab0-150">Urządzenia GPS, a wiele usług mapowania tym map programu Google i interfejsów API map Bing Użyj WGS 84.</span><span class="sxs-lookup"><span data-stu-id="08ab0-150">GPS devices, and many mapping services including Google Maps and Bing Maps APIs use WGS-84.</span></span> <span data-ttu-id="08ab0-151">Azure DB rozwiązania Cosmos obsługuje indeksowanie i wyszukiwanie przy użyciu CRS WGS 84 w tylko dane geograficzne.</span><span class="sxs-lookup"><span data-stu-id="08ab0-151">Azure Cosmos DB supports indexing and querying of geospatial data using the WGS-84 CRS only.</span></span> 

## <a name="creating-documents-with-spatial-data"></a><span data-ttu-id="08ab0-152">Tworzenie dokumentów z danymi przestrzennymi</span><span class="sxs-lookup"><span data-stu-id="08ab0-152">Creating documents with spatial data</span></span>
<span data-ttu-id="08ab0-153">Podczas tworzenia dokumentów, które zawierają wartości GeoJSON one są automatycznie indeksowane z indeksu przestrzennego w zgodnie z zasadami indeksowania w kolekcji.</span><span class="sxs-lookup"><span data-stu-id="08ab0-153">When you create documents that contain GeoJSON values, they are automatically indexed with a spatial index in accordance to the indexing policy of the collection.</span></span> <span data-ttu-id="08ab0-154">Podczas pracy z zestawem Azure rozwiązania Cosmos DB SDK w typach określanych dynamicznie języka Python lub Node.js, należy utworzyć prawidłowy GeoJSON.</span><span class="sxs-lookup"><span data-stu-id="08ab0-154">If you're working with an Azure Cosmos DB SDK in a dynamically typed language like Python or Node.js, you must create valid GeoJSON.</span></span>

<span data-ttu-id="08ab0-155">**Utwórz dokument z dane geograficzne w środowisku Node.js**</span><span class="sxs-lookup"><span data-stu-id="08ab0-155">**Create Document with Geospatial data in Node.js**</span></span>

```json
var userProfileDocument = {
    "name":"documentdb",
    "location":{
        "type":"Point",
        "coordinates":[ -122.12, 47.66 ]
    }
};

client.createDocument(`dbs/${databaseName}/colls/${collectionName}`, userProfileDocument, (err, created) => {
    // additional code within the callback
});
```

<span data-ttu-id="08ab0-156">Jeśli pracujesz z interfejsami API usługi DocumentDB, możesz użyć `Point` i `Polygon` klas w ramach `Microsoft.Azure.Documents.Spatial` przestrzeni nazw osadzanie informacji o lokalizacji w obrębie obiektów aplikacji.</span><span class="sxs-lookup"><span data-stu-id="08ab0-156">If you're working with the DocumentDB APIs, you can use the `Point` and `Polygon` classes within the `Microsoft.Azure.Documents.Spatial` namespace to embed location information within your application objects.</span></span> <span data-ttu-id="08ab0-157">Te klasy ułatwić serializacji i deserializacji obiektu danych przestrzennych w GeoJSON.</span><span class="sxs-lookup"><span data-stu-id="08ab0-157">These classes help simplify the serialization and deserialization of spatial data into GeoJSON.</span></span>

<span data-ttu-id="08ab0-158">**Utwórz dokument z dane geograficzne w .NET**</span><span class="sxs-lookup"><span data-stu-id="08ab0-158">**Create Document with Geospatial data in .NET**</span></span>

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

<span data-ttu-id="08ab0-159">Jeśli nie ma informacji współrzędne geograficzne, ale ma adresów fizycznych ani nazwy lokalizacji, takiej jak nazwa miejscowości lub kraj, rzeczywiste współrzędne można wyszukiwać za pomocą usług geokodowanie, takich jak usługi REST mapy Bing.</span><span class="sxs-lookup"><span data-stu-id="08ab0-159">If you don't have the latitude and longitude information, but have the physical addresses or location name like city or country, you can look up the actual coordinates by using a geocoding service like Bing Maps REST Services.</span></span> <span data-ttu-id="08ab0-160">Więcej informacji na temat usługi mapy Bing geokodowanie [tutaj](https://msdn.microsoft.com/library/ff701713.aspx).</span><span class="sxs-lookup"><span data-stu-id="08ab0-160">Learn more about Bing Maps geocoding [here](https://msdn.microsoft.com/library/ff701713.aspx).</span></span>

## <a name="querying-spatial-types"></a><span data-ttu-id="08ab0-161">Wykonywanie zapytania typów przestrzennych</span><span class="sxs-lookup"><span data-stu-id="08ab0-161">Querying spatial types</span></span>
<span data-ttu-id="08ab0-162">Teraz, gdy firma Microsoft zajęło przyjrzeć się jak wstawić dane geograficzne, Spójrzmy na sposób tworzenia zapytań te dane przy użyciu bazy danych rozwiązania Cosmos Azure przy użyciu programu SQL i LINQ.</span><span class="sxs-lookup"><span data-stu-id="08ab0-162">Now that we've taken a look at how to insert geospatial data, let's take a look at how to query this data using Azure Cosmos DB using SQL and LINQ.</span></span>

### <a name="spatial-sql-built-in-functions"></a><span data-ttu-id="08ab0-163">Przestrzenne wbudowanych funkcji SQL</span><span class="sxs-lookup"><span data-stu-id="08ab0-163">Spatial SQL built-in functions</span></span>
<span data-ttu-id="08ab0-164">Azure DB rozwiązania Cosmos obsługuje następujące funkcje wbudowane Otwórz geograficzne konsorcjum (OGC) na potrzeby zapytań o dane geograficzne.</span><span class="sxs-lookup"><span data-stu-id="08ab0-164">Azure Cosmos DB supports the following Open Geospatial Consortium (OGC) built-in functions for geospatial querying.</span></span> <span data-ttu-id="08ab0-165">Więcej szczegółów na pełny zestaw funkcji wbudowanych w języku SQL, można znaleźć na stronie [kwerendy bazy danych z rozwiązania Cosmos Azure](documentdb-sql-query.md).</span><span class="sxs-lookup"><span data-stu-id="08ab0-165">For more details on the complete set of built-in functions in the SQL language, please refer to [Query Azure Cosmos DB](documentdb-sql-query.md).</span></span>

<table>
<tr>
  <td><span data-ttu-id="08ab0-166"><strong>Użycie</strong></span><span class="sxs-lookup"><span data-stu-id="08ab0-166"><strong>Usage</strong></span></span></td>
  <td><span data-ttu-id="08ab0-167"><strong>Opis</strong></span><span class="sxs-lookup"><span data-stu-id="08ab0-167"><strong>Description</strong></span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="08ab0-168">ST_DISTANCE (spatial_expr, spatial_expr)</span><span class="sxs-lookup"><span data-stu-id="08ab0-168">ST_DISTANCE (spatial_expr, spatial_expr)</span></span></td>
  <td><span data-ttu-id="08ab0-169">Zwraca odległość między dwoma wyrażeniami GeoJSON punktu wielokąta i LineString.</span><span class="sxs-lookup"><span data-stu-id="08ab0-169">Returns the distance between the two GeoJSON Point, Polygon, or LineString expressions.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="08ab0-170">ST_WITHIN (spatial_expr, spatial_expr)</span><span class="sxs-lookup"><span data-stu-id="08ab0-170">ST_WITHIN (spatial_expr, spatial_expr)</span></span></td>
  <td><span data-ttu-id="08ab0-171">Zwraca wyrażenie logiczne, wskazującą, czy pierwszy obiekt GeoJSON (punkt, wielokąta lub LineString) znajduje się w drugim obiektu GeoJSON (punkt, wielokąta lub LineString).</span><span class="sxs-lookup"><span data-stu-id="08ab0-171">Returns a Boolean expression indicating whether the first GeoJSON object (Point, Polygon, or LineString) is within the second GeoJSON object (Point, Polygon, or LineString).</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="08ab0-172">ST_INTERSECTS (spatial_expr, spatial_expr)</span><span class="sxs-lookup"><span data-stu-id="08ab0-172">ST_INTERSECTS (spatial_expr, spatial_expr)</span></span></td>
  <td><span data-ttu-id="08ab0-173">Zwraca wartość wskazującą, czy dwa określonych obiektów GeoJSON (punkt, wielokąta lub LineString) intersect wyrażenie logiczne.</span><span class="sxs-lookup"><span data-stu-id="08ab0-173">Returns a Boolean expression indicating whether the two specified GeoJSON objects (Point, Polygon, or LineString) intersect.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="08ab0-174">ST_ISVALID</span><span class="sxs-lookup"><span data-stu-id="08ab0-174">ST_ISVALID</span></span></td>
  <td><span data-ttu-id="08ab0-175">Zwraca wartość logiczną wskazującą, czy określone wyrażenie GeoJSON punktu wielokąta i LineString jest nieprawidłowy.</span><span class="sxs-lookup"><span data-stu-id="08ab0-175">Returns a Boolean value indicating whether the specified GeoJSON Point, Polygon, or LineString expression is valid.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="08ab0-176">ST_ISVALIDDETAILED</span><span class="sxs-lookup"><span data-stu-id="08ab0-176">ST_ISVALIDDETAILED</span></span></td>
  <td><span data-ttu-id="08ab0-177">Zwraca wartość wartość JSON, zawierające wartość typu Boolean, jeśli określone wyrażenie GeoJSON punktu wielokąta i LineString jest prawidłowy, a nieprawidłowy, ponadto Przyczyna jako wartość typu ciąg.</span><span class="sxs-lookup"><span data-stu-id="08ab0-177">Returns a JSON value containing a Boolean value if the specified GeoJSON Point, Polygon, or LineString expression is valid, and if invalid, additionally the reason as a string value.</span></span></td>
</tr>
</table>

<span data-ttu-id="08ab0-178">Funkcje przestrzenne może służyć do wykonywania zapytań zbliżeniowe względem danych przestrzennych.</span><span class="sxs-lookup"><span data-stu-id="08ab0-178">Spatial functions can be used to perform proximity queries against spatial data.</span></span> <span data-ttu-id="08ab0-179">Na przykład w tym miejscu jest kwerendę, która zwraca wszystkie dokumenty rodziny, które są w ciągu 30 km do określonej lokalizacji za pomocą wbudowanych funkcji ST_DISTANCE.</span><span class="sxs-lookup"><span data-stu-id="08ab0-179">For example, here's a query that returns all family documents that are within 30 km of the specified location using the ST_DISTANCE built-in function.</span></span> 

<span data-ttu-id="08ab0-180">**Zapytanie**</span><span class="sxs-lookup"><span data-stu-id="08ab0-180">**Query**</span></span>

    SELECT f.id 
    FROM Families f 
    WHERE ST_DISTANCE(f.location, {'type': 'Point', 'coordinates':[31.9, -4.8]}) < 30000

<span data-ttu-id="08ab0-181">**Wyniki**</span><span class="sxs-lookup"><span data-stu-id="08ab0-181">**Results**</span></span>

    [{
      "id": "WakefieldFamily"
    }]

<span data-ttu-id="08ab0-182">Jeśli dołączysz przestrzennych indeksowania w zasady indeksowania, następnie "odległość zapytania" zostanie obsłużona wydajnie przez indeks.</span><span class="sxs-lookup"><span data-stu-id="08ab0-182">If you include spatial indexing in your indexing policy, then "distance queries" will be served efficiently through the index.</span></span> <span data-ttu-id="08ab0-183">Więcej szczegółów na indeksowanie przestrzennych zobacz sekcję poniżej.</span><span class="sxs-lookup"><span data-stu-id="08ab0-183">For more details on spatial indexing, please see the section below.</span></span> <span data-ttu-id="08ab0-184">Jeśli nie masz indeks przestrzenny dla określonej ścieżki, można wykonywać zapytania przestrzennych, określając `x-ms-documentdb-query-enable-scan` nagłówek żądania z ustawioną wartość "true".</span><span class="sxs-lookup"><span data-stu-id="08ab0-184">If you don't have a spatial index for the specified paths, you can still perform spatial queries by specifying `x-ms-documentdb-query-enable-scan` request header with the value set to "true".</span></span> <span data-ttu-id="08ab0-185">W środowisku .NET, można to zrobić przez przekazanie opcjonalny **FeedOptions** argument zapytania z [EnableScanInQuery](https://msdn.microsoft.com/library/microsoft.azure.documents.client.feedoptions.enablescaninquery.aspx#P:Microsoft.Azure.Documents.Client.FeedOptions.EnableScanInQuery) ustawioną na true.</span><span class="sxs-lookup"><span data-stu-id="08ab0-185">In .NET, this can be done by passing the optional **FeedOptions** argument to queries with [EnableScanInQuery](https://msdn.microsoft.com/library/microsoft.azure.documents.client.feedoptions.enablescaninquery.aspx#P:Microsoft.Azure.Documents.Client.FeedOptions.EnableScanInQuery) set to true.</span></span> 

<span data-ttu-id="08ab0-186">ST_WITHIN może służyć do sprawdzenia, czy punkt znajduje się wewnątrz wielokąta.</span><span class="sxs-lookup"><span data-stu-id="08ab0-186">ST_WITHIN can be used to check if a point lies within a Polygon.</span></span> <span data-ttu-id="08ab0-187">Często wielokątów są używane do reprezentowania granice, takimi jak kodów pocztowych, stan granice lub tworzenie fizycznych.</span><span class="sxs-lookup"><span data-stu-id="08ab0-187">Commonly Polygons are used to represent boundaries like zip codes, state boundaries, or natural formations.</span></span> <span data-ttu-id="08ab0-188">Ponownie Jeśli przestrzennych indeksowania w zasady indeksowania, następnie "w" zapytania zostanie obsłużona wydajnie przez indeks.</span><span class="sxs-lookup"><span data-stu-id="08ab0-188">Again if you include spatial indexing in your indexing policy, then "within" queries will be served efficiently through the index.</span></span> 

<span data-ttu-id="08ab0-189">Argumenty wielokąta ST_WITHIN może zawierać tylko jeden pierścień, tj. wielokątów nie może zawierać luk w nich.</span><span class="sxs-lookup"><span data-stu-id="08ab0-189">Polygon arguments in ST_WITHIN can contain only a single ring, i.e. the Polygons must not contain holes in them.</span></span> 

<span data-ttu-id="08ab0-190">**Zapytanie**</span><span class="sxs-lookup"><span data-stu-id="08ab0-190">**Query**</span></span>

    SELECT * 
    FROM Families f 
    WHERE ST_WITHIN(f.location, {
        'type':'Polygon', 
        'coordinates': [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]
    })

<span data-ttu-id="08ab0-191">**Wyniki**</span><span class="sxs-lookup"><span data-stu-id="08ab0-191">**Results**</span></span>

    [{
      "id": "WakefieldFamily",
    }]

> [!NOTE]
> <span data-ttu-id="08ab0-192">Podobne jak niedopasowanych typów działa zapytanie bazy danych Azure rozwiązania Cosmos Jeśli określona wartość lokalizacji w albo argument jest źle sformułowany lub nieprawidłowy, a następnie będą oceniać do **Niezdefiniowany** i obliczane dokumentu do pominięcia z kwerendy wyniki.</span><span class="sxs-lookup"><span data-stu-id="08ab0-192">Similar to how mismatched types works in Azure Cosmos DB query, if the location value specified in either argument is malformed or invalid, then it will evaluate to **undefined** and the evaluated document to be skipped from the query results.</span></span> <span data-ttu-id="08ab0-193">Jeśli zapytanie nie przynosi efektów, uruchom ST_ISVALIDDETAILED do debugowania Dlaczego typ spatail jest nieprawidłowy.</span><span class="sxs-lookup"><span data-stu-id="08ab0-193">If your query returns no results, run ST_ISVALIDDETAILED To debug why the spatail type is invalid.</span></span>     
> 
> 

<span data-ttu-id="08ab0-194">Azure DB rozwiązania Cosmos obsługuje również wykonywania kwerend odwrotny, tj. Możesz indeksu wierszy w usłudze Azure DB rozwiązania Cosmos lub wielokątów, a następnie wyszukać obszarów, które zawierają określony punkt.</span><span class="sxs-lookup"><span data-stu-id="08ab0-194">Azure Cosmos DB also supports performing inverse queries, i.e. you can index Polygons or lines in Azure Cosmos DB, then query for the areas that contain a specified point.</span></span> <span data-ttu-id="08ab0-195">Ten wzorzec jest najczęściej używany w logistyki do identyfikowania np. podczas ciężarówka wprowadza lub pozostawia wyznaczonego obszaru.</span><span class="sxs-lookup"><span data-stu-id="08ab0-195">This pattern is commonly used in logistics to identify e.g. when a truck enters or leaves a designated area.</span></span> 

<span data-ttu-id="08ab0-196">**Zapytanie**</span><span class="sxs-lookup"><span data-stu-id="08ab0-196">**Query**</span></span>

    SELECT * 
    FROM Areas a 
    WHERE ST_WITHIN({'type': 'Point', 'coordinates':[31.9, -4.8]}, a.location)


<span data-ttu-id="08ab0-197">**Wyniki**</span><span class="sxs-lookup"><span data-stu-id="08ab0-197">**Results**</span></span>

    [{
      "id": "MyDesignatedLocation",
      "location": {
        "type":"Polygon", 
        "coordinates": [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]
      }
    }]

<span data-ttu-id="08ab0-198">ST_ISVALID i ST_ISVALIDDETAILED może służyć do sprawdzenia, czy obiektu przestrzennego jest prawidłowy.</span><span class="sxs-lookup"><span data-stu-id="08ab0-198">ST_ISVALID and ST_ISVALIDDETAILED can be used to check if a spatial object is valid.</span></span> <span data-ttu-id="08ab0-199">Na przykład poniższe zapytanie sprawdza ważność punktu z poza zakresu wartości szerokości geograficznej (-132.8).</span><span class="sxs-lookup"><span data-stu-id="08ab0-199">For example, the following query checks the validity of a point with an out of range latitude value (-132.8).</span></span> <span data-ttu-id="08ab0-200">ST_ISVALID zwraca wartość logiczną, natomiast ST_ISVALIDDETAILED logicznych i ciąg zawierający przyczyny, dlaczego jest uznawane za nieprawidłowe.</span><span class="sxs-lookup"><span data-stu-id="08ab0-200">ST_ISVALID returns just a Boolean value, and ST_ISVALIDDETAILED returns the Boolean and a string containing the reason why it is considered invalid.</span></span>

<span data-ttu-id="08ab0-201">** Zapytania **</span><span class="sxs-lookup"><span data-stu-id="08ab0-201">** Query **</span></span>

    SELECT ST_ISVALID({ "type": "Point", "coordinates": [31.9, -132.8] })

<span data-ttu-id="08ab0-202">**Wyniki**</span><span class="sxs-lookup"><span data-stu-id="08ab0-202">**Results**</span></span>

    [{
      "$1": false
    }]

<span data-ttu-id="08ab0-203">Funkcje te mogą służyć do sprawdzania poprawności wielokątów.</span><span class="sxs-lookup"><span data-stu-id="08ab0-203">These functions can also be used to validate Polygons.</span></span> <span data-ttu-id="08ab0-204">Na przykład w tym miejscu używamy ST_ISVALIDDETAILED do sprawdzania poprawności wielokąta, który nie jest zamknięty.</span><span class="sxs-lookup"><span data-stu-id="08ab0-204">For example, here we use ST_ISVALIDDETAILED to validate a Polygon that is not closed.</span></span> 

<span data-ttu-id="08ab0-205">**Zapytanie**</span><span class="sxs-lookup"><span data-stu-id="08ab0-205">**Query**</span></span>

    SELECT ST_ISVALIDDETAILED({ "type": "Polygon", "coordinates": [[ 
        [ 31.8, -5 ], [ 31.8, -4.7 ], [ 32, -4.7 ], [ 32, -5 ] 
        ]]})

<span data-ttu-id="08ab0-206">**Wyniki**</span><span class="sxs-lookup"><span data-stu-id="08ab0-206">**Results**</span></span>

    [{
       "$1": { 
            "valid": false, 
            "reason": "The Polygon input is not valid because the start and end points of the ring number 1 are not the same. Each ring of a Polygon must have the same start and end points." 
          }
    }]

### <a name="linq-querying-in-the-net-sdk"></a><span data-ttu-id="08ab0-207">Wykonywanie zapytania do zestawu .NET SDK LINQ</span><span class="sxs-lookup"><span data-stu-id="08ab0-207">LINQ Querying in the .NET SDK</span></span>
<span data-ttu-id="08ab0-208">Zestaw SDK .NET usługi DocumentDB również dostawców stub metody `Distance()` i `Within()` do użytku w wyrażenia LINQ.</span><span class="sxs-lookup"><span data-stu-id="08ab0-208">The DocumentDB .NET SDK also providers stub methods `Distance()` and `Within()` for use within LINQ expressions.</span></span> <span data-ttu-id="08ab0-209">Dostawca usługi DocumentDB LINQ tłumaczy tych wywołań metody odpowiednik wywołania funkcji wbudowanej SQL (ST_DISTANCE i ST_WITHIN odpowiednio).</span><span class="sxs-lookup"><span data-stu-id="08ab0-209">The DocumentDB LINQ provider translates these method calls to the equivalent SQL built-in function calls (ST_DISTANCE and ST_WITHIN respectively).</span></span> 

<span data-ttu-id="08ab0-210">Oto przykład kwerendy LINQ znajduje wszystkie dokumenty w kolekcji bazy danych Azure rozwiązania Cosmos, którego wartość "Lokalizacja" jest w ramach usługi radius 30 km określonego punktu za pomocą LINQ.</span><span class="sxs-lookup"><span data-stu-id="08ab0-210">Here's an example of a LINQ query that finds all documents in the Azure Cosmos DB collection whose "location" value is within a radius of 30km of the specified point using LINQ.</span></span>

<span data-ttu-id="08ab0-211">**Zapytania LINQ odległość**</span><span class="sxs-lookup"><span data-stu-id="08ab0-211">**LINQ query for Distance**</span></span>

    foreach (UserProfile user in client.CreateDocumentQuery<UserProfile>(UriFactory.CreateDocumentCollectionUri("db", "profiles"))
        .Where(u => u.ProfileType == "Public" && a.Location.Distance(new Point(32.33, -4.66)) < 30000))
    {
        Console.WriteLine("\t" + user);
    }

<span data-ttu-id="08ab0-212">Podobnie w tym miejscu jest zapytaniem wyszukanie wszystkich dokumentów, których "Lokalizacja" znajduje się w określonym polu/wielokąta.</span><span class="sxs-lookup"><span data-stu-id="08ab0-212">Similarly, here's a query for finding all the documents whose "location" is within the specified box/Polygon.</span></span> 

<span data-ttu-id="08ab0-213">**W ramach kwerendy LINQ**</span><span class="sxs-lookup"><span data-stu-id="08ab0-213">**LINQ query for Within**</span></span>

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


<span data-ttu-id="08ab0-214">Teraz, gdy firma Microsoft zajęło przyjrzeć się jak wykonać zapytanie dotyczące dokumentów za pomocą LINQ i SQL, Spójrzmy na sposób konfigurowania bazy danych Azure rozwiązania Cosmos przestrzennych indeksowania.</span><span class="sxs-lookup"><span data-stu-id="08ab0-214">Now that we've taken a look at how to query documents using LINQ and SQL, let's take a look at how to configure Azure Cosmos DB for spatial indexing.</span></span>

## <a name="indexing"></a><span data-ttu-id="08ab0-215">Indeksowanie</span><span class="sxs-lookup"><span data-stu-id="08ab0-215">Indexing</span></span>
<span data-ttu-id="08ab0-216">Firma Microsoft opisane w [schematu niezależny od indeksowanie z bazy danych Azure rozwiązania Cosmos](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf) papieru, możemy zaprojektowane aparatu bazy danych DB rozwiązania Cosmos Azure jako naprawdę niezależny od schematu oraz zapewnić wsparcie pierwszej klasie dla formatu JSON.</span><span class="sxs-lookup"><span data-stu-id="08ab0-216">As we described in the [Schema Agnostic Indexing with Azure Cosmos DB](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf) paper, we designed Azure Cosmos DB’s database engine to be truly schema agnostic and provide first class support for JSON.</span></span> <span data-ttu-id="08ab0-217">Aparat bazy danych zoptymalizowanych pod kątem zapisu Azure DB rozwiązania Cosmos rozumie natywnie danych przestrzennych (punkty, wielokątów i linii), reprezentowany w standardzie GeoJSON.</span><span class="sxs-lookup"><span data-stu-id="08ab0-217">The write optimized database engine of Azure Cosmos DB natively understands spatial data (points, Polygons and lines) represented in the GeoJSON standard.</span></span>

<span data-ttu-id="08ab0-218">Mówiąc, geometrii jest zaprojektowana geodezyjnej współrzędne na płaszczyźnie 2D, a następnie stopniowo podzielone komórki za pomocą **quadtree**.</span><span class="sxs-lookup"><span data-stu-id="08ab0-218">In a nutshell, the geometry is projected from geodetic coordinates onto a 2D plane then divided progressively into cells using a **quadtree**.</span></span> <span data-ttu-id="08ab0-219">Tych komórek są mapowane na 1D na podstawie lokalizacji komórki znajdującej się w **Hilberta miejsca wypełnianie krzywej**, który zachowuje lokalizację punktów.</span><span class="sxs-lookup"><span data-stu-id="08ab0-219">These cells are mapped to 1D based on the location of the cell within a **Hilbert space filling curve**, which preserves locality of points.</span></span> <span data-ttu-id="08ab0-220">Ponadto gdy danych lokalizacji jest indeksowany, przechodzi ona przez proces znany jako **tworzenia mozaiki**, tj. wszystkie komórki przecinających lokalizacji są zidentyfikowane i przechowywane jako klucze w indeksie bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="08ab0-220">Additionally when location data is indexed, it goes through a process known as **tessellation**, i.e. all the cells that intersect a location are identified and stored as keys in the Azure Cosmos DB index.</span></span> <span data-ttu-id="08ab0-221">Podczas przeszukiwania argumenty, takie jak punkty i wielokątów są również tesselowaną wyodrębnić zakresy identyfikatorów odpowiednie komórki, a następnie używane do pobierania danych z indeksu.</span><span class="sxs-lookup"><span data-stu-id="08ab0-221">At query time, arguments like points and Polygons are also tessellated to extract the relevant cell ID ranges, then used to retrieve data from the index.</span></span>

<span data-ttu-id="08ab0-222">Jeśli można określić zasady indeksowania, który zawiera indeks przestrzenny dla / * (wszystkie ścieżki), a następnie wszystkie punkty znaleziony w kolekcji są indeksowane wydajnych zapytań przestrzennych (ST_WITHIN i ST_DISTANCE).</span><span class="sxs-lookup"><span data-stu-id="08ab0-222">If you specify an indexing policy that includes spatial index for /* (all paths), then all points found within the collection are indexed for efficient spatial queries (ST_WITHIN and ST_DISTANCE).</span></span> <span data-ttu-id="08ab0-223">Indeksy przestrzenne nie ma wartość precyzji i zawsze używaj domyślną wartość precyzji.</span><span class="sxs-lookup"><span data-stu-id="08ab0-223">Spatial indexes do not have a precision value, and always use a default precision value.</span></span>

> [!NOTE]
> <span data-ttu-id="08ab0-224">Obsługuje bazę danych systemu Azure rozwiązania Cosmos automatycznego indeksowania punktów, wielokątów i LineStrings</span><span class="sxs-lookup"><span data-stu-id="08ab0-224">Azure Cosmos DB supports automatic indexing of Points, Polygons, and LineStrings</span></span>
> 
> 

<span data-ttu-id="08ab0-225">Poniższy fragment kodu JSON przedstawia zasady indeksowania z włączone indeksowanie przestrzennych, tj. indeks dowolnego punktu GeoJSON znaleziono w dokumentach do wykonywania zapytań przestrzennych.</span><span class="sxs-lookup"><span data-stu-id="08ab0-225">The following JSON snippet shows an indexing policy with spatial indexing enabled, i.e. index any GeoJSON point found within documents for spatial querying.</span></span> <span data-ttu-id="08ab0-226">W przypadku modyfikowania zasady indeksowania, przy użyciu portalu Azure, można określić następujące JSON dla zasady indeksowania umożliwiające przestrzennych indeksowania w kolekcji.</span><span class="sxs-lookup"><span data-stu-id="08ab0-226">If you are modifying the indexing policy using the Azure Portal, you can specify the following JSON for indexing policy to enable spatial indexing on your collection.</span></span>

<span data-ttu-id="08ab0-227">**Kolekcja indeksowania zasad JSON z przestrzennym włączone punktów i wielokątów**</span><span class="sxs-lookup"><span data-stu-id="08ab0-227">**Collection Indexing Policy JSON with Spatial enabled for points and Polygons**</span></span>

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

<span data-ttu-id="08ab0-228">Oto fragment kodu w programie .NET, który pokazuje, jak utworzyć kolekcję z przestrzennego indeksowania włączona dla wszystkich ścieżek zawierających punkty.</span><span class="sxs-lookup"><span data-stu-id="08ab0-228">Here's a code snippet in .NET that shows how to create a collection with spatial indexing turned on for all paths containing points.</span></span> 

<span data-ttu-id="08ab0-229">**Utwórz kolekcję z przestrzennego indeksowania**</span><span class="sxs-lookup"><span data-stu-id="08ab0-229">**Create a collection with spatial indexing**</span></span>

    DocumentCollection spatialData = new DocumentCollection()
    spatialData.IndexingPolicy = new IndexingPolicy(new SpatialIndex(DataType.Point)); //override to turn spatial on by default
    collection = await client.CreateDocumentCollectionAsync(UriFactory.CreateDatabaseUri("db"), spatialData);

<span data-ttu-id="08ab0-230">A Oto, jak można zmodyfikować istniejącą kolekcję przeprowadzać przestrzennych indeksowania za pośrednictwem punktów, które są przechowywane w dokumentach.</span><span class="sxs-lookup"><span data-stu-id="08ab0-230">And here's how you can modify an existing collection to take advantage of spatial indexing over any points that are stored within documents.</span></span>

<span data-ttu-id="08ab0-231">**Zmodyfikuj istniejącą kolekcję z przestrzennego indeksowania**</span><span class="sxs-lookup"><span data-stu-id="08ab0-231">**Modify an existing collection with spatial indexing**</span></span>

    Console.WriteLine("Updating collection with spatial indexing enabled in indexing policy...");
    collection.IndexingPolicy = new IndexingPolicy(new SpatialIndex(DataType.Point));
    await client.ReplaceDocumentCollectionAsync(collection);

    Console.WriteLine("Waiting for indexing to complete...");
    long indexTransformationProgress = 0;
    while (indexTransformationProgress < 100)
    {
        ResourceResponse<DocumentCollection> response = await client.ReadDocumentCollectionAsync(UriFactory.CreateDocumentCollectionUri("db", "coll"));
        indexTransformationProgress = response.IndexTransformationProgress;

        await Task.Delay(TimeSpan.FromSeconds(1));
    }

> [!NOTE]
> <span data-ttu-id="08ab0-232">Jeśli lokalizacja wartość GeoJSON dokumentu jest źle sformułowany lub nieprawidłowy, następnie go zostanie nie indeksowanie przestrzennych zapytań.</span><span class="sxs-lookup"><span data-stu-id="08ab0-232">If the location GeoJSON value within the document is malformed or invalid, then it will not get indexed for spatial querying.</span></span> <span data-ttu-id="08ab0-233">Można sprawdzić za pomocą ST_ISVALID i ST_ISVALIDDETAILED wartości lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="08ab0-233">You can validate location values using ST_ISVALID and ST_ISVALIDDETAILED.</span></span>
> 
> <span data-ttu-id="08ab0-234">Jeśli definicja kolekcja zawiera klucz partycji, indeksowania postępu przekształcenie nie został zgłoszony.</span><span class="sxs-lookup"><span data-stu-id="08ab0-234">If your collection definition includes a partition key, indexing transformation progress is not reported.</span></span> 
> 
> 

## <a name="next-steps"></a><span data-ttu-id="08ab0-235">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="08ab0-235">Next steps</span></span>
<span data-ttu-id="08ab0-236">Teraz możesz już wcześniej o tym, jak rozpocząć pracę z obsługą dane geograficzne w usłudze Azure DB rozwiązania Cosmos, możesz:</span><span class="sxs-lookup"><span data-stu-id="08ab0-236">Now that you've learnt about how to get started with geospatial support in Azure Cosmos DB, you can:</span></span>

* <span data-ttu-id="08ab0-237">Rozpoczęcie kodowania z [przykłady kodu .NET dane geograficzne w witrynie GitHub](https://github.com/Azure/azure-documentdb-dotnet/blob/fcf23d134fc5019397dcf7ab97d8d6456cd94820/samples/code-samples/Geospatial/Program.cs)</span><span class="sxs-lookup"><span data-stu-id="08ab0-237">Start coding with the [Geospatial .NET code samples on GitHub](https://github.com/Azure/azure-documentdb-dotnet/blob/fcf23d134fc5019397dcf7ab97d8d6456cd94820/samples/code-samples/Geospatial/Program.cs)</span></span>
* <span data-ttu-id="08ab0-238">Uzyskać ręce na z geograficzne zapytań w [Plac zabaw dla Azure rozwiązania Cosmos DB zapytań](http://www.documentdb.com/sql/demo#geospatial)</span><span class="sxs-lookup"><span data-stu-id="08ab0-238">Get hands on with geospatial querying at the [Azure Cosmos DB Query Playground](http://www.documentdb.com/sql/demo#geospatial)</span></span>
* <span data-ttu-id="08ab0-239">Dowiedz się więcej o [kwerendy bazy danych Azure rozwiązania Cosmos](documentdb-sql-query.md)</span><span class="sxs-lookup"><span data-stu-id="08ab0-239">Learn more about [Azure Cosmos DB Query](documentdb-sql-query.md)</span></span>
* <span data-ttu-id="08ab0-240">Dowiedz się więcej o [zasady indeksowania bazy danych Azure rozwiązania Cosmos](indexing-policies.md)</span><span class="sxs-lookup"><span data-stu-id="08ab0-240">Learn more about [Azure Cosmos DB Indexing Policies](indexing-policies.md)</span></span>

