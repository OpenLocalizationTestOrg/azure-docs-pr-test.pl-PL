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
# <a name="how-toouse-hello-microsoft-smooth-streaming-plugin-for-hello-adobe-open-source-media-framework"></a>Jak tooUse hello Microsoft Smooth Streaming wtyczki dla hello Adobe Open Framework nośnika źródła
## <a name="overview"></a>Omówienie
Witaj dodatek Microsoft Smooth Streaming, otwórz źródła Media Framework w wersji 2.0 (SS dla OSMF) rozszerza możliwości domyślne hello OSMF i dodaje Microsoft Smooth Streaming toonew odtwarzanie zawartości i istniejące OSMF graczy. Dodatek Hello dodaje również Smooth Streaming tooStrobe możliwości odtwarzania multimediów odtwarzania (SMP).

SS dla OSMF obejmuje dwie wersje dodatku:

* Statyczne Smooth Streaming dodatek plug-in dla OSMF (SWC)
* Dynamiczne Smooth Streaming dodatek plug-in dla OSMF (SWF)

Tym dokumencie przyjęto założenie, że czytelnik hello ma ogólne praktyczną znajomość OSMF i OSMF dodatków plug-in. Aby uzyskać więcej informacji na temat OSMF Zobacz hello dokumentację hello [oficjalna witryna OSMF](http://osmf.org/).

### <a name="smooth-streaming-plugin-for-osmf-20"></a>Wtyczka Smooth Streaming OSMF 2.0
Dodatek Hello obsługuje ładowania i odtwarzania zawartości Smooth Streaming na żądanie z hello następujące funkcje:

* Odtwarzanie Smooth Streaming na żądanie (Wstrzymaj, wyszukiwania, Zatrzymaj odtwarzanie)
* Odtwarzanie Live Smooth Streaming (Odtwórz)
* Na żywo funkcji DVR (Wstrzymaj, wyszukiwania, odtwarzania DVR, Go Live)
* Obsługa wideo koderów-dekoderów - H.264
* Obsługę Audio koderów-dekoderów - AAC
* Wiele wersji językowych audio przełączenie OSMF wbudowanych interfejsów API
* Maksymalna liczba odtwarzania jakości wybór z interfejsami API wbudowanych OSMF
* Podpisy z wtyczki podpisy OSMF kodowane boczną
* Adobe&reg; Flash&reg; Player 11.4 lub nowszej.
* Ta wersja obsługuje tylko OSMF 2.0.

## <a name="supported-features-and-known-issues"></a>Obsługiwane funkcje i znane problemy
Aby uzyskać pełną listę obsługiwanych funkcji, nieobsługiwane funkcje i znanych problemów można znaleźć zbyt[tego dokumentu](http://download.microsoft.com/download/3/1/B/31B63D97-574E-4A8D-BF8D-170744181724/Smooth_Streaming_Plugin_for_OSMF.pdf).

## <a name="loading-hello-plugin"></a>Ładowanie hello wtyczki
Można załadować wtyczki OSMF statycznie (w czasie kompilacji) lub dynamicznie (w czasie wykonywania). Witaj Smooth Streaming wtyczki do pobrania OSMF obejmuje zarówno dynamicznej i statycznej wersji.

* Ładowanie statycznych: tooload statycznie, plik biblioteki statycznej (SWC) jest wymagana. Statyczne wtyczek są dodawane jako odwołania toohello projektów i dokonać scalania w hello ostateczne dane wyjściowe pliku w czasie kompilacji hello.
* Dynamiczne ładowanie: tooload dynamicznie, wstępnie skompilowanych plików (SWF) jest wymagana. Dynamiczne dodatków plug-in są ładowane w środowisku uruchomieniowym hello i nie są uwzględnione w danych wyjściowych projektu hello. (Skompilowanych danych wyjściowych) Wtyczki dynamicznej mogą być ładowane przy użyciu protokołów HTTP i plików.

Aby uzyskać więcej informacji na ładowanie statycznych i dynamicznych, zobacz oficjalne hello [strona wtyczek OSMF](http://osmf.org/dev/osmf/OtherPDFs/osmf_plugin_dev_guide.pdf).

### <a name="ss-for-osmf-static-loading"></a>SS do ładowania statycznych OSMF
Poniższy fragment kodu Hello pokazuje, jak tooload statycznie hello SS wtyczki dla OSMF i odtwarzanie wideo podstawowe za pomocą klasy OSMF MediaFactory. Przed dołączeniem hello SS OSMF kodu, upewnij się, że odwołania projektu hello zawiera wtyczki statycznych hello "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swc".

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


### <a name="ss-for-osmf-dynamic-loading"></a>SS dla OSMF dynamiczne ładowanie
Poniższy fragment kodu Hello pokazuje, jak tooload dynamicznie hello SS wtyczki dla OSMF i odtwarzanie wideo podstawowe za pomocą klasy OSMF MediaFactory hello. Przed dołączeniem hello SS OSMF kodu, należy skopiować folder projektu toohello dynamiczne wtyczki "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swf" hello tooload przy użyciu protokołu pliku, lub skopiować na serwerze sieci web, obciążenia HTTP. Nie ma żadnych tooinclude potrzeby "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swc" w odwołaniach projektu hello.

{pakietu

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
}

## <a name="strobe-media--playback-with-hello-ss-odmf-dynamic-plugin"></a>Odtwarzanie multimediów światła z hello wtyczki dynamiczne ODMF SS
Hello Smooth Streaming wtyczki dynamiczne OSMF jest zgodny z [odtwarzania multimediów światła (SMP)](http://osmf.org/strobe_mediaplayback.html). Hello SS służy do odtwarzania zawartości Smooth Streaming programu OSMF wtyczki tooadd tooSMP. toodo, kopii "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swf" na serwerze sieci web dla obciążenia HTTP przy użyciu hello następujące kroki:

1. Przeglądaj hello [strony Instalatora odtwarzanie multimediów światła](http://osmf.org/dev/2.0gm/setup.html). 
2. Ustaw hello src tooa Smooth Streaming źródła (np. http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest) 
3. Hello potrzeby zmian konfiguracji, a następnie kliknij polecenie Podgląd i aktualizacji.
   
   **Uwaga** prawidłowy crossdomain.xml wymaga serwera zawartości sieci web. 
4. Skopiuj i Wklej hello tooa proste HTML strony kodowej w hello poniższy przykład za pomocą edytora tekstu, takich jak:

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



1. Dodaj toohello wtyczki Smooth Streaming OSMF kod osadzania i Zapisz.
   
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
2. Zapisz strony HTML i opublikuj tooa serwera sieci web. Przeglądaj toohello opublikowane strony sieci web przy użyciu Twoje ulubione Flash&reg; Player włączone przeglądarki internetowej (program Internet Explorer, Chrome, Firefox, itp).
3. Korzystanie z funkcji Smooth Streaming zawartości wewnątrz Adobe&reg; Flash&reg; Player.

Aby uzyskać więcej informacji na ogólne programowanie OSMF, zobacz oficjalne hello [OSMF programowanie strony](http://osmf.org/resources.html).

## <a name="media-services-learning-paths"></a>Ścieżki szkoleniowe dotyczące usługi Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Przekazywanie opinii
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>Zobacz też
[Adaptacyjne przesyłanie strumieniowe wtyczki dla aktualizacji OSMF firmy Microsoft](https://azure.microsoft.com/blog/2014/10/27/microsoft-adaptive-streaming-plugin-for-osmf-update/) 

