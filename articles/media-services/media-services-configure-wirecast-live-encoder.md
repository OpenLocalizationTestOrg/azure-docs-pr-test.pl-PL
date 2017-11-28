---
title: "aaaConfigure hello toosend koder Telestream Wirecast strumień na żywo o pojedynczej szybkości transmisji bitów | Dokumentacja firmy Microsoft"
description: "W tym temacie przedstawiono sposób tooconfigure hello Wirecast live toosend kodera kanałami tooAMS strumienia pojedynczej szybkości transmisji bitów, obsługującymi kodowanie na żywo. "
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
ms.openlocfilehash: e373f6c08232c652e65db584ded409c405d8cffe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-wirecast-encoder-toosend-a-single-bitrate-live-stream"></a><span data-ttu-id="7beb8-103">Użyj hello Wirecast koder toosend strumień na żywo o pojedynczej szybkości transmisji bitów</span><span class="sxs-lookup"><span data-stu-id="7beb8-103">Use hello Wirecast encoder toosend a single bitrate live stream</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7beb8-104">Wirecast</span><span class="sxs-lookup"><span data-stu-id="7beb8-104">Wirecast</span></span>](media-services-configure-wirecast-live-encoder.md)
> * [<span data-ttu-id="7beb8-105">Elemental na żywo</span><span class="sxs-lookup"><span data-stu-id="7beb8-105">Elemental Live</span></span>](media-services-configure-elemental-live-encoder.md)
> * [<span data-ttu-id="7beb8-106">Tricaster</span><span class="sxs-lookup"><span data-stu-id="7beb8-106">Tricaster</span></span>](media-services-configure-tricaster-live-encoder.md)
> * [<span data-ttu-id="7beb8-107">FMLE</span><span class="sxs-lookup"><span data-stu-id="7beb8-107">FMLE</span></span>](media-services-configure-fmle-live-encoder.md)
>
>

<span data-ttu-id="7beb8-108">W tym temacie przedstawiono sposób tooconfigure hello [Telestream Wirecast](http://www.telestream.net/wirecast/overview.htm) kanałami tooAMS strumienia pojedynczej szybkości transmisji bitów, obsługującymi kodowanie na żywo toosend kodera na żywo.</span><span class="sxs-lookup"><span data-stu-id="7beb8-108">This topic shows how tooconfigure hello [Telestream Wirecast](http://www.telestream.net/wirecast/overview.htm) live encoder toosend a single bitrate stream tooAMS channels that are enabled for live encoding.</span></span>  <span data-ttu-id="7beb8-109">Aby uzyskać więcej informacji, zobacz [Praca z kanałami, że włączono tooPerform Live kodowania za pomocą usługi Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).</span><span class="sxs-lookup"><span data-stu-id="7beb8-109">For more information, see [Working with Channels that are Enabled tooPerform Live Encoding with Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).</span></span>

<span data-ttu-id="7beb8-110">Ten samouczek pokazuje, jak toomanage usługi Azure Media Services (AMS) za pomocą narzędzia Azure Media Services Explorer (AMSE).</span><span class="sxs-lookup"><span data-stu-id="7beb8-110">This tutorial shows how toomanage Azure Media Services (AMS) with Azure Media Services Explorer (AMSE) tool.</span></span> <span data-ttu-id="7beb8-111">To narzędzie jest uruchamiane tylko na komputerze z systemem Windows.</span><span class="sxs-lookup"><span data-stu-id="7beb8-111">This tool only runs on Windows PC.</span></span> <span data-ttu-id="7beb8-112">Mac lub Linux, za pomocą hello Azure portalu toocreate [kanałów](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) i [programy](media-services-portal-creating-live-encoder-enabled-channel.md).</span><span class="sxs-lookup"><span data-stu-id="7beb8-112">If you are on Mac or Linux, use hello Azure portal toocreate [channels](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) and [programs](media-services-portal-creating-live-encoder-enabled-channel.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7beb8-113">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="7beb8-113">Prerequisites</span></span>
* [<span data-ttu-id="7beb8-114">Tworzenie konta usługi Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="7beb8-114">Create an Azure Media Services account</span></span>](media-services-portal-create-account.md)
* <span data-ttu-id="7beb8-115">Upewnij się, brak punktu końcowego przesyłania strumieniowego uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="7beb8-115">Ensure there is a Streaming Endpoint running.</span></span> <span data-ttu-id="7beb8-116">Aby uzyskać więcej informacji, zobacz [zarządzanie punktami końcowymi przesyłania strumieniowego w konta usługi Media Services](media-services-portal-manage-streaming-endpoints.md)</span><span class="sxs-lookup"><span data-stu-id="7beb8-116">For more information, see [Manage Streaming Endpoints in a Media Services Account](media-services-portal-manage-streaming-endpoints.md)</span></span>
* <span data-ttu-id="7beb8-117">Zainstaluj najnowszą wersję hello hello [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) narzędzia.</span><span class="sxs-lookup"><span data-stu-id="7beb8-117">Install hello latest version of hello [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) tool.</span></span>
* <span data-ttu-id="7beb8-118">Uruchom narzędzie hello i Połącz konto tooyour AMS.</span><span class="sxs-lookup"><span data-stu-id="7beb8-118">Launch hello tool and connect tooyour AMS account.</span></span>

## <a name="tips"></a><span data-ttu-id="7beb8-119">Porady</span><span class="sxs-lookup"><span data-stu-id="7beb8-119">Tips</span></span>
* <span data-ttu-id="7beb8-120">Jeśli to możliwe, użyj połączenia internetowego hardwired.</span><span class="sxs-lookup"><span data-stu-id="7beb8-120">Whenever possible, use a hardwired internet connection.</span></span>
* <span data-ttu-id="7beb8-121">Regułą podczas określania wymaganiach odnośnie do przepustowości jest hello toodouble przesyłania strumieniowego szybkości transmisji bitów.</span><span class="sxs-lookup"><span data-stu-id="7beb8-121">A good rule of thumb when determining bandwidth requirements is toodouble hello streaming bitrates.</span></span> <span data-ttu-id="7beb8-122">Chociaż nie jest to wymagane, może pomóc zmniejszyć wpływ hello sieci przeciążona.</span><span class="sxs-lookup"><span data-stu-id="7beb8-122">While this is not a mandatory requirement, it will help mitigate hello impact of network congestion.</span></span>
* <span data-ttu-id="7beb8-123">Gdy za pomocą oprogramowania na podstawie koderów, zamknij wszystkie zbędne programy.</span><span class="sxs-lookup"><span data-stu-id="7beb8-123">When using software based encoders, close out any unnecessary programs.</span></span>

## <a name="create-a-channel"></a><span data-ttu-id="7beb8-124">Tworzenie kanału</span><span class="sxs-lookup"><span data-stu-id="7beb8-124">Create a channel</span></span>
1. <span data-ttu-id="7beb8-125">Narzędzie AMSE hello Przejdź toohello **Live** karcie, a następnie kliknij prawym przyciskiem myszy w obszarze kanału hello.</span><span class="sxs-lookup"><span data-stu-id="7beb8-125">In hello AMSE tool, navigate toohello **Live** tab, and right click within hello channel area.</span></span> <span data-ttu-id="7beb8-126">Wybierz **Utwórz kanał...**</span><span class="sxs-lookup"><span data-stu-id="7beb8-126">Select **Create channel…**</span></span> <span data-ttu-id="7beb8-127">z hello menu.</span><span class="sxs-lookup"><span data-stu-id="7beb8-127">from hello menu.</span></span>

    ![wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast1.png)

2. <span data-ttu-id="7beb8-129">Określ nazwę kanału hello pole opisu jest opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="7beb8-129">Specify a channel name, hello description field is optional.</span></span> <span data-ttu-id="7beb8-130">W ustawieniach kanału, wybierz **standardowe** dla hello opcji kodowanie na żywo z hello wprowadzania ustawiony protokół zbyt**RTMP**.</span><span class="sxs-lookup"><span data-stu-id="7beb8-130">Under Channel Settings, select **Standard** for hello Live Encoding option, with hello Input Protocol set too**RTMP**.</span></span> <span data-ttu-id="7beb8-131">Możesz pozostawić wszystkie inne ustawienia, ponieważ jest.</span><span class="sxs-lookup"><span data-stu-id="7beb8-131">You can leave all other settings as is.</span></span>

    <span data-ttu-id="7beb8-132">Upewnij się, że hello **Start hello nowy kanał teraz** jest zaznaczone.</span><span class="sxs-lookup"><span data-stu-id="7beb8-132">Make sure hello **Start hello new channel now** is selected.</span></span>

3. <span data-ttu-id="7beb8-133">Kliknij przycisk **utworzyć kanał**.</span><span class="sxs-lookup"><span data-stu-id="7beb8-133">Click **Create Channel**.</span></span>

   ![wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast2.png)

> [!NOTE]
> <span data-ttu-id="7beb8-135">kanał Hello może zająć toostart 20 minut.</span><span class="sxs-lookup"><span data-stu-id="7beb8-135">hello channel can take as long as 20 minutes toostart.</span></span>
>
>

<span data-ttu-id="7beb8-136">Podczas uruchamiania kanału hello można [skonfigurować koder hello](media-services-configure-wirecast-live-encoder.md#configure_wirecast_rtmp).</span><span class="sxs-lookup"><span data-stu-id="7beb8-136">While hello channel is starting you can [configure hello encoder](media-services-configure-wirecast-live-encoder.md#configure_wirecast_rtmp).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7beb8-137">Należy pamiętać, że rozliczanie zaczyna się jak kanału przechodzi do stanu gotowości.</span><span class="sxs-lookup"><span data-stu-id="7beb8-137">Note that billing starts as soon as Channel goes into a ready state.</span></span> <span data-ttu-id="7beb8-138">Aby uzyskać więcej informacji, zobacz [stanów kanału](media-services-manage-live-encoder-enabled-channels.md#states).</span><span class="sxs-lookup"><span data-stu-id="7beb8-138">For more information, see [Channel's states](media-services-manage-live-encoder-enabled-channels.md#states).</span></span>
>
>

## <span data-ttu-id="7beb8-139"><a id=configure_wirecast_rtmp></a>Skonfiguruj hello koder Telestream Wirecast</span><span class="sxs-lookup"><span data-stu-id="7beb8-139"><a id=configure_wirecast_rtmp></a>Configure hello Telestream Wirecast encoder</span></span>
<span data-ttu-id="7beb8-140">W tym samouczek hello są używane następujące ustawienia danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="7beb8-140">In this tutorial hello following output settings are used.</span></span> <span data-ttu-id="7beb8-141">Hello pozostałej części tej sekcji opisano kroki konfiguracji szczegółowo.</span><span class="sxs-lookup"><span data-stu-id="7beb8-141">hello rest of this section describes configuration steps in more detail.</span></span>

<span data-ttu-id="7beb8-142">**Wideo**:</span><span class="sxs-lookup"><span data-stu-id="7beb8-142">**Video**:</span></span>

* <span data-ttu-id="7beb8-143">Koder-dekoder: H.264</span><span class="sxs-lookup"><span data-stu-id="7beb8-143">Codec: H.264</span></span>
* <span data-ttu-id="7beb8-144">Profil: Wysoki (poziom 4.0)</span><span class="sxs-lookup"><span data-stu-id="7beb8-144">Profile: High (Level 4.0)</span></span>
* <span data-ttu-id="7beb8-145">Szybkość transmisji bitów: 5000 KB/s</span><span class="sxs-lookup"><span data-stu-id="7beb8-145">Bitrate: 5000 kbps</span></span>
* <span data-ttu-id="7beb8-146">Klatki kluczowej: 2 sekundy (60 sekund)</span><span class="sxs-lookup"><span data-stu-id="7beb8-146">Keyframe: 2 seconds (60 seconds)</span></span>
* <span data-ttu-id="7beb8-147">Szybkość klatek: 30</span><span class="sxs-lookup"><span data-stu-id="7beb8-147">Frame Rate: 30</span></span>

<span data-ttu-id="7beb8-148">**Audio**:</span><span class="sxs-lookup"><span data-stu-id="7beb8-148">**Audio**:</span></span>

* <span data-ttu-id="7beb8-149">Koder-dekoder: AAC (LC —)</span><span class="sxs-lookup"><span data-stu-id="7beb8-149">Codec: AAC (LC)</span></span>
* <span data-ttu-id="7beb8-150">Szybkość transmisji bitów: 192 kb/s</span><span class="sxs-lookup"><span data-stu-id="7beb8-150">Bitrate: 192 kbps</span></span>
* <span data-ttu-id="7beb8-151">Częstotliwość próbkowania: 44,1 kHz</span><span class="sxs-lookup"><span data-stu-id="7beb8-151">Sample Rate: 44.1 kHz</span></span>

### <a name="configuration-steps"></a><span data-ttu-id="7beb8-152">Kroki konfiguracji</span><span class="sxs-lookup"><span data-stu-id="7beb8-152">Configuration steps</span></span>
1. <span data-ttu-id="7beb8-153">Otwórz aplikację Telestream Wirecast hello na powitania maszyna nie jest używane i skonfigurować do przesyłania strumieniowego RTMP.</span><span class="sxs-lookup"><span data-stu-id="7beb8-153">Open hello Telestream Wirecast application on hello machine being used, and set up for RTMP streaming.</span></span>
2. <span data-ttu-id="7beb8-154">Konfigurowanie danych wyjściowych hello przechodząc toohello **dane wyjściowe** kartę i wybierając **ustawienia wyjściowej...** .</span><span class="sxs-lookup"><span data-stu-id="7beb8-154">Configure hello output by navigating toohello **Output** tab and selecting **Output Settings…**.</span></span>

    <span data-ttu-id="7beb8-155">Upewnij się, że hello **miejsce docelowe danych wyjściowych** ustawiono zbyt**serwera RTMP**.</span><span class="sxs-lookup"><span data-stu-id="7beb8-155">Make sure hello **Output Destination** is set too**RTMP Server**.</span></span>
3. <span data-ttu-id="7beb8-156">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="7beb8-156">Click **OK**.</span></span>
4. <span data-ttu-id="7beb8-157">Na stronie ustawień hello ustawić hello **docelowego** toobe pola **usługi Azure Media Services**.</span><span class="sxs-lookup"><span data-stu-id="7beb8-157">On hello settings page, set hello **Destination** field toobe **Azure Media Services**.</span></span>

    <span data-ttu-id="7beb8-158">Witaj profilu kodowanie jest wstępnie zaznaczona zbyt**H.264 Azure 720 p 16:9 (1280 x 720)**.</span><span class="sxs-lookup"><span data-stu-id="7beb8-158">hello Encoding profile is pre-selected too**Azure H.264 720p 16:9 (1280x720)**.</span></span> <span data-ttu-id="7beb8-159">toocustomize te ustawienia, wybierz opcję hello koło zębate ikonę toohello rogu hello listy rozwijanej, a następnie wybierz **nowe ustawienie wstępne**.</span><span class="sxs-lookup"><span data-stu-id="7beb8-159">toocustomize these settings, select hello gear icon toohello right of hello drop down, and then choose **New Preset**.</span></span>

    ![wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast3.png)
5. <span data-ttu-id="7beb8-161">Skonfiguruj ustawienia kodera.</span><span class="sxs-lookup"><span data-stu-id="7beb8-161">Configure encoder presets.</span></span>

    <span data-ttu-id="7beb8-162">Hello nazwy ustawienia wstępnego i sprawdź, czy hello następujących zalecanych ustawień:</span><span class="sxs-lookup"><span data-stu-id="7beb8-162">Name hello preset, and check for hello following recommended settings:</span></span>

    <span data-ttu-id="7beb8-163">**Wideo**</span><span class="sxs-lookup"><span data-stu-id="7beb8-163">**Video**</span></span>

   * <span data-ttu-id="7beb8-164">Koder: MainConcept H.264</span><span class="sxs-lookup"><span data-stu-id="7beb8-164">Encoder: MainConcept H.264</span></span>
   * <span data-ttu-id="7beb8-165">Klatek na sekundę: 30</span><span class="sxs-lookup"><span data-stu-id="7beb8-165">Frames per Second: 30</span></span>
   * <span data-ttu-id="7beb8-166">Średnia szybkość transmisji bitów: 5000 kbitów na sekundę (może być określany na podstawie ograniczenia sieci)</span><span class="sxs-lookup"><span data-stu-id="7beb8-166">Average bit rate: 5000 kbits/sec (Can be adjusted based on network limitations)</span></span>
   * <span data-ttu-id="7beb8-167">Profil: Main</span><span class="sxs-lookup"><span data-stu-id="7beb8-167">Profile: Main</span></span>
   * <span data-ttu-id="7beb8-168">Klatki co: 60 klatek</span><span class="sxs-lookup"><span data-stu-id="7beb8-168">Key frame every: 60 frames</span></span>

    <span data-ttu-id="7beb8-169">**Audio**</span><span class="sxs-lookup"><span data-stu-id="7beb8-169">**Audio**</span></span>

   * <span data-ttu-id="7beb8-170">Docelowa szybkość transmisji bitów: 192 kbitów/s</span><span class="sxs-lookup"><span data-stu-id="7beb8-170">Target bit rate: 192 kbits/sec</span></span>
   * <span data-ttu-id="7beb8-171">Częstotliwość próbkowania: 44 100 kHz</span><span class="sxs-lookup"><span data-stu-id="7beb8-171">Sample Rate: 44.100 kHz</span></span>

     ![wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast4.png)
6. <span data-ttu-id="7beb8-173">Naciśnij klawisz **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="7beb8-173">Press **Save**.</span></span>

    <span data-ttu-id="7beb8-174">pola Encoding Hello ma teraz hello nowo utworzony profil dostępne do wyboru.</span><span class="sxs-lookup"><span data-stu-id="7beb8-174">hello Encoding field now has hello newly created profile available for selection.</span></span>

    <span data-ttu-id="7beb8-175">Upewnij się, że wybrano hello nowy profil.</span><span class="sxs-lookup"><span data-stu-id="7beb8-175">Make sure hello new profile is selected.</span></span>
7. <span data-ttu-id="7beb8-176">Pobierz hello kanał wejściowy adres URL w kolejności tooassign on toohello Wirecast **punktu końcowego protokołu RTMP**.</span><span class="sxs-lookup"><span data-stu-id="7beb8-176">Get hello channel's input URL in order tooassign it toohello Wirecast **RTMP Endpoint**.</span></span>

    <span data-ttu-id="7beb8-177">Przejdź wstecz toohello narzędzie AMSE i sprawdzić stan ukończenia hello kanału.</span><span class="sxs-lookup"><span data-stu-id="7beb8-177">Navigate back toohello AMSE tool, and check on hello channel completion status.</span></span> <span data-ttu-id="7beb8-178">Po hello stan został zmieniony z **uruchamianie** za**systemem**, możesz uzyskać hello wejściowy adres URL.</span><span class="sxs-lookup"><span data-stu-id="7beb8-178">Once hello State has changed from **Starting** too**Running**, you can get hello input URL.</span></span>

    <span data-ttu-id="7beb8-179">Gdy kanał hello jest uruchomiona, kliknij prawym przyciskiem myszy nazwę kanału hello, przechodzenia toohover za pośrednictwem **tooclipboard kopia danych wejściowych URL** , a następnie wybierz **podstawowego adresu URL danych wejściowych**.</span><span class="sxs-lookup"><span data-stu-id="7beb8-179">When hello channel is running, right click hello channel name, navigate down toohover over **Copy Input URL tooclipboard** and then select **Primary Input  URL**.</span></span>  

    ![wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast6.png)
8. <span data-ttu-id="7beb8-181">W hello Wirecast **ustawienia wyjściowej** okna, Wklej te informacje w hello **adres** pole hello dane wyjściowe sekcji, a następnie przypisz nazwę strumienia.</span><span class="sxs-lookup"><span data-stu-id="7beb8-181">In hello Wirecast **Output Settings** window, paste this information in hello **Address** field of hello output section, and assign a stream name.</span></span>

    ![wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast5.png)

1. <span data-ttu-id="7beb8-183">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="7beb8-183">Select **OK**.</span></span>
2. <span data-ttu-id="7beb8-184">Na powitania głównego **Wirecast** Sprawdź źródeł danych wejściowych dla audio i wideo są gotowe, a następnie naciśnij **strumienia** w hello lewego górnego rogu.</span><span class="sxs-lookup"><span data-stu-id="7beb8-184">On hello main **Wirecast** screen, confirm input sources for video and audio are ready and then hit **Stream** in hello top left hand corner.</span></span>

   ![wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast7.png)

> [!IMPORTANT]
> <span data-ttu-id="7beb8-186">Przed kliknięciem przycisku **strumienia**, możesz **musi** upewnij się, że kanał hello jest gotowy.</span><span class="sxs-lookup"><span data-stu-id="7beb8-186">Before you click **Stream**, you **must** ensure that hello Channel is ready.</span></span>
> <span data-ttu-id="7beb8-187">Sprawdź także, czy nie tooleave hello kanału w stanie Gotowe bez wprowadzania wkład źródła danych przez czas dłuższy niż > 15 minut.</span><span class="sxs-lookup"><span data-stu-id="7beb8-187">Also, make sure not tooleave hello Channel in a ready state without an input contribution feed for longer than > 15 minutes.</span></span>
>
>

## <a name="test-playback"></a><span data-ttu-id="7beb8-188">Podczas odtwarzania testu</span><span class="sxs-lookup"><span data-stu-id="7beb8-188">Test playback</span></span>

<span data-ttu-id="7beb8-189">Przejdź narzędzie AMSE toohello, a następnie kliknij prawym przyciskiem myszy toobe kanału hello przetestowane.</span><span class="sxs-lookup"><span data-stu-id="7beb8-189">Navigate toohello AMSE tool, and right click hello channel toobe tested.</span></span> <span data-ttu-id="7beb8-190">Z hello menu, umieść kursor nad **hello odtwarzania podglądu** i wybierz **z usługi Azure Media Player**.</span><span class="sxs-lookup"><span data-stu-id="7beb8-190">From hello menu, hover over **Playback hello Preview** and select **with Azure Media Player**.</span></span>  

    ![wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast8.png)

<span data-ttu-id="7beb8-191">Czy strumienia hello znajduje się w hello player, koder hello został tooAMS tooconnect poprawnie skonfigurowana.</span><span class="sxs-lookup"><span data-stu-id="7beb8-191">If hello stream appears in hello player, then hello encoder has been properly configured tooconnect tooAMS.</span></span>

<span data-ttu-id="7beb8-192">Jeśli błąd kanału hello należy toobe resetowania i koder zmienić ustawienia.</span><span class="sxs-lookup"><span data-stu-id="7beb8-192">If an error is received, hello channel will need toobe reset and encoder settings adjusted.</span></span> <span data-ttu-id="7beb8-193">Zobacz hello [Rozwiązywanie problemów z](media-services-troubleshooting-live-streaming.md) tematu, aby uzyskać wskazówki.</span><span class="sxs-lookup"><span data-stu-id="7beb8-193">Please see hello [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>  

## <a name="create-a-program"></a><span data-ttu-id="7beb8-194">Utwórz program</span><span class="sxs-lookup"><span data-stu-id="7beb8-194">Create a program</span></span>
1. <span data-ttu-id="7beb8-195">Po potwierdzeniu kanału odtwarzania, tworzenia programu.</span><span class="sxs-lookup"><span data-stu-id="7beb8-195">Once channel playback is confirmed, create a program.</span></span> <span data-ttu-id="7beb8-196">W obszarze hello **Live** narzędzia AMSE hello, kliknij prawym przyciskiem myszy w obszarze program hello i wybierz **utworzyć nowy Program**.</span><span class="sxs-lookup"><span data-stu-id="7beb8-196">Under hello **Live** tab in hello AMSE tool, right click within hello program area and select **Create New Program**.</span></span>  

    ![wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast9.png)
2. <span data-ttu-id="7beb8-198">Nazwy hello program i w razie potrzeby dostosuj hello **długość okna archiwum** (domyślne ustawienia too4 godzin, w których).</span><span class="sxs-lookup"><span data-stu-id="7beb8-198">Name hello program and, if needed, adjust hello **Archive Window Length** (which defaults too4 hours).</span></span> <span data-ttu-id="7beb8-199">Można także określić miejsce przechowywania lub pozostaw domyślne hello.</span><span class="sxs-lookup"><span data-stu-id="7beb8-199">You can also specify a storage location or leave as hello default.</span></span>  
3. <span data-ttu-id="7beb8-200">Sprawdź hello **Start hello Program teraz** pole.</span><span class="sxs-lookup"><span data-stu-id="7beb8-200">Check hello **Start hello Program now** box.</span></span>
4. <span data-ttu-id="7beb8-201">Kliknij przycisk **utworzyć Program**.</span><span class="sxs-lookup"><span data-stu-id="7beb8-201">Click **Create Program**.</span></span>  

   >[!NOTE]
   ><span data-ttu-id="7beb8-202">Tworzenie programu zajmuje mniej czasu niż tworzenie kanału.</span><span class="sxs-lookup"><span data-stu-id="7beb8-202">Program creation takes less time than channel creation.</span></span>
       
5. <span data-ttu-id="7beb8-203">Po uruchomieniu hello program potwierdzić odtwarzania przez kliknięcie prawym przyciskiem myszy hello program i przechodząc zbyt**programach hello odtwarzania** , a następnie wybierając **z usługi Azure Media Player**.</span><span class="sxs-lookup"><span data-stu-id="7beb8-203">Once hello program is running, confirm playback by right clicking hello program and navigating too**Playback hello program(s)** and then selecting **with Azure Media Player**.</span></span>  
6. <span data-ttu-id="7beb8-204">Po potwierdzeniu, kliknij prawym przyciskiem myszy hello program ponownie i wybierz **skopiuj hello adresu URL danych wyjściowych tooClipboard** (lub pobrać te informacje z hello **programu informacji i ustawień** opcji z hello menu).</span><span class="sxs-lookup"><span data-stu-id="7beb8-204">Once confirmed, right click hello program again and select **Copy hello Output URL tooClipboard** (or retrieve this information from hello **Program information and settings** option from hello menu).</span></span>

<span data-ttu-id="7beb8-205">strumień Hello jest teraz gotowy toobe osadzony w odtwarzacza lub odbiorcami tooan rozproszone na żywo wyświetlanie.</span><span class="sxs-lookup"><span data-stu-id="7beb8-205">hello stream is now ready toobe embedded in a player, or distributed tooan audience for live viewing.</span></span>  

## <a name="troubleshooting"></a><span data-ttu-id="7beb8-206">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="7beb8-206">Troubleshooting</span></span>
<span data-ttu-id="7beb8-207">Zobacz hello [Rozwiązywanie problemów z](media-services-troubleshooting-live-streaming.md) tematu, aby uzyskać wskazówki.</span><span class="sxs-lookup"><span data-stu-id="7beb8-207">Please see hello [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="7beb8-208">Ścieżki szkoleniowe dotyczące usługi Media Services</span><span class="sxs-lookup"><span data-stu-id="7beb8-208">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="7beb8-209">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="7beb8-209">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
