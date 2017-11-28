---
title: "Płynnego przesyłania strumieniowego dodatek plug-in dla typu Open Source Media Framework"
description: "Dowiedz się, jak używać usługi Azure Media Services Smooth Streaming wtyczki dla otwartej struktury nośnika źródłowego programu Adobe."
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
ms.openlocfilehash: 9c764f176ae75085320882de3fb26d8e7d52daaf
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-the-microsoft-smooth-streaming-plugin-for-the-adobe-open-source-media-framework"></a><span data-ttu-id="13f34-103">Jak używać Smooth Microsoft przesyłania strumieniowego dodatek dla programu Adobe typu Open Source Media Framework</span><span class="sxs-lookup"><span data-stu-id="13f34-103">How to Use the Microsoft Smooth Streaming Plugin for the Adobe Open Source Media Framework</span></span>
## <a name="overview"></a><span data-ttu-id="13f34-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="13f34-104">Overview</span></span>
<span data-ttu-id="13f34-105">Dodatek Microsoft Smooth Streaming dla Otwórz źródła Media Framework w wersji 2.0 (SS dla OSMF) rozszerza możliwości domyślne OSMF i dodaje Microsoft Smooth Streaming odtwarzanie zawartości dla nowych i istniejących odtwarzaczy OSMF.</span><span class="sxs-lookup"><span data-stu-id="13f34-105">The Microsoft Smooth Streaming plugin for Open Source Media Framework 2.0 (SS for OSMF) extends the default capabilities of OSMF and adds Microsoft Smooth Streaming content playback to new and existing OSMF players.</span></span> <span data-ttu-id="13f34-106">Wtyczka dodaje również funkcje Smooth Streaming odtwarzania do odtwarzania multimediów światła (SMP).</span><span class="sxs-lookup"><span data-stu-id="13f34-106">The plugin also adds Smooth Streaming playback capabilities to Strobe Media Playback (SMP).</span></span>

<span data-ttu-id="13f34-107">SS dla OSMF obejmuje dwie wersje dodatku:</span><span class="sxs-lookup"><span data-stu-id="13f34-107">SS for OSMF includes two versions of plugin:</span></span>

* <span data-ttu-id="13f34-108">Statyczne Smooth Streaming dodatek plug-in dla OSMF (SWC)</span><span class="sxs-lookup"><span data-stu-id="13f34-108">Static Smooth Streaming plugin for OSMF (.swc)</span></span>
* <span data-ttu-id="13f34-109">Dynamiczne Smooth Streaming dodatek plug-in dla OSMF (SWF)</span><span class="sxs-lookup"><span data-stu-id="13f34-109">Dynamic Smooth Streaming plugin for OSMF (.swf)</span></span>

<span data-ttu-id="13f34-110">Tym dokumencie przyjęto założenie, że czytelnik ma ogólne praktyczną znajomość OSMF i OSMF dodatków plug-in. Aby uzyskać więcej informacji na temat OSMF można znaleźć w dokumentacji na [oficjalna witryna OSMF](http://osmf.org/).</span><span class="sxs-lookup"><span data-stu-id="13f34-110">This document assumes that the reader has a general working knowledge of OSMF and OSMF plug-ins. For more information about OSMF, please see the documentation on the [official OSMF site](http://osmf.org/).</span></span>

### <a name="smooth-streaming-plugin-for-osmf-20"></a><span data-ttu-id="13f34-111">Wtyczka Smooth Streaming OSMF 2.0</span><span class="sxs-lookup"><span data-stu-id="13f34-111">Smooth Streaming plugin for OSMF 2.0</span></span>
<span data-ttu-id="13f34-112">Wtyczka obsługuje ładowania i odtwarzania zawartości Smooth Streaming na żądanie przy użyciu następujących funkcji:</span><span class="sxs-lookup"><span data-stu-id="13f34-112">The plugin supports loading and playback of on-demand Smooth Streaming content with the following features:</span></span>

* <span data-ttu-id="13f34-113">Odtwarzanie Smooth Streaming na żądanie (Wstrzymaj, wyszukiwania, Zatrzymaj odtwarzanie)</span><span class="sxs-lookup"><span data-stu-id="13f34-113">On-demand Smooth Streaming playback (Play, Pause, Seek, Stop)</span></span>
* <span data-ttu-id="13f34-114">Odtwarzanie Live Smooth Streaming (Odtwórz)</span><span class="sxs-lookup"><span data-stu-id="13f34-114">Live Smooth Streaming playback (Play)</span></span>
* <span data-ttu-id="13f34-115">Na żywo funkcji DVR (Wstrzymaj, wyszukiwania, odtwarzania DVR, Go Live)</span><span class="sxs-lookup"><span data-stu-id="13f34-115">Live DVR functions (Pause, Seek, DVR Playback, Go-to-Live)</span></span>
* <span data-ttu-id="13f34-116">Obsługa wideo koderów-dekoderów - H.264</span><span class="sxs-lookup"><span data-stu-id="13f34-116">Support for video codecs - H.264</span></span>
* <span data-ttu-id="13f34-117">Obsługę Audio koderów-dekoderów - AAC</span><span class="sxs-lookup"><span data-stu-id="13f34-117">Support for Audio codecs - AAC</span></span>
* <span data-ttu-id="13f34-118">Wiele wersji językowych audio przełączenie OSMF wbudowanych interfejsów API</span><span class="sxs-lookup"><span data-stu-id="13f34-118">Multiple audio language switching with OSMF built-in APIs</span></span>
* <span data-ttu-id="13f34-119">Maksymalna liczba odtwarzania jakości wybór z interfejsami API wbudowanych OSMF</span><span class="sxs-lookup"><span data-stu-id="13f34-119">Max playback quality selection with OSMF built-in APIs</span></span>
* <span data-ttu-id="13f34-120">Podpisy z wtyczki podpisy OSMF kodowane boczną</span><span class="sxs-lookup"><span data-stu-id="13f34-120">Sidecar closed captions with OSMF captions plugin</span></span>
* <span data-ttu-id="13f34-121">Adobe&reg; Flash&reg; Player 11.4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="13f34-121">Adobe&reg; Flash&reg; Player 11.4 or higher.</span></span>
* <span data-ttu-id="13f34-122">Ta wersja obsługuje tylko OSMF 2.0.</span><span class="sxs-lookup"><span data-stu-id="13f34-122">This version only supports OSMF 2.0.</span></span>

## <a name="supported-features-and-known-issues"></a><span data-ttu-id="13f34-123">Obsługiwane funkcje i znane problemy</span><span class="sxs-lookup"><span data-stu-id="13f34-123">Supported features and known issues</span></span>
<span data-ttu-id="13f34-124">Aby uzyskać pełną listę obsługiwanych funkcji, nieobsługiwanych funkcji oraz znanych problemów, zapoznaj się [tego dokumentu](http://download.microsoft.com/download/3/1/B/31B63D97-574E-4A8D-BF8D-170744181724/Smooth_Streaming_Plugin_for_OSMF.pdf).</span><span class="sxs-lookup"><span data-stu-id="13f34-124">For a full list of supported features, unsupported features and known issues, refer to [this document](http://download.microsoft.com/download/3/1/B/31B63D97-574E-4A8D-BF8D-170744181724/Smooth_Streaming_Plugin_for_OSMF.pdf).</span></span>

## <a name="loading-the-plugin"></a><span data-ttu-id="13f34-125">Podczas ładowania dodatku plug-in</span><span class="sxs-lookup"><span data-stu-id="13f34-125">Loading the Plugin</span></span>
<span data-ttu-id="13f34-126">Można załadować wtyczki OSMF statycznie (w czasie kompilacji) lub dynamicznie (w czasie wykonywania).</span><span class="sxs-lookup"><span data-stu-id="13f34-126">OSMF plugins can be loaded statically (at compile time) or dynamically (at run-time).</span></span> <span data-ttu-id="13f34-127">Dodatek Smooth Streaming do pobrania OSMF obejmuje zarówno dynamicznej i statycznej wersji.</span><span class="sxs-lookup"><span data-stu-id="13f34-127">The Smooth Streaming plugin for OSMF download includes both dynamic and static versions.</span></span>

* <span data-ttu-id="13f34-128">Ładowanie statycznych: Aby załadować statycznie, jest wymagany plik biblioteki statycznej (SWC).</span><span class="sxs-lookup"><span data-stu-id="13f34-128">Static loading: To load statically, a static library (SWC) file is required.</span></span> <span data-ttu-id="13f34-129">Statyczne wtyczek są dodawane jako odwołania do projektów i dokonać scalania w pliku wyjściowego w czasie kompilacji.</span><span class="sxs-lookup"><span data-stu-id="13f34-129">Static plugins are added as a reference to the projects and merge inside the final output file at the compile time.</span></span>
* <span data-ttu-id="13f34-130">Dynamiczne ładowanie: Aby załadować dynamicznie, wymagany jest prekompilowany plik (SWF).</span><span class="sxs-lookup"><span data-stu-id="13f34-130">Dynamic loading: To load dynamically, a precompiled (SWF) file is required.</span></span> <span data-ttu-id="13f34-131">Dynamiczne dodatków plug-in są załadowane w czasie wykonywania i nie są uwzględnione w danych wyjściowych projektu.</span><span class="sxs-lookup"><span data-stu-id="13f34-131">Dynamic plugins are loaded in the runtime and not included in the project output.</span></span> <span data-ttu-id="13f34-132">(Skompilowanych danych wyjściowych) Wtyczki dynamicznej mogą być ładowane przy użyciu protokołów HTTP i plików.</span><span class="sxs-lookup"><span data-stu-id="13f34-132">(Compiled output) Dynamic plugins can be loaded using HTTP and FILE protocols.</span></span>

<span data-ttu-id="13f34-133">Aby uzyskać więcej informacji na ładowanie statycznych i dynamicznych, można znaleźć w oficjalnej [strona wtyczek OSMF](http://osmf.org/dev/osmf/OtherPDFs/osmf_plugin_dev_guide.pdf).</span><span class="sxs-lookup"><span data-stu-id="13f34-133">For more information on static and dynamic loading, see the official [OSMF plugin page](http://osmf.org/dev/osmf/OtherPDFs/osmf_plugin_dev_guide.pdf).</span></span>

### <a name="ss-for-osmf-static-loading"></a><span data-ttu-id="13f34-134">SS do ładowania statycznych OSMF</span><span class="sxs-lookup"><span data-stu-id="13f34-134">SS for OSMF Static Loading</span></span>
<span data-ttu-id="13f34-135">Poniższy fragment kodu przedstawia sposób załadować wtyczki SS statycznie dla OSMF i odtwarzanie wideo podstawowe za pomocą klasy OSMF MediaFactory.</span><span class="sxs-lookup"><span data-stu-id="13f34-135">The code snippet below shows how to load the SS plugin for OSMF statically and play a basic video using OSMF MediaFactory class.</span></span> <span data-ttu-id="13f34-136">Przed dołączeniem SS OSMF kodu, upewnij się, że odwołania projektu zawiera wtyczki statyczny "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swc".</span><span class="sxs-lookup"><span data-stu-id="13f34-136">Before including the SS for OSMF code, please ensure that the project reference includes the "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swc" static plugin.</span></span>

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

            // Create the container (sprite) for managing display and layout
            _mediaPlayerSprite = new MediaPlayerSprite();    
            _mediaPlayerSprite.addEventListener(MediaErrorEvent.MEDIA_ERROR, onPlayerFailed);
            _mediaPlayerSprite.addEventListener(MediaPlayerStateChangeEvent.MEDIA_PLAYER_STATE_CHANGE, onPlayerStateChange);
            _mediaPlayerSprite.scaleMode = ScaleMode.NONE;
            _mediaPlayerSprite.width = stage.stageWidth;
            _mediaPlayerSprite.height = stage.stageHeight;
            //Adds the container to the stage
            addChild(_mediaPlayerSprite);

            // Create a mediafactory instance
            _mediaFactory = new DefaultMediaFactory();

            // Add the listeners for PLUGIN_LOADING
            _mediaFactory.addEventListener(MediaFactoryEvent.PLUGIN_LOAD,onPluginLoaded);
            _mediaFactory.addEventListener(MediaFactoryEvent.PLUGIN_LOAD_ERROR, onPluginLoadFailed );

            // Load the plugin class 
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
            // The plugin is loaded successfully.
            // Your web server needs to host a valid crossdomain.xml file to allow plugin to download Smooth Streaming files.
        loadMediaSource("http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest")

        }

        private function onPluginLoadFailed( event:MediaFactoryEvent ):void
        {
            // The plugin is failed to load ...
        }


        private function onPlayerStateChange(event:MediaPlayerStateChangeEvent) : void
        {
            var state:String;

            state =  event.state;

            switch (state)
            {
                case MediaPlayerState.LOADING: 

                    // A new source is started to load.

                    break;

                case  MediaPlayerState.READY :   
                    // Add code to deal with Player Ready when it is hit the first load after a source is loaded. 

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
            // Take an URL of SmoothStreamingSource's manifest and add it to the page.

            var resource:URLResource= new URLResource( sourceURL );

            var element:MediaElement = _mediaFactory.createMediaElement( resource );
            _mediaPlayerSprite.scaleMode = ScaleMode.LETTERBOX;
            _mediaPlayerSprite.width = stage.stageWidth;
            _mediaPlayerSprite.height = stage.stageHeight;

            // Add the media element
            _mediaPlayerSprite.media = element;
        }     

    }
}
```


### <a name="ss-for-osmf-dynamic-loading"></a><span data-ttu-id="13f34-137">SS dla OSMF dynamiczne ładowanie</span><span class="sxs-lookup"><span data-stu-id="13f34-137">SS for OSMF Dynamic Loading</span></span>
<span data-ttu-id="13f34-138">Poniższy fragment kodu przedstawia sposób załadować wtyczki SS dla OSMF dynamicznie i odtwarzać podstawowego wideo przy użyciu klasy OSMF MediaFactory.</span><span class="sxs-lookup"><span data-stu-id="13f34-138">The code snippet below shows how to load the SS plugin for OSMF dynamically and play a basic video using the OSMF MediaFactory class.</span></span> <span data-ttu-id="13f34-139">Przed dołączeniem SS OSMF kodu, skopiuj do folderu projektu wtyczki dynamiczne "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swf", aby załadować przy użyciu protokołu pliku, lub skopiuj na serwerze sieci web, obciążenia HTTP.</span><span class="sxs-lookup"><span data-stu-id="13f34-139">Before including the SS for OSMF code, copy the "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swf" dynamic plugin to the project folder if you want to load using FILE protocol, or copy under a web server for HTTP load.</span></span> <span data-ttu-id="13f34-140">Nie istnieje potrzeba do dołączenia "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swc" odwołania do projektu.</span><span class="sxs-lookup"><span data-stu-id="13f34-140">There is no need to include "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swc" in the project references.</span></span>

<span data-ttu-id="13f34-141">{pakietu</span><span class="sxs-lookup"><span data-stu-id="13f34-141">package {</span></span>

    import flash.display.*;
    import org.osmf.media.*;
    import org.osmf.containers.MediaContainer;
    import org.osmf.events.MediaErrorEvent;
    import org.osmf.events.MediaFactoryEvent;
    import org.osmf.events.MediaPlayerStateChangeEvent;
    import org.osmf.layout.*;
    import flash.events.Event;
    import flash.system.Capabilities;


    //Sets the size of the SWF

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

            // Create the container (sprite) for managing display and layout
            _mediaPlayerSprite = new MediaPlayerSprite();    
            _mediaPlayerSprite.addEventListener(MediaErrorEvent.MEDIA_ERROR, onPlayerFailed);
            _mediaPlayerSprite.addEventListener(MediaPlayerStateChangeEvent.MEDIA_PLAYER_STATE_CHANGE, onPlayerStateChange);

            //Adds the container to the stage
            addChild(_mediaPlayerSprite);

            // Create a mediafactory instance
            _mediaFactory = new DefaultMediaFactory();

            // Add the listeners for PLUGIN_LOADING
            _mediaFactory.addEventListener(MediaFactoryEvent.PLUGIN_LOAD,onPluginLoaded);
            _mediaFactory.addEventListener(MediaFactoryEvent.PLUGIN_LOAD_ERROR, onPluginLoadFailed );

            // Load the plugin class 
            loadAdaptiveStreamingPlugin( );  

        }

        private function loadAdaptiveStreamingPlugin( ):void
        {
            var pluginResource:MediaResourceBase;
            var adaptiveStreamingPluginUrl:String;

            // Your dynamic plugin web server needs to host a valid crossdomain.xml file to allow loading plugins.

            adaptiveStreamingPluginUrl = "http://yourdomain/MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swf";
            pluginResource = new URLResource(adaptiveStreamingPluginUrl);
            _mediaFactory.loadPlugin( pluginResource ); 

        }

        private function onPluginLoaded( event:MediaFactoryEvent ):void
        {
            // The plugin is loaded successfully.

            // Your web server needs to host a valid crossdomain.xml file to allow plugin to download Smooth Streaming files.

    loadMediaSource("http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest")
        }

        private function onPluginLoadFailed( event:MediaFactoryEvent ):void
        {
            // The plugin is failed to load ...
        }


        private function onPlayerStateChange(event:MediaPlayerStateChangeEvent) : void
        {
            var state:String;

            state =  event.state;

            switch (state)
            {
                case MediaPlayerState.LOADING: 

                    // A new source is started to load.

                    break;

                case  MediaPlayerState.READY :   
                    // Add code to deal with Player Ready when it is hit the first load after a source is loaded. 

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
            // Take an URL of SmoothStreamingSource's manifest and add it to the page.

            var resource:URLResource= new URLResource( sourceURL );

            var element:MediaElement = _mediaFactory.createMediaElement( resource );
            _mediaPlayerSprite.scaleMode = ScaleMode.LETTERBOX;
            _mediaPlayerSprite.width = stage.stageWidth;
            _mediaPlayerSprite.height = stage.stageHeight;
            // Add the media element
            _mediaPlayerSprite.media = element;
        }     

    }
<span data-ttu-id="13f34-142">}</span><span class="sxs-lookup"><span data-stu-id="13f34-142">}</span></span>

## <a name="strobe-media--playback-with-the-ss-odmf-dynamic-plugin"></a><span data-ttu-id="13f34-143">Odtwarzanie multimediów światła z wtyczki dynamiczne SS ODMF</span><span class="sxs-lookup"><span data-stu-id="13f34-143">Strobe Media  Playback with the SS ODMF Dynamic Plugin</span></span>
<span data-ttu-id="13f34-144">Smooth Streaming wtyczki dynamiczne OSMF jest zgodny z [odtwarzania multimediów światła (SMP)](http://osmf.org/strobe_mediaplayback.html).</span><span class="sxs-lookup"><span data-stu-id="13f34-144">The Smooth Streaming for OSMF dynamic plugin is compatible with [Strobe Media Playback (SMP)](http://osmf.org/strobe_mediaplayback.html).</span></span> <span data-ttu-id="13f34-145">SS wtyczki OSMF służy do dodawania Smooth Streaming odtwarzanie zawartości do punktu SMP.</span><span class="sxs-lookup"><span data-stu-id="13f34-145">You can use the SS for OSMF plugin to add Smooth Streaming content playback to SMP.</span></span> <span data-ttu-id="13f34-146">Aby to zrobić, należy skopiować "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swf" na serwerze sieci web, obciążenia HTTP, wykonując następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="13f34-146">To do this, copy "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swf" under a web server for HTTP load using the following steps:</span></span>

1. <span data-ttu-id="13f34-147">Przeglądaj [strony Instalatora odtwarzanie multimediów światła](http://osmf.org/dev/2.0gm/setup.html).</span><span class="sxs-lookup"><span data-stu-id="13f34-147">Browse the [Strobe Media Playback setup page](http://osmf.org/dev/2.0gm/setup.html).</span></span> 
2. <span data-ttu-id="13f34-148">Ustaw src ze źródłem Smooth Streaming, (np. http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest)</span><span class="sxs-lookup"><span data-stu-id="13f34-148">Set the src to a Smooth Streaming source, (e.g. http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest)</span></span> 
3. <span data-ttu-id="13f34-149">Wprowadź żądane zmiany w konfiguracji, a następnie kliknij polecenie Podgląd i aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="13f34-149">Make the desired configuration changes and click Preview and Update.</span></span>
   
   <span data-ttu-id="13f34-150">**Uwaga** prawidłowy crossdomain.xml wymaga serwera zawartości sieci web.</span><span class="sxs-lookup"><span data-stu-id="13f34-150">**Note** Your content web server needs a valid crossdomain.xml.</span></span> 
4. <span data-ttu-id="13f34-151">Skopiuj i Wklej kod, aby to prosta strona HTML za pomocą edytora tekstu, takich jak w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="13f34-151">Copy and paste the code to a simple HTML page using your favorite text editor, such as in the following example:</span></span>

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



1. <span data-ttu-id="13f34-152">Dodaj wtyczkę Smooth Streaming OSMF kod osadzania i Zapisz.</span><span class="sxs-lookup"><span data-stu-id="13f34-152">Add Smooth Streaming OSMF plugin to the embed code and save.</span></span>
   
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
2. <span data-ttu-id="13f34-153">Zapisz strony HTML i opublikować na serwerze sieci web.</span><span class="sxs-lookup"><span data-stu-id="13f34-153">Save your HTML page and publish to a web server.</span></span> <span data-ttu-id="13f34-154">Przejdź do strony sieci web opublikowanych przy użyciu Twoje ulubione Flash&reg; Player włączone przeglądarki internetowej (program Internet Explorer, Chrome, Firefox, itp).</span><span class="sxs-lookup"><span data-stu-id="13f34-154">Browse to the published web page using your favorite Flash&reg; Player enabled Internet browser (Internet Explorer, Chrome, Firefox, so on).</span></span>
3. <span data-ttu-id="13f34-155">Korzystanie z funkcji Smooth Streaming zawartości wewnątrz Adobe&reg; Flash&reg; Player.</span><span class="sxs-lookup"><span data-stu-id="13f34-155">Enjoy Smooth Streaming content inside Adobe&reg; Flash&reg; Player.</span></span>

<span data-ttu-id="13f34-156">Aby uzyskać więcej informacji na ogólne programowanie OSMF, zobacz urzędnika [OSMF programowanie strony](http://osmf.org/resources.html).</span><span class="sxs-lookup"><span data-stu-id="13f34-156">For more information on general OSMF development, please see the official [OSMF development page](http://osmf.org/resources.html).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="13f34-157">Ścieżki szkoleniowe dotyczące usługi Media Services</span><span class="sxs-lookup"><span data-stu-id="13f34-157">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="13f34-158">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="13f34-158">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="13f34-159">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="13f34-159">See Also</span></span>
[<span data-ttu-id="13f34-160">Adaptacyjne przesyłanie strumieniowe wtyczki dla aktualizacji OSMF firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="13f34-160">Microsoft Adaptive Streaming Plugin for OSMF Update</span></span>](https://azure.microsoft.com/blog/2014/10/27/microsoft-adaptive-streaming-plugin-for-osmf-update/) 

