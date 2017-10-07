---
title: "aaaWhat jest usługa Azure Search | Dokumentacja firmy Microsoft"
description: "Wyszukiwanie Azure jest usługą wyszukiwania pełni zarządzane chmury hostowanej. Dowiedz się więcej informacji, zobacz Omówienie tej funkcji."
services: search
manager: jhubbard
author: ashmaka
documentationcenter: 
ms.assetid: 50bed849-b716-4cc9-bbbc-b5b34e2c6153
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 06/26/2017
ms.author: ashmaka
ms.openlocfilehash: b38a7e93a7f0e0d5f8a3779858032271b3883778
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-search"></a>Co to jest usługa Azure Search?
Usługa Azure Search jest rozwiązaniem chmury wyszukiwanie jako usługa, która zapewnia deweloperom interfejsów API i narzędzia do dodawania obsługi wyszukiwania sformatowanego za pośrednictwem danych w aplikacjach sieci web, mobilnych i enterprise.

Funkcje są dostępne za pośrednictwem prostą [interfejsu API REST](/rest/api/searchservice/) lub [zestawu .NET SDK](search-howto-dotnet-sdk.md) który maskuje złożoność związanego z używaniem hello technologii wyszukiwania. W tooAPIs dodanie hello portalu Azure zapewnia administracji i obsługi tworzenie prototypów. Infrastruktura i dostępności są zarządzane przez firmę Microsoft.

<a name="feature-drilldown"></a>

## <a name="feature-summary"></a>Podsumowanie funkcji

| Kategoria | Funkcje |
|----------|----------|
|Wyszukiwanie pełnotekstowe i analiza tekstu | [**Wyszukiwanie pełnotekstowe** ](search-lucene-query-architecture.md) jest podstawowym przypadek użycia dla większości aplikacji na podstawie wyszukiwania. Zapytania można sformułować za pomocą obsługiwanych składni: <br/><br/>[**Prosta składnia zapytań**](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search), które oferuje operatorów logicznych, frazy operatorami wyszukiwania, Operatorzy sufiks, pierwszeństwo operatorów.<br/><br/>[**Składnia zapytań Lucene** ](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search) oferuje wszystkie termin pomocy technicznej, a także Wyszukiwanie rozmyte, wyszukiwanie w sąsiedztwie prostego zapytania zwiększania wyniku i regularnego wyrażenia.| 
| Integracja danych | Azure indeksy wyszukiwania zaakceptować danych z dowolnego źródła, pod warunkiem jest przesyłany w strukturze danych JSON. <br/><br/> Opcjonalnie, dla obsługiwanych źródeł danych na platformie Azure, możesz użyć [ **indeksatory** ](search-indexer-overview.md) przeszukiwania tooautomatically [bazy danych SQL Azure](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md), [bazy danych Azure rozwiązania Cosmos](search-howto-index-documentdb.md), lub [magazynu obiektów Blob Azure](search-howto-indexing-azure-blob-storage.md) toosync indeksu wyszukiwania elementu zawartości o magazynie danych podstawowych. Indeksatory obiektów Blob platformy Azure można wykonać *łamania dokumentu* dla [indeksowania głównych formatach](search-howto-indexing-azure-blob-storage.md), łącznie z dokumentów Microsoft Office, plików PDF i HTML. |
| Analiza wyszukiwania | [**Niestandardowe analizatorów leksykalne** ](https://docs.microsoft.com/rest/api/searchservice/custom-analyzers-in-azure-search) są dostępne dla zapytań wyszukiwania złożonych przy użyciu fonetycznych dopasowywania i wyrażenia regularne. |
| Obsługa języków | [**Analizatorów języka** ](https://docs.microsoft.com/rest/api/searchservice/language-support) od firmy Microsoft, a także Lucene obiektu języka naturalnego procesorów dostępnych w różnych językach w 56 toointelligently dojście specyficzny dla języka linguistics w tym czasowników, płci, nieregularne w liczbie mnogiej rzeczowniki (na przykład "myszy" a "myszy"), do łączenia programu word, dzielenie wyrazów (dla języków, bez spacji) i inne. |
| Wyszukiwanie Geo | Usługa Azure Search inteligentnie przetwarza filtrów i wyświetla lokalizacje geograficzne. Umożliwia użytkownikom tooexplore dane oparte na zbliżeniowe hello lokalizacji fizycznej tooa wyników wyszukiwania. [Obejrzyj ten film](https://channel9.msdn.com/Shows/Data-Exposed/Azure-Search-and-Geospatial-Data) lub [Przejrzyj ten przykład](https://github.com/Azure-Samples/search-dotnet-asp-net-mvc-jobs) toolearn więcej. |
| Funkcje środowiska użytkownika | [**Sugestie dotyczące wyszukiwania** ](https://docs.microsoft.com/rest/api/searchservice/suggesters) można włączyć Autouzupełnianie zapytań w pasku wyszukiwania. Rzeczywiste dokumenty w indeksie sugerowane użytkowników wprowadzania danych wejściowych z częściowa wyszukiwania. <br/><br/>[**Nawigacji aspektowej** ](https://docs.microsoft.com/azure/search/search-faceted-navigation) jest włączana za pomocą parametru pojedynczego zapytania. Usługa Azure Search zwraca strukturze nawigacji aspektowej służący jako hello kod związany z listy Kategorie, w celu samodzielnego filtrowania (na przykład toofilter elementy katalogu zakresu cen lub marki). <br/><br/> [**Filtry** ](https://docs.microsoft.com/rest/api/searchservice/odata-expression-syntax-for-azure-search) mogą być używane tooincorporate nawigacji aspektowej do interfejsu użytkownika aplikacji, zwiększyć formułowanie zapytania i filtrowanie w oparciu o kryteria określone przez użytkownika lub dewelopera. Tworzenie przy użyciu składni OData hello filtrów.<br/><br/> [**Wyróżnianie trafień** ](https://docs.microsoft.com/rest/api/searchservice/Search-Documents) stosuje tooa atting wizualnego dopasowanie słów kluczowych w wynikach wyszukiwania. Możesz wybrać pola, które zwraca zaznaczony fragmentów.<br/><br/>[**Sortowanie** ](https://docs.microsoft.com/rest/api/searchservice/Search-Documents) jest dostępna w przypadku wielu pól za pośrednictwem hello Indeksuj schemat i następnie przełączane na etapie zapytania z pojedynczy parametr.<br/><br/> [**Stronicowanie** ](search-pagination-page-layout.md) i ograniczania wyników wyszukiwania jest bezpośrednia z hello precyzyjne dopasowane formant, który udostępnia usługi Azure Search w wynikach wyszukiwania.  
| Trafność | [**Proste oceniania** ](/rest/api/searchservice/add-scoring-profiles-to-a-search-index) jest ważnym elementem usługi Azure Search. Oceniania profile są istotność toomodel używane jako funkcja wartości w hello dokumentów samodzielnie. Na przykład może być nowsza produktów lub obniżonej cenie wyżej w wynikach wyszukiwania hello tooappear produktów. Można również tworzyć profile oceniania przy użyciu tagów spersonalizowanych wyników na podstawie preferencji wyszukiwania klienta już śledzone i przechowywane w innej lokalizacji. |
| Monitorowanie i raportowanie | [**Wyszukaj analizy ruchu** ](search-traffic-analytics.md) są zbierane i przeanalizowane toounlock wgląd w dane dotyczące co użytkownicy są wprowadzania wartości do pola wyszukiwania hello. <br/><br/>Metryki dotyczące zapytań na sekundę, opóźnienia i ograniczania przechwycenie i zgłaszane na stronach portalu nie konieczności dodatkowej konfiguracji. Można też łatwo indeks monitor i dokument zlicza tak, aby w razie potrzeby można dostosować pojemności. Aby uzyskać więcej informacji, zobacz [obsługi administracyjnej](search-manage.md) |
| Narzędzia prototypowania i inspekcji | W portalu hello, można użyć hello [ **Kreatora importu danych** ](search-import-data-portal.md) indeksatory tooconfigure indeksu projektanta toostand indeksu i [ **Eksplorator wyszukiwania** ](search-explorer.md) tootest zapytań i Dostosuj oceniania profilów. Można również otworzyć żadnych tooview indeksu schematem. |
| Infrastruktura | Witaj **wysokiej dostępności platformy** zapewnia bardzo niezawodnej usługi wyszukiwanie. Podczas skalowania poprawnie, [usługi Azure Search udostępnia SLA 99,9%](https://azure.microsoft.com/support/legal/sla/search/v1_0/).<br/><br/> **W pełni zarządzany i skalowalne** jako rozwiązaniem na trasie usługi Azure Search wymaga absolutnie nie zarządzanie infrastrukturą. Usługi mogą być dopasowane tooyour potrzeb przez skalowanie w dwóch wymiarów toohandle dokumentu miejsca do magazynowania, wyższych obciążeń zapytania lub obu.

## <a name="how-it-works"></a>Jak to działa
### <a name="step-1-provision-service"></a>Krok 1: Świadczenia usługi
Można pokrętła usługi Azure Search w hello [portalu Azure](https://portal.azure.com/) lub za pośrednictwem hello [interfejsu API usługi Azure Resource Management](/rest/api/searchmanagement/). Można wybrać obu hello bezpłatnej usługi udostępniane innym subskrybentów lub [płatnej warstwy](https://azure.microsoft.com/pricing/details/search/) który rezerwuje zasoby używane tylko przez usługę. Warstw płatnych w dwóch wymiarów można skalować usługi: 

- Dodaj toogrow repliki, który ładuje kwerendy duże toohandle pojemności.   
- Dodaj magazyn toogrow partycje więcej dokumentów. 

Dzięki obsłudze przepływności magazynu i zapytania dokumentu oddzielnie, można kalibrować pozyskiwania na podstawie wymagań produkcji.

### <a name="step-2-create-index"></a>Krok 2: Tworzenie indeksu
Zanim można przekazać zawartości wyszukiwanie, należy najpierw zdefiniować indeksu usługi Azure Search. Indeks przypomina tabeli bazy danych, która przechowuje dane i może zaakceptować zapytania wyszukiwania. Zdefiniuj hello indeksu schematu toomap tooreflect hello struktury dokumentów hello mają toosearch, podobne toofields w bazie danych.

Schemat można tworzyć w hello Azure hello portalu lub programowo przy użyciu [zestawu .NET SDK](search-howto-dotnet-sdk.md) lub [interfejsu API REST](/rest/api/searchservice/).

### <a name="step-3-index-data"></a>Krok 3: Dane indeksu
Po zdefiniowaniu indeksu, wszystko jest gotowe tooupload zawartości. Można użyć modelu wypychania i ściągania.

model ściągania Hello pobiera dane z zewnętrznych źródeł danych. Jest on obsługiwany przez *indeksatory* usprawnić i zautomatyzować aspektów wprowadzanie danych, takich jak połączenie, odczytywanie i serializacja danych. [Indeksatory](/rest/api/searchservice/Indexer-operations) są dostępne dla bazy danych Azure rozwiązania Cosmos, baza danych SQL Azure, magazyn obiektów Blob Azure i SQL Server w maszynie Wirtualnej platformy Azure. Możesz skonfigurować indeksator dla na żądanie lub zaplanowane odświeżanie danych.

Witaj, model wypychania jest zapewniana za pomocą hello zestawu SDK lub interfejsów API REST, używany do wysyłania zaktualizowane dokumenty tooan indeksu. Można wypychać dane z niemal dowolnego zestawu danych za pomocą formatu JSON hello. Zobacz [Add, update lub delete dokumentów](/rest/api/searchservice/addupdate-or-delete-documents) lub [jak toouse hello zestawu .NET SDK)](search-howto-dotnet-sdk.md) wskazówki dotyczące ładowania danych.

### <a name="step-4-search"></a>Krok 4: wyszukiwania
Po wypełnieniu indeksu, możesz [wysyłania zapytań wyszukiwania](/rest/api/searchservice/Search-Documents) tooyour punktu końcowego usługi przy użyciu prostego protokołu HTTP żądania z interfejsu API REST lub hello zestawu .NET SDK.

## <a name="how-it-compares"></a>Sposób porównywania

Klienci często dotyczy jak [wyszukiwania pełnotekstowego w usłudze Azure Search](search-lucene-query-architecture.md) porównuje [wyszukiwanie pełnotekstowe](https://en.wikipedia.org/wiki/Full_text_search) w swoich produktach bazy danych. Nasze odpowiedzi jest, że funkcje językowe usługi Azure Search są bardziej rozbudowane i bardziej elastyczne i Obsługa zapytań Lucene, analizatorów języka z Lucene i firmy Microsoft, niestandardowe analizatorów dla fonetyczne lub innych danych wejściowych specjalistyczne i hello możliwości toomerge danych z wiele źródeł w hello w indeksie. 

Inny punkt modulacją jest, że rozwiązanie wyszukiwania adresów przeszukiwanie całego hello. Na przykład można niestandardowych oceniania wyników, nawigacji aspektowej samodzielnego filtrowania, wyróżnianie trafień i sugestie dotyczące zapytań typeahead. 

Narzędzia dla monitorowanie i zrozumienie działania zapytania można również uwzględnić decyzji rozwiązania wyszukiwania. Na przykład usługi Azure Search obsługuje [analizy ruchu wyszukiwania](search-traffic-analytics.md) dla metryki na szybkość przeglądowego, najczęstsze wyszukiwania, wyszukuje bez kliknięcia i tak dalej. W produktach, gdzie wyszukiwania jest dodatek, jest mało prawdopodobne toofind te funkcje.

Użycie zasobów jest kolejnym zagadnieniem. Wyszukiwanie w języku naturalnym jest często znacznym w praktyce. Niektóre z naszym klientom odciążony tooAzure operacji wyszukiwania wyszukiwania jako zasoby maszyny toopreserve w sposób przetwarzania transakcji. Przez jego oddzielenie wyszukiwania można łatwo dostosować skali toomatch zapytania woluminu.

Decydujesz się toogo z dedykowanym wyszukiwania, dalej zdecydować, czy po między usługą w chmurze lub serwera lokalnego. Usługi w chmurze jest właściwie hello, jeśli chcesz [gotowe rozwiązanie przy minimalnym nakładzie kosztów i konserwacji i skali regulowany](#cloud-service-advantage).

W ramach modelu chmury hello wielu dostawców oferują funkcje można porównywać pod względem linii bazowej, wyszukiwanie pełnotekstowe, geograficznie wyszukiwania i toohandle możliwości hello niejednoznaczności w danych wejściowych wyszukiwanie określonego poziomu. Zwykle ma [specjalnych funkcji](#feature-drilldown), lub łatwość hello i uproszczenia ogólnego interfejsów API, narzędzi i zarządzania, które określa optymalnie hello.

Wśród dostawców w chmurze usługi Azure Search jest najwyższego poziomu dla obciążeń wyszukiwania pełnotekstowego w zawartości magazynów i baz danych na platformie Azure, w przypadku aplikacji, które opierają się głównie na wyszukiwania dla pobierania informacji i nawigację po zawartości. Sile klucza obejmują:

+ Integracja danych Azure (przeszukiwarek) w warstwie indeksowania hello
+ Portal Azure centralnego zarządzania
+ Azure skalowania, niezawodności i dostępności światowej klasy
+ Niestandardowe i językowej analizy ze analizatorów wyszukiwania pełnotekstowego stałe w 56 językach
+ [Podstawowe funkcje typowych aplikacji skoncentrowane na toosearch](#feature-drilldown): oceniania, tworzenie aspektów, sugestii, synonimy, geograficznie wyszukiwania i inne.

> [!Note]
> źródeł danych Wyczyść, innych niż Azure toobe są w pełni obsługiwane, ale zależą od metodologii wypychania bardziej intensywnie dla kodu, a nie indeksatorów. Za pomocą naszych interfejsów API, można przekazać indeksu usługi Azure Search tooan kolekcji dokumentów JSON.

Między klientami tych stanie tooleverage hello szeroką gamą funkcji w usłudze Azure Search obejmują katalogi online, programy z biznesowych i odnajdywania dokumenty i aplikacje.

## <a name="rest-api--net-sdk"></a>Interfejs API REST | .net SDK

Natomiast wielu zadań, które może zostać przeprowadzone w portalu hello, usługi Azure Search jest przeznaczony dla deweloperów, którzy chcą toointegrate funkcji wyszukiwania do istniejących aplikacji. Witaj następujących interfejsów programowania są dostępne.

|Platforma |Opis |
|-----|------------|
|[REST](/rest/api/searchservice/) | Polecenia HTTP obsługiwane przez wszystkie platformy programowania i język, w tym Xamarin, Java i JavaScript|
|[Zestaw SDK platformy .NET](search-howto-dotnet-sdk.md) | .NET otoki dla interfejsu API REST hello oferuje efektywne programowania w języku C# i innych języków kodu zarządzanego przeznaczonych dla hello .NET Framework |

## <a name="free-trial"></a>Bezpłatna wersja próbna
Subskrybenci platformy Azure można [alokowanie usługi w warstwie bezpłatna hello](search-create-service-portal.md).

Jeśli nie masz subskrybenta, możesz [otworzyć bezpłatne konto platformy Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F). Otrzymasz kredyt do wypróbowania płatnych usług Azure. Po wyczerpaniu, można zachować konta hello i używać [bezpłatnych usług platformy Azure](https://azure.microsoft.com/free/). Karta kredytowa nigdy nie jest obciążona, chyba że jawnie zmienić ustawienia i poproś toobe obciążona.

Można też [aktywować korzyści dla subskrybentów MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F): subskrypcji Your MSDN otrzymasz kredyt, co miesiąc, używanego programu płatnych usług Azure. 

## <a name="how-tooget-started"></a>Sposób uruchamiania tooget

1. Tworzenie usługi w hello [warstwę bezpłatna](search-create-service-portal.md).

2. Przejrzyj kroki co najmniej jednego z następujących samouczków hello. 

  + [Jak toouse hello zestawu .NET SDK](search-howto-dotnet-sdk.md) pokazuje hello główne kroki w kodzie zarządzanym.  
  + [Wprowadzenie do interfejsu API REST hello](https://github.com/Azure-Samples/search-rest-api-getting-started) pokazuje hello same czynności przy użyciu hello interfejsu API REST.  
  + [Utworzyć pierwszy indeks w portalu hello](search-get-started-portal.md) przedstawiono wbudowane funkcje indeksowanie i prototypu hello portalu.   

Aparaty wyszukiwania są typowe sterowniki hello pobierania informacji w aplikacjach mobilnych, hello sieci Web i w magazynach danych firmowych. Usługa Azure Search udostępnia narzędzia do tworzenia toothose podobne środowisko wyszukiwania w dużych witryn sieci web.

Dowiedz się, w tym 9-minutowy film wideo z Menedżera programów Liam Cavanagh, integrowanie z wyszukiwarki korzyści aplikacji. Krótkie pokazy opisano najważniejsze funkcje usługi Azure Search i jak wygląda Typowy przepływ pracy. 

>[!VIDEO https://channel9.msdn.com/Events/Connect/2016/138/player]
 
+ 0 – 3 min omawia kluczowe funkcje i przypadki użycia.
+ 3 4 minut obejmuje Inicjowanie obsługi usługi. 
+ 4 – 6 min obejmuje toocreate używać Kreatora importu danych indeks, używając hello nieruchomości wbudowanej w zestawie danych.
+ 6 9 minut obejmuje Eksplorator wyszukiwania i różne zapytania.


