---
title: "aaaRequest jednostki i planowania przepływności - DB rozwiązania Cosmos Azure | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie toounderstand, określ i oszacować wymagania dotyczące jednostki żądania w usłudze Azure DB rozwiązania Cosmos."
services: cosmos-db
author: mimig1
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: d0a3c310-eb63-4e45-8122-b7724095c32f
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: 13c4e7aeb6222fa14ef982e238716e15a0159fd5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="request-units-in-azure-cosmos-db"></a>Żądanie jednostki w Azure rozwiązania Cosmos bazy danych
Teraz dostępne: Azure DB rozwiązania Cosmos [Kalkulator jednostki żądania](https://www.documentdb.com/capacityplanner). Dowiedz się więcej w [Szacowanie przepustowość sieci musi](request-units.md#estimating-throughput-needs).

![Kalkulator przepływności][5]

## <a name="introduction"></a>Wprowadzenie
[Azure DB rozwiązania Cosmos](https://azure.microsoft.com/services/cosmos-db/) jest globalnie rozproszone wielu modelu bazy danych firmy Microsoft. Z bazy danych rozwiązania Cosmos platformy Azure nie toorent z maszyn wirtualnych, wdrażania oprogramowania lub monitora bazy danych. Azure DB rozwiązania Cosmos jest obsługiwane i stale monitorowane przez program Microsoft inżynierów najwyższego toodeliver światowej klasy dostępności, wydajności i danych ochrony. Są dostępne dane przy użyciu interfejsów API wybranych jako [SQL usługi DocumentDB](documentdb-sql-query.md) (dokument) bazy danych MongoDB (dokument), [Azure Table Storage](https://azure.microsoft.com/services/storage/tables/) (klucz wartość) i [Gremlin](https://tinkerpop.apache.org/gremlin.html) (wykres) znajdują się w obsługiwane. Waluta Hello Azure DB rozwiązania Cosmos jest hello jednostek żądań (RU). RUs nie wymaga możliwości odczytu/zapisu tooreserve lub udostępnić Procesora, pamięci i IOPS.

Azure DB rozwiązania Cosmos obsługuje kilka interfejsów API z różnych operacji — od prostych odczytuje i zapisuje toocomplex zapytania wykresu. Ponieważ nie wszystkie żądania są takie same, są przypisane znormalizowane ilość **jednostek żądania** na podstawie kwoty hello obliczenia wymagane tooserve hello żądania. Liczba Hello jednostek żądania dla operacji jest deterministyczna, a można śledzić hello liczby jednostek żądania używane przez żadnych operacji w usłudze Azure DB rozwiązania Cosmos za pośrednictwem nagłówka odpowiedzi. 

tooprovide przewidywalną wydajność, należy tooreserve przepływności w jednostkach 100 RU/sekundę. 

Po przeczytaniu tego artykułu, będziesz w stanie tooanswer hello następujące pytania:  

* Co to są jednostek żądania i żądania opłat?
* Jak określić żądanie pojemność jednostki dla kolekcji?
* Jak oszacować musi jednostki żądania Moja aplikacja
* Co się stanie, jeśli I przekracza pojemność jednostki żądania dla kolekcji?

Bazy danych Azure rozwiązania Cosmos jest wiele modeli bazy danych, jest ważne toonote, że dokument interfejsu API, wykres/węzła Graph API i tabeli na jednostkę tabeli interfejsu API odnoszą się tooa kolekcji lub dokumentu. Przepływność tego dokumentu, firma Microsoft będzie generalize pojęcia toohello kontenera/elementu.

## <a name="request-units-and-request-charges"></a>Jednostek żądania i żądania opłat
Azure DB rozwiązania Cosmos zapewnia szybkie, przewidywalną wydajność przez *rezerwowania* musi przepływność aplikacji toosatisfy zasobów.  Ponieważ aplikacji obciążenia oraz dostęp wzorce zmian w czasie, bazy danych Azure rozwiązania Cosmos pozwala zwiększyć tooeasily lub zmniejszyć ilość hello zarezerwowaną przepływnością tooyour dostępnych aplikacji.

Z bazy danych Azure rozwiązania Cosmos zarezerwowaną przepływnością jest określane w przeliczeniu na jednostki żądania przetwarzania na sekundę. Można potraktować jednostki żądania jako walutę przepływności, zgodnie z którymi możesz *zarezerwować* ilość gwarantowane jednostki żądania tooyour dostępnych aplikacji na podstawie sekundowym.  Każdej operacji w usłudze Azure DB rozwiązania Cosmos — zapisywanie dokumentu, wykonywania zapytania, aktualizowanie dokumentu — korzysta z Procesora, pamięci i IOPS.  Oznacza to, że każda operacja wiąże się z *żądań bezpłatnie*, który jest wyrażona w *jednostek żądania*.  Opis czynników hello, to wpływ na koszty jednostki żądania, oraz wymagania dotyczące przepływności aplikacji, umożliwia toorun możesz aplikacji jako koszt skutecznie, jak to możliwe. Eksplorator zapytań Hello jest również podstawowa cudowne narzędzie tootest hello zapytania.

Zalecamy rozpoczęcie pracy od obejrzenia powitania po wideo, w którym Aravind Ramachandran wyjaśniono jednostek żądania i przewidywalną wydajność bazy danych Azure rozwiązania Cosmos.

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Predictable-Performance-with-DocumentDB/player]
> 
> 

## <a name="specifying-request-unit-capacity-in-azure-cosmos-db"></a>Określanie pojemność jednostki żądania w usłudze Azure DB rozwiązania Cosmos
Przy uruchamianiu nową kolekcję, tabeli lub wykres, określ numer hello jednostek żądań na sekundę (RU na sekundę) mają zastrzeżone. Oparte na powitania udostępnionej przepływności, bazy danych rozwiązania Cosmos Azure przydziela toohost partycji fizycznej kolekcji i podziałów/rebalances danych na partycji jako ich przyrostu.

Azure DB rozwiązania Cosmos wymaga toobe klucza partycji określone, gdy kolekcja jest inicjowana z 2500 jednostek żądania lub nowszej. Klucz partycji jest również wymagany tooscale przepływność kolekcji poza 2500 jednostki żądania w przyszłości hello. W związku z tym zdecydowanie zaleca się tooconfigure [klucza partycji](partition-data.md) podczas tworzenia kontenera niezależnie od programu początkowej przepływności. Ponieważ dane mogą mieć toobe podzielić na wiele partycji, jest konieczne toopick klucza partycji, który ma dużej kardynalności (100 toomillions unikatowe wartości), dzięki czemu żądania i kolekcji/tabeli/graph mogą być skalowane jednolicie Azure DB rozwiązania Cosmos. 

> [!NOTE]
> Klucz partycji to logiczne granic, a nie jeden fizyczny. W związku z tym nie trzeba toolimit hello liczba wartości kluczy partycji distinct. W rzeczywistości jest znacznie lepszą toohave partycji wartości klucza niż mniej, jako bazy danych rozwiązania Cosmos Azure ma więcej opcje równoważenia obciążenia.

Oto fragment kodu dotyczący tworzenia kolekcji z 3000 żądania jednostek na drugi przy użyciu hello zestawu .NET SDK:

```csharp
DocumentCollection myCollection = new DocumentCollection();
myCollection.Id = "coll";
myCollection.PartitionKey.Paths.Add("/deviceId");

await client.CreateDocumentCollectionAsync(
    UriFactory.CreateDatabaseUri("db"),
    myCollection,
    new RequestOptions { OfferThroughput = 3000 });
```

Azure DB rozwiązania Cosmos działa modelu rezerwacji przepływności. Oznacza to, że są rozliczane hello ilość przepustowości *zastrzeżone*, niezależnie od tego, jaka część tego przepływności jest aktywnie *używane*. Jako aplikacji obciążenia, danych i stosowania wzorców zmiany możesz łatwo skalować w górę i w dół hello ilość zastrzeżone RUs za pomocą zestawów SDK lub przy użyciu hello [Azure Portal](https://portal.azure.com).

Każda kolekcja/tabeli/wykresu są mapowane tooan `Offer` zasobów w usłudze Azure DB rozwiązania Cosmos mającej metadane dotyczące hello udostępnionej przepływności. Możesz zmienić przepływności hello przydzielone wyszukiwania hello odpowiadający jej zasób oferta dla kontenera, a następnie Uaktualnianie hello nową wartość przepływności. Oto fragment kodu do zmiany hello przepływność too5 kolekcji, 000 jednostek żądań na drugi przy użyciu hello zestawu .NET SDK:

```csharp
// Fetch hello resource toobe updated
Offer offer = client.CreateOfferQuery()
                .Where(r => r.ResourceLink == collection.SelfLink)    
                .AsEnumerable()
                .SingleOrDefault();

// Set hello throughput too5000 request units per second
offer = new OfferV2(offer, 5000);

// Now persist these changes toohello database by replacing hello original resource
await client.ReplaceOfferAsync(offer);
```

Jeśli zmienisz przepływności hello jest wpływ dostępności toohello Twojego kontenera. Zazwyczaj nowe zarezerwowaną przepływnością hello obowiązuje w ciągu kilku sekund na aplikacji hello przepływności nowe.

## <a name="request-unit-considerations"></a>Zagadnienia dotyczące jednostki żądania
Podczas oceny hello liczba tooreserve jednostki żądania dla Twojej bazy danych Azure rozwiązania Cosmos kontenera, jest ważne tootake hello następujące zmienne pod uwagę:

* **Rozmiar elementu**. Rozmiar zwiększa tooread jednostki używane hello lub zwiększa zapis hello danych.
* **Liczba właściwości elementu**. Zakładając, że domyślna indeksowania wszystkich właściwości, hello toowrite zużywanych jednostek, które dokumentu/węzła/ntity zwiększa się wraz ze wzrostem liczby właściwości hello.
* **Spójność danych**. Po za pomocą poziomów spójności danych silne lub ograniczonych nieaktualności, dodatkowych jednostek będzie wykorzystanych tooread elementów.
* **Właściwości indeksowanych**. Zasady indeksu na każdego kontenera określa właściwości, które są indeksowane domyślnie. Można ograniczyć zużycie jednostki Twoje żądanie, przez ograniczanie liczby hello właściwości indeksowanych lub włączenie indeksowanie z opóźnieniem.
* **Indeksowanie dokumentów**. Domyślnie każdy element jest indeksowany automatycznie będą korzystać mniejszej liczby jednostek żądania, jeśli wybierzesz nie tooindex niektórych elementów.
* **Zapytanie wzorce**. złożoność Hello zapytania ma wpływ na liczbę jednostek żądania są używane dla operacji. Hello liczba predykatów, rodzaj predykaty hello, projekcje, liczba funkcji UDF i hello rozmiaru zestawu danych źródła hello wszystkie wpływ koszt hello zapytania operacji.
* **Użycie skryptu**.  Podobnie jak w przypadku zapytań, procedury składowane i wyzwalaczy wykorzystywać oparte na powitania złożoność operacjom hello jednostki żądania. Podczas opracowywania aplikacji hello żądań bezpłatnie sprawdzić toobetter nagłówka zrozumieć, jak każdej operacji zajmuje pojemność jednostki żądania.

## <a name="estimating-throughput-needs"></a>Planowania potrzeb w zakresie przepustowości
Jednostka żądania jest znormalizowane miara kosztu przetwarzania żądania. Jednostka pojedyncze żądanie reprezentuje tooread wymaganą wydajność przetwarzania hello (za pośrednictwem łączy własnych lub identyfikator) pojedynczego 1KB elementu składające się z 10 unikatowe wartości (z wyjątkiem właściwości systemu). Żądanie toocreate (Wstaw), Zamień lub usuń hello sam element zajmie więcej przetwarzania z usługi hello i tym samym więcej jednostek żądania.   

> [!NOTE]
> linii bazowej Hello jednostki 1 żądanie dla 1KB elementu odpowiada tooa proste UZYSKAĆ łącze własne lub identyfikator elementu hello.
> 
> 

Na przykład, w tym miejscu jest tabelę, która pokazuje, ile żądań tooprovision jednostki na trzy rozmiary innego elementu (1KB, 4KB do 64KB) i na dwa różne poziomy wydajności (odczyty 500 na sekundę 100 zapisy na sekundę i 500 odczyty/sekundę + 500 zapisy na sekundę). spójność danych Hello został skonfigurowany na sesji i hello indeksowania zasad ustawiono tooNone.

<table border="0" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td valign="top"><p><strong>Rozmiar elementu</strong></p></td>
            <td valign="top"><p><strong>Odczyty/sekundę</strong></p></td>
            <td valign="top"><p><strong>Zapisy na sekundę</strong></p></td>
            <td valign="top"><p><strong>Jednostki żądania</strong></p></td>
        </tr>
        <tr>
            <td valign="top"><p>1 KB</p></td>
            <td valign="top"><p>500</p></td>
            <td valign="top"><p>100</p></td>
            <td valign="top"><p>(500 * 1) + (100 * 5) = 1 000 RU/s</p></td>
        </tr>
        <tr>
            <td valign="top"><p>1 KB</p></td>
            <td valign="top"><p>500</p></td>
            <td valign="top"><p>500</p></td>
            <td valign="top"><p>(500 * 1) + (500 * 5) = 3 000 RU/s</p></td>
        </tr>
        <tr>
            <td valign="top"><p>4 KB</p></td>
            <td valign="top"><p>500</p></td>
            <td valign="top"><p>100</p></td>
            <td valign="top"><p>(500 * 1,3) + (100 * 7) = 1,350 RU/s</p></td>
        </tr>
        <tr>
            <td valign="top"><p>4 KB</p></td>
            <td valign="top"><p>500</p></td>
            <td valign="top"><p>500</p></td>
            <td valign="top"><p>(500 * 1,3) + (500 * 7) = 4,150 RU/s</p></td>
        </tr>
        <tr>
            <td valign="top"><p>64 KB</p></td>
            <td valign="top"><p>500</p></td>
            <td valign="top"><p>100</p></td>
            <td valign="top"><p>(500 * 10) + (100 * 48) = 9,800 RU/s</p></td>
        </tr>
        <tr>
            <td valign="top"><p>64 KB</p></td>
            <td valign="top"><p>500</p></td>
            <td valign="top"><p>500</p></td>
            <td valign="top"><p>(500 * 10) + (500 * 48) = 29,000 RU/s</p></td>
        </tr>
    </tbody>
</table>

### <a name="use-hello-request-unit-calculator"></a>Użycie kalkulatora jednostki żądania hello
Klienci toohelp poprawnie dostroić ich ocen przepływności, jest opartego na sieci web [Kalkulator jednostki żądania](https://www.documentdb.com/capacityplanner) wymagań hello szacowania toohelp jednostki żądania dla operacji typowych, w tym:

* Element tworzy (zapisy)
* Odczytuje element
* Usuwa element
* Element aktualizacji

Narzędzie Hello obejmuje również obsługę Szacowanie oparte na powitania przykładowych elementów podane wymagania dotyczące przechowywania danych.

Za pomocą narzędzia hello jest prosty:

1. Należy przekazać co najmniej jeden element reprezentatywny.
   
    ![Przekaż Kalkulator jednostki żądania toohello elementów][2]
2. wymagania dotyczące magazynu danych tooestimate, wprowadź hello łączna liczba elementów spodziewasz się toostore.
3. Wprowadź hello liczba elementów tworzenia, odczytu, aktualizacji i usuwania działań, które wymagają (na podstawie na sekundę). opłaty za jednostki żądania hello tooestimate elementu operacji aktualizacji, Przekaż kopię hello próbka z kroku 1 zawiera pole typowe aktualizacje.  Na przykład jeśli element aktualizacje zwykle zmodyfikować dwie właściwości o nazwie lastLogin i userVisits, a następnie po prostu skopiuj element przykładowych hello, zaktualizuj hello wartości tych dwóch właściwości i przekaż hello skopiowany element.
   
    ![Wprowadź wymagania dotyczące przepływności w Kalkulator jednostki żądania hello][3]
4. Kliknij przycisk Oblicz i wyniki hello sprawdzić.
   
    ![Wyniki Kalkulator jednostki żądania][4]

> [!NOTE]
> Jeśli masz typów elementów, które różnią się znacznie pod względem rozmiaru i hello liczbę właściwości indeksowanych, Przekaż przykładowe każdego *typu* z toohello elementu typowe narzędzia, a następnie obliczyć hello wyników.
> 
> 

### <a name="use-hello-azure-cosmos-db-request-charge-response-header"></a>Użyj nagłówka odpowiedzi opłat hello Azure DB rozwiązania Cosmos żądania
Każdy odpowiedź z hello Azure DB rozwiązania Cosmos usługi zawiera niestandardowy nagłówek (`x-ms-request-charge`) zawiera jednostki żądania hello używane dla hello żądania. Ten nagłówek jest również dostępny za pośrednictwem hello Azure rozwiązania Cosmos DB SDK. W hello zestawu .NET SDK RequestCharge jest właściwością obiektu ResourceResponse hello.  Dla zapytań hello Eksploratora zapytań DB rozwiązania Cosmos Azure w portalu Azure hello informacje żądania opłaty dotyczące wykonywane zapytania.

![Badanie RU opłat w hello Eksploratora zapytań][1]

Pamiętając o tym, jedną z metod szacowania hello ilość zarezerwowaną przepływnością wymagane przez aplikację jest toorecord hello żądania jednostki opłat związanych z prowadzeniem typowymi operacjami względem elementu reprezentatywny używanych przez aplikację, a następnie Szacowanie hello liczba operacji przewidywania wykonywania każdej sekundy.  Można się toomeasure i obejmują typowe zapytania i również użycie skryptu bazy danych Azure rozwiązania Cosmos.

> [!NOTE]
> Jeśli masz typów elementów, które różnią się znacznie pod względem rozmiaru i hello liczbę właściwości indeksowanych rejestrowania hello odpowiednich operacji żądania jednostki opłat związanych z każdym *typu* typowe elementu.
> 
> 

Na przykład:

1. Zarejestruj hello żądania jednostkę opłatą tworzenia (Wstawianie) typowe elementu. 
2. Opłata jednostki żądania rekordów hello odczytywania typowe elementu.
3. Opłata jednostki żądania rekordów hello aktualizowania typowych elementu.
4. Opłata jednostki żądania hello rekordów zapytań typowe, wspólnego elementu.
5. Witaj rekordów żądania jednostki opłat skrypty niestandardowe (procedury składowane, wyzwalacze, funkcje zdefiniowane przez użytkownika) wykorzystywane przez aplikacji hello
6. Oblicz hello żądania wymaganych jednostek podanych hello szacowana liczba operacji przewidujesz toorun każdej sekundy.

### <a id="GetLastRequestStatistics"></a>Za pomocą interfejsu API dla bazy danych MongoDB w GetLastRequestStatistics polecenia
Interfejs API bazy danych mongodb obsługuje polecenia niestandardowych, *getLastRequestStatistics*, pobierania hello opłat żądania dla określonej operacji.

Na przykład w hello powłokę Mongo, wykonaj operację hello, którą chcesz tooverify hello żądania opłata za.
```
> db.sample.find()
```

Następnie wykonaj polecenie hello *getLastRequestStatistics*.
```
> db.runCommand({getLastRequestStatistics: 1})
{
    "_t": "GetRequestStatisticsResponse",
    "ok": 1,
    "CommandName": "OP_QUERY",
    "RequestCharge": 2.48,
    "RequestDurationInMilliSeconds" : 4.0048
}
```

Pamiętając o tym, jedną z metod szacowania hello ilość zarezerwowaną przepływnością wymagane przez aplikację jest toorecord hello żądania jednostki opłat związanych z prowadzeniem typowymi operacjami względem elementu reprezentatywny używanych przez aplikację, a następnie Szacowanie hello liczba operacji przewidywania wykonywania każdej sekundy.

> [!NOTE]
> Jeśli masz typów elementów, które różnią się znacznie pod względem rozmiaru i hello liczbę właściwości indeksowanych rejestrowania hello odpowiednich operacji żądania jednostki opłat związanych z każdym *typu* typowe elementu.
> 
> 

## <a name="use-api-for-mongodbs-portal-metrics"></a>Za pomocą interfejsu API dla bazy danych MongoDB w portalu metryki
Witaj najprostszym tooget sposób dobrej szacowania jednostki żądania opłaty do interfejsu API dla bazy danych MongoDB jest toouse hello [portalu Azure](https://portal.azure.com) metryki. Z hello *liczba żądań* i *opłat żądania* wykresy, można uzyskać oszacowanie liczbę jednostek żądania każdej operacji jest wykorzystywanie i liczbę jednostek żądania zużywają tooone względną innej.

![Interfejs API dla metryki portalu bazy danych MongoDB][6]

## <a name="a-request-unit-estimation-example"></a>W przykładzie szacowania jednostki żądania
Należy wziąć pod uwagę powitania po ~ 1KB dokumentu:

```json
{
 "id": "08259",
  "description": "Cereals ready-to-eat, KELLOGG, KELLOGG'S CRISPIX",
  "tags": [
    {
      "name": "cereals ready-to-eat"
    },
    {
      "name": "kellogg"
    },
    {
      "name": "kellogg's crispix"
    }
  ],
  "version": 1,
  "commonName": "Includes USDA Commodity B855",
  "manufacturerName": "Kellogg, Co.",
  "isFromSurvey": false,
  "foodGroup": "Breakfast Cereals",
  "nutrients": [
    {
      "id": "262",
      "description": "Caffeine",
      "nutritionValue": 0,
      "units": "mg"
    },
    {
      "id": "307",
      "description": "Sodium, Na",
      "nutritionValue": 611,
      "units": "mg"
    },
    {
      "id": "309",
      "description": "Zinc, Zn",
      "nutritionValue": 5.2,
      "units": "mg"
    }
  ],
  "servings": [
    {
      "amount": 1,
      "description": "cup (1 NLEA serving)",
      "weightInGrams": 29
    }
  ]
}
```

> [!NOTE]
> Dokumenty są zminimalizowany w usłudze Azure DB rozwiązania Cosmos, więc hello system obliczeniowe rozmiar dokumentu hello powyżej jest nieco mniej niż 1 KB.
> 
> 

Witaj poniższej tabeli przedstawiono przybliżone żądania jednostki związanych z typowymi operacjami na tym elemencie (opłat jednostki żądania przybliżonej hello zakłada poziomu spójności konta hello ustawiono zbyt "Sesja" i że wszystkie elementy są automatycznie indeksowane):

| Operacja | Opłata jednostki żądania |
| --- | --- |
| Utwórz element |~ 15 RU |
| Odczytu elementu |~ 1 RU |
| Element zapytania według identyfikatora |~2.5 RU |

Ponadto w poniższej tabeli zamieszczono przybliżonej żądania jednostki opłat za typowe zapytania używane w aplikacji hello:

| Zapytanie | Opłata jednostki żądania | Liczba zwróconych elementów |
| --- | --- | --- |
| Wybierz żywności według identyfikatora |~2.5 RU |1 |
| Wybierz żywności według producenta |~ 7 RU |7 |
| Wybierz grupy żywności i kolejność według wagi |~ 70 RU |100 |
| Zaznacz górny żywności 10 w grupie żywności |~ 10 RU |10 |

> [!NOTE]
> Opłaty RU różnić w zależności od hello liczbę zwracanych elementów.
> 
> 

Dzięki tym informacjom możemy oszacować hello RU wymagania dla tej aplikacji, podanych hello liczby operacji i zapytań Oczekujemy na sekundę:

| Operacja/zapytania | Szacowaną liczbę na sekundę | Wymagane RUs |
| --- | --- | --- |
| Utwórz element |10 |150 |
| Odczytu elementu |100 |100 |
| Wybierz żywności według producenta |25 |175 |
| Wybierz grupy żywności |10 |700 |
| Wybierz 10 pierwszych |15 |Łącznie 150 |

W takim przypadku oczekujemy wymaganie średniej przepływności 1,275 RU/s.  Zaokrąglania toohello najbliższej 100, firma Microsoft może udostępnić 1300 RU/s dla kolekcji tej aplikacji.

## <a id="RequestRateTooLarge"></a>Przekraczanie limitów zarezerwowaną przepływnością w usłudze Azure DB rozwiązania Cosmos
Odwołaj, że zużycie jednostka żądania jest oceniana jako szybkość na sekundę, jeśli budżetu hello jest pusta. Dla aplikacji, które przekraczają hello elastycznie jednostki częstość kontenera, żądania kolekcji toothat będzie ograniczony, dopóki hello spada poniżej poziomu hello zastrzeżone. W przypadku przepustnicy powitania serwera preemptively zakończy się Żądanie hello RequestRateTooLargeException (kod stanu HTTP 429) i zwracany hello nagłówka x-ms ponawiania — po ms wskazujący, że hello ilość czasu, w milisekundach hello użytkownik musi zaczekać na Interwał ponawiania hello żądanie.

    HTTP Status 429
    Status Line: RequestRateTooLarge
    x-ms-retry-after-ms :100

Jeśli używasz hello zestawu SDK klienta usługi .NET i LINQ zapytania, a następnie w większości przypadków hello nigdy nie masz toodeal z tym wyjątkiem, zgodnie z bieżącą wersję hello hello zestawu SDK klienta .NET niejawnie przechwytuje tej odpowiedzi względem hello określony serwer ponownych prób po nagłówka i Żądanie hello ponownych prób. Hello Następna ponowna próba powiedzie się, chyba że Twoje konto jest uzyskiwany jednocześnie przez wielu klientów.

Jeśli masz więcej niż jednego klienta zbiorczo operacyjnego powyżej liczby żądań hello, hello domyślne zachowanie ponawiania mogą być niewystarczające i powitania klienta zgłosi DocumentClientException z aplikacją toohello 429 kodu stanu. W przypadkach, takich jak ta można rozważyć Obsługa zachowanie ponownych prób i logikę w aplikacji Błąd procedury obsługi lub zwiększenie hello zarezerwowaną przepływnością hello kontenera.

## <a id="RequestRateTooLargeAPIforMongoDB"></a>Przekraczanie limitów zarezerwowaną przepływnością w interfejsie API, bazy danych mongodb
Aplikacje, które przekraczają hello elastycznie jednostek żądania dla kolekcji będzie ograniczony, dopóki hello spada poniżej poziomu hello zastrzeżone. W przypadku przepustnicy zaplecza hello preemptively zakończy się hello żądania z *16500* kod błędu: - *zbyt wiele żądań*. Domyślnie interfejsu API dla bazy danych MongoDB automatycznie ponowi próbę zapasowej razy too10 przed zwróceniem *zbyt wiele żądań* kod błędu. W przypadku otrzymania wiele *zbyt wiele żądań* kody błędów, można rozważyć albo dodanie zachowanie ponownych prób w aplikacji Błąd procedury obsługi lub [zwiększenie hello zarezerwowaną przepływnością dla kolekcji hello](set-throughput.md).

## <a name="next-steps"></a>Następne kroki
toolearn więcej informacji na temat zarezerwowaną przepływnością z bazami danych bazy danych Azure rozwiązania Cosmos, zapoznaj się z tymi zasobami:

* [Cennik platformy Azure DB rozwiązania Cosmos](https://azure.microsoft.com/pricing/details/cosmos-db/)
* [Partycjonowanie danych w usłudze Azure DB rozwiązania Cosmos](partition-data.md)

toolearn więcej informacji na temat bazy danych rozwiązania Cosmos platformy Azure, zobacz hello Azure DB rozwiązania Cosmos [dokumentacji](https://azure.microsoft.com/documentation/services/cosmos-db/). 

Zobacz tooget wprowadzenie testowanie Azure DB rozwiązania Cosmos, wydajności i skalowania [wydajności i skalowania testowania z bazy danych Azure rozwiązania Cosmos](performance-testing.md).

[1]: ./media/request-units/queryexplorer.png 
[2]: ./media/request-units/RUEstimatorUpload.png
[3]: ./media/request-units/RUEstimatorDocuments.png
[4]: ./media/request-units/RUEstimatorResults.png
[5]: ./media/request-units/RUCalculator2.png
[6]: ./media/request-units/api-for-mongodb-metrics.png
