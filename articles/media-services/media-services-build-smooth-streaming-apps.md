---
title: Funkcje Smooth Streaming samouczek aplikacji Sklepu Windows | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak używać usługi Azure Media Services do tworzenia aplikacji Sklepu Windows w języku C# za pomocą formantu XML MediaElement do strumienia Smooth odtwarzania zawartości."
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
ms.openlocfilehash: c9bb3b1915543fea3561cb309f55c4e8a74ded6d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-build-a-smooth-streaming-windows-store-application"></a><span data-ttu-id="22f86-103">Jak tworzyć Smooth Streaming aplikację ze Sklepu Windows</span><span class="sxs-lookup"><span data-stu-id="22f86-103">How to Build a Smooth Streaming Windows Store Application</span></span>

<span data-ttu-id="22f86-104">Smooth Streaming klienta zestawu SDK dla systemu Windows 8 umożliwia deweloperom tworzenie aplikacji Sklepu Windows, które można odtwarzać zawartości na żądanie i na żywo Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="22f86-104">The Smooth Streaming Client SDK for Windows 8 enables developers to build Windows Store applications that can play on-demand and live Smooth Streaming content.</span></span> <span data-ttu-id="22f86-105">Oprócz podstawowych odtwarzania zawartości Smooth Streaming, zestaw SDK udostępnia zaawansowane funkcje, takie jak Microsoft PlayReady ochrony ograniczenie poziomu jakości, Live DVR, strumieniem audio przełączania, nasłuchiwanie aktualizacji stanu (np. zmiany poziomu jakości) i zdarzenia błędu i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="22f86-105">In addition to the basic playback of Smooth Streaming content, the SDK also provides rich features like Microsoft PlayReady protection, quality level restriction, Live DVR, audio stream switching, listening for status updates (such as quality level changes) and error events, and so on.</span></span> <span data-ttu-id="22f86-106">Aby uzyskać więcej informacji na obsługiwanych funkcji, zobacz [informacje o wersji](http://www.iis.net/learn/media/smooth-streaming/smooth-streaming-client-sdk-for-windows-8-release-notes).</span><span class="sxs-lookup"><span data-stu-id="22f86-106">For more information of the supported features, see the [release notes](http://www.iis.net/learn/media/smooth-streaming/smooth-streaming-client-sdk-for-windows-8-release-notes).</span></span> <span data-ttu-id="22f86-107">Aby uzyskać więcej informacji, zobacz [Framework Player dla systemu Windows 8](http://playerframework.codeplex.com/).</span><span class="sxs-lookup"><span data-stu-id="22f86-107">For more information, see [Player Framework for Windows 8](http://playerframework.codeplex.com/).</span></span> 

<span data-ttu-id="22f86-108">Ten samouczek zawiera cztery lekcje:</span><span class="sxs-lookup"><span data-stu-id="22f86-108">This tutorial contains four lessons:</span></span>

1. <span data-ttu-id="22f86-109">Tworzenie podstawowej płynnego przesyłania strumieniowego aplikacji sklepu</span><span class="sxs-lookup"><span data-stu-id="22f86-109">Create a Basic Smooth Streaming Store Application</span></span>
2. <span data-ttu-id="22f86-110">Dodawanie paska suwaka do kontrolowania postępu nośnika</span><span class="sxs-lookup"><span data-stu-id="22f86-110">Add a Slider Bar to Control the Media Progress</span></span>
3. <span data-ttu-id="22f86-111">Wybierz Smooth Streaming strumieni</span><span class="sxs-lookup"><span data-stu-id="22f86-111">Select Smooth Streaming Streams</span></span>
4. <span data-ttu-id="22f86-112">Wybierz Smooth Streaming ścieżki</span><span class="sxs-lookup"><span data-stu-id="22f86-112">Select Smooth Streaming Tracks</span></span>

## <a name="prerequisites"></a><span data-ttu-id="22f86-113">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="22f86-113">Prerequisites</span></span>
* <span data-ttu-id="22f86-114">Windows 8, 32-bitowy lub 64-bitowej.</span><span class="sxs-lookup"><span data-stu-id="22f86-114">Windows 8 32-bit or 64-bit.</span></span> <span data-ttu-id="22f86-115">Możesz uzyskać [systemu Windows 8 Enterprise Evaluation](http://msdn.microsoft.com/evalcenter/jj554510.aspx) w witrynie MSDN.</span><span class="sxs-lookup"><span data-stu-id="22f86-115">You can get [Windows 8 Enterprise Evaluation](http://msdn.microsoft.com/evalcenter/jj554510.aspx) from MSDN.</span></span>
* <span data-ttu-id="22f86-116">Program Visual Studio 2012 lub Visual Studio Express 2012 (lub nowszy).</span><span class="sxs-lookup"><span data-stu-id="22f86-116">Visual Studio 2012 or Visual Studio Express 2012 (or a later version).</span></span> <span data-ttu-id="22f86-117">Można pobrać wersję próbną z [tutaj](http://www.microsoft.com/visualstudio/11/downloads).</span><span class="sxs-lookup"><span data-stu-id="22f86-117">You can get the trial version from [here](http://www.microsoft.com/visualstudio/11/downloads).</span></span>
* <span data-ttu-id="22f86-118">[Microsoft Smooth Streaming Client zestawu SDK dla systemu Windows 8](http://visualstudiogallery.msdn.microsoft.com/04423d13-3b3e-4741-a01c-1ae29e84fea6?SRC=Homehttp://visualstudiogallery.msdn.microsoft.com/04423d13-3b3e-4741-a01c-1ae29e84fea6?SRC=Home).</span><span class="sxs-lookup"><span data-stu-id="22f86-118">[Microsoft Smooth Streaming Client SDK for Windows 8](http://visualstudiogallery.msdn.microsoft.com/04423d13-3b3e-4741-a01c-1ae29e84fea6?SRC=Homehttp://visualstudiogallery.msdn.microsoft.com/04423d13-3b3e-4741-a01c-1ae29e84fea6?SRC=Home).</span></span>

<span data-ttu-id="22f86-119">Gotowego rozwiązania dla każdej lekcji można pobrać z przykładów kodu deweloperów MSDN (Galeria kodu):</span><span class="sxs-lookup"><span data-stu-id="22f86-119">The completed solution for each lesson can be downloaded from MSDN Developer Code Samples (Code Gallery):</span></span> 

* <span data-ttu-id="22f86-120">[Lekcja 1](http://code.msdn.microsoft.com/Smooth-Streaming-Client-0bb1471f) — sprawne prostego systemu Windows 8 przesyłania strumieniowego Media Player</span><span class="sxs-lookup"><span data-stu-id="22f86-120">[Lesson 1](http://code.msdn.microsoft.com/Smooth-Streaming-Client-0bb1471f) - A Simple Windows 8 Smooth Streaming Media Player,</span></span> 
* <span data-ttu-id="22f86-121">[Lekcja 2](http://code.msdn.microsoft.com/A-simple-Windows-8-Smooth-ee98f63a) — sprawne prostego systemu Windows 8 przesyłania strumieniowego Media Player paska suwaka formantu</span><span class="sxs-lookup"><span data-stu-id="22f86-121">[Lesson 2](http://code.msdn.microsoft.com/A-simple-Windows-8-Smooth-ee98f63a) - A Simple Windows 8 Smooth Streaming Media Player with a Slider Bar Control,</span></span> 
* <span data-ttu-id="22f86-122">[Lekcja 3](http://code.msdn.microsoft.com/A-Windows-8-Smooth-883c3b44) — sprawne systemu Windows 8 przesyłania strumieniowego Media Player do wyboru strumienia</span><span class="sxs-lookup"><span data-stu-id="22f86-122">[Lesson 3](http://code.msdn.microsoft.com/A-Windows-8-Smooth-883c3b44) - A Windows 8 Smooth Streaming Media Player with Stream Selection,</span></span>  
* <span data-ttu-id="22f86-123">[Lekcja 4](http://code.msdn.microsoft.com/A-Windows-8-Smooth-aa9e4907) — sprawne systemu Windows 8 przesyłania strumieniowego Media Player śledzenie zaznaczenia.</span><span class="sxs-lookup"><span data-stu-id="22f86-123">[Lesson 4](http://code.msdn.microsoft.com/A-Windows-8-Smooth-aa9e4907)  - A Windows 8 Smooth Streaming Media Player with Track Selection.</span></span>

## <a name="lesson-1-create-a-basic-smooth-streaming-store-application"></a><span data-ttu-id="22f86-124">Lekcja 1: Tworzenie podstawowej płynnego przesyłania strumieniowego aplikacji sklepu</span><span class="sxs-lookup"><span data-stu-id="22f86-124">Lesson 1: Create a Basic Smooth Streaming Store Application</span></span>

<span data-ttu-id="22f86-125">W tej lekcji utworzysz aplikację ze Sklepu Windows za pomocą formantu MediaElement do odtwarzania Smooth Stream zawartości.</span><span class="sxs-lookup"><span data-stu-id="22f86-125">In this lesson, you will create a Windows Store application with a MediaElement control to play Smooth Stream content.</span></span>  <span data-ttu-id="22f86-126">Działającej aplikacji wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="22f86-126">The running application looks like:</span></span>

![Przykładowa aplikacja Sklepu Windows Smooth Streaming][PlayerApplication]

<span data-ttu-id="22f86-128">Aby uzyskać więcej informacji na temat tworzenia aplikacji Sklepu Windows, temacie [tworzenie wspaniałych aplikacji dla systemu Windows 8](http://msdn.microsoft.com/windows/apps/br229512.aspx).</span><span class="sxs-lookup"><span data-stu-id="22f86-128">For more information on developing Windows Store application, see [Develop Great Apps for Windows 8](http://msdn.microsoft.com/windows/apps/br229512.aspx).</span></span> <span data-ttu-id="22f86-129">W tej lekcji obejmuje następujące procedury:</span><span class="sxs-lookup"><span data-stu-id="22f86-129">This lesson contains the following procedures:</span></span>

1. <span data-ttu-id="22f86-130">Tworzenie projektu ze Sklepu Windows</span><span class="sxs-lookup"><span data-stu-id="22f86-130">Create a Windows Store project</span></span>
2. <span data-ttu-id="22f86-131">Projektowanie interfejsu użytkownika (XAML)</span><span class="sxs-lookup"><span data-stu-id="22f86-131">Design the user interface (XAML)</span></span>
3. <span data-ttu-id="22f86-132">Zmodyfikuj plik związany z kodem</span><span class="sxs-lookup"><span data-stu-id="22f86-132">Modify the code behind file</span></span>
4. <span data-ttu-id="22f86-133">Kompilowanie i testowanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="22f86-133">Compile and test the application</span></span>

<span data-ttu-id="22f86-134">**Aby utworzyć projekt Sklepu Windows**</span><span class="sxs-lookup"><span data-stu-id="22f86-134">**To create a Windows Store project**</span></span>

1. <span data-ttu-id="22f86-135">Uruchom program Visual Studio 2012 lub nowszym.</span><span class="sxs-lookup"><span data-stu-id="22f86-135">Run Visual Studio 2012 or later.</span></span>
2. <span data-ttu-id="22f86-136">W menu **PLIK** kliknij pozycję **Nowy**, a następnie kliknij pozycję **Projekt**.</span><span class="sxs-lookup"><span data-stu-id="22f86-136">From the **FILE** menu, click **New**, and then click **Project**.</span></span>
3. <span data-ttu-id="22f86-137">W oknie dialogowym Nowy projekt wpisz lub wybierz następujące wartości:</span><span class="sxs-lookup"><span data-stu-id="22f86-137">From the New Project dialog, type or select  the following values:</span></span>

| <span data-ttu-id="22f86-138">Nazwa</span><span class="sxs-lookup"><span data-stu-id="22f86-138">Name</span></span> | <span data-ttu-id="22f86-139">Wartość</span><span class="sxs-lookup"><span data-stu-id="22f86-139">Value</span></span> |
| --- | --- |
| <span data-ttu-id="22f86-140">Grupa szablonów</span><span class="sxs-lookup"><span data-stu-id="22f86-140">Template group</span></span> |<span data-ttu-id="22f86-141">Zainstalowane/szablony/Visual C# / ze Sklepu Windows</span><span class="sxs-lookup"><span data-stu-id="22f86-141">Installed/Templates/Visual C#/Windows Store</span></span> |
| <span data-ttu-id="22f86-142">Szablon</span><span class="sxs-lookup"><span data-stu-id="22f86-142">Template</span></span> |<span data-ttu-id="22f86-143">Pusta aplikacja (XAML)</span><span class="sxs-lookup"><span data-stu-id="22f86-143">Blank App (XAML)</span></span> |
| <span data-ttu-id="22f86-144">Nazwa</span><span class="sxs-lookup"><span data-stu-id="22f86-144">Name</span></span> |<span data-ttu-id="22f86-145">SSPlayer</span><span class="sxs-lookup"><span data-stu-id="22f86-145">SSPlayer</span></span> |
| <span data-ttu-id="22f86-146">Lokalizacja</span><span class="sxs-lookup"><span data-stu-id="22f86-146">Location</span></span> |<span data-ttu-id="22f86-147">C:\SSTutorials</span><span class="sxs-lookup"><span data-stu-id="22f86-147">C:\SSTutorials</span></span> |
| <span data-ttu-id="22f86-148">Nazwa rozwiązania</span><span class="sxs-lookup"><span data-stu-id="22f86-148">Solution Name</span></span> |<span data-ttu-id="22f86-149">SSPlayer</span><span class="sxs-lookup"><span data-stu-id="22f86-149">SSPlayer</span></span> |
| <span data-ttu-id="22f86-150">Utwórz katalog rozwiązania</span><span class="sxs-lookup"><span data-stu-id="22f86-150">Create directory for solution</span></span> |<span data-ttu-id="22f86-151">(wybrane)</span><span class="sxs-lookup"><span data-stu-id="22f86-151">(selected)</span></span> |

1. <span data-ttu-id="22f86-152">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="22f86-152">Click **OK**.</span></span>

<span data-ttu-id="22f86-153">**Aby dodać odwołanie do Smooth Streaming SDK klienta**</span><span class="sxs-lookup"><span data-stu-id="22f86-153">**To add a reference to the Smooth Streaming Client SDK**</span></span>

1. <span data-ttu-id="22f86-154">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy **SSPlayer**, a następnie kliknij przycisk **Dodaj odwołanie**.</span><span class="sxs-lookup"><span data-stu-id="22f86-154">From Solution Explorer, right-click **SSPlayer**, and then click **Add Reference**.</span></span>
2. <span data-ttu-id="22f86-155">Wpisz lub wybierz poniższe wartości:</span><span class="sxs-lookup"><span data-stu-id="22f86-155">Type or select the following values:</span></span>

| <span data-ttu-id="22f86-156">Nazwa</span><span class="sxs-lookup"><span data-stu-id="22f86-156">Name</span></span> | <span data-ttu-id="22f86-157">Wartość</span><span class="sxs-lookup"><span data-stu-id="22f86-157">Value</span></span> |
| --- | --- |
| <span data-ttu-id="22f86-158">Grupy odwołania</span><span class="sxs-lookup"><span data-stu-id="22f86-158">Reference group</span></span> |<span data-ttu-id="22f86-159">Rozszerzenia/systemu Windows</span><span class="sxs-lookup"><span data-stu-id="22f86-159">Windows/Extensions</span></span> |
| <span data-ttu-id="22f86-160">Dokumentacja</span><span class="sxs-lookup"><span data-stu-id="22f86-160">Reference</span></span> |<span data-ttu-id="22f86-161">Wybierz Microsoft Smooth Streaming Client zestawu SDK dla systemu Windows 8 i Microsoft Visual C++ Runtime Package</span><span class="sxs-lookup"><span data-stu-id="22f86-161">Select Microsoft Smooth Streaming Client SDK for Windows 8 and Microsoft Visual C++ Runtime Package</span></span> |

1. <span data-ttu-id="22f86-162">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="22f86-162">Click **OK**.</span></span> 

<span data-ttu-id="22f86-163">Po dodaniu odwołań, musisz wybrać platformę docelową (x64 lub x86), Dodawanie odwołania nie będą działać dla konfiguracji platformy dowolnego Procesora.</span><span class="sxs-lookup"><span data-stu-id="22f86-163">After adding the references, you must select the targeted platform (x64 or x86), adding references will not work for Any CPU platform configuration.</span></span>  <span data-ttu-id="22f86-164">W Eksploratorze rozwiązań pojawi się żółty znak ostrzeżenie tych dodać odwołań.</span><span class="sxs-lookup"><span data-stu-id="22f86-164">In solution explorer, you will see yellow warning mark for these added references.</span></span>

<span data-ttu-id="22f86-165">**Projektowanie interfejsu użytkownika player**</span><span class="sxs-lookup"><span data-stu-id="22f86-165">**To design the player user interface**</span></span>

1. <span data-ttu-id="22f86-166">W Eksploratorze rozwiązań kliknij dwukrotnie kliknij **MainPage.xaml** aby otworzyć go w widoku Projekt.</span><span class="sxs-lookup"><span data-stu-id="22f86-166">From Solution Explorer, double click **MainPage.xaml** to open it in the design view.</span></span>
2. <span data-ttu-id="22f86-167">Zlokalizuj  **&lt;siatki&gt;**  i  **&lt;/Grid&gt;**  znaczniki pliku XAML i wklej następujący kod między tagami dwóch:</span><span class="sxs-lookup"><span data-stu-id="22f86-167">Locate the **&lt;Grid&gt;** and **&lt;/Grid&gt;**  tags the XAML file, and paste the following code between the two tags:</span></span>

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
   
   <span data-ttu-id="22f86-168">Formant MediaElement służy do odtwarzania multimediów.</span><span class="sxs-lookup"><span data-stu-id="22f86-168">The MediaElement control is used to playback media.</span></span> <span data-ttu-id="22f86-169">Kontrolka suwaka o nazwie sliderProgress będzie można użyć w następnej lekcji do kontrolowania postępu nośnika.</span><span class="sxs-lookup"><span data-stu-id="22f86-169">The slider control named sliderProgress will be used in the next lesson to control the media progress.</span></span>
3. <span data-ttu-id="22f86-170">Naciśnij klawisz **CTRL + S** można zapisać pliku.</span><span class="sxs-lookup"><span data-stu-id="22f86-170">Press **CTRL+S** to save the file.</span></span>

<span data-ttu-id="22f86-171">Formant MediaElement nie obsługuje funkcji Smooth Streaming zawartości out-of-box.</span><span class="sxs-lookup"><span data-stu-id="22f86-171">The MediaElement control does not support Smooth Streaming content out-of-box.</span></span> <span data-ttu-id="22f86-172">Aby włączyć obsługę Smooth Streaming, należy zarejestrować obsługi strumienia bajtów Smooth Streaming przez rozszerzenie nazwy pliku i typ MIME.</span><span class="sxs-lookup"><span data-stu-id="22f86-172">To enable the Smooth Streaming support, you must register the Smooth Streaming byte-stream handler by file name extension and MIME type.</span></span>  <span data-ttu-id="22f86-173">Aby zarejestrować, należy użyć metody MediaExtensionManager.RegisterByteStremHandler Windows.Media przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="22f86-173">To register, you use the MediaExtensionManager.RegisterByteStremHandler method of the Windows.Media namespace.</span></span>

<span data-ttu-id="22f86-174">W tym pliku XAML niektóre programy obsługi zdarzeń skojarzonych z formantami.</span><span class="sxs-lookup"><span data-stu-id="22f86-174">In this XAML file, some event handlers are associated with the controls.</span></span>  <span data-ttu-id="22f86-175">Należy zdefiniować te programy obsługi zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="22f86-175">You must define those event handlers.</span></span>

<span data-ttu-id="22f86-176">**Aby zmodyfikować kodzie pliku**</span><span class="sxs-lookup"><span data-stu-id="22f86-176">**To modify the code behind file**</span></span>

1. <span data-ttu-id="22f86-177">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy **MainPage.xaml**, a następnie kliknij przycisk **kod widoku**.</span><span class="sxs-lookup"><span data-stu-id="22f86-177">From Solution Explorer, right-click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="22f86-178">W górnej części pliku, dodaj następującą instrukcję using:</span><span class="sxs-lookup"><span data-stu-id="22f86-178">At the top of the file, add the following using statement:</span></span>
   
        using Windows.Media;
3. <span data-ttu-id="22f86-179">Na początku **MainPage** klasy, Dodaj następujący element członkowski danych:</span><span class="sxs-lookup"><span data-stu-id="22f86-179">At the beginning of the **MainPage** class, add the following data member:</span></span>
   
         private MediaExtensionManager extensions = new MediaExtensionManager();
4. <span data-ttu-id="22f86-180">Na koniec **MainPage** konstruktora, Dodaj następujące dwa wiersze:</span><span class="sxs-lookup"><span data-stu-id="22f86-180">At the end of the **MainPage** constructor, add the following two lines:</span></span>
   
        extensions.RegisterByteStreamHandler("Microsoft.Media.AdaptiveStreaming.SmoothByteStreamHandler", ".ism", "text/xml");
        extensions.RegisterByteStreamHandler("Microsoft.Media.AdaptiveStreaming.SmoothByteStreamHandler", ".ism", "application/vnd.ms-sstr+xml");
5. <span data-ttu-id="22f86-181">Na koniec **MainPage** klasy, wklej następujący kod:</span><span class="sxs-lookup"><span data-stu-id="22f86-181">At the end of the **MainPage** class, paste the following code:</span></span>
   
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
             txtStatus.Text = "Click the Play button to play the media source.";
         }
         }
         private void btnStop_Click(object sender, RoutedEventArgs e)
         {

         mediaElement.Stop();
         txtStatus.Text = "MediaElement is stopped";
         }
         private void sliderProgress_PointerPressed(object sender, PointerRoutedEventArgs e)
         {

         txtStatus.Text = "Seek to position " + sliderProgress.Value;
         mediaElement.Position = new TimeSpan(0, 0, (int)(sliderProgress.Value));
         }
         # endregion

<span data-ttu-id="22f86-182">Program obsługi zdarzeń sliderProgress_PointerPressed jest zdefiniowany w tym miejscu.</span><span class="sxs-lookup"><span data-stu-id="22f86-182">The sliderProgress_PointerPressed event handler is defined here.</span></span>  <span data-ttu-id="22f86-183">Istnieje więcej działa zrobić, aby przygotować go do pracy, które będą objęte w następnej lekcji tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="22f86-183">There are more works to do to get it working, which will be covered in the next lesson of this tutorial.</span></span>
6. <span data-ttu-id="22f86-184">Naciśnij klawisz **CTRL + S** można zapisać pliku.</span><span class="sxs-lookup"><span data-stu-id="22f86-184">Press **CTRL+S** to save the file.</span></span>

<span data-ttu-id="22f86-185">Zakończono kodzie pliku powinna wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="22f86-185">The finished the code behind file shall look like this:</span></span>

![Codeview w aplikacji Visual Studio programu Smooth Streaming Sklepu Windows][CodeViewPic]

<span data-ttu-id="22f86-187">**Aby skompilować i testowanie aplikacji**</span><span class="sxs-lookup"><span data-stu-id="22f86-187">**To compile and test the application**</span></span>

1. <span data-ttu-id="22f86-188">Z **kompilacji** menu, kliknij przycisk **programu Configuration Manager**.</span><span class="sxs-lookup"><span data-stu-id="22f86-188">From the **BUILD** menu, click **Configuration Manager**.</span></span>
2. <span data-ttu-id="22f86-189">Zmień **platformy aktywne rozwiązanie** odpowiadające rozwoju platformy.</span><span class="sxs-lookup"><span data-stu-id="22f86-189">Change **Active solution platform** to match your development platform.</span></span>
3. <span data-ttu-id="22f86-190">Naciśnij klawisz **F6** skompilować projekt.</span><span class="sxs-lookup"><span data-stu-id="22f86-190">Press **F6** to compile the project.</span></span> 
4. <span data-ttu-id="22f86-191">Naciśnij klawisz **F5**, aby uruchomić aplikację.</span><span class="sxs-lookup"><span data-stu-id="22f86-191">Press **F5** to run the application.</span></span>
5. <span data-ttu-id="22f86-192">W górnej części aplikacji możesz użyć domyślnej Smooth Streaming URL lub wprowadź inną.</span><span class="sxs-lookup"><span data-stu-id="22f86-192">At the top of the application, you can either use the default Smooth Streaming URL or enter a different one.</span></span> 
6. <span data-ttu-id="22f86-193">Kliknij przycisk **Ustaw źródło**.</span><span class="sxs-lookup"><span data-stu-id="22f86-193">Click **Set Source**.</span></span> <span data-ttu-id="22f86-194">Ponieważ **Auto-odtwarzanie** jest włączona domyślnie nośnika jest odtwarzany automatycznie.</span><span class="sxs-lookup"><span data-stu-id="22f86-194">Because **Auto Play** is enabled by default, the media shall play automatically.</span></span>  <span data-ttu-id="22f86-195">Można kontrolować przy użyciu nośnika **odtwarzanie**, **Wstrzymaj** i **zatrzymać** przycisków.</span><span class="sxs-lookup"><span data-stu-id="22f86-195">You can control the media using the **Play**, **Pause** and **Stop** buttons.</span></span>  <span data-ttu-id="22f86-196">Można kontrolować woluminu nośnika przy użyciu pionowej kontrolce slider.</span><span class="sxs-lookup"><span data-stu-id="22f86-196">You can control the media volume using the vertical slider.</span></span>  <span data-ttu-id="22f86-197">Jednak suwak poziomy kontroli postępu nośnika nie jest całkowicie jeszcze zaimplementowane.</span><span class="sxs-lookup"><span data-stu-id="22f86-197">However the horizontal slider for controlling the media progress is not fully implemented yet.</span></span> 

<span data-ttu-id="22f86-198">Lesson1 została ukończona.</span><span class="sxs-lookup"><span data-stu-id="22f86-198">You have completed lesson1.</span></span>  <span data-ttu-id="22f86-199">W tej lekcji służy do odtwarzania zawartości Smooth Streaming Formant MediaElement.</span><span class="sxs-lookup"><span data-stu-id="22f86-199">In this lesson, you use a MediaElement control to playback Smooth Streaming content.</span></span>  <span data-ttu-id="22f86-200">W następnej lekcji doda suwak do kontrolowania postęp Smooth Streaming zawartości.</span><span class="sxs-lookup"><span data-stu-id="22f86-200">In the next lesson, you will add a slider to control the progress of the Smooth Streaming content.</span></span>

## <a name="lesson-2-add-a-slider-bar-to-control-the-media-progress"></a><span data-ttu-id="22f86-201">Lekcja 2: Dodawanie paska suwaka do kontrolowania postępu nośnika</span><span class="sxs-lookup"><span data-stu-id="22f86-201">Lesson 2: Add a Slider Bar to Control the Media Progress</span></span>

<span data-ttu-id="22f86-202">W Lekcja 1 utworzono aplikację ze Sklepu Windows za pomocą formantu MediaElement XAML do odtwarzania zawartości multimedialnej Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="22f86-202">In lesson 1, you created a Windows Store application with a MediaElement XAML control to playback Smooth Streaming media content.</span></span>  <span data-ttu-id="22f86-203">Pochodzi niektórych funkcji podstawowych nośników, takich jak start, stop i wstrzymania.</span><span class="sxs-lookup"><span data-stu-id="22f86-203">It comes some basic media functions like start, stop and pause.</span></span>  <span data-ttu-id="22f86-204">W tej lekcji formantu paska suwaka doda do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="22f86-204">In this lesson, you will add a slider bar control to the application.</span></span>

<span data-ttu-id="22f86-205">W tym samouczku używamy czasomierz do zaktualizowania pozycji suwaka na podstawie bieżącego położenia kontrolki MediaElement.</span><span class="sxs-lookup"><span data-stu-id="22f86-205">In this tutorial, we will use a timer to update the slider position based on the current position of the MediaElement control.</span></span>  <span data-ttu-id="22f86-206">Suwak rozpoczęcia i zakończenia czasu również muszą zostać zaktualizowane w przypadku zawartości na żywo.</span><span class="sxs-lookup"><span data-stu-id="22f86-206">The slider start and end time also need to be updated in case of live content.</span></span>  <span data-ttu-id="22f86-207">Mogą być lepiej obsłużone w zdarzeniu adaptacyjną źródła aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="22f86-207">This can be better handled in the adaptive source update event.</span></span>

<span data-ttu-id="22f86-208">Źródeł multimediów to obiekty, które generować dane do nośnika.</span><span class="sxs-lookup"><span data-stu-id="22f86-208">Media sources are objects that generate media data.</span></span>  <span data-ttu-id="22f86-209">Źródło programu rozpoznawania nazw przyjmujący element stream adres URL lub bajt i tworzy odpowiedni nośnik źródła dla tej zawartości.</span><span class="sxs-lookup"><span data-stu-id="22f86-209">The source resolver takes a URL or byte stream and creates the appropriate media source for that content.</span></span>  <span data-ttu-id="22f86-210">Mechanizm rozpoznawania źródła jest standardowym sposobem dla aplikacji do tworzenia źródeł multimediów.</span><span class="sxs-lookup"><span data-stu-id="22f86-210">The source resolver is the standard way for the applications to create media sources.</span></span> 

<span data-ttu-id="22f86-211">W tej lekcji obejmuje następujące procedury:</span><span class="sxs-lookup"><span data-stu-id="22f86-211">This lesson contains the following procedures:</span></span>

1. <span data-ttu-id="22f86-212">Zarejestrować obsługi Smooth Streaming</span><span class="sxs-lookup"><span data-stu-id="22f86-212">Register the Smooth Streaming handler</span></span> 
2. <span data-ttu-id="22f86-213">Dodawanie obsługi zdarzeń na poziomie menedżera adaptacyjną źródła</span><span class="sxs-lookup"><span data-stu-id="22f86-213">Add the adaptive source manager level event handlers</span></span>
3. <span data-ttu-id="22f86-214">Dodawanie obsługi zdarzeń poziomu adaptacyjną źródła</span><span class="sxs-lookup"><span data-stu-id="22f86-214">Add the adaptive source level event handlers</span></span>
4. <span data-ttu-id="22f86-215">Dodaj element MediaElement procedury obsługi zdarzeń</span><span class="sxs-lookup"><span data-stu-id="22f86-215">Add MediaElement event handlers</span></span>
5. <span data-ttu-id="22f86-216">Dodaj suwaka kodu powiązanego</span><span class="sxs-lookup"><span data-stu-id="22f86-216">Add slider bar related code</span></span>
6. <span data-ttu-id="22f86-217">Kompilowanie i testowanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="22f86-217">Compile and test the application</span></span>

<span data-ttu-id="22f86-218">**Aby zarejestrować obsługi strumienia bajtów Smooth Streaming i przekaż propertyset**</span><span class="sxs-lookup"><span data-stu-id="22f86-218">**To register the Smooth Streaming byte-stream handler and pass the propertyset**</span></span>

1. <span data-ttu-id="22f86-219">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy **MainPage.xaml**, a następnie kliknij przycisk **kod widoku**.</span><span class="sxs-lookup"><span data-stu-id="22f86-219">From Solution Explorer, right click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="22f86-220">Na początku pliku, dodaj następującą instrukcję using:</span><span class="sxs-lookup"><span data-stu-id="22f86-220">At the beginning of the file, add the following using statement:</span></span>

        using Microsoft.Media.AdaptiveStreaming;
3. <span data-ttu-id="22f86-221">Na początku klasy MainPage, Dodaj następujące elementy członkowskie danych:</span><span class="sxs-lookup"><span data-stu-id="22f86-221">At the beginning of the MainPage class, add the following data members:</span></span>

         private Windows.Foundation.Collections.PropertySet propertySet = new Windows.Foundation.Collections.PropertySet();             
         private IAdaptiveSourceManager adaptiveSourceManager;
4. <span data-ttu-id="22f86-222">Wewnątrz **MainPage** konstruktora, Dodaj następujący kod po **to. Inicjowanie Components();**  wiersza i rejestracji kodu wierszach w poprzedniej lekcji:</span><span class="sxs-lookup"><span data-stu-id="22f86-222">Inside the **MainPage** constructor, add the following code after the **this.Initialize Components();** line and the registration code lines written in the previous lesson:</span></span>

        // Gets the default instance of AdaptiveSourceManager which manages Smooth 
        //Streaming media sources.
        adaptiveSourceManager = AdaptiveSourceManager.GetDefault();
        // Sets property key value to AdaptiveSourceManager default instance.
        // {A5CE1DE8-1D00-427B-ACEF-FB9A3C93DE2D}" must be hardcoded.
        propertySet["{A5CE1DE8-1D00-427B-ACEF-FB9A3C93DE2D}"] = adaptiveSourceManager;
5. <span data-ttu-id="22f86-223">Wewnątrz **MainPage** konstruktora, zmodyfikuj te dwie metody RegisterByteStreamHandler, aby dodać określonymi parametrami:</span><span class="sxs-lookup"><span data-stu-id="22f86-223">Inside the **MainPage** constructor, modify the two RegisterByteStreamHandler methods to add the forth parameters:</span></span>

         // Registers Smooth Streaming byte-stream handler for ".ism" extension and, 
         // "text/xml" and "application/vnd.ms-ss" mime-types and pass the propertyset. 
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
6. <span data-ttu-id="22f86-224">Naciśnij klawisz **CTRL + S** można zapisać pliku.</span><span class="sxs-lookup"><span data-stu-id="22f86-224">Press **CTRL+S** to save the file.</span></span>

<span data-ttu-id="22f86-225">**Aby dodać obsługi zdarzeń na poziomie menedżera adaptacyjną źródła**</span><span class="sxs-lookup"><span data-stu-id="22f86-225">**To add the adaptive source manager level event handler**</span></span>

1. <span data-ttu-id="22f86-226">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy **MainPage.xaml**, a następnie kliknij przycisk **kod widoku**.</span><span class="sxs-lookup"><span data-stu-id="22f86-226">From Solution Explorer, right click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="22f86-227">Wewnątrz **MainPage** klasy, Dodaj następujący element członkowski danych:</span><span class="sxs-lookup"><span data-stu-id="22f86-227">Inside the **MainPage** class, add the following data member:</span></span>
   
     <span data-ttu-id="22f86-228">prywatne adaptiveSource AdaptiveSource = null;</span><span class="sxs-lookup"><span data-stu-id="22f86-228">private AdaptiveSource adaptiveSource = null;</span></span>
3. <span data-ttu-id="22f86-229">Na koniec **MainPage** klasy, Dodaj następujący program obsługi zdarzeń:</span><span class="sxs-lookup"><span data-stu-id="22f86-229">At the end of the **MainPage** class, add the following event handler:</span></span>
   
         # region Adaptive Source Manager Level Events
         private void mediaElement_AdaptiveSourceOpened(AdaptiveSource sender, AdaptiveSourceOpenedEventArgs args)
         {

            adaptiveSource = args.AdaptiveSource;
         }

         # endregion Adaptive Source Manager Level Events
4. <span data-ttu-id="22f86-230">Na koniec **MainPage** konstruktora, Dodaj następujący wiersz, aby subskrybować zdarzenia otwarte adaptacyjną źródłowego:</span><span class="sxs-lookup"><span data-stu-id="22f86-230">At the end of the **MainPage** constructor, add the following line to subscribe to the adaptive source open event:</span></span>
   
         adaptiveSourceManager.AdaptiveSourceOpenedEvent += 
           new AdaptiveSourceOpenedEventHandler(mediaElement_AdaptiveSourceOpened);
5. <span data-ttu-id="22f86-231">Naciśnij klawisz **CTRL + S** można zapisać pliku.</span><span class="sxs-lookup"><span data-stu-id="22f86-231">Press **CTRL+S** to save the file.</span></span>

<span data-ttu-id="22f86-232">**Aby dodać obsługę zdarzeń poziomu adaptacyjną źródła**</span><span class="sxs-lookup"><span data-stu-id="22f86-232">**To add adaptive source level event handlers**</span></span>

1. <span data-ttu-id="22f86-233">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy **MainPage.xaml**, a następnie kliknij przycisk **kod widoku**.</span><span class="sxs-lookup"><span data-stu-id="22f86-233">From Solution Explorer, right click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="22f86-234">Wewnątrz **MainPage** klasy, Dodaj następujący element członkowski danych:</span><span class="sxs-lookup"><span data-stu-id="22f86-234">Inside the **MainPage** class, add the following data member:</span></span>
   
     <span data-ttu-id="22f86-235">prywatne adaptiveSourceStatusUpdate AdaptiveSourceStatusUpdatedEventArgs;   prywatne manifestObject manifestu;</span><span class="sxs-lookup"><span data-stu-id="22f86-235">private AdaptiveSourceStatusUpdatedEventArgs adaptiveSourceStatusUpdate;   private Manifest manifestObject;</span></span>
3. <span data-ttu-id="22f86-236">Na koniec **MainPage** klasy, Dodaj następujące programy obsługi zdarzeń:</span><span class="sxs-lookup"><span data-stu-id="22f86-236">At the end of the **MainPage** class, add the following event handlers:</span></span>

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
4. <span data-ttu-id="22f86-237">Na koniec **mediaElement AdaptiveSourceOpened** metody, Dodaj następujący kod, aby subskrybować zdarzenia:</span><span class="sxs-lookup"><span data-stu-id="22f86-237">At the end of the **mediaElement AdaptiveSourceOpened** method, add the following code to subscribe to the events:</span></span>
   
         adaptiveSource.ManifestReadyEvent +=

                    mediaElement_ManifestReady;
         adaptiveSource.AdaptiveSourceStatusUpdatedEvent += 

            mediaElement_AdaptiveSourceStatusUpdated;
         adaptiveSource.AdaptiveSourceFailedEvent += 

            mediaElement_AdaptiveSourceFailed;
5. <span data-ttu-id="22f86-238">Naciśnij klawisz **CTRL + S** można zapisać pliku.</span><span class="sxs-lookup"><span data-stu-id="22f86-238">Press **CTRL+S** to save the file.</span></span>

<span data-ttu-id="22f86-239">Tego samego zdarzenia są dostępne na adaptacyjną Menedżer poziom źródła również, która może służyć do obsługi funkcji wspólne dla wszystkich elementów nośnika w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="22f86-239">The same events are available on Adaptive Source manger level as well, which can be used for handling functionality common to all media elements in the app.</span></span> <span data-ttu-id="22f86-240">Każdy AdaptiveSource zawiera własnych zdarzeń i wszystkie zdarzenia AdaptiveSource będzie kaskadowych w obszarze AdaptiveSourceManager.</span><span class="sxs-lookup"><span data-stu-id="22f86-240">Each AdaptiveSource includes its own events and all AdaptiveSource events will be cascaded under AdaptiveSourceManager.</span></span>

<span data-ttu-id="22f86-241">**Aby dodać obsługę zdarzeń Element multimediów**</span><span class="sxs-lookup"><span data-stu-id="22f86-241">**To add Media Element event handlers**</span></span>

1. <span data-ttu-id="22f86-242">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy **MainPage.xaml**, a następnie kliknij przycisk **kod widoku**.</span><span class="sxs-lookup"><span data-stu-id="22f86-242">From Solution Explorer, right click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="22f86-243">Na koniec **MainPage** klasy, Dodaj następujące programy obsługi zdarzeń:</span><span class="sxs-lookup"><span data-stu-id="22f86-243">At the end of the **MainPage** class, add the following event handlers:</span></span>

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
3. <span data-ttu-id="22f86-244">Na koniec **MainPage** konstruktora, Dodaj następujący kod do indeks dolny do zdarzeń:</span><span class="sxs-lookup"><span data-stu-id="22f86-244">At the end of the **MainPage** constructor, add the following code to subscript to the events:</span></span>

         mediaElement.MediaOpened += MediaOpened;
         mediaElement.MediaEnded += MediaEnded;
         mediaElement.MediaFailed += MediaFailed;
4. <span data-ttu-id="22f86-245">Naciśnij klawisz **CTRL + S** można zapisać pliku.</span><span class="sxs-lookup"><span data-stu-id="22f86-245">Press **CTRL+S** to save the file.</span></span>

<span data-ttu-id="22f86-246">**Aby dodać paska suwaka związane z kodu**</span><span class="sxs-lookup"><span data-stu-id="22f86-246">**To add slider bar related code**</span></span>

1. <span data-ttu-id="22f86-247">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy **MainPage.xaml**, a następnie kliknij przycisk **kod widoku**.</span><span class="sxs-lookup"><span data-stu-id="22f86-247">From Solution Explorer, right click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="22f86-248">Na początku pliku, dodaj następującą instrukcję using:</span><span class="sxs-lookup"><span data-stu-id="22f86-248">At the beginning of the file, add the following using statement:</span></span>
      
        using Windows.UI.Core;
3. <span data-ttu-id="22f86-249">Wewnątrz **MainPage** klasy, Dodaj następujące elementy członkowskie danych:</span><span class="sxs-lookup"><span data-stu-id="22f86-249">Inside the **MainPage** class, add the following data members:</span></span>
   
         public static CoreDispatcher _dispatcher;
         private DispatcherTimer sliderPositionUpdateDispatcher;
4. <span data-ttu-id="22f86-250">Na koniec **MainPage** konstruktora, Dodaj następujący kod:</span><span class="sxs-lookup"><span data-stu-id="22f86-250">At the end of the **MainPage** constructor, add the following code:</span></span>
   
         _dispatcher = Window.Current.Dispatcher;
         PointerEventHandler pointerpressedhandler = new PointerEventHandler(sliderProgress_PointerPressed);
         sliderProgress.AddHandler(Control.PointerPressedEvent, pointerpressedhandler, true);    
5. <span data-ttu-id="22f86-251">Na koniec **MainPage** klasy, Dodaj następujący kod:</span><span class="sxs-lookup"><span data-stu-id="22f86-251">At the end of the **MainPage** class, add the following code:</span></span>

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
><span data-ttu-id="22f86-252">CoreDispatcher jest używany do wprowadzania zmian w wątku interfejsu użytkownika z wątku interfejsu użytkownika innych niż.</span><span class="sxs-lookup"><span data-stu-id="22f86-252">CoreDispatcher is used to make changes to the UI thread from non UI Thread.</span></span> <span data-ttu-id="22f86-253">W przypadku "wąskie gardło" na Wątek dyspozytora developer mogą być używane dyspozytora dostarczonych przez jego zamierza zaktualizować elementu interfejsu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="22f86-253">In case of bottleneck on dispatcher thread, developer can choose to use dispatcher provided by UI-element he/she intends to update.</span></span>  <span data-ttu-id="22f86-254">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="22f86-254">For example:</span></span>
   
         await sliderProgress.Dispatcher.RunAsync(CoreDispatcherPriority.Normal, () => { TimeSpan 

         timespan = new TimeSpan(adaptiveSourceStatusUpdate.EndTime); 
         double absvalue  = (int)Math.Round(timespan.TotalSeconds, MidpointRounding.AwayFromZero); 

         sliderProgress.Maximum = absvalue; }); 
6. <span data-ttu-id="22f86-255">Na koniec **mediaElement_AdaptiveSourceStatusUpdated** metody, Dodaj następujący kod:</span><span class="sxs-lookup"><span data-stu-id="22f86-255">At the end of the **mediaElement_AdaptiveSourceStatusUpdated** method, add the following code:</span></span>

         setSliderStartTime(args.StartTime);
         setSliderEndTime(args.EndTime);
7. <span data-ttu-id="22f86-256">Na koniec **MediaOpened** metody, Dodaj następujący kod:</span><span class="sxs-lookup"><span data-stu-id="22f86-256">At the end of the **MediaOpened** method, add the following code:</span></span>

         sliderProgress.StepFrequency = SliderFrequency(mediaElement.NaturalDuration.TimeSpan);
         sliderProgress.Width = mediaElement.Width;
         setupTimer();
8. <span data-ttu-id="22f86-257">Naciśnij klawisz **CTRL + S** można zapisać pliku.</span><span class="sxs-lookup"><span data-stu-id="22f86-257">Press **CTRL+S** to save the file.</span></span>

<span data-ttu-id="22f86-258">**Aby skompilować i testowanie aplikacji**</span><span class="sxs-lookup"><span data-stu-id="22f86-258">**To compile and test the application**</span></span>

1. <span data-ttu-id="22f86-259">Naciśnij klawisz **F6** skompilować projekt.</span><span class="sxs-lookup"><span data-stu-id="22f86-259">Press **F6** to compile the project.</span></span> 
2. <span data-ttu-id="22f86-260">Naciśnij klawisz **F5**, aby uruchomić aplikację.</span><span class="sxs-lookup"><span data-stu-id="22f86-260">Press **F5** to run the application.</span></span>
3. <span data-ttu-id="22f86-261">W górnej części aplikacji możesz użyć domyślnej Smooth Streaming URL lub wprowadź inną.</span><span class="sxs-lookup"><span data-stu-id="22f86-261">At the top of the application, you can either use the default Smooth Streaming URL or enter a different one.</span></span> 
4. <span data-ttu-id="22f86-262">Kliknij przycisk **Ustaw źródło**.</span><span class="sxs-lookup"><span data-stu-id="22f86-262">Click **Set Source**.</span></span> 
5. <span data-ttu-id="22f86-263">Przetestuj paska suwaka.</span><span class="sxs-lookup"><span data-stu-id="22f86-263">Test the slider bar.</span></span>

<span data-ttu-id="22f86-264">Lekcja 2 została ukończona.</span><span class="sxs-lookup"><span data-stu-id="22f86-264">You have completed lesson 2.</span></span>  <span data-ttu-id="22f86-265">W tej lekcji suwaka jest dodanych do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="22f86-265">In this lesson you added a slider to application.</span></span> 

## <a name="lesson-3-select-smooth-streaming-streams"></a><span data-ttu-id="22f86-266">Lekcja 3: Wybierz Smooth Streaming strumieni</span><span class="sxs-lookup"><span data-stu-id="22f86-266">Lesson 3: Select Smooth Streaming Streams</span></span>
<span data-ttu-id="22f86-267">Smooth Streaming jest w stanie do strumieniowego przesyłania zawartości z wielu ścieżek audio języka, które można wybrać przez przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="22f86-267">Smooth Streaming is capable to stream content with multiple language audio tracks that are selectable by the viewers.</span></span>  <span data-ttu-id="22f86-268">W tej lekcji spowoduje włączenie przeglądarki wybrać strumieni.</span><span class="sxs-lookup"><span data-stu-id="22f86-268">In this lesson, you will enable viewers to select streams.</span></span> <span data-ttu-id="22f86-269">W tej lekcji obejmuje następujące procedury:</span><span class="sxs-lookup"><span data-stu-id="22f86-269">This lesson contains the following procedures:</span></span>

1. <span data-ttu-id="22f86-270">Zmodyfikuj plik XAML</span><span class="sxs-lookup"><span data-stu-id="22f86-270">Modify the XAML file</span></span>
2. <span data-ttu-id="22f86-271">Modyfikowanie pliku behand kodu</span><span class="sxs-lookup"><span data-stu-id="22f86-271">Modify the code behand file</span></span>
3. <span data-ttu-id="22f86-272">Kompilowanie i testowanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="22f86-272">Compile and test the application</span></span>

<span data-ttu-id="22f86-273">**Aby zmodyfikować plik XAML**</span><span class="sxs-lookup"><span data-stu-id="22f86-273">**To modify the XAML file**</span></span>

1. <span data-ttu-id="22f86-274">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy **MainPage.xaml**, a następnie kliknij przycisk **Widok projektanta**.</span><span class="sxs-lookup"><span data-stu-id="22f86-274">From Solution Explorer, right-click **MainPage.xaml**, and then click **View Designer**.</span></span>
2. <span data-ttu-id="22f86-275">Zlokalizuj &lt;Grid.RowDefinitions&gt;i zmodyfikować RowDefinitions, aby ich wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="22f86-275">Locate &lt;Grid.RowDefinitions&gt;, and modify the RowDefinitions so they looks like:</span></span>
   
         <Grid.RowDefinitions>            
            <RowDefinition Height="20"/>
            <RowDefinition Height="50"/>
            <RowDefinition Height="100"/>
            <RowDefinition Height="80"/>
            <RowDefinition Height="50"/>
         </Grid.RowDefinitions>
3. <span data-ttu-id="22f86-276">Wewnątrz &lt;siatki&gt;&lt;/Grid&gt; tagów, Dodaj następujący kod do zdefiniowania kontrolki listbox, dlatego użytkownicy mogą zobaczyć listę dostępnych strumieni i wybierz strumieni:</span><span class="sxs-lookup"><span data-stu-id="22f86-276">Inside the &lt;Grid&gt;&lt;/Grid&gt; tags, add the following code to define a listbox control, so users can see the list of available streams, and select streams:</span></span>

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
4. <span data-ttu-id="22f86-277">Naciśnij klawisz **CTRL + S** Aby zapisać zmiany.</span><span class="sxs-lookup"><span data-stu-id="22f86-277">Press **CTRL+S** to save the changes.</span></span>

<span data-ttu-id="22f86-278">**Aby zmodyfikować kodzie pliku**</span><span class="sxs-lookup"><span data-stu-id="22f86-278">**To modify the code behind file**</span></span>

1. <span data-ttu-id="22f86-279">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy **MainPage.xaml**, a następnie kliknij przycisk **kod widoku**.</span><span class="sxs-lookup"><span data-stu-id="22f86-279">From Solution Explorer, right-click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="22f86-280">W obszarze nazw SSPlayer Dodaj nową klasę:</span><span class="sxs-lookup"><span data-stu-id="22f86-280">Inside the SSPlayer namespace, add a new class:</span></span>
   
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
                    // mMke the video stream always checked.
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
3. <span data-ttu-id="22f86-281">Na początku klasy MainPage, Dodaj następujące definicje zmiennych:</span><span class="sxs-lookup"><span data-stu-id="22f86-281">At the beginning of the MainPage class, add the following variable definitions:</span></span>
   
         private List<Stream> availableStreams;
         private List<Stream> availableAudioStreams;
         private List<Stream> availableTextStreams;
         private List<Stream> availableVideoStreams;
4. <span data-ttu-id="22f86-282">Wewnątrz klasy MainPage Dodaj następujący region:</span><span class="sxs-lookup"><span data-stu-id="22f86-282">Inside the MainPage class, add the following region:</span></span>
   
        #region stream selection
        ///<summary>
        ///Functionality to select streams from IManifestStream available streams
        /// </summary>
   
        // This function is called from the mediaElement_ManifestReady event handler 
        // to retrieve the streams and populate them to the local data members.
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
   
                    //populate the stream lists based on the types
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
   
                    // Select the default selected streams from the manifest.
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
   
        // This function set the list box ItemSource
        private async void refreshAvailableStreamsListBoxItemSource()
        {
            try
            {
                //update the stream check box list on the UI
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
   
            // Select the frist video stream from the list if no video stream is selected
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
                    txtStatus.Text = "The audio stream is changed to " + availableAudioStreams[j].ManifestStream.Name;
                }
            }
   
            // Select the frist audio stream from the list if no audio steam is selected.
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
5. <span data-ttu-id="22f86-283">Zlokalizuj metody mediaElement_ManifestReady, Dołącz następujący kod na końcu funkcji:</span><span class="sxs-lookup"><span data-stu-id="22f86-283">Locate the mediaElement_ManifestReady method, append the following code at the end of the function:</span></span>
   
        getStreams(manifestObject);
        refreshAvailableStreamsListBoxItemSource();
   
    <span data-ttu-id="22f86-284">Element MediaElement manifestu jest gotowy, kod pobiera listę dostępnych strumieni i wypełnia pole listy interfejsu użytkownika z listy.</span><span class="sxs-lookup"><span data-stu-id="22f86-284">So when MediaElement manifest is ready, the code gets a list of the available streams, and populates the UI list box with the list.</span></span>
6. <span data-ttu-id="22f86-285">Wewnątrz klasy MainPage zlokalizować interfejsu użytkownika przycisków kliknij region zdarzenia, a następnie dodaj następującą definicję funkcji:</span><span class="sxs-lookup"><span data-stu-id="22f86-285">Inside the MainPage class, locate the UI buttons click events region, and then add the following function definition:</span></span>
   
        private void btnChangeStream_Click(object sender, RoutedEventArgs e)
        {
            List<IManifestStream> selectedStreams = new List<IManifestStream>();
   
            // Create a list of the selected streams
            createSelectedStreamsList(selectedStreams);
   
            // Change streams on the presentation
            changeStreams(selectedStreams);
        }

<span data-ttu-id="22f86-286">**Aby skompilować i testowanie aplikacji**</span><span class="sxs-lookup"><span data-stu-id="22f86-286">**To compile and test the application**</span></span>

1. <span data-ttu-id="22f86-287">Naciśnij klawisz **F6** skompilować projekt.</span><span class="sxs-lookup"><span data-stu-id="22f86-287">Press **F6** to compile the project.</span></span> 
2. <span data-ttu-id="22f86-288">Naciśnij klawisz **F5**, aby uruchomić aplikację.</span><span class="sxs-lookup"><span data-stu-id="22f86-288">Press **F5** to run the application.</span></span>
3. <span data-ttu-id="22f86-289">W górnej części aplikacji możesz użyć domyślnej Smooth Streaming URL lub wprowadź inną.</span><span class="sxs-lookup"><span data-stu-id="22f86-289">At the top of the application, you can either use the default Smooth Streaming URL or enter a different one.</span></span> 
4. <span data-ttu-id="22f86-290">Kliknij przycisk **Ustaw źródło**.</span><span class="sxs-lookup"><span data-stu-id="22f86-290">Click **Set Source**.</span></span> 
5. <span data-ttu-id="22f86-291">Język domyślny jest audio_eng.</span><span class="sxs-lookup"><span data-stu-id="22f86-291">The default language is audio_eng.</span></span> <span data-ttu-id="22f86-292">Spróbuj przełączać się między audio_eng i audio_es.</span><span class="sxs-lookup"><span data-stu-id="22f86-292">Try to switch between audio_eng and audio_es.</span></span> <span data-ttu-id="22f86-293">Zawsze, gdy, wybierz nowego strumienia, należy kliknąć przycisk przesyłania.</span><span class="sxs-lookup"><span data-stu-id="22f86-293">Everytime, you select a new stream, you must click the Submit button.</span></span>

<span data-ttu-id="22f86-294">Ukończono Lekcja 3.</span><span class="sxs-lookup"><span data-stu-id="22f86-294">You have completed lesson 3.</span></span>  <span data-ttu-id="22f86-295">W tej lekcji możesz dodać funkcje wybrać strumieni.</span><span class="sxs-lookup"><span data-stu-id="22f86-295">In this lesson, you add the functionality to choose streams.</span></span>

## <a name="lesson-4-select-smooth-streaming-tracks"></a><span data-ttu-id="22f86-296">Lekcja 4: Wybierz Smooth Streaming ścieżki</span><span class="sxs-lookup"><span data-stu-id="22f86-296">Lesson 4: Select Smooth Streaming Tracks</span></span>
<span data-ttu-id="22f86-297">Prezentacja Smooth Streaming może zawierać wiele plików wideo zakodowane za pomocą różne poziomy jakości (szybkości transmisji bitów) i rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="22f86-297">A Smooth Streaming presentation can contain multiple video files encoded with different quality levels (bit rates) and resolutions.</span></span> <span data-ttu-id="22f86-298">W tej lekcji umożliwi użytkownikom na wybór ścieżki.</span><span class="sxs-lookup"><span data-stu-id="22f86-298">In this lesson, you will enable users to select tracks.</span></span> <span data-ttu-id="22f86-299">W tej lekcji obejmuje następujące procedury:</span><span class="sxs-lookup"><span data-stu-id="22f86-299">This lesson contains the following procedures:</span></span>

1. <span data-ttu-id="22f86-300">Zmodyfikuj plik XAML</span><span class="sxs-lookup"><span data-stu-id="22f86-300">Modify the XAML file</span></span>
2. <span data-ttu-id="22f86-301">Modyfikowanie pliku behand kodu</span><span class="sxs-lookup"><span data-stu-id="22f86-301">Modify the code behand file</span></span>
3. <span data-ttu-id="22f86-302">Kompilowanie i testowanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="22f86-302">Compile and test the application</span></span>

<span data-ttu-id="22f86-303">**Aby zmodyfikować plik XAML**</span><span class="sxs-lookup"><span data-stu-id="22f86-303">**To modify the XAML file**</span></span>

1. <span data-ttu-id="22f86-304">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy **MainPage.xaml**, a następnie kliknij przycisk **Widok projektanta**.</span><span class="sxs-lookup"><span data-stu-id="22f86-304">From Solution Explorer, right-click **MainPage.xaml**, and then click **View Designer**.</span></span>
2. <span data-ttu-id="22f86-305">Zlokalizuj &lt;siatki&gt; tag o nazwie **gridStreamAndBitrateSelection**, Dołącz następujący kod na końcu tagu:</span><span class="sxs-lookup"><span data-stu-id="22f86-305">Locate the &lt;Grid&gt; tag with the name **gridStreamAndBitrateSelection**, append the following code at the end of the tag:</span></span>
   
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
3. <span data-ttu-id="22f86-306">Naciśnij klawisz **CTRL + S** można zapisać zmian he</span><span class="sxs-lookup"><span data-stu-id="22f86-306">Press **CTRL+S** to save he changes</span></span>

<span data-ttu-id="22f86-307">**Aby zmodyfikować kodzie pliku**</span><span class="sxs-lookup"><span data-stu-id="22f86-307">**To modify the code behind file**</span></span>

1. <span data-ttu-id="22f86-308">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy **MainPage.xaml**, a następnie kliknij przycisk **kod widoku**.</span><span class="sxs-lookup"><span data-stu-id="22f86-308">From Solution Explorer, right-click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="22f86-309">W obszarze nazw SSPlayer Dodaj nową klasę:</span><span class="sxs-lookup"><span data-stu-id="22f86-309">Inside the SSPlayer namespace, add a new class:</span></span>
   
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
3. <span data-ttu-id="22f86-310">Na początku klasy MainPage, Dodaj następujące definicje zmiennych:</span><span class="sxs-lookup"><span data-stu-id="22f86-310">At the beginning of the MainPage class, add the following variable definitions:</span></span>
   
        private List<Track> availableTracks;
4. <span data-ttu-id="22f86-311">Wewnątrz klasy MainPage Dodaj następujący region:</span><span class="sxs-lookup"><span data-stu-id="22f86-311">Inside the MainPage class, add the following region:</span></span>
   
        #region track selection
        /// <summary>
        /// Functionality to select video streams
        /// </summary>
   
        /// This Function gets the tracks for the selected video stream
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
   
        // This function gets the video stream that is playing
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
   
        // This function set the UI list box control ItemSource
        private async void refreshAvailableTracksListBoxItemSource()
        {
            try
            {
                // Update the track check box list on the UI 
                await _dispatcher.RunAsync(CoreDispatcherPriority.Normal, ()
                    => { lbAvailableVideoTracks.ItemsSource = availableTracks; });
            }
            catch (Exception e)
            {
                txtStatus.Text = "Error: " + e.Message;
            }        
        }
   
        // This function creates a list of the selected tracks.
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
   
        // This function selects the tracks based on user selection 
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
5. <span data-ttu-id="22f86-312">Zlokalizuj metody mediaElement_ManifestReady, Dołącz następujący kod na końcu funkcji:</span><span class="sxs-lookup"><span data-stu-id="22f86-312">Locate the mediaElement_ManifestReady method, append the following code at the end of the function:</span></span>
   
         getTracks(manifestObject);
         refreshAvailableTracksListBoxItemSource();
6. <span data-ttu-id="22f86-313">Wewnątrz klasy MainPage zlokalizować interfejsu użytkownika przycisków kliknij region zdarzenia, a następnie dodaj następującą definicję funkcji:</span><span class="sxs-lookup"><span data-stu-id="22f86-313">Inside the MainPage class, locate the UI buttons click events region, and then add the following function definition:</span></span>
   
         private void btnChangeStream_Click(object sender, RoutedEventArgs e)
         {
            List<IManifestStream> selectedStreams = new List<IManifestStream>();

            // Create a list of the selected streams
            createSelectedStreamsList(selectedStreams);

            // Change streams on the presentation
            changeStreams(selectedStreams);
         }

<span data-ttu-id="22f86-314">**Aby skompilować i testowanie aplikacji**</span><span class="sxs-lookup"><span data-stu-id="22f86-314">**To compile and test the application**</span></span>

1. <span data-ttu-id="22f86-315">Naciśnij klawisz **F6** skompilować projekt.</span><span class="sxs-lookup"><span data-stu-id="22f86-315">Press **F6** to compile the project.</span></span> 
2. <span data-ttu-id="22f86-316">Naciśnij klawisz **F5**, aby uruchomić aplikację.</span><span class="sxs-lookup"><span data-stu-id="22f86-316">Press **F5** to run the application.</span></span>
3. <span data-ttu-id="22f86-317">W górnej części aplikacji możesz użyć domyślnej Smooth Streaming URL lub wprowadź inną.</span><span class="sxs-lookup"><span data-stu-id="22f86-317">At the top of the application, you can either use the default Smooth Streaming URL or enter a different one.</span></span> 
4. <span data-ttu-id="22f86-318">Kliknij przycisk **Ustaw źródło**.</span><span class="sxs-lookup"><span data-stu-id="22f86-318">Click **Set Source**.</span></span> 
5. <span data-ttu-id="22f86-319">Domyślnie wszystkie ścieżki strumienia wideo wybrane.</span><span class="sxs-lookup"><span data-stu-id="22f86-319">By default, all of the tracks of the video stream are selected.</span></span> <span data-ttu-id="22f86-320">Wypróbować zmiany szybkości bitowej, można wybrać najniższa szybkość transmisji bitów, dostępne, a następnie wybierz najwyższy szybkość transmisji bitów, dostępne.</span><span class="sxs-lookup"><span data-stu-id="22f86-320">To experiment the bit rate changes, you can select the lowest bit rate available, and then select the highest bit rate available.</span></span> <span data-ttu-id="22f86-321">Należy kliknąć przesyłania po każdej zmianie.</span><span class="sxs-lookup"><span data-stu-id="22f86-321">You must click Submit after each change.</span></span>  <span data-ttu-id="22f86-322">Zmiany jakości wideo jest widoczny.</span><span class="sxs-lookup"><span data-stu-id="22f86-322">You can see the video quality changes.</span></span>

<span data-ttu-id="22f86-323">Ukończono lekcji 4.</span><span class="sxs-lookup"><span data-stu-id="22f86-323">You have completed lesson 4.</span></span>  <span data-ttu-id="22f86-324">W tej lekcji możesz dodać funkcje, aby wybrać ścieżki.</span><span class="sxs-lookup"><span data-stu-id="22f86-324">In this lesson, you add the functionality to choose tracks.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="22f86-325">Ścieżki szkoleniowe dotyczące usługi Media Services</span><span class="sxs-lookup"><span data-stu-id="22f86-325">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="22f86-326">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="22f86-326">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="other-resources"></a><span data-ttu-id="22f86-327">Inne zasoby:</span><span class="sxs-lookup"><span data-stu-id="22f86-327">Other Resources:</span></span>
* [<span data-ttu-id="22f86-328">Jak utworzyć aplikację z zaawansowanych funkcji Smooth JavaScript 8 Windows przesyłania strumieniowego</span><span class="sxs-lookup"><span data-stu-id="22f86-328">How to build a Smooth Streaming Windows 8 JavaScript application with advanced features</span></span>](http://blogs.iis.net/cenkd/archive/2012/08/10/how-to-build-a-smooth-streaming-windows-8-javascript-application-with-advanced-features.aspx)
* [<span data-ttu-id="22f86-329">Płynnego przesyłania strumieniowego — omówienie</span><span class="sxs-lookup"><span data-stu-id="22f86-329">Smooth Streaming Technical Overview</span></span>](http://www.iis.net/learn/media/on-demand-smooth-streaming/smooth-streaming-technical-overview)

[PlayerApplication]: ./media/media-services-build-smooth-streaming-apps/SSClientWin8-1.png
[CodeViewPic]: ./media/media-services-build-smooth-streaming-apps/SSClientWin8-2.png

