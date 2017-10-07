---
title: "aplikacje mobilne aaaBuild dzięki platformie Xamarin i usłudze Azure DB rozwiązania Cosmos | Dokumentacja firmy Microsoft"
description: "Samouczek, który tworzy Xamarin iOS, Android lub formularzy aplikacji za pomocą bazy danych Azure rozwiązania Cosmos. Azure DB rozwiązania Cosmos jest szybkie, planety skali, bazy danych chmury dla aplikacji mobilnych."
services: cosmos-db
documentationcenter: .net
author: arramac
manager: monicar
editor: 
ms.assetid: ff97881a-b41a-499d-b7ab-4f394df0e153
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/03/2017
ms.author: arramac
ms.openlocfilehash: 362a0e239a61e1309e1cf720c23151760952cf69
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="build-mobile-applications-with-xamarin-and-azure-cosmos-db"></a>Tworzenie aplikacji dla urządzeń przenośnych dzięki platformie Xamarin i usłudze Azure DB rozwiązania Cosmos
Aplikacje mobilne najbardziej potrzebne toostore danych w chmurze hello i bazy danych Azure rozwiązania Cosmos jest bazą danych chmury dla aplikacji mobilnych. Zawiera wszystko, co jest wymagane przez dewelopera przenośnych. Pełni zarządzana baza danych jest jako usługa, która może obsłużyć na żądanie. Uruchamiać aplikacji tooyour danych przejrzysty, wszędzie tam, gdzie użytkownicy znajdują się na całym świecie hello. Za pomocą hello [Azure rozwiązania Cosmos DB .NET Core SDK](documentdb-sdk-dotnet-core.md), można włączyć toointeract aplikacjami mobilnymi Xamarin bezpośrednio z bazy danych z rozwiązania Cosmos platformy Azure, bez warstwy środkowej.

Ten artykuł zawiera samouczek tworzenia aplikacji mobilnych dzięki platformie Xamarin i usłudze Azure DB rozwiązania Cosmos. Możesz znaleźć kodu źródłowego pełną hello samouczek hello na [Xamarin i usłudze Azure DB rozwiązania Cosmos w serwisie GitHub](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/xamarin), w tym jak toomanage użytkowników i uprawnienia.

## <a name="azure-cosmos-db-capabilities-for-mobile-apps"></a>Możliwości rozwiązania Cosmos bazy danych platformy Azure dla aplikacji mobilnych
Azure DB rozwiązania Cosmos zapewnia hello następujących kluczowych możliwości dla deweloperów aplikacji mobilnych:

![Możliwości rozwiązania Cosmos bazy danych platformy Azure dla aplikacji mobilnych](media/mobile-apps-with-xamarin/documentdb-for-mobile.png)

* Zaawansowana zapytania dotyczące danych schematu. Azure DB rozwiązania Cosmos przechowuje dane jako schematu dokumentów JSON w kolekcjach heterogenicznych. Oferuje [zapytania bogaty i szybkie](documentdb-sql-query.md) bez hello potrzebna tooworry o schematów lub indeksy.
* Szybkie przepływności. Trwa tylko kilka milisekund dokumenty tooread i zapis z bazy danych Azure rozwiązania Cosmos. Deweloperzy można określić przepustowość hello, które są im potrzebne, a bazy danych Azure rozwiązania Cosmos honoruje go SLA 99,99%.
* Skala nieograniczona. Kolekcji bazy danych Azure rozwiązania Cosmos [rosnąć w miarę wzrastania aplikacji](partition-data.md). Można uruchomić z rozmiar danych w małych i przepływności setki żądań na sekundę. Kolekcji można powiększać toopetabytes danych i dowolnie dużą przepływność setki miliony żądań na sekundę.
* Globalnie rozproszone. Aplikacji mobilnej, które użytkownicy znajdują się na powitania poprzek, często hello world. Azure DB rozwiązania Cosmos jest [globalnie rozproszoną bazę danych](distribute-data-globally.md). Kliknij przycisk toomake mapy hello użytkownikom tooyour dostępnych danych.
* Wbudowane sformatowanego autoryzacji. Z bazy danych rozwiązania Cosmos platformy Azure, można łatwo zaimplementować popularnych wzorców, takich jak [danych użytkownika](https://aka.ms/documentdb-xamarin-todouser) lub wielodostępnego udostępnionych danych bez kodu złożonych autoryzacji niestandardowej.
* Dane geograficzne zapytania. Wiele aplikacji mobilnych zapewniają kontekstowe geograficznie środowiska dzisiaj. O najwyższej jakości pomoc techniczną dla [typy dane geograficzne](geospatial.md), sprawia, że bazy danych Azure rozwiązania Cosmos tworzenie tooaccomplish łatwe tych środowisk.
* Załączników binarnych. Dane aplikacji zawierają często binarnego obiektów blob. Natywna obsługa załączników ułatwia łatwiejsze toouse bazy danych Azure rozwiązania Cosmos jako zaspokaja dla danych aplikacji.

## <a name="azure-cosmos-db-and-xamarin-tutorial"></a>Samouczek usługi Azure DB rozwiązania Cosmos i Xamarin
Witaj, po samouczku przedstawiono sposób toobuild aplikacjami mobilnymi za pomocą platformy Xamarin i usłudze Azure DB rozwiązania Cosmos. Kod źródłowy pełną hello można znaleźć samouczek hello na [Xamarin i usłudze Azure DB rozwiązania Cosmos w serwisie GitHub](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/xamarin).

### <a name="get-started"></a>Rozpoczęcie pracy
Jest łatwy tooget korzystania z bazy danych Azure rozwiązania Cosmos. Przejdź toohello portalu Azure i Utwórz nowe konto bazy danych Azure rozwiązania Cosmos. Kliknij przycisk hello **szybki start** kartę. Pobieranie hello Xamarin Forms zadań do wykonania listy przykład, który jest już połączony tooyour konta bazy danych Azure rozwiązania Cosmos. 

![Azure DB rozwiązania Cosmos — szybki start dla aplikacji mobilnych](media/mobile-apps-with-xamarin/cosmos-db-quickstart.png)

Lub jeśli masz istniejącą aplikację platformy Xamarin, można dodać hello [pakietu NuGet DB rozwiązania Cosmos Azure](documentdb-sdk-dotnet-core.md). Azure DB rozwiązania Cosmos obsługuje Xamarin.IOS, Xamarin.Android, i biblioteki udostępnione Xamarin Forms.

### <a name="work-with-data"></a>Praca z danymi
Rekordy danych są przechowywane w usłudze Azure DB rozwiązania Cosmos jako schematu dokumentów JSON w kolekcjach heterogenicznych. Dokumenty z różnych struktur można przechowywać w hello tej samej kolekcji:

```cs
    var result = await client.CreateDocumentAsync(collectionLink, todoItem);
```

W projektach Xamarin można użyć zapytania o języku zintegrowanym nad danymi schematu:

```cs
    var query = await client.CreateDocumentQuery<ToDoItem>(collectionLink)
                    .Where(todoItem => todoItem.Complete == false)
                    .AsDocumentQuery();

    Items = new List<TodoItem>();
    while (query.HasMoreResults) {
        Items.AddRange(await query.ExecuteNextAsync<TodoItem>());
    }
```
### <a name="add-users"></a>Dodawanie użytkowników
Jak uzyskać wiele próbek wprowadzenie, przykładowej bazy danych Azure rozwiązania Cosmos hello, pobrany uwierzytelnia toohello usługi przy użyciu ustalony klucza głównego w kodzie aplikacji hello. To ustawienie domyślne nie jest dobrym rozwiązaniem dla aplikacji, które mają toorun dowolnego miejsca, z wyjątkiem sieci lokalnej emulatora. Jeśli nieautoryzowany użytkownik uzyskany klucz główny hello, wszystkie dane hello za pomocą konta Azure DB rozwiązania Cosmos może być zagrożone. Zamiast tego chcesz tooaccess Twojej aplikacji hello tylko rekordy hello zalogowanego użytkownika. Azure DB rozwiązania Cosmos umożliwia deweloperom aplikacji toogrant odczytu lub odczytu/zapisu kolekcji tooa uprawnień, zestaw dokumentów pogrupowane według klucza partycji lub określonego dokumentu. 

Wykonaj te kroki toomodify hello zadań do wykonania listy aplikacji tooa wielodostępnym zadań do wykonania listy aplikacji: 

  1. Dodaj aplikację tooyour logowania za pomocą usługi Facebook, usługi Active Directory lub innego dostawcy.

  2. Utwórz kolekcję usługi Azure rozwiązania Cosmos DB UserItems z **/userId** jako klucza partycji hello. Określanie klucza partycji hello kolekcji umożliwia tooscale bazy danych Azure rozwiązania Cosmos nieograniczonej jako hello liczba użytkowników aplikacji rozwoju, pozostawiając toooffer szybkiego zapytania.

  3. Dodaj Token brokera zasobów Azure rozwiązania Cosmos bazy danych. Ten prosty interfejs API sieci Web uwierzytelnia użytkowników i wystawia tokeny krótkim okresie toosigned użytkowników z dostępem tylko dokumenty toohello ich partycji. W tym przykładzie brokera tokenu zasobów znajduje się w usłudze App Service.

  4. Zmodyfikuj tooResource tooauthenticate aplikacji hello brokera tokenu z usługą Facebook, a Żądanie hello tokenów zasobów dla hello zalogowanych użytkowników usługi Facebook. Można następnie uzyskać dostępu do swoich danych w programie hello UserItems kolekcji.  

Możesz znaleźć tego wzorca na przykład kompletny kod [zasobu brokera tokenu w serwisie GitHub](http://aka.ms/documentdb-xamarin-todouser). Ten diagram przedstawia hello rozwiązania:

![Azure DB rozwiązania Cosmos uprawnienia użytkowników i broker](media/mobile-apps-with-xamarin/documentdb-resource-token-broker.png)

Jeśli chcesz, aby dwa toohello dostępu toohave użytkowników tej samej listy zadań do wykonania, można dodać token dostępu toohello dodatkowe uprawnienia w brokerze Token zasobu.

### <a name="scale-on-demand"></a>Skalowanie na żądanie
Azure DB rozwiązania Cosmos jest zarządzany bazy danych jako usługa. Wraz z rozwojem bazy użytkowników, nie trzeba tooworry dotyczące inicjowania obsługi administracyjnej maszyn wirtualnych lub zwiększenie rdzeni. Tootell bazy danych Azure rozwiązania Cosmos wystarczy wymaga aplikacji liczbę operacji na sekundę (przepływność). Można określić przepustowość hello za pośrednictwem hello **skali** kartę za pomocą miara przepływności wywołuje jednostek żądania (RUs) na sekundę. Operacja odczytu dokumentu 1 KB wymaga na przykład 1 RU. Możesz także dodać alerty toohello **przepływności** toomonitor metryki hello wzrost ruchu i programowo zmienić hello przepływności jak alerty fire.

![Azure DB rozwiązania Cosmos skali przepływności na żądanie](media/mobile-apps-with-xamarin/cosmos-db-xamarin-scale.png)

### <a name="go-planet-scale"></a>Przejdź planety skali
Jako sieci popularne zyski aplikacji może uzyskać użytkowników między Witaj świecie. Lub może być przygotowane na potrzeby nieprzewidzianych toobe. Przejdź toohello portalu Azure i otwórz konto bazy danych Azure rozwiązania Cosmos. Kliknij przycisk hello toomake mapy numer tooany stale replikowanie danych regionów, między hello world. Ta funkcja udostępnia dane wszędzie tam, gdzie są użytkownicy. Można również dodać przygotowany dla warunkowych toobe zasad trybu failover.

![Azure skali DB rozwiązania Cosmos w regionach geograficznych](media/mobile-apps-with-xamarin/cosmos-db-xamarin-replicate.png)

Gratulacje. Ukończono hello rozwiązania i aplikacji mobilnej dzięki platformie Xamarin i usłudze Azure DB rozwiązania Cosmos. Należy wykonać podobne kroki toobuild Cordova aplikacji przy użyciu hello Azure rozwiązania Cosmos DB JavaScript SDK i natywne aplikacje dla systemu iOS/Android przy użyciu interfejsów API REST usługi Azure rozwiązania Cosmos bazy danych.

## <a name="next-steps"></a>Następne kroki
* Wyświetl kod źródłowy hello [Xamarin i usłudze Azure DB rozwiązania Cosmos w serwisie GitHub](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/xamarin).
* Pobierz hello [Azure rozwiązania Cosmos DB .NET Core SDK](documentdb-sdk-dotnet-core.md).
* Znajdź więcej przykładów kodu dla [aplikacji .NET](documentdb-dotnet-samples.md).
* Dowiedz się więcej o [sformatowanego bazy danych Azure rozwiązania Cosmos zapytania możliwości](documentdb-sql-query.md).
* Dowiedz się więcej o [Obsługa dane geograficzne w usłudze Azure DB rozwiązania Cosmos](geospatial.md).



