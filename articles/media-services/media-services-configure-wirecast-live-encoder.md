---
title: "Skonfiguruj koder Telestream Wirecast wysłać strumień na żywo o pojedynczej szybkości transmisji bitów | Dokumentacja firmy Microsoft"
description: "W tym temacie przedstawiono sposób konfigurowania kodera na żywo Wirecast do wysłania do kanałów AMS, które są włączone dla kodowanie na żywo o pojedynczej szybkości transmisji. "
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 0d2f1e81-51a6-4ca9-894a-6dfa51ce4c70
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 01/05/2017
ms.author: juliako;cenkdin;anilmur
ms.openlocfilehash: c4df14f24650ce431dfb31cc774cab6d3cf3aef0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="use-the-wirecast-encoder-to-send-a-single-bitrate-live-stream"></a><span data-ttu-id="47e47-103">Użyj koder Wirecast, aby wysyłać strumień na żywo o pojedynczej szybkości transmisji bitów</span><span class="sxs-lookup"><span data-stu-id="47e47-103">Use the Wirecast encoder to send a single bitrate live stream</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="47e47-104">Wirecast</span><span class="sxs-lookup"><span data-stu-id="47e47-104">Wirecast</span></span>](media-services-configure-wirecast-live-encoder.md)
> * [<span data-ttu-id="47e47-105">Elemental na żywo</span><span class="sxs-lookup"><span data-stu-id="47e47-105">Elemental Live</span></span>](media-services-configure-elemental-live-encoder.md)
> * [<span data-ttu-id="47e47-106">Tricaster</span><span class="sxs-lookup"><span data-stu-id="47e47-106">Tricaster</span></span>](media-services-configure-tricaster-live-encoder.md)
> * [<span data-ttu-id="47e47-107">FMLE</span><span class="sxs-lookup"><span data-stu-id="47e47-107">FMLE</span></span>](media-services-configure-fmle-live-encoder.md)
>
>

<span data-ttu-id="47e47-108">W tym temacie przedstawiono sposób konfigurowania [Telestream Wirecast](http://www.telestream.net/wirecast/overview.htm) kodera na żywo do wysyłania strumienia pojedynczej szybkości transmisji bitów AMS kanałów, które są włączone kodowanie na żywo.</span><span class="sxs-lookup"><span data-stu-id="47e47-108">This topic shows how to configure the [Telestream Wirecast](http://www.telestream.net/wirecast/overview.htm) live encoder to send a single bitrate stream to AMS channels that are enabled for live encoding.</span></span>  <span data-ttu-id="47e47-109">Aby uzyskać więcej informacji, zobacz temat [Praca z kanałami obsługującymi funkcję Live Encoding w usłudze Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).</span><span class="sxs-lookup"><span data-stu-id="47e47-109">For more information, see [Working with Channels that are Enabled to Perform Live Encoding with Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).</span></span>

<span data-ttu-id="47e47-110">W tym samouczku przedstawiono sposób zarządzania usługi Azure Media Services (AMS) za pomocą narzędzia Azure Media Services Explorer (AMSE).</span><span class="sxs-lookup"><span data-stu-id="47e47-110">This tutorial shows how to manage Azure Media Services (AMS) with Azure Media Services Explorer (AMSE) tool.</span></span> <span data-ttu-id="47e47-111">To narzędzie jest uruchamiane tylko na komputerze z systemem Windows.</span><span class="sxs-lookup"><span data-stu-id="47e47-111">This tool only runs on Windows PC.</span></span> <span data-ttu-id="47e47-112">Jeśli na Mac lub Linux, użyj portalu Azure do utworzenia [kanałów](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) i [programy](media-services-portal-creating-live-encoder-enabled-channel.md).</span><span class="sxs-lookup"><span data-stu-id="47e47-112">If you are on Mac or Linux, use the Azure portal to create [channels](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) and [programs](media-services-portal-creating-live-encoder-enabled-channel.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="47e47-113">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="47e47-113">Prerequisites</span></span>
* [<span data-ttu-id="47e47-114">Tworzenie konta usługi Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="47e47-114">Create an Azure Media Services account</span></span>](media-services-portal-create-account.md)
* <span data-ttu-id="47e47-115">Upewnij się, brak punktu końcowego przesyłania strumieniowego uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="47e47-115">Ensure there is a Streaming Endpoint running.</span></span> <span data-ttu-id="47e47-116">Aby uzyskać więcej informacji, zobacz [zarządzanie punktami końcowymi przesyłania strumieniowego w konta usługi Media Services](media-services-portal-manage-streaming-endpoints.md)</span><span class="sxs-lookup"><span data-stu-id="47e47-116">For more information, see [Manage Streaming Endpoints in a Media Services Account](media-services-portal-manage-streaming-endpoints.md)</span></span>
* <span data-ttu-id="47e47-117">Zainstaluj najnowszą wersję pakietu [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) narzędzia.</span><span class="sxs-lookup"><span data-stu-id="47e47-117">Install the latest version of the [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) tool.</span></span>
* <span data-ttu-id="47e47-118">Uruchom narzędzie i połącz się z kontem AMS.</span><span class="sxs-lookup"><span data-stu-id="47e47-118">Launch the tool and connect to your AMS account.</span></span>

## <a name="tips"></a><span data-ttu-id="47e47-119">Porady</span><span class="sxs-lookup"><span data-stu-id="47e47-119">Tips</span></span>
* <span data-ttu-id="47e47-120">Jeśli to możliwe, użyj połączenia internetowego hardwired.</span><span class="sxs-lookup"><span data-stu-id="47e47-120">Whenever possible, use a hardwired internet connection.</span></span>
* <span data-ttu-id="47e47-121">Regułą podczas określania wymaganiach odnośnie do przepustowości jest dwukrotnie przesyłania strumieniowego szybkości transmisji bitów.</span><span class="sxs-lookup"><span data-stu-id="47e47-121">A good rule of thumb when determining bandwidth requirements is to double the streaming bitrates.</span></span> <span data-ttu-id="47e47-122">Chociaż nie jest to wymagane, może pomóc zmniejszyć skuteczność przeciążenie sieci.</span><span class="sxs-lookup"><span data-stu-id="47e47-122">While this is not a mandatory requirement, it will help mitigate the impact of network congestion.</span></span>
* <span data-ttu-id="47e47-123">Gdy za pomocą oprogramowania na podstawie koderów, zamknij wszystkie zbędne programy.</span><span class="sxs-lookup"><span data-stu-id="47e47-123">When using software based encoders, close out any unnecessary programs.</span></span>

## <a name="create-a-channel"></a><span data-ttu-id="47e47-124">Tworzenie kanału</span><span class="sxs-lookup"><span data-stu-id="47e47-124">Create a channel</span></span>
1. <span data-ttu-id="47e47-125">W przy użyciu narzędzia AMSE, przejdź do **Live** karcie, a następnie kliknij prawym przyciskiem myszy w obszarze kanału.</span><span class="sxs-lookup"><span data-stu-id="47e47-125">In the AMSE tool, navigate to the **Live** tab, and right click within the channel area.</span></span> <span data-ttu-id="47e47-126">Wybierz **Utwórz kanał...**</span><span class="sxs-lookup"><span data-stu-id="47e47-126">Select **Create channel…**</span></span> <span data-ttu-id="47e47-127">z menu.</span><span class="sxs-lookup"><span data-stu-id="47e47-127">from the menu.</span></span>

    ![wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast1.png)

2. <span data-ttu-id="47e47-129">Określ nazwę kanału pole opisu jest opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="47e47-129">Specify a channel name, the description field is optional.</span></span> <span data-ttu-id="47e47-130">W ustawieniach kanału, wybierz **standardowe** dla opcji Live Encoding z protokołem wprowadzania ustawioną **RTMP**.</span><span class="sxs-lookup"><span data-stu-id="47e47-130">Under Channel Settings, select **Standard** for the Live Encoding option, with the Input Protocol set to **RTMP**.</span></span> <span data-ttu-id="47e47-131">Możesz pozostawić wszystkie inne ustawienia, ponieważ jest.</span><span class="sxs-lookup"><span data-stu-id="47e47-131">You can leave all other settings as is.</span></span>

    <span data-ttu-id="47e47-132">Upewnij się, że **teraz uruchomić nowy kanał** jest zaznaczone.</span><span class="sxs-lookup"><span data-stu-id="47e47-132">Make sure the **Start the new channel now** is selected.</span></span>

3. <span data-ttu-id="47e47-133">Kliknij przycisk **utworzyć kanał**.</span><span class="sxs-lookup"><span data-stu-id="47e47-133">Click **Create Channel**.</span></span>

   ![wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast2.png)

> [!NOTE]
> <span data-ttu-id="47e47-135">Kanał może trwać tyle samo co 20 minut, aby rozpocząć.</span><span class="sxs-lookup"><span data-stu-id="47e47-135">The channel can take as long as 20 minutes to start.</span></span>
>
>

<span data-ttu-id="47e47-136">Podczas uruchamiania kanału możesz [skonfigurować koder](media-services-configure-wirecast-live-encoder.md#configure_wirecast_rtmp).</span><span class="sxs-lookup"><span data-stu-id="47e47-136">While the channel is starting you can [configure the encoder](media-services-configure-wirecast-live-encoder.md#configure_wirecast_rtmp).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="47e47-137">Należy pamiętać, że rozliczanie zaczyna się jak kanału przechodzi do stanu gotowości.</span><span class="sxs-lookup"><span data-stu-id="47e47-137">Note that billing starts as soon as Channel goes into a ready state.</span></span> <span data-ttu-id="47e47-138">Aby uzyskać więcej informacji, zobacz [stanów kanału](media-services-manage-live-encoder-enabled-channels.md#states).</span><span class="sxs-lookup"><span data-stu-id="47e47-138">For more information, see [Channel's states](media-services-manage-live-encoder-enabled-channels.md#states).</span></span>
>
>

## <span data-ttu-id="47e47-139"><a id=configure_wirecast_rtmp></a>Skonfiguruj koder Telestream Wirecast</span><span class="sxs-lookup"><span data-stu-id="47e47-139"><a id=configure_wirecast_rtmp></a>Configure the Telestream Wirecast encoder</span></span>
<span data-ttu-id="47e47-140">W tym samouczku są używane następujące ustawienia danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="47e47-140">In this tutorial the following output settings are used.</span></span> <span data-ttu-id="47e47-141">Pozostałej części tej sekcji opisano kroki konfiguracji szczegółowo.</span><span class="sxs-lookup"><span data-stu-id="47e47-141">The rest of this section describes configuration steps in more detail.</span></span>

<span data-ttu-id="47e47-142">**Wideo**:</span><span class="sxs-lookup"><span data-stu-id="47e47-142">**Video**:</span></span>

* <span data-ttu-id="47e47-143">Koder-dekoder: H.264</span><span class="sxs-lookup"><span data-stu-id="47e47-143">Codec: H.264</span></span>
* <span data-ttu-id="47e47-144">Profil: Wysoki (poziom 4.0)</span><span class="sxs-lookup"><span data-stu-id="47e47-144">Profile: High (Level 4.0)</span></span>
* <span data-ttu-id="47e47-145">Szybkość transmisji bitów: 5000 KB/s</span><span class="sxs-lookup"><span data-stu-id="47e47-145">Bitrate: 5000 kbps</span></span>
* <span data-ttu-id="47e47-146">Klatki kluczowej: 2 sekundy (60 sekund)</span><span class="sxs-lookup"><span data-stu-id="47e47-146">Keyframe: 2 seconds (60 seconds)</span></span>
* <span data-ttu-id="47e47-147">Szybkość klatek: 30</span><span class="sxs-lookup"><span data-stu-id="47e47-147">Frame Rate: 30</span></span>

<span data-ttu-id="47e47-148">**Audio**:</span><span class="sxs-lookup"><span data-stu-id="47e47-148">**Audio**:</span></span>

* <span data-ttu-id="47e47-149">Koder-dekoder: AAC (LC —)</span><span class="sxs-lookup"><span data-stu-id="47e47-149">Codec: AAC (LC)</span></span>
* <span data-ttu-id="47e47-150">Szybkość transmisji bitów: 192 kb/s</span><span class="sxs-lookup"><span data-stu-id="47e47-150">Bitrate: 192 kbps</span></span>
* <span data-ttu-id="47e47-151">Częstotliwość próbkowania: 44,1 kHz</span><span class="sxs-lookup"><span data-stu-id="47e47-151">Sample Rate: 44.1 kHz</span></span>

### <a name="configuration-steps"></a><span data-ttu-id="47e47-152">Kroki konfiguracji</span><span class="sxs-lookup"><span data-stu-id="47e47-152">Configuration steps</span></span>
1. <span data-ttu-id="47e47-153">Otwórz aplikację Telestream Wirecast z tego komputera, używane i skonfigurować do przesyłania strumieniowego RTMP.</span><span class="sxs-lookup"><span data-stu-id="47e47-153">Open the Telestream Wirecast application on the machine being used, and set up for RTMP streaming.</span></span>
2. <span data-ttu-id="47e47-154">Skonfiguruj dane wyjściowe, przechodząc do **dane wyjściowe** kartę i wybierając **ustawienia wyjściowej...** .</span><span class="sxs-lookup"><span data-stu-id="47e47-154">Configure the output by navigating to the **Output** tab and selecting **Output Settings…**.</span></span>

    <span data-ttu-id="47e47-155">Upewnij się, że **miejsce docelowe danych wyjściowych** ustawiono **serwera RTMP**.</span><span class="sxs-lookup"><span data-stu-id="47e47-155">Make sure the **Output Destination** is set to **RTMP Server**.</span></span>
3. <span data-ttu-id="47e47-156">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="47e47-156">Click **OK**.</span></span>
4. <span data-ttu-id="47e47-157">Na stronie Ustawienia ustawić **docelowego** ono być **usługi Azure Media Services**.</span><span class="sxs-lookup"><span data-stu-id="47e47-157">On the settings page, set the **Destination** field to be **Azure Media Services**.</span></span>

    <span data-ttu-id="47e47-158">Profil kodowanie jest wstępnie wybrane do **H.264 Azure 720 p 16:9 (1280 x 720)**.</span><span class="sxs-lookup"><span data-stu-id="47e47-158">The Encoding profile is pre-selected to **Azure H.264 720p 16:9 (1280x720)**.</span></span> <span data-ttu-id="47e47-159">Aby dostosować te ustawienia, wybierz ikonę Koło zębate po prawej stronie listy rozwijanej, a następnie wybierz **nowe ustawienie wstępne**.</span><span class="sxs-lookup"><span data-stu-id="47e47-159">To customize these settings, select the gear icon to the right of the drop down, and then choose **New Preset**.</span></span>

    ![wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast3.png)
5. <span data-ttu-id="47e47-161">Skonfiguruj ustawienia kodera.</span><span class="sxs-lookup"><span data-stu-id="47e47-161">Configure encoder presets.</span></span>

    <span data-ttu-id="47e47-162">Nazwę ustawienia i sprawdź, czy następujących zalecanych ustawień:</span><span class="sxs-lookup"><span data-stu-id="47e47-162">Name the preset, and check for the following recommended settings:</span></span>

    <span data-ttu-id="47e47-163">**Wideo**</span><span class="sxs-lookup"><span data-stu-id="47e47-163">**Video**</span></span>

   * <span data-ttu-id="47e47-164">Koder: MainConcept H.264</span><span class="sxs-lookup"><span data-stu-id="47e47-164">Encoder: MainConcept H.264</span></span>
   * <span data-ttu-id="47e47-165">Klatek na sekundę: 30</span><span class="sxs-lookup"><span data-stu-id="47e47-165">Frames per Second: 30</span></span>
   * <span data-ttu-id="47e47-166">Średnia szybkość transmisji bitów: 5000 kbitów na sekundę (może być określany na podstawie ograniczenia sieci)</span><span class="sxs-lookup"><span data-stu-id="47e47-166">Average bit rate: 5000 kbits/sec (Can be adjusted based on network limitations)</span></span>
   * <span data-ttu-id="47e47-167">Profil: Main</span><span class="sxs-lookup"><span data-stu-id="47e47-167">Profile: Main</span></span>
   * <span data-ttu-id="47e47-168">Klatki co: 60 klatek</span><span class="sxs-lookup"><span data-stu-id="47e47-168">Key frame every: 60 frames</span></span>

    <span data-ttu-id="47e47-169">**Audio**</span><span class="sxs-lookup"><span data-stu-id="47e47-169">**Audio**</span></span>

   * <span data-ttu-id="47e47-170">Docelowa szybkość transmisji bitów: 192 kbitów/s</span><span class="sxs-lookup"><span data-stu-id="47e47-170">Target bit rate: 192 kbits/sec</span></span>
   * <span data-ttu-id="47e47-171">Częstotliwość próbkowania: 44 100 kHz</span><span class="sxs-lookup"><span data-stu-id="47e47-171">Sample Rate: 44.100 kHz</span></span>

     ![wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast4.png)
6. <span data-ttu-id="47e47-173">Naciśnij klawisz **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="47e47-173">Press **Save**.</span></span>

    <span data-ttu-id="47e47-174">Pola Encoding ma teraz nowo utworzony profil dostępne do wyboru.</span><span class="sxs-lookup"><span data-stu-id="47e47-174">The Encoding field now has the newly created profile available for selection.</span></span>

    <span data-ttu-id="47e47-175">Upewnij się, że wybrano nowy profil.</span><span class="sxs-lookup"><span data-stu-id="47e47-175">Make sure the new profile is selected.</span></span>
7. <span data-ttu-id="47e47-176">Get kanału wejściowych adres URL, aby przypisać Wirecast **punktu końcowego protokołu RTMP**.</span><span class="sxs-lookup"><span data-stu-id="47e47-176">Get the channel's input URL in order to assign it to the Wirecast **RTMP Endpoint**.</span></span>

    <span data-ttu-id="47e47-177">Przejdź z powrotem do przy użyciu narzędzia AMSE i sprawdzić stan ukończenia kanału.</span><span class="sxs-lookup"><span data-stu-id="47e47-177">Navigate back to the AMSE tool, and check on the channel completion status.</span></span> <span data-ttu-id="47e47-178">Gdy stan został zmieniony z **uruchamianie** do **systemem**, można uzyskać wejściowy adres URL.</span><span class="sxs-lookup"><span data-stu-id="47e47-178">Once the State has changed from **Starting** to **Running**, you can get the input URL.</span></span>

    <span data-ttu-id="47e47-179">Gdy kanał jest uruchomiona, kliknij prawym przyciskiem myszy nazwę kanału, przejdź do aktywowania przez **kopia danych wejściowych z adresu URL do Schowka** , a następnie wybierz **podstawowego adresu URL danych wejściowych**.</span><span class="sxs-lookup"><span data-stu-id="47e47-179">When the channel is running, right click the channel name, navigate down to hover over **Copy Input URL to clipboard** and then select **Primary Input  URL**.</span></span>  

    ![wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast6.png)
8. <span data-ttu-id="47e47-181">W Wirecast **ustawienia wyjściowej** okna, Wklej te informacje w **adres** pole sekcji danych wyjściowych i przypisz nazwę strumienia.</span><span class="sxs-lookup"><span data-stu-id="47e47-181">In the Wirecast **Output Settings** window, paste this information in the **Address** field of the output section, and assign a stream name.</span></span>

    ![wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast5.png)

1. <span data-ttu-id="47e47-183">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="47e47-183">Select **OK**.</span></span>
2. <span data-ttu-id="47e47-184">W głównym **Wirecast** Sprawdź źródeł danych wejściowych dla audio i wideo są gotowe, a następnie naciśnij **strumienia** w lewego górnego rogu.</span><span class="sxs-lookup"><span data-stu-id="47e47-184">On the main **Wirecast** screen, confirm input sources for video and audio are ready and then hit **Stream** in the top left hand corner.</span></span>

   ![wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast7.png)

> [!IMPORTANT]
> <span data-ttu-id="47e47-186">Przed kliknięciem przycisku **strumienia**, możesz **musi** upewnij się, że kanał jest gotowy.</span><span class="sxs-lookup"><span data-stu-id="47e47-186">Before you click **Stream**, you **must** ensure that the Channel is ready.</span></span>
> <span data-ttu-id="47e47-187">Upewnij się również, nie należy pozostawiać kanału w stanie Gotowe bez wprowadzania wkład źródła danych przez czas dłuższy niż > 15 minut.</span><span class="sxs-lookup"><span data-stu-id="47e47-187">Also, make sure not to leave the Channel in a ready state without an input contribution feed for longer than > 15 minutes.</span></span>
>
>

## <a name="test-playback"></a><span data-ttu-id="47e47-188">Podczas odtwarzania testu</span><span class="sxs-lookup"><span data-stu-id="47e47-188">Test playback</span></span>

<span data-ttu-id="47e47-189">Przejdź do przy użyciu narzędzia AMSE, a następnie kliknij prawym przyciskiem myszy kanału, który ma zostać przetestowana.</span><span class="sxs-lookup"><span data-stu-id="47e47-189">Navigate to the AMSE tool, and right click the channel to be tested.</span></span> <span data-ttu-id="47e47-190">Z menu, umieść kursor nad **odtwarzania podglądu** i wybierz **z usługi Azure Media Player**.</span><span class="sxs-lookup"><span data-stu-id="47e47-190">From the menu, hover over **Playback the Preview** and select **with Azure Media Player**.</span></span>  

    ![wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast8.png)

<span data-ttu-id="47e47-191">Strumień jest widoczna w player, następnie koder został poprawnie skonfigurowany do nawiązania połączenia usługi AMS.</span><span class="sxs-lookup"><span data-stu-id="47e47-191">If the stream appears in the player, then the encoder has been properly configured to connect to AMS.</span></span>

<span data-ttu-id="47e47-192">Jeśli błąd kanału należy zresetować i dostosowane ustawienia kodera.</span><span class="sxs-lookup"><span data-stu-id="47e47-192">If an error is received, the channel will need to be reset and encoder settings adjusted.</span></span> <span data-ttu-id="47e47-193">Zobacz [Rozwiązywanie problemów z](media-services-troubleshooting-live-streaming.md) tematu, aby uzyskać wskazówki.</span><span class="sxs-lookup"><span data-stu-id="47e47-193">Please see the [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>  

## <a name="create-a-program"></a><span data-ttu-id="47e47-194">Utwórz program</span><span class="sxs-lookup"><span data-stu-id="47e47-194">Create a program</span></span>
1. <span data-ttu-id="47e47-195">Po potwierdzeniu kanału odtwarzania, tworzenia programu.</span><span class="sxs-lookup"><span data-stu-id="47e47-195">Once channel playback is confirmed, create a program.</span></span> <span data-ttu-id="47e47-196">W obszarze **Live** w przy użyciu narzędzia AMSE, kliknij prawym przyciskiem myszy w obszarze program i wybierz **utworzyć nowy Program**.</span><span class="sxs-lookup"><span data-stu-id="47e47-196">Under the **Live** tab in the AMSE tool, right click within the program area and select **Create New Program**.</span></span>  

    ![wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast9.png)
2. <span data-ttu-id="47e47-198">Nazwa programu, a w razie potrzeby dostosuj **długość okna archiwum** (który domyślnie 4 godziny).</span><span class="sxs-lookup"><span data-stu-id="47e47-198">Name the program and, if needed, adjust the **Archive Window Length** (which defaults to 4 hours).</span></span> <span data-ttu-id="47e47-199">Można także określić miejsce przechowywania lub pozostaw domyślnie.</span><span class="sxs-lookup"><span data-stu-id="47e47-199">You can also specify a storage location or leave as the default.</span></span>  
3. <span data-ttu-id="47e47-200">Sprawdź **teraz uruchomić Program** pole.</span><span class="sxs-lookup"><span data-stu-id="47e47-200">Check the **Start the Program now** box.</span></span>
4. <span data-ttu-id="47e47-201">Kliknij przycisk **utworzyć Program**.</span><span class="sxs-lookup"><span data-stu-id="47e47-201">Click **Create Program**.</span></span>  

   >[!NOTE]
   ><span data-ttu-id="47e47-202">Tworzenie programu zajmuje mniej czasu niż tworzenie kanału.</span><span class="sxs-lookup"><span data-stu-id="47e47-202">Program creation takes less time than channel creation.</span></span>
       
5. <span data-ttu-id="47e47-203">Po uruchomieniu programu potwierdzić odtwarzania przez kliknięcie prawym przyciskiem myszy program i przechodząc do **odtwarzania programach** , a następnie wybierając **z usługi Azure Media Player**.</span><span class="sxs-lookup"><span data-stu-id="47e47-203">Once the program is running, confirm playback by right clicking the program and navigating to **Playback the program(s)** and then selecting **with Azure Media Player**.</span></span>  
6. <span data-ttu-id="47e47-204">Po potwierdzeniu, kliknij prawym przyciskiem myszy program ponownie i wybierz **skopiuj dane wyjściowe adres URL do Schowka** (lub pobrać tych informacji z **programu informacji i ustawień** opcji z menu).</span><span class="sxs-lookup"><span data-stu-id="47e47-204">Once confirmed, right click the program again and select **Copy the Output URL to Clipboard** (or retrieve this information from the **Program information and settings** option from the menu).</span></span>

<span data-ttu-id="47e47-205">Strumień jest teraz gotowy do osadzonego w odtwarzacza lub dystrybuowane do odbiorców w celu wyświetlenia na żywo.</span><span class="sxs-lookup"><span data-stu-id="47e47-205">The stream is now ready to be embedded in a player, or distributed to an audience for live viewing.</span></span>  

## <a name="troubleshooting"></a><span data-ttu-id="47e47-206">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="47e47-206">Troubleshooting</span></span>
<span data-ttu-id="47e47-207">Zobacz [Rozwiązywanie problemów z](media-services-troubleshooting-live-streaming.md) tematu, aby uzyskać wskazówki.</span><span class="sxs-lookup"><span data-stu-id="47e47-207">Please see the [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="47e47-208">Ścieżki szkoleniowe dotyczące usługi Media Services</span><span class="sxs-lookup"><span data-stu-id="47e47-208">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="47e47-209">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="47e47-209">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
