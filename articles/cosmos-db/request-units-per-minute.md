---
title: "Azure CosmosDB: Jednostek na minutę (RU/m) żądania | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak koszt tooreduce przy użyciu żądania jednostki na minutę."
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 
ms.service: cosmos-db
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: fcc3a92b9788750a2bfba361c3a9cebdb56eee05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="request-units-per-minute-in-azure-cosmos-db"></a>Jednostki żądania na minutę w usłudze Azure DB rozwiązania Cosmos

Azure DB rozwiązania Cosmos jest zaprojektowana toohelp osiągnięcia szybkie, przewidywalną wydajność i skalę bezproblemowo wraz z wzrostu aplikacji. Można udostępnić przepływności w kontenerze DB rozwiązania Cosmos zarówno, na sekundę i szczegółowości na minutę (RU/m). Hello udostępnionej przepływności na minutę szczegółowości jest używane toomanage nieoczekiwany największego obciążenia hello występujących w szczegółowości na sekundę. 

Ten artykuł zawiera omówienie działania hello inicjowania obsługi administracyjnej jednostki żądań na minutę (RU/m). Celem Hello pamiętać z inicjowaniem obsługi administracyjnej RU/m jest tooprovide przewidywalną wydajność wokół nieprzewidywalne potrzeb (zwłaszcza, jeśli potrzebujesz toorun analytics na dane operacyjne) i spiky obciążeń. Chcemy toohave naszym klientom korzystać więcej przepustowości hello, który udostępnia, można szybko skalować z bez obaw.

Po przeczytaniu tego artykułu, będą mogli tooanswer hello następujące pytania:

* Jak działa jednostkę żądań na minutę
* Jaka jest różnica hello jednostki żądania na minutę i jednostki żądania na sekundę?
* Jak tooprovision RU/m?
* W obszarze scenariusza są wziąć pod uwagę inicjowania obsługi administracyjnej jednostki żądania na minutę?
* Jak toouse hello toooptimize metryki portalu Moje kosztów i wydajności?
* Zdefiniuj typy żądań, jaką może wykorzystać budżet RU/m?

## <a name="provisioning-request-units-per-minute-rum"></a>Inicjowanie obsługi administracyjnej jednostki żądania na minutę (RU/m)

Podczas obsługi administracyjnej bazy danych Azure rozwiązania Cosmos w drugiego stopnia szczegółowości hello (RU/s), możesz uzyskać hello gwarancji, że przy niskim opóźnieniem powiedzie się żądanie przepustowość sieci nie przekroczył pojemności hello udostępniane w ramach tego drugiego. Z RU/m szczegółowości hello jest na minutę hello z hello gwarancji, że Twoje żądanie zakończy się pomyślnie w ciągu tej minuty. Porównaniu systemów toobursting możemy upewnij się, że otrzymasz wydajności hello jest atrybutem wartości prognozowanych i można zaplanować na nim.

sposób Hello na minutę inicjowania obsługi administracyjnej działania jest prosty:

* RU/m są rozliczane co godzinę i w dodatku tooRU/s. Aby uzyskać więcej informacji, odwiedź stronę bazy danych Azure rozwiązania Cosmos [cennikiem](https://aka.ms/acdbpricing).
* RU/m może być włączone na poziomie kolekcji. Który może odbywać się za pośrednictwem hello zestawów SDK (Node.js, Java lub .net) lub za pośrednictwem portalu hello (również obejmować obciążeń bazy danych MongoDB interfejsu API)
* Po włączeniu RU/m, dla każdego 100 RU/s alokacji również uzyskać 1 000 RU/m udostępniane (stosunek hello jest 10 x)
* W drugiej danej, jednostka żądania zużywa Twojej RU/m udostępniania tylko wtedy, gdy został przekroczony z na drugi udostępniania w ramach tego drugiego
* Raz hello 60 sekund czasu (UTC) zakończenia, hello na minutę inicjowania obsługi administracyjnej jest uzupełniania
* RU/m można włączyć tylko w przypadku kolekcji z maksymalną inicjowania obsługi 5000 RU/s dla każdej partycji. Jeśli skalować potrzeb przepływności i wysoki poziom obsługi na partycję, otrzyma komunikat ostrzegawczy

Poniżej jest konkretnym przykładzie, w którym klient może udostępnić 10kRU/s z 100kRU/m, zapisywanie 73% w koszt Inicjowanie obsługi szczytowego (w 50kRU na sekundę) za pośrednictwem okres 90 sekund na kolekcję, która ma 10 000 RU/s do 100 000 RU/m udostępniane:

* 1 sekundę: hello RU/m budżetu jest ustawiona na 100 000
* 3 sekundy: podczas tej drugiej hello zużycie jednostki żądania zostało 11,010 RUs 1,010 RUs powyżej hello RU/s inicjowania obsługi administracyjnej. W związku z tym 1,010 RUs odejmuje się z hello RU/m budżetu. 98,990 RUs są dostępne dla hello dalej sekund 57 hello budżetu RU/m
* 29 sekundę: podczas tego drugiego wystąpiły duże kolekcji (> 4 x wyższe niż inicjowania obsługi na sekundę) i 46,920 RUs hello zużycia jednostki żądania. 36,920 RUs odejmuje się od budżetu RU/m hello z 92,323 too55 RUs (28 sekunda), RUs 403 (29 sekundy)
* drugie 61st: budżetu RU/m jest ustawiana too100, 000 RUs.
 
![Wykres przedstawiający zużycie hello i inicjowania obsługi bazy danych Azure rozwiązania Cosmos](./media/request-units-per-minute/azure-cosmos-db-request-units-per-minute.png)

## <a name="specifying-request-unit-capacity-with-rum"></a>Określanie pojemność jednostki żądania przy użyciu RU/m

Podczas tworzenia kolekcji usługi Azure DB rozwiązania Cosmos, określ numer hello jednostek żądań na sekundę (RU na sekundę) mają zastrzeżone dla hello kolekcji. Można również określić, czy RU tooadd na minutę. Można to zrobić za pośrednictwem portalu hello lub hello zestawu SDK. 

### <a name="through-hello-portal"></a>Za pomocą hello portalu

Włączanie lub wyłączanie RU na minutę po prostu wymaga kliknięcia podczas inicjowania obsługi administracyjnej kolekcji. 

 ![Zrzut ekranu przedstawiający sposób tooset RU/m w hello portalu Azure](./media/request-units-per-minute/azure-cosmos-db-request-unit-per-minute-portal.png)

### <a name="through-hello-sdk"></a>Za pomocą hello zestawu SDK
Po pierwsze jest ważne toonote czy RU/m jest dostępna tylko dla następujących zestawów SDK hello:

* .NET 1.14.0
* Java 1.11.0
* Node.js 1.12.0
* Python 2.2.0

Oto fragment kodu dotyczący tworzenia kolekcji z 3000 jednostki żądania na żądanie drugi i 30 000 jednostek na minutę przy użyciu zestawu .NET SDK hello:

```csharp
// Create a collection with RU/m enabled
DocumentCollection myCollection = new DocumentCollection();
myCollection.Id = "coll";
myCollection.PartitionKey.Paths.Add("/deviceId");

// Set hello throughput too3,000 request units per second which will give you 30,000 request units per minute as hello RU/m budget
await client.CreateDocumentCollectionAsync(
    UriFactory.CreateDatabaseUri("db"),
    myCollection,
    new RequestOptions { OfferThroughput = 3000, OfferEnableRUPerMinuteThroughput = true });
```

Oto fragment kodu do zmiany hello przepływność too5 kolekcji, 000 jednostek żądań na sekundę bez udostępniania RU na użyciu minuty hello zestawu .NET SDK:

```csharp
// Get hello current offer
Offer offer = client.CreateOfferQuery()
    .Where(r => r.ResourceLink == collection.SelfLink)    
    .AsEnumerable()
    .SingleOrDefault();

// Set hello throughput too5000 request units per second without RU/m enabled (hello last parameter tooOfferV2 constructor below)
OfferV2 offerV2 = new OfferV2(offer, 5000, false);

// Now persist these changes toohello database by replacing hello original resource
await client.ReplaceOfferAsync(offerV2);
```

## <a name="good-fit-scenarios"></a>Dobra obejmował scenariusze

W tej sekcji firma Microsoft udostępnia przegląd scenariuszy, które są dobrze umożliwiających jednostek żądań na minutę.

**Tworzenie/testowanie środowiska:** dobrze. Na etapie programowania hello w przypadku testowania aplikacji z różnych obciążeń RU/m zapewniają elastyczność hello na tym etapie. Podczas hello [emulatora](local-emulator.md) to doskonałe narzędzie wolnego tootest bazy danych Azure rozwiązania Cosmos. Jednak jeśli chcesz toostart w środowisku chmury, konieczne będzie dużą elastyczność przy RU/m do potrzeb wydajności ad hoc. Zostanie poświęcić więcej czasu na tworzenie mniej niepokojącego o potrzebach wydajności na początku. Zaleca się, począwszy od hello minimalna inicjowania obsługi RU/s i włączyć RU/m.

**Wymaga szczegółowości nieprzewidywalne, spiky, minuty:** dobrej dopasowania — oszczędności: 25 75%. Zaobserwowano są duże korzyści z większości środowisk produkcyjnych i RU/m do tej grupy. Jeśli masz obciążenie IoT, które ma kilka razy w ciągu jednej minuty, kolekcji, jeśli masz zapytań wykonywanych po systemu sprawia, że masa wstawić na powitania sama godzina, konieczne będzie dodatkowej pojemności dla potrzeb handeling spiky. Firma Microsoft zaleca optymalizacji zapotrzebowanie na zasoby, stosując nasze podejście krok po kroku poniżej.

 ![Wykres przedstawiający zużycie żądania w szczegółowości 5 minut](./media/request-units-per-minute/azure-cosmos-db-request-units-per-minute-consumption.png)
 
 *Rysunek - RU zużycie testu*

**Spokój umysłu:** dobrej dopasowania — oszczędności: 10-20%. Czasami po prostu chcesz spokój toohave i nie martw się o potencjalnych pików i ograniczania przepustowości. Ta funkcja jest hello odpowiedniej jeden dla Ciebie. W takim przypadku zaleca się włączenie RU/m i nieco niższy użytkownika na drugim inicjowania obsługi administracyjnej. Przypadek różni się od hello powyżej, ponieważ użytkownik nie będzie podejmował toooptimize agresywnie programu obsługi. Jest to jeden mindset "Zero ograniczania", które znajdują się w.

Ważne operacje o potrzebach ad hoc: Firma Microsoft zaleca czasami tooonly let ważne operacje dostępu RU/m budżetu, dlatego nie pobrać budżetu hello korzystanie przez ad hoc lub mniej ważne operacje. Który można łatwo zdefiniować w sekcji hello poniżej.

## <a name="using-hello-portal-metrics-toooptimize-cost-and-performance"></a>Przy użyciu hello portalu metryki toooptimize kosztów i wydajności

**W najbliższych tygodniach hello firma Microsoft będzie kontynuować rozwijanie hello zawartością wokół monitorowania toooptimize minuty zużycie RUs, przepustowość sieci musi.**

Za pomocą portalu metryki hello widać, jaka część regularne sekund RU zużywają i RU minut. Monitorowanie tych metryk powinny pomóc w optymalizacji programu obsługi. 

Zalecane podejście krok po kroku na temat toouse RU/m tooyour korzyści. Dla każdego kroku powinny mieć omówienie zużycia hello RU reprezentujący pełnego cyklu obciążenie (możliwe, godziny, dni lub nawet tygodnie) i uzyskiwanie szczegółowych informacji na powitania wykorzystania można udostępnić.

zasada Hello za takie podejście jest toomake udostępniania przepływności jako zamknąć jako możliwych tooa inicjowania obsługi administracyjnej punktu, który jest zgodna z kryteriami wydajności poniżej. 

![Wykres przedstawiający zużycie żądania w 5-minutowy szczegółowości](./media/request-units-per-minute/azure-cosmos-db-request-units-per-minute-adjust-provisioning.png)
 
toounderstand hello optymalne inicjowania obsługi administracyjnej punktu dla obciążenia, należy toounderstand:

* Wzorce użycia: Brak, rzadko lub utrzymujących nagłego? Mała liczba godzin (średnia x 2), średnich i dużych (> 10 x średniej) nagłego?
* Procent żądań ograniczeniem przepustowości: czy można bezpiecznie mając z bitowego ograniczania przepustowości? Jeśli tak, jak duże? 

Po zidentyfikowaniu, jakie są cele, będzie tooget stanie bliżej toohello optymalną inicjowania obsługi administracyjnej.

tooassist, chcemy tooprovide ogólne wskazówki dotyczące sposobu toooptimize Twojego inicjowania obsługi na podstawie RU/m użycia. W tych wskazówkach nie ma zastosowania tooall rodzaju obciążenia, ale jest oparta na powitania wiedzy prywatnej wersji zapoznawczej. Firma Microsoft może zmienić takie linii bazowych jak możemy Dowiedz się więcej:

|RU/m % wykorzystania|Stopień wykorzystania RU/m|Zalecane akcje dotyczące inicjowania obsługi administracyjnej|
|---|---|---|
|0-1%|W obszarze wykorzystania|Dolny więcej RU/m tooconsume RU/s|
|1-10%|Użyj dobrej kondycji|Zachowaj hello sam inicjowania obsługi administracyjnej poziom|
|Powyżej 10%|Przez użycie|Zwiększ RU/s toorely mniej na RU/m|

## <a name="select-which-operations-can-consume-hello-rum-budget"></a>Wybierz, jakie operacje, jaką może wykorzystać hello budżetu RU/m

Na poziomie żądania użytkownik może także włączanie/wyłączanie RU/m budżetu tooserve hello żądania niezależnie od typu operacji. Regularne elastycznie budżetu RUs na sekundę jest zużywany hello żądania nie mogą korzystać z hello RU/m budżetu, zostanie ograniczony tego żądania. Domyślnie wszystkie żądania jest obsługiwana przez budżetu RU/m, jeśli RU/m przepływności budżetu jest aktywna. 

Oto fragment kodu dotyczący wyłączenie budżetu RU/m przy użyciu hello interfejsu API usługi DocumentDB dla operacji CRUD i zapytań.

```csharp
// In order toodisable any CRUD request for RU/m, set DisableRUPerMinuteUsage tootrue in RequestOptions
await client.CreateDocumentAsync(
    UriFactory.CreateDocumentCollectionUri("db", "container"),
    new Document { Id = "Cosmos DB" },
    new RequestOptions { DisableRUPerMinuteUsage = true });
// In order toodisable any query request for RU/m, set DisableRUPerMinuteOnRequest tootrue in RequestOptions
FeedOptions feedOptions = new FeedOptions();
feedOptions.DisableRUPerMinuteUsage = true;
var query = client.CreateDocumentQuery<Book>(
    UriFactory.CreateDocumentCollectionUri("db", "container"),
    "select * from c",feedOptions).AsDocumentQuery();
```

## <a name="next-steps"></a>Następne kroki

W tym artykule możemy zostały opisane działa jak partycjonowania w usłudze Azure DB rozwiązania Cosmos, tworzenia kolekcji partycjonowanych i jak można wybrać stanowi dobry klucz partycji aplikacji.

* Należy przeprowadzić testowanie z bazy danych Azure rozwiązania Cosmos wydajności i skalowania. Zobacz [wydajności i skalowania testowania z bazy danych Azure rozwiązania Cosmos](performance-testing.md) przykładowe.
* Rozpoczynanie pracy kodowania z hello [zestawów SDK](documentdb-sdk-dotnet.md) lub hello [interfejsu API REST](/rest/api/documentdb/).
* Dowiedz się więcej o [udostępnionej przepływności](request-units.md) w usłudze Azure DB rozwiązania Cosmos 

