---
title: "Zagadnienia wydajności i optymalizacji wyszukiwania aaaAzure | Dokumentacja firmy Microsoft"
description: "Dostrajanie wydajności usługi Azure Search i skonfigurować optymalnej skali"
services: search
documentationcenter: 
author: LiamCavanagh
manager: pablocas
editor: 
ms.assetid: 4d3cd864-29d2-4921-be0d-a3f1a819de46
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 05/01/2017
ms.author: liamca
ms.openlocfilehash: 725149ba32773ab6b4c9d4b441424aba78db7c42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-search-performance-and-optimization-considerations"></a>Azure zagadnienia wydajności i optymalizacji wyszukiwania
Wyszukiwanie dużą jest klucza toosuccess dla wielu urządzeń przenośnych i aplikacji sieci web. Z nieruchomości tooused samochodu rynków tooonline katalogi, szybkie wyszukiwanie i odpowiednie wyniki będzie miało wpływ na wrażenia hello. Ten dokument jest zamierzone toohelp odnajdywanie najlepsze rozwiązania dotyczące sposobu hello tooget maksymalne wykorzystanie możliwości usługi Azure Search, szczególnie w przypadku zaawansowanych scenariuszy z zaawansowane opcje wymagań dotyczących skalowalności, obsługi wielu języków lub niestandardowych klasyfikacji.  Ponadto ten dokument przedstawia ustawienia wewnętrzne i obejmuje metodami działał efektywnie w aplikacjach rzeczywistych klientów.

## <a name="performance-and-scale-tuning-for-search-services"></a>Wydajność i skalę dostrajania dla usługi wyszukiwania
Możemy wszystkie aparaty używane toosearch takich jak Bing i Google hello wysokiej wydajności i oferują.  W związku z tym gdy klienci użyć wyszukiwania sieci web lub aplikacji mobilnej, będzie oczekiwać podobne charakterystyki wydajności.  Podczas optymalizacji wydajności wyszukiwania, jednym z najlepszych metod hello jest toofocus na opóźnienia, czyli hello czas kwerendy toocomplete i zwrot wyników.  Podczas optymalizacji dla opóźnienia wyszukiwania ważne jest, aby:

1. Wybierz docelowym czasem oczekiwania (lub maksymalną ilość czasu) o tym, że żądania wyszukiwania typowych powinno mieć toocomplete.
2. Tworzenie i testowanie rzeczywiste obciążenie wysyłane do usługi wyszukiwania z toomeasure realistyczne zestawu danych z tych wskaźników opóźnienia.
3. Rozpoczynać się od małej liczbie zapytania na sekundę (QPS) i kontynuować tooincrease hello liczbę wykonywanych w hello testu do momentu hello zapytań, czas oczekiwania spadnie poniżej hello zdefiniowania docelowym czasem oczekiwania.  Jest to ważne testu porównawczego toohelp, której planujesz skali wraz z rozwojem aplikacji w sposób użycia.
4. W miarę możliwości ponownego użycia połączenia HTTP.  Jeśli używasz hello zestawu .NET SDK usługi Azure Search, oznacza to, należy używać ponownie wystąpienia lub [SearchIndexClient](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.searchindexclient) wystąpienia, a jeśli używasz hello interfejsu API REST, należy używać ponownie pojedynczego HttpClient.

Podczas tworzenia tych testów obciążenia, brak niektórych właściwości tookeep usługi Azure Search pamiętać:

1. Istnieje możliwość toopush wyszukiwania tak wiele zapytań w tym samym czasie, że będzie przeciążony hello zasoby dostępne w usłudze Azure Search.  W takim przypadku zobaczysz kody odpowiedzi HTTP 503.  Z tego powodu jest najlepszym toostart z różnych zakresów wyszukiwania żądań toosee hello różnice w stawki opóźnienia podczas dodawania więcej żądań wyszukiwania.
2. Przekazywanie zawartości tooAzure, który wyszukiwania będzie miało wpływ na hello ogólną wydajność i opóźnienie hello usługi Azure Search.  Jeśli toosend danych podczas przeprowadzania wyszukiwania użytkowników, jest ważne tootake to obciążenie do konta w testach.
3. Nie wszystkie zapytania wyszukiwania będzie wykonywać na powitania same poziomy wydajności.  Na przykład sugestii wyszukiwania lub wyszukiwania dokumentu zazwyczaj będzie wykonywać szybciej niż zapytanie z znaczących aspektów i filtry.  Jest najlepszym hello tootake różne zapytania oczekiwanych toosee do konta podczas kompilowania testów.  
4. Zmiany żądania wyszukiwania jest ważne, ponieważ Jeśli stale wykonane hello wyszukiwania same żądania, buforowanie danych wydajności toomake start wygląd nie może być bardziej różnych zapytania ustawiana.

> [!NOTE]
> [Visual Studio obciążenia testowania](https://www.visualstudio.com/docs/test/performance-testing/run-performance-tests-app-before-release) jest naprawdę dobrze tooperform Twojego testu porównawczego testów, ponieważ umożliwia on żądań tooexecute HTTP potrzebnych do wykonywania zapytań dotyczących usługi Azure Search i umożliwia paralelizacja żądań.
> 
> 

## <a name="scaling-azure-search-for-high-query-rates-and-throttled-requests"></a>Skalowanie usługi Azure Search dla zapytania wysokiej szybkości i ograniczenie żądań
Gdy otrzymują zbyt wiele żądań z ograniczeniem przepustowości lub przekracza stawki opóźnienia sieci docelowej z zapytania zwiększenie obciążenia, można sprawdzić toodecrease opóźnienia szybkości w jeden z dwóch sposobów:

1. **Zwiększ replik:** repliki przypomina kopię stosowanie usługi Azure Search tooload równoważenie żądań przed hello wiele kopii danych.  Wszystkie Równoważenie obciążenia i replikacji danych między replikami jest zarządzane przez usługę Azure Search i hello liczby replikami przydzielone dla usługi w dowolnym momencie można zmienić.  Możesz przydzielić too12 replik w standardową usługę wyszukiwania i 3 replik w usłudze wyszukiwania podstawowego. Repliki mogą być dostosowane z hello [portalu Azure](search-create-service-portal.md) lub [PowerShell](search-manage-powershell.md).
2. **Zwiększ wyszukiwania warstwy:** usługa Azure Search jest dostarczany [liczba warstw](https://azure.microsoft.com/pricing/details/search/) i każdy z tych warstw oferuje różne poziomy wydajności.  W niektórych przypadkach może być tak wiele zapytań warstwa hello sieci nie może dostarczyć szybkości wystarczająco małe opóźnienia, nawet wtedy, gdy limit maksymalnego wykorzystania replik.  W takim przypadku można tooconsider, wykorzystując jedną z hello wyższych warstw wyszukiwania hello Azure Search S3 warstwy, która jest odpowiednia w scenariuszach z dużą liczbą dokumentów i bardzo dużej zapytania obciążeń.

## <a name="scaling-azure-search-for-slow-individual-queries"></a>Skalowanie usługi Azure Search dla poszczególnych zapytań powolne
Kolejny powód, dlaczego stawki opóźnienia może działać powoli pochodzi z pojedynczego zapytania biorąc toocomplete zbyt długa.  W takim przypadku Dodawanie repliki nie spowoduje zwiększenie szybkości opóźnienia.  Dla tego przypadku dostępne są dwie opcje:

1. **Zwiększ partycje** partycja to mechanizm służący do dzielenia danych na dodatkowe zasoby.  Z tego powodu po dodaniu drugiej partycji, dane pobiera podzielić na dwa.  Trzeci partycji dzieli indeksu na trzech itp.  Ma to również hello efekt, że w niektórych przypadkach powolne zapytania wykona szybciej powodu paralelizacja toohello obliczeń.  Istnieje kilka przykładów którym zaobserwowano tego paralelizacja bardzo dobrze współpracować zapytań, które mają niski wybieralność zapytania.  Składa się z zapytań, które odpowiada wiele dokumentów, lub gdy tworzenie aspektów musi tooprovide liczniki przez dużą liczbę dokumentów.  Ponieważ istnieje wiele obliczeń potrzebne dokładność hello tooscore dokumentów hello lub toocount hello liczby dokumentów, dodając dodatkowe partycje mogą pomóc tooprovide dodatkowe obliczeń.  
   
   Może istnieć maksymalnie 12 partycji w standardową usługę wyszukiwania i 1 partycji w usłudze wyszukiwania podstawowego hello.  Partycje mogą być dostosowane z hello [portalu Azure](search-create-service-portal.md) lub [PowerShell](search-manage-powershell.md).
2. **Limit wysokiej pola Kardynalność:** pola dużej kardynalności składa się z aspektów lub Filtrowanie pola, które ma znaczący liczbę unikatowych wartości i w związku z tym przejmuje dużej ilości zasobów toocompute wyników.   Na przykład ustawienie pola Identyfikator produktu lub opisu jako aspektów/filtrowanie spowodowałoby dla dużej kardynalności ponieważ większość hello wartości z toodocument dokumentu są unikatowe. Gdy jest to możliwe, Ogranicz liczbę hello dużej kardynalności pól.
3. **Zwiększ wyszukiwania warstwy:** przesunięcie w górę tooa wyższej warstwy usługi Azure Search może być inny sposób tooimprove wydajność kwerend powolne.  Każdy wyższego poziomu także szybsze Procesora i większa ilość pamięci, które mogą mieć pozytywny wpływ na wydajność kwerend.

## <a name="scaling-for-availability"></a>Skalowanie dla dostępności
Replik nie tylko zmniejszenia opóźnienia kwerendy, ale może również umożliwiać wysokiej dostępności.  Z pojedynczą replikę należy oczekiwać okresowe przestoje powodu tooserver jest uruchamiany ponownie po aktualizacji oprogramowania lub inne zdarzenia konserwacji, które będą przeprowadzane.  W związku z tym jest ważne tooconsider Jeśli aplikacja wymaga wysokiej dostępności wyszukiwania (queries) oraz zapisów (indeksowania zdarzeń).  Usługa wyszukiwanie Azure oferuje opcje SLA na wszystkich hello oferty płatnej wyszukiwania z hello następujące atrybuty:

* 2 replik wysokiej dostępności obciążeń tylko do odczytu (queries)
* 3 lub więcej replik wysokiej dostępności obciążeń odczytu i zapisu (zapytań i indeksowanie)

Więcej szczegółów na ten, odwiedź stronę hello [umową dotyczącą poziomu usług wyszukiwanie Azure](https://azure.microsoft.com/support/legal/sla/search/v1_0/).

Ponieważ repliki są kopie danych, mających wiele replik umożliwia ponowne uruchomienie komputera toodo usługi Azure Search i konserwacji względem jednej replice w czasie, podczas gdy zapytanie wykonywane toobe toocontinue hello innych replik.  Z tego powodu należy również tooconsider, jak to przestoju może mieć wpływ na powitania zapytań, które jest wykonywane co mniej kopii danych hello toobe.

## <a name="scaling-geo-distributed-workloads-and-provide-geo-redundancy"></a>Skalowanie rozproszona geograficznie obciążeń i zapewnić nadmiarowość geograficzna
W przypadku obciążeń rozproszona geograficznie zostanie ustalone, że użytkownicy znajdujący się daleko od hello centrum danych, gdzie jest hostowana usługi Azure Search większe opóźnienia.  Z tego powodu często jest ważne toohave wyszukiwania wielu usług w regionach, znajdujących się w bliżej zbliżeniowe toothese użytkowników.  Usługa Azure Search nie ma obecnie zautomatyzowaną metodę replikację geograficzną indeksów usługi Azure Search w regionach, ale istnieją pewne techniki, które mogą być używane, które można wprowadzić ten proces tooimplement proste i zarządzać nimi. Te są opisane w hello kolejnych sekcjach kilku.

Hello celem rozproszona geograficznie zbiór usług wyszukiwania jest toohave dwa lub więcej indeksów, dostępne w dwóch lub więcej regionów, w którym użytkownik będzie kierowany usługa Azure Search toohello, która zapewnia hello można uzyskać najmniejsze opóźnienia, jak pokazano w poniższym przykładzie:

   ![Między — karta usług według regionu][1]

### <a name="keeping-data-in-sync-across-multiple-azure-search-services"></a>Synchronizacja danych w wielu usługach Azure Search
Dostępne są dwie opcje przechowywania wyszukiwania rozproszonego usługi synchronizacji składające się z przy użyciu hello [indeksatora wyszukiwania Azure](search-indexer-overview.md) lub hello Push interfejsu API (nazywana także tooas hello [interfejsu API REST wyszukiwania Azure](https://docs.microsoft.com/rest/api/searchservice/)).  

### <a name="azure-search-indexers"></a>Indeksatory w usłudze Azure Search
Jeśli używasz hello Azure indeksatora wyszukiwania są już importowanie zmiany danych z centralnego magazynu danych, takich jak bazy danych SQL Azure lub bazy danych Azure rozwiązania Cosmos. Podczas tworzenia nowego wyszukiwania usługi, należy po prostu również tworzyć nowe indeksatora wyszukiwania Azure dla tej usługi tego toothis punktów tego samego magazynu danych. W ten sposób, przy każdym nowych zmian wejścia hello magazynu danych, zostaną indeksowane według hello różnych indeksatorów.  

Oto przykład jak będzie wyglądać danej architekturze.

   ![Pojedyncze źródło danych z kombinacji usługi i rozproszone indeksatora][2]

### <a name="push-api"></a>Wypychanie interfejsu API
Jeśli używasz hello interfejsu API usługi Azure Search Push zbyt[zaktualizować zawartość w indeksie usługi Azure Search](https://docs.microsoft.com/rest/api/searchservice/update-index), można zachować na różne usługi wyszukiwania w synchronizacji przez wypychanie usługi wyszukiwania tooall zmiany, gdy wymagana jest aktualizacja.  W ten sposób jest ważne toomake się, że toohandle przypadkach, gdy usługa wyszukiwania tooone aktualizacji nie powiedzie się i pomyślnie co najmniej jednej aktualizacji.

## <a name="leveraging-azure-traffic-manager"></a>Korzystanie z usług Azure Traffic Manager
[Menedżer ruchu Azure](../traffic-manager/traffic-manager-overview.md) pozwala tooroute żądań toomultiple znajdujący się geograficznie witryn, które następnie bazują na wielu usług wyszukiwanie Azure.  Jedną z zalet hello Menedżera ruchu jest może on sondowania tooensure usługi Azure Search, że jest dostępny i kierować usługi wyszukiwania tooalternate użytkowników w przypadku hello przestoju.  Ponadto jeśli są routingu żądań wyszukiwania do witryn sieci Web platformy Azure, Azure Traffic Manager można tooload saldo przypadku witryny sieci Web hello się, ale nie usługi Azure Search.  Oto przykład jakie architektury hello, który korzysta z Menedżera ruchu.

   ![Między — karta usług według regionu, centralnej menedżera ruchu][3]

## <a name="monitoring-performance"></a>Monitorowanie wydajności
Usługa Azure Search udostępnia hello możliwości tooanalyze i monitorować hello wydajność usługi za pośrednictwem [analizy ruchu wyszukiwania (STA)](search-traffic-analytics.md). Za pomocą STA można opcjonalnie dziennika operacji wyszukiwania poszczególnych hello, a także konta magazynu Azure tooan zagregowane metryk, które następnie mogą być przetwarzane do analizy lub wizualizowane w usłudze Power BI.  Metryki STA można przeglądać statystyki, takie jak średnia liczba zapytań lub czas odpowiedzi na zapytania.  Ponadto rejestrowanie operacji hello pozwala toodrill do szczegółów operacji wyszukiwania określonych.

STA jest przydatnym narzędziem toounderstand opóźnienia stawki z punktu widzenia tej usługi Azure Search.  Ponieważ metryki wydajności kwerendy hello rejestrowane są oparte na powitania czasu zapytania ma toobe całkowicie przetworzone w usłudze Azure Search (od czasu hello jest żądany toowhen zostaną wysłane), są możliwe toouse toodetermine, to w przypadku problemów z opóźnieniem z hello usługi Azure Search po stronie lub poza hello usługi, na przykład opóźnienia sieci.  

## <a name="next-steps"></a>Następne kroki
toolearn więcej informacji na temat hello ceny warstw i limity usług dla każdego z nich, zobacz [usługi limity w usłudze Azure Search](search-limits-quotas-capacity.md).

Odwiedź stronę [planowania pojemności](search-capacity-planning.md) toolearn więcej informacji na temat kombinacji partycji i replik.

Do rozwijania więcej szczegółów na wydajność i toosee niektórych pokazy jak tooimplement hello optymalizacje omówione w tym artykule Obejrzyj powitania po wideo:

> [!VIDEO https://channel9.msdn.com/Events/Microsoft-Azure/AzureCon-2015/ACON319/player]
> 
> 

<!--Image references-->
[1]: ./media/search-performance-optimization/geo-redundancy.png
[2]: ./media/search-performance-optimization/scale-indexers.png
[3]: ./media/search-performance-optimization/geo-search-traffic-mgr.png
