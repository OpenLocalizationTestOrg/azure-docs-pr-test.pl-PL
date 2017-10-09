---
title: "aaaAnalyze wydajności węzłów brzegowych w usłudze Azure CDN | Dokumentacja firmy Microsoft"
description: "Analizowanie wydajności węzłów brzegowych w usłudze Microsoft Azure CDN. Analiza wydajności krawędzi zawiera szczegółowe informacje o ruchu i użycia przepustowości hello CDN."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 8cc596a7-3e01-4f76-af7b-a05a1421517e
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 35361d1c5e27fc6b8536c29e33c2ed217ee4d17e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-edge-node-performance-in-microsoft-azure-cdn"></a>Analizowanie wydajności węzła brzegowego w usłudze Microsoft Azure CDN
[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

## <a name="overview"></a>Omówienie
Analiza wydajności krawędzi zawiera szczegółowe informacje o ruchu i użycia przepustowości hello CDN. Te informacje mogą być następnie używane toogenerate trendów statystyk umożliwiające toogain wgląd w sposób zasobów są klientów pamięci podręcznej i dostarczonego tooyour. Z kolei to umożliwia tooform możesz strategii w sposób toooptimize hello dostarczania zawartości i toodetermine problemy, jakie należy zająć się toobetter wykorzystać hello CDN. W związku z tym nie tylko możesz będą mogli tooimprove danych wydajność, ale będą również być stanie tooreduce koszty sieci CDN.

> [!NOTE]
> Wszystkie raporty Notacja UTC/GMT podczas określania daty/godziny.
> 
> 

## <a name="reports-and-log-collection"></a>Raporty i zbierania dzienników
Należy zbierać dane działanie CDN przez moduł analizy wydajności krawędzi hello przed może generować raporty na nim. Ten proces zbierania występuje, gdy dziennie i obejmuje hello działanie, które miało miejsce podczas hello poprzedniego dnia. To oznacza, że dane statystyczne raportu reprezentują próbkę dzień hello statystyki w czasie hello zostało przetworzone i nie musi zawierać hello pełny zestaw danych dla hello bieżącego dnia. podstawową funkcją Hello tych raportów jest tooassess wydajności. Ich nie stosuje się do celów rozliczeń lub dokładną statystyki liczbowych.

> [!NOTE]
> nieprzetworzone dane Hello, z którego są generowane raporty analityczne wydajności krawędzi jest dostępna dla co najmniej 90 dni.
> 
> 

## <a name="dashboard"></a>Pulpit nawigacyjny
pulpitu nawigacyjnego Analytics wydajności krawędzi Hello śledzi bieżące i historyczne ruch CDN przez wykres i statystyki. Użyj tego pulpitu nawigacyjnego toodetect ostatnie i długoterminowych trendów na wydajność hello ruchu w sieci CDN dla Twojego konta.

Ten pulpit nawigacyjny zawiera:

* Wykres interakcyjny, który umożliwia wizualizację hello kluczowych metryk i trendów.
* Oś czasu, która zapewnia w pewnym sensie wzorce długoterminowej kluczowych metryk i trendów.
* Kluczowe metryki i informacje statystyczne na temat naszych sieci CDN poprawia ruch w witrynie mierzony ogólnej wydajności, użycia i wydajności.

### <a name="accessing-hello-edge-performance-dashboard"></a>Uzyskiwanie dostępu do pulpitu nawigacyjnego wydajności krawędzi hello
1. Blok profilu CDN hello, kliknij hello **Zarządzaj** przycisku.
   
    ![Przycisk Zarządzaj blok profilu CDN](./media/cdn-edge-performance/cdn-manage-btn.png)
   
    Otwiera portalu zarządzania Hello CDN.
2. Przesuń kursor myszy hello **Analytics** kartę, a następnie przesuń kursor myszy hello **analizy wydajności krawędzi** wysuwane okno.  Polecenie **pulpitu nawigacyjnego**.
   
    nawigacyjnym analizy węzła krawędzi Hello jest wyświetlany.

### <a name="chart"></a>Wykres
pulpit nawigacyjny Hello zawiera wykres umożliwia śledzenie metrykę hello okresu wybranego hello osi czasu, który pojawia się bezpośrednio pod.  Oś czasu, który wykresach się toohello ostatnie dwa lata działania w sieci CDN w warstwie jest wyświetlana bezpośrednio pod hello wykresu.

#### <a name="using-hello-chart"></a>Za pomocą wykresu hello
* Domyślnie zostanie wykresie szybkość wydajność pamięci podręcznej hello hello ostatnich 30 dni.
* Ten wykres jest generowany na podstawie danych sortowane codziennie.
* Kursora myszy nad dzień w wykres liniowy hello wskaże wartość daty i hello metryki hello w tym dniu.
* Kliknij przycisk Wyróżnij weekendów tootoggle nakładki światła szarego pionowych słupków, reprezentujących weekendów na powitania wykres. Ten typ nakładki jest przydatny do identyfikowania wzorców ruchu w weekendy.
* Kliknij widok jednego roku temu tootoggle nakładką hello poprzedniego działania roku za pośrednictwem hello sam okres na powitania wykres czasu. Ten typ porównania zapewnia wgląd w długoterminowej wzorców użycia sieci CDN. Witaj prawym górnym rogu wykresu hello zawiera legendy, wskazującą hello kod dla każdego wiersza wykresu.

#### <a name="updating-hello-chart"></a>Aktualizowanie wykresu hello
* Przedział czasu: Wykonaj jedną z następujących hello:
  * Wybierz odpowiedni region hello hello osi czasu. Wykres Hello zostanie zaktualizowany z danymi, które odpowiada toohello w wybranym okresie.
  * Kliknij dwukrotnie hello toodisplay wykresu wszystkie dostępne dane historyczne w górę tooa maksymalnie dwa lata.
* Metryka: Kliknij ikonę wykres hello dalej Metryka toohello potrzeby. oś czasu hello i wykres Hello zostanie odświeżona danych dla metryki odpowiedniego hello.

### <a name="key-metrics-and-statistics"></a>Kluczowe metryki i dane statystyczne
#### <a name="efficiency-metrics"></a>Metryki wydajności
Witaj celem tych metryk jest toosee, czy można zwiększyć wydajność pamięci podręcznej. korzyściami Hello pochodną wydajność pamięci podręcznej są:

* Zmniejszenie obciążenia serwera pochodzenia hello, co może prowadzić do:
  * Lepszą wydajność serwera sieci web.
  * Mniejsze koszty operacyjne.
* Ulepszona przyspieszenia dostarczania danych, ponieważ więcej żądań zostanie obsłużona bezpośrednio z hello CDN.

| Pole | Opis |
| --- | --- |
| Wydajność pamięci podręcznej |Wskazuje procent hello danych przesyłanych zostało obsłużone z pamięci podręcznej. Ta metryka środków po buforowanej wersji hello zażądał zawartości zostało obsłużone bezpośrednio z hello sieci CDN (serwery krawędzi) toorequesters (np. przeglądarki sieci web) |
| Częstotliwość trafień |Wskazuje hello odsetek żądań, które zostały obsłużone z pamięci podręcznej. Ta metryka środków po buforowanej wersji hello zażądał zawartości zostało obsłużone bezpośrednio z hello sieci CDN (serwery krawędzi) toorequesters (np. przeglądarki sieci web). |
| % liczby bajtów zdalnego — nie konfiguracji pamięci podręcznej |Wskazuje procent hello ruchu, który zostało obsłużone z toohello serwerów pochodzenia sieci CDN (serwery krawędzi) nie będzie zapisywane w wyniku hello funkcja pomijania pamięci podręcznej (aparat reguł HTTP). |
| % Zdalnego bajtów - wygasł pamięci podręcznej |Wskazuje procent hello ruchu, który zostało obsłużone z pochodzenia toohello serwerów (serwery krawędzi) w sieci CDN w wyniku starych ponowna Walidacja zawartości. |

#### <a name="usage-metrics"></a>Metryki użycia
Witaj tych metryk służy tooprovide wgląd w hello następujące środki Wycinanie koszt:

* Minimalizację kosztów operacyjnych za pośrednictwem hello CDN.
* Ograniczenie wydatków CDN za pośrednictwem wydajność pamięci podręcznej i kompresji.

> [!NOTE]
> Numery hurtowych ruchu reprezentują ruch, który był używany w obliczeniach stosunek i wartości procentowe i mogą być wyświetlane tylko część hello ruch związany z dużej liczby klientów.
> 
> 

| Pole | Opis |
| --- | --- |
| Zapisz bajtów wyjściowych |Wskazuje hello średnią liczbę bajtów przesłanych dla każdego żądania z hello sieci CDN (serwery krawędzi) toohello żądający (np. przeglądarki sieci web). |
| Nie szybkość Config bajtów pamięci podręcznej |Wskazuje procent hello ruch pochodzący z hello sieci CDN (serwery krawędzi) toohello żądający (np. przeglądarki sieci web), które nie będą buforowane z powodu toohello funkcja pomijania pamięci podręcznej. |
| Szybkość skompresowanych bajtów |Wskazuje procent hello ruch wysyłany z hello sieci CDN (serwery krawędzi) toorequesters (np. przeglądarki sieci web), w formacie skompresowanym. |
| Bajty wysłane |Wskazuje hello ilości danych w bajtach, które zostały dostarczone z hello sieci CDN (serwery krawędzi) toohello żądający (np. przeglądarki sieci web). |
| Wyrażona w bajtach |Wskazuje hello ilości danych, bajtów wysłanych z toohello jednostek żądających (np. przeglądarki sieci web) sieci CDN (serwery krawędzi). |
| Zdalne bajtów |Wskazuje hello ilości danych, bajtów wysłanych z sieci CDN i klienta toohello serwerów pochodzenia sieci CDN (serwery krawędzi). |

#### <a name="performance-metrics"></a>Metryki wydajności
Witaj tych metryk służy tootrack ogólną wydajność sieci CDN dla ruchu.

| Pole | Opis |
| --- | --- |
| Szybkość transferu |Wskazuje średnią hello przeniesienia zawartości z hello CDN tooa żądającego. |
| Czas trwania |Wskazuje hello Średni czas w milisekundach, zajęło toodeliver żądający tooa zasobów (np. przeglądarki sieci web). |
| Współczynnik żądań skompresowane |Wskazuje hello procent trafień, które zostały dostarczone z hello sieci CDN (serwery krawędzi) toohello żądający (np. przeglądarki sieci web), w formacie skompresowanym. |
| Współczynnik błędów 4xx |Wskazuje hello procent trafień wygenerowanych 4xx kod stanu. |
| Współczynnik błędów 5xx |Wskazuje hello procent trafień wygenerowanych 5xx kod stanu. |
| Liczba trafień |Wskazuje liczbę hello żądania dotyczące zawartości w sieci CDN. |

#### <a name="secure-traffic-metrics"></a>Bezpieczny ruch metryk
Celem Hello tych metryk jest tootrack CDN wydajności dla ruchu HTTPS.

| Pole | Opis |
| --- | --- |
| Zabezpieczenia, wydajność pamięci podręcznej |Wskazuje procent hello danych przesyłanych do żądań HTTPS, które zostały obsłużone z pamięci podręcznej. Ta metryka mierzy podczas buforowanej wersji hello zażądał zawartości zostało obsłużone bezpośrednio z hello sieci CDN (serwery krawędzi) toorequesters (np. przeglądarki sieci web) za pośrednictwem protokołu HTTPS. |
| Zabezpieczanie szybkość transferu |Wskazuje średnią hello przeniesienia zawartości z hello sieci CDN (serwery krawędzi) toorequesters (np. serwery sieci web) za pośrednictwem protokołu HTTPS. |
| Średni czas trwania bezpieczne |Wskazuje hello Średni czas w milisekundach, zajęło toodeliver żądający tooa zasobów (np. przeglądarki sieci web) za pośrednictwem protokołu HTTPS. |
| Bezpieczne trafień |Wskazuje liczbę hello żądania HTTPS zawartości usługi CDN. |
| Bezpieczne bajtów wyjściowych |Wskazuje wielkość hello ruch HTTPS w bajtach, które zostały dostarczone z hello sieci CDN (serwery krawędzi) toohello żądający (np. przeglądarki sieci web). |

## <a name="reports"></a>Raporty
Każdy raport, w tym module zawiera wykres i statystyki dotyczące wykorzystania przepustowości i ruchu dla różnych typów metryki (np. kody stanu HTTP, kodów stanu pamięci podręcznej, żądanie adresu URL itp).. Te informacje mogą być używane toodelve zapoznanie się jak zawartość jest obsługiwanej tooyour klientów i strojenia toofine CDN zachowanie tooimprove danych wydajność.

### <a name="accessing-hello-edge-performance-reports"></a>Uzyskiwanie dostępu do raportów wydajności hello krawędzi
1. Blok profilu CDN hello, kliknij hello **Zarządzaj** przycisku.
   
    ![Przycisk Zarządzaj blok profilu CDN](./media/cdn-edge-performance/cdn-manage-btn.png)
   
    Otwiera portalu zarządzania Hello CDN.
2. Przesuń kursor myszy hello **Analytics** kartę, a następnie przesuń kursor myszy hello **analizy wydajności krawędzi** wysuwane okno.  Polecenie **HTTP dużego obiektu**.
   
    Witaj krawędzi węzła analytics raporty ekran jest wyświetlany.

| Raport | Opis |
| --- | --- |
| Dzienne podsumowanie |Umożliwia tooview dzienne trendy ruchu w określonym przedziale czasu. Każdy słupek na wykresie reprezentuje określonej daty. rozmiar Hello paska hello wskazuje hello łączna liczba trafień, które wystąpiły w tym dniu. |
| Podsumowanie co godzinę |Umożliwia tooview co godzinę ruchu trendów w określonym przedziale czasu. Każdy słupek na tym wykresie reprezentuje pojedynczy godzinę w określonym dniu. rozmiar Hello paska hello wskazuje hello łączna liczba trafień, które wystąpiły podczas danej godziny. |
| Protokoły |Przedstawia podział hello ruchu między hello HTTP i HTTPS protokołów. Wykres pierścieniowy przedstawiający wskazuje hello procent trafień, które wystąpiły dla każdego typu protokołu. |
| Metody HTTP |Pozwala tooget są nowościami metod HTTP, które są używane toorequest danych. Zazwyczaj hello najbardziej typowe metody żądania HTTP są GET, HEAD i POST. Wykres pierścieniowy przedstawiający wskazuje hello procent trafień, które wystąpiły dla każdego typu Metoda żądania HTTP. |
| Adresy URL |Zawiera wykres przedstawia hello top 10 adresy URL. Dla każdego adresu URL jest wyświetlany pasek. Hello wysokość paska hello wskazuje, ile razy wygenerowanych określonego adresu URL za pośrednictwem przedział czasu hello objętego raportem hello. Statystyka dla hello pierwszych 100 zażądał adresy URL są wyświetlane bezpośrednio poniżej tego wykresu. |
| CNAME |Zawiera wykresu, który zawiera hello top 10 CNAME używane toorequest zasoby za pośrednictwem hello przedział czasu raportu. Statystyka dla hello pierwszych 100 zażądał CNAME są wyświetlane bezpośrednio poniżej tego wykresu. |
| Źródeł |Zawiera wykresu, który wyświetla hello 10 pierwszych CDN lub klienta pochodzenia serwery z których wystąpiło zasobów w określonym okresie. Statystyka dla hello pierwszych 100 zażądał serwery pochodzenia CDN lub klienta są wyświetlane bezpośrednio poniżej tego wykresu. Serwery pochodzenia klienta są identyfikowane przez nazwę hello zdefiniowany w hello opcji Nazwa katalogu. |
| POP Geo |Pokazuje, ile ruchu rozsyłane do określonego punktu elementu obecności (POP). Skrót trzyliterowy Hello reprezentuje POP w naszej sieci CDN. |
| Klienci |Zawiera wykres przedstawia hello top 10 klientów, którzy zażądali zasobów w określonym okresie. Do celów hello tego raportu, wszystkie żądania, które pochodzą ze hello sam adres IP, są traktowane jako toobe z hello tego samego klienta. Statystyki dotyczące hello top 100 klientów są wyświetlane bezpośrednio poniżej tego wykresu. Ten raport jest przydatne w przypadku określania wzorce działania pobierania top klientów. |
| Stany pamięci podręcznej |Zapewnia szczegółowe podział zachowanie pamięci podręcznej może ujawnić podejścia do poprawy hello środowisko pracy użytkownika końcowego. Ponieważ hello największą wydajność pochodzi z trafień w pamięci podręcznej, aby zoptymalizować szybkości dostarczania danych, minimalizując Chybienia pamięci podręcznej i trafień w pamięci podręcznej wygasła. |
| Brak szczegółowych informacji |Zawiera wykres przedstawia hello top 10 adresów URL dla zasobów, dla których aktualności zawartości pamięci podręcznej nie została sprawdzona w określonym okresie. Statystyki dotyczące hello top 100 adresów URL dla tych typów zasobów są wyświetlane bezpośrednio poniżej tego wykresu. |
| Szczegóły CONFIG_NOCACHE |Zawiera wykresu, który wyświetla adresy URL 10 pierwszych hello zasoby, które nie zostały zapisane ukończenia konfiguracji CDN toohello klienta. Tego rodzaju zasoby zostały obsłużone bezpośrednio z serwera źródłowego hello. Statystyki dotyczące hello top 100 adresów URL dla tych typów zasobów są wyświetlane bezpośrednio poniżej tego wykresu. |
| Szczegóły UNCACHEABLE |Zawiera wykres przedstawia hello top 10 adresów URL dla zasobów, których nie można buforować powodu toorequest danych nagłówka. Statystyki dotyczące hello top 100 adresów URL dla tych typów zasobów są wyświetlane bezpośrednio poniżej tego wykresu. |
| Szczegóły TCP_HIT |Zawiera wykres przedstawia hello top 10 adresów URL dla zasobów, które są obsługiwane bezpośrednio z pamięci podręcznej. Statystyki dotyczące hello top 100 adresów URL dla tych typów zasobów są wyświetlane bezpośrednio poniżej tego wykresu. |
| Szczegóły TCP_MISS |Zawiera wykres przedstawia hello top 10 adresów URL dla zasobów, które będą miały stan TCP_MISS pamięci podręcznej. Statystyki dotyczące hello top 100 adresów URL dla tych typów zasobów są wyświetlane bezpośrednio poniżej tego wykresu. |
| Szczegóły TCP_EXPIRED_HIT |Zawiera wykres przedstawia hello top 10 adresy URL starych zasoby, które były przekazywane bezpośrednio z hello POP. Statystyki dotyczące hello top 100 adresów URL dla tych typów zasobów są wyświetlane bezpośrednio poniżej tego wykresu. |
| Szczegóły TCP_EXPIRED_MISS |Zawiera wykres przedstawia hello top 10 adresów URL starych zasobów, dla których nowa wersja ma toobe pobrane z serwera źródłowego hello. Statystyki dotyczące hello top 100 adresów URL dla tych typów zasobów są wyświetlane bezpośrednio poniżej tego wykresu. |
| Szczegóły TCP_CLIENT_REFRESH_MISS |Zawiera wykres słupkowy wyświetlający hello top 10 adresów URL dla zasobów zostały pobrane z serwera pochodzenia ukończenia żądania nie-cache tooa powitania klienta. Statystyki dla hello top 100 adresów URL dla tych typów żądań, które są wyświetlane bezpośrednio pod ten wykres. |
| Typy żądań klienta |Wskazuje typ hello żądań, które zostały dokonane przez klientów HTTP (np. przeglądarki). Ten raport zawiera wykres pierścieniowy przedstawiający zapewnia zorientować się jako toohow, które żądania są obsługiwane. Informacje o przepustowości i ruchu dla każdego typu żądania jest wyświetlony poniżej hello wykresu. |
| Agent użytkownika |Zawiera wykres słupkowy wyświetlanie zawartości za pośrednictwem naszego CDN hello top toorequest agentów użytkownika 10. Agent użytkownika jest zwykle przeglądarki sieci web, odtwarzacza lub przeglądarki telefonu komórkowego. Statystyki dotyczące hello top agentów 100 użytkowników są wyświetlane bezpośrednio pod ten wykres. |
| Odwołań |Zawiera wykres słupkowy wyświetlanie toocontent najczęstsze 10 hello dostępne za pośrednictwem naszego CDN. Zazwyczaj odwołania jest adres URL hello hello strony sieci web lub zasobu, który stanowi łącze tooyour zawartości. Szczegółowe informacje podano poniżej wykresu hello dotyczących hello najczęstsze 100. |
| Typy kompresji |Zawiera wykres pierścieniowy przedstawiający dzieli żądanych zasobów według tego, czy zostały skompresowane przez serwery krawędzi. Procent Hello skompresowany zasobów jest rozbiciu hello typ kompresji używany. Szczegółowe informacje poniżej hello wykresu dla każdego typu kompresji i stanu. |
| Typy plików |Zawiera wykres słupkowy Wyświetla hello top 10 typów plików, które żądano za pośrednictwem naszego CDN dla Twojego konta. Do celów hello tego raportu, typu pliku jest definiowany przez rozszerzenie nazwy pliku hello zasobów i typ nośnika Internet (np. .html \[tekst i html\], .htm \[tekst i html\], .aspx \[tekstu/koduhtml\]itp.). Szczegółowe informacje poniżej wykresu hello hello top 100 plików. |
| Unikatowy plików |Zawiera wykres geograficzne hello całkowitej liczby unikatowych zasobów, zażądanych danego dnia w określonym okresie. |
| Token uwierzytelniania podsumowania |Zawiera wykresu kołowego, która zapewnia szybki przegląd na czy żądanych zasobów były chronione przez uwierzytelnianie oparte na Token. Chronionych zasobów są wyświetlane na wykresie hello zgodnie z wyników toohello ich próba uwierzytelniania. |
| Szczegóły Odmów tokenu uwierzytelniania |Zawiera wykres słupkowy, która pozwala tooview hello top 10 żądań, które zostały odrzucone ze względu na podstawie tooToken uwierzytelniania. |
| Kody odpowiedzi HTTP |Zawiera podział kodów stanu hello HTTP (np. 200 OK 403 Zabroniony, nie można odnaleźć 404, itp.) które zostały dostarczone klientów tooyour HTTP przez serwery krawędzi. Wykres kołowy pozwala tooquickly ocenić, jak zostały obsłużone zasobów. Szczegółowe dane statystyczne jest dostępna dla każdego kodu odpowiedzi poniżej hello wykresu. |
| Błędów 404 |Zawiera wykres słupkowy umożliwiający tooview hello top 10 żądań, które spowodowało 404 kod odpowiedzi nie znaleziono. |
| Błędy 403 |Zawiera wykres słupkowy umożliwiający tooview hello top 10 żądań, które spowodowało kod odpowiedzi 403 Zabroniony. Kod odpowiedzi 403 Zabroniony występuje, gdy żądanie zostanie odrzucone przez serwer pochodzenia klient lub serwer graniczny na naszych POP. |
| Błędy 4xx |Zawiera wykres słupkowy umożliwiający tooview hello top 10 żądań, które spowodowało kod odpowiedzi hello 400 zakresu. Ten raport to 403 404 kody odpowiedzi zabroniony i nie można odnaleźć. Zazwyczaj kod odpowiedzi 4xx występuje, gdy żądanie zostanie odrzucone wyniku błąd klienta. |
| Błędy 504 |Zawiera wykres słupkowy umożliwiający tooview hello top 10 żądań, które spowodowało 504 kod odpowiedzi upływu limitu czasu bramy. Kod odpowiedzi 504 upływu limitu czasu bramy występuje, gdy zostanie przekroczony limit czasu, gdy serwer proxy HTTP próbuje toocommunicate z innym serwerem. W przypadku hello naszych CDN 504 kod odpowiedzi upływu limitu czasu bramy zwykle występuje, gdy serwer graniczny jest tooestablish komunikacji z serwerem pochodzenia klienta. |
| Błędy 502 |Zawiera wykres słupkowy umożliwiający tooview hello top 10 żądań, które spowodowało 502 kod odpowiedzi zły bramy. 502 kod odpowiedzi Zła brama występuje, gdy wystąpił błąd protokołu HTTP między serwerem i serwer proxy HTTP. W przypadku hello naszych CDN 502 kod odpowiedzi Zła brama zwykle występuje, gdy serwer pochodzenia klienta zwraca serwer graniczny tooan nieprawidłową odpowiedź. Odpowiedź jest nieprawidłowa, jeśli nie można przeanalizować lub jest niekompletny. |
| Błędy 5xx |Zawiera umożliwiający tooview hello top 10 żądań, które spowodowało kod odpowiedzi w zakresie 500 hello wykresu słupkowego.  Ten raport to 502 Niewłaściwa brama i 504 kody odpowiedzi upływu limitu czasu bramy. |

## <a name="see-also"></a>Zobacz też
* [Omówienie usługi Azure CDN](cdn-overview.md)
* [Statystyki w czasie rzeczywistym w usłudze Microsoft Azure CDN](cdn-real-time-stats.md)
* [Zastępowanie domyślnego zachowania HTTP przy użyciu aparatu reguł hello](cdn-rules-engine.md)
* [Raporty HTTP zaawansowane](cdn-advanced-http-reports.md)

