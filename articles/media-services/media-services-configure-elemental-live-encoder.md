---
title: "Konfigurowanie kodera na żywo stanie wolnym wysłać strumień na żywo o pojedynczej szybkości transmisji bitów | Dokumentacja firmy Microsoft"
description: "W tym temacie przedstawiono sposób konfigurowania kodera na żywo stanie wolnym do wysłania do kanałów AMS, które są włączone dla kodowanie na żywo o pojedynczej szybkości transmisji."
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
ms.openlocfilehash: 668a3ab46a70c0ee25fa87031d27c0f4333ec89c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="use-the-elemental-live-encoder-to-send-a-single-bitrate-live-stream"></a><span data-ttu-id="98d9b-103">Użyj kodera na żywo stanie wolnym, aby wysyłać strumień na żywo o pojedynczej szybkości transmisji bitów</span><span class="sxs-lookup"><span data-stu-id="98d9b-103">Use the Elemental Live encoder to send a single bitrate live stream</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="98d9b-104">Elemental na żywo</span><span class="sxs-lookup"><span data-stu-id="98d9b-104">Elemental Live</span></span>](media-services-configure-elemental-live-encoder.md)
> * [<span data-ttu-id="98d9b-105">Tricaster</span><span class="sxs-lookup"><span data-stu-id="98d9b-105">Tricaster</span></span>](media-services-configure-tricaster-live-encoder.md)
> * [<span data-ttu-id="98d9b-106">Wirecast</span><span class="sxs-lookup"><span data-stu-id="98d9b-106">Wirecast</span></span>](media-services-configure-wirecast-live-encoder.md)
> * [<span data-ttu-id="98d9b-107">FMLE</span><span class="sxs-lookup"><span data-stu-id="98d9b-107">FMLE</span></span>](media-services-configure-fmle-live-encoder.md)
>
>

<span data-ttu-id="98d9b-108">W tym temacie przedstawiono sposób konfigurowania [stanie wolnym Live](http://www.elementaltechnologies.com/products/elemental-live) kodera do wysyłania strumienia pojedynczej szybkości transmisji bitów AMS kanałów, które są włączone kodowanie na żywo.</span><span class="sxs-lookup"><span data-stu-id="98d9b-108">This topic shows how to configure the [Elemental Live](http://www.elementaltechnologies.com/products/elemental-live) encoder to send a single bitrate stream to AMS channels that are enabled for live encoding.</span></span>  <span data-ttu-id="98d9b-109">Aby uzyskać więcej informacji, zobacz temat [Praca z kanałami obsługującymi funkcję Live Encoding w usłudze Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).</span><span class="sxs-lookup"><span data-stu-id="98d9b-109">For more information, see [Working with Channels that are Enabled to Perform Live Encoding with Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).</span></span>

<span data-ttu-id="98d9b-110">W tym samouczku przedstawiono sposób zarządzania usługi Azure Media Services (AMS) za pomocą narzędzia Azure Media Services Explorer (AMSE).</span><span class="sxs-lookup"><span data-stu-id="98d9b-110">This tutorial shows how to manage Azure Media Services (AMS) with Azure Media Services Explorer (AMSE) tool.</span></span> <span data-ttu-id="98d9b-111">To narzędzie jest uruchamiane tylko na komputerze z systemem Windows.</span><span class="sxs-lookup"><span data-stu-id="98d9b-111">This tool only runs on Windows PC.</span></span> <span data-ttu-id="98d9b-112">Jeśli na Mac lub Linux, użyj portalu Azure do utworzenia [kanałów](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) i [programy](media-services-portal-creating-live-encoder-enabled-channel.md).</span><span class="sxs-lookup"><span data-stu-id="98d9b-112">If you are on Mac or Linux, use the Azure portal to create [channels](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) and [programs](media-services-portal-creating-live-encoder-enabled-channel.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="98d9b-113">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="98d9b-113">Prerequisites</span></span>
* <span data-ttu-id="98d9b-114">Musi mieć praktyczną wiedzę o tworzenie wydarzeń na żywo przy użyciu interfejsu sieci web stanie wolnym na żywo.</span><span class="sxs-lookup"><span data-stu-id="98d9b-114">Must have a working knowledge of using Elemental Live web interface to create live events.</span></span>
* [<span data-ttu-id="98d9b-115">Tworzenie konta usługi Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="98d9b-115">Create an Azure Media Services account</span></span>](media-services-portal-create-account.md)
* <span data-ttu-id="98d9b-116">Upewnij się, brak punktu końcowego przesyłania strumieniowego uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="98d9b-116">Ensure there is a Streaming Endpoint running.</span></span> <span data-ttu-id="98d9b-117">Aby uzyskać więcej informacji, zobacz [zarządzanie punktami końcowymi przesyłania strumieniowego w konta usługi Media Services](media-services-portal-manage-streaming-endpoints.md).</span><span class="sxs-lookup"><span data-stu-id="98d9b-117">For more information, see [Manage Streaming Endpoints in a Media Services Account](media-services-portal-manage-streaming-endpoints.md).</span></span>
* <span data-ttu-id="98d9b-118">Zainstaluj najnowszą wersję pakietu [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) narzędzia.</span><span class="sxs-lookup"><span data-stu-id="98d9b-118">Install the latest version of the [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) tool.</span></span>
* <span data-ttu-id="98d9b-119">Uruchom narzędzie i połącz się z kontem AMS.</span><span class="sxs-lookup"><span data-stu-id="98d9b-119">Launch the tool and connect to your AMS account.</span></span>

## <a name="tips"></a><span data-ttu-id="98d9b-120">Porady</span><span class="sxs-lookup"><span data-stu-id="98d9b-120">Tips</span></span>
* <span data-ttu-id="98d9b-121">Jeśli to możliwe, użyj połączenia internetowego hardwired.</span><span class="sxs-lookup"><span data-stu-id="98d9b-121">Whenever possible, use a hardwired internet connection.</span></span>
* <span data-ttu-id="98d9b-122">Regułą podczas określania wymaganiach odnośnie do przepustowości jest dwukrotnie przesyłania strumieniowego szybkości transmisji bitów.</span><span class="sxs-lookup"><span data-stu-id="98d9b-122">A good rule of thumb when determining bandwidth requirements is to double the streaming bitrates.</span></span> <span data-ttu-id="98d9b-123">Chociaż nie jest to wymagane, może pomóc zmniejszyć skuteczność przeciążenie sieci.</span><span class="sxs-lookup"><span data-stu-id="98d9b-123">While this is not a mandatory requirement, it will help mitigate the impact of network congestion.</span></span>
* <span data-ttu-id="98d9b-124">Gdy za pomocą oprogramowania na podstawie koderów, zamknij wszystkie zbędne programy.</span><span class="sxs-lookup"><span data-stu-id="98d9b-124">When using software based encoders, close out any unnecessary programs.</span></span>

## <a name="elemental-live-with-rtp-ingest"></a><span data-ttu-id="98d9b-125">Pozyskiwania stanie wolnym Live przy włączonej ochronie czasu rzeczywistego</span><span class="sxs-lookup"><span data-stu-id="98d9b-125">Elemental Live with RTP ingest</span></span>
<span data-ttu-id="98d9b-126">W tej sekcji przedstawiono sposób konfigurowania kodera na żywo stanie wolnym, który wysyła strumień na żywo o pojedynczej szybkości transmisji bitów przy użyciu protokołu RTP.</span><span class="sxs-lookup"><span data-stu-id="98d9b-126">This section shows how to configure the Elemental Live encoder that sends a single bitrate live stream over RTP.</span></span>  <span data-ttu-id="98d9b-127">Aby uzyskać więcej informacji, zobacz [strumieni MPEG-TS przy użyciu protokołu RTP](media-services-manage-live-encoder-enabled-channels.md#channel).</span><span class="sxs-lookup"><span data-stu-id="98d9b-127">For more information, see [MPEG-TS stream over RTP](media-services-manage-live-encoder-enabled-channels.md#channel).</span></span>

### <a name="create-a-channel"></a><span data-ttu-id="98d9b-128">Tworzenie kanału</span><span class="sxs-lookup"><span data-stu-id="98d9b-128">Create a channel</span></span>

1. <span data-ttu-id="98d9b-129">W przy użyciu narzędzia AMSE, przejdź do **Live** karcie, a następnie kliknij prawym przyciskiem myszy w obszarze kanału.</span><span class="sxs-lookup"><span data-stu-id="98d9b-129">In the AMSE tool, navigate to the **Live** tab, and right click within the channel area.</span></span> <span data-ttu-id="98d9b-130">Wybierz **Utwórz kanał...**</span><span class="sxs-lookup"><span data-stu-id="98d9b-130">Select **Create channel…**</span></span> <span data-ttu-id="98d9b-131">z menu.</span><span class="sxs-lookup"><span data-stu-id="98d9b-131">from the menu.</span></span>

    ![Stanie wolnym](./media/media-services-elemental-live-encoder/media-services-elemental1.png)

2. <span data-ttu-id="98d9b-133">Określ nazwę kanału pole opisu jest opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="98d9b-133">Specify a channel name, the description field is optional.</span></span> <span data-ttu-id="98d9b-134">W ustawieniach kanału, wybierz **standardowe** dla opcji Live Encoding z protokołem wprowadzania ustawioną **RTP (MPEG-TS)**.</span><span class="sxs-lookup"><span data-stu-id="98d9b-134">Under Channel Settings, select **Standard** for the Live Encoding option, with the Input Protocol set to **RTP (MPEG-TS)**.</span></span> <span data-ttu-id="98d9b-135">Możesz pozostawić wszystkie inne ustawienia, ponieważ jest.</span><span class="sxs-lookup"><span data-stu-id="98d9b-135">You can leave all other settings as is.</span></span>

    <span data-ttu-id="98d9b-136">Upewnij się, że **teraz uruchomić nowy kanał** jest zaznaczone.</span><span class="sxs-lookup"><span data-stu-id="98d9b-136">Make sure the **Start the new channel now** is selected.</span></span>

3. <span data-ttu-id="98d9b-137">Kliknij przycisk **utworzyć kanał**.</span><span class="sxs-lookup"><span data-stu-id="98d9b-137">Click **Create Channel**.</span></span>

   ![Stanie wolnym](./media/media-services-elemental-live-encoder/media-services-elemental12.png)

> [!NOTE]
> <span data-ttu-id="98d9b-139">Kanał może trwać tyle samo co 20 minut, aby rozpocząć.</span><span class="sxs-lookup"><span data-stu-id="98d9b-139">The channel can take as long as 20 minutes to start.</span></span>
>
>

<span data-ttu-id="98d9b-140">Podczas uruchamiania kanału możesz [skonfigurować koder](media-services-configure-elemental-live-encoder.md#configure_elemental_rtp).</span><span class="sxs-lookup"><span data-stu-id="98d9b-140">While the channel is starting you can [configure the encoder](media-services-configure-elemental-live-encoder.md#configure_elemental_rtp).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="98d9b-141">Należy pamiętać, że rozliczanie zaczyna się jak kanału przechodzi do stanu gotowości.</span><span class="sxs-lookup"><span data-stu-id="98d9b-141">Note that billing starts as soon as Channel goes into a ready state.</span></span> <span data-ttu-id="98d9b-142">Aby uzyskać więcej informacji, zobacz [stanów kanału](media-services-manage-live-encoder-enabled-channels.md#states).</span><span class="sxs-lookup"><span data-stu-id="98d9b-142">For more information, see [Channel's states](media-services-manage-live-encoder-enabled-channels.md#states).</span></span>
>
>

### <span data-ttu-id="98d9b-143"><a id=configure_elemental_rtp></a>Konfigurowanie kodera na żywo stanie wolnym</span><span class="sxs-lookup"><span data-stu-id="98d9b-143"><a id=configure_elemental_rtp></a>Configure the Elemental Live encoder</span></span>
<span data-ttu-id="98d9b-144">W tym samouczku są używane następujące ustawienia danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="98d9b-144">In this tutorial the following output settings are used.</span></span> <span data-ttu-id="98d9b-145">Pozostałej części tej sekcji opisano kroki konfiguracji szczegółowo.</span><span class="sxs-lookup"><span data-stu-id="98d9b-145">The rest of this section describes configuration steps in more detail.</span></span>

<span data-ttu-id="98d9b-146">**Wideo**:</span><span class="sxs-lookup"><span data-stu-id="98d9b-146">**Video**:</span></span>

* <span data-ttu-id="98d9b-147">Koder-dekoder: H.264</span><span class="sxs-lookup"><span data-stu-id="98d9b-147">Codec: H.264</span></span>
* <span data-ttu-id="98d9b-148">Profil: Wysoki (poziom 4.0)</span><span class="sxs-lookup"><span data-stu-id="98d9b-148">Profile: High (Level 4.0)</span></span>
* <span data-ttu-id="98d9b-149">Szybkość transmisji bitów: 5000 KB/s</span><span class="sxs-lookup"><span data-stu-id="98d9b-149">Bitrate: 5000 kbps</span></span>
* <span data-ttu-id="98d9b-150">Klatki kluczowej: 2 sekundy (60 sekund)</span><span class="sxs-lookup"><span data-stu-id="98d9b-150">Keyframe: 2 seconds (60 seconds)</span></span>
* <span data-ttu-id="98d9b-151">Szybkość klatek: 30</span><span class="sxs-lookup"><span data-stu-id="98d9b-151">Frame Rate: 30</span></span>

<span data-ttu-id="98d9b-152">**Audio**:</span><span class="sxs-lookup"><span data-stu-id="98d9b-152">**Audio**:</span></span>

* <span data-ttu-id="98d9b-153">Koder-dekoder: AAC (LC —)</span><span class="sxs-lookup"><span data-stu-id="98d9b-153">Codec: AAC (LC)</span></span>
* <span data-ttu-id="98d9b-154">Szybkość transmisji bitów: 192 kb/s</span><span class="sxs-lookup"><span data-stu-id="98d9b-154">Bitrate: 192 kbps</span></span>
* <span data-ttu-id="98d9b-155">Częstotliwość próbkowania: 44,1 kHz</span><span class="sxs-lookup"><span data-stu-id="98d9b-155">Sample Rate: 44.1 kHz</span></span>

#### <a name="configuration-steps"></a><span data-ttu-id="98d9b-156">Kroki konfiguracji</span><span class="sxs-lookup"><span data-stu-id="98d9b-156">Configuration steps</span></span>
1. <span data-ttu-id="98d9b-157">Przejdź do **stanie wolnym Live** sieci web interfejsu i skonfigurować kodera dla **UDP/TS** przesyłania strumieniowego.</span><span class="sxs-lookup"><span data-stu-id="98d9b-157">Navigate to the **Elemental Live** web interface, and set up the encoder for **UDP/TS** streaming.</span></span>
2. <span data-ttu-id="98d9b-158">Po utworzeniu nowego zdarzenia, przewiń w dół do grupy danych wyjściowych i Dodaj **UDP/TS** grupy wyjściowej.</span><span class="sxs-lookup"><span data-stu-id="98d9b-158">Once a new event is created, scroll down to the output groups and add the **UDP/TS** output group.</span></span>
3. <span data-ttu-id="98d9b-159">Utwórz nowe dane wyjściowe, zaznaczając **nowego strumienia** , a następnie klikając polecenie **dodać danych wyjściowych**.</span><span class="sxs-lookup"><span data-stu-id="98d9b-159">Create a new output by selecting **New Stream** and then clicking **Add Output**.</span></span>  

    ![Stanie wolnym](./media/media-services-elemental-live-encoder/media-services-elemental13.png)

   > [!NOTE]
   > <span data-ttu-id="98d9b-161">Zaleca się, że stanie wolnym zdarzenie ma kod czasowy, ustawione na "Zegara systemowego", aby pomóc koder ponownie w przypadku awarii strumienia.</span><span class="sxs-lookup"><span data-stu-id="98d9b-161">It is recommended that the Elemental event has the timecode set to "System Clock" to help the encoder reconnect in the case of a stream failure.</span></span>
   >
   >
4. <span data-ttu-id="98d9b-162">Teraz, dane wyjściowe został utworzony, kliknij przycisk **dodać strumienia**.</span><span class="sxs-lookup"><span data-stu-id="98d9b-162">Now that the Output has been created, click **Add Stream**.</span></span> <span data-ttu-id="98d9b-163">Teraz można skonfigurować ustawienia danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="98d9b-163">The output settings can now be configured.</span></span>
5. <span data-ttu-id="98d9b-164">Przewiń w dół "Strumienia 1" został utworzony, kliknij przycisk **wideo** karcie po lewej stronie, a następnie rozwiń węzeł **zaawansowane** w sekcji Ustawienia.</span><span class="sxs-lookup"><span data-stu-id="98d9b-164">Scroll down to the "Stream 1" that was just created, click the **Video** tab on the left and expand the **Advanced** settings section.</span></span>

    ![Stanie wolnym](./media/media-services-elemental-live-encoder/media-services-elemental4.png)

    <span data-ttu-id="98d9b-166">Podczas aktywnego stanie wolnym ma szeroki zakres dostosowywania dostępne, następujące ustawienia są zalecane w przypadku wprowadzenie do przesyłania strumieniowego AMS.</span><span class="sxs-lookup"><span data-stu-id="98d9b-166">While Elemental Live has a wide range of available customizing, the following settings are recommended for getting started with streaming to AMS.</span></span>

   * <span data-ttu-id="98d9b-167">Rozdzielczość: 1280 x 720</span><span class="sxs-lookup"><span data-stu-id="98d9b-167">Resolution: 1280 x 720</span></span>
   * <span data-ttu-id="98d9b-168">Szybkość klatek: 30</span><span class="sxs-lookup"><span data-stu-id="98d9b-168">Framerate: 30</span></span>
   * <span data-ttu-id="98d9b-169">Rozmiar GOP: 60 klatek</span><span class="sxs-lookup"><span data-stu-id="98d9b-169">GOP Size: 60 frames</span></span>
   * <span data-ttu-id="98d9b-170">Tryb przeplotu: progresywnego</span><span class="sxs-lookup"><span data-stu-id="98d9b-170">Interlace Mode: Progressive</span></span>
   * <span data-ttu-id="98d9b-171">Szybkość transmisji bitów: 5000000 bit/s (to może być określany na podstawie ograniczenia sieci)</span><span class="sxs-lookup"><span data-stu-id="98d9b-171">Bitrate: 5000000 bit/s (This can be adjusted based on network limitations)</span></span>

    ![Stanie wolnym](./media/media-services-elemental-live-encoder/media-services-elemental5.png)

1. <span data-ttu-id="98d9b-173">Pobierz wejściowy adres URL kanału.</span><span class="sxs-lookup"><span data-stu-id="98d9b-173">Get the channel's input URL.</span></span>

    <span data-ttu-id="98d9b-174">Przejdź z powrotem do przy użyciu narzędzia AMSE i sprawdzić stan ukończenia kanału.</span><span class="sxs-lookup"><span data-stu-id="98d9b-174">Navigate back to the AMSE tool, and check on the channel completion status.</span></span> <span data-ttu-id="98d9b-175">Gdy stan został zmieniony z **uruchamianie** do **systemem**, można uzyskać wejściowy adres URL.</span><span class="sxs-lookup"><span data-stu-id="98d9b-175">Once the State has changed from **Starting** to **Running**, you can get the input URL.</span></span>

    <span data-ttu-id="98d9b-176">Gdy kanał jest uruchomiona, kliknij prawym przyciskiem myszy nazwę kanału, przejdź do aktywowania przez **kopia danych wejściowych z adresu URL do Schowka** , a następnie wybierz **podstawowego adresu URL danych wejściowych**.</span><span class="sxs-lookup"><span data-stu-id="98d9b-176">When the channel is running, right click the channel name, navigate down to hover over **Copy Input URL to clipboard** and then select **Primary Input  URL**.</span></span>  

    ![Stanie wolnym](./media/media-services-elemental-live-encoder/media-services-elemental6.png)
2. <span data-ttu-id="98d9b-178">Wklej te informacje w **miejsce docelowe głównej** pole Elemental.</span><span class="sxs-lookup"><span data-stu-id="98d9b-178">Paste this information in the **Primary Destination** field of the Elemental.</span></span> <span data-ttu-id="98d9b-179">Wszystkie inne ustawienia mogą pozostać domyślny.</span><span class="sxs-lookup"><span data-stu-id="98d9b-179">All other settings can remain the default.</span></span>

    ![Stanie wolnym](./media/media-services-elemental-live-encoder/media-services-elemental14.png)

    <span data-ttu-id="98d9b-181">Nadmiarowości dodatkowe Powtórz te kroki dodatkowej adresu URL danych wejściowych, tworząc osobne karty "Wyjściowej" do przesyłania strumieniowego UDP/usług terminalowych.</span><span class="sxs-lookup"><span data-stu-id="98d9b-181">For extra redundancy, repeat these steps with the Secondary Input URL by creating a separate "Output" tab for UDP/TS Streaming.</span></span>
3. <span data-ttu-id="98d9b-182">Kliknij przycisk **Utwórz** (Jeśli utworzono nowe zdarzenie) lub **aktualizacji** (jeśli edycji istniejące zdarzenie), a następnie przejdź do uruchomienia kodera.</span><span class="sxs-lookup"><span data-stu-id="98d9b-182">Click **Create** (if a new event was created) or **Update** (if editing a pre-existing event) and then proceed to start the encoder.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="98d9b-183">Przed kliknięciem przycisku **Start** dla interfejsu sieci web stanie wolnym na żywo można **musi** upewnij się, że kanał jest gotowy.</span><span class="sxs-lookup"><span data-stu-id="98d9b-183">Before you click **Start** on the Elemental Live web interface, you **must** ensure that the Channel is ready.</span></span>
> <span data-ttu-id="98d9b-184">Upewnij się również, nie należy pozostawiać kanału w stanie Gotowe bez zdarzenia przez czas dłuższy niż > 15 minut.</span><span class="sxs-lookup"><span data-stu-id="98d9b-184">Also, make sure not to leave the Channel in a ready state without an event for longer than > 15 minutes.</span></span>
>
>

<span data-ttu-id="98d9b-185">Po działaniu strumienia 30 sekund, przejdź z powrotem do odtwarzania AMSE narzędzia i testowania.</span><span class="sxs-lookup"><span data-stu-id="98d9b-185">After the stream has been running for 30 seconds, navigate back to the AMSE tool and test playback.</span></span>  

### <a name="test-playback"></a><span data-ttu-id="98d9b-186">Podczas odtwarzania testu</span><span class="sxs-lookup"><span data-stu-id="98d9b-186">Test playback</span></span>

<span data-ttu-id="98d9b-187">Przejdź do przy użyciu narzędzia AMSE, a następnie kliknij prawym przyciskiem myszy kanału, który ma zostać przetestowana.</span><span class="sxs-lookup"><span data-stu-id="98d9b-187">Navigate to the AMSE tool, and right click the channel to be tested.</span></span> <span data-ttu-id="98d9b-188">Z menu, umieść kursor nad **odtwarzania podglądu** i wybierz **z usługi Azure Media Player**.</span><span class="sxs-lookup"><span data-stu-id="98d9b-188">From the menu, hover over **Playback the Preview** and select **with Azure Media Player**.</span></span>  

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental8.png)

<span data-ttu-id="98d9b-189">Strumień jest widoczna w player, następnie koder został poprawnie skonfigurowany do nawiązania połączenia usługi AMS.</span><span class="sxs-lookup"><span data-stu-id="98d9b-189">If the stream appears in the player, then the encoder has been properly configured to connect to AMS.</span></span>

<span data-ttu-id="98d9b-190">Jeśli błąd kanału należy zresetować i dostosowane ustawienia kodera.</span><span class="sxs-lookup"><span data-stu-id="98d9b-190">If an error is received, the channel will need to be reset and encoder settings adjusted.</span></span> <span data-ttu-id="98d9b-191">Zobacz [Rozwiązywanie problemów z](media-services-troubleshooting-live-streaming.md) tematu, aby uzyskać wskazówki.</span><span class="sxs-lookup"><span data-stu-id="98d9b-191">Please see the [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>   

### <a name="create-a-program"></a><span data-ttu-id="98d9b-192">Utwórz program</span><span class="sxs-lookup"><span data-stu-id="98d9b-192">Create a program</span></span>
1. <span data-ttu-id="98d9b-193">Po potwierdzeniu kanału odtwarzania, tworzenia programu.</span><span class="sxs-lookup"><span data-stu-id="98d9b-193">Once channel playback is confirmed, create a program.</span></span> <span data-ttu-id="98d9b-194">W obszarze **Live** w przy użyciu narzędzia AMSE, kliknij prawym przyciskiem myszy w obszarze program i wybierz **utworzyć nowy Program**.</span><span class="sxs-lookup"><span data-stu-id="98d9b-194">Under the **Live** tab in the AMSE tool, right click within the program area and select **Create New Program**.</span></span>  

    ![Stanie wolnym](./media/media-services-elemental-live-encoder/media-services-elemental9.png)
2. <span data-ttu-id="98d9b-196">Nazwa programu, a w razie potrzeby dostosuj **długość okna archiwum** (który domyślnie 4 godziny).</span><span class="sxs-lookup"><span data-stu-id="98d9b-196">Name the program and, if needed, adjust the **Archive Window Length** (which defaults to 4 hours).</span></span> <span data-ttu-id="98d9b-197">Można także określić miejsce przechowywania lub pozostaw domyślnie.</span><span class="sxs-lookup"><span data-stu-id="98d9b-197">You can also specify a storage location or leave as the default.</span></span>  
3. <span data-ttu-id="98d9b-198">Sprawdź **teraz uruchomić Program** pole.</span><span class="sxs-lookup"><span data-stu-id="98d9b-198">Check the **Start the Program now** box.</span></span>
4. <span data-ttu-id="98d9b-199">Kliknij przycisk **utworzyć Program**.</span><span class="sxs-lookup"><span data-stu-id="98d9b-199">Click **Create Program**.</span></span>  

    >[!NOTE]
    > <span data-ttu-id="98d9b-200">Tworzenie programu zajmuje mniej czasu niż tworzenie kanału.</span><span class="sxs-lookup"><span data-stu-id="98d9b-200">Program creation takes less time than channel creation.</span></span>   
      
5. <span data-ttu-id="98d9b-201">Po uruchomieniu programu potwierdzić odtwarzania przez kliknięcie prawym przyciskiem myszy program i przechodząc do **odtwarzania programach** , a następnie wybierając **z usługi Azure Media Player**.</span><span class="sxs-lookup"><span data-stu-id="98d9b-201">Once the program is running, confirm playback by right clicking the program and navigating to **Playback the program(s)** and then selecting **with Azure Media Player**.</span></span>  
6. <span data-ttu-id="98d9b-202">Po potwierdzeniu, kliknij prawym przyciskiem myszy program ponownie i wybierz **skopiuj dane wyjściowe adres URL do Schowka** (lub pobrać tych informacji z **programu informacji i ustawień** opcji z menu).</span><span class="sxs-lookup"><span data-stu-id="98d9b-202">Once confirmed, right click the program again and select **Copy the Output URL to Clipboard** (or retrieve this information from the **Program information and settings** option from the menu).</span></span>

<span data-ttu-id="98d9b-203">Strumień jest teraz gotowy do osadzonego w odtwarzacza lub dystrybuowane do odbiorców w celu wyświetlenia na żywo.</span><span class="sxs-lookup"><span data-stu-id="98d9b-203">The stream is now ready to be embedded in a player, or distributed to an audience for live viewing.</span></span>  

## <a name="troubleshooting"></a><span data-ttu-id="98d9b-204">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="98d9b-204">Troubleshooting</span></span>
<span data-ttu-id="98d9b-205">Zobacz [Rozwiązywanie problemów z](media-services-troubleshooting-live-streaming.md) tematu, aby uzyskać wskazówki.</span><span class="sxs-lookup"><span data-stu-id="98d9b-205">Please see the [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="98d9b-206">Ścieżki szkoleniowe dotyczące usługi Media Services</span><span class="sxs-lookup"><span data-stu-id="98d9b-206">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="98d9b-207">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="98d9b-207">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
