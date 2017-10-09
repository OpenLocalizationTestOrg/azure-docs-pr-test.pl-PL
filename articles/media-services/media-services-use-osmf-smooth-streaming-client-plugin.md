---
title: "aaaSmooth wtyczki przesyłania strumieniowego dla hello Open Framework nośnika źródłowego"
description: "Dowiedz się, jak toouse hello Azure Media Services Smooth Streaming dodatek plug-in dla hello Adobe otwartej struktury nośnika źródłowego."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 6068151f-b6b0-4507-9346-f03416d3d572
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/26/2016
ms.author: juliako
ms.openlocfilehash: 3cf8e4679279344cf79c3f0e5b28f63adf88179d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-microsoft-smooth-streaming-plugin-for-hello-adobe-open-source-media-framework"></a><span data-ttu-id="1c0b8-103">Jak tooUse hello Microsoft Smooth Streaming wtyczki dla hello Adobe Open Framework nośnika źródła</span><span class="sxs-lookup"><span data-stu-id="1c0b8-103">How tooUse hello Microsoft Smooth Streaming Plugin for hello Adobe Open Source Media Framework</span></span>
## <a name="overview"></a><span data-ttu-id="1c0b8-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="1c0b8-104">Overview</span></span>
<span data-ttu-id="1c0b8-105">Witaj dodatek Microsoft Smooth Streaming, otwórz źródła Media Framework w wersji 2.0 (SS dla OSMF) rozszerza możliwości domyślne hello OSMF i dodaje Microsoft Smooth Streaming toonew odtwarzanie zawartości i istniejące OSMF graczy.</span><span class="sxs-lookup"><span data-stu-id="1c0b8-105">hello Microsoft Smooth Streaming plugin for Open Source Media Framework 2.0 (SS for OSMF) extends hello default capabilities of OSMF and adds Microsoft Smooth Streaming content playback toonew and existing OSMF players.</span></span> <span data-ttu-id="1c0b8-106">Dodatek Hello dodaje również Smooth Streaming tooStrobe możliwości odtwarzania multimediów odtwarzania (SMP).</span><span class="sxs-lookup"><span data-stu-id="1c0b8-106">hello plugin also adds Smooth Streaming playback capabilities tooStrobe Media Playback (SMP).</span></span>

<span data-ttu-id="1c0b8-107">SS dla OSMF obejmuje dwie wersje dodatku:</span><span class="sxs-lookup"><span data-stu-id="1c0b8-107">SS for OSMF includes two versions of plugin:</span></span>

* <span data-ttu-id="1c0b8-108">Statyczne Smooth Streaming dodatek plug-in dla OSMF (SWC)</span><span class="sxs-lookup"><span data-stu-id="1c0b8-108">Static Smooth Streaming plugin for OSMF (.swc)</span></span>
* <span data-ttu-id="1c0b8-109">Dynamiczne Smooth Streaming dodatek plug-in dla OSMF (SWF)</span><span class="sxs-lookup"><span data-stu-id="1c0b8-109">Dynamic Smooth Streaming plugin for OSMF (.swf)</span></span>

<span data-ttu-id="1c0b8-110">Tym dokumencie przyjęto założenie, że czytelnik hello ma ogólne praktyczną znajomość OSMF i OSMF dodatków plug-in. Aby uzyskać więcej informacji na temat OSMF Zobacz hello dokumentację hello [oficjalna witryna OSMF](http://osmf.org/).</span><span class="sxs-lookup"><span data-stu-id="1c0b8-110">This document assumes that hello reader has a general working knowledge of OSMF and OSMF plug-ins. For more information about OSMF, please see hello documentation on hello [official OSMF site](http://osmf.org/).</span></span>

### <a name="smooth-streaming-plugin-for-osmf-20"></a><span data-ttu-id="1c0b8-111">Wtyczka Smooth Streaming OSMF 2.0</span><span class="sxs-lookup"><span data-stu-id="1c0b8-111">Smooth Streaming plugin for OSMF 2.0</span></span>
<span data-ttu-id="1c0b8-112">Dodatek Hello obsługuje ładowania i odtwarzania zawartości Smooth Streaming na żądanie z hello następujące funkcje:</span><span class="sxs-lookup"><span data-stu-id="1c0b8-112">hello plugin supports loading and playback of on-demand Smooth Streaming content with hello following features:</span></span>

* <span data-ttu-id="1c0b8-113">Odtwarzanie Smooth Streaming na żądanie (Wstrzymaj, wyszukiwania, Zatrzymaj odtwarzanie)</span><span class="sxs-lookup"><span data-stu-id="1c0b8-113">On-demand Smooth Streaming playback (Play, Pause, Seek, Stop)</span></span>
* <span data-ttu-id="1c0b8-114">Odtwarzanie Live Smooth Streaming (Odtwórz)</span><span class="sxs-lookup"><span data-stu-id="1c0b8-114">Live Smooth Streaming playback (Play)</span></span>
* <span data-ttu-id="1c0b8-115">Na żywo funkcji DVR (Wstrzymaj, wyszukiwania, odtwarzania DVR, Go Live)</span><span class="sxs-lookup"><span data-stu-id="1c0b8-115">Live DVR functions (Pause, Seek, DVR Playback, Go-to-Live)</span></span>
* <span data-ttu-id="1c0b8-116">Obsługa wideo koderów-dekoderów - H.264</span><span class="sxs-lookup"><span data-stu-id="1c0b8-116">Support for video codecs - H.264</span></span>
* <span data-ttu-id="1c0b8-117">Obsługę Audio koderów-dekoderów - AAC</span><span class="sxs-lookup"><span data-stu-id="1c0b8-117">Support for Audio codecs - AAC</span></span>
* <span data-ttu-id="1c0b8-118">Wiele wersji językowych audio przełączenie OSMF wbudowanych interfejsów API</span><span class="sxs-lookup"><span data-stu-id="1c0b8-118">Multiple audio language switching with OSMF built-in APIs</span></span>
* <span data-ttu-id="1c0b8-119">Maksymalna liczba odtwarzania jakości wybór z interfejsami API wbudowanych OSMF</span><span class="sxs-lookup"><span data-stu-id="1c0b8-119">Max playback quality selection with OSMF built-in APIs</span></span>
* <span data-ttu-id="1c0b8-120">Podpisy z wtyczki podpisy OSMF kodowane boczną</span><span class="sxs-lookup"><span data-stu-id="1c0b8-120">Sidecar closed captions with OSMF captions plugin</span></span>
* <span data-ttu-id="1c0b8-121">Adobe&reg; Flash&reg; Player 11.4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="1c0b8-121">Adobe&reg; Flash&reg; Player 11.4 or higher.</span></span>
* <span data-ttu-id="1c0b8-122">Ta wersja obsługuje tylko OSMF 2.0.</span><span class="sxs-lookup"><span data-stu-id="1c0b8-122">This version only supports OSMF 2.0.</span></span>

## <a name="supported-features-and-known-issues"></a><span data-ttu-id="1c0b8-123">Obsługiwane funkcje i znane problemy</span><span class="sxs-lookup"><span data-stu-id="1c0b8-123">Supported features and known issues</span></span>
<span data-ttu-id="1c0b8-124">Aby uzyskać pełną listę obsługiwanych funkcji, nieobsługiwane funkcje i znanych problemów można znaleźć zbyt[tego dokumentu](http://download.microsoft.com/download/3/1/B/31B63D97-574E-4A8D-BF8D-170744181724/Smooth_Streaming_Plugin_for_OSMF.pdf).</span><span class="sxs-lookup"><span data-stu-id="1c0b8-124">For a full list of supported features, unsupported features and known issues, refer too[this document](http://download.microsoft.com/download/3/1/B/31B63D97-574E-4A8D-BF8D-170744181724/Smooth_Streaming_Plugin_for_OSMF.pdf).</span></span>

## <a name="loading-hello-plugin"></a><span data-ttu-id="1c0b8-125">Ładowanie hello wtyczki</span><span class="sxs-lookup"><span data-stu-id="1c0b8-125">Loading hello Plugin</span></span>
<span data-ttu-id="1c0b8-126">Można załadować wtyczki OSMF statycznie (w czasie kompilacji) lub dynamicznie (w czasie wykonywania).</span><span class="sxs-lookup"><span data-stu-id="1c0b8-126">OSMF plugins can be loaded statically (at compile time) or dynamically (at run-time).</span></span> <span data-ttu-id="1c0b8-127">Witaj Smooth Streaming wtyczki do pobrania OSMF obejmuje zarówno dynamicznej i statycznej wersji.</span><span class="sxs-lookup"><span data-stu-id="1c0b8-127">hello Smooth Streaming plugin for OSMF download includes both dynamic and static versions.</span></span>

* <span data-ttu-id="1c0b8-128">Ładowanie statycznych: tooload statycznie, plik biblioteki statycznej (SWC) jest wymagana.</span><span class="sxs-lookup"><span data-stu-id="1c0b8-128">Static loading: tooload statically, a static library (SWC) file is required.</span></span> <span data-ttu-id="1c0b8-129">Statyczne wtyczek są dodawane jako odwołania toohello projektów i dokonać scalania w hello ostateczne dane wyjściowe pliku w czasie kompilacji hello.</span><span class="sxs-lookup"><span data-stu-id="1c0b8-129">Static plugins are added as a reference toohello projects and merge inside hello final output file at hello compile time.</span></span>
* <span data-ttu-id="1c0b8-130">Dynamiczne ładowanie: tooload dynamicznie, wstępnie skompilowanych plików (SWF) jest wymagana.</span><span class="sxs-lookup"><span data-stu-id="1c0b8-130">Dynamic loading: tooload dynamically, a precompiled (SWF) file is required.</span></span> <span data-ttu-id="1c0b8-131">Dynamiczne dodatków plug-in są ładowane w środowisku uruchomieniowym hello i nie są uwzględnione w danych wyjściowych projektu hello.</span><span class="sxs-lookup"><span data-stu-id="1c0b8-131">Dynamic plugins are loaded in hello runtime and not included in hello project output.</span></span> <span data-ttu-id="1c0b8-132">(Skompilowanych danych wyjściowych) Wtyczki dynamicznej mogą być ładowane przy użyciu protokołów HTTP i plików.</span><span class="sxs-lookup"><span data-stu-id="1c0b8-132">(Compiled output) Dynamic plugins can be loaded using HTTP and FILE protocols.</span></span>

<span data-ttu-id="1c0b8-133">Aby uzyskać więcej informacji na ładowanie statycznych i dynamicznych, zobacz oficjalne hello [strona wtyczek OSMF](http://osmf.org/dev/osmf/OtherPDFs/osmf_plugin_dev_guide.pdf).</span><span class="sxs-lookup"><span data-stu-id="1c0b8-133">For more information on static and dynamic loading, see hello official [OSMF plugin page](http://osmf.org/dev/osmf/OtherPDFs/osmf_plugin_dev_guide.pdf).</span></span>

### <a name="ss-for-osmf-static-loading"></a><span data-ttu-id="1c0b8-134">SS do ładowania statycznych OSMF</span><span class="sxs-lookup"><span data-stu-id="1c0b8-134">SS for OSMF Static Loading</span></span>
<span data-ttu-id="1c0b8-135">Poniższy fragment kodu Hello pokazuje, jak tooload statycznie hello SS wtyczki dla OSMF i odtwarzanie wideo podstawowe za pomocą klasy OSMF MediaFactory.</span><span class="sxs-lookup"><span data-stu-id="1c0b8-135">hello code snippet below shows how tooload hello SS plugin for OSMF statically and play a basic video using OSMF MediaFactory class.</span></span> <span data-ttu-id="1c0b8-136">Przed dołączeniem hello SS OSMF kodu, upewnij się, że odwołania projektu hello zawiera wtyczki statycznych hello "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swc".</span><span class="sxs-lookup"><span data-stu-id="1c0b8-136">Before including hello SS for OSMF code, please ensure that hello project reference includes hello "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swc" static plugin.</span></span>

```
package 
{

    import com.microsoft.azure.media.AdaptiveStreamingPluginInfo;

    import flash.display.*;
    import org.osmf.media.*;
    import org.osmf.containers.MediaContainer;
    import org.osmf.events.MediaErrorEvent;
    import org.osmf.events.MediaFactoryEvent;
    import org.osmf.events.MediaPlayerStateChangeEvent;
    import org.osmf.layout.*;



    [SWF(width="1024", height="768", backgroundColor='#405050', frameRate="25")]
    public class TestPlayer extends Sprite
    {        
        public var _container:MediaContainer;
        public var _mediaFactory:DefaultMediaFactory;
        private var _mediaPlayerSprite:MediaPlayerSprite;


        public function TestPlayer( )
        {
            stage.quality = StageQuality.HIGH;

            initMediaPlayer();

        }

        private function initMediaPlayer():void
        {

            // Create hello container (sprite) for managing display and layout
            _mediaPlayerSprite = new MediaPlayerSprite();    
            _mediaPlayerSprite.addEventListener(MediaErrorEvent.MEDIA_ERROR, onPlayerFailed);
            _mediaPlayerSprite.addEventListener(MediaPlayerStateChangeEvent.MEDIA_PLAYER_STATE_CHANGE, onPlayerStateChange);
            _mediaPlayerSprite.scaleMode = ScaleMode.NONE;
            _mediaPlayerSprite.width = stage.stageWidth;
            _mediaPlayerSprite.height = stage.stageHeight;
            //Adds hello container toohello stage
            addChild(_mediaPlayerSprite);

            // Create a mediafactory instance
            _mediaFactory = new DefaultMediaFactory();

            // Add hello listeners for PLUGIN_LOADING
            _mediaFactory.addEventListener(MediaFactoryEvent.PLUGIN_LOAD,onPluginLoaded);
            _mediaFactory.addEventListener(MediaFactoryEvent.PLUGIN_LOAD_ERROR, onPluginLoadFailed );

            // Load hello plugin class 
            loadAdaptiveStreamingPlugin( );  

        }

        private function loadAdaptiveStreamingPlugin( ):void
        {
            var pluginResource:MediaResourceBase;

            pluginResource = new PluginInfoResource(new AdaptiveStreamingPluginInfo( )); 
            _mediaFactory.loadPlugin( pluginResource ); 
        }

        private function onPluginLoaded( event:MediaFactoryEvent ):void
        {
            // hello plugin is loaded successfully.
            // Your web server needs toohost a valid crossdomain.xml file tooallow plugin toodownload Smooth Streaming files.
        loadMediaSource("http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest")

        }

        private function onPluginLoadFailed( event:MediaFactoryEvent ):void
        {
            // hello plugin is failed tooload ...
        }


        private function onPlayerStateChange(event:MediaPlayerStateChangeEvent) : void
        {
            var state:String;

            state =  event.state;

            switch (state)
            {
                case MediaPlayerState.LOADING: 

                    // A new source is started tooload.

                    break;

                case  MediaPlayerState.READY :   
                    // Add code toodeal with Player Ready when it is hit hello first load after a source is loaded. 

                    break;

                case MediaPlayerState.BUFFERING :

                    break;

                case  MediaPlayerState.PAUSED :
                    break;      
                // other states ...          
            }
        }

        private function onPlayerFailed(event:MediaErrorEvent) : void
        {
            // Media Player is failed .           
        }

        private function loadMediaSource(sourceURL : String):void 
        {
            // Take an URL of SmoothStreamingSource's manifest and add it toohello page.

            var resource:URLResource= new URLResource( sourceURL );

            var element:MediaElement = _mediaFactory.createMediaElement( resource );
            _mediaPlayerSprite.scaleMode = ScaleMode.LETTERBOX;
            _mediaPlayerSprite.width = stage.stageWidth;
            _mediaPlayerSprite.height = stage.stageHeight;

            // Add hello media element
            _mediaPlayerSprite.media = element;
        }     

    }
}
```


### <a name="ss-for-osmf-dynamic-loading"></a><span data-ttu-id="1c0b8-137">SS dla OSMF dynamiczne ładowanie</span><span class="sxs-lookup"><span data-stu-id="1c0b8-137">SS for OSMF Dynamic Loading</span></span>
<span data-ttu-id="1c0b8-138">Poniższy fragment kodu Hello pokazuje, jak tooload dynamicznie hello SS wtyczki dla OSMF i odtwarzanie wideo podstawowe za pomocą klasy OSMF MediaFactory hello.</span><span class="sxs-lookup"><span data-stu-id="1c0b8-138">hello code snippet below shows how tooload hello SS plugin for OSMF dynamically and play a basic video using hello OSMF MediaFactory class.</span></span> <span data-ttu-id="1c0b8-139">Przed dołączeniem hello SS OSMF kodu, należy skopiować folder projektu toohello dynamiczne wtyczki "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swf" hello tooload przy użyciu protokołu pliku, lub skopiować na serwerze sieci web, obciążenia HTTP.</span><span class="sxs-lookup"><span data-stu-id="1c0b8-139">Before including hello SS for OSMF code, copy hello "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swf" dynamic plugin toohello project folder if you want tooload using FILE protocol, or copy under a web server for HTTP load.</span></span> <span data-ttu-id="1c0b8-140">Nie ma żadnych tooinclude potrzeby "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swc" w odwołaniach projektu hello.</span><span class="sxs-lookup"><span data-stu-id="1c0b8-140">There is no need tooinclude "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swc" in hello project references.</span></span>

<span data-ttu-id="1c0b8-141">{pakietu</span><span class="sxs-lookup"><span data-stu-id="1c0b8-141">package {</span></span>

    import flash.display.*;
    import org.osmf.media.*;
    import org.osmf.containers.MediaContainer;
    import org.osmf.events.MediaErrorEvent;
    import org.osmf.events.MediaFactoryEvent;
    import org.osmf.events.MediaPlayerStateChangeEvent;
    import org.osmf.layout.*;
    import flash.events.Event;
    import flash.system.Capabilities;


    //Sets hello size of hello SWF

    [SWF(width="1024", height="768", backgroundColor='#405050', frameRate="25")]
    public class TestPlayer extends Sprite
    {        
        public var _container:MediaContainer;
        public var _mediaFactory:DefaultMediaFactory;
        private var _mediaPlayerSprite:MediaPlayerSprite;


        public function TestPlayer( )
        {
            stage.quality = StageQuality.HIGH;
            initMediaPlayer();
        }

        private function initMediaPlayer():void
        {

            // Create hello container (sprite) for managing display and layout
            _mediaPlayerSprite = new MediaPlayerSprite();    
            _mediaPlayerSprite.addEventListener(MediaErrorEvent.MEDIA_ERROR, onPlayerFailed);
            _mediaPlayerSprite.addEventListener(MediaPlayerStateChangeEvent.MEDIA_PLAYER_STATE_CHANGE, onPlayerStateChange);

            //Adds hello container toohello stage
            addChild(_mediaPlayerSprite);

            // Create a mediafactory instance
            _mediaFactory = new DefaultMediaFactory();

            // Add hello listeners for PLUGIN_LOADING
            _mediaFactory.addEventListener(MediaFactoryEvent.PLUGIN_LOAD,onPluginLoaded);
            _mediaFactory.addEventListener(MediaFactoryEvent.PLUGIN_LOAD_ERROR, onPluginLoadFailed );

            // Load hello plugin class 
            loadAdaptiveStreamingPlugin( );  

        }

        private function loadAdaptiveStreamingPlugin( ):void
        {
            var pluginResource:MediaResourceBase;
            var adaptiveStreamingPluginUrl:String;

            // Your dynamic plugin web server needs toohost a valid crossdomain.xml file tooallow loading plugins.

            adaptiveStreamingPluginUrl = "http://yourdomain/MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swf";
            pluginResource = new URLResource(adaptiveStreamingPluginUrl);
            _mediaFactory.loadPlugin( pluginResource ); 

        }

        private function onPluginLoaded( event:MediaFactoryEvent ):void
        {
            // hello plugin is loaded successfully.

            // Your web server needs toohost a valid crossdomain.xml file tooallow plugin toodownload Smooth Streaming files.

    loadMediaSource("http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest")
        }

        private function onPluginLoadFailed( event:MediaFactoryEvent ):void
        {
            // hello plugin is failed tooload ...
        }


        private function onPlayerStateChange(event:MediaPlayerStateChangeEvent) : void
        {
            var state:String;

            state =  event.state;

            switch (state)
            {
                case MediaPlayerState.LOADING: 

                    // A new source is started tooload.

                    break;

                case  MediaPlayerState.READY :   
                    // Add code toodeal with Player Ready when it is hit hello first load after a source is loaded. 

                    break;

                case MediaPlayerState.BUFFERING :

                    break;

                case  MediaPlayerState.PAUSED :
                    break;      
                // other states ...          
            }
        }

        private function onPlayerFailed(event:MediaErrorEvent) : void
        {
            // Media Player is failed .           
        }

        private function loadMediaSource(sourceURL : String):void 
        {
            // Take an URL of SmoothStreamingSource's manifest and add it toohello page.

            var resource:URLResource= new URLResource( sourceURL );

            var element:MediaElement = _mediaFactory.createMediaElement( resource );
            _mediaPlayerSprite.scaleMode = ScaleMode.LETTERBOX;
            _mediaPlayerSprite.width = stage.stageWidth;
            _mediaPlayerSprite.height = stage.stageHeight;
            // Add hello media element
            _mediaPlayerSprite.media = element;
        }     

    }
<span data-ttu-id="1c0b8-142">}</span><span class="sxs-lookup"><span data-stu-id="1c0b8-142">}</span></span>

## <a name="strobe-media--playback-with-hello-ss-odmf-dynamic-plugin"></a><span data-ttu-id="1c0b8-143">Odtwarzanie multimediów światła z hello wtyczki dynamiczne ODMF SS</span><span class="sxs-lookup"><span data-stu-id="1c0b8-143">Strobe Media  Playback with hello SS ODMF Dynamic Plugin</span></span>
<span data-ttu-id="1c0b8-144">Hello Smooth Streaming wtyczki dynamiczne OSMF jest zgodny z [odtwarzania multimediów światła (SMP)](http://osmf.org/strobe_mediaplayback.html).</span><span class="sxs-lookup"><span data-stu-id="1c0b8-144">hello Smooth Streaming for OSMF dynamic plugin is compatible with [Strobe Media Playback (SMP)](http://osmf.org/strobe_mediaplayback.html).</span></span> <span data-ttu-id="1c0b8-145">Hello SS służy do odtwarzania zawartości Smooth Streaming programu OSMF wtyczki tooadd tooSMP.</span><span class="sxs-lookup"><span data-stu-id="1c0b8-145">You can use hello SS for OSMF plugin tooadd Smooth Streaming content playback tooSMP.</span></span> <span data-ttu-id="1c0b8-146">toodo, kopii "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swf" na serwerze sieci web dla obciążenia HTTP przy użyciu hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="1c0b8-146">toodo this, copy "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swf" under a web server for HTTP load using hello following steps:</span></span>

1. <span data-ttu-id="1c0b8-147">Przeglądaj hello [strony Instalatora odtwarzanie multimediów światła](http://osmf.org/dev/2.0gm/setup.html).</span><span class="sxs-lookup"><span data-stu-id="1c0b8-147">Browse hello [Strobe Media Playback setup page](http://osmf.org/dev/2.0gm/setup.html).</span></span> 
2. <span data-ttu-id="1c0b8-148">Ustaw hello src tooa Smooth Streaming źródła (np. http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest)</span><span class="sxs-lookup"><span data-stu-id="1c0b8-148">Set hello src tooa Smooth Streaming source, (e.g. http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest)</span></span> 
3. <span data-ttu-id="1c0b8-149">Hello potrzeby zmian konfiguracji, a następnie kliknij polecenie Podgląd i aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="1c0b8-149">Make hello desired configuration changes and click Preview and Update.</span></span>
   
   <span data-ttu-id="1c0b8-150">**Uwaga** prawidłowy crossdomain.xml wymaga serwera zawartości sieci web.</span><span class="sxs-lookup"><span data-stu-id="1c0b8-150">**Note** Your content web server needs a valid crossdomain.xml.</span></span> 
4. <span data-ttu-id="1c0b8-151">Skopiuj i Wklej hello tooa proste HTML strony kodowej w hello poniższy przykład za pomocą edytora tekstu, takich jak:</span><span class="sxs-lookup"><span data-stu-id="1c0b8-151">Copy and paste hello code tooa simple HTML page using your favorite text editor, such as in hello following example:</span></span>

        <html>
        <body>
        <object width="920" height="640"> 
        <param name="movie" value="http://osmf.org/dev/2.0gm/StrobeMediaPlayback.swf"></param>
        <param name="flashvars" value="src=http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest &autoPlay=true"></param>
        <param name="allowFullScreen" value="true"></param>
        <param name="allowscriptaccess" value="always"></param>
        <param name="wmode" value="direct"></param>
        <embed src="http://osmf.org/dev/2.0gm/StrobeMediaPlayback.swf" 
            type="application/x-shockwave-flash" 
            allowscriptaccess="always" 
            allowfullscreen="true" 
            wmode="direct" 
            width="920" 
            height="640" 
            flashvars=" src=http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest&autoPlay=true">
        </embed>
        </object>
        </body>
        </html>



1. <span data-ttu-id="1c0b8-152">Dodaj toohello wtyczki Smooth Streaming OSMF kod osadzania i Zapisz.</span><span class="sxs-lookup"><span data-stu-id="1c0b8-152">Add Smooth Streaming OSMF plugin toohello embed code and save.</span></span>
   
        <html>
        <object width="920" height="640"> 
        <param name="movie" value="http://osmf.org/dev/2.0gm/StrobeMediaPlayback.swf"></param>
        <param name="flashvars" value="src=http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest&autoPlay=true&plugin_AdaptiveStreamingPlugin=http://yourdomain/MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swf&AdaptiveStreamingPlugin_retryLive=true&AdaptiveStreamingPlugin_retryInterval=10"></param>
        <param name="allowFullScreen" value="true"></param>
        <param name="allowscriptaccess" value="always"></param>
        <param name="wmode" value="direct"></param>
        <embed src="http://osmf.org/dev/2.0gm/StrobeMediaPlayback.swf" 
            type="application/x-shockwave-flash" 
            allowscriptaccess="always" 
            allowfullscreen="true" 
            wmode="direct" 
            width="920" 
            height="640" 
            flashvars="src=http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest&autoPlay=true&plugin_AdaptiveStreamingPlugin=http://yourdomain/MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swf&AdaptiveStreamingPlugin_retryLive=true&AdaptiveStreamingPlugin_retryInterval=10">
        </embed>
        </object>
        </html>
2. <span data-ttu-id="1c0b8-153">Zapisz strony HTML i opublikuj tooa serwera sieci web.</span><span class="sxs-lookup"><span data-stu-id="1c0b8-153">Save your HTML page and publish tooa web server.</span></span> <span data-ttu-id="1c0b8-154">Przeglądaj toohello opublikowane strony sieci web przy użyciu Twoje ulubione Flash&reg; Player włączone przeglądarki internetowej (program Internet Explorer, Chrome, Firefox, itp).</span><span class="sxs-lookup"><span data-stu-id="1c0b8-154">Browse toohello published web page using your favorite Flash&reg; Player enabled Internet browser (Internet Explorer, Chrome, Firefox, so on).</span></span>
3. <span data-ttu-id="1c0b8-155">Korzystanie z funkcji Smooth Streaming zawartości wewnątrz Adobe&reg; Flash&reg; Player.</span><span class="sxs-lookup"><span data-stu-id="1c0b8-155">Enjoy Smooth Streaming content inside Adobe&reg; Flash&reg; Player.</span></span>

<span data-ttu-id="1c0b8-156">Aby uzyskać więcej informacji na ogólne programowanie OSMF, zobacz oficjalne hello [OSMF programowanie strony](http://osmf.org/resources.html).</span><span class="sxs-lookup"><span data-stu-id="1c0b8-156">For more information on general OSMF development, please see hello official [OSMF development page](http://osmf.org/resources.html).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="1c0b8-157">Ścieżki szkoleniowe dotyczące usługi Media Services</span><span class="sxs-lookup"><span data-stu-id="1c0b8-157">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="1c0b8-158">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="1c0b8-158">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="1c0b8-159">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="1c0b8-159">See Also</span></span>
[<span data-ttu-id="1c0b8-160">Adaptacyjne przesyłanie strumieniowe wtyczki dla aktualizacji OSMF firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="1c0b8-160">Microsoft Adaptive Streaming Plugin for OSMF Update</span></span>](https://azure.microsoft.com/blog/2014/10/27/microsoft-adaptive-streaming-plugin-for-osmf-update/) 

