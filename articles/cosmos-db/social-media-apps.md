---
title: "Wzorzec projektowy w usłudze Azure DB rozwiązania Cosmos: aplikacje mediów społecznościowych | Dokumentacja firmy Microsoft"
description: "Informacje na temat wzorzec projektowania dla sieci społecznościowych dzięki wykorzystaniu hello elastyczność magazynu bazy danych Azure rozwiązania Cosmos i innymi usługami Azure."
keywords: "Aplikacje mediów społecznościowych"
services: cosmos-db
author: ealsur
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: 2dbf83a7-512a-4993-bf1b-ea7d72e095d9
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/29/2017
ms.author: mimig
ms.openlocfilehash: 47a22f2c5762d62b176921c8052e7bd75d8cf6ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="going-social-with-azure-cosmos-db"></a>Przechodzenie społecznościowych z bazy danych Azure rozwiązania Cosmos
Życia społeczeństwa ogromną skalę połączenia oznacza, że w pewnym momencie życia staje się częścią **sieci społecznościowych**. Używamy tookeep sieci społecznościowych ze znajomych, współpracowników, rodziny i czasami tooshare naszych męczennicy osobom z typowych zainteresowań.

Jako inżynierów lub deweloperów firma Microsoft może mieć zastanawiasz się, jak te sieci magazynu i łączenie danych lub może mieć nawet zostały zlecił toocreate lub architekta nowej sieci społecznościowych dla określonych niszowych rynku yourselves. Gdy to kwestia big hello: jak te dane są przechowywane?

Załóżmy, że tworzenia nowych i obiektowi błyszczący sieci społecznościowych, gdzie naszych użytkowników umożliwia opublikowanie artykułów z powiązanych nośniku, na przykład, obrazów, klipów wideo lub nawet utworów muzycznych. Użytkownicy mogą dodać komentarz dotyczący ogłoszeń i zapewniają punktów klasyfikacji. Nie będzie można źródło wpisów, które użytkownicy zobaczą i stanie toointeract z na strony docelowej hello głównym witryny sieci Web. To nie dźwiękowej naprawdę złożonych (na początku), ale dla zapewnienia hello prostotę, umożliwia zatrzymać istnieje (Firma Microsoft może delve do źródła danych użytkownika niestandardowego wpływ relacji, ale jego rozmiar przekracza hello celem tego artykułu).

Tak jak możemy zapisać tej i gdzie?

Wiele osób może zawierać obsługi baz danych SQL lub co najmniej zawiera pojęcie [modelowania danych relacyjnych](https://en.wikipedia.org/wiki/Relational_model) i może się wydawać toostart rysowania podobny do następującego:

![Diagram pokazujący względną modelu relacyjnych](./media/social-media-apps/social-media-apps-sql.png) 

Struktura danych doskonale znormalizowane i łatwa... że nie skalowania. 

Nie pobieraj mnie niewłaściwy I pracował z bazy danych SQL wszystkie moje życia, są one bardzo, ale jak każdej platformy wzorzec, praktyki i oprogramowania nie jest idealny dla każdego scenariusza.

Dlaczego SQL hello najlepszym rozwiązaniem w tym scenariuszu? Przyjrzyjmy się struktury hello jednego wpisu, jeśli miała tooshow, który blogu w witrynie sieci Web lub aplikacji, czy mam toodo zapytania... Tabela 8 sprzężenia (!) tooshow tylko jeden pojedynczy post, teraz, obraz strumień wpisów dynamicznie obciążenia i są wyświetlane na ekranie powitania i można napotkać, gdzie użyjemy.

Można oczywiście używamy agencji wystąpienie serwera SQL o wystarczającej ilości toosolve power tysięcy zapytań z tych wiele tooserve sprzężenia zawartość, ale naprawdę, dlaczego czy możemy gdy rozwiązanie prostsze istnieje?

## <a name="hello-nosql-road"></a>Witaj NoSQL drogowej
Ten artykuł przeprowadzi Cię do modelowania platformy społecznościowych danych z bazy danych NoSQL platformy Azure [bazy danych Azure rozwiązania Cosmos](https://azure.microsoft.com/services/cosmos-db/) w sposób ekonomiczny, podczas korzystania z innych funkcji bazy danych rozwiązania Cosmos platformy Azure, takich jak hello [Gremlin interfejsu API programu Graph ](../cosmos-db/graph-introduction.md). Przy użyciu [NoSQL](https://en.wikipedia.org/wiki/NoSQL) podejście, przechowywanie danych w formacie JSON i stosowanie [denormalization](https://en.wikipedia.org/wiki/Denormalization), naszych wcześniej skomplikowane post może zostać zamieniony na pojedynczy [dokumentu](https://en.wikipedia.org/wiki/Document-oriented_database):


    {
        "id":"ew12-res2-234e-544f",
        "title":"post title",
        "date":"2016-01-01",
        "body":"this is an awesome post stored on NoSQL",
        "createdBy":User,
        "images":["http://myfirstimage.png","http://mysecondimage.png"],
        "videos":[
            {"url":"http://myfirstvideo.mp4", "title":"hello first video"},
            {"url":"http://mysecondvideo.mp4", "title":"hello second video"}
        ],
        "audios":[
            {"url":"http://myfirstaudio.mp3", "title":"hello first audio"},
            {"url":"http://mysecondaudio.mp3", "title":"hello second audio"}
        ]
    }

I można uzyskać z pojedynczego zapytania i nie sprzężenia. Jest to bardziej proste i bezpośrednie i budget-wise, wymaga mniej zasobów tooachieve lepszy wynik.

Azure DB rozwiązania Cosmos upewnia się, że wszystkie właściwości hello są indeksowane z jego automatycznego indeksowania może nawet to [dostosowane](indexing-policies.md). Witaj bez schematu podejście pozwala nam przechowywania dokumentów z różnymi i dynamicznych struktur, może być jutro chcemy toohave wpisów, które obsłuży listę kategorii ani hashtagów skojarzonych z nimi rozwiązania Cosmos DB hello nowych dokumentów z hello dodane atrybuty z bez dodatkowych Praca wymagana przez nas.

Komentarze na ogłoszenie (post) może być traktowana jako tylko innych wpisów z właściwością nadrzędnego (upraszcza naszych mapowania obiektu). 

    {
        "id":"1234-asd3-54ts-199a",
        "title":"Awesome post!",
        "date":"2016-01-02",
        "createdBy":User2,
        "parent":"ew12-res2-234e-544f"
    }

    {
        "id":"asd2-fee4-23gc-jh67",
        "title":"Ditto!",
        "date":"2016-01-03",
        "createdBy":User3,
        "parent":"ew12-res2-234e-544f"
    }

I wszystkie interakcje społecznościowych mogą być przechowywane na oddzielnych obiektów jako liczników:

    {
        "id":"dfe3-thf5-232s-dse4",
        "post":"ew12-res2-234e-544f",
        "comments":2,
        "likes":10,
        "points":200
    }

Tworzenie źródła danych jest wystarczy tworzenie dokumentów zawierających listy identyfikatorów post z kolejnością danego znaczenie:

    [
        {"relevance":9, "post":"ew12-res2-234e-544f"},
        {"relevance":8, "post":"fer7-mnb6-fgh9-2344"},
        {"relevance":7, "post":"w34r-qeg6-ref6-8565"}
    ]

Firma Microsoft może mieć "najnowszej" strumienia z wpisów uporządkowanych według daty utworzenia, "najnowszych" strumienia z tymi ogłoszenia o więcej podobne w hello ostatnich 24 godzinach, może nawet wprowadzania niestandardowych strumieni dla każdego użytkownika opartych na logice, takich jak adherentami i udziałów i nadal będzie listę  wpisów. Jest kwestią jak toobuild te listy, ale wydajność odczytu hello pozostaje swobodnego. Po możemy uzyskać jeden z tych list, możemy wystawić tooCosmos pojedynczego zapytania bazy danych przy użyciu hello [w operatorze](documentdb-sql-query.md#WhereClause) stron tooobtain stanowisk naraz.

mogą być zbudowane Hello strumieni źródła przy użyciu [usługi aplikacji Azure](https://azure.microsoft.com/services/app-service/) procesów w tle: [Webjob](../app-service-web/web-sites-create-web-jobs.md). Po utworzeniu wpisu proces przetwarzania w tle może zostać zainicjowany przy użyciu [usługi Azure Storage](https://azure.microsoft.com/services/storage/) [kolejek](../storage/queues/storage-dotnet-how-to-use-queues.md) i zadania Webjob wyzwalane za pomocą hello [zestaw SDK zadań Webjob Azure](../app-service-web/websites-dotnet-webjobs-sdk.md), wdrożenia powitania po propagacji wewnątrz strumieni oparte na własnej logiki niestandardowej. 

Punkty i podobne za pośrednictwem ogłoszenie (post) mogą być przetwarzane w sposób odroczonego przy użyciu tego samego toocreate technika ostatecznie spójne środowisko.

Adherentami są trudniejszy. Rozwiązania cosmos bazy danych ma dokumentu maksymalny limit rozmiaru i odczytu/zapisu dużych dokumentów może wpłynąć na powitania skalowalność aplikacji. Dlatego sądzisz o zapisywaniu adherentami jako dokument z tej struktury:

    {
        "id":"234d-sd23-rrf2-552d",
        "followersOf": "dse4-qwe2-ert4-aad2",
        "followers":[
            "ewr5-232d-tyrg-iuo2",
            "qejh-2345-sdf1-ytg5",
            //...
            "uie0-4tyg-3456-rwjh"
        ]
    }

To może działać dla użytkownika z kilku tysięcy adherentami, ale gdy niektóre renomy sprzężenia naszych rangi, tej metody spowoduje rozmiar dokumentu dużych tooa i może cap ostatecznie trafień hello rozmiar dokumentu.

toosolve, możemy użyć mieszanych podejście. Jako część dokumentu statystyki użytkownika hello firma Microsoft może przechowywać hello liczba adherentami:

    {
        "id":"234d-sd23-rrf2-552d",
        "user": "dse4-qwe2-ert4-aad2",
        "followers":55230,
        "totalPosts":452,
        "totalPoints":11342
    }

I hello rzeczywiste wykres adherentami mogą być przechowywane przy użyciu bazy danych Azure rozwiązania Cosmos [interfejsu API programu Graph Gremlin](../cosmos-db/graph-introduction.md), toocreate [wierzchołków](http://mathworld.wolfram.com/GraphVertex.html) dla każdego użytkownika i [krawędzi](http://mathworld.wolfram.com/GraphEdge.html) który Obsługa hello " Relacje A-następujące B". Hello interfejsu API programu Graph umożliwia można nie tylko uzyskać hello adherentami określonego użytkownika, ale tworzenie bardziej złożonych zapytań tooeven Sugeruj osób wspólnych. Jeśli dodamy hello wykres toohello kategorie zawartości tej osoby, takich jak lub kredyty, możemy rozpocząć tkania procesów, które obejmują inteligentne funkcję odnajdowania zawartości, sugerowanie zawartości tym te, które firma Microsoft wykonaj, takich jak lub znajdowania osoby, z którym firma Microsoft może być znacznie wspólnych.

Hello statystyki użytkownika dokumentu można nadal kart toocreate używanych w hello interfejsu użytkownika lub podglądy szybkie profilu.

## <a name="hello-ladder-pattern-and-data-duplication"></a>Witaj duplikacji danych i wzorzec "Drabina"
Jak można zauważyć w dokumencie JSON hello, który odwołuje się do wpisu, istnieje wiele wystąpień użytkownika. I można będzie mieć odgadnąć prawo, to oznacza, że informacje hello reprezentuje podana przez użytkownika, to denormalization może być obecny w więcej niż jednym miejscu.

W kolejności tooallow szybsze zapytań możemy pociągnąć za sobą deduplikacji danych. Hello problem z efektem ubocznym jest, że jeśli przez niektóre akcje zmian danych użytkownika, potrzebujemy toofind wszystkie działania hello kiedykolwiek została i zaktualizować je wszystkie. Nie dźwięk bardzo praktyczne, prawy?

Możemy toosolve będzie on identyfikując hello atrybuty klucza użytkownika, który zostanie przedstawiony w naszej aplikacji dla każdego działania. Jeśli firma Microsoft wizualnie Pokaż ogłoszenie (post) w naszej aplikacji i zawierają tylko twórca hello nazwę i obraz, dlaczego przechowywać wszystkie dane użytkownika hello w atrybucie hello "recenzowania utworzone przez"? Jeśli dla każdego komentarza możemy tylko wyświetlić obraz powitania użytkownika, firma Microsoft nie wymagają hello reszty jego informacje. To, gdzie wejścia coś można wywołać hello "drabina wzorzec" play.

Spójrzmy informacje o użytkowniku, na przykład:

    {
        "id":"dse4-qwe2-ert4-aad2",
        "name":"John",
        "surname":"Doe",
        "address":"742 Evergreen Terrace",
        "birthday":"1983-05-07",
        "email":"john@doe.com",
        "twitterHandle":"@john",
        "username":"johndoe",
        "password":"some_encrypted_phrase",
        "totalPoints":100,
        "totalPosts":24
    }

Analizując te informacje, firma Microsoft szybko wykrywać czyli kluczowych informacji i który nie jest tworząc "Drabina":

![Diagram przedstawiający wzorzec drabinę](./media/social-media-apps/social-media-apps-ladder.png)

krok najmniejszą Hello jest nazywany UserChunk, hello minimalnego część informacji umożliwiających identyfikację użytkownika i jest używany do duplikacji danych. Zmniejszenie rozmiaru hello "w tekście" hello zduplikowane dane tooonly hello informacji, firma Microsoft ograniczenie możliwości hello ogromną aktualizacji.

krok środkowej Hello jest nazywany hello użytkownika, jest hello pełnych danych, które będą używane w większości kwerend wydajności zależnych na DB rozwiązania Cosmos hello najbardziej uzyskuje się dostęp i krytyczne. Zawiera ona informacje hello reprezentowany przez UserChunk.

największy Hello jest hello rozszerzone użytkownika. Zawiera wszystkie informacje o użytkowniku krytyczne hello oraz inne dane, które nie naprawdę potrzebne odczytu toobe szybko lub jej użycie jest ostatecznego (na przykład hello procesu logowania). Te dane mogą być przechowywane poza rozwiązania Cosmos bazy danych, w bazie danych SQL Azure lub tabel magazynu Azure.

Dlaczego czy możemy podzielić hello użytkownika i nawet przechowywać tych informacji w różnych miejscach? Ponieważ z punktu widzenia wydajności, hello większy hello dokumentów, hello costlier hello zapytania. Przechowuje dokumenty cienki z hello prawo toodo informacji wszystkie Twoje wydajności zależnych od wysyła zapytanie sieci społecznościowych i magazynu hello innych dodatkowych informacji dotyczących ostatecznego scenariuszy, takich jak, edycji profilu pełne, logowania, nawet wyszukiwania danych do analizy użycia i Big Inicjatyw danych. Firma Microsoft naprawdę nieważne Jeśli hello zbierania danych do wyszukiwania danych jest mniejsza, ponieważ nie jest uruchomiona w bazie danych SQL Azure, firma Microsoft ma dotyczy jednak użytkowników że szybkie i obsługiwane środowiska. Użytkownik, przechowywane na DB rozwiązania Cosmos będzie wyglądać następująco:

    {
        "id":"dse4-qwe2-ert4-aad2",
        "name":"John",
        "surname":"Doe",
        "username":"johndoe"
        "email":"john@doe.com",
        "twitterHandle":"@john"
    }

I Post powinien wyglądać tak:

    {
        "id":"1234-asd3-54ts-199a",
        "title":"Awesome post!",
        "date":"2016-01-02",
        "createdBy":{
            "id":"dse4-qwe2-ert4-aad2",
            "username":"johndoe"
        }
    }

I podczas edycji występuje, gdy jeden z atrybutów hello fragmentu hello naruszona, jest łatwe toofind hello wpływ dokumentów przy użyciu zapytań, które wskazują atrybuty toohello indeksowane (Wybierz * FROM ogłoszeń p WHERE p.createdBy.id == "edited_user_id"), a następnie zaktualizowanie Witaj fragmentów.

## <a name="hello-search-box"></a>pole wyszukiwania Hello
Użytkownicy wygeneruje szczęście dużo zawartości. Firma Microsoft powinny być możliwe tooprovide hello możliwości toosearch i znaleźć zawartość, która może być bezpośrednio w ich strumieni zawartości, może być ponieważ firma Microsoft nie wykonuj twórców hello i może być tylko próbujemy toofind tego starego post, które robiliśmy 6 mies.

Thankfully i ponieważ używamy bazy danych Azure rozwiązania Cosmos, firma Microsoft może łatwo zaimplementować aparat wyszukiwania przy użyciu [usługi Azure Search](https://azure.microsoft.com/services/search/) w kilka minut i bez wprowadzania pojedynczy wiersz kodu (inne niż oczywiście hello wyszukiwania procesu i interfejsu użytkownika).

Dlaczego jest to tak proste?

Usługa Azure Search implementuje one wywołać [indeksatory](https://msdn.microsoft.com/library/azure/dn946891.aspx)tła przetwarza tego punktu zaczepienia w repozytoriami danych i automagically dodać, zaktualizować lub usunąć obiektów w indeksach hello. Obsługują one [indeksatory bazy danych SQL Azure](https://blogs.msdn.microsoft.com/kaevans/2015/03/06/indexing-azure-sql-database-with-azure-search/), [indeksatory obiektów blob Azure](../search/search-howto-indexing-azure-blob-storage.md) i thankfully, [indeksatory bazy danych Azure rozwiązania Cosmos](../search/search-howto-index-documentdb.md). Witaj przejścia informacji z bazy danych rozwiązania Cosmos tooAzure wyszukiwania jest bezpośrednie jako zarówno informacje magazynie w formacie JSON, potrzebujemy zbyt[tworzenia indeksu](../search/search-create-index-portal.md) i mapowanie atrybutów, które z naszych dokumentów chcemy indeksowane i to wszystko, w ciągu kilku minut (zależy od rozmiaru hello naszych danych), wszystkich naszych zawartość będzie dostępna toobe wyszukiwanych przez hello najlepsze rozwiązanie wyszukiwanie jako usługa w chmurze infrastruktury. 

Aby uzyskać więcej informacji na temat usługi Azure Search, możesz odwiedzić hello [Hitchhiker w przewodniku tooSearch](https://blogs.msdn.microsoft.com/mvpawardprogram/2016/02/02/a-hitchhikers-guide-to-search/).

## <a name="hello-underlying-knowledge"></a>Witaj podstawowej wiedzy
Po zapisaniu tej zawartości, który powiększa się i rozwoju codziennie, firma Microsoft może jesteśmy myśląc: co można zrobić z tego strumienia informacji od moich użytkowników?

odpowiedzi Hello jest prosta: umieszcza je toowork i Dowiedz się od niego.

Ale co możemy informacje? Kilka łatwe przykładów [analizy wskaźniki nastrojów klientów](https://en.wikipedia.org/wiki/Sentiment_analysis), zawartości zalecenia zgodnie z preferencjami użytkownika lub nawet automatycznych zawartości moderatora, który zapewnia, że wszystkie hello zawartości opublikowane przez naszych sieci społecznościowych jest bezpieczne dla hello rodziny.

Teraz, możesz argumentów podłączono otrzymano, prawdopodobnie będzie traktować należy niektórych Praca w tooextract nauki matematyczne tych wzorców i informacje o proste baz danych i plików, ale może być nieprawidłowy.

[Usługa Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/), część hello [pakietu Cortana Intelligence Suite](https://www.microsoft.com/en/server-cloud/cortana-analytics-suite/overview.aspx), jest hello pełni zarządzanej usługi w chmurze umożliwiający tworzenie przepływów pracy za pomocą prostego interfejsu przeciągania i upuszczania za pomocą algorytmów, kod własnych algorytmów w [R](https://en.wikipedia.org/wiki/R_\(programming_language\)) lub korzystać z niektórych hello już utworzone i gotowe toouse interfejsów API, takich jak: [Analiza tekstu](https://gallery.cortanaanalytics.com/MachineLearningAPI/Text-Analytics-2), [zawartości moderatora](https://www.microsoft.com/moderator) lub [zalecenia](https://gallery.cortanaanalytics.com/MachineLearningAPI/Recommendations-2).

tooachieve dowolnego z tych scenariuszy uczenia maszynowego, możemy użyć [usługi Azure Data Lake](https://azure.microsoft.com/services/data-lake-store/) tooingest hello informacji z różnych źródeł i użyj [U-SQL](https://azure.microsoft.com/documentation/videos/data-lake-u-sql-query-execution/) tooprocess hello informacji i generowania danych wyjściowych które mogą być przetwarzane przez usługi Azure Machine Learning.

Toouse jest też druga opcja dostępna [kognitywnych usług firmy Microsoft](https://www.microsoft.com/cognitive-services) tooanalyze naszych użytkowników zawartości; nie tylko będziemy ich zrozumienie lepsze (za pośrednictwem analizowanie zapisują z [interfejsu API z analizy tekstu](https://www.microsoft.com/cognitive-services/en-us/text-analytics-api)), ale Firma Microsoft może również wykrywania niechcianych ani dojrzałe zawartości i odpowiednio działają z [komputera wizji API](https://www.microsoft.com/cognitive-services/en-us/computer-vision-api). Kognitywnych usługi obejmują wiele rozwiązań poza pole, które nie wymagają dowolnego rodzaju toouse wiedzy uczenia maszynowego.

## <a name="a-planet-scale-social-experience"></a>W środowisku społecznościowych planety skali
Jest ostatni, ale nie najmniej ważne tematu I muszą spełnić: **skalowalność**. Podczas projektowania architektury, które ważne jest, że każdego składnika można skalować na własną, albo ponieważ potrzebujemy tooprocess większej ilości danych lub ponieważ chcemy toohave większy pokrycia geograficznego (lub obu tych!). Thankfully, jest złożonym zadaniem osiągnięcia **gotowe środowisko** DB rozwiązania Cosmos.

Obsługuje rozwiązania cosmos DB [dynamiczne partycjonowanie](https://azure.microsoft.com/blog/10-things-to-know-about-documentdb-partitioned-collections/) out-of--box przez automatyczne tworzenie partycji na podstawie danego **klucza partycji** (zdefiniowany jako jeden z atrybutów hello w dokumentach). Definiowanie hello poprawny klucz partycji musi odbywać się w czasie projektowania i utrzymywanie w uwadze hello [najlepsze rozwiązania](../cosmos-db/partition-data.md#designing-for-partitioning) dostępne; w przypadku hello środowisko społecznościowych, muszą być wyrównane strategii partycjonowania sposób hello zapytania (odczyty w ramach hello tej samej partycji są pożądane) i zapisu (uniknąć "punkty aktywne" przez rozłożenie zapisy na wielu partycjach). Niektóre opcje są: partycje oparte na kluczu danych czasowych (dzień/miesiąc/tydzień), zawartości kategorii, regionu geograficznego, przez użytkownika. wszystko naprawdę zależy od sposobu będzie zapytania na danych hello i pokazać środowiska społecznościowych. 

Jedną jest interesujące punktu warto zauważyć, które DB rozwiązania Cosmos wykona zapytania (w tym [agreguje](https://azure.microsoft.com/blog/planet-scale-aggregates-with-azure-documentdb/)) we wszystkich partycji w sposób przezroczysty, nie potrzebujesz tooadd wszelka logika wraz z rozwojem danych.

Z upływem czasu, należy po pewnym czasie wzrośnie w ruchu i użycia zasobów (mierzony w [RUs](request-units.md), albo w jednostkach żądań) wzrośnie. Zostanie odczytu i zapisu w częściej, Twoje userbase rozwoju lub rozpocznie tworzenie i odczytywanie więcej zawartości; Witaj zdolność **skalowanie sieci przepływności** jest ważna. Zwiększenie naszych RUs jest bardzo proste, możemy go za pomocą kilku kliknięć na powitania portalu Azure lub [wydawania polecenia przy użyciu interfejsu API hello](https://docs.microsoft.com/rest/api/documentdb/replace-an-offer).

![Skalowanie w i definiowanie klucza partycji](./media/social-media-apps/social-media-apps-scaling.png)

Co się stanie, jeśli elementy pojawiają się lepiej użytkownicy z innego regionu, kraj lub kontynencie, zwróć uwagę, platformy i rozpocząć korzystanie z niej zaskoczeniem doskonałe!

Czekaj..., ale wkrótce realizować ich obsługi platformy nie są optymalne; są one wykonanej do tej pory od regionu operacyjne opóźnienie hello jest olbrzymich, czy oczywiście nie chcesz ich tooquit. Jeśli tylko było łatwo z **rozszerzanie zasięg globalny**..., ale istnieje!

Rozwiązania cosmos DB umożliwia [replikowany globalnie danych](../cosmos-db/tutorial-global-distribution-documentdb.md) i niewidocznie za pomocą paru kliknięć i automatycznie wybrać spośród dostępnych regionów hello z Twojej [kodu klienta](../cosmos-db/tutorial-global-distribution-documentdb.md). Oznacza to również, że może mieć [kilka obszarów failover](regional-failover.md). 

Gdy danych jest replikowany globalnie, należy się upewnić, że klienci mogą wykorzystać go toomake. Jeśli używasz frontonu sieci web lub w celu dostępu interfejsy API z klientów mobilnych, można wdrożyć [usługi Azure Traffic Manager](https://azure.microsoft.com/services/traffic-manager/) i klonowanie usługi aplikacji Azure na wszystkie potrzeby hello regionach, przy użyciu [konfigurację wydajności](../app-service-web/web-sites-traffic-manager.md)toosupport ten rozszerzonej zasięg globalny. W przypadku klientów dostępu z frontonu lub interfejsów API, zostaną one toohello routingiem najbliższego usługi aplikacji, co z kolei powoduje ustanowienie połączenia toohello lokalnej repliki bazy danych rozwiązania Cosmos.

![Dodawanie platformy społecznościowych tooyour pokrycia globalne](./media/social-media-apps/social-media-apps-global-replicate.png)

## <a name="conclusion"></a>Podsumowanie
W tym artykule próbuje tooshed niektóre jasny do alternatyw hello całkowicie tworzenie sieci społecznościowych na platformie Azure z ekonomicznych usług i zapewnienia doskonałe wyniki przy użyciu hello wspieranie dystrybucji rozwiązanie i danych wielowarstwowy magazynu o nazwie "Drabina".

![Diagram interakcji między usługami Azure, sieci społecznościowych](./media/social-media-apps/social-media-apps-azure-solution.png)

prawdy Hello jest czy bez srebrny punktora dla tego rodzaju scenariusze nie istnieje, ma hello współdziałania utworzone za pomocą kombinacji hello niezwykłych usług, które zezwalają toobuild doskonałe funkcje: hello szybkość i swobody tooprovide bazy danych Azure rozwiązania Cosmos dużą społecznego aplikacji, analizy Hello za rozwiązania najwyższej jakości wyszukiwania, takich jak usługi Azure Search, elastyczność hello toohost usługi aplikacji Azure nawet aplikacji niezależny od języka, ale procesów w tle wydajne i hello rozwijania usługi Azure Storage i bazą danych SQL Azure dla przechowywania dużych ilości danych i hello możliwości analityczne toocreate usługi Azure Machine Learning wiedzy i analizy, które można wyrazić swoją opinię tooour procesy i pomóc nam dostarczania hello prawo zawartości toohello odpowiednich użytkowników.

## <a name="next-steps"></a>Następne kroki
toolearn więcej informacji na temat przypadki użycia rozwiązania Cosmos bazy danych, zobacz [DB rozwiązania Cosmos typowych zastosowań](use-cases.md).
