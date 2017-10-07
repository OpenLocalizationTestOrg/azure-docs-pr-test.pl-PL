---
title: Samouczek aplikacji Sklepu Windows Streaming aaaSmooth | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toouse usługi Azure Media Services toocreate aplikacją ze Sklepu Windows w języku C# z XML MediaElement kontrolować tooplayback Smooth Stream zawartości."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 0fa5d8c5-3d5f-4886-ae55-fb6de4f5256d
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/11/2017
ms.author: juliako
ms.openlocfilehash: b02aa2c7f68fe22a23ea846d72fdd23bfba2b19c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toobuild-a-smooth-streaming-windows-store-application"></a>Jak tooBuild Smooth Streaming aplikację ze Sklepu Windows

Witaj Smooth Streaming klienta zestawu SDK dla systemu Windows 8 umożliwia deweloperom toobuild aplikacji ze Sklepu Windows, które można odtwarzać zawartości na żądanie i na żywo Smooth Streaming. Ponadto toohello podstawowe odtwarzania programu Smooth Streaming zawartości, hello SDK również zapewnia zaawansowane funkcje, takie jak Microsoft PlayReady ochrony ograniczenie poziomu jakości, Live DVR, strumieniem audio przełączania, nasłuchiwanie aktualizacji stanu (np. zmiany poziomu jakości ) i zdarzeń błędu i tak dalej. Aby uzyskać więcej informacji na powitania obsługiwanych funkcji, zobacz hello [informacje o wersji](http://www.iis.net/learn/media/smooth-streaming/smooth-streaming-client-sdk-for-windows-8-release-notes). Aby uzyskać więcej informacji, zobacz [Framework Player dla systemu Windows 8](http://playerframework.codeplex.com/). 

Ten samouczek zawiera cztery lekcje:

1. Tworzenie podstawowej płynnego przesyłania strumieniowego aplikacji sklepu
2. Dodaj suwaka hello tooControl postępu nośnika
3. Wybierz Smooth Streaming strumieni
4. Wybierz Smooth Streaming ścieżki

## <a name="prerequisites"></a>Wymagania wstępne
* Windows 8, 32-bitowy lub 64-bitowej. Możesz uzyskać [systemu Windows 8 Enterprise Evaluation](http://msdn.microsoft.com/evalcenter/jj554510.aspx) w witrynie MSDN.
* Program Visual Studio 2012 lub Visual Studio Express 2012 (lub nowszy). Można uzyskać wersji próbnej hello z [tutaj](http://www.microsoft.com/visualstudio/11/downloads).
* [Microsoft Smooth Streaming Client zestawu SDK dla systemu Windows 8](http://visualstudiogallery.msdn.microsoft.com/04423d13-3b3e-4741-a01c-1ae29e84fea6?SRC=Homehttp://visualstudiogallery.msdn.microsoft.com/04423d13-3b3e-4741-a01c-1ae29e84fea6?SRC=Home).

rozwiązanie ukończyć powitalnych dla każdej lekcji można pobrać z przykładów kodu deweloperów MSDN (Galeria kodu): 

* [Lekcja 1](http://code.msdn.microsoft.com/Smooth-Streaming-Client-0bb1471f) — sprawne prostego systemu Windows 8 przesyłania strumieniowego Media Player 
* [Lekcja 2](http://code.msdn.microsoft.com/A-simple-Windows-8-Smooth-ee98f63a) — sprawne prostego systemu Windows 8 przesyłania strumieniowego Media Player paska suwaka formantu 
* [Lekcja 3](http://code.msdn.microsoft.com/A-Windows-8-Smooth-883c3b44) — sprawne systemu Windows 8 przesyłania strumieniowego Media Player do wyboru strumienia  
* [Lekcja 4](http://code.msdn.microsoft.com/A-Windows-8-Smooth-aa9e4907) — sprawne systemu Windows 8 przesyłania strumieniowego Media Player śledzenie zaznaczenia.

## <a name="lesson-1-create-a-basic-smooth-streaming-store-application"></a>Lekcja 1: Tworzenie podstawowej płynnego przesyłania strumieniowego aplikacji sklepu

W tej lekcji utworzysz aplikacji Sklepu Windows za pomocą MediaElement kontroli tooplay Smooth strumienia zawartości.  działającej aplikacji Hello wygląda następująco:

![Przykładowa aplikacja Sklepu Windows Smooth Streaming][PlayerApplication]

Aby uzyskać więcej informacji na temat tworzenia aplikacji Sklepu Windows, temacie [tworzenie wspaniałych aplikacji dla systemu Windows 8](http://msdn.microsoft.com/windows/apps/br229512.aspx). Tej lekcji zawiera hello następujące procedury:

1. Tworzenie projektu ze Sklepu Windows
2. Projektowanie interfejsu użytkownika hello (XAML)
3. Modyfikowanie pliku CodeBehind hello
4. Kompilowanie i testowanie aplikacji hello

**toocreate projektu ze Sklepu Windows**

1. Uruchom program Visual Studio 2012 lub nowszym.
2. Z hello **pliku** menu, kliknij przycisk **nowy**, a następnie kliknij przycisk **projektu**.
3. W oknie dialogowym Nowy projekt hello wpisz lub wybierz hello następujące wartości:

| Nazwa | Wartość |
| --- | --- |
| Grupa szablonów |Zainstalowane/szablony/Visual C# / ze Sklepu Windows |
| Szablon |Pusta aplikacja (XAML) |
| Nazwa |SSPlayer |
| Lokalizacja |C:\SSTutorials |
| Nazwa rozwiązania |SSPlayer |
| Utwórz katalog rozwiązania |(wybrane) |

1. Kliknij przycisk **OK**.

**tooadd toohello odwołania Smooth Streaming Client SDK**

1. W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy **SSPlayer**, a następnie kliknij przycisk **Dodaj odwołanie**.
2. Wpisz lub wybierz hello następujące wartości:

| Nazwa | Wartość |
| --- | --- |
| Grupy odwołania |Rozszerzenia/systemu Windows |
| Dokumentacja |Wybierz Microsoft Smooth Streaming Client zestawu SDK dla systemu Windows 8 i Microsoft Visual C++ Runtime Package |

1. Kliknij przycisk **OK**. 

Po dodaniu odwołań hello, musisz wybrać platformy docelowe hello (x64 lub x86), Dodawanie odwołania nie będą działać dla konfiguracji platformy dowolnego Procesora.  W Eksploratorze rozwiązań pojawi się żółty znak ostrzeżenie tych dodać odwołań.

**Interfejs użytkownika player hello toodesign**

1. W Eksploratorze rozwiązań kliknij dwukrotnie kliknij **MainPage.xaml** tooopen go w projekcie hello wyświetlić.
2. Zlokalizuj hello  **&lt;siatki&gt;**  i  **&lt;/Grid&gt;**  tagi hello pliku XAML, a następnie wklej hello poniższy kod między tagami hello dwa:

         <Grid.RowDefinitions>

            <RowDefinition Height="20"/>    <!-- spacer -->
            <RowDefinition Height="50"/>    <!-- media controls -->
            <RowDefinition Height="100*"/>  <!-- media element -->
            <RowDefinition Height="80*"/>   <!-- media stream and track selection -->
            <RowDefinition Height="50"/>    <!-- status bar -->
         </Grid.RowDefinitions>

         <StackPanel Name="spMediaControl" Grid.Row="1" Orientation="Horizontal">
            <TextBlock x:Name="tbSource" Text="Source :  " FontSize="16" FontWeight="Bold" VerticalAlignment="Center" />
            <TextBox x:Name="txtMediaSource" Text="http://ecn.channel9.msdn.com/o9/content/smf/smoothcontent/elephantsdream/Elephants_Dream_1024-h264-st-aac.ism/manifest" FontSize="10" Width="700" Margin="0,4,0,10" />
            <Button x:Name="btnSetSource" Content="Set Source" Width="111" Height="43" Click="btnSetSource_Click"/>
            <Button x:Name="btnPlay" Content="Play" Width="111" Height="43" Click="btnPlay_Click"/>
            <Button x:Name="btnPause" Content="Pause"  Width="111" Height="43" Click="btnPause_Click"/>
            <Button x:Name="btnStop" Content="Stop"  Width="111" Height="43" Click="btnStop_Click"/>
            <CheckBox x:Name="chkAutoPlay" Content="Auto Play" Height="55" Width="Auto" IsChecked="{Binding AutoPlay, ElementName=mediaElement, Mode=TwoWay}"/>
            <CheckBox x:Name="chkMute" Content="Mute" Height="55" Width="67" IsChecked="{Binding IsMuted, ElementName=mediaElement, Mode=TwoWay}"/>
         </StackPanel>

         <StackPanel Name="spMediaElement" Grid.Row="2" Height="435" Width="1072"
                    HorizontalAlignment="Center" VerticalAlignment="Center">
            <MediaElement x:Name="mediaElement" Height="356" Width="924" MinHeight="225"
                          HorizontalAlignment="Center" VerticalAlignment="Center" 
                          AudioCategory="BackgroundCapableMedia" />
            <StackPanel Orientation="Horizontal">
                <Slider x:Name="sliderProgress" Width="924" Height="44"
                        HorizontalAlignment="Center" VerticalAlignment="Center"
                        PointerPressed="sliderProgress_PointerPressed"/>
                <Slider x:Name="sliderVolume" 
                        HorizontalAlignment="Right" VerticalAlignment="Center" Orientation="Vertical" 
                        Height="79" Width="148" Minimum="0" Maximum="1" StepFrequency="0.1" 
                        Value="{Binding Volume, ElementName=mediaElement, Mode=TwoWay}" 
                        ToolTipService.ToolTip="{Binding Value, RelativeSource={RelativeSource Mode=Self}}"/>
            </StackPanel>
         </StackPanel>

         <StackPanel Name="spStatus" Grid.Row="4" Orientation="Horizontal">
            <TextBlock x:Name="tbStatus" Text="Status :  " 
               FontSize="16" FontWeight="Bold" VerticalAlignment="Center" HorizontalAlignment="Center" />
            <TextBox x:Name="txtStatus" FontSize="10" Width="700" VerticalAlignment="Center"/>
         </StackPanel>
   
   Hello Formant MediaElement jest używane tooplayback nośnika. Kontrolka suwaka Hello o nazwie sliderProgress będzie służyć trwa hello dalej lekcji toocontrol hello nośnika.
3. Naciśnij klawisz **CTRL + S** toosave hello pliku.

Hello Formant MediaElement nie obsługuje funkcji Smooth Streaming zawartości out-of-box. Obsługa Smooth Streaming hello tooenable należy zarejestrować obsługi hello strumień bajtów Smooth Streaming przez rozszerzenie nazwy pliku i typ MIME.  tooregister, należy użyć metody MediaExtensionManager.RegisterByteStremHandler hello hello Windows.Media w przestrzeni nazw.

W tym pliku XAML niektóre programy obsługi zdarzeń skojarzonych z hello kontrolki.  Należy zdefiniować te programy obsługi zdarzeń.

**toomodify hello kodzie pliku**

1. W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy **MainPage.xaml**, a następnie kliknij przycisk **kod widoku**.
2. U góry pliku hello hello, Dodaj następujące hello instrukcję using:
   
        using Windows.Media;
3. Na początku hello hello **MainPage** klasy, Dodaj hello następującego elementu członkowskiego danych:
   
         private MediaExtensionManager extensions = new MediaExtensionManager();
4. Na końcu hello hello **MainPage** konstruktora, Dodaj hello następujące dwa wiersze:
   
        extensions.RegisterByteStreamHandler("Microsoft.Media.AdaptiveStreaming.SmoothByteStreamHandler", ".ism", "text/xml");
        extensions.RegisterByteStreamHandler("Microsoft.Media.AdaptiveStreaming.SmoothByteStreamHandler", ".ism", "application/vnd.ms-sstr+xml");
5. Na końcu hello hello **MainPage** klasy, Wklej hello następującego kodu:
   
         # region UI Button Click Events
         private void btnPlay_Click(object sender, RoutedEventArgs e)
         {

         mediaElement.Play();
         txtStatus.Text = "MediaElement is playing ...";
         }
         private void btnPause_Click(object sender, RoutedEventArgs e)
         {

         mediaElement.Pause();
         txtStatus.Text = "MediaElement is paused";
         }
         private void btnSetSource_Click(object sender, RoutedEventArgs e)
         {

         sliderProgress.Value = 0;
         mediaElement.Source = new Uri(txtMediaSource.Text);

         if (chkAutoPlay.IsChecked == true)
         {
             txtStatus.Text = "MediaElement is playing ...";
         }
         else
         {
             txtStatus.Text = "Click hello Play button tooplay hello media source.";
         }
         }
         private void btnStop_Click(object sender, RoutedEventArgs e)
         {

         mediaElement.Stop();
         txtStatus.Text = "MediaElement is stopped";
         }
         private void sliderProgress_PointerPressed(object sender, PointerRoutedEventArgs e)
         {

         txtStatus.Text = "Seek tooposition " + sliderProgress.Value;
         mediaElement.Position = new TimeSpan(0, 0, (int)(sliderProgress.Value));
         }
         # endregion

Program obsługi zdarzeń sliderProgress_PointerPressed Hello jest zdefiniowany w tym miejscu.  Istnieje więcej tooget toodo works pracy, który będzie uwzględnione w następnej lekcji hello tego samouczka.
6. Naciśnij klawisz **CTRL + S** toosave hello pliku.

Witaj hello gotowym kodzie pliku powinna wyglądać następująco:

![Codeview w aplikacji Visual Studio programu Smooth Streaming Sklepu Windows][CodeViewPic]

**toocompile i testowania aplikacji hello**

1. Z hello **kompilacji** menu, kliknij przycisk **programu Configuration Manager**.
2. Zmień **platformy aktywne rozwiązanie** toomatch rozwoju platformy.
3. Naciśnij klawisz **F6** toocompile hello projektu. 
4. Naciśnij klawisz **F5** toorun hello aplikacji.
5. U góry hello aplikacji hello możesz użyć domyślnej hello Smooth Streaming URL lub wprowadź inną. 
6. Kliknij przycisk **Ustaw źródło**. Ponieważ **Auto-odtwarzanie** jest włączona domyślnie hello nośnika jest odtwarzany automatycznie.  Można kontrolować hello nośnika przy użyciu hello **odtwarzanie**, **Wstrzymaj** i **zatrzymać** przycisków.  Można kontrolować hello nośnika woluminu przy użyciu hello pionowej kontrolce slider.  Jednak hello suwak poziomy kontroli powitalne postępu nośnika nie jest całkowicie jeszcze zaimplementowane. 

Lesson1 została ukończona.  W tej lekcji służy element MediaElement kontroli tooplayback Smooth Streaming zawartości.  W następnej lekcji hello doda postęp hello toocontrol suwaka hello Smooth Streaming zawartości.

## <a name="lesson-2-add-a-slider-bar-toocontrol-hello-media-progress"></a>Lekcja 2: Dodaj suwaka hello tooControl postępu nośnika

W lekcji 1 zostały utworzone z tooplayback kontrolki MediaElement XAML Smooth Streaming zawartości multimedialnej aplikacji Sklepu Windows.  Pochodzi niektórych funkcji podstawowych nośników, takich jak start, stop i wstrzymania.  W tej lekcji spowoduje dodanie aplikacji toohello formantów paska suwaka.

W tym samouczku używamy pozycji suwaka hello tooupdate czasomierza oparte na bieżącej pozycji hello hello Formant MediaElement.  suwak Hello start i czas zakończenia również toobe należy zaktualizować w przypadku zawartości na żywo.  Mogą być lepiej obsłużone w hello adaptacyjną źródła aktualizacji zdarzeń.

Źródeł multimediów to obiekty, które generować dane do nośnika.  Witaj źródła programu rozpoznawania nazw przyjmujący element stream adres URL lub bajt i tworzy hello odpowiedni nośnik źródła dla tej zawartości.  Program rozpoznawania nazw Hello źródła jest hello standardowy sposób dla źródeł multimediów toocreate aplikacji hello. 

Tej lekcji zawiera hello następujące procedury:

1. Zarejestrować hello Smooth Streaming obsługi 
2. Dodać obsługę zdarzeń poziomu Menedżera źródła adaptacyjną hello
3. Dodaj programy obsługi zdarzeń na poziomie adaptacyjną źródła hello
4. Dodaj element MediaElement procedury obsługi zdarzeń
5. Dodaj suwaka kodu powiązanego
6. Kompilowanie i testowanie aplikacji hello

**tooregister hello strumień bajtów Smooth Streaming obsługi i przekazać hello propertyset**

1. W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy **MainPage.xaml**, a następnie kliknij przycisk **kod widoku**.
2. Na początku hello pliku hello, Dodaj następujące hello instrukcję using:

        using Microsoft.Media.AdaptiveStreaming;
3. Na początku hello hello klasy MainPage, Dodaj hello następujące elementy członkowskie danych:

         private Windows.Foundation.Collections.PropertySet propertySet = new Windows.Foundation.Collections.PropertySet();             
         private IAdaptiveSourceManager adaptiveSourceManager;
4. Witaj wewnątrz **MainPage** konstruktora, Dodaj hello następującego kodu po hello **to. Inicjowanie Components();**  wiersza i hello rejestracji kodu wierszach w poprzedniej lekcji hello:

        // Gets hello default instance of AdaptiveSourceManager which manages Smooth 
        //Streaming media sources.
        adaptiveSourceManager = AdaptiveSourceManager.GetDefault();
        // Sets property key value tooAdaptiveSourceManager default instance.
        // {A5CE1DE8-1D00-427B-ACEF-FB9A3C93DE2D}" must be hardcoded.
        propertySet["{A5CE1DE8-1D00-427B-ACEF-FB9A3C93DE2D}"] = adaptiveSourceManager;
5. Witaj wewnątrz **MainPage** konstruktora, zmodyfikuj Witaj dwie RegisterByteStreamHandler metody tooadd Witaj określonymi parametry:

         // Registers Smooth Streaming byte-stream handler for ".ism" extension and, 
         // "text/xml" and "application/vnd.ms-ss" mime-types and pass hello propertyset. 
         // http://*.ism/manifest URI resources will be resolved by Byte-stream handler.
         extensions.RegisterByteStreamHandler(

            "Microsoft.Media.AdaptiveStreaming.SmoothByteStreamHandler", 
            ".ism", 
            "text/xml", 
            propertySet );
         extensions.RegisterByteStreamHandler(

            "Microsoft.Media.AdaptiveStreaming.SmoothByteStreamHandler", 
            ".ism", 
            "application/vnd.ms-sstr+xml", 
         propertySet);
6. Naciśnij klawisz **CTRL + S** toosave hello pliku.

**Program obsługi zdarzeń na poziomie menedżera tooadd hello adaptacyjną źródła**

1. W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy **MainPage.xaml**, a następnie kliknij przycisk **kod widoku**.
2. Witaj wewnątrz **MainPage** klasy, Dodaj hello następującego elementu członkowskiego danych:
   
     prywatne adaptiveSource AdaptiveSource = null;
3. Na końcu hello hello **MainPage** klasy, Dodaj powitania po obsługi zdarzeń:
   
         # region Adaptive Source Manager Level Events
         private void mediaElement_AdaptiveSourceOpened(AdaptiveSource sender, AdaptiveSourceOpenedEventArgs args)
         {

            adaptiveSource = args.AdaptiveSource;
         }

         # endregion Adaptive Source Manager Level Events
4. Na końcu hello hello **MainPage** konstruktora, Dodaj następujące zdarzenia otwarte adaptacyjną źródłowego toohello toosubscribe wiersza hello:
   
         adaptiveSourceManager.AdaptiveSourceOpenedEvent += 
           new AdaptiveSourceOpenedEventHandler(mediaElement_AdaptiveSourceOpened);
5. Naciśnij klawisz **CTRL + S** toosave hello pliku.

**programy obsługi zdarzeń na poziomie adaptacyjną źródła tooadd**

1. W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy **MainPage.xaml**, a następnie kliknij przycisk **kod widoku**.
2. Witaj wewnątrz **MainPage** klasy, Dodaj hello następującego elementu członkowskiego danych:
   
     prywatne adaptiveSourceStatusUpdate AdaptiveSourceStatusUpdatedEventArgs;   prywatne manifestObject manifestu;
3. Na końcu hello hello **MainPage** klasy, Dodaj hello następujące procedury obsługi zdarzeń:

         # region Adaptive Source Level Events
         private void mediaElement_ManifestReady(AdaptiveSource sender, ManifestReadyEventArgs args)
         {

            adaptiveSource = args.AdaptiveSource;
            manifestObject = args.AdaptiveSource.Manifest;
         }

         private void mediaElement_AdaptiveSourceStatusUpdated(AdaptiveSource sender, AdaptiveSourceStatusUpdatedEventArgs args)
         {

            adaptiveSourceStatusUpdate = args;
         }

         private void mediaElement_AdaptiveSourceFailed(AdaptiveSource sender, AdaptiveSourceFailedEventArgs args)
         {

            txtStatus.Text = "Error: " + args.HttpResponse;
         }

         # endregion Adaptive Source Level Events
4. Na końcu hello hello **mediaElement AdaptiveSourceOpened** metody, Dodaj następujące zdarzenia toohello toosubscribe kodu hello:
   
         adaptiveSource.ManifestReadyEvent +=

                    mediaElement_ManifestReady;
         adaptiveSource.AdaptiveSourceStatusUpdatedEvent += 

            mediaElement_AdaptiveSourceStatusUpdated;
         adaptiveSource.AdaptiveSourceFailedEvent += 

            mediaElement_AdaptiveSourceFailed;
5. Naciśnij klawisz **CTRL + S** toosave hello pliku.

Witaj, które same zdarzenia są dostępne na adaptacyjną Menedżer poziom źródła również, która może służyć do obsługi funkcji typowe tooall nośnika elementy w aplikacji hello. Każdy AdaptiveSource zawiera własnych zdarzeń i wszystkie zdarzenia AdaptiveSource będzie kaskadowych w obszarze AdaptiveSourceManager.

**programy obsługi zdarzeń elementu mediów tooadd**

1. W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy **MainPage.xaml**, a następnie kliknij przycisk **kod widoku**.
2. Na końcu hello hello **MainPage** klasy, Dodaj hello następujące procedury obsługi zdarzeń:

         # region Media Element Event Handlers
         private void MediaOpened(object sender, RoutedEventArgs e)
         {

            txtStatus.Text = "MediaElement opened";
         }

         private void MediaFailed(object sender, ExceptionRoutedEventArgs e)
         {

            txtStatus.Text= "MediaElement failed: " + e.ErrorMessage;
         }

         private void MediaEnded(object sender, RoutedEventArgs e)
         {

            txtStatus.Text ="MediaElement ended.";
         }

         # endregion Media Element Event Handlers
3. Na końcu hello hello **MainPage** konstruktora, Dodaj następujące zdarzenia toohello toosubscript kodu hello:

         mediaElement.MediaOpened += MediaOpened;
         mediaElement.MediaEnded += MediaEnded;
         mediaElement.MediaFailed += MediaFailed;
4. Naciśnij klawisz **CTRL + S** toosave hello pliku.

**suwak tooadd powiązane kodu kreskowego**

1. W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy **MainPage.xaml**, a następnie kliknij przycisk **kod widoku**.
2. Na początku hello pliku hello, Dodaj następujące hello instrukcję using:
      
        using Windows.UI.Core;
3. Witaj wewnątrz **MainPage** klasy, Dodaj następujące elementy członkowskie danych hello:
   
         public static CoreDispatcher _dispatcher;
         private DispatcherTimer sliderPositionUpdateDispatcher;
4. Na końcu hello hello **MainPage** konstruktora, Dodaj hello następującego kodu:
   
         _dispatcher = Window.Current.Dispatcher;
         PointerEventHandler pointerpressedhandler = new PointerEventHandler(sliderProgress_PointerPressed);
         sliderProgress.AddHandler(Control.PointerPressedEvent, pointerpressedhandler, true);    
5. Na końcu hello hello **MainPage** klasy, Dodaj hello następującego kodu:

         # region sliderMediaPlayer
         private double SliderFrequency(TimeSpan timevalue)
         {

            long absvalue = 0;
            double stepfrequency = -1;

            if (manifestObject != null)
            {
                absvalue = manifestObject.Duration - (long)manifestObject.StartTime;
            }
            else
            {
                absvalue = mediaElement.NaturalDuration.TimeSpan.Ticks;
            }

            TimeSpan totalDVRDuration = new TimeSpan(absvalue);

            if (totalDVRDuration.TotalMinutes >= 10 && totalDVRDuration.TotalMinutes < 30)
            {
               stepfrequency = 10;
            }
            else if (totalDVRDuration.TotalMinutes >= 30 
                     && totalDVRDuration.TotalMinutes < 60)
            {
                stepfrequency = 30;
            }
            else if (totalDVRDuration.TotalHours >= 1)
            {
                stepfrequency = 60;
            }

            return stepfrequency;
         }

         void updateSliderPositionoNTicks(object sender, object e)
         {

            sliderProgress.Value = mediaElement.Position.TotalSeconds;
         }

         public void setupTimer()
         {

            sliderPositionUpdateDispatcher = new DispatcherTimer();
            sliderPositionUpdateDispatcher.Interval = new TimeSpan(0, 0, 0, 0, 300);
            startTimer();
         }

         public void startTimer()
         {

            sliderPositionUpdateDispatcher.Tick += updateSliderPositionoNTicks;
            sliderPositionUpdateDispatcher.Start();
         }

         // Slider start and end time must be updated in case of live content
         public async void setSliderStartTime(long startTime)
         {

            await _dispatcher.RunAsync(CoreDispatcherPriority.Normal, () =>
            {
                TimeSpan timespan = new TimeSpan(adaptiveSourceStatusUpdate.StartTime);
                double absvalue = (int)Math.Round(timespan.TotalSeconds, MidpointRounding.AwayFromZero);
                sliderProgress.Minimum = absvalue;
            });
         }

         // Slider start and end time must be updated in case of live content
         public async void setSliderEndTime(long startTime)
         {

            await _dispatcher.RunAsync(CoreDispatcherPriority.Normal, () =>
            {
                TimeSpan timespan = new TimeSpan(adaptiveSourceStatusUpdate.EndTime);
                double absvalue = (int)Math.Round(timespan.TotalSeconds, MidpointRounding.AwayFromZero);
                sliderProgress.Maximum = absvalue;
            });
         }

         # endregion sliderMediaPlayer
      
>[!NOTE]
>CoreDispatcher jest zmian używanych toomake wątku toohello interfejsu użytkownika z wątku interfejsu użytkownika innych niż. W przypadku "wąskie gardło" na Wątek dyspozytora developer można wybrać dyspozytora toouse pod warunkiem przez element interfejsu użytkownika, że jego zamierza tooupdate.  Na przykład:
   
         await sliderProgress.Dispatcher.RunAsync(CoreDispatcherPriority.Normal, () => { TimeSpan 

         timespan = new TimeSpan(adaptiveSourceStatusUpdate.EndTime); 
         double absvalue  = (int)Math.Round(timespan.TotalSeconds, MidpointRounding.AwayFromZero); 

         sliderProgress.Maximum = absvalue; }); 
6. Na końcu hello hello **mediaElement_AdaptiveSourceStatusUpdated** metody, Dodaj hello następującego kodu:

         setSliderStartTime(args.StartTime);
         setSliderEndTime(args.EndTime);
7. Na końcu hello hello **MediaOpened** metody, Dodaj hello następującego kodu:

         sliderProgress.StepFrequency = SliderFrequency(mediaElement.NaturalDuration.TimeSpan);
         sliderProgress.Width = mediaElement.Width;
         setupTimer();
8. Naciśnij klawisz **CTRL + S** toosave hello pliku.

**toocompile i testowania aplikacji hello**

1. Naciśnij klawisz **F6** toocompile hello projektu. 
2. Naciśnij klawisz **F5** toorun hello aplikacji.
3. U góry hello aplikacji hello możesz użyć domyślnej hello Smooth Streaming URL lub wprowadź inną. 
4. Kliknij przycisk **Ustaw źródło**. 
5. Test hello paska suwaka.

Lekcja 2 została ukończona.  W tej lekcji dodano tooapplication suwaka. 

## <a name="lesson-3-select-smooth-streaming-streams"></a>Lekcja 3: Wybierz Smooth Streaming strumieni
Smooth Streaming jest funkcją toostream zawartości z wielu ścieżek audio języka, które można wybrać przez hello przeglądarki.  W tej lekcji spowoduje włączenie strumienie tooselect przeglądarki. Tej lekcji zawiera hello następujące procedury:

1. Modyfikowanie pliku XAML hello
2. Modyfikowanie pliku behand kodu hello
3. Kompilowanie i testowanie aplikacji hello

**Plik XAML hello toomodify**

1. W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy **MainPage.xaml**, a następnie kliknij przycisk **Widok projektanta**.
2. Zlokalizuj &lt;Grid.RowDefinitions&gt;i zmodyfikować hello RowDefinitions, aby ich wygląda następująco:
   
         <Grid.RowDefinitions>            
            <RowDefinition Height="20"/>
            <RowDefinition Height="50"/>
            <RowDefinition Height="100"/>
            <RowDefinition Height="80"/>
            <RowDefinition Height="50"/>
         </Grid.RowDefinitions>
3. Witaj wewnątrz &lt;siatki&gt;&lt;/Grid&gt; tagów, Dodaj hello poniższy kod toodefine kontrolki listbox, aby użytkownicy mogli widzieć hello listę dostępnych strumieni i wybierz strumieni:

         <Grid Name="gridStreamAndBitrateSelection" Grid.Row="3">
            <Grid.RowDefinitions>
                <RowDefinition Height="300"/>
            </Grid.RowDefinitions>
            <Grid.ColumnDefinitions>
                <ColumnDefinition Width="250*"/>
                <ColumnDefinition Width="250*"/>
            </Grid.ColumnDefinitions>
            <StackPanel Name="spStreamSelection" Grid.Row="1" Grid.Column="0">
                <StackPanel Orientation="Horizontal">
                    <TextBlock Name="tbAvailableStreams" Text="Available Streams:" FontSize="16" VerticalAlignment="Center"></TextBlock>
                    <Button Name="btnChangeStreams" Content="Submit" Click="btnChangeStream_Click"/>
                </StackPanel>
                <ListBox x:Name="lbAvailableStreams" Height="200" Width="200" Background="Transparent" HorizontalAlignment="Left" 
                    ScrollViewer.VerticalScrollMode="Enabled" ScrollViewer.VerticalScrollBarVisibility="Visible">
                    <ListBox.ItemTemplate>
                        <DataTemplate>
                            <CheckBox Content="{Binding Name}" IsChecked="{Binding isChecked, Mode=TwoWay}" />
                        </DataTemplate>
                    </ListBox.ItemTemplate>
                </ListBox>
            </StackPanel>
         </Grid>
4. Naciśnij klawisz **CTRL + S** toosave hello zmiany.

**toomodify hello kodzie pliku**

1. W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy **MainPage.xaml**, a następnie kliknij przycisk **kod widoku**.
2. W obszarze nazw SSPlayer hello Dodaj nową klasę:
   
        #region class Stream
   
        public class Stream
        {
            private IManifestStream stream;
            public bool isCheckedValue;
            public string name;
   
            public string Name
            {
                get { return name; }
                set { name = value; }
            }
   
            public IManifestStream ManifestStream
            {
                get { return stream; }
                set { stream = value; }
            }
   
            public bool isChecked
            {
                get { return isCheckedValue; }
                set
                {
                    // mMke hello video stream always checked.
                    if (stream.Type == MediaStreamType.Video)
                    {
                        isCheckedValue = true;
                    }
                    else
                    {
                        isCheckedValue = value;
                    }
                }
            }
   
            public Stream(IManifestStream streamIn)
            {
                stream = streamIn;
                name = stream.Name;
            }
        }
        #endregion class Stream
3. Na początku hello hello klasy MainPage, Dodaj hello następujące definicje zmiennych:
   
         private List<Stream> availableStreams;
         private List<Stream> availableAudioStreams;
         private List<Stream> availableTextStreams;
         private List<Stream> availableVideoStreams;
4. Wewnątrz klasy MainPage hello Dodaj powitania od regionu:
   
        #region stream selection
        ///<summary>
        ///Functionality tooselect streams from IManifestStream available streams
        /// </summary>
   
        // This function is called from hello mediaElement_ManifestReady event handler 
        // tooretrieve hello streams and populate them toohello local data members.
        public void getStreams(Manifest manifestObject)
        {
            availableStreams = new List<Stream>();
            availableVideoStreams = new List<Stream>();
            availableAudioStreams = new List<Stream>();
            availableTextStreams = new List<Stream>();
   
            try
            {
                for (int i = 0; i<manifestObject.AvailableStreams.Count; i++)
                {
                    Stream newStream = new Stream(manifestObject.AvailableStreams[i]);
                    newStream.isChecked = false;
   
                    //populate hello stream lists based on hello types
                    availableStreams.Add(newStream);
   
                    switch (newStream.ManifestStream.Type)
                    {
                        case MediaStreamType.Video:
                            availableVideoStreams.Add(newStream);
                            break;
                        case MediaStreamType.Audio:
                            availableAudioStreams.Add(newStream);
                            break;
                        case MediaStreamType.Text:
                            availableTextStreams.Add(newStream);
                            break;
                    }
   
                    // Select hello default selected streams from hello manifest.
                    for (int j = 0; j<manifestObject.SelectedStreams.Count; j++)
                    {
                        string selectedStreamName = manifestObject.SelectedStreams[j].Name;
                        if (selectedStreamName.Equals(newStream.Name))
                        {
                            newStream.isChecked = true;
                            break;
                        }
                    }
                }
            }
            catch (Exception e)
            {
                txtStatus.Text = "Error: " + e.Message;
            }
        }
   
        // This function set hello list box ItemSource
        private async void refreshAvailableStreamsListBoxItemSource()
        {
            try
            {
                //update hello stream check box list on hello UI
                await _dispatcher.RunAsync(CoreDispatcherPriority.Normal, ()
                    => { lbAvailableStreams.ItemsSource = availableStreams; });
            }
            catch (Exception e)
            {
                txtStatus.Text = "Error: " + e.Message;
            }
        }
   
        // This function creates a selected streams list
        private void createSelectedStreamsList(List<IManifestStream> selectedStreams)
        {
            bool isOneVideoSelected = false;
            bool isOneAudioSelected = false;
   
            // Only one video stream can be selected
            for (int j = 0; j<availableVideoStreams.Count; j++)
            {
                if (availableVideoStreams[j].isChecked && (!isOneVideoSelected))
                {
                    selectedStreams.Add(availableVideoStreams[j].ManifestStream);
                    isOneVideoSelected = true;
                }
            }
   
            // Select hello frist video stream from hello list if no video stream is selected
            if (!isOneVideoSelected)
            {
                availableVideoStreams[0].isChecked = true;
                selectedStreams.Add(availableVideoStreams[0].ManifestStream);
            }
   
            // Only one audio stream can be selected
            for (int j = 0; j<availableAudioStreams.Count; j++)
            {
                if (availableAudioStreams[j].isChecked && (!isOneAudioSelected))
                {
                    selectedStreams.Add(availableAudioStreams[j].ManifestStream);
                    isOneAudioSelected = true;
                    txtStatus.Text = "hello audio stream is changed too" + availableAudioStreams[j].ManifestStream.Name;
                }
            }
   
            // Select hello frist audio stream from hello list if no audio steam is selected.
            if (!isOneAudioSelected)
            {
                availableAudioStreams[0].isChecked = true;
                selectedStreams.Add(availableAudioStreams[0].ManifestStream);
            }
   
            // Multiple text streams are supported.
            for (int j = 0; j < availableTextStreams.Count; j++)
            {
                if (availableTextStreams[j].isChecked)
                {
                    selectedStreams.Add(availableTextStreams[j].ManifestStream);
                }
            }
        }
   
        // Change streams on a smooth streaming presentation with multiple video streams.
        private async void changeStreams(List<IManifestStream> selectStreams)
        {
            try
            {
                IReadOnlyList<IStreamChangedResult> returnArgs =
                    await manifestObject.SelectStreamsAsync(selectStreams);
            }
            catch (Exception e)
            {
                txtStatus.Text = "Error: " + e.Message;
            }
        }
        #endregion stream selection
5. Zlokalizuj metody mediaElement_ManifestReady hello, Dołącz hello następującego kodu na końcu hello hello funkcji:
   
        getStreams(manifestObject);
        refreshAvailableStreamsListBoxItemSource();
   
    Tak, gdy element MediaElement manifestu jest gotowy, hello kod pobiera listę dostępnych strumieni hello i wypełnia hello pole listy interfejsu użytkownika z listy hello.
6. Wewnątrz klasy MainPage hello, zlokalizuj przycisków interfejsu użytkownika powitania kliknij region zdarzenia, a następnie dodaj powitania po definicji funkcji:
   
        private void btnChangeStream_Click(object sender, RoutedEventArgs e)
        {
            List<IManifestStream> selectedStreams = new List<IManifestStream>();
   
            // Create a list of hello selected streams
            createSelectedStreamsList(selectedStreams);
   
            // Change streams on hello presentation
            changeStreams(selectedStreams);
        }

**toocompile i testowania aplikacji hello**

1. Naciśnij klawisz **F6** toocompile hello projektu. 
2. Naciśnij klawisz **F5** toorun hello aplikacji.
3. U góry hello aplikacji hello możesz użyć domyślnej hello Smooth Streaming URL lub wprowadź inną. 
4. Kliknij przycisk **Ustaw źródło**. 
5. język domyślny Hello jest audio_eng. Spróbuj tooswitch między audio_eng i audio_es. Zawsze, gdy, wybierz nowego strumienia, należy kliknąć przycisk Prześlij hello.

Ukończono Lekcja 3.  W tej lekcji możesz dodać hello funkcji toochoose strumieni.

## <a name="lesson-4-select-smooth-streaming-tracks"></a>Lekcja 4: Wybierz Smooth Streaming ścieżki
Prezentacja Smooth Streaming może zawierać wiele plików wideo zakodowane za pomocą różne poziomy jakości (szybkości transmisji bitów) i rozwiązania. W tej lekcji umożliwi użytkownikom tooselect ścieżki. Tej lekcji zawiera hello następujące procedury:

1. Modyfikowanie pliku XAML hello
2. Modyfikowanie pliku behand kodu hello
3. Kompilowanie i testowanie aplikacji hello

**Plik XAML hello toomodify**

1. W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy **MainPage.xaml**, a następnie kliknij przycisk **Widok projektanta**.
2. Zlokalizuj hello &lt;siatki&gt; tag o nazwie hello **gridStreamAndBitrateSelection**, Dołącz hello następującego kodu na końcu hello hello tagu:
   
         <StackPanel Name="spBitRateSelection" Grid.Row="1" Grid.Column="1">
         <StackPanel Orientation="Horizontal">
             <TextBlock Name="tbBitRate" Text="Available Bitrates:" FontSize="16" VerticalAlignment="Center"/>
             <Button Name="btnChangeTracks" Content="Submit" Click="btnChangeTrack_Click" />
         </StackPanel>
         <ListBox x:Name="lbAvailableVideoTracks" Height="200" Width="200" Background="Transparent" HorizontalAlignment="Left" 
                  ScrollViewer.VerticalScrollMode="Enabled" ScrollViewer.VerticalScrollBarVisibility="Visible">
             <ListBox.ItemTemplate>
                 <DataTemplate>
                     <CheckBox Content="{Binding Bitrate}" IsChecked="{Binding isChecked, Mode=TwoWay}"/>
                 </DataTemplate>
             </ListBox.ItemTemplate>
         </ListBox>
         </StackPanel>
3. Naciśnij klawisz **CTRL + S** toosave zmieniane

**toomodify hello kodzie pliku**

1. W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy **MainPage.xaml**, a następnie kliknij przycisk **kod widoku**.
2. W obszarze nazw SSPlayer hello Dodaj nową klasę:
   
        #region class Track
        public class Track
        {
            private IManifestTrack trackInfo;
            public string _bitrate;
            public bool isCheckedValue;
   
            public IManifestTrack TrackInfo
            {
                get { return trackInfo; }
                set { trackInfo = value; }
            }
   
            public string Bitrate
            {
                get { return _bitrate; }
                set { _bitrate = value; }
            }
   
            public bool isChecked
            {
                get { return isCheckedValue; }
                set
                {
                    isCheckedValue = value;
                }
            }
   
            public Track(IManifestTrack trackInfoIn)
            {
                trackInfo = trackInfoIn;
                _bitrate = trackInfoIn.Bitrate.ToString();
            }
            //public Track() { }
        }
        #endregion class Track
3. Na początku hello hello klasy MainPage, Dodaj hello następujące definicje zmiennych:
   
        private List<Track> availableTracks;
4. Wewnątrz klasy MainPage hello Dodaj powitania od regionu:
   
        #region track selection
        /// <summary>
        /// Functionality tooselect video streams
        /// </summary>
   
        /// This Function gets hello tracks for hello selected video stream
        public void getTracks(Manifest manifestObject)
        {
            availableTracks = new List<Track>();
   
            IManifestStream videoStream = getVideoStream();
            IReadOnlyList<IManifestTrack> availableTracksLocal = videoStream.AvailableTracks;
            IReadOnlyList<IManifestTrack> selectedTracksLocal = videoStream.SelectedTracks;
   
            try
            {
                for (int i = 0; i < availableTracksLocal.Count; i++)
                {
                    Track thisTrack = new Track(availableTracksLocal[i]);
                    thisTrack.isChecked = true;
   
                    for (int j = 0; j < selectedTracksLocal.Count; j++)
                    {
                        string selectedTrackName = selectedTracksLocal[j].Bitrate.ToString();
                        if (selectedTrackName.Equals(thisTrack.Bitrate))
                        {
                            thisTrack.isChecked = true;
                            break;
                        }
                    }
                    availableTracks.Add(thisTrack);
                }
            }
            catch (Exception e)
            {
                txtStatus.Text = e.Message;
            }
        }
   
        // This function gets hello video stream that is playing
        private IManifestStream getVideoStream()
        {
            IManifestStream videoStream = null;
            for (int i = 0; i < manifestObject.SelectedStreams.Count; i++)
            {
                if (manifestObject.SelectedStreams[i].Type == MediaStreamType.Video)
                {
                    videoStream = manifestObject.SelectedStreams[i];
                    break;
                }
            }
            return videoStream;
        }
   
        // This function set hello UI list box control ItemSource
        private async void refreshAvailableTracksListBoxItemSource()
        {
            try
            {
                // Update hello track check box list on hello UI 
                await _dispatcher.RunAsync(CoreDispatcherPriority.Normal, ()
                    => { lbAvailableVideoTracks.ItemsSource = availableTracks; });
            }
            catch (Exception e)
            {
                txtStatus.Text = "Error: " + e.Message;
            }        
        }
   
        // This function creates a list of hello selected tracks.
        private void createSelectedTracksList(List<IManifestTrack> selectedTracks)
        {
            // Create a list of selected tracks
            for (int j = 0; j < availableTracks.Count; j++)
            {
                if (availableTracks[j].isCheckedValue == true)
                {
                    selectedTracks.Add(availableTracks[j].TrackInfo);
                }
            }
        }
   
        // This function selects hello tracks based on user selection 
        private void changeTracks(List<IManifestTrack> selectedTracks)
        {
            IManifestStream videoStream = getVideoStream();
            try
            {
                videoStream.SelectTracks(selectedTracks);
            }
            catch (Exception ex)
            {
                txtStatus.Text = ex.Message;
            }
        }
        #endregion track selection
5. Zlokalizuj metody mediaElement_ManifestReady hello, Dołącz hello następującego kodu na końcu hello hello funkcji:
   
         getTracks(manifestObject);
         refreshAvailableTracksListBoxItemSource();
6. Wewnątrz klasy MainPage hello, zlokalizuj przycisków interfejsu użytkownika powitania kliknij region zdarzenia, a następnie dodaj powitania po definicji funkcji:
   
         private void btnChangeStream_Click(object sender, RoutedEventArgs e)
         {
            List<IManifestStream> selectedStreams = new List<IManifestStream>();

            // Create a list of hello selected streams
            createSelectedStreamsList(selectedStreams);

            // Change streams on hello presentation
            changeStreams(selectedStreams);
         }

**toocompile i testowania aplikacji hello**

1. Naciśnij klawisz **F6** toocompile hello projektu. 
2. Naciśnij klawisz **F5** toorun hello aplikacji.
3. U góry hello aplikacji hello możesz użyć domyślnej hello Smooth Streaming URL lub wprowadź inną. 
4. Kliknij przycisk **Ustaw źródło**. 
5. Domyślnie wszystkie ścieżki hello strumienia wideo hello wybrane. Witaj tooexperiment bit szybkość zmian, można wybrać hello najniższa szybkość transmisji bitów dostępne, a następnie wybierz hello najwyższą szybkość transmisji bitów dostępne. Należy kliknąć przesyłania po każdej zmianie.  Zmiany jakości wideo hello jest widoczny.

Ukończono lekcji 4.  W tej lekcji możesz dodać hello funkcji toochoose ścieżki.

## <a name="media-services-learning-paths"></a>Ścieżki szkoleniowe dotyczące usługi Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Przekazywanie opinii
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="other-resources"></a>Inne zasoby:
* [Jak toobuild aplikacja Smooth JavaScript 8 Windows przesyłania strumieniowego o funkcje zaawansowane](http://blogs.iis.net/cenkd/archive/2012/08/10/how-to-build-a-smooth-streaming-windows-8-javascript-application-with-advanced-features.aspx)
* [Płynnego przesyłania strumieniowego — omówienie](http://www.iis.net/learn/media/on-demand-smooth-streaming/smooth-streaming-technical-overview)

[PlayerApplication]: ./media/media-services-build-smooth-streaming-apps/SSClientWin8-1.png
[CodeViewPic]: ./media/media-services-build-smooth-streaming-apps/SSClientWin8-2.png

