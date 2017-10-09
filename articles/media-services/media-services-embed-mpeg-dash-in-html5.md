---
title: "aaaEmbedding MPEG-DASH adaptacyjne przesyłanie strumieniowe wideo w aplikacji HTML5 z DASH.js | Dokumentacja firmy Microsoft"
description: "W tym temacie przedstawiono sposób tooembed MPEG-DASH adaptacyjne przesyłanie strumieniowe wideo w aplikacji HTML5 z DASH.js."
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 5aa0e7b6-f5c3-4cc1-aa33-ed16ea4780c2
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/26/2016
ms.author: juliako
ms.openlocfilehash: a73713d20f95262654532b94576ae9669d829354
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="embedding-a-mpeg-dash-adaptive-streaming-video-in-an-html5-application-with-dashjs"></a>Osadzania wideo adaptacyjnego przesyłania strumieniowego MPEG-DASH w aplikacji HTML5 z DASH.js
## <a name="overview"></a>Omówienie
MPEG-DASH jest standardem ISO hello adaptacyjne przesyłanie strumieniowe zawartości wideo, która oferuje istotne korzyści dla tych, którzy chcą wideo wysokiej jakości, adaptacyjną toodeliver strumienia wyjściowego. Z MPEG-DASH strumienia wideo o hello automatycznie porzuca tooa definicji niższe, gdy hello sieć jest przeciążona. Zmniejsza to prawdopodobieństwo hello podglądu hello wyświetlanie "Wstrzymano" wideo, gdy odtwarzacz hello hello pobiera obok kilka tooplay sekund (alias buforowania). Ponieważ zmniejsza przeciążenie sieci, hello odtwarzacza wideo z kolei zwróci tooa wyższej jakości strumienia. Ta możliwość tooadapt hello przepustowość wymagana powoduje również skrócić czas rozpoczęcia wideo. Oznacza, że hello pierwszych kilku sekund można odtworzyć w segmencie jakości niższe fast do pobierania i następnie uaktualnić tooa wyższej jakości po wystarczającej zawartości została buforowana.

Dash.js jest typu open source MPEG-DASH odtwarzacza wideo napisane w języku JavaScript. Jego celem jest tooprovide odtwarzacz niezawodne, między platformami, który może nastąpić za darmo w aplikacjach, które wymagają odtwarzania wideo. Zapewnia odtwarzanie MPEG-DASH w dowolnej przeglądarki obsługującej hello W3C nośnika źródłowego rozszerzenia (MSE), czyli dzisiaj Chrome, Microsoft Edge i IE11 (innych przeglądarek wskazał, ich konwersji toosupport MSE). Aby uzyskać więcej informacji na temat DASH.js js Zobacz hello GitHub dash.js repozytorium.

## <a name="creating-a-browser-based-streaming-video-player"></a>Tworzenie przeglądarki przesyłania strumieniowego odtwarzacza wideo
Formanty toocreate prosta strona sieci web, która wyświetla odtwarzacza wideo z hello oczekiwano takiego play, Wstrzymaj, przewiń itp., konieczne będzie:

1. Tworzenie strony HTML
2. Dodaj tag wideo hello
3. Dodaj hello dash.js player
4. Inicjowanie hello player
5. Dodaj niektórych stylu CSS
6. Wyświetl wyniki hello w przeglądarce, która implementuje MSE

Inicjowanie player hello mogą być wykonywane w kilku wierszach kodu JavaScript. Przy użyciu dash.js, naprawdę to proste tooembed MPEG-DASH wideo w aplikacjach opartych na przeglądarce.

## <a name="creating-hello-html-page"></a>Tworzenie hello strony HTML
pierwszym krokiem Hello jest strona toocreate standardowego kodu HTML zawierający hello **wideo** elementu, Zapisz ten plik jako basicPlayer.html jako hello poniższy przykład przedstawia:

    <!DOCTYPE html>
    <html>
      <head><title>Adaptive Streaming in HTML5</title></head>
      <body>
        <h1>Adaptive Streaming with HTML5</h1>
        <video id="videoplayer" controls></video>
      </body>
    </html>

## <a name="adding-hello-dashjs-player"></a>Dodawanie hello DASH.js Player
tooadd hello dash.js odwołanie do implementacji toohello aplikacji, musisz toograb hello dash.all.js pliku w wersji hello 1.0 dash.js projektu. Powinna to być zapisane w folderze JavaScript hello aplikacji. Ten plik jest plikiem wygody, ściągający cały kod niezbędne dash.js hello w jednym pliku w razem. Jeśli masz wyszukiwania wokół repozytorium dash.js hello będzie Znajdź hello pojedyncze pliki, testowania kodu i wiele innych, ale jeśli wszystkie toodo jest dash.js Użyj, a następnie plik dash.all.js hello jest, co jest potrzebne.

tooadd hello dash.js player tooyour aplikacje, Dodaj skrypt tag toohello head sekcję basicPlayer.html:

    <!-- DASH-AVC/265 reference implementation -->
    < script src="js/dash.all.js"></script>


Następnie należy utworzyć odtwarzacza hello tooinitialize funkcji podczas ładowania strony hello. Dodaj następujące skryptu po wierszu hello załadować dash.all.js hello:

    <script>
    // setup hello video element and attach it toohello Dash player
    function setupVideo() {
      var url = "http://wams.edgesuite.net/media/MPTExpressionData02/BigBuckBunny_1080p24_IYUV_2ch.ism/manifest(format=mpd-time-csf)";
      var context = new Dash.di.DashContext();
      var player = new MediaPlayer(context);
                      player.startup();
                      player.attachView(document.querySelector("#videoplayer"));
                      player.attachSource(url);
    }
    </script>

Ta funkcja najpierw tworzy DashContext. To jest aplikacja hello tooconfigure używane dla określonego środowiska. Z technicznego punktu widzenia definiuje powitalne podczas tworzenia aplikacji hello należy używać klas, które hello framework iniekcji zależności. W większości przypadków będzie używany Dash.di.DashContext.

Następnie można utworzyć wystąpienia hello klasy podstawowej struktury dash.js hello, MediaPlayer. Ta klasa zawiera podstawowe hello metody takie jak odtwarzanie i wstrzymywanie, zarządza hello relacji z elementem wideo hello i zarządza także interpretacji hello hello opis prezentacji nośnika (MPD) pliku, który opisuje hello toobe wideo odtwarzane.

Funkcja startup() Hello hello MediaPlayer klasy jest nazywany tooensure tego player hello jest gotowy tooplay wideo. Między innymi tej funkcji powoduje, że wszystkie niezbędne klasy hello (zgodnie z definicją w kontekście hello) zostały załadowane. Gdy hello player jest gotowy, możesz dołączyć hello tooit element wideo przy użyciu funkcji attachView() hello. Włącza hello MediaPlayer tooinject hello strumienia wideo o do elementu hello, a także sterować odtwarzania w razie potrzeby.

Przekaż hello adres URL hello MPD pliku toohello MediaPlayer tak, aby go zna hello wideo oczekuje się, funkcja setupVideo() tooplay.hello właśnie utworzony należy toobe wykonywane po stronie powitania pełni został załadowany. W tym celu za pomocą zdarzenia onload hello hello treści elementu. Zmień Twoje <body> elementu:

    <body onload="setupVideo()">

Wreszcie Ustaw rozmiar hello hello elementu wideo za pomocą CSS. W środowisku adaptacyjnego przesyłania strumieniowego jest to szczególnie ważne, ponieważ rozmiar hello hello odtwarzania wideo może zmienić odtwarzania dostosowuje się warunków sieciowych toochanging. W tym prosty pokaz po prostu wymusić hello wideo element toobe 80% okna przeglądarki dostępne hello przez dodanie powitania po CSS toohello sekcji head hello strony:

    <style>
    video {
      width: 80%;
      height: 80%;
    }
    </style>

## <a name="playing-a-video"></a>Odtwarzanie wideo
tooplay wideo, wskazać w przeglądarce hello basicPlayback.html plik i kliknij przycisk play na powitania odtwarzacza wideo wyświetlane.

## <a name="media-services-learning-paths"></a>Ścieżki szkoleniowe dotyczące usługi Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Przekazywanie opinii
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>Zobacz też
[Opracowywanie aplikacji odtwarzacza wideo](media-services-develop-video-players.md)

[Repozytorium GitHub dash.js](https://github.com/Dash-Industry-Forum/dash.js) 

