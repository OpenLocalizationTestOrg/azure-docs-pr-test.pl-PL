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
# <a name="how-toobuild-a-smooth-streaming-windows-store-application"></a><span data-ttu-id="41a95-103">Jak tooBuild Smooth Streaming aplikację ze Sklepu Windows</span><span class="sxs-lookup"><span data-stu-id="41a95-103">How tooBuild a Smooth Streaming Windows Store Application</span></span>

<span data-ttu-id="41a95-104">Witaj Smooth Streaming klienta zestawu SDK dla systemu Windows 8 umożliwia deweloperom toobuild aplikacji ze Sklepu Windows, które można odtwarzać zawartości na żądanie i na żywo Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="41a95-104">hello Smooth Streaming Client SDK for Windows 8 enables developers toobuild Windows Store applications that can play on-demand and live Smooth Streaming content.</span></span> <span data-ttu-id="41a95-105">Ponadto toohello podstawowe odtwarzania programu Smooth Streaming zawartości, hello SDK również zapewnia zaawansowane funkcje, takie jak Microsoft PlayReady ochrony ograniczenie poziomu jakości, Live DVR, strumieniem audio przełączania, nasłuchiwanie aktualizacji stanu (np. zmiany poziomu jakości ) i zdarzeń błędu i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="41a95-105">In addition toohello basic playback of Smooth Streaming content, hello SDK also provides rich features like Microsoft PlayReady protection, quality level restriction, Live DVR, audio stream switching, listening for status updates (such as quality level changes) and error events, and so on.</span></span> <span data-ttu-id="41a95-106">Aby uzyskać więcej informacji na powitania obsługiwanych funkcji, zobacz hello [informacje o wersji](http://www.iis.net/learn/media/smooth-streaming/smooth-streaming-client-sdk-for-windows-8-release-notes).</span><span class="sxs-lookup"><span data-stu-id="41a95-106">For more information of hello supported features, see hello [release notes](http://www.iis.net/learn/media/smooth-streaming/smooth-streaming-client-sdk-for-windows-8-release-notes).</span></span> <span data-ttu-id="41a95-107">Aby uzyskać więcej informacji, zobacz [Framework Player dla systemu Windows 8](http://playerframework.codeplex.com/).</span><span class="sxs-lookup"><span data-stu-id="41a95-107">For more information, see [Player Framework for Windows 8](http://playerframework.codeplex.com/).</span></span> 

<span data-ttu-id="41a95-108">Ten samouczek zawiera cztery lekcje:</span><span class="sxs-lookup"><span data-stu-id="41a95-108">This tutorial contains four lessons:</span></span>

1. <span data-ttu-id="41a95-109">Tworzenie podstawowej płynnego przesyłania strumieniowego aplikacji sklepu</span><span class="sxs-lookup"><span data-stu-id="41a95-109">Create a Basic Smooth Streaming Store Application</span></span>
2. <span data-ttu-id="41a95-110">Dodaj suwaka hello tooControl postępu nośnika</span><span class="sxs-lookup"><span data-stu-id="41a95-110">Add a Slider Bar tooControl hello Media Progress</span></span>
3. <span data-ttu-id="41a95-111">Wybierz Smooth Streaming strumieni</span><span class="sxs-lookup"><span data-stu-id="41a95-111">Select Smooth Streaming Streams</span></span>
4. <span data-ttu-id="41a95-112">Wybierz Smooth Streaming ścieżki</span><span class="sxs-lookup"><span data-stu-id="41a95-112">Select Smooth Streaming Tracks</span></span>

## <a name="prerequisites"></a><span data-ttu-id="41a95-113">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="41a95-113">Prerequisites</span></span>
* <span data-ttu-id="41a95-114">Windows 8, 32-bitowy lub 64-bitowej.</span><span class="sxs-lookup"><span data-stu-id="41a95-114">Windows 8 32-bit or 64-bit.</span></span> <span data-ttu-id="41a95-115">Możesz uzyskać [systemu Windows 8 Enterprise Evaluation](http://msdn.microsoft.com/evalcenter/jj554510.aspx) w witrynie MSDN.</span><span class="sxs-lookup"><span data-stu-id="41a95-115">You can get [Windows 8 Enterprise Evaluation](http://msdn.microsoft.com/evalcenter/jj554510.aspx) from MSDN.</span></span>
* <span data-ttu-id="41a95-116">Program Visual Studio 2012 lub Visual Studio Express 2012 (lub nowszy).</span><span class="sxs-lookup"><span data-stu-id="41a95-116">Visual Studio 2012 or Visual Studio Express 2012 (or a later version).</span></span> <span data-ttu-id="41a95-117">Można uzyskać wersji próbnej hello z [tutaj](http://www.microsoft.com/visualstudio/11/downloads).</span><span class="sxs-lookup"><span data-stu-id="41a95-117">You can get hello trial version from [here](http://www.microsoft.com/visualstudio/11/downloads).</span></span>
* <span data-ttu-id="41a95-118">[Microsoft Smooth Streaming Client zestawu SDK dla systemu Windows 8](http://visualstudiogallery.msdn.microsoft.com/04423d13-3b3e-4741-a01c-1ae29e84fea6?SRC=Homehttp://visualstudiogallery.msdn.microsoft.com/04423d13-3b3e-4741-a01c-1ae29e84fea6?SRC=Home).</span><span class="sxs-lookup"><span data-stu-id="41a95-118">[Microsoft Smooth Streaming Client SDK for Windows 8](http://visualstudiogallery.msdn.microsoft.com/04423d13-3b3e-4741-a01c-1ae29e84fea6?SRC=Homehttp://visualstudiogallery.msdn.microsoft.com/04423d13-3b3e-4741-a01c-1ae29e84fea6?SRC=Home).</span></span>

<span data-ttu-id="41a95-119">rozwiązanie ukończyć powitalnych dla każdej lekcji można pobrać z przykładów kodu deweloperów MSDN (Galeria kodu):</span><span class="sxs-lookup"><span data-stu-id="41a95-119">hello completed solution for each lesson can be downloaded from MSDN Developer Code Samples (Code Gallery):</span></span> 

* <span data-ttu-id="41a95-120">[Lekcja 1](http://code.msdn.microsoft.com/Smooth-Streaming-Client-0bb1471f) — sprawne prostego systemu Windows 8 przesyłania strumieniowego Media Player</span><span class="sxs-lookup"><span data-stu-id="41a95-120">[Lesson 1](http://code.msdn.microsoft.com/Smooth-Streaming-Client-0bb1471f) - A Simple Windows 8 Smooth Streaming Media Player,</span></span> 
* <span data-ttu-id="41a95-121">[Lekcja 2](http://code.msdn.microsoft.com/A-simple-Windows-8-Smooth-ee98f63a) — sprawne prostego systemu Windows 8 przesyłania strumieniowego Media Player paska suwaka formantu</span><span class="sxs-lookup"><span data-stu-id="41a95-121">[Lesson 2](http://code.msdn.microsoft.com/A-simple-Windows-8-Smooth-ee98f63a) - A Simple Windows 8 Smooth Streaming Media Player with a Slider Bar Control,</span></span> 
* <span data-ttu-id="41a95-122">[Lekcja 3](http://code.msdn.microsoft.com/A-Windows-8-Smooth-883c3b44) — sprawne systemu Windows 8 przesyłania strumieniowego Media Player do wyboru strumienia</span><span class="sxs-lookup"><span data-stu-id="41a95-122">[Lesson 3](http://code.msdn.microsoft.com/A-Windows-8-Smooth-883c3b44) - A Windows 8 Smooth Streaming Media Player with Stream Selection,</span></span>  
* <span data-ttu-id="41a95-123">[Lekcja 4](http://code.msdn.microsoft.com/A-Windows-8-Smooth-aa9e4907) — sprawne systemu Windows 8 przesyłania strumieniowego Media Player śledzenie zaznaczenia.</span><span class="sxs-lookup"><span data-stu-id="41a95-123">[Lesson 4](http://code.msdn.microsoft.com/A-Windows-8-Smooth-aa9e4907)  - A Windows 8 Smooth Streaming Media Player with Track Selection.</span></span>

## <a name="lesson-1-create-a-basic-smooth-streaming-store-application"></a><span data-ttu-id="41a95-124">Lekcja 1: Tworzenie podstawowej płynnego przesyłania strumieniowego aplikacji sklepu</span><span class="sxs-lookup"><span data-stu-id="41a95-124">Lesson 1: Create a Basic Smooth Streaming Store Application</span></span>

<span data-ttu-id="41a95-125">W tej lekcji utworzysz aplikacji Sklepu Windows za pomocą MediaElement kontroli tooplay Smooth strumienia zawartości.</span><span class="sxs-lookup"><span data-stu-id="41a95-125">In this lesson, you will create a Windows Store application with a MediaElement control tooplay Smooth Stream content.</span></span>  <span data-ttu-id="41a95-126">działającej aplikacji Hello wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="41a95-126">hello running application looks like:</span></span>

![Przykładowa aplikacja Sklepu Windows Smooth Streaming][PlayerApplication]

<span data-ttu-id="41a95-128">Aby uzyskać więcej informacji na temat tworzenia aplikacji Sklepu Windows, temacie [tworzenie wspaniałych aplikacji dla systemu Windows 8](http://msdn.microsoft.com/windows/apps/br229512.aspx).</span><span class="sxs-lookup"><span data-stu-id="41a95-128">For more information on developing Windows Store application, see [Develop Great Apps for Windows 8](http://msdn.microsoft.com/windows/apps/br229512.aspx).</span></span> <span data-ttu-id="41a95-129">Tej lekcji zawiera hello następujące procedury:</span><span class="sxs-lookup"><span data-stu-id="41a95-129">This lesson contains hello following procedures:</span></span>

1. <span data-ttu-id="41a95-130">Tworzenie projektu ze Sklepu Windows</span><span class="sxs-lookup"><span data-stu-id="41a95-130">Create a Windows Store project</span></span>
2. <span data-ttu-id="41a95-131">Projektowanie interfejsu użytkownika hello (XAML)</span><span class="sxs-lookup"><span data-stu-id="41a95-131">Design hello user interface (XAML)</span></span>
3. <span data-ttu-id="41a95-132">Modyfikowanie pliku CodeBehind hello</span><span class="sxs-lookup"><span data-stu-id="41a95-132">Modify hello code behind file</span></span>
4. <span data-ttu-id="41a95-133">Kompilowanie i testowanie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="41a95-133">Compile and test hello application</span></span>

<span data-ttu-id="41a95-134">**toocreate projektu ze Sklepu Windows**</span><span class="sxs-lookup"><span data-stu-id="41a95-134">**toocreate a Windows Store project**</span></span>

1. <span data-ttu-id="41a95-135">Uruchom program Visual Studio 2012 lub nowszym.</span><span class="sxs-lookup"><span data-stu-id="41a95-135">Run Visual Studio 2012 or later.</span></span>
2. <span data-ttu-id="41a95-136">Z hello **pliku** menu, kliknij przycisk **nowy**, a następnie kliknij przycisk **projektu**.</span><span class="sxs-lookup"><span data-stu-id="41a95-136">From hello **FILE** menu, click **New**, and then click **Project**.</span></span>
3. <span data-ttu-id="41a95-137">W oknie dialogowym Nowy projekt hello wpisz lub wybierz hello następujące wartości:</span><span class="sxs-lookup"><span data-stu-id="41a95-137">From hello New Project dialog, type or select  hello following values:</span></span>

| <span data-ttu-id="41a95-138">Nazwa</span><span class="sxs-lookup"><span data-stu-id="41a95-138">Name</span></span> | <span data-ttu-id="41a95-139">Wartość</span><span class="sxs-lookup"><span data-stu-id="41a95-139">Value</span></span> |
| --- | --- |
| <span data-ttu-id="41a95-140">Grupa szablonów</span><span class="sxs-lookup"><span data-stu-id="41a95-140">Template group</span></span> |<span data-ttu-id="41a95-141">Zainstalowane/szablony/Visual C# / ze Sklepu Windows</span><span class="sxs-lookup"><span data-stu-id="41a95-141">Installed/Templates/Visual C#/Windows Store</span></span> |
| <span data-ttu-id="41a95-142">Szablon</span><span class="sxs-lookup"><span data-stu-id="41a95-142">Template</span></span> |<span data-ttu-id="41a95-143">Pusta aplikacja (XAML)</span><span class="sxs-lookup"><span data-stu-id="41a95-143">Blank App (XAML)</span></span> |
| <span data-ttu-id="41a95-144">Nazwa</span><span class="sxs-lookup"><span data-stu-id="41a95-144">Name</span></span> |<span data-ttu-id="41a95-145">SSPlayer</span><span class="sxs-lookup"><span data-stu-id="41a95-145">SSPlayer</span></span> |
| <span data-ttu-id="41a95-146">Lokalizacja</span><span class="sxs-lookup"><span data-stu-id="41a95-146">Location</span></span> |<span data-ttu-id="41a95-147">C:\SSTutorials</span><span class="sxs-lookup"><span data-stu-id="41a95-147">C:\SSTutorials</span></span> |
| <span data-ttu-id="41a95-148">Nazwa rozwiązania</span><span class="sxs-lookup"><span data-stu-id="41a95-148">Solution Name</span></span> |<span data-ttu-id="41a95-149">SSPlayer</span><span class="sxs-lookup"><span data-stu-id="41a95-149">SSPlayer</span></span> |
| <span data-ttu-id="41a95-150">Utwórz katalog rozwiązania</span><span class="sxs-lookup"><span data-stu-id="41a95-150">Create directory for solution</span></span> |<span data-ttu-id="41a95-151">(wybrane)</span><span class="sxs-lookup"><span data-stu-id="41a95-151">(selected)</span></span> |

1. <span data-ttu-id="41a95-152">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="41a95-152">Click **OK**.</span></span>

<span data-ttu-id="41a95-153">**tooadd toohello odwołania Smooth Streaming Client SDK**</span><span class="sxs-lookup"><span data-stu-id="41a95-153">**tooadd a reference toohello Smooth Streaming Client SDK**</span></span>

1. <span data-ttu-id="41a95-154">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy **SSPlayer**, a następnie kliknij przycisk **Dodaj odwołanie**.</span><span class="sxs-lookup"><span data-stu-id="41a95-154">From Solution Explorer, right-click **SSPlayer**, and then click **Add Reference**.</span></span>
2. <span data-ttu-id="41a95-155">Wpisz lub wybierz hello następujące wartości:</span><span class="sxs-lookup"><span data-stu-id="41a95-155">Type or select hello following values:</span></span>

| <span data-ttu-id="41a95-156">Nazwa</span><span class="sxs-lookup"><span data-stu-id="41a95-156">Name</span></span> | <span data-ttu-id="41a95-157">Wartość</span><span class="sxs-lookup"><span data-stu-id="41a95-157">Value</span></span> |
| --- | --- |
| <span data-ttu-id="41a95-158">Grupy odwołania</span><span class="sxs-lookup"><span data-stu-id="41a95-158">Reference group</span></span> |<span data-ttu-id="41a95-159">Rozszerzenia/systemu Windows</span><span class="sxs-lookup"><span data-stu-id="41a95-159">Windows/Extensions</span></span> |
| <span data-ttu-id="41a95-160">Dokumentacja</span><span class="sxs-lookup"><span data-stu-id="41a95-160">Reference</span></span> |<span data-ttu-id="41a95-161">Wybierz Microsoft Smooth Streaming Client zestawu SDK dla systemu Windows 8 i Microsoft Visual C++ Runtime Package</span><span class="sxs-lookup"><span data-stu-id="41a95-161">Select Microsoft Smooth Streaming Client SDK for Windows 8 and Microsoft Visual C++ Runtime Package</span></span> |

1. <span data-ttu-id="41a95-162">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="41a95-162">Click **OK**.</span></span> 

<span data-ttu-id="41a95-163">Po dodaniu odwołań hello, musisz wybrać platformy docelowe hello (x64 lub x86), Dodawanie odwołania nie będą działać dla konfiguracji platformy dowolnego Procesora.</span><span class="sxs-lookup"><span data-stu-id="41a95-163">After adding hello references, you must select hello targeted platform (x64 or x86), adding references will not work for Any CPU platform configuration.</span></span>  <span data-ttu-id="41a95-164">W Eksploratorze rozwiązań pojawi się żółty znak ostrzeżenie tych dodać odwołań.</span><span class="sxs-lookup"><span data-stu-id="41a95-164">In solution explorer, you will see yellow warning mark for these added references.</span></span>

<span data-ttu-id="41a95-165">**Interfejs użytkownika player hello toodesign**</span><span class="sxs-lookup"><span data-stu-id="41a95-165">**toodesign hello player user interface**</span></span>

1. <span data-ttu-id="41a95-166">W Eksploratorze rozwiązań kliknij dwukrotnie kliknij **MainPage.xaml** tooopen go w projekcie hello wyświetlić.</span><span class="sxs-lookup"><span data-stu-id="41a95-166">From Solution Explorer, double click **MainPage.xaml** tooopen it in hello design view.</span></span>
2. <span data-ttu-id="41a95-167">Zlokalizuj hello  **&lt;siatki&gt;**  i  **&lt;/Grid&gt;**  tagi hello pliku XAML, a następnie wklej hello poniższy kod między tagami hello dwa:</span><span class="sxs-lookup"><span data-stu-id="41a95-167">Locate hello **&lt;Grid&gt;** and **&lt;/Grid&gt;**  tags hello XAML file, and paste hello following code between hello two tags:</span></span>

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
   
   <span data-ttu-id="41a95-168">Hello Formant MediaElement jest używane tooplayback nośnika.</span><span class="sxs-lookup"><span data-stu-id="41a95-168">hello MediaElement control is used tooplayback media.</span></span> <span data-ttu-id="41a95-169">Kontrolka suwaka Hello o nazwie sliderProgress będzie służyć trwa hello dalej lekcji toocontrol hello nośnika.</span><span class="sxs-lookup"><span data-stu-id="41a95-169">hello slider control named sliderProgress will be used in hello next lesson toocontrol hello media progress.</span></span>
3. <span data-ttu-id="41a95-170">Naciśnij klawisz **CTRL + S** toosave hello pliku.</span><span class="sxs-lookup"><span data-stu-id="41a95-170">Press **CTRL+S** toosave hello file.</span></span>

<span data-ttu-id="41a95-171">Hello Formant MediaElement nie obsługuje funkcji Smooth Streaming zawartości out-of-box.</span><span class="sxs-lookup"><span data-stu-id="41a95-171">hello MediaElement control does not support Smooth Streaming content out-of-box.</span></span> <span data-ttu-id="41a95-172">Obsługa Smooth Streaming hello tooenable należy zarejestrować obsługi hello strumień bajtów Smooth Streaming przez rozszerzenie nazwy pliku i typ MIME.</span><span class="sxs-lookup"><span data-stu-id="41a95-172">tooenable hello Smooth Streaming support, you must register hello Smooth Streaming byte-stream handler by file name extension and MIME type.</span></span>  <span data-ttu-id="41a95-173">tooregister, należy użyć metody MediaExtensionManager.RegisterByteStremHandler hello hello Windows.Media w przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="41a95-173">tooregister, you use hello MediaExtensionManager.RegisterByteStremHandler method of hello Windows.Media namespace.</span></span>

<span data-ttu-id="41a95-174">W tym pliku XAML niektóre programy obsługi zdarzeń skojarzonych z hello kontrolki.</span><span class="sxs-lookup"><span data-stu-id="41a95-174">In this XAML file, some event handlers are associated with hello controls.</span></span>  <span data-ttu-id="41a95-175">Należy zdefiniować te programy obsługi zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="41a95-175">You must define those event handlers.</span></span>

<span data-ttu-id="41a95-176">**toomodify hello kodzie pliku**</span><span class="sxs-lookup"><span data-stu-id="41a95-176">**toomodify hello code behind file**</span></span>

1. <span data-ttu-id="41a95-177">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy **MainPage.xaml**, a następnie kliknij przycisk **kod widoku**.</span><span class="sxs-lookup"><span data-stu-id="41a95-177">From Solution Explorer, right-click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="41a95-178">U góry pliku hello hello, Dodaj następujące hello instrukcję using:</span><span class="sxs-lookup"><span data-stu-id="41a95-178">At hello top of hello file, add hello following using statement:</span></span>
   
        using Windows.Media;
3. <span data-ttu-id="41a95-179">Na początku hello hello **MainPage** klasy, Dodaj hello następującego elementu członkowskiego danych:</span><span class="sxs-lookup"><span data-stu-id="41a95-179">At hello beginning of hello **MainPage** class, add hello following data member:</span></span>
   
         private MediaExtensionManager extensions = new MediaExtensionManager();
4. <span data-ttu-id="41a95-180">Na końcu hello hello **MainPage** konstruktora, Dodaj hello następujące dwa wiersze:</span><span class="sxs-lookup"><span data-stu-id="41a95-180">At hello end of hello **MainPage** constructor, add hello following two lines:</span></span>
   
        extensions.RegisterByteStreamHandler("Microsoft.Media.AdaptiveStreaming.SmoothByteStreamHandler", ".ism", "text/xml");
        extensions.RegisterByteStreamHandler("Microsoft.Media.AdaptiveStreaming.SmoothByteStreamHandler", ".ism", "application/vnd.ms-sstr+xml");
5. <span data-ttu-id="41a95-181">Na końcu hello hello **MainPage** klasy, Wklej hello następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="41a95-181">At hello end of hello **MainPage** class, paste hello following code:</span></span>
   
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

<span data-ttu-id="41a95-182">Program obsługi zdarzeń sliderProgress_PointerPressed Hello jest zdefiniowany w tym miejscu.</span><span class="sxs-lookup"><span data-stu-id="41a95-182">hello sliderProgress_PointerPressed event handler is defined here.</span></span>  <span data-ttu-id="41a95-183">Istnieje więcej tooget toodo works pracy, który będzie uwzględnione w następnej lekcji hello tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="41a95-183">There are more works toodo tooget it working, which will be covered in hello next lesson of this tutorial.</span></span>
6. <span data-ttu-id="41a95-184">Naciśnij klawisz **CTRL + S** toosave hello pliku.</span><span class="sxs-lookup"><span data-stu-id="41a95-184">Press **CTRL+S** toosave hello file.</span></span>

<span data-ttu-id="41a95-185">Witaj hello gotowym kodzie pliku powinna wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="41a95-185">hello finished hello code behind file shall look like this:</span></span>

![Codeview w aplikacji Visual Studio programu Smooth Streaming Sklepu Windows][CodeViewPic]

<span data-ttu-id="41a95-187">**toocompile i testowania aplikacji hello**</span><span class="sxs-lookup"><span data-stu-id="41a95-187">**toocompile and test hello application**</span></span>

1. <span data-ttu-id="41a95-188">Z hello **kompilacji** menu, kliknij przycisk **programu Configuration Manager**.</span><span class="sxs-lookup"><span data-stu-id="41a95-188">From hello **BUILD** menu, click **Configuration Manager**.</span></span>
2. <span data-ttu-id="41a95-189">Zmień **platformy aktywne rozwiązanie** toomatch rozwoju platformy.</span><span class="sxs-lookup"><span data-stu-id="41a95-189">Change **Active solution platform** toomatch your development platform.</span></span>
3. <span data-ttu-id="41a95-190">Naciśnij klawisz **F6** toocompile hello projektu.</span><span class="sxs-lookup"><span data-stu-id="41a95-190">Press **F6** toocompile hello project.</span></span> 
4. <span data-ttu-id="41a95-191">Naciśnij klawisz **F5** toorun hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="41a95-191">Press **F5** toorun hello application.</span></span>
5. <span data-ttu-id="41a95-192">U góry hello aplikacji hello możesz użyć domyślnej hello Smooth Streaming URL lub wprowadź inną.</span><span class="sxs-lookup"><span data-stu-id="41a95-192">At hello top of hello application, you can either use hello default Smooth Streaming URL or enter a different one.</span></span> 
6. <span data-ttu-id="41a95-193">Kliknij przycisk **Ustaw źródło**.</span><span class="sxs-lookup"><span data-stu-id="41a95-193">Click **Set Source**.</span></span> <span data-ttu-id="41a95-194">Ponieważ **Auto-odtwarzanie** jest włączona domyślnie hello nośnika jest odtwarzany automatycznie.</span><span class="sxs-lookup"><span data-stu-id="41a95-194">Because **Auto Play** is enabled by default, hello media shall play automatically.</span></span>  <span data-ttu-id="41a95-195">Można kontrolować hello nośnika przy użyciu hello **odtwarzanie**, **Wstrzymaj** i **zatrzymać** przycisków.</span><span class="sxs-lookup"><span data-stu-id="41a95-195">You can control hello media using hello **Play**, **Pause** and **Stop** buttons.</span></span>  <span data-ttu-id="41a95-196">Można kontrolować hello nośnika woluminu przy użyciu hello pionowej kontrolce slider.</span><span class="sxs-lookup"><span data-stu-id="41a95-196">You can control hello media volume using hello vertical slider.</span></span>  <span data-ttu-id="41a95-197">Jednak hello suwak poziomy kontroli powitalne postępu nośnika nie jest całkowicie jeszcze zaimplementowane.</span><span class="sxs-lookup"><span data-stu-id="41a95-197">However hello horizontal slider for controlling hello media progress is not fully implemented yet.</span></span> 

<span data-ttu-id="41a95-198">Lesson1 została ukończona.</span><span class="sxs-lookup"><span data-stu-id="41a95-198">You have completed lesson1.</span></span>  <span data-ttu-id="41a95-199">W tej lekcji służy element MediaElement kontroli tooplayback Smooth Streaming zawartości.</span><span class="sxs-lookup"><span data-stu-id="41a95-199">In this lesson, you use a MediaElement control tooplayback Smooth Streaming content.</span></span>  <span data-ttu-id="41a95-200">W następnej lekcji hello doda postęp hello toocontrol suwaka hello Smooth Streaming zawartości.</span><span class="sxs-lookup"><span data-stu-id="41a95-200">In hello next lesson, you will add a slider toocontrol hello progress of hello Smooth Streaming content.</span></span>

## <a name="lesson-2-add-a-slider-bar-toocontrol-hello-media-progress"></a><span data-ttu-id="41a95-201">Lekcja 2: Dodaj suwaka hello tooControl postępu nośnika</span><span class="sxs-lookup"><span data-stu-id="41a95-201">Lesson 2: Add a Slider Bar tooControl hello Media Progress</span></span>

<span data-ttu-id="41a95-202">W lekcji 1 zostały utworzone z tooplayback kontrolki MediaElement XAML Smooth Streaming zawartości multimedialnej aplikacji Sklepu Windows.</span><span class="sxs-lookup"><span data-stu-id="41a95-202">In lesson 1, you created a Windows Store application with a MediaElement XAML control tooplayback Smooth Streaming media content.</span></span>  <span data-ttu-id="41a95-203">Pochodzi niektórych funkcji podstawowych nośników, takich jak start, stop i wstrzymania.</span><span class="sxs-lookup"><span data-stu-id="41a95-203">It comes some basic media functions like start, stop and pause.</span></span>  <span data-ttu-id="41a95-204">W tej lekcji spowoduje dodanie aplikacji toohello formantów paska suwaka.</span><span class="sxs-lookup"><span data-stu-id="41a95-204">In this lesson, you will add a slider bar control toohello application.</span></span>

<span data-ttu-id="41a95-205">W tym samouczku używamy pozycji suwaka hello tooupdate czasomierza oparte na bieżącej pozycji hello hello Formant MediaElement.</span><span class="sxs-lookup"><span data-stu-id="41a95-205">In this tutorial, we will use a timer tooupdate hello slider position based on hello current position of hello MediaElement control.</span></span>  <span data-ttu-id="41a95-206">suwak Hello start i czas zakończenia również toobe należy zaktualizować w przypadku zawartości na żywo.</span><span class="sxs-lookup"><span data-stu-id="41a95-206">hello slider start and end time also need toobe updated in case of live content.</span></span>  <span data-ttu-id="41a95-207">Mogą być lepiej obsłużone w hello adaptacyjną źródła aktualizacji zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="41a95-207">This can be better handled in hello adaptive source update event.</span></span>

<span data-ttu-id="41a95-208">Źródeł multimediów to obiekty, które generować dane do nośnika.</span><span class="sxs-lookup"><span data-stu-id="41a95-208">Media sources are objects that generate media data.</span></span>  <span data-ttu-id="41a95-209">Witaj źródła programu rozpoznawania nazw przyjmujący element stream adres URL lub bajt i tworzy hello odpowiedni nośnik źródła dla tej zawartości.</span><span class="sxs-lookup"><span data-stu-id="41a95-209">hello source resolver takes a URL or byte stream and creates hello appropriate media source for that content.</span></span>  <span data-ttu-id="41a95-210">Program rozpoznawania nazw Hello źródła jest hello standardowy sposób dla źródeł multimediów toocreate aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="41a95-210">hello source resolver is hello standard way for hello applications toocreate media sources.</span></span> 

<span data-ttu-id="41a95-211">Tej lekcji zawiera hello następujące procedury:</span><span class="sxs-lookup"><span data-stu-id="41a95-211">This lesson contains hello following procedures:</span></span>

1. <span data-ttu-id="41a95-212">Zarejestrować hello Smooth Streaming obsługi</span><span class="sxs-lookup"><span data-stu-id="41a95-212">Register hello Smooth Streaming handler</span></span> 
2. <span data-ttu-id="41a95-213">Dodać obsługę zdarzeń poziomu Menedżera źródła adaptacyjną hello</span><span class="sxs-lookup"><span data-stu-id="41a95-213">Add hello adaptive source manager level event handlers</span></span>
3. <span data-ttu-id="41a95-214">Dodaj programy obsługi zdarzeń na poziomie adaptacyjną źródła hello</span><span class="sxs-lookup"><span data-stu-id="41a95-214">Add hello adaptive source level event handlers</span></span>
4. <span data-ttu-id="41a95-215">Dodaj element MediaElement procedury obsługi zdarzeń</span><span class="sxs-lookup"><span data-stu-id="41a95-215">Add MediaElement event handlers</span></span>
5. <span data-ttu-id="41a95-216">Dodaj suwaka kodu powiązanego</span><span class="sxs-lookup"><span data-stu-id="41a95-216">Add slider bar related code</span></span>
6. <span data-ttu-id="41a95-217">Kompilowanie i testowanie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="41a95-217">Compile and test hello application</span></span>

<span data-ttu-id="41a95-218">**tooregister hello strumień bajtów Smooth Streaming obsługi i przekazać hello propertyset**</span><span class="sxs-lookup"><span data-stu-id="41a95-218">**tooregister hello Smooth Streaming byte-stream handler and pass hello propertyset**</span></span>

1. <span data-ttu-id="41a95-219">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy **MainPage.xaml**, a następnie kliknij przycisk **kod widoku**.</span><span class="sxs-lookup"><span data-stu-id="41a95-219">From Solution Explorer, right click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="41a95-220">Na początku hello pliku hello, Dodaj następujące hello instrukcję using:</span><span class="sxs-lookup"><span data-stu-id="41a95-220">At hello beginning of hello file, add hello following using statement:</span></span>

        using Microsoft.Media.AdaptiveStreaming;
3. <span data-ttu-id="41a95-221">Na początku hello hello klasy MainPage, Dodaj hello następujące elementy członkowskie danych:</span><span class="sxs-lookup"><span data-stu-id="41a95-221">At hello beginning of hello MainPage class, add hello following data members:</span></span>

         private Windows.Foundation.Collections.PropertySet propertySet = new Windows.Foundation.Collections.PropertySet();             
         private IAdaptiveSourceManager adaptiveSourceManager;
4. <span data-ttu-id="41a95-222">Witaj wewnątrz **MainPage** konstruktora, Dodaj hello następującego kodu po hello **to. Inicjowanie Components();**  wiersza i hello rejestracji kodu wierszach w poprzedniej lekcji hello:</span><span class="sxs-lookup"><span data-stu-id="41a95-222">Inside hello **MainPage** constructor, add hello following code after hello **this.Initialize Components();** line and hello registration code lines written in hello previous lesson:</span></span>

        // Gets hello default instance of AdaptiveSourceManager which manages Smooth 
        //Streaming media sources.
        adaptiveSourceManager = AdaptiveSourceManager.GetDefault();
        // Sets property key value tooAdaptiveSourceManager default instance.
        // {A5CE1DE8-1D00-427B-ACEF-FB9A3C93DE2D}" must be hardcoded.
        propertySet["{A5CE1DE8-1D00-427B-ACEF-FB9A3C93DE2D}"] = adaptiveSourceManager;
5. <span data-ttu-id="41a95-223">Witaj wewnątrz **MainPage** konstruktora, zmodyfikuj Witaj dwie RegisterByteStreamHandler metody tooadd Witaj określonymi parametry:</span><span class="sxs-lookup"><span data-stu-id="41a95-223">Inside hello **MainPage** constructor, modify hello two RegisterByteStreamHandler methods tooadd hello forth parameters:</span></span>

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
6. <span data-ttu-id="41a95-224">Naciśnij klawisz **CTRL + S** toosave hello pliku.</span><span class="sxs-lookup"><span data-stu-id="41a95-224">Press **CTRL+S** toosave hello file.</span></span>

<span data-ttu-id="41a95-225">**Program obsługi zdarzeń na poziomie menedżera tooadd hello adaptacyjną źródła**</span><span class="sxs-lookup"><span data-stu-id="41a95-225">**tooadd hello adaptive source manager level event handler**</span></span>

1. <span data-ttu-id="41a95-226">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy **MainPage.xaml**, a następnie kliknij przycisk **kod widoku**.</span><span class="sxs-lookup"><span data-stu-id="41a95-226">From Solution Explorer, right click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="41a95-227">Witaj wewnątrz **MainPage** klasy, Dodaj hello następującego elementu członkowskiego danych:</span><span class="sxs-lookup"><span data-stu-id="41a95-227">Inside hello **MainPage** class, add hello following data member:</span></span>
   
     <span data-ttu-id="41a95-228">prywatne adaptiveSource AdaptiveSource = null;</span><span class="sxs-lookup"><span data-stu-id="41a95-228">private AdaptiveSource adaptiveSource = null;</span></span>
3. <span data-ttu-id="41a95-229">Na końcu hello hello **MainPage** klasy, Dodaj powitania po obsługi zdarzeń:</span><span class="sxs-lookup"><span data-stu-id="41a95-229">At hello end of hello **MainPage** class, add hello following event handler:</span></span>
   
         # region Adaptive Source Manager Level Events
         private void mediaElement_AdaptiveSourceOpened(AdaptiveSource sender, AdaptiveSourceOpenedEventArgs args)
         {

            adaptiveSource = args.AdaptiveSource;
         }

         # endregion Adaptive Source Manager Level Events
4. <span data-ttu-id="41a95-230">Na końcu hello hello **MainPage** konstruktora, Dodaj następujące zdarzenia otwarte adaptacyjną źródłowego toohello toosubscribe wiersza hello:</span><span class="sxs-lookup"><span data-stu-id="41a95-230">At hello end of hello **MainPage** constructor, add hello following line toosubscribe toohello adaptive source open event:</span></span>
   
         adaptiveSourceManager.AdaptiveSourceOpenedEvent += 
           new AdaptiveSourceOpenedEventHandler(mediaElement_AdaptiveSourceOpened);
5. <span data-ttu-id="41a95-231">Naciśnij klawisz **CTRL + S** toosave hello pliku.</span><span class="sxs-lookup"><span data-stu-id="41a95-231">Press **CTRL+S** toosave hello file.</span></span>

<span data-ttu-id="41a95-232">**programy obsługi zdarzeń na poziomie adaptacyjną źródła tooadd**</span><span class="sxs-lookup"><span data-stu-id="41a95-232">**tooadd adaptive source level event handlers**</span></span>

1. <span data-ttu-id="41a95-233">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy **MainPage.xaml**, a następnie kliknij przycisk **kod widoku**.</span><span class="sxs-lookup"><span data-stu-id="41a95-233">From Solution Explorer, right click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="41a95-234">Witaj wewnątrz **MainPage** klasy, Dodaj hello następującego elementu członkowskiego danych:</span><span class="sxs-lookup"><span data-stu-id="41a95-234">Inside hello **MainPage** class, add hello following data member:</span></span>
   
     <span data-ttu-id="41a95-235">prywatne adaptiveSourceStatusUpdate AdaptiveSourceStatusUpdatedEventArgs;   prywatne manifestObject manifestu;</span><span class="sxs-lookup"><span data-stu-id="41a95-235">private AdaptiveSourceStatusUpdatedEventArgs adaptiveSourceStatusUpdate;   private Manifest manifestObject;</span></span>
3. <span data-ttu-id="41a95-236">Na końcu hello hello **MainPage** klasy, Dodaj hello następujące procedury obsługi zdarzeń:</span><span class="sxs-lookup"><span data-stu-id="41a95-236">At hello end of hello **MainPage** class, add hello following event handlers:</span></span>

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
4. <span data-ttu-id="41a95-237">Na końcu hello hello **mediaElement AdaptiveSourceOpened** metody, Dodaj następujące zdarzenia toohello toosubscribe kodu hello:</span><span class="sxs-lookup"><span data-stu-id="41a95-237">At hello end of hello **mediaElement AdaptiveSourceOpened** method, add hello following code toosubscribe toohello events:</span></span>
   
         adaptiveSource.ManifestReadyEvent +=

                    mediaElement_ManifestReady;
         adaptiveSource.AdaptiveSourceStatusUpdatedEvent += 

            mediaElement_AdaptiveSourceStatusUpdated;
         adaptiveSource.AdaptiveSourceFailedEvent += 

            mediaElement_AdaptiveSourceFailed;
5. <span data-ttu-id="41a95-238">Naciśnij klawisz **CTRL + S** toosave hello pliku.</span><span class="sxs-lookup"><span data-stu-id="41a95-238">Press **CTRL+S** toosave hello file.</span></span>

<span data-ttu-id="41a95-239">Witaj, które same zdarzenia są dostępne na adaptacyjną Menedżer poziom źródła również, która może służyć do obsługi funkcji typowe tooall nośnika elementy w aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="41a95-239">hello same events are available on Adaptive Source manger level as well, which can be used for handling functionality common tooall media elements in hello app.</span></span> <span data-ttu-id="41a95-240">Każdy AdaptiveSource zawiera własnych zdarzeń i wszystkie zdarzenia AdaptiveSource będzie kaskadowych w obszarze AdaptiveSourceManager.</span><span class="sxs-lookup"><span data-stu-id="41a95-240">Each AdaptiveSource includes its own events and all AdaptiveSource events will be cascaded under AdaptiveSourceManager.</span></span>

<span data-ttu-id="41a95-241">**programy obsługi zdarzeń elementu mediów tooadd**</span><span class="sxs-lookup"><span data-stu-id="41a95-241">**tooadd Media Element event handlers**</span></span>

1. <span data-ttu-id="41a95-242">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy **MainPage.xaml**, a następnie kliknij przycisk **kod widoku**.</span><span class="sxs-lookup"><span data-stu-id="41a95-242">From Solution Explorer, right click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="41a95-243">Na końcu hello hello **MainPage** klasy, Dodaj hello następujące procedury obsługi zdarzeń:</span><span class="sxs-lookup"><span data-stu-id="41a95-243">At hello end of hello **MainPage** class, add hello following event handlers:</span></span>

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
3. <span data-ttu-id="41a95-244">Na końcu hello hello **MainPage** konstruktora, Dodaj następujące zdarzenia toohello toosubscript kodu hello:</span><span class="sxs-lookup"><span data-stu-id="41a95-244">At hello end of hello **MainPage** constructor, add hello following code toosubscript toohello events:</span></span>

         mediaElement.MediaOpened += MediaOpened;
         mediaElement.MediaEnded += MediaEnded;
         mediaElement.MediaFailed += MediaFailed;
4. <span data-ttu-id="41a95-245">Naciśnij klawisz **CTRL + S** toosave hello pliku.</span><span class="sxs-lookup"><span data-stu-id="41a95-245">Press **CTRL+S** toosave hello file.</span></span>

<span data-ttu-id="41a95-246">**suwak tooadd powiązane kodu kreskowego**</span><span class="sxs-lookup"><span data-stu-id="41a95-246">**tooadd slider bar related code**</span></span>

1. <span data-ttu-id="41a95-247">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy **MainPage.xaml**, a następnie kliknij przycisk **kod widoku**.</span><span class="sxs-lookup"><span data-stu-id="41a95-247">From Solution Explorer, right click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="41a95-248">Na początku hello pliku hello, Dodaj następujące hello instrukcję using:</span><span class="sxs-lookup"><span data-stu-id="41a95-248">At hello beginning of hello file, add hello following using statement:</span></span>
      
        using Windows.UI.Core;
3. <span data-ttu-id="41a95-249">Witaj wewnątrz **MainPage** klasy, Dodaj następujące elementy członkowskie danych hello:</span><span class="sxs-lookup"><span data-stu-id="41a95-249">Inside hello **MainPage** class, add hello following data members:</span></span>
   
         public static CoreDispatcher _dispatcher;
         private DispatcherTimer sliderPositionUpdateDispatcher;
4. <span data-ttu-id="41a95-250">Na końcu hello hello **MainPage** konstruktora, Dodaj hello następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="41a95-250">At hello end of hello **MainPage** constructor, add hello following code:</span></span>
   
         _dispatcher = Window.Current.Dispatcher;
         PointerEventHandler pointerpressedhandler = new PointerEventHandler(sliderProgress_PointerPressed);
         sliderProgress.AddHandler(Control.PointerPressedEvent, pointerpressedhandler, true);    
5. <span data-ttu-id="41a95-251">Na końcu hello hello **MainPage** klasy, Dodaj hello następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="41a95-251">At hello end of hello **MainPage** class, add hello following code:</span></span>

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
><span data-ttu-id="41a95-252">CoreDispatcher jest zmian używanych toomake wątku toohello interfejsu użytkownika z wątku interfejsu użytkownika innych niż.</span><span class="sxs-lookup"><span data-stu-id="41a95-252">CoreDispatcher is used toomake changes toohello UI thread from non UI Thread.</span></span> <span data-ttu-id="41a95-253">W przypadku "wąskie gardło" na Wątek dyspozytora developer można wybrać dyspozytora toouse pod warunkiem przez element interfejsu użytkownika, że jego zamierza tooupdate.</span><span class="sxs-lookup"><span data-stu-id="41a95-253">In case of bottleneck on dispatcher thread, developer can choose toouse dispatcher provided by UI-element he/she intends tooupdate.</span></span>  <span data-ttu-id="41a95-254">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="41a95-254">For example:</span></span>
   
         await sliderProgress.Dispatcher.RunAsync(CoreDispatcherPriority.Normal, () => { TimeSpan 

         timespan = new TimeSpan(adaptiveSourceStatusUpdate.EndTime); 
         double absvalue  = (int)Math.Round(timespan.TotalSeconds, MidpointRounding.AwayFromZero); 

         sliderProgress.Maximum = absvalue; }); 
6. <span data-ttu-id="41a95-255">Na końcu hello hello **mediaElement_AdaptiveSourceStatusUpdated** metody, Dodaj hello następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="41a95-255">At hello end of hello **mediaElement_AdaptiveSourceStatusUpdated** method, add hello following code:</span></span>

         setSliderStartTime(args.StartTime);
         setSliderEndTime(args.EndTime);
7. <span data-ttu-id="41a95-256">Na końcu hello hello **MediaOpened** metody, Dodaj hello następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="41a95-256">At hello end of hello **MediaOpened** method, add hello following code:</span></span>

         sliderProgress.StepFrequency = SliderFrequency(mediaElement.NaturalDuration.TimeSpan);
         sliderProgress.Width = mediaElement.Width;
         setupTimer();
8. <span data-ttu-id="41a95-257">Naciśnij klawisz **CTRL + S** toosave hello pliku.</span><span class="sxs-lookup"><span data-stu-id="41a95-257">Press **CTRL+S** toosave hello file.</span></span>

<span data-ttu-id="41a95-258">**toocompile i testowania aplikacji hello**</span><span class="sxs-lookup"><span data-stu-id="41a95-258">**toocompile and test hello application**</span></span>

1. <span data-ttu-id="41a95-259">Naciśnij klawisz **F6** toocompile hello projektu.</span><span class="sxs-lookup"><span data-stu-id="41a95-259">Press **F6** toocompile hello project.</span></span> 
2. <span data-ttu-id="41a95-260">Naciśnij klawisz **F5** toorun hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="41a95-260">Press **F5** toorun hello application.</span></span>
3. <span data-ttu-id="41a95-261">U góry hello aplikacji hello możesz użyć domyślnej hello Smooth Streaming URL lub wprowadź inną.</span><span class="sxs-lookup"><span data-stu-id="41a95-261">At hello top of hello application, you can either use hello default Smooth Streaming URL or enter a different one.</span></span> 
4. <span data-ttu-id="41a95-262">Kliknij przycisk **Ustaw źródło**.</span><span class="sxs-lookup"><span data-stu-id="41a95-262">Click **Set Source**.</span></span> 
5. <span data-ttu-id="41a95-263">Test hello paska suwaka.</span><span class="sxs-lookup"><span data-stu-id="41a95-263">Test hello slider bar.</span></span>

<span data-ttu-id="41a95-264">Lekcja 2 została ukończona.</span><span class="sxs-lookup"><span data-stu-id="41a95-264">You have completed lesson 2.</span></span>  <span data-ttu-id="41a95-265">W tej lekcji dodano tooapplication suwaka.</span><span class="sxs-lookup"><span data-stu-id="41a95-265">In this lesson you added a slider tooapplication.</span></span> 

## <a name="lesson-3-select-smooth-streaming-streams"></a><span data-ttu-id="41a95-266">Lekcja 3: Wybierz Smooth Streaming strumieni</span><span class="sxs-lookup"><span data-stu-id="41a95-266">Lesson 3: Select Smooth Streaming Streams</span></span>
<span data-ttu-id="41a95-267">Smooth Streaming jest funkcją toostream zawartości z wielu ścieżek audio języka, które można wybrać przez hello przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="41a95-267">Smooth Streaming is capable toostream content with multiple language audio tracks that are selectable by hello viewers.</span></span>  <span data-ttu-id="41a95-268">W tej lekcji spowoduje włączenie strumienie tooselect przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="41a95-268">In this lesson, you will enable viewers tooselect streams.</span></span> <span data-ttu-id="41a95-269">Tej lekcji zawiera hello następujące procedury:</span><span class="sxs-lookup"><span data-stu-id="41a95-269">This lesson contains hello following procedures:</span></span>

1. <span data-ttu-id="41a95-270">Modyfikowanie pliku XAML hello</span><span class="sxs-lookup"><span data-stu-id="41a95-270">Modify hello XAML file</span></span>
2. <span data-ttu-id="41a95-271">Modyfikowanie pliku behand kodu hello</span><span class="sxs-lookup"><span data-stu-id="41a95-271">Modify hello code behand file</span></span>
3. <span data-ttu-id="41a95-272">Kompilowanie i testowanie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="41a95-272">Compile and test hello application</span></span>

<span data-ttu-id="41a95-273">**Plik XAML hello toomodify**</span><span class="sxs-lookup"><span data-stu-id="41a95-273">**toomodify hello XAML file**</span></span>

1. <span data-ttu-id="41a95-274">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy **MainPage.xaml**, a następnie kliknij przycisk **Widok projektanta**.</span><span class="sxs-lookup"><span data-stu-id="41a95-274">From Solution Explorer, right-click **MainPage.xaml**, and then click **View Designer**.</span></span>
2. <span data-ttu-id="41a95-275">Zlokalizuj &lt;Grid.RowDefinitions&gt;i zmodyfikować hello RowDefinitions, aby ich wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="41a95-275">Locate &lt;Grid.RowDefinitions&gt;, and modify hello RowDefinitions so they looks like:</span></span>
   
         <Grid.RowDefinitions>            
            <RowDefinition Height="20"/>
            <RowDefinition Height="50"/>
            <RowDefinition Height="100"/>
            <RowDefinition Height="80"/>
            <RowDefinition Height="50"/>
         </Grid.RowDefinitions>
3. <span data-ttu-id="41a95-276">Witaj wewnątrz &lt;siatki&gt;&lt;/Grid&gt; tagów, Dodaj hello poniższy kod toodefine kontrolki listbox, aby użytkownicy mogli widzieć hello listę dostępnych strumieni i wybierz strumieni:</span><span class="sxs-lookup"><span data-stu-id="41a95-276">Inside hello &lt;Grid&gt;&lt;/Grid&gt; tags, add hello following code toodefine a listbox control, so users can see hello list of available streams, and select streams:</span></span>

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
4. <span data-ttu-id="41a95-277">Naciśnij klawisz **CTRL + S** toosave hello zmiany.</span><span class="sxs-lookup"><span data-stu-id="41a95-277">Press **CTRL+S** toosave hello changes.</span></span>

<span data-ttu-id="41a95-278">**toomodify hello kodzie pliku**</span><span class="sxs-lookup"><span data-stu-id="41a95-278">**toomodify hello code behind file**</span></span>

1. <span data-ttu-id="41a95-279">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy **MainPage.xaml**, a następnie kliknij przycisk **kod widoku**.</span><span class="sxs-lookup"><span data-stu-id="41a95-279">From Solution Explorer, right-click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="41a95-280">W obszarze nazw SSPlayer hello Dodaj nową klasę:</span><span class="sxs-lookup"><span data-stu-id="41a95-280">Inside hello SSPlayer namespace, add a new class:</span></span>
   
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
3. <span data-ttu-id="41a95-281">Na początku hello hello klasy MainPage, Dodaj hello następujące definicje zmiennych:</span><span class="sxs-lookup"><span data-stu-id="41a95-281">At hello beginning of hello MainPage class, add hello following variable definitions:</span></span>
   
         private List<Stream> availableStreams;
         private List<Stream> availableAudioStreams;
         private List<Stream> availableTextStreams;
         private List<Stream> availableVideoStreams;
4. <span data-ttu-id="41a95-282">Wewnątrz klasy MainPage hello Dodaj powitania od regionu:</span><span class="sxs-lookup"><span data-stu-id="41a95-282">Inside hello MainPage class, add hello following region:</span></span>
   
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
5. <span data-ttu-id="41a95-283">Zlokalizuj metody mediaElement_ManifestReady hello, Dołącz hello następującego kodu na końcu hello hello funkcji:</span><span class="sxs-lookup"><span data-stu-id="41a95-283">Locate hello mediaElement_ManifestReady method, append hello following code at hello end of hello function:</span></span>
   
        getStreams(manifestObject);
        refreshAvailableStreamsListBoxItemSource();
   
    <span data-ttu-id="41a95-284">Tak, gdy element MediaElement manifestu jest gotowy, hello kod pobiera listę dostępnych strumieni hello i wypełnia hello pole listy interfejsu użytkownika z listy hello.</span><span class="sxs-lookup"><span data-stu-id="41a95-284">So when MediaElement manifest is ready, hello code gets a list of hello available streams, and populates hello UI list box with hello list.</span></span>
6. <span data-ttu-id="41a95-285">Wewnątrz klasy MainPage hello, zlokalizuj przycisków interfejsu użytkownika powitania kliknij region zdarzenia, a następnie dodaj powitania po definicji funkcji:</span><span class="sxs-lookup"><span data-stu-id="41a95-285">Inside hello MainPage class, locate hello UI buttons click events region, and then add hello following function definition:</span></span>
   
        private void btnChangeStream_Click(object sender, RoutedEventArgs e)
        {
            List<IManifestStream> selectedStreams = new List<IManifestStream>();
   
            // Create a list of hello selected streams
            createSelectedStreamsList(selectedStreams);
   
            // Change streams on hello presentation
            changeStreams(selectedStreams);
        }

<span data-ttu-id="41a95-286">**toocompile i testowania aplikacji hello**</span><span class="sxs-lookup"><span data-stu-id="41a95-286">**toocompile and test hello application**</span></span>

1. <span data-ttu-id="41a95-287">Naciśnij klawisz **F6** toocompile hello projektu.</span><span class="sxs-lookup"><span data-stu-id="41a95-287">Press **F6** toocompile hello project.</span></span> 
2. <span data-ttu-id="41a95-288">Naciśnij klawisz **F5** toorun hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="41a95-288">Press **F5** toorun hello application.</span></span>
3. <span data-ttu-id="41a95-289">U góry hello aplikacji hello możesz użyć domyślnej hello Smooth Streaming URL lub wprowadź inną.</span><span class="sxs-lookup"><span data-stu-id="41a95-289">At hello top of hello application, you can either use hello default Smooth Streaming URL or enter a different one.</span></span> 
4. <span data-ttu-id="41a95-290">Kliknij przycisk **Ustaw źródło**.</span><span class="sxs-lookup"><span data-stu-id="41a95-290">Click **Set Source**.</span></span> 
5. <span data-ttu-id="41a95-291">język domyślny Hello jest audio_eng.</span><span class="sxs-lookup"><span data-stu-id="41a95-291">hello default language is audio_eng.</span></span> <span data-ttu-id="41a95-292">Spróbuj tooswitch między audio_eng i audio_es.</span><span class="sxs-lookup"><span data-stu-id="41a95-292">Try tooswitch between audio_eng and audio_es.</span></span> <span data-ttu-id="41a95-293">Zawsze, gdy, wybierz nowego strumienia, należy kliknąć przycisk Prześlij hello.</span><span class="sxs-lookup"><span data-stu-id="41a95-293">Everytime, you select a new stream, you must click hello Submit button.</span></span>

<span data-ttu-id="41a95-294">Ukończono Lekcja 3.</span><span class="sxs-lookup"><span data-stu-id="41a95-294">You have completed lesson 3.</span></span>  <span data-ttu-id="41a95-295">W tej lekcji możesz dodać hello funkcji toochoose strumieni.</span><span class="sxs-lookup"><span data-stu-id="41a95-295">In this lesson, you add hello functionality toochoose streams.</span></span>

## <a name="lesson-4-select-smooth-streaming-tracks"></a><span data-ttu-id="41a95-296">Lekcja 4: Wybierz Smooth Streaming ścieżki</span><span class="sxs-lookup"><span data-stu-id="41a95-296">Lesson 4: Select Smooth Streaming Tracks</span></span>
<span data-ttu-id="41a95-297">Prezentacja Smooth Streaming może zawierać wiele plików wideo zakodowane za pomocą różne poziomy jakości (szybkości transmisji bitów) i rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="41a95-297">A Smooth Streaming presentation can contain multiple video files encoded with different quality levels (bit rates) and resolutions.</span></span> <span data-ttu-id="41a95-298">W tej lekcji umożliwi użytkownikom tooselect ścieżki.</span><span class="sxs-lookup"><span data-stu-id="41a95-298">In this lesson, you will enable users tooselect tracks.</span></span> <span data-ttu-id="41a95-299">Tej lekcji zawiera hello następujące procedury:</span><span class="sxs-lookup"><span data-stu-id="41a95-299">This lesson contains hello following procedures:</span></span>

1. <span data-ttu-id="41a95-300">Modyfikowanie pliku XAML hello</span><span class="sxs-lookup"><span data-stu-id="41a95-300">Modify hello XAML file</span></span>
2. <span data-ttu-id="41a95-301">Modyfikowanie pliku behand kodu hello</span><span class="sxs-lookup"><span data-stu-id="41a95-301">Modify hello code behand file</span></span>
3. <span data-ttu-id="41a95-302">Kompilowanie i testowanie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="41a95-302">Compile and test hello application</span></span>

<span data-ttu-id="41a95-303">**Plik XAML hello toomodify**</span><span class="sxs-lookup"><span data-stu-id="41a95-303">**toomodify hello XAML file**</span></span>

1. <span data-ttu-id="41a95-304">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy **MainPage.xaml**, a następnie kliknij przycisk **Widok projektanta**.</span><span class="sxs-lookup"><span data-stu-id="41a95-304">From Solution Explorer, right-click **MainPage.xaml**, and then click **View Designer**.</span></span>
2. <span data-ttu-id="41a95-305">Zlokalizuj hello &lt;siatki&gt; tag o nazwie hello **gridStreamAndBitrateSelection**, Dołącz hello następującego kodu na końcu hello hello tagu:</span><span class="sxs-lookup"><span data-stu-id="41a95-305">Locate hello &lt;Grid&gt; tag with hello name **gridStreamAndBitrateSelection**, append hello following code at hello end of hello tag:</span></span>
   
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
3. <span data-ttu-id="41a95-306">Naciśnij klawisz **CTRL + S** toosave zmieniane</span><span class="sxs-lookup"><span data-stu-id="41a95-306">Press **CTRL+S** toosave he changes</span></span>

<span data-ttu-id="41a95-307">**toomodify hello kodzie pliku**</span><span class="sxs-lookup"><span data-stu-id="41a95-307">**toomodify hello code behind file**</span></span>

1. <span data-ttu-id="41a95-308">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy **MainPage.xaml**, a następnie kliknij przycisk **kod widoku**.</span><span class="sxs-lookup"><span data-stu-id="41a95-308">From Solution Explorer, right-click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="41a95-309">W obszarze nazw SSPlayer hello Dodaj nową klasę:</span><span class="sxs-lookup"><span data-stu-id="41a95-309">Inside hello SSPlayer namespace, add a new class:</span></span>
   
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
3. <span data-ttu-id="41a95-310">Na początku hello hello klasy MainPage, Dodaj hello następujące definicje zmiennych:</span><span class="sxs-lookup"><span data-stu-id="41a95-310">At hello beginning of hello MainPage class, add hello following variable definitions:</span></span>
   
        private List<Track> availableTracks;
4. <span data-ttu-id="41a95-311">Wewnątrz klasy MainPage hello Dodaj powitania od regionu:</span><span class="sxs-lookup"><span data-stu-id="41a95-311">Inside hello MainPage class, add hello following region:</span></span>
   
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
5. <span data-ttu-id="41a95-312">Zlokalizuj metody mediaElement_ManifestReady hello, Dołącz hello następującego kodu na końcu hello hello funkcji:</span><span class="sxs-lookup"><span data-stu-id="41a95-312">Locate hello mediaElement_ManifestReady method, append hello following code at hello end of hello function:</span></span>
   
         getTracks(manifestObject);
         refreshAvailableTracksListBoxItemSource();
6. <span data-ttu-id="41a95-313">Wewnątrz klasy MainPage hello, zlokalizuj przycisków interfejsu użytkownika powitania kliknij region zdarzenia, a następnie dodaj powitania po definicji funkcji:</span><span class="sxs-lookup"><span data-stu-id="41a95-313">Inside hello MainPage class, locate hello UI buttons click events region, and then add hello following function definition:</span></span>
   
         private void btnChangeStream_Click(object sender, RoutedEventArgs e)
         {
            List<IManifestStream> selectedStreams = new List<IManifestStream>();

            // Create a list of hello selected streams
            createSelectedStreamsList(selectedStreams);

            // Change streams on hello presentation
            changeStreams(selectedStreams);
         }

<span data-ttu-id="41a95-314">**toocompile i testowania aplikacji hello**</span><span class="sxs-lookup"><span data-stu-id="41a95-314">**toocompile and test hello application**</span></span>

1. <span data-ttu-id="41a95-315">Naciśnij klawisz **F6** toocompile hello projektu.</span><span class="sxs-lookup"><span data-stu-id="41a95-315">Press **F6** toocompile hello project.</span></span> 
2. <span data-ttu-id="41a95-316">Naciśnij klawisz **F5** toorun hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="41a95-316">Press **F5** toorun hello application.</span></span>
3. <span data-ttu-id="41a95-317">U góry hello aplikacji hello możesz użyć domyślnej hello Smooth Streaming URL lub wprowadź inną.</span><span class="sxs-lookup"><span data-stu-id="41a95-317">At hello top of hello application, you can either use hello default Smooth Streaming URL or enter a different one.</span></span> 
4. <span data-ttu-id="41a95-318">Kliknij przycisk **Ustaw źródło**.</span><span class="sxs-lookup"><span data-stu-id="41a95-318">Click **Set Source**.</span></span> 
5. <span data-ttu-id="41a95-319">Domyślnie wszystkie ścieżki hello strumienia wideo hello wybrane.</span><span class="sxs-lookup"><span data-stu-id="41a95-319">By default, all of hello tracks of hello video stream are selected.</span></span> <span data-ttu-id="41a95-320">Witaj tooexperiment bit szybkość zmian, można wybrać hello najniższa szybkość transmisji bitów dostępne, a następnie wybierz hello najwyższą szybkość transmisji bitów dostępne.</span><span class="sxs-lookup"><span data-stu-id="41a95-320">tooexperiment hello bit rate changes, you can select hello lowest bit rate available, and then select hello highest bit rate available.</span></span> <span data-ttu-id="41a95-321">Należy kliknąć przesyłania po każdej zmianie.</span><span class="sxs-lookup"><span data-stu-id="41a95-321">You must click Submit after each change.</span></span>  <span data-ttu-id="41a95-322">Zmiany jakości wideo hello jest widoczny.</span><span class="sxs-lookup"><span data-stu-id="41a95-322">You can see hello video quality changes.</span></span>

<span data-ttu-id="41a95-323">Ukończono lekcji 4.</span><span class="sxs-lookup"><span data-stu-id="41a95-323">You have completed lesson 4.</span></span>  <span data-ttu-id="41a95-324">W tej lekcji możesz dodać hello funkcji toochoose ścieżki.</span><span class="sxs-lookup"><span data-stu-id="41a95-324">In this lesson, you add hello functionality toochoose tracks.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="41a95-325">Ścieżki szkoleniowe dotyczące usługi Media Services</span><span class="sxs-lookup"><span data-stu-id="41a95-325">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="41a95-326">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="41a95-326">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="other-resources"></a><span data-ttu-id="41a95-327">Inne zasoby:</span><span class="sxs-lookup"><span data-stu-id="41a95-327">Other Resources:</span></span>
* [<span data-ttu-id="41a95-328">Jak toobuild aplikacja Smooth JavaScript 8 Windows przesyłania strumieniowego o funkcje zaawansowane</span><span class="sxs-lookup"><span data-stu-id="41a95-328">How toobuild a Smooth Streaming Windows 8 JavaScript application with advanced features</span></span>](http://blogs.iis.net/cenkd/archive/2012/08/10/how-to-build-a-smooth-streaming-windows-8-javascript-application-with-advanced-features.aspx)
* [<span data-ttu-id="41a95-329">Płynnego przesyłania strumieniowego — omówienie</span><span class="sxs-lookup"><span data-stu-id="41a95-329">Smooth Streaming Technical Overview</span></span>](http://www.iis.net/learn/media/on-demand-smooth-streaming/smooth-streaming-technical-overview)

[PlayerApplication]: ./media/media-services-build-smooth-streaming-apps/SSClientWin8-1.png
[CodeViewPic]: ./media/media-services-build-smooth-streaming-apps/SSClientWin8-2.png

