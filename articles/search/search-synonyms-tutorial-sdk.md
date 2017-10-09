---
title: "aaaSynonyms Podgląd samouczek w usłudze Azure Search | Dokumentacja firmy Microsoft"
description: "Dodaj hello synonimy Podgląd funkcji tooan indeksu w usłudze Azure Search."
services: search
manager: jhubbard
documentationcenter: 
author: HeidiSteen
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 03/31/2017
ms.author: heidist
ms.openlocfilehash: 055c1cbafb945823a3dc4da0c522db236b1d192c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="synonym-preview-c-tutorial-for-azure-search"></a>Samouczek dotyczący synonimów (wersja zapoznawcza) języka C# dla usługi Azure Search

Synonimy rozwiń węzeł kwerendy przez dopasowanie na warunkach uznawane za semantycznie równoważne toohello termin wejściowego. Na przykład może być "samochód" toomatch dokumenty zawierające warunki hello "samochodów" lub "nośnika".

W usłudze Azure Search synonimy są definiowane w *mapie synonimów* za pośrednictwem *reguł mapowania*, które kojarzą równoważne wyrażenia. Można tworzyć wiele map synonim, zamieścić je jako indeks tooany dostępnych zasobów całej usługi i odwoływanie które jeden toouse na poziomie pola hello. Podczas przeszukiwania Ponadto toosearching indeksu usługi Azure Search pojawia się wyszukiwania w mapie synonim został określony dla pól używanych w zapytaniu hello.

> [!NOTE]
> synonimy Hello funkcja jest aktualnie Podgląd i obsługiwana w tylko hello najnowszej wersji zapoznawczej interfejsu API i wersje zestawu SDK (interfejs api-version = 2016-09-01-Preview, wersji zestawu SDK 4.x-preview). Obecnie witryna Azure Portal nie jest obsługiwana. Interfejsy API w wersji zapoznawczej nie są objęte umową SLA, a funkcje wersji zapoznawczej mogą ulec zmianie, dlatego nie zaleca się ich używania w aplikacjach produkcyjnych.

## <a name="prerequisites"></a>Wymagania wstępne

Samouczek wymagania obejmują następujące hello:

* [Program Visual Studio](https://www.visualstudio.com/downloads/)
* [Usługa Azure Search](search-create-service-portal.md)
* [Wersja zapoznawcza biblioteki Microsoft.Azure.Search .NET](https://aka.ms/search-sdk-preview)
* [W jaki sposób toouse Azure wyszukiwanie od aplikacji .NET](https://docs.microsoft.com/azure/search/search-howto-dotnet-sdk)

## <a name="overview"></a>Omówienie

Przed i po zapytania pokazują, wartość hello synonimów. W tym samouczku używamy przykładowej aplikacji, która wykonuje zapytania i zwraca wyniki w przykładowym indeksie. Witaj przykładowej aplikacji tworzy małych indeks o nazwie "hotels" wypełniane przy użyciu dwa dokumenty. Aplikacja Hello wykonuje zapytania wyszukiwania korzystania z warunków i wyrażeń, które nie są wyświetlane w indeksie hello, funkcje hello synonimy, następnie problemów Witaj ponownie wyszukiwania tego samego. Poniższy kod Hello pokazuje hello ogólny przepływ.

```csharp
  static void Main(string[] args)
  {
      SearchServiceClient serviceClient = CreateSearchServiceClient();

      Console.WriteLine("{0}", "Cleaning up resources...\n");
      CleanupResources(serviceClient);

      Console.WriteLine("{0}", "Creating index...\n");
      CreateHotelsIndex(serviceClient);

      ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");

      Console.WriteLine("{0}", "Uploading documents...\n");
      UploadDocuments(indexClient);

      ISearchIndexClient indexClientForQueries = CreateSearchIndexClient();

      RunQueriesWithNonExistentTermsInIndex(indexClientForQueries);

      Console.WriteLine("{0}", "Adding synonyms...\n");
      UploadSynonyms(serviceClient);
      EnableSynonymsInHotelsIndex(serviceClient);
      Thread.Sleep(10000); // Wait for hello changes toopropagate

      RunQueriesWithNonExistentTermsInIndex(indexClientForQueries);

      Console.WriteLine("{0}", "Complete.  Press any key tooend application...\n");

      Console.ReadKey();
  }
```
Witaj toocreate kroki i wypełnić Indeks przykładów hello opisano szczegółowo w [jak toouse Azure wyszukiwanie od aplikacji .NET](https://docs.microsoft.com/azure/search/search-howto-dotnet-sdk).

## <a name="before-queries"></a>Zapytania „przed”

W indeksie `RunQueriesWithNonExistentTermsInIndex` wykonujemy zapytania wyszukiwania z użyciem wyrażeń „five star”, „internet” oraz „economy AND hotel”.
```csharp
Console.WriteLine("Search hello entire index for hello phrase \"five star\":\n");
results = indexClient.Documents.Search<Hotel>("\"five star\"", parameters);
WriteDocuments(results);

Console.WriteLine("Search hello entire index for hello term 'internet':\n");
results = indexClient.Documents.Search<Hotel>("internet", parameters);
WriteDocuments(results);

Console.WriteLine("Search hello entire index for hello terms 'economy' AND 'hotel':\n");
results = indexClient.Documents.Search<Hotel>("economy AND hotel", parameters);
WriteDocuments(results);
```
Ani dwa dokumenty indeksowanego hello zawierają postanowienia hello, tak aby uzyskujemy hello następujące dane wyjściowe z hello `RunQueriesWithNonExistentTermsInIndex`.
~~~
Search hello entire index for hello phrase "five star":

no document matched

Search hello entire index for hello term 'internet':

no document matched

Search hello entire index for hello terms 'economy' AND 'hotel':

no document matched
~~~

## <a name="enable-synonyms"></a>Włączanie synonimów

Włączenie synonimów to dwuetapowy proces. Firma Microsoft najpierw zdefiniować i przekaż synonim reguły, a następnie skonfiguruj toouse pola je. proces Hello jest opisane w temacie `UploadSynonyms` i `EnableSynonymsInHotelsIndex`.

1. Dodaj usługę wyszukiwania tooyour synonim mapy. W `UploadSynonyms`, możemy zdefiniować cztery reguły w naszym mapy synonim "desc synonymmap" i usługa toohello przekazywania.
```csharp
    var synonymMap = new SynonymMap()
    {
        Name = "desc-synonymmap",
        Format = "solr",
        Synonyms = "hotel, motel\n
                    internet,wifi\n
                    five star=>luxury\n
                    economy,inexpensive=>budget"
    };

    serviceClient.SynonymMaps.CreateOrUpdate(synonymMap);
```
Mapa synonim musi być zgodna standard typu open source toohello `solr` format. Hello format zostało wyjaśnione w dokumencie [synonimy w usłudze Azure Search](search-synonyms.md) sekcji hello `Apache Solr synonym format`.

2. W definicji indeksu hello, należy skonfigurować pola z możliwością przeszukiwania toouse hello synonim mapy. W `EnableSynonymsInHotelsIndex`, włączysz synonimy na dwa pola `category` i `tags` przez ustawienie hello `synonymMaps` toohello nazwę właściwości hello nowo przekazać synonim mapy.
```csharp
  Index index = serviceClient.Indexes.Get("hotels");
  index.Fields.First(f => f.Name == "category").SynonymMaps = new[] { "desc-synonymmap" };
  index.Fields.First(f => f.Name == "tags").SynonymMaps = new[] { "desc-synonymmap" };

  serviceClient.Indexes.CreateOrUpdate(index);
```
Podczas dodawania mapy synonimów ponowne kompilowanie indeksu nie jest wymagane. Można dodać usługę tooyour mapy synonim, a następnie zmiana istniejących definicji pola w dowolnej nowej mapy synonim indeksu toouse hello. dodanie nowych atrybutów Hello nie ma wpływu na dostępność indeksu. Witaj, którego dotyczy to również w wyłączenie synonimy dla pola. Można ustawić po prostu hello `synonymMaps` właściwości tooan pustej listy.
```csharp
  index.Fields.First(f => f.Name == "category").SynonymMaps = new List<string>();
```

## <a name="after-queries"></a>Zapytania „po”

Po przekazaniu mapy synonim hello i indeks hello jest zaktualizowane toouse hello synonim mapy, drugi hello `RunQueriesWithNonExistentTermsInIndex` hello następujących danych wyjściowych wywołania:

~~~
Search hello entire index for hello phrase "five star":

Name: Fancy Stay        Category: Luxury        Tags: [pool, view, wifi, concierge]

Search hello entire index for hello term 'internet':

Name: Fancy Stay        Category: Luxury        Tags: [pool, view, wifi, concierge]

Search hello entire index for hello terms 'economy' AND 'hotel':

Name: Roach Motel       Category: Budget        Tags: [motel, budget]
~~~
Hello pierwszego zapytania znajduje hello dokumentu z reguły hello `five star=>luxury`. Rozszerza Hello drugiego zapytania hello wyszukiwanie przy użyciu `internet,wifi` i hello innej przy użyciu zarówno `hotel, motel` i `economy,inexpensive=>budget` w znajdowaniu dokumentów hello one zgodne.

Dodawanie synonimy całkowicie zmienia hello wyników wyszukiwania. W tym samouczku hello oryginalnego zapytania nie tooreturn znaczących wyników, nawet jeśli były odpowiednie hello dokumenty w indeksie. Przez włączenie synonimy, możemy rozwiń tooinclude indeksu wspólną użyć warunki, bez zmian danych toounderlying hello indeksu.

## <a name="sample-application-source-code"></a>Kod źródłowy przykładowej aplikacji
Można znaleźć hello pełny kod źródłowy hello przykładowej aplikacji używane w tym krokach związanych z na [GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowToSynonyms).

## <a name="next-steps"></a>Następne kroki

* Przegląd [jak synonimy toouse w usłudze Azure Search](search-synonyms.md)
* Zapoznaj się z [Dokumentacją interfejsu API REST synonimów](https://aka.ms/rgm6rq)
* Przeglądaj hello odwołań dla hello [zestawu .NET SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.search) i [interfejsu API REST](https://docs.microsoft.com/rest/api/searchservice/).
