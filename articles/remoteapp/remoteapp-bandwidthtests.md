---
title: "aaaAzure RemoteApp — użycie przepustowości sieci z niektórych typowych scenariuszy testowania | Dokumentacja firmy Microsoft"
description: "Dowiedz się więcej o typowe scenariusze użycia, które mogą pomóc ustalić potrzeb przepustowości sieci usługi Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 06417c75-0c63-4ecf-b9d1-66a7af6b7b91
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 22c1dbb61d956d58d01eb4e11363266168e337e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-remoteapp---testing-your-network-bandwidth-usage-with-some-common-scenarios"></a>Usługa Azure RemoteApp — użycie przepustowości sieci z niektórych typowych scenariuszy testowania
> [!IMPORTANT]
> Usługa Azure RemoteApp nie będzie obsługiwana od 31 sierpnia 2017 r. Witaj odczytu [anonsu](https://go.microsoft.com/fwlink/?linkid=821148) szczegółowe informacje.
> 
> 

Jak wspomniano w [wykorzystanie przepustowości sieci usługi Azure RemoteApp szacowania](remoteapp-bandwidth.md), hello najlepsze toofigure sposób w jaki wpływ hello sieci tooyour usługi Azure RemoteApp jest toorun niektórych testów użycia. Uruchom testy dla zestawu czasu okresu i miary hello przepustowości wymagane dla każdego scenariusza. Jeśli masz możliwość hello, można również zastosować miary hello sieci pakietów utraty i sieci zakłócenia toounderstand hello sieci wzorców, które zostaną utworzone w całym środowisku.

Podczas obliczania hello przepustowości, należy pamiętać, że użycie różni się między różnymi użytkownikami w obrębie firmy. Na przykład czytników tekstu oraz zapisywania zwykle używać mniejszej przepustowości od użytkowników, które współpracują z wideo. Aby uzyskać najlepsze wyniki bada potrzeb użytkowników i utworzyć kombinację hello następujące scenariusze, które najlepiej informują hello użytkowników w firmie. Pamiętaj zbyt[wystąpić przeglądu hello czynników, które mają wpływ na wykorzystanie przepustowości i użytkownika](remoteapp-bandwidthexperience.md) — która ułatwi identyfikowanie hello idealne testy.

Najpierw przeczytać temat hello testy, wybierz użytkownika mieszanego, a następnie uruchom je. Można użyć tabeli hello poniżej toohelp śledzenie wydajności.

> [!NOTE]
> Jeśli nie własnego testowania sieci lub nie masz toodo czasu hello tak, zapoznaj się naszego [przepustowość sieci podstawowej szacuje/zalecenia](remoteapp-bandwidthguidelines.md). Przebieg może się różnić, dlatego jeśli użytkownik *można* uruchamiać własne testy, wykonaj następujące czynności.
> 
> 

## <a name="hello-usage-tests"></a>Witaj użycia testów
Tych testów dla różnych okresach czasu i testować różne funkcje/funkcje, które korzystać z przepustowości sieci. Należy pamiętać, toochoose hello mieszanki testów, który najlepiej odpowiada indywidualnych użytkowników.

### <a name="executivecomplex-powerpoint---run-for-900-1000-seconds"></a>PowerPoint wykonawczego/złożone — Uruchom sekund 900 – 1000
Użytkownik przedstawia między 45 50 o wysokiej wierności slajdów za pomocą programu Microsoft Office PowerPoint w trybie pełnoekranowym. slajdów Hello powinien zawierać obrazów, przejścia (z animacji) i z kolor gradientu tła, które są typowe dla Twojej firmy. Hello użytkownika należy przeznaczyć co najmniej 20 sekund na każdego slajdu.

Ten scenariusz tworzy ruchem seryjnym toohello dalej slajd z prezentacji hello przejścia slajdów.

### <a name="simple-powerpoint---run-for-620-seconds"></a>Proste PowerPoint — uruchom ~ 620 sekund
Użytkownik przedstawia prostego pliku PowerPoint z około 30 slajdów za pomocą programu Microsoft Office PowerPoint w trybie pełnoekranowym. slajdów Hello więcej tekstu CPU niż w scenariuszu PowerPoint wykonawczego/złożone hello oraz prostsze tła i obrazów (diagramy czarny). 

### <a name="internet-explorer---run-for-250-seconds"></a>Internet Explorer — Uruchom ~ 250 sekund
Użytkownik przejdzie hello sieci web w programie Internet Explorer. Użytkownik Hello przegląda i przewija kombinacji tekst, obrazy fizyczną i niektóre diagramów schematów. Witaj przechowywane na powitania lokalnym dysku twardym powitania serwera hosta sesji usług pulpitu zdalnego (Host sesji usług pulpitu zdalnego) jako stron sieci web. Plik MHT. Witaj użytkownik przewinie, przy użyciu Page Up, Page Down, w górę i w dół kluczy, z różnych interwałów dla każdego klucza/typu przewijania:

    - Dół - 250 naciśnięcia klawiszy bardzo 500 ms
    - Page Up - 36 naciśnięcia klawiszy co 1000 ms
    - W dół - 75 naciśnięcia klawiszy co 100 ms
    - Page Down - 20 naciśnięcia klawiszy co 500 ms
    - W górę - 120 naciśnięcia klawiszy co 300 ms

### <a name="pdf-document---simple---run-for-610-seconds"></a>Dokument PDF — prosty — Uruchom ~ 610 sekund
Użytkownik odczytuje i wyszukuje dokumentu PDF na różne sposoby, za pomocą programu Adobe Acrobat Reader. dokument Hello powinien składać się z tabel, wykresy proste i wielu czcionki tekstu. dokument Hello jest 35 40 stron długo. Użytkownik Hello do przewijania w dwóch różnych stawek, Wstecz i przekazuje w czterech powiększenia różnych rozmiarach (dopasowania toopage, dopasowania toowidth 100%, a druga wybrane). Powiększanie Hello gwarantuje, że tekst hello (czcionki) renderowania w różnych rozmiarach. Przewijanie jest wyłączony przy użyciu hello Page Up, Page Down, w górę i w dół kluczy, z różnych interwałów dla każdego przewijania.

### <a name="pdf-document---mixed---run-for-320-seconds"></a>-Mieszane — Uruchom ~ 320 sekund dokumentu PDF
Użytkownik odczytuje i wyszukuje dokumentu PDF na różne sposoby, za pomocą programu Adobe Acrobat Reader. dokument Hello zawiera wysokiej jakości obrazów (w tym zdjęcia), tabel, wykresy proste i wielu czcionki tekstu. Użytkownik Hello do przewijania w dwóch różnych stawek, Wstecz i przekazuje w czterech powiększenia różnych rozmiarach (dopasowania toopage, dopasowania toowidth 100%, a druga wybrane). Powiększanie Hello gwarantuje, że tekst hello (czcionki) renderowania w różnych rozmiarach. Przewijanie jest wyłączony przy użyciu hello Page Up, Page Down, w górę i w dół kluczy, z różnych interwałów dla każdego przewijania.

### <a name="flash-video-playback---run-for-180-seconds"></a>Odtwarzanie wideo Flash — Uruchom ~ 180 sekund
Użytkownik wyświetla wideo Adobe Flash kodowany w formacie osadzonego w stronie sieci web. strony sieci web Hello jest przechowywany w lokalnym dysku twardym powitania powitania serwera hosta sesji usług pulpitu zdalnego. Witaj wideo jest odtwarzany w programie Internet Explorer przez osadzony player wtyczki.

W tym scenariuszu emuluje użytkownikom sformatowanego zawartości stron sieci web zawierających multimediów. Większość danych hello powinien bo za pośrednictwem VOBR.

### <a name="word-remote-typing---run-for-1800-seconds"></a>Word, wpisując zdalnego — uruchom ~ 1800 sekund
Użytkownik wpisze dokumentu za pośrednictwem sesji protokołu RDP. Są one wysyłane z powitania po stronie klienta za pośrednictwem hello RDP sesji tooa dokument w programie Microsoft Word uruchomione w sesji zdalnej hello. Witaj, wpisując szybkość jest jeden znak co 250 ms (całkowita liczba znaków 7050). 

To jest jednym z najbardziej typowych scenariuszy hello pracownika wiedzy. W tym scenariuszu testy hello reakcji użytkownika, wpisując procesora nowoczesnych pracy. Ten scenariusz jest poufnych tooeven niewielkich zmian w użycia przepustowości.

## <a name="tracking-hello-test-results"></a>Wyniki testu hello śledzenia
Możesz użyć hello następujące scenariusze hello tooevaluate tabeli w danym środowisku. podane poniżej dane Hello jest tylko do celów informacyjnych — może być znacznie inne, niż można zaobserwować. 

Dla uproszczenia przyjęto założenie, że przy użyciu rozdzielczość ekranu hello tego samego 1920 x 1080 pikseli, sprawdzane są wszystkie scenariusze i zakłóceń transportu TCP w sieci z opóźnieniem (opóźnienie) poniżej 200 ms i sieci w hello 120 ms + znak około 1%.

O hello tabeli:

* **Średni środowisko** zawiera hello przepustowość sieci, gdy nie ma znacznie wpływu na wydajność pracy użytkownika, ale nie wyklucza okazjonalne błędami występującymi wideo lub audio. Hello system jest toorecover może szybko dzięki wykorzystaniu logiki dynamiczne hello. Witaj przepustowości szacuje próba tooguarantee hello jakości sieci hello środowisko użytkownika.
  * **Zauważalne problemów (punkt przerwania)** zawiera hello przepustowość sieci, gdzie użytkownicy mogą zauważyć istotne problemy w ich środowisku, a ich wydajność. dotyczy to wymierne okresów. W tym momencie hello RDP algorytmy są klienci i nie może zagwarantować użytkownika hello jakości obsługi z powodu niewystarczających przepustowości.
  * **Zalecane** zawiera hello przepustowość sieci zalecane w przypadku dobrej lub doskonałe środowisko. Jest wyższa niż wartość hello odpowiadającego hello zwykle jeden krok **średni środowisko** kolumny.
  * **Informacje o** obejmują uwag i komentarzy.

| Testowanie | Środowisko średni | Zauważalne problemów (punkt przerwania) | Przepustowość sieci zalecane | Uwagi |
| --- | --- | --- | --- | --- |
| PPT wykonawczego/złożone |10 MB/s |1 MB/s |> 10 MB/s, 100 MB/s preferowane |1 MB/s wiele animacji zostaną utracone |
| Proste PPT |5 MB/s |256 KB/s |10 MB/s |256 KB/s slajdów hello załadować z opóźnieniem zauważalne |
| Program Internet Explorer |10 MB/s |1 MB/s |> 10 MB/s, 100 MB/s preferowane |1 MB/s rozmyte są filmy wideo w sieci web i zniekształcony, szybkie przewijanie występują problemy |
| Proste PDF |1 MB/s |256 KB/s |5 MB/s |256 KB/s zajmie trochę czasu tooload hello strony |
| Mieszane PDF |1 MB/s |256 KB/s |5 MB/s |W 256 KB/s strony hello wykonuje znaczną ilość czasu tooload |
| Flash odtwarzania wideo. |10 MB/s |1 MB/s |> 10 MB/s, 100 MB/s preferowane |1 MB/s jest ziarnisty hello wideo i niektóre ramki są usuwane. |
| Wpisywanie zdalnego w programie Word |256 KB/s |128 KB/s |1 MB/s |256 KB/s użytkownika mogą pojawić się hello czas między naciśnięcia klawiszy |

przepustowość sieci hello tooevaluate dla poszczególnych użytkowników, Utwórz kombinację hello powyżej scenariuszy i hello odpowiedni udział przepustowości wymagane. Wybierz najwyższy numer hello potrzebne dla scenariuszy. Ponieważ użytkownicy prawie nigdy nie używaj systemu hello samodzielnie, należy wziąć pod uwagę pewne rezerwy dla użytkowników, którzy jednocześnie na pracy hello tej samej sieci.

## <a name="learn-more"></a>Dowiedz się więcej
* [Szacowanie użycia przepustowości sieci usługi Azure RemoteApp](remoteapp-bandwidth.md)
* [Usługa Azure RemoteApp — jak przepustowości sieci i jakości środowisko pracy ze sobą?](remoteapp-bandwidthexperience.md)
* [Azure RemoteApp przepustowość sieci — ogólne wytyczne (Jeśli użytkownik nie może przetestować własnych)](remoteapp-bandwidthguidelines.md)

