---
title: "aaaAnalyze statystyk użycia z usługą Azure CDN zaawansowane raporty HTTP | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate zaawansowane raporty HTTP w usłudze Microsoft Azure CDN. Te raporty zawierają szczegółowe informacje w działaniu usługi CDN."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: ef90adc1-580e-4955-8ff1-bde3f3cafc5d
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 3184ec00d089613e25c62762f93043cb4ba68394
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-usage-statistics-with-azure-cdn-advanced-http-reports"></a>Analizowanie statystyk użycia z usługą Azure CDN zaawansowane raporty HTTP
## <a name="overview"></a>Omówienie
W tym dokumencie opisano zaawansowane HTTP raportowania w programie Microsoft Azure CDN. Te raporty zawierają szczegółowe informacje w działaniu usługi CDN.

[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

## <a name="accessing-advanced-http-reports"></a>Uzyskiwanie dostępu do zaawansowane raporty HTTP
1. Blok profilu CDN hello, kliknij hello **Zarządzaj** przycisku.
   
    ![Przycisk Zarządzaj blok profilu CDN](./media/cdn-advanced-http-reports/cdn-manage-btn.png)
   
    Otwiera portalu zarządzania Hello CDN.
2. Przesuń kursor myszy hello **Analytics** kartę, a następnie przesuń kursor myszy hello **zaawansowane raporty HTTP** wysuwane okno.  Polecenie **HTTP platformy dużych**.
   
    ![Portal zarządzania w sieci CDN — menu Zaawansowane raporty](./media/cdn-advanced-http-reports/cdn-advanced-reports.png)
   
    Opcje raportu są wyświetlane.

## <a name="geography-reports-map-based"></a>Lokalizacja geograficzna raporty (w oparciu o mapy)
Brak pięć raportów, które zalet tooindicate mapy hello regionów, z których zawartość jest wymagany. Te raporty są World mapy, mapy Stanów Zjednoczonych, Kanady mapy, mapy Europy i Azja i Pacyfik mapy.

Każdy raport na podstawie mapy szereguje geograficzne jednostek (tj. krajach, Stany i prowincje) zgodnie z toohello procent trafień, które pochodzą z tego regionu. Ponadto mapy jest warunkiem toohelp wizualizacji hello lokalizacje, z których zawartość jest wymagany. Jest możliwe toodo, więc przez kolorami każdego regionu, zgodnie z toohello ilość żądanie wystąpił w tym regionie. Jaśniejsze przyciemnione regionów wskazują niższe żądanie dla zawartości, gdy ciemniejszego regionów wskazać wyższego poziomu żądanie dla zawartości.

Szczegółowe informacje ruchu i przepustowości dla każdego regionu, znajduje się bezpośrednio pod hello mapy. Dzięki temu można tooview hello całkowitej liczby trafień, hello procent trafień, hello łączną ilość danych przesyłanych (w gigabajtach) i hello części danych przesyłanych do każdego regionu. Wyświetl opis każdego z tych metryk. Na koniec, po umieszczeniu na region (tj., kraj, Województwo), nazwę hello i hello procent trafień, które wystąpiły w regionie hello zostaną wyświetlone jako etykietka narzędzia.

Krótki opis podano poniżej dla każdego typu raportu na podstawie mapy geograficzne.

| Nazwa raportu | Opis |
| --- | --- |
| Mapa świata |Ten raport umożliwia tooview hello na całym świecie żądanie dla zawartości usługi CDN. Każdego kraju jest oznaczone kolorami na hello world mapy tooindicate hello procent trafień, które pochodzą z tego regionu. |
| Mapy Stanów Zjednoczonych |Ten raport umożliwia tooview hello żądanie dla zawartości w sieci CDN w hello Stanów Zjednoczonych. Każdy stan jest oznaczone kolorami, w tym mapy tooindicate hello procent trafień, które pochodzą z tego regionu. |
| Kanada mapy |Ten raport umożliwia tooview hello popytu na zawartość z sieci CDN w Kanady. Każdy region jest oznaczone kolorami, w tym mapy tooindicate hello procent trafień, które pochodzą z tego regionu. |
| Europa mapy |Ten raport umożliwia tooview hello popytu na zawartość z sieci CDN w Europie. Każdego kraju jest oznaczone kolorami, w tym mapy tooindicate hello procent trafień, które pochodzą z tego regionu. |
| Azja pacyficzny mapy |Ten raport umożliwia tooview hello popytu na zawartość z sieci CDN w Azji. Każdego kraju jest oznaczone kolorami, w tym mapy tooindicate hello procent trafień, które pochodzą z tego regionu. |

## <a name="geography-reports-bar-charts"></a>Lokalizacja geograficzna raportów (wykresy słupkowe)
Istnieją dwa dodatkowe raporty zawierające informacje statystyczne zgodnie z toogeography, miasta i krajów Top. Te raporty rank miejscowości i krajów, odpowiednio, zgodnie z toohello liczba trafień, pochodzących z tych obszarów. Podczas generowania raportu z tego typu, wykres słupkowy poinformuje hello top 10 miasta lub krajach, którzy zażądali zawartości na danej platformie. Ten wykres słupkowy pozwala tooquickly oceny regiony hello Generowanie hello największa liczba żądań dla zawartości.

powitania po lewej stronie powitania graph (oś y) wskazuje, ile razy wystąpił w wybranym regionie hello. Bezpośrednio pod hello graph (oś x) można znaleźć etykiety dla każdego top regionów 10 hello.

### <a name="using-hello-bar-charts"></a>Przy użyciu wykresy słupkowe hello
* Jeśli wskaźnik nad paskiem, nazwę hello i hello łączna liczba trafień, które wystąpiły w regionie hello będzie wyświetlany jako etykietka narzędzia.
* Hello etykietkę narzędzia hello raportu miasta identyfikuje Miasto według jego nazwy, Województwo i skrót kraju.
* Jeśli nie można ustalić hello miasta lub regionu (np. pola Województwo), z której pochodzi żądanie, następnie go będzie wskazuje, że są nieznane. Jeśli kraju hello jest nieznany, a następnie dwa znaki zapytania (tj.??), zostanie wyświetlony.
* Raport może zawierać metryki "Europie" lub hello "Region Azji i Pacyfiku." Elementy te nie mają tooprovide informacje statystyczne na temat wszystkich adresów IP w regionach. Zamiast mają one zastosowanie tylko toorequests, że pochodzą z adresów IP, które są rozproszone na Europa lub Azja i Pacyfik zamiast tooa określonym mieście lub kraju.

można wyświetlić dane Hello wykres słupkowy hello toogenerate używane poniżej. Można znaleźć hello łączna liczba trafień, hello procent trafień, hello ilość danych przesyłanych (w gigabajtach) i procent hello danych przesyłanych do hello top regionów 250. Wyświetl opis każdego z tych metryk.

Krótki opis jest dostępna dla obu typów raportów poniżej.

| Nazwa raportu | Opis |
| --- | --- |
| Miasta |Ten raport szereguje miast zgodnie z toohello liczba trafień, które pochodzą z tego regionu. |
| Górny krajach |Ten raport szereguje krajów zgodnie z toohello liczba trafień, które pochodzą z tego regionu. |

## <a name="daily-summary"></a>Dzienne podsumowanie
Raport dzienne podsumowanie Hello umożliwia tooview hello łączna liczba trafień i danych przesyłanych w konkretnej platformy codziennie. Informacje te mogą być używane tooquickly wykrycia wzorce działania w sieci CDN. Na przykład ten raport ułatwia wykrywanie dni doświadczonym wyższe lub niższe od oczekiwanego natężenia ruchu.

Podczas generowania raportu z tego typu, wykres słupkowy będzie wskazywania stanu jako toohello ilość doświadczonym żądanie specyficzne dla platformy codziennie przez hello objętego raportem hello przedziale czasu. Zostanie ona to wyświetlając pasek dla poszczególnych dni w raporcie hello. Na przykład wybranie hello okresie o nazwie "Ostatniego tygodnia" wygeneruje wykres słupkowy siedmiu pasków. Każdy pasek będzie wskazywać hello całkowita liczba trafień wystąpił w tym dniu.

Hello po lewej stronie powitania graph (oś y) wskazuje, ile razy na wystąpił hello określona data. Bezpośrednio pod hello graph (oś x), można znaleźć etykiety, która wskazuje datę hello (Format: RRRR-MM-DD) dla każdego dnia uwzględnionych w raporcie hello.

> [!TIP]
> Po umieszczeniu wskaźnika myszy nad paskiem hello łączna liczba trafień, które wystąpiły w tym dniu będzie wyświetlany jako etykietka narzędzia.
> 
> 

można wyświetlić dane Hello wykres słupkowy hello toogenerate używane poniżej. Można znaleźć hello łączna liczba trafień i hello ilość danych przesyłanych (w gigabajtach) dla każdego dnia objętego raportem hello.

## <a name="by-hour"></a>Według godzin
Witaj raportu przez godzinę umożliwia tooview hello łączna liczba trafień i danych przesyłanych w danej platformy na godzinę. Informacje te mogą być używane tooquickly wykrycia wzorce działania w sieci CDN. Na przykład ten raport ułatwia wykrywanie hello okresów w dniu hello, które występują wyższe lub niższe od oczekiwanego natężenia ruchu.

Podczas generowania raportu z tego typu, wykres słupkowy zawierają oznaczenie wizualne jako toohello ilość wystąpił co godzinę przez hello przedział czasu zdefiniowany przez raport hello żądanie specyficzne dla platformy. Zostanie ona to wyświetlając pasek dla każdej godziny objętego raportem hello. Na przykład wybranie 24-godzinnym przedziale czasu wygeneruje wykres słupkowy z paskami 24. Każdy pasek będzie wskazywać hello całkowita liczba trafień podczas danej godziny.

powitania po lewej stronie powitania graph (oś y) wskazuje, ile razy wystąpił na określoną godzinę hello. Bezpośrednio pod hello graph (oś x), można znaleźć etykietę wskazującą hello daty/godziny (Format: RRRR-MM-DD gg: mm) dla każdej godziny uwzględnionych w raporcie hello. Czas jest zgłaszany w formacie 24-godzinnym i zostanie określona, przy użyciu strefy czasowej UTC/GMT hello.

> [!TIP]
> Po umieszczeniu wskaźnika myszy nad paskiem hello łączna liczba trafień, które wystąpiły podczas tego godzinę będzie wyświetlany jako etykietka narzędzia.
> 
> 

można wyświetlić dane Hello wykres słupkowy hello toogenerate używane poniżej. Można znaleźć hello łączna liczba trafień i hello ilość danych przesyłanych (w gigabajtach) dla każdej godziny objętego raportem hello.

## <a name="by-file"></a>W pliku
Hello przez plik raport umożliwia możesz tooview hello ilość ruchu żądanie i hello poniesionych w konkretnej platformy dla hello najbardziej wymagane zasoby. Podczas generowania raportu z tego typu, wykres słupkowy zostanie wygenerowany na powitania top 10 najczęściej żądanych zasobów za pośrednictwem hello zdefiniowanym okresie.

> [!NOTE]
> Do celów hello tego raportu adresy URL CNAME krawędzi są adresy URL tootheir przekonwertowanego równoważne CDN. Dzięki temu dokładne rejestr dla hello łączna liczba trafień skojarzoną z zasobów, niezależnie od tego, czy hello CDN lub toorequest CNAME adres URL używany krawędzi.
> 
> 

powitania po lewej stronie powitania graph (oś y) wskazuje hello liczba żądań dla każdego elementu zawartości za pośrednictwem hello zdefiniowanym okresie. Bezpośrednio pod hello graph (oś x) można znaleźć etykietę wskazującą hello nazwę pliku dla każdego hello top 10 żądanych zasobów.

można wyświetlić dane Hello wykres słupkowy hello toogenerate używane poniżej. Można znaleźć hello następujące informacje dla każdego hello top 250 żądanych zasobów: ścieżki względnej, hello łączna liczba trafień, hello procent trafień, hello ilość danych przesyłanych (w gigabajtach) i procent hello przesyłane dane.

## <a name="by-file-detail"></a>Według szczegółów pliku
Witaj przez szczegółów pliku raportu umożliwia tooview hello ilość ruchu żądanie i hello poniesionych w konkretnej platformy dla określonego zasobu. Na powitania górze tego raportu jest hello szczegółów pliku dla opcji. Ta opcja zawiera listę najczęściej żądanych zasobów na powitania wybranej platformy. W kolejności toogenerate przez szczegółów pliku raportu konieczne będzie tooselect hello żądanego zasobu z hello szczegółów pliku dla opcji. Po upływie którego wykres słupkowy będzie wskazywać hello ilość dzienny popyt generowany przez hello zdefiniowanym okresie.

powitania po lewej stronie powitania graph (oś y) wskazuje hello całkowita liczba żądań, że zasób wystąpił w określonym dniu. Bezpośrednio pod hello graph (oś x), można znaleźć etykiety, która wskazuje datę hello (Format: RRRR-MM-DD) dla sieci CDN popytu na powitania zasobów został zgłoszony.

można wyświetlić dane Hello wykres słupkowy hello toogenerate używane poniżej. Można znaleźć hello łączna liczba trafień i hello ilość danych przesyłanych (w gigabajtach) dla każdego dnia objętego raportem hello.

## <a name="by-file-type"></a>Według typu pliku
Witaj raport według typu plików umożliwia możesz tooview hello ilość ruchu żądanie i hello poniesionych przez typ pliku. Podczas generowania raportu z tego typu, wykres pierścieniowy przedstawiający wskaże hello procent trafień generowane przez hello top 10 typy.

> [!TIP]
> Jeśli Aktywuj wycinek wykresu pierścień hello, hello Internet typ nośnika czy typ pliku będzie wyświetlany jako etykietka narzędzia.
> 
> 

można wyświetlić dane Hello wykres pierścieniowy przedstawiający hello toogenerate używane poniżej. Będzie Znajdź typ nośnika hello pliku nazwa rozszerzenia/Internet, hello łączna liczba trafień, hello procent trafień, hello ilość danych przesyłanych (w gigabajtach), a hello odsetek danych przesyłanych dla każdego hello top 250 typów plików.

## <a name="by-directory"></a>Za pomocą katalogu
Raport przez katalog Hello umożliwia tooview hello ilość ruchu żądanie i hello poniesionych w danej platformy na zawartość z określonego katalogu. Podczas generowania raportu z tego typu, wykres słupkowy wskaże hello całkowita liczba trafień generowane przez zawartość w katalogach 10 top hello.

### <a name="using-hello-bar-chart"></a>Przy użyciu hello wykres słupkowy
* Umieść kursor nad paskiem tooview hello ścieżki względnej toohello odpowiedni katalog.
* Zawartości przechowywanej w podfolderze katalogu nie będą uwzględniane podczas obliczania żądanie za pomocą katalogu. Obliczona w ten sposób wykorzystuje wyłącznie hello liczby generowanych dla zawartości przechowywanej w katalogu rzeczywiste hello.
* Do celów hello tego raportu adresy URL CNAME krawędzi są adresy URL tootheir przekonwertowanego równoważne CDN. Dzięki temu dokładne zgadzają się dla wszystkich statystyk skojarzoną z zasobów, niezależnie od tego, czy hello CDN lub toorequest CNAME adres URL używany krawędzi.

Witaj po lewej stronie powitania graph (oś y) wskazuje hello całkowita liczba żądań dotyczących zawartości hello przechowywanych w katalogach 10 top. Każdy słupek na wykresie hello reprezentuje katalog. Użyj hello kolorami toomatch schemat się pasek katalogu tooa wymienionych w sekcji górnej 250 pełne katalogów hello.

można wyświetlić dane Hello wykres słupkowy hello toogenerate używane poniżej. Można znaleźć hello następujące informacje dla każdego hello top 250 katalogów: ścieżki względnej, hello łączna liczba trafień, hello procent trafień, hello ilość danych przesyłanych (w gigabajtach) i procent hello przesyłane dane.

## <a name="by-browser"></a>W przeglądarce
Witaj przez przeglądarki raportów umożliwia tooview przeglądarek, które były używane toorequest zawartości. Podczas generowania raportu z tego typu, wykres kołowy wskaże hello odsetek żądań obsłużonych przez hello najpopularniejsze 10 przeglądarki.

### <a name="using-hello-pie-chart"></a>Przy użyciu wykresu kołowego hello
* Umieść kursor nad wycinek tooview wykresu kołowego hello przeglądarki nazwę i wersję.
* Do celów hello tego raportu każda kombinacja unikatowe przeglądarki/wersja jest traktowany jako innej przeglądarki.
* wycinek Hello o nazwie "Inne" wskazuje hello odsetek żądań obsłużonych przez wszystkie przeglądarki i wersje.

można wyświetlić dane Hello wykresu kołowego hello toogenerate używane poniżej. Można znaleźć hello przeglądarki typu i wersji numer, łączna liczba trafień hello i hello procent trafień dla każdego hello najpopularniejsze 250 przeglądarki.

## <a name="by-referrer"></a>Według odwołania
Witaj raport według odwołania umożliwia tooview hello najczęstsze toocontent hello wybranej platformy. Odwołania wskazuje hello nazwy hosta, na którym żądanie zostało wygenerowane. Podczas generowania raportu z tego typu, wykres słupkowy wskazuje ilość hello żądanie (tj. liczba trafień) generowany przez hello najczęstsze 10.

Lewa strona Hello hello wykresu (oś y) wskazuje hello całkowita liczba żądań, że zasób wystąpił dla każdego odwołania. Każdy słupek na wykresie hello reprezentuje odwołania. Użyj hello kolorami toomatch schemat się pasek odwołania tooa wymienionych w sekcji odwołania 250 Top hello.

można wyświetlić dane Hello wykres słupkowy hello toogenerate używane poniżej. Można znaleźć hello adres URL, łączna liczba trafień hello i hello procent trafień wygenerowane z każdej hello najczęstsze 250.

## <a name="by-download"></a>Do pobrania
Witaj pobierany raportu umożliwia tooanalyze wzorce pobierania najbardziej żądanej zawartości. Witaj początku hello raportu zawiera wykres słupkowy, że nastąpiła porównuje pliki do pobrania z pobrania zakończone dla hello pierwszych 10 żądanych zasobów. Każdy pasek jest oznaczone kolorami, zgodnie z toowhether jest próba pobrania (niebieski) lub Pobieranie ukończone (zielony).

> [!NOTE]
> Do celów hello tego raportu adresy URL CNAME krawędzi są adresy URL tootheir przekonwertowanego równoważne CDN. Dzięki temu dokładne zgadzają się dla wszystkich statystyk skojarzoną z zasobów, niezależnie od tego, czy hello CDN lub toorequest CNAME adres URL używany krawędzi.
> 
> 

powitania po lewej stronie powitania graph (oś y) wskazuje hello nazwę pliku dla każdego hello top 10 żądanych zasobów. Bezpośrednio pod hello graph (oś x) można znaleźć etykiet wskazujących hello całkowitą liczbę pobrań podjęto ukończone.

Bezpośrednio poniżej hello wykres słupkowy, hello następujące informacje zostaną wyświetlone hello top 250 żądanych zasobów: ścieżka względna (takie jak nazwa pliku), hello liczbę razy, które było toocompletion pobrany, hello liczbę jej żądanie zostało przesłane i hello Procent żądań, które spowodowało ukończenia pobierania.

> [!TIP]
> Nasze CDN nie otrzymuje informacji przez klienta protokołu HTTP (tj. przeglądarki) gdy zasób został całkowicie pobrany. W związku z tym mamy toocalculate czy zasób całkowitym pobraniu zgodnie z kodów toostatus i żądania zakresu bajtów. Witaj po pierwsze szukamy podczas wprowadzania tego obliczenia jest Określa, czy Żądanie hello powoduje w kodzie 200 OK stanu. Jeśli tak, możemy Przyjrzyj się tooensure żądania zakresu bajtów dotyczą całej zawartości hello. Na koniec mamy porównać hello ilość danych przesyłanych toohello rozmiar żądanych zasobów hello. Jeśli hello dane przesyłane jest większy niż rozmiar pliku hello równy tooor i żądania zakresu bajtów hello są odpowiednie dla tego zasobu, trafień hello będą liczone jako zakończenie pobierania.
> 
> Powodu toohello interpretive charakter tego raportu należy mieć na powitania uwadze następujące punkty, które nie może zmienić spójności hello dokładność tego raportu.
> 
> * Wzorce ruchu nie można dokładnie przewidzieć, gdy agenci użytkownika zachowywać się inaczej. Może to powodować wyniki pobierania zakończonych, które są większe niż 100%.
> * Zasoby, które korzystają z pobierania progresywnego HTTP nie może być dokładnie reprezentowany przez ten raport. Jest to powodu toousers wyszukiwania toodifferent pozycji w pliku wideo.
> 
> 

## <a name="by-404-errors"></a>Z powodu błędów 404
Witaj raport według błędów 404 umożliwia tooidentify hello typu zawartości, które generuje hello najbardziej liczba kodów stanu 404 Nie znaleziono. Witaj początku hello raportu zawiera wykres słupkowy hello 10 pierwszych zasobów, dla których został zwrócony kod stanu nie znaleziono 404. Ten wykres słupkowy porównuje hello całkowita liczba żądań z żądaniami, które spowodowało 404 Nie odnaleziono kodu stanu tych zasobów. Każdy pasek jest oznaczone kolorami. Żółty pasek służy tooindicate, który hello żądanie spowodowało 404 Nie odnaleziono kodu stanu. Czerwony pasek służy tooindicate hello całkowita liczba żądań hello trwałego.

> [!NOTE]
> Do celów hello tego raportu należy zwrócić uwagę hello następujące:
> 
> * Trafienie reprezentuje wszystkie żądania dla zasobów, niezależnie od tego, kod stanu.
> * Adresy URL CNAME krawędzi są adresy URL tootheir przekonwertowanego równoważne CDN. Dzięki temu dokładne zgadzają się dla wszystkich statystyk skojarzoną z zasobów, niezależnie od tego, czy hello CDN lub toorequest CNAME adres URL używany krawędzi.
> 
> 

powitania po lewej stronie powitania graph (oś y) wskazuje hello nazwę pliku dla każdego hello top 10 żądanych zasobów, które spowodowało 404 Nie odnaleziono kodu stanu. Bezpośrednio pod hello graph (oś x) można znaleźć etykiet wskazujących hello całkowita liczba żądań i hello liczba żądań, które wywołały kod stanu nie znaleziono 404.

Bezpośrednio poniżej hello wykres słupkowy, hello następujące informacje zostaną wyświetlone hello top 250 żądanych zasobów: został hello liczba żądań, które spowodowały 404 Nie odnaleziono kodu stanu, hello łączna liczba uruchomień hello zasobów ścieżki względnej (takie jak nazwa pliku) żądanie i hello odsetek żądań, które spowodowało 404 Nie odnaleziono kodu stanu.

## <a name="see-also"></a>Zobacz też
* [Omówienie usługi Azure CDN](cdn-overview.md)
* [Statystyki w czasie rzeczywistym w usłudze Microsoft Azure CDN](cdn-real-time-stats.md)
* [Zastępowanie domyślnego zachowania HTTP przy użyciu aparatu reguł hello](cdn-rules-engine.md)
* [Analizowanie wydajności](cdn-edge-performance.md)

