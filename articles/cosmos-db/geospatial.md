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
# <a name="working-with-geospatial-and-geojson-location-data-in-azure-cosmos-db"></a>Praca z dane geograficzne i danych lokalizacji GeoJSON w usłudze Azure DB rozwiązania Cosmos
Ten artykuł obejmuje wprowadzenie toohello dane geograficzne funkcji [bazy danych Azure rozwiązania Cosmos](https://azure.microsoft.com/services/cosmos-db/). Po przeczytaniu tego, będą mogli tooanswer hello następujące pytania:

* Sposób przechowywania danych przestrzennych w usłudze Azure DB rozwiązania Cosmos?
* Jak wykonać zapytanie dane geograficzne w usłudze Azure DB rozwiązania Cosmos w SQL i LINQ
* Jak włączyć lub wyłączyć indeksowanie przestrzenne w usłudze Azure DB rozwiązania Cosmos

W tym artykule opisano, jak toowork z danych przestrzennych z hello interfejsu API usługi DocumentDB. Zobacz to [projektu GitHub](https://github.com/Azure/azure-documentdb-dotnet/blob/master/samples/code-samples/Geospatial/Program.cs) dla przykładów kodu.

## <a name="introduction-toospatial-data"></a>Wprowadzenie toospatial danych
Dane przestrzenne opisano hello pozycji i kształt obiektów w przestrzeni. W większości aplikacji one odpowiadać tooobjects na powitania ziemi, tj. dane geograficzne. Dane przestrzenne może być używane toorepresent hello lokalizacji osoby, miejsca lub granic hello miejscowości lub jeziora. Typowe przypadki użycia obejmują często zbliżeniowe zapytań, dotyczących np. "Znajdź wszystkie kawiarniach niemal mojej bieżącej lokalizacji". 

### <a name="geojson"></a>GeoJSON
Azure DB rozwiązania Cosmos obsługuje indeksowanie i wyszukiwanie danych punktu geograficznych reprezentowanej przy użyciu hello [specyfikacji GeoJSON](https://tools.ietf.org/html/rfc7946). Struktury danych GeoJSON są zawsze prawidłowych obiektów JSON, dzięki czemu mogą być przechowywane i wyświetlić przy użyciu bazy danych Azure rozwiązania Cosmos bez żadnych specjalnych narzędzi i bibliotek. Hello Azure rozwiązania Cosmos DB SDK zapewniają pomocnika klasy i metody, dzięki któremu można łatwo toowork z danymi przestrzennymi. 

### <a name="points-linestrings-and-polygons"></a>Punkty, LineStrings i wielokątów
A **punktu** oznacza pojedynczego pozycję w przestrzeni. W danych geograficznych punkt reprezentuje hello dokładnej lokalizacji, która może być ulicę sklepów spożywczych, kiosku, samochodu lub miejscowości.  Punkt jest reprezentowana w pary GeoJSON (i bazy danych Azure rozwiązania Cosmos) przy użyciu jego współrzędnych lub długości i szerokości geograficznej. Oto przykład JSON dla punktu.

**Punkty Azure rozwiązania Cosmos bazy danych**

```json
{
    "type":"Point",
    "coordinates":[ 31.9, -4.8 ]
}
```

> [!NOTE]
> Hello specyfikacji GeoJSON określa długość pierwszy i szerokości geograficznej drugiego. Podobnie jak w innych aplikacjach mapowania długości i szerokości geograficznej są kąty i wyświetlany w postaci stopni. Wartości długości geograficznej są mierzone od głównego południka hello i należą do zakresu od- i 180.0 stopni, 180 do szerokości geograficznej wartości są mierzone od równika hello i należą do zakresu od-90.0 i 90.0 stopni. 
> 
> Azure DB rozwiązania Cosmos interpretuje współrzędne reprezentowane na powitania WGS 84 odwołanie systemu. Zobacz poniżej więcej szczegółów dotyczących systemów współrzędnych odwołania.
> 
> 

Można ją osadzić w dokumencie bazy danych Azure rozwiązania Cosmos opisane w tym przykładzie profilu użytkownika zawierającego dane dotyczące lokalizacji:

**Użyj profilu z lokalizacją przechowywane w usłudze Azure DB rozwiązania Cosmos**

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

Ponadto toopoints, GeoJSON obsługuje również LineStrings i wielokątów. **LineStrings** reprezentują dwa lub więcej punktów w miejscu i hello segmenty linii, które łączą te elementy. W danych geograficznych LineStrings są często używane toorepresent drogami lub rzek. A **wielokąta** jest granicę punktów połączonych formularzy LineString zamknięte. Wielokąty są często używane toorepresent tworzenie fizyczne jak jeziora lub polityczną jurysdykcjach przykład miast i stanów. Oto przykład wielokąta w usłudze Azure DB rozwiązania Cosmos. 

**Wielokąty w GeoJSON**

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
> Hello GeoJSON specyfikacji wymaga, aby uzyskać prawidłową wielokątów hello ostatnią parę współrzędnych podane powinien hello sam toocreate najpierw hello zamknięty kształt.
> 
> Punktów w wielokąta muszą być określone w kolejności przeciwnie do ruchu wskazówek zegara. Wielokąt określony w kolejności zegara reprezentuje odwrotność hello hello regionu w niej.
> 
> 

W dodatku tooPoint, LineString, Polygon, a GeoJSON określa również hello reprezentację jak toogroup wielu lokalizacji geograficznych, oraz dowolne właściwości tooassociate z używanie funkcji geolokalizacji jako **funkcji**. Ponieważ te obiekty są poprawne dane JSON, ich można wszystkie przechowywane i przetwarzane w usłudze Azure DB rozwiązania Cosmos. Niemniej jednak bazy danych Azure rozwiązania Cosmos obsługuje tylko, automatycznego indeksowania punktów.

### <a name="coordinate-reference-systems"></a>Koordynacji systemów odniesienia
Ponieważ kształtu hello ziemi hello jest nieprawidłowa, współrzędne geograficzne danych jest reprezentowana w wielu systemach współrzędnych odwołania (znaki CR), każdy z ramek odniesienia i jednostki miary. Na przykład "National siatki Brytania" hello jest systemu odniesienia są bardzo dokładne na brytyjski hello, ale nie poza nią. 

Witaj najpopularniejszych używany obecnie jest hello World geodezyjnej systemu [WGS 84](http://earth-info.nga.mil/GandG/wgs84/). Urządzenia GPS, a wiele usług mapowania tym map programu Google i interfejsów API map Bing Użyj WGS 84. Azure DB rozwiązania Cosmos obsługuje indeksowanie i wyszukiwanie przy użyciu hello CRS WGS 84 tylko dane geograficzne. 

## <a name="creating-documents-with-spatial-data"></a>Tworzenie dokumentów z danymi przestrzennymi
Podczas tworzenia dokumentów, które zawierają wartości GeoJSON, są one automatycznie indeksowane z indeksu przestrzennego w zasadach indeksowania toohello zgodnie z kolekcji hello. Podczas pracy z zestawem Azure rozwiązania Cosmos DB SDK w typach określanych dynamicznie języka Python lub Node.js, należy utworzyć prawidłowy GeoJSON.

**Utwórz dokument z dane geograficzne w środowisku Node.js**

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

Jeśli pracujesz z hello interfejsów API usługi DocumentDB, można użyć hello `Point` i `Polygon` klas w ramach hello `Microsoft.Azure.Documents.Spatial` informacji o lokalizacji tooembed przestrzeni nazw w obrębie obiektów aplikacji. Te klasy ułatwić hello serializacji i deserializacji danych przestrzennych w GeoJSON.

**Utwórz dokument z dane geograficzne w .NET**

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

Jeśli nie ma informacji hello współrzędne geograficzne, ale ma hello adresów fizycznych ani nazwy lokalizacji, takiej jak nazwa miejscowości lub kraj, rzeczywiste współrzędne hello można wyszukiwać za pomocą usług geokodowanie, takich jak usługi REST mapy Bing. Więcej informacji na temat usługi mapy Bing geokodowanie [tutaj](https://msdn.microsoft.com/library/ff701713.aspx).

## <a name="querying-spatial-types"></a>Wykonywanie zapytania typów przestrzennych
Teraz, gdy firma Microsoft zajęło przyjrzeć się jak dane geograficzne tooinsert, Spójrzmy na jak tooquery te dane przy użyciu bazy danych rozwiązania Cosmos Azure przy użyciu programu SQL i LINQ.

### <a name="spatial-sql-built-in-functions"></a>Przestrzenne wbudowanych funkcji SQL
Azure DB rozwiązania Cosmos obsługuje hello następujące funkcje wbudowane Otwórz geograficzne konsorcjum (OGC) na potrzeby zapytań o dane geograficzne. Więcej szczegółów na powitania pełnego zestawu funkcji wbudowanych hello języka SQL, zobacz zbyt[kwerendy bazy danych z rozwiązania Cosmos Azure](documentdb-sql-query.md).

<table>
<tr>
  <td><strong>Użycie</strong></td>
  <td><strong>Opis</strong></td>
</tr>
<tr>
  <td>ST_DISTANCE (spatial_expr, spatial_expr)</td>
  <td>Zwraca hello odległość między hello dwóch wyrażeń GeoJSON punktu wielokąta i LineString.</td>
</tr>
<tr>
  <td>ST_WITHIN (spatial_expr, spatial_expr)</td>
  <td>Zwraca wyrażenie logiczne, wskazującą, czy hello pierwszego obiektu GeoJSON (punkt, wielokąta lub LineString) jest w obrębie hello drugiego obiektu GeoJSON (punkt, wielokąta lub LineString).</td>
</tr>
<tr>
  <td>ST_INTERSECTS (spatial_expr, spatial_expr)</td>
  <td>Zwraca wyrażenie logiczne, wskazującą, czy intersect hello dwóch określonych GeoJSON obiektów (punkt, wielokąta lub LineString).</td>
</tr>
<tr>
  <td>ST_ISVALID</td>
  <td>Zwraca wartość logiczną wskazującą, czy określono hello wyrażenie GeoJSON punktu wielokąta i LineString jest nieprawidłowy.</td>
</tr>
<tr>
  <td>ST_ISVALIDDETAILED</td>
  <td>Zwraca wartość JSON zawierający wartość logiczna, jeśli hello określone wyrażenie GeoJSON punktu wielokąta i LineString jest prawidłowy, a jeśli jest nieprawidłowy, ponadto hello Przyczyna jako wartość typu ciąg.</td>
</tr>
</table>

Funkcje przestrzenne mogą być używane tooperform zbliżeniowe zapytań dotyczących danych przestrzennych. Na przykład w tym miejscu jest kwerendę, która zwraca rodziny wszystkie dokumenty, czy są w ciągu 30 km hello określonej lokalizacji przy użyciu wbudowanych funkcji ST_DISTANCE hello. 

**Zapytanie**

    SELECT f.id 
    FROM Families f 
    WHERE ST_DISTANCE(f.location, {'type': 'Point', 'coordinates':[31.9, -4.8]}) < 30000

**Wyniki**

    [{
      "id": "WakefieldFamily"
    }]

Jeśli dołączysz przestrzennych indeksowania w zasady indeksowania, następnie "odległość zapytania" zostanie obsłużona wydajnie za pomocą hello indeksu. Więcej szczegółów na indeksowanie przestrzennych zobacz sekcję hello poniżej. Jeśli nie masz przestrzennych indeks hello określonych ścieżek, można wykonywać zapytania przestrzennych, określając `x-ms-documentdb-query-enable-scan` nagłówek żądania z hello wartość ustawiona zbyt "true". W środowisku .NET, można to zrobić przez przekazanie hello opcjonalne **FeedOptions** tooqueries argumentu z [EnableScanInQuery](https://msdn.microsoft.com/library/microsoft.azure.documents.client.feedoptions.enablescaninquery.aspx#P:Microsoft.Azure.Documents.Client.FeedOptions.EnableScanInQuery) ustawić tootrue. 

ST_WITHIN mogą być używane toocheck punkt znajduje się wewnątrz wielokąta. Często wielokątów są granicami toorepresent używanych kodów pocztowych, stan granice lub tworzenie fizycznych. Ponownie Jeśli przestrzennych indeksowania w zasady indeksowania, następnie "w" zapytania zostanie obsłużona wydajnie za pomocą hello indeksu. 

Argumenty wielokąta ST_WITHIN może zawierać tylko jeden pierścień, tj. hello wielokątów nie może zawierać luk w nich. 

**Zapytanie**

    SELECT * 
    FROM Families f 
    WHERE ST_WITHIN(f.location, {
        'type':'Polygon', 
        'coordinates': [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]
    })

**Wyniki**

    [{
      "id": "WakefieldFamily",
    }]

> [!NOTE]
> Podobnych typów toohow niezgodne działa w zapytaniu bazy danych rozwiązania Cosmos Azure, jeśli wartość lokalizacji hello określony w albo argument jest źle sformułowany lub nieprawidłowy, a następnie będą oceniać za**Niezdefiniowany** i toobe dokumentu hello obliczone pominięte z hello wyniki zapytania. Jeśli zapytanie nie przynosi efektów, uruchom toodebug ST_ISVALIDDETAILED Dlaczego hello spatail typ jest nieprawidłowy.     
> 
> 

Azure DB rozwiązania Cosmos obsługuje również wykonywania kwerend odwrotny, tj. Możesz indeksu wierszy w usłudze Azure DB rozwiązania Cosmos lub wielokątów, a następnie wyszukać hello obszarów, które zawierają określony punkt. Ten wzorzec jest często używana w tooidentify logistyki np. podczas ciężarówka wprowadza lub pozostawia wyznaczonego obszaru. 

**Zapytanie**

    SELECT * 
    FROM Areas a 
    WHERE ST_WITHIN({'type': 'Point', 'coordinates':[31.9, -4.8]}, a.location)


**Wyniki**

    [{
      "id": "MyDesignatedLocation",
      "location": {
        "type":"Polygon", 
        "coordinates": [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]
      }
    }]

ST_ISVALID i ST_ISVALIDDETAILED mogą być toocheck używane, jeśli obiektu przestrzennego jest prawidłowy. Na przykład hello następującego zapytania sprawdza ważność hello punktu z poza zakresu wartości szerokości geograficznej (-132.8). ST_ISVALID zwraca wartość logiczną, a zwraca ST_ISVALIDDETAILED hello logicznych i ciąg zawierający Przyczyna hello dlaczego jest uznawane za nieprawidłowe.

** Zapytania **

    SELECT ST_ISVALID({ "type": "Point", "coordinates": [31.9, -132.8] })

**Wyniki**

    [{
      "$1": false
    }]

Te funkcje mogą być również używane toovalidate wielokątów. Na przykład w tym miejscu używamy toovalidate ST_ISVALIDDETAILED wielokąta, który nie jest zamknięty. 

**Zapytanie**

    SELECT ST_ISVALIDDETAILED({ "type": "Polygon", "coordinates": [[ 
        [ 31.8, -5 ], [ 31.8, -4.7 ], [ 32, -4.7 ], [ 32, -5 ] 
        ]]})

**Wyniki**

    [{
       "$1": { 
            "valid": false, 
            "reason": "hello Polygon input is not valid because hello start and end points of hello ring number 1 are not hello same. Each ring of a Polygon must have hello same start and end points." 
          }
    }]

### <a name="linq-querying-in-hello-net-sdk"></a>W hello zestawu .NET SDK zapytań LINQ
Witaj zestawu SDK .NET usługi DocumentDB również dostawców stub metody `Distance()` i `Within()` do użytku w wyrażenia LINQ. Witaj dostawcy DocumentDB LINQ tłumaczy tych wywołań toohello równoważne SQL wbudowanych funkcji wywołania metody (ST_DISTANCE i ST_WITHIN odpowiednio). 

Oto przykład kwerendy LINQ znajduje wszystkie dokumenty w hello Azure DB rozwiązania Cosmos kolekcji o wartości "Lokalizacja" w ramach usługi radius 30 km hello określono punktu, przy użyciu LINQ.

**Zapytania LINQ odległość**

    foreach (UserProfile user in client.CreateDocumentQuery<UserProfile>(UriFactory.CreateDocumentCollectionUri("db", "profiles"))
        .Where(u => u.ProfileType == "Public" && a.Location.Distance(new Point(32.33, -4.66)) < 30000))
    {
        Console.WriteLine("\t" + user);
    }

Podobnie w tym miejscu jest zapytania do znajdowania się, że wszystkie dokumenty hello, w których "Lokalizacja" znajduje się w hello określone pole/wielokąta. 

**W ramach kwerendy LINQ**

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


Teraz, gdy firma Microsoft zajęło przyjrzeć się jak tooquery dokumentów za pomocą LINQ i SQL, Spójrzmy na jak tooconfigure bazy danych Azure rozwiązania Cosmos przestrzennych indeksowania.

## <a name="indexing"></a>Indeksowanie
Zgodnie z opisem możemy w hello [schematu niezależny od indeksowanie z bazy danych Azure rozwiązania Cosmos](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf) papier, możemy zaprojektowane toobe aparatu bazy danych DB rozwiązania Cosmos Azure rzeczywiście niezależny od schematu oraz zapewnić wsparcie pierwszej klasie dla formatu JSON. Aparat bazy danych zoptymalizowanych pod kątem zapisu Hello Azure DB rozwiązania Cosmos rozumie natywnie danych przestrzennych (punkty, wielokątów i linii) reprezentowany w standardzie GeoJSON hello.

Mówiąc, geometrii hello jest zaprojektowana geodezyjnej współrzędne na płaszczyźnie 2D, a następnie stopniowo podzielone komórki za pomocą **quadtree**. Te komórki są mapowane too1D na podstawie lokalizacji hello hello komórki znajdującej się w **Hilberta miejsca wypełnianie krzywej**, który zachowuje lokalizację punktów. Ponadto gdy danych lokalizacji jest indeksowany, przechodzi ona przez proces znany jako **tworzenia mozaiki**, tj. wszystkie komórki hello, przecinających lokalizacji są zidentyfikowane i przechowywane jako klucze hello Azure DB rozwiązania Cosmos indeksu. Podczas przeszukiwania argumenty, np. punkty i wielokątów są również tesselowaną tooextract hello zakresów identyfikator odpowiedniego komórek, a następnie użyć danych tooretrieve z indeksu hello.

Jeśli można określić zasady indeksowania, który zawiera indeks przestrzenny dla / * (wszystkie ścieżki), a następnie wszystkie punkty znaleziony w kolekcji hello są indeksowane wydajnych zapytań przestrzennych (ST_WITHIN i ST_DISTANCE). Indeksy przestrzenne nie ma wartość precyzji i zawsze używaj domyślną wartość precyzji.

> [!NOTE]
> Obsługuje bazę danych systemu Azure rozwiązania Cosmos automatycznego indeksowania punktów, wielokątów i LineStrings
> 
> 

Hello następujący fragment kodu JSON przedstawia zasady indeksowania z włączone indeksowanie przestrzennych, tj. indeks dowolnego punktu GeoJSON znaleziono w dokumentach do wykonywania zapytań przestrzennych. W przypadku modyfikowania hello indeksowania zasady za pomocą hello portalu Azure, można określić powitania po JSON do indeksowania tooenable zasad przestrzennych indeksowania w kolekcji.

**Kolekcja indeksowania zasad JSON z przestrzennym włączone punktów i wielokątów**

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

Oto fragment kodu w programie .NET, który pokazuje, jak toocreate kolekcji z przestrzennego indeksowania włączona dla wszystkich ścieżek zawierających punkty. 

**Utwórz kolekcję z przestrzennego indeksowania**

    DocumentCollection spatialData = new DocumentCollection()
    spatialData.IndexingPolicy = new IndexingPolicy(new SpatialIndex(DataType.Point)); //override tooturn spatial on by default
    collection = await client.CreateDocumentCollectionAsync(UriFactory.CreateDatabaseUri("db"), spatialData);

A Oto, jak można zmodyfikować istniejący kolekcji tootake zaletą przestrzennych indeksowania za pośrednictwem punktów, które są przechowywane w dokumentach.

**Zmodyfikuj istniejącą kolekcję z przestrzennego indeksowania**

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
> Jeśli lokalizacja hello GeoJSON wartość w dokumencie hello jest źle sformułowany lub nieprawidłowy, następnie go zostanie nie indeksowanie przestrzennych zapytań. Można sprawdzić za pomocą ST_ISVALID i ST_ISVALIDDETAILED wartości lokalizacji.
> 
> Jeśli definicja kolekcja zawiera klucz partycji, indeksowania postępu przekształcenie nie został zgłoszony. 
> 
> 

## <a name="next-steps"></a>Następne kroki
Teraz, gdy zostały wcześniej o jak tooget pracę z obsługą dane geograficzne w usłudze Azure DB rozwiązania Cosmos, można wykonywać następujące czynności:

* Rozpoczęcie kodowania z hello [przykłady kodu .NET dane geograficzne w witrynie GitHub](https://github.com/Azure/azure-documentdb-dotnet/blob/fcf23d134fc5019397dcf7ab97d8d6456cd94820/samples/code-samples/Geospatial/Program.cs)
* Uzyskać ręce na z geograficzne zapytań na powitania [Plac zabaw dla Azure rozwiązania Cosmos DB zapytań](http://www.documentdb.com/sql/demo#geospatial)
* Dowiedz się więcej o [kwerendy bazy danych Azure rozwiązania Cosmos](documentdb-sql-query.md)
* Dowiedz się więcej o [zasady indeksowania bazy danych Azure rozwiązania Cosmos](indexing-policies.md)

