---
title: "aaaConfigure hello toosend kodera na żywo stanie wolnym strumień na żywo o pojedynczej szybkości transmisji bitów | Dokumentacja firmy Microsoft"
description: "W tym temacie przedstawiono sposób tooconfigure hello toosend kodera na żywo stanie wolnym kanałami tooAMS strumienia pojedynczej szybkości transmisji bitów, obsługującymi kodowanie na żywo."
services: media-services
documentationcenter: 
author: cenkdin
manager: cfowler
editor: 
ms.assetid: 9c6bf6a9-6273-4fdd-9477-f0e565280b5b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 01/05/2017
ms.author: cenkd;anilmur;juliako
ms.openlocfilehash: 9a5de6189bfb123768a9da038b8c8db69cf85e91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-elemental-live-encoder-toosend-a-single-bitrate-live-stream"></a><span data-ttu-id="fa1e9-103">Użyj toosend kodera na żywo stanie wolnym hello strumień na żywo o pojedynczej szybkości transmisji bitów</span><span class="sxs-lookup"><span data-stu-id="fa1e9-103">Use hello Elemental Live encoder toosend a single bitrate live stream</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="fa1e9-104">Elemental na żywo</span><span class="sxs-lookup"><span data-stu-id="fa1e9-104">Elemental Live</span></span>](media-services-configure-elemental-live-encoder.md)
> * [<span data-ttu-id="fa1e9-105">Tricaster</span><span class="sxs-lookup"><span data-stu-id="fa1e9-105">Tricaster</span></span>](media-services-configure-tricaster-live-encoder.md)
> * [<span data-ttu-id="fa1e9-106">Wirecast</span><span class="sxs-lookup"><span data-stu-id="fa1e9-106">Wirecast</span></span>](media-services-configure-wirecast-live-encoder.md)
> * [<span data-ttu-id="fa1e9-107">FMLE</span><span class="sxs-lookup"><span data-stu-id="fa1e9-107">FMLE</span></span>](media-services-configure-fmle-live-encoder.md)
>
>

<span data-ttu-id="fa1e9-108">W tym temacie przedstawiono sposób tooconfigure hello [stanie wolnym Live](http://www.elementaltechnologies.com/products/elemental-live) toosend kodera kanałami tooAMS, obsługującymi kodowanie na żywo strumienia pojedynczej szybkości transmisji bitów.</span><span class="sxs-lookup"><span data-stu-id="fa1e9-108">This topic shows how tooconfigure hello [Elemental Live](http://www.elementaltechnologies.com/products/elemental-live) encoder toosend a single bitrate stream tooAMS channels that are enabled for live encoding.</span></span>  <span data-ttu-id="fa1e9-109">Aby uzyskać więcej informacji, zobacz [Praca z kanałami, że włączono tooPerform Live kodowania za pomocą usługi Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).</span><span class="sxs-lookup"><span data-stu-id="fa1e9-109">For more information, see [Working with Channels that are Enabled tooPerform Live Encoding with Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).</span></span>

<span data-ttu-id="fa1e9-110">Ten samouczek pokazuje, jak toomanage usługi Azure Media Services (AMS) za pomocą narzędzia Azure Media Services Explorer (AMSE).</span><span class="sxs-lookup"><span data-stu-id="fa1e9-110">This tutorial shows how toomanage Azure Media Services (AMS) with Azure Media Services Explorer (AMSE) tool.</span></span> <span data-ttu-id="fa1e9-111">To narzędzie jest uruchamiane tylko na komputerze z systemem Windows.</span><span class="sxs-lookup"><span data-stu-id="fa1e9-111">This tool only runs on Windows PC.</span></span> <span data-ttu-id="fa1e9-112">Mac lub Linux, za pomocą hello Azure portalu toocreate [kanałów](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) i [programy](media-services-portal-creating-live-encoder-enabled-channel.md).</span><span class="sxs-lookup"><span data-stu-id="fa1e9-112">If you are on Mac or Linux, use hello Azure portal toocreate [channels](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) and [programs](media-services-portal-creating-live-encoder-enabled-channel.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fa1e9-113">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="fa1e9-113">Prerequisites</span></span>
* <span data-ttu-id="fa1e9-114">Musi mieć praktyczną wiedzę o użyciu stanie wolnym Live sieci web interfejsu toocreate wydarzeń na żywo.</span><span class="sxs-lookup"><span data-stu-id="fa1e9-114">Must have a working knowledge of using Elemental Live web interface toocreate live events.</span></span>
* [<span data-ttu-id="fa1e9-115">Tworzenie konta usługi Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="fa1e9-115">Create an Azure Media Services account</span></span>](media-services-portal-create-account.md)
* <span data-ttu-id="fa1e9-116">Upewnij się, brak punktu końcowego przesyłania strumieniowego uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="fa1e9-116">Ensure there is a Streaming Endpoint running.</span></span> <span data-ttu-id="fa1e9-117">Aby uzyskać więcej informacji, zobacz [zarządzanie punktami końcowymi przesyłania strumieniowego w konta usługi Media Services](media-services-portal-manage-streaming-endpoints.md).</span><span class="sxs-lookup"><span data-stu-id="fa1e9-117">For more information, see [Manage Streaming Endpoints in a Media Services Account](media-services-portal-manage-streaming-endpoints.md).</span></span>
* <span data-ttu-id="fa1e9-118">Zainstaluj najnowszą wersję hello hello [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) narzędzia.</span><span class="sxs-lookup"><span data-stu-id="fa1e9-118">Install hello latest version of hello [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) tool.</span></span>
* <span data-ttu-id="fa1e9-119">Uruchom narzędzie hello i Połącz konto tooyour AMS.</span><span class="sxs-lookup"><span data-stu-id="fa1e9-119">Launch hello tool and connect tooyour AMS account.</span></span>

## <a name="tips"></a><span data-ttu-id="fa1e9-120">Porady</span><span class="sxs-lookup"><span data-stu-id="fa1e9-120">Tips</span></span>
* <span data-ttu-id="fa1e9-121">Jeśli to możliwe, użyj połączenia internetowego hardwired.</span><span class="sxs-lookup"><span data-stu-id="fa1e9-121">Whenever possible, use a hardwired internet connection.</span></span>
* <span data-ttu-id="fa1e9-122">Regułą podczas określania wymaganiach odnośnie do przepustowości jest hello toodouble przesyłania strumieniowego szybkości transmisji bitów.</span><span class="sxs-lookup"><span data-stu-id="fa1e9-122">A good rule of thumb when determining bandwidth requirements is toodouble hello streaming bitrates.</span></span> <span data-ttu-id="fa1e9-123">Chociaż nie jest to wymagane, może pomóc zmniejszyć wpływ hello sieci przeciążona.</span><span class="sxs-lookup"><span data-stu-id="fa1e9-123">While this is not a mandatory requirement, it will help mitigate hello impact of network congestion.</span></span>
* <span data-ttu-id="fa1e9-124">Gdy za pomocą oprogramowania na podstawie koderów, zamknij wszystkie zbędne programy.</span><span class="sxs-lookup"><span data-stu-id="fa1e9-124">When using software based encoders, close out any unnecessary programs.</span></span>

## <a name="elemental-live-with-rtp-ingest"></a><span data-ttu-id="fa1e9-125">Pozyskiwania stanie wolnym Live przy włączonej ochronie czasu rzeczywistego</span><span class="sxs-lookup"><span data-stu-id="fa1e9-125">Elemental Live with RTP ingest</span></span>
<span data-ttu-id="fa1e9-126">W tej sekcji przedstawiono, jak tooconfigure hello stanie wolnym Live kodera, który wysyła pojedynczej szybkości transmisji bitów strumień na żywo przy użyciu protokołu RTP.</span><span class="sxs-lookup"><span data-stu-id="fa1e9-126">This section shows how tooconfigure hello Elemental Live encoder that sends a single bitrate live stream over RTP.</span></span>  <span data-ttu-id="fa1e9-127">Aby uzyskać więcej informacji, zobacz [strumieni MPEG-TS przy użyciu protokołu RTP](media-services-manage-live-encoder-enabled-channels.md#channel).</span><span class="sxs-lookup"><span data-stu-id="fa1e9-127">For more information, see [MPEG-TS stream over RTP](media-services-manage-live-encoder-enabled-channels.md#channel).</span></span>

### <a name="create-a-channel"></a><span data-ttu-id="fa1e9-128">Tworzenie kanału</span><span class="sxs-lookup"><span data-stu-id="fa1e9-128">Create a channel</span></span>

1. <span data-ttu-id="fa1e9-129">Narzędzie AMSE hello Przejdź toohello **Live** karcie, a następnie kliknij prawym przyciskiem myszy w obszarze kanału hello.</span><span class="sxs-lookup"><span data-stu-id="fa1e9-129">In hello AMSE tool, navigate toohello **Live** tab, and right click within hello channel area.</span></span> <span data-ttu-id="fa1e9-130">Wybierz **Utwórz kanał...**</span><span class="sxs-lookup"><span data-stu-id="fa1e9-130">Select **Create channel…**</span></span> <span data-ttu-id="fa1e9-131">z hello menu.</span><span class="sxs-lookup"><span data-stu-id="fa1e9-131">from hello menu.</span></span>

    ![Stanie wolnym](./media/media-services-elemental-live-encoder/media-services-elemental1.png)

2. <span data-ttu-id="fa1e9-133">Określ nazwę kanału hello pole opisu jest opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="fa1e9-133">Specify a channel name, hello description field is optional.</span></span> <span data-ttu-id="fa1e9-134">W ustawieniach kanału, wybierz **standardowe** dla hello opcji kodowanie na żywo z hello wprowadzania ustawiony protokół zbyt**RTP (MPEG-TS)**.</span><span class="sxs-lookup"><span data-stu-id="fa1e9-134">Under Channel Settings, select **Standard** for hello Live Encoding option, with hello Input Protocol set too**RTP (MPEG-TS)**.</span></span> <span data-ttu-id="fa1e9-135">Możesz pozostawić wszystkie inne ustawienia, ponieważ jest.</span><span class="sxs-lookup"><span data-stu-id="fa1e9-135">You can leave all other settings as is.</span></span>

    <span data-ttu-id="fa1e9-136">Upewnij się, że hello **Start hello nowy kanał teraz** jest zaznaczone.</span><span class="sxs-lookup"><span data-stu-id="fa1e9-136">Make sure hello **Start hello new channel now** is selected.</span></span>

3. <span data-ttu-id="fa1e9-137">Kliknij przycisk **utworzyć kanał**.</span><span class="sxs-lookup"><span data-stu-id="fa1e9-137">Click **Create Channel**.</span></span>

   ![Stanie wolnym](./media/media-services-elemental-live-encoder/media-services-elemental12.png)

> [!NOTE]
> <span data-ttu-id="fa1e9-139">kanał Hello może zająć toostart 20 minut.</span><span class="sxs-lookup"><span data-stu-id="fa1e9-139">hello channel can take as long as 20 minutes toostart.</span></span>
>
>

<span data-ttu-id="fa1e9-140">Podczas uruchamiania kanału hello można [skonfigurować koder hello](media-services-configure-elemental-live-encoder.md#configure_elemental_rtp).</span><span class="sxs-lookup"><span data-stu-id="fa1e9-140">While hello channel is starting you can [configure hello encoder](media-services-configure-elemental-live-encoder.md#configure_elemental_rtp).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fa1e9-141">Należy pamiętać, że rozliczanie zaczyna się jak kanału przechodzi do stanu gotowości.</span><span class="sxs-lookup"><span data-stu-id="fa1e9-141">Note that billing starts as soon as Channel goes into a ready state.</span></span> <span data-ttu-id="fa1e9-142">Aby uzyskać więcej informacji, zobacz [stanów kanału](media-services-manage-live-encoder-enabled-channels.md#states).</span><span class="sxs-lookup"><span data-stu-id="fa1e9-142">For more information, see [Channel's states](media-services-manage-live-encoder-enabled-channels.md#states).</span></span>
>
>

### <span data-ttu-id="fa1e9-143"><a id=configure_elemental_rtp></a>Konfigurowanie kodera na żywo stanie wolnym hello</span><span class="sxs-lookup"><span data-stu-id="fa1e9-143"><a id=configure_elemental_rtp></a>Configure hello Elemental Live encoder</span></span>
<span data-ttu-id="fa1e9-144">W tym samouczek hello są używane następujące ustawienia danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="fa1e9-144">In this tutorial hello following output settings are used.</span></span> <span data-ttu-id="fa1e9-145">Hello pozostałej części tej sekcji opisano kroki konfiguracji szczegółowo.</span><span class="sxs-lookup"><span data-stu-id="fa1e9-145">hello rest of this section describes configuration steps in more detail.</span></span>

<span data-ttu-id="fa1e9-146">**Wideo**:</span><span class="sxs-lookup"><span data-stu-id="fa1e9-146">**Video**:</span></span>

* <span data-ttu-id="fa1e9-147">Koder-dekoder: H.264</span><span class="sxs-lookup"><span data-stu-id="fa1e9-147">Codec: H.264</span></span>
* <span data-ttu-id="fa1e9-148">Profil: Wysoki (poziom 4.0)</span><span class="sxs-lookup"><span data-stu-id="fa1e9-148">Profile: High (Level 4.0)</span></span>
* <span data-ttu-id="fa1e9-149">Szybkość transmisji bitów: 5000 KB/s</span><span class="sxs-lookup"><span data-stu-id="fa1e9-149">Bitrate: 5000 kbps</span></span>
* <span data-ttu-id="fa1e9-150">Klatki kluczowej: 2 sekundy (60 sekund)</span><span class="sxs-lookup"><span data-stu-id="fa1e9-150">Keyframe: 2 seconds (60 seconds)</span></span>
* <span data-ttu-id="fa1e9-151">Szybkość klatek: 30</span><span class="sxs-lookup"><span data-stu-id="fa1e9-151">Frame Rate: 30</span></span>

<span data-ttu-id="fa1e9-152">**Audio**:</span><span class="sxs-lookup"><span data-stu-id="fa1e9-152">**Audio**:</span></span>

* <span data-ttu-id="fa1e9-153">Koder-dekoder: AAC (LC —)</span><span class="sxs-lookup"><span data-stu-id="fa1e9-153">Codec: AAC (LC)</span></span>
* <span data-ttu-id="fa1e9-154">Szybkość transmisji bitów: 192 kb/s</span><span class="sxs-lookup"><span data-stu-id="fa1e9-154">Bitrate: 192 kbps</span></span>
* <span data-ttu-id="fa1e9-155">Częstotliwość próbkowania: 44,1 kHz</span><span class="sxs-lookup"><span data-stu-id="fa1e9-155">Sample Rate: 44.1 kHz</span></span>

#### <a name="configuration-steps"></a><span data-ttu-id="fa1e9-156">Kroki konfiguracji</span><span class="sxs-lookup"><span data-stu-id="fa1e9-156">Configuration steps</span></span>
1. <span data-ttu-id="fa1e9-157">Przejdź toohello **stanie wolnym Live** sieci web interfejsu i skonfigurować hello kodera dla **UDP/TS** przesyłania strumieniowego.</span><span class="sxs-lookup"><span data-stu-id="fa1e9-157">Navigate toohello **Elemental Live** web interface, and set up hello encoder for **UDP/TS** streaming.</span></span>
2. <span data-ttu-id="fa1e9-158">Po utworzeniu nowego zdarzenia, przewiń w dół toohello grupy danych wyjściowych i dodać hello **UDP/TS** grupy wyjściowej.</span><span class="sxs-lookup"><span data-stu-id="fa1e9-158">Once a new event is created, scroll down toohello output groups and add hello **UDP/TS** output group.</span></span>
3. <span data-ttu-id="fa1e9-159">Utwórz nowe dane wyjściowe, zaznaczając **nowego strumienia** , a następnie klikając polecenie **dodać danych wyjściowych**.</span><span class="sxs-lookup"><span data-stu-id="fa1e9-159">Create a new output by selecting **New Stream** and then clicking **Add Output**.</span></span>  

    ![Stanie wolnym](./media/media-services-elemental-live-encoder/media-services-elemental13.png)

   > [!NOTE]
   > <span data-ttu-id="fa1e9-161">Zaleca się zdarzenie stanie wolnym hello ma kod czasowy hello ustawić także kodera hello toohelp "Zegara systemowego" Połącz ponownie w przypadku hello awarii strumienia.</span><span class="sxs-lookup"><span data-stu-id="fa1e9-161">It is recommended that hello Elemental event has hello timecode set too"System Clock" toohelp hello encoder reconnect in hello case of a stream failure.</span></span>
   >
   >
4. <span data-ttu-id="fa1e9-162">Teraz, gdy hello danych wyjściowych został utworzony, kliknij przycisk **dodać strumienia**.</span><span class="sxs-lookup"><span data-stu-id="fa1e9-162">Now that hello Output has been created, click **Add Stream**.</span></span> <span data-ttu-id="fa1e9-163">Teraz można skonfigurować ustawienia wyjściowej Hello.</span><span class="sxs-lookup"><span data-stu-id="fa1e9-163">hello output settings can now be configured.</span></span>
5. <span data-ttu-id="fa1e9-164">Przewiń w dół toohello "Strumień 1", która właśnie została utworzona, kliknij przycisk hello **wideo** karcie po lewej stronie powitania i rozwiń hello **zaawansowane** w sekcji Ustawienia.</span><span class="sxs-lookup"><span data-stu-id="fa1e9-164">Scroll down toohello "Stream 1" that was just created, click hello **Video** tab on hello left and expand hello **Advanced** settings section.</span></span>

    ![Stanie wolnym](./media/media-services-elemental-live-encoder/media-services-elemental4.png)

    <span data-ttu-id="fa1e9-166">Podczas aktywnego stanie wolnym ma szeroki zakres dostosowywania dostępne, hello następujące ustawienia są zalecane w przypadku wprowadzenie do przesyłania strumieniowego tooAMS.</span><span class="sxs-lookup"><span data-stu-id="fa1e9-166">While Elemental Live has a wide range of available customizing, hello following settings are recommended for getting started with streaming tooAMS.</span></span>

   * <span data-ttu-id="fa1e9-167">Rozdzielczość: 1280 x 720</span><span class="sxs-lookup"><span data-stu-id="fa1e9-167">Resolution: 1280 x 720</span></span>
   * <span data-ttu-id="fa1e9-168">Szybkość klatek: 30</span><span class="sxs-lookup"><span data-stu-id="fa1e9-168">Framerate: 30</span></span>
   * <span data-ttu-id="fa1e9-169">Rozmiar GOP: 60 klatek</span><span class="sxs-lookup"><span data-stu-id="fa1e9-169">GOP Size: 60 frames</span></span>
   * <span data-ttu-id="fa1e9-170">Tryb przeplotu: progresywnego</span><span class="sxs-lookup"><span data-stu-id="fa1e9-170">Interlace Mode: Progressive</span></span>
   * <span data-ttu-id="fa1e9-171">Szybkość transmisji bitów: 5000000 bit/s (to może być określany na podstawie ograniczenia sieci)</span><span class="sxs-lookup"><span data-stu-id="fa1e9-171">Bitrate: 5000000 bit/s (This can be adjusted based on network limitations)</span></span>

    ![Stanie wolnym](./media/media-services-elemental-live-encoder/media-services-elemental5.png)

1. <span data-ttu-id="fa1e9-173">Pobierz hello kanał wejściowy adres URL.</span><span class="sxs-lookup"><span data-stu-id="fa1e9-173">Get hello channel's input URL.</span></span>

    <span data-ttu-id="fa1e9-174">Przejdź wstecz toohello narzędzie AMSE i sprawdzić stan ukończenia hello kanału.</span><span class="sxs-lookup"><span data-stu-id="fa1e9-174">Navigate back toohello AMSE tool, and check on hello channel completion status.</span></span> <span data-ttu-id="fa1e9-175">Po hello stan został zmieniony z **uruchamianie** za**systemem**, możesz uzyskać hello wejściowy adres URL.</span><span class="sxs-lookup"><span data-stu-id="fa1e9-175">Once hello State has changed from **Starting** too**Running**, you can get hello input URL.</span></span>

    <span data-ttu-id="fa1e9-176">Gdy kanał hello jest uruchomiona, kliknij prawym przyciskiem myszy nazwę kanału hello, przechodzenia toohover za pośrednictwem **tooclipboard kopia danych wejściowych URL** , a następnie wybierz **podstawowego adresu URL danych wejściowych**.</span><span class="sxs-lookup"><span data-stu-id="fa1e9-176">When hello channel is running, right click hello channel name, navigate down toohover over **Copy Input URL tooclipboard** and then select **Primary Input  URL**.</span></span>  

    ![Stanie wolnym](./media/media-services-elemental-live-encoder/media-services-elemental6.png)
2. <span data-ttu-id="fa1e9-178">Wklej te informacje w hello **miejsce docelowe głównej** pole hello Elemental.</span><span class="sxs-lookup"><span data-stu-id="fa1e9-178">Paste this information in hello **Primary Destination** field of hello Elemental.</span></span> <span data-ttu-id="fa1e9-179">Wszystkie inne ustawienia mogą pozostać hello domyślne.</span><span class="sxs-lookup"><span data-stu-id="fa1e9-179">All other settings can remain hello default.</span></span>

    ![Stanie wolnym](./media/media-services-elemental-live-encoder/media-services-elemental14.png)

    <span data-ttu-id="fa1e9-181">Nadmiarowości dodatkowe Powtórz te kroki hello dodatkowej wprowadzania adresu URL, tworząc osobne karty "Wyjściowej" do przesyłania strumieniowego UDP/usług terminalowych.</span><span class="sxs-lookup"><span data-stu-id="fa1e9-181">For extra redundancy, repeat these steps with hello Secondary Input URL by creating a separate "Output" tab for UDP/TS Streaming.</span></span>
3. <span data-ttu-id="fa1e9-182">Kliknij przycisk **Utwórz** (Jeśli utworzono nowe zdarzenie) lub **aktualizacji** (jeśli edycji istniejące zdarzenie) i przejdź dalej toostart hello kodera.</span><span class="sxs-lookup"><span data-stu-id="fa1e9-182">Click **Create** (if a new event was created) or **Update** (if editing a pre-existing event) and then proceed toostart hello encoder.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fa1e9-183">Przed kliknięciem przycisku **Start** na powitania stanie wolnym Live interfejs sieci web, możesz **musi** upewnij się, że kanał hello jest gotowy.</span><span class="sxs-lookup"><span data-stu-id="fa1e9-183">Before you click **Start** on hello Elemental Live web interface, you **must** ensure that hello Channel is ready.</span></span>
> <span data-ttu-id="fa1e9-184">Sprawdź także, czy nie tooleave hello kanału w stanie Gotowe bez zdarzenia przez czas dłuższy niż > 15 minut.</span><span class="sxs-lookup"><span data-stu-id="fa1e9-184">Also, make sure not tooleave hello Channel in a ready state without an event for longer than > 15 minutes.</span></span>
>
>

<span data-ttu-id="fa1e9-185">Po działaniu strumienia hello 30 sekund, przejdź wstecz toohello AMSE narzędzia i testowania odtwarzania.</span><span class="sxs-lookup"><span data-stu-id="fa1e9-185">After hello stream has been running for 30 seconds, navigate back toohello AMSE tool and test playback.</span></span>  

### <a name="test-playback"></a><span data-ttu-id="fa1e9-186">Podczas odtwarzania testu</span><span class="sxs-lookup"><span data-stu-id="fa1e9-186">Test playback</span></span>

<span data-ttu-id="fa1e9-187">Przejdź narzędzie AMSE toohello, a następnie kliknij prawym przyciskiem myszy toobe kanału hello przetestowane.</span><span class="sxs-lookup"><span data-stu-id="fa1e9-187">Navigate toohello AMSE tool, and right click hello channel toobe tested.</span></span> <span data-ttu-id="fa1e9-188">Z hello menu, umieść kursor nad **hello odtwarzania podglądu** i wybierz **z usługi Azure Media Player**.</span><span class="sxs-lookup"><span data-stu-id="fa1e9-188">From hello menu, hover over **Playback hello Preview** and select **with Azure Media Player**.</span></span>  

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental8.png)

<span data-ttu-id="fa1e9-189">Czy strumienia hello znajduje się w hello player, koder hello został tooAMS tooconnect poprawnie skonfigurowana.</span><span class="sxs-lookup"><span data-stu-id="fa1e9-189">If hello stream appears in hello player, then hello encoder has been properly configured tooconnect tooAMS.</span></span>

<span data-ttu-id="fa1e9-190">Jeśli błąd kanału hello należy toobe resetowania i koder zmienić ustawienia.</span><span class="sxs-lookup"><span data-stu-id="fa1e9-190">If an error is received, hello channel will need toobe reset and encoder settings adjusted.</span></span> <span data-ttu-id="fa1e9-191">Zobacz hello [Rozwiązywanie problemów z](media-services-troubleshooting-live-streaming.md) tematu, aby uzyskać wskazówki.</span><span class="sxs-lookup"><span data-stu-id="fa1e9-191">Please see hello [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>   

### <a name="create-a-program"></a><span data-ttu-id="fa1e9-192">Utwórz program</span><span class="sxs-lookup"><span data-stu-id="fa1e9-192">Create a program</span></span>
1. <span data-ttu-id="fa1e9-193">Po potwierdzeniu kanału odtwarzania, tworzenia programu.</span><span class="sxs-lookup"><span data-stu-id="fa1e9-193">Once channel playback is confirmed, create a program.</span></span> <span data-ttu-id="fa1e9-194">W obszarze hello **Live** narzędzia AMSE hello, kliknij prawym przyciskiem myszy w obszarze program hello i wybierz **utworzyć nowy Program**.</span><span class="sxs-lookup"><span data-stu-id="fa1e9-194">Under hello **Live** tab in hello AMSE tool, right click within hello program area and select **Create New Program**.</span></span>  

    ![Stanie wolnym](./media/media-services-elemental-live-encoder/media-services-elemental9.png)
2. <span data-ttu-id="fa1e9-196">Nazwy hello program i w razie potrzeby dostosuj hello **długość okna archiwum** (domyślne ustawienia too4 godzin, w których).</span><span class="sxs-lookup"><span data-stu-id="fa1e9-196">Name hello program and, if needed, adjust hello **Archive Window Length** (which defaults too4 hours).</span></span> <span data-ttu-id="fa1e9-197">Można także określić miejsce przechowywania lub pozostaw domyślne hello.</span><span class="sxs-lookup"><span data-stu-id="fa1e9-197">You can also specify a storage location or leave as hello default.</span></span>  
3. <span data-ttu-id="fa1e9-198">Sprawdź hello **Start hello Program teraz** pole.</span><span class="sxs-lookup"><span data-stu-id="fa1e9-198">Check hello **Start hello Program now** box.</span></span>
4. <span data-ttu-id="fa1e9-199">Kliknij przycisk **utworzyć Program**.</span><span class="sxs-lookup"><span data-stu-id="fa1e9-199">Click **Create Program**.</span></span>  

    >[!NOTE]
    > <span data-ttu-id="fa1e9-200">Tworzenie programu zajmuje mniej czasu niż tworzenie kanału.</span><span class="sxs-lookup"><span data-stu-id="fa1e9-200">Program creation takes less time than channel creation.</span></span>   
      
5. <span data-ttu-id="fa1e9-201">Po uruchomieniu hello program potwierdzić odtwarzania przez kliknięcie prawym przyciskiem myszy hello program i przechodząc zbyt**programach hello odtwarzania** , a następnie wybierając **z usługi Azure Media Player**.</span><span class="sxs-lookup"><span data-stu-id="fa1e9-201">Once hello program is running, confirm playback by right clicking hello program and navigating too**Playback hello program(s)** and then selecting **with Azure Media Player**.</span></span>  
6. <span data-ttu-id="fa1e9-202">Po potwierdzeniu, kliknij prawym przyciskiem myszy hello program ponownie i wybierz **skopiuj hello adresu URL danych wyjściowych tooClipboard** (lub pobrać te informacje z hello **programu informacji i ustawień** opcji z hello menu).</span><span class="sxs-lookup"><span data-stu-id="fa1e9-202">Once confirmed, right click hello program again and select **Copy hello Output URL tooClipboard** (or retrieve this information from hello **Program information and settings** option from hello menu).</span></span>

<span data-ttu-id="fa1e9-203">strumień Hello jest teraz gotowy toobe osadzony w odtwarzacza lub odbiorcami tooan rozproszone na żywo wyświetlanie.</span><span class="sxs-lookup"><span data-stu-id="fa1e9-203">hello stream is now ready toobe embedded in a player, or distributed tooan audience for live viewing.</span></span>  

## <a name="troubleshooting"></a><span data-ttu-id="fa1e9-204">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="fa1e9-204">Troubleshooting</span></span>
<span data-ttu-id="fa1e9-205">Zobacz hello [Rozwiązywanie problemów z](media-services-troubleshooting-live-streaming.md) tematu, aby uzyskać wskazówki.</span><span class="sxs-lookup"><span data-stu-id="fa1e9-205">Please see hello [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="fa1e9-206">Ścieżki szkoleniowe dotyczące usługi Media Services</span><span class="sxs-lookup"><span data-stu-id="fa1e9-206">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="fa1e9-207">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="fa1e9-207">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
