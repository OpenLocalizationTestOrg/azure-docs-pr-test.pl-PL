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
# <a name="embedding-a-mpeg-dash-adaptive-streaming-video-in-an-html5-application-with-dashjs"></a><span data-ttu-id="accbf-103">Osadzania wideo adaptacyjnego przesyłania strumieniowego MPEG-DASH w aplikacji HTML5 z DASH.js</span><span class="sxs-lookup"><span data-stu-id="accbf-103">Embedding a MPEG-DASH Adaptive Streaming Video in an HTML5 Application with DASH.js</span></span>
## <a name="overview"></a><span data-ttu-id="accbf-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="accbf-104">Overview</span></span>
<span data-ttu-id="accbf-105">MPEG-DASH jest standardem ISO hello adaptacyjne przesyłanie strumieniowe zawartości wideo, która oferuje istotne korzyści dla tych, którzy chcą wideo wysokiej jakości, adaptacyjną toodeliver strumienia wyjściowego.</span><span class="sxs-lookup"><span data-stu-id="accbf-105">MPEG-DASH is an ISO standard for hello adaptive streaming of video content, which offers significant benefits for those who wish toodeliver high-quality, adaptive video streaming output.</span></span> <span data-ttu-id="accbf-106">Z MPEG-DASH strumienia wideo o hello automatycznie porzuca tooa definicji niższe, gdy hello sieć jest przeciążona.</span><span class="sxs-lookup"><span data-stu-id="accbf-106">With MPEG-DASH, hello video stream will automatically drop tooa lower definition when hello network becomes congested.</span></span> <span data-ttu-id="accbf-107">Zmniejsza to prawdopodobieństwo hello podglądu hello wyświetlanie "Wstrzymano" wideo, gdy odtwarzacz hello hello pobiera obok kilka tooplay sekund (alias buforowania).</span><span class="sxs-lookup"><span data-stu-id="accbf-107">This reduces hello likelihood of hello viewer seeing a "paused" video while hello player downloads hello next few seconds tooplay (aka buffering).</span></span> <span data-ttu-id="accbf-108">Ponieważ zmniejsza przeciążenie sieci, hello odtwarzacza wideo z kolei zwróci tooa wyższej jakości strumienia.</span><span class="sxs-lookup"><span data-stu-id="accbf-108">As network congestion reduces, hello video player will in turn return tooa higher quality stream.</span></span> <span data-ttu-id="accbf-109">Ta możliwość tooadapt hello przepustowość wymagana powoduje również skrócić czas rozpoczęcia wideo.</span><span class="sxs-lookup"><span data-stu-id="accbf-109">This ability tooadapt hello bandwidth required also results in a faster start time for video.</span></span> <span data-ttu-id="accbf-110">Oznacza, że hello pierwszych kilku sekund można odtworzyć w segmencie jakości niższe fast do pobierania i następnie uaktualnić tooa wyższej jakości po wystarczającej zawartości została buforowana.</span><span class="sxs-lookup"><span data-stu-id="accbf-110">That means that hello first few seconds can be played in a fast-to-download lower quality segment and then step up tooa higher quality once sufficient content has been buffered.</span></span>

<span data-ttu-id="accbf-111">Dash.js jest typu open source MPEG-DASH odtwarzacza wideo napisane w języku JavaScript.</span><span class="sxs-lookup"><span data-stu-id="accbf-111">Dash.js is an open source MPEG-DASH video player written in JavaScript.</span></span> <span data-ttu-id="accbf-112">Jego celem jest tooprovide odtwarzacz niezawodne, między platformami, który może nastąpić za darmo w aplikacjach, które wymagają odtwarzania wideo.</span><span class="sxs-lookup"><span data-stu-id="accbf-112">Its goal is tooprovide a robust, cross-platform player that can be freely reused in applications that require video playback.</span></span> <span data-ttu-id="accbf-113">Zapewnia odtwarzanie MPEG-DASH w dowolnej przeglądarki obsługującej hello W3C nośnika źródłowego rozszerzenia (MSE), czyli dzisiaj Chrome, Microsoft Edge i IE11 (innych przeglądarek wskazał, ich konwersji toosupport MSE).</span><span class="sxs-lookup"><span data-stu-id="accbf-113">It provides MPEG-DASH playback in any browser that supports hello W3C Media Source Extensions (MSE), today that is Chrome, Microsoft Edge and IE11 (other browsers have indicated their intent toosupport MSE).</span></span> <span data-ttu-id="accbf-114">Aby uzyskać więcej informacji na temat DASH.js js Zobacz hello GitHub dash.js repozytorium.</span><span class="sxs-lookup"><span data-stu-id="accbf-114">For more information about DASH.js, js see hello GitHub dash.js repository.</span></span>

## <a name="creating-a-browser-based-streaming-video-player"></a><span data-ttu-id="accbf-115">Tworzenie przeglądarki przesyłania strumieniowego odtwarzacza wideo</span><span class="sxs-lookup"><span data-stu-id="accbf-115">Creating a browser-based streaming video player</span></span>
<span data-ttu-id="accbf-116">Formanty toocreate prosta strona sieci web, która wyświetla odtwarzacza wideo z hello oczekiwano takiego play, Wstrzymaj, przewiń itp., konieczne będzie:</span><span class="sxs-lookup"><span data-stu-id="accbf-116">toocreate a simple web page that displays a video player with hello expected controls such a play, pause, rewind etc., you will need to:</span></span>

1. <span data-ttu-id="accbf-117">Tworzenie strony HTML</span><span class="sxs-lookup"><span data-stu-id="accbf-117">Create an HTML page</span></span>
2. <span data-ttu-id="accbf-118">Dodaj tag wideo hello</span><span class="sxs-lookup"><span data-stu-id="accbf-118">Add hello video tag</span></span>
3. <span data-ttu-id="accbf-119">Dodaj hello dash.js player</span><span class="sxs-lookup"><span data-stu-id="accbf-119">Add hello dash.js player</span></span>
4. <span data-ttu-id="accbf-120">Inicjowanie hello player</span><span class="sxs-lookup"><span data-stu-id="accbf-120">Initialize hello player</span></span>
5. <span data-ttu-id="accbf-121">Dodaj niektórych stylu CSS</span><span class="sxs-lookup"><span data-stu-id="accbf-121">Add some CSS style</span></span>
6. <span data-ttu-id="accbf-122">Wyświetl wyniki hello w przeglądarce, która implementuje MSE</span><span class="sxs-lookup"><span data-stu-id="accbf-122">View hello results in a browser that implements MSE</span></span>

<span data-ttu-id="accbf-123">Inicjowanie player hello mogą być wykonywane w kilku wierszach kodu JavaScript.</span><span class="sxs-lookup"><span data-stu-id="accbf-123">Initializing hello player can be completed in just a handful of lines of JavaScript code.</span></span> <span data-ttu-id="accbf-124">Przy użyciu dash.js, naprawdę to proste tooembed MPEG-DASH wideo w aplikacjach opartych na przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="accbf-124">Using dash.js, it really is that simple tooembed MPEG-DASH video in your browser based applications.</span></span>

## <a name="creating-hello-html-page"></a><span data-ttu-id="accbf-125">Tworzenie hello strony HTML</span><span class="sxs-lookup"><span data-stu-id="accbf-125">Creating hello HTML Page</span></span>
<span data-ttu-id="accbf-126">pierwszym krokiem Hello jest strona toocreate standardowego kodu HTML zawierający hello **wideo** elementu, Zapisz ten plik jako basicPlayer.html jako hello poniższy przykład przedstawia:</span><span class="sxs-lookup"><span data-stu-id="accbf-126">hello first step is toocreate a standard HTML page containing hello **video** element, save this file as basicPlayer.html, as hello following example illustrates:</span></span>

    <!DOCTYPE html>
    <html>
      <head><title>Adaptive Streaming in HTML5</title></head>
      <body>
        <h1>Adaptive Streaming with HTML5</h1>
        <video id="videoplayer" controls></video>
      </body>
    </html>

## <a name="adding-hello-dashjs-player"></a><span data-ttu-id="accbf-127">Dodawanie hello DASH.js Player</span><span class="sxs-lookup"><span data-stu-id="accbf-127">Adding hello DASH.js Player</span></span>
<span data-ttu-id="accbf-128">tooadd hello dash.js odwołanie do implementacji toohello aplikacji, musisz toograb hello dash.all.js pliku w wersji hello 1.0 dash.js projektu.</span><span class="sxs-lookup"><span data-stu-id="accbf-128">tooadd hello dash.js reference implementation toohello application, you’ll need toograb hello dash.all.js file from hello 1.0 release of dash.js project.</span></span> <span data-ttu-id="accbf-129">Powinna to być zapisane w folderze JavaScript hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="accbf-129">This should be saved in hello JavaScript folder of your application.</span></span> <span data-ttu-id="accbf-130">Ten plik jest plikiem wygody, ściągający cały kod niezbędne dash.js hello w jednym pliku w razem.</span><span class="sxs-lookup"><span data-stu-id="accbf-130">This file is a convenience file that pulls together all hello necessary dash.js code into a single file.</span></span> <span data-ttu-id="accbf-131">Jeśli masz wyszukiwania wokół repozytorium dash.js hello będzie Znajdź hello pojedyncze pliki, testowania kodu i wiele innych, ale jeśli wszystkie toodo jest dash.js Użyj, a następnie plik dash.all.js hello jest, co jest potrzebne.</span><span class="sxs-lookup"><span data-stu-id="accbf-131">If you have a look around hello dash.js repository, you will find hello individual files, test code and much more, but if all you want toodo is use dash.js, then hello dash.all.js file is what you need.</span></span>

<span data-ttu-id="accbf-132">tooadd hello dash.js player tooyour aplikacje, Dodaj skrypt tag toohello head sekcję basicPlayer.html:</span><span class="sxs-lookup"><span data-stu-id="accbf-132">tooadd hello dash.js player tooyour applications, add a script tag toohello head section of basicPlayer.html:</span></span>

    <!-- DASH-AVC/265 reference implementation -->
    < script src="js/dash.all.js"></script>


<span data-ttu-id="accbf-133">Następnie należy utworzyć odtwarzacza hello tooinitialize funkcji podczas ładowania strony hello.</span><span class="sxs-lookup"><span data-stu-id="accbf-133">Next, create a function tooinitialize hello player when hello page loads.</span></span> <span data-ttu-id="accbf-134">Dodaj następujące skryptu po wierszu hello załadować dash.all.js hello:</span><span class="sxs-lookup"><span data-stu-id="accbf-134">Add hello following script after hello line in which you load dash.all.js:</span></span>

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

<span data-ttu-id="accbf-135">Ta funkcja najpierw tworzy DashContext.</span><span class="sxs-lookup"><span data-stu-id="accbf-135">This function first creates a DashContext.</span></span> <span data-ttu-id="accbf-136">To jest aplikacja hello tooconfigure używane dla określonego środowiska.</span><span class="sxs-lookup"><span data-stu-id="accbf-136">This is used tooconfigure hello application for a specific runtime environment.</span></span> <span data-ttu-id="accbf-137">Z technicznego punktu widzenia definiuje powitalne podczas tworzenia aplikacji hello należy używać klas, które hello framework iniekcji zależności.</span><span class="sxs-lookup"><span data-stu-id="accbf-137">From a technical point of view, it defines hello classes that hello dependency injection framework should use when constructing hello application.</span></span> <span data-ttu-id="accbf-138">W większości przypadków będzie używany Dash.di.DashContext.</span><span class="sxs-lookup"><span data-stu-id="accbf-138">In most cases, you will use Dash.di.DashContext.</span></span>

<span data-ttu-id="accbf-139">Następnie można utworzyć wystąpienia hello klasy podstawowej struktury dash.js hello, MediaPlayer.</span><span class="sxs-lookup"><span data-stu-id="accbf-139">Next, instantiate hello primary class of hello dash.js framework, MediaPlayer.</span></span> <span data-ttu-id="accbf-140">Ta klasa zawiera podstawowe hello metody takie jak odtwarzanie i wstrzymywanie, zarządza hello relacji z elementem wideo hello i zarządza także interpretacji hello hello opis prezentacji nośnika (MPD) pliku, który opisuje hello toobe wideo odtwarzane.</span><span class="sxs-lookup"><span data-stu-id="accbf-140">This class contains hello core methods needed such as play and pause, manages hello relationship with hello video element and also manages hello interpretation of hello Media Presentation Description (MPD) file which describes hello video toobe played.</span></span>

<span data-ttu-id="accbf-141">Funkcja startup() Hello hello MediaPlayer klasy jest nazywany tooensure tego player hello jest gotowy tooplay wideo.</span><span class="sxs-lookup"><span data-stu-id="accbf-141">hello startup() function of hello MediaPlayer class is called tooensure that hello player is ready tooplay video.</span></span> <span data-ttu-id="accbf-142">Między innymi tej funkcji powoduje, że wszystkie niezbędne klasy hello (zgodnie z definicją w kontekście hello) zostały załadowane.</span><span class="sxs-lookup"><span data-stu-id="accbf-142">Amongst other things this function ensures that all hello necessary classes (as defined by hello context) have been loaded.</span></span> <span data-ttu-id="accbf-143">Gdy hello player jest gotowy, możesz dołączyć hello tooit element wideo przy użyciu funkcji attachView() hello.</span><span class="sxs-lookup"><span data-stu-id="accbf-143">Once hello player is ready, you can attach hello video element tooit using hello attachView() function.</span></span> <span data-ttu-id="accbf-144">Włącza hello MediaPlayer tooinject hello strumienia wideo o do elementu hello, a także sterować odtwarzania w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="accbf-144">This enables hello MediaPlayer tooinject hello video stream into hello element and also control playback as necessary.</span></span>

<span data-ttu-id="accbf-145">Przekaż hello adres URL hello MPD pliku toohello MediaPlayer tak, aby go zna hello wideo oczekuje się, funkcja setupVideo() tooplay.hello właśnie utworzony należy toobe wykonywane po stronie powitania pełni został załadowany.</span><span class="sxs-lookup"><span data-stu-id="accbf-145">Pass hello URL of hello MPD file toohello MediaPlayer so that it knows about hello video it is expected tooplay.hello setupVideo() function just created will need toobe executed once hello page has fully loaded.</span></span> <span data-ttu-id="accbf-146">W tym celu za pomocą zdarzenia onload hello hello treści elementu.</span><span class="sxs-lookup"><span data-stu-id="accbf-146">Do this by using hello onload event of hello body element.</span></span> <span data-ttu-id="accbf-147">Zmień Twoje <body> elementu:</span><span class="sxs-lookup"><span data-stu-id="accbf-147">Change your <body> element to:</span></span>

    <body onload="setupVideo()">

<span data-ttu-id="accbf-148">Wreszcie Ustaw rozmiar hello hello elementu wideo za pomocą CSS.</span><span class="sxs-lookup"><span data-stu-id="accbf-148">Finally, set hello size of hello video element using CSS.</span></span> <span data-ttu-id="accbf-149">W środowisku adaptacyjnego przesyłania strumieniowego jest to szczególnie ważne, ponieważ rozmiar hello hello odtwarzania wideo może zmienić odtwarzania dostosowuje się warunków sieciowych toochanging.</span><span class="sxs-lookup"><span data-stu-id="accbf-149">In an adaptive streaming environment, this is especially important because hello size of hello video being played may change as playback adapts toochanging network conditions.</span></span> <span data-ttu-id="accbf-150">W tym prosty pokaz po prostu wymusić hello wideo element toobe 80% okna przeglądarki dostępne hello przez dodanie powitania po CSS toohello sekcji head hello strony:</span><span class="sxs-lookup"><span data-stu-id="accbf-150">In this simple demo simply force hello video element toobe 80% of hello available browser window by adding hello following CSS toohello head section of hello page:</span></span>

    <style>
    video {
      width: 80%;
      height: 80%;
    }
    </style>

## <a name="playing-a-video"></a><span data-ttu-id="accbf-151">Odtwarzanie wideo</span><span class="sxs-lookup"><span data-stu-id="accbf-151">Playing a Video</span></span>
<span data-ttu-id="accbf-152">tooplay wideo, wskazać w przeglądarce hello basicPlayback.html plik i kliknij przycisk play na powitania odtwarzacza wideo wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="accbf-152">tooplay a video, point your browser at hello basicPlayback.html file and click play on hello video player displayed.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="accbf-153">Ścieżki szkoleniowe dotyczące usługi Media Services</span><span class="sxs-lookup"><span data-stu-id="accbf-153">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="accbf-154">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="accbf-154">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="accbf-155">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="accbf-155">See Also</span></span>
[<span data-ttu-id="accbf-156">Opracowywanie aplikacji odtwarzacza wideo</span><span class="sxs-lookup"><span data-stu-id="accbf-156">Develop video player applications</span></span>](media-services-develop-video-players.md)

[<span data-ttu-id="accbf-157">Repozytorium GitHub dash.js</span><span class="sxs-lookup"><span data-stu-id="accbf-157">GitHub dash.js repository</span></span>](https://github.com/Dash-Industry-Forum/dash.js) 

