---
title: "Konfigurowanie kodera NewTek TriCaster wysłać strumień na żywo o pojedynczej szybkości transmisji bitów | Dokumentacja firmy Microsoft"
description: "W tym temacie przedstawiono sposób konfigurowania kodera na żywo Tricaster do wysłania do kanałów AMS, które są włączone dla kodowanie na żywo o pojedynczej szybkości transmisji."
services: media-services
documentationcenter: 
author: cenkdin
manager: cfowler
editor: 
ms.assetid: 8973181a-3059-471a-a6bb-ccda7d3ff297
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 01/05/2017
ms.author: juliako;cenkd;anilmur
ms.openlocfilehash: 42b012fb98bd0504c931ce391d63aecca8c3d311
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="use-the-newtek-tricaster-encoder-to-send-a-single-bitrate-live-stream"></a><span data-ttu-id="20d59-103">Użyj koder NewTek TriCaster, aby wysyłać strumień na żywo o pojedynczej szybkości transmisji bitów</span><span class="sxs-lookup"><span data-stu-id="20d59-103">Use the NewTek TriCaster encoder to send a single bitrate live stream</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="20d59-104">Tricaster</span><span class="sxs-lookup"><span data-stu-id="20d59-104">Tricaster</span></span>](media-services-configure-tricaster-live-encoder.md)
> * [<span data-ttu-id="20d59-105">Elemental na żywo</span><span class="sxs-lookup"><span data-stu-id="20d59-105">Elemental Live</span></span>](media-services-configure-elemental-live-encoder.md)
> * [<span data-ttu-id="20d59-106">Wirecast</span><span class="sxs-lookup"><span data-stu-id="20d59-106">Wirecast</span></span>](media-services-configure-wirecast-live-encoder.md)
> * [<span data-ttu-id="20d59-107">FMLE</span><span class="sxs-lookup"><span data-stu-id="20d59-107">FMLE</span></span>](media-services-configure-fmle-live-encoder.md)
>
>

<span data-ttu-id="20d59-108">W tym temacie przedstawiono sposób konfigurowania [NewTek TriCaster](http://newtek.com/products/tricaster-40.html) kodera na żywo do wysyłania strumienia pojedynczej szybkości transmisji bitów AMS kanałów, które są włączone kodowanie na żywo.</span><span class="sxs-lookup"><span data-stu-id="20d59-108">This topic shows how to configure the [NewTek TriCaster](http://newtek.com/products/tricaster-40.html) live encoder to send a single bitrate stream to AMS channels that are enabled for live encoding.</span></span> <span data-ttu-id="20d59-109">Aby uzyskać więcej informacji, zobacz temat [Praca z kanałami obsługującymi funkcję Live Encoding w usłudze Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).</span><span class="sxs-lookup"><span data-stu-id="20d59-109">For more information, see [Working with Channels that are Enabled to Perform Live Encoding with Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).</span></span>

<span data-ttu-id="20d59-110">W tym samouczku przedstawiono sposób zarządzania usługi Azure Media Services (AMS) za pomocą narzędzia Azure Media Services Explorer (AMSE).</span><span class="sxs-lookup"><span data-stu-id="20d59-110">This tutorial shows how to manage Azure Media Services (AMS) with Azure Media Services Explorer (AMSE) tool.</span></span> <span data-ttu-id="20d59-111">To narzędzie jest uruchamiane tylko na komputerze z systemem Windows.</span><span class="sxs-lookup"><span data-stu-id="20d59-111">This tool only runs on Windows PC.</span></span> <span data-ttu-id="20d59-112">Jeśli na Mac lub Linux, użyj portalu Azure do utworzenia [kanałów](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) i [programy](media-services-portal-creating-live-encoder-enabled-channel.md).</span><span class="sxs-lookup"><span data-stu-id="20d59-112">If you are on Mac or Linux, use the Azure portal to create [channels](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) and [programs](media-services-portal-creating-live-encoder-enabled-channel.md).</span></span>

> [!NOTE]
> <span data-ttu-id="20d59-113">Korzystając Tricaster wysyłanie wkład do kanałów AMS, które są włączone kodowanie na żywo, może istnieć błędami występującymi audio/wideo w zdarzenia na żywo w przypadku określonych funkcji Tricaster, takie jak szybka Wycinanie między źródła danych lub przełączanie z typu.</span><span class="sxs-lookup"><span data-stu-id="20d59-113">When using Tricaster for sending in a contribution feed to AMS channels that are enabled for live encoding, there can be video/audio glitches in your live event if you use certain features of Tricaster, such as rapid cutting between feeds, or switching to/from slates.</span></span> <span data-ttu-id="20d59-114">Zespołu AMS działa w rozwiązaniu tych problemów, do tego czasu, go jest nie zaleca się używania tych funkcji.</span><span class="sxs-lookup"><span data-stu-id="20d59-114">The AMS team is working on fixing these issues, until then, it is not recommend to use these features.</span></span>
>
>

## <a name="prerequisites"></a><span data-ttu-id="20d59-115">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="20d59-115">Prerequisites</span></span>
* [<span data-ttu-id="20d59-116">Tworzenie konta usługi Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="20d59-116">Create an Azure Media Services account</span></span>](media-services-portal-create-account.md)
* <span data-ttu-id="20d59-117">Upewnij się, brak punktu końcowego przesyłania strumieniowego uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="20d59-117">Ensure there is a Streaming Endpoint running.</span></span> <span data-ttu-id="20d59-118">Aby uzyskać więcej informacji, zobacz [zarządzanie punktami końcowymi przesyłania strumieniowego w konta usługi Media Services](media-services-portal-manage-streaming-endpoints.md)</span><span class="sxs-lookup"><span data-stu-id="20d59-118">For more information, see [Manage Streaming Endpoints in a Media Services Account](media-services-portal-manage-streaming-endpoints.md)</span></span>
* <span data-ttu-id="20d59-119">Zainstaluj najnowszą wersję pakietu [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) narzędzia.</span><span class="sxs-lookup"><span data-stu-id="20d59-119">Install the latest version of the [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) tool.</span></span>
* <span data-ttu-id="20d59-120">Uruchom narzędzie i połącz się z kontem AMS.</span><span class="sxs-lookup"><span data-stu-id="20d59-120">Launch the tool and connect to your AMS account.</span></span>

## <a name="tips"></a><span data-ttu-id="20d59-121">Porady</span><span class="sxs-lookup"><span data-stu-id="20d59-121">Tips</span></span>
* <span data-ttu-id="20d59-122">Jeśli to możliwe, użyj połączenia internetowego hardwired.</span><span class="sxs-lookup"><span data-stu-id="20d59-122">Whenever possible, use a hardwired internet connection.</span></span>
* <span data-ttu-id="20d59-123">Regułą podczas określania wymaganiach odnośnie do przepustowości jest dwukrotnie przesyłania strumieniowego szybkości transmisji bitów.</span><span class="sxs-lookup"><span data-stu-id="20d59-123">A good rule of thumb when determining bandwidth requirements is to double the streaming bitrates.</span></span> <span data-ttu-id="20d59-124">Chociaż nie jest to wymagane, może pomóc zmniejszyć skuteczność przeciążenie sieci.</span><span class="sxs-lookup"><span data-stu-id="20d59-124">While this is not a mandatory requirement, it will help mitigate the impact of network congestion.</span></span>
* <span data-ttu-id="20d59-125">Gdy za pomocą oprogramowania na podstawie koderów, zamknij wszystkie zbędne programy.</span><span class="sxs-lookup"><span data-stu-id="20d59-125">When using software based encoders, close out any unnecessary programs.</span></span>

## <a name="create-a-channel"></a><span data-ttu-id="20d59-126">Tworzenie kanału</span><span class="sxs-lookup"><span data-stu-id="20d59-126">Create a channel</span></span>
1. <span data-ttu-id="20d59-127">W przy użyciu narzędzia AMSE, przejdź do **Live** karcie, a następnie kliknij prawym przyciskiem myszy w obszarze kanału.</span><span class="sxs-lookup"><span data-stu-id="20d59-127">In the AMSE tool, navigate to the **Live** tab, and right click within the channel area.</span></span> <span data-ttu-id="20d59-128">Wybierz **Utwórz kanał...**</span><span class="sxs-lookup"><span data-stu-id="20d59-128">Select **Create channel…**</span></span> <span data-ttu-id="20d59-129">z menu.</span><span class="sxs-lookup"><span data-stu-id="20d59-129">from the menu.</span></span>

    ![tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster1.png)

2. <span data-ttu-id="20d59-131">Określ nazwę kanału pole opisu jest opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="20d59-131">Specify a channel name, the description field is optional.</span></span> <span data-ttu-id="20d59-132">W ustawieniach kanału, wybierz **standardowe** dla opcji Live Encoding z protokołem wprowadzania ustawioną **RTMP**.</span><span class="sxs-lookup"><span data-stu-id="20d59-132">Under Channel Settings, select **Standard** for the Live Encoding option, with the Input Protocol set to **RTMP**.</span></span> <span data-ttu-id="20d59-133">Możesz pozostawić wszystkie inne ustawienia, ponieważ jest.</span><span class="sxs-lookup"><span data-stu-id="20d59-133">You can leave all other settings as is.</span></span>

    <span data-ttu-id="20d59-134">Upewnij się, że **teraz uruchomić nowy kanał** jest zaznaczone.</span><span class="sxs-lookup"><span data-stu-id="20d59-134">Make sure the **Start the new channel now** is selected.</span></span>

3. <span data-ttu-id="20d59-135">Kliknij przycisk **utworzyć kanał**.</span><span class="sxs-lookup"><span data-stu-id="20d59-135">Click **Create Channel**.</span></span>

   ![tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster2.png)

> [!NOTE]
> <span data-ttu-id="20d59-137">Kanał może trwać tyle samo co 20 minut, aby rozpocząć.</span><span class="sxs-lookup"><span data-stu-id="20d59-137">The channel can take as long as 20 minutes to start.</span></span>
>
>

<span data-ttu-id="20d59-138">Podczas uruchamiania kanału możesz [skonfigurować koder](media-services-configure-tricaster-live-encoder.md#configure_tricaster_rtmp).</span><span class="sxs-lookup"><span data-stu-id="20d59-138">While the channel is starting you can [configure the encoder](media-services-configure-tricaster-live-encoder.md#configure_tricaster_rtmp).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="20d59-139">Należy pamiętać, że rozliczanie zaczyna się jak kanału przechodzi do stanu gotowości.</span><span class="sxs-lookup"><span data-stu-id="20d59-139">Note that billing starts as soon as Channel goes into a ready state.</span></span> <span data-ttu-id="20d59-140">Aby uzyskać więcej informacji, zobacz [stanów kanału](media-services-manage-live-encoder-enabled-channels.md#states).</span><span class="sxs-lookup"><span data-stu-id="20d59-140">For more information, see [Channel's states](media-services-manage-live-encoder-enabled-channels.md#states).</span></span>
>
>

## <span data-ttu-id="20d59-141"><a id=configure_tricaster_rtmp></a>Konfigurowanie kodera NewTek TriCaster</span><span class="sxs-lookup"><span data-stu-id="20d59-141"><a id=configure_tricaster_rtmp></a>Configure the NewTek TriCaster encoder</span></span>
<span data-ttu-id="20d59-142">W tym samouczku są używane następujące ustawienia danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="20d59-142">In this tutorial the following output settings are used.</span></span> <span data-ttu-id="20d59-143">Pozostałej części tej sekcji opisano kroki konfiguracji szczegółowo.</span><span class="sxs-lookup"><span data-stu-id="20d59-143">The rest of this section describes configuration steps in more detail.</span></span>

<span data-ttu-id="20d59-144">**Wideo**:</span><span class="sxs-lookup"><span data-stu-id="20d59-144">**Video**:</span></span>

* <span data-ttu-id="20d59-145">Koder-dekoder: H.264</span><span class="sxs-lookup"><span data-stu-id="20d59-145">Codec: H.264</span></span>
* <span data-ttu-id="20d59-146">Profil: Wysoki (poziom 4.0)</span><span class="sxs-lookup"><span data-stu-id="20d59-146">Profile: High (Level 4.0)</span></span>
* <span data-ttu-id="20d59-147">Szybkość transmisji bitów: 5000 KB/s</span><span class="sxs-lookup"><span data-stu-id="20d59-147">Bitrate: 5000 kbps</span></span>
* <span data-ttu-id="20d59-148">Klatki kluczowej: 2 sekundy (60 sekund)</span><span class="sxs-lookup"><span data-stu-id="20d59-148">Keyframe: 2 seconds (60 seconds)</span></span>
* <span data-ttu-id="20d59-149">Szybkość klatek: 30</span><span class="sxs-lookup"><span data-stu-id="20d59-149">Frame Rate: 30</span></span>

<span data-ttu-id="20d59-150">**Audio**:</span><span class="sxs-lookup"><span data-stu-id="20d59-150">**Audio**:</span></span>

* <span data-ttu-id="20d59-151">Koder-dekoder: AAC (LC —)</span><span class="sxs-lookup"><span data-stu-id="20d59-151">Codec: AAC (LC)</span></span>
* <span data-ttu-id="20d59-152">Szybkość transmisji bitów: 192 kb/s</span><span class="sxs-lookup"><span data-stu-id="20d59-152">Bitrate: 192 kbps</span></span>
* <span data-ttu-id="20d59-153">Częstotliwość próbkowania: 44,1 kHz</span><span class="sxs-lookup"><span data-stu-id="20d59-153">Sample Rate: 44.1 kHz</span></span>

### <a name="configuration-steps"></a><span data-ttu-id="20d59-154">Kroki konfiguracji</span><span class="sxs-lookup"><span data-stu-id="20d59-154">Configuration steps</span></span>
1. <span data-ttu-id="20d59-155">Utwórz nową **NewTek TriCaster** projektu w zależności od tego, jakie wideo źródło danych wejściowych jest używany.</span><span class="sxs-lookup"><span data-stu-id="20d59-155">Create a new **NewTek TriCaster** project depending on what video input source is being used.</span></span>
2. <span data-ttu-id="20d59-156">Raz w ramach tego projektu należy znaleźć **strumienia** przycisk, a następnie kliknij koło zębate ikonę obok niej dostęp do menu konfiguracji strumienia.</span><span class="sxs-lookup"><span data-stu-id="20d59-156">Once within that project, find the **Stream** button, and click the gear icon next to it to access the stream configuration menu.</span></span>

    ![tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster3.png)
3. <span data-ttu-id="20d59-158">Po otwarciu menu, kliknij przycisk **nowy** pozycji połączenia.</span><span class="sxs-lookup"><span data-stu-id="20d59-158">Once the menu has opened, click **New** under the Connection heading.</span></span> <span data-ttu-id="20d59-159">Po wyświetleniu monitu dla typu połączenia, wybierz **Adobe Flash**.</span><span class="sxs-lookup"><span data-stu-id="20d59-159">When prompted for the connection type, select **Adobe Flash**.</span></span>

    ![tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster4.png)
4. <span data-ttu-id="20d59-161">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="20d59-161">Click **OK**.</span></span>
5. <span data-ttu-id="20d59-162">Teraz można zaimportować profil FMLE, klikając strzałkę listy rozwijanej w obszarze **przesyłania strumieniowego profilu** i przechodząc do **Przeglądaj**.</span><span class="sxs-lookup"><span data-stu-id="20d59-162">An FMLE profile can now be imported by clicking the drop down arrow under **Streaming Profile** and navigating to **Browse**.</span></span>

    ![tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster5.png)
6. <span data-ttu-id="20d59-164">Przejdź do gdzie skonfigurowanego profilu FMLE został zapisany.</span><span class="sxs-lookup"><span data-stu-id="20d59-164">Navigate to where the configured FMLE profile was saved.</span></span>
7. <span data-ttu-id="20d59-165">Wybierz go, a następnie naciśnij klawisz **OK**.</span><span class="sxs-lookup"><span data-stu-id="20d59-165">Select it, and press **OK**.</span></span>

    <span data-ttu-id="20d59-166">Po przekazaniu profilu, przejdź do następnego kroku.</span><span class="sxs-lookup"><span data-stu-id="20d59-166">Once the profile is uploaded, proceed to the next step.</span></span>
8. <span data-ttu-id="20d59-167">Get kanału wejściowych adres URL, aby przypisać Tricaster **punktu końcowego protokołu RTMP**.</span><span class="sxs-lookup"><span data-stu-id="20d59-167">Get the channel's input URL in order to assign it to the Tricaster **RTMP Endpoint**.</span></span>

    <span data-ttu-id="20d59-168">Przejdź z powrotem do przy użyciu narzędzia AMSE i sprawdzić stan ukończenia kanału.</span><span class="sxs-lookup"><span data-stu-id="20d59-168">Navigate back to the AMSE tool, and check on the channel completion status.</span></span> <span data-ttu-id="20d59-169">Gdy stan został zmieniony z **uruchamianie** do **systemem**, można uzyskać wejściowy adres URL.</span><span class="sxs-lookup"><span data-stu-id="20d59-169">Once the State has changed from **Starting** to **Running**, you can get the input URL.</span></span>

    <span data-ttu-id="20d59-170">Gdy kanał jest uruchomiona, kliknij prawym przyciskiem myszy nazwę kanału, przejdź do aktywowania przez **kopia danych wejściowych z adresu URL do Schowka** , a następnie wybierz **podstawowego adresu URL danych wejściowych**.</span><span class="sxs-lookup"><span data-stu-id="20d59-170">When the channel is running, right click the channel name, navigate down to hover over **Copy Input URL to clipboard** and then select **Primary Input  URL**.</span></span>  

    ![tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster6.png)
9. <span data-ttu-id="20d59-172">Wklej te informacje w **lokalizacji** pole w obszarze **Flash Server** w projekcie Tricaster.</span><span class="sxs-lookup"><span data-stu-id="20d59-172">Paste this information in the **Location** field under **Flash Server** within the Tricaster project.</span></span> <span data-ttu-id="20d59-173">Również przypisać nazwę strumienia w **Identyfikator strumienia** pola.</span><span class="sxs-lookup"><span data-stu-id="20d59-173">Also assign a stream name in the **Stream ID** field.</span></span>

    <span data-ttu-id="20d59-174">Jeśli informacje strumień został dodany do profilu FMLE, jego można również zaimportować do tej sekcji, klikając **importowanie ustawień**, przechodząc do zapisanego profilu FMLE i klikając pozycję **OK**.</span><span class="sxs-lookup"><span data-stu-id="20d59-174">If stream information was added to the FMLE profile, it can also be imported to this section by clicking **Import Settings**, navigating to the saved FMLE profile and clicking **OK**.</span></span> <span data-ttu-id="20d59-175">Odpowiednie pola Flash serwera należy wypełnić o informacje z FMLE.</span><span class="sxs-lookup"><span data-stu-id="20d59-175">The relevant Flash Server fields should populate with the information from FMLE.</span></span>

    ![tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster7.png)
10. <span data-ttu-id="20d59-177">Gdy skończysz, kliknij przycisk **OK** w dolnej części ekranu.</span><span class="sxs-lookup"><span data-stu-id="20d59-177">When finished, click **OK** at the bottom of the screen.</span></span> <span data-ttu-id="20d59-178">Po zakończeniu dane wejściowe audio i wideo w Tricaster rozpoczęcia przesyłania strumieniowego AMS, klikając **strumienia** przycisku.</span><span class="sxs-lookup"><span data-stu-id="20d59-178">When video and audio inputs into the Tricaster are ready, begin streaming to AMS by clicking the **Stream** button.</span></span>

     ![tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster11.png)

> [!IMPORTANT]
> <span data-ttu-id="20d59-180">Przed kliknięciem przycisku **strumienia**, możesz **musi** upewnij się, że kanał jest gotowy.</span><span class="sxs-lookup"><span data-stu-id="20d59-180">Before you click **Stream**, you **must** ensure that the Channel is ready.</span></span>
> <span data-ttu-id="20d59-181">Upewnij się również, nie należy pozostawiać kanału w stanie Gotowe bez wprowadzania wkład źródła danych przez czas dłuższy niż > 15 minut.</span><span class="sxs-lookup"><span data-stu-id="20d59-181">Also, make sure not to leave the Channel in a ready state without an input contribution feed for longer than > 15 minutes.</span></span>
>
>

## <a name="test-playback"></a><span data-ttu-id="20d59-182">Podczas odtwarzania testu</span><span class="sxs-lookup"><span data-stu-id="20d59-182">Test playback</span></span>
<span data-ttu-id="20d59-183">Przejdź do przy użyciu narzędzia AMSE, a następnie kliknij prawym przyciskiem myszy kanału, który ma zostać przetestowana.</span><span class="sxs-lookup"><span data-stu-id="20d59-183">Navigate to the AMSE tool, and right click the channel to be tested.</span></span> <span data-ttu-id="20d59-184">Z menu, umieść kursor nad **odtwarzania podglądu** i wybierz **z usługi Azure Media Player**.</span><span class="sxs-lookup"><span data-stu-id="20d59-184">From the menu, hover over **Playback the Preview** and select **with Azure Media Player**.</span></span>  

    ![tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster8.png)

<span data-ttu-id="20d59-185">Strumień jest widoczna w player, następnie koder został poprawnie skonfigurowany do nawiązania połączenia usługi AMS.</span><span class="sxs-lookup"><span data-stu-id="20d59-185">If the stream appears in the player, then the encoder has been properly configured to connect to AMS.</span></span>

<span data-ttu-id="20d59-186">Jeśli błąd kanału należy zresetować i dostosowane ustawienia kodera.</span><span class="sxs-lookup"><span data-stu-id="20d59-186">If an error is received, the channel will need to be reset and encoder settings adjusted.</span></span> <span data-ttu-id="20d59-187">Zobacz [Rozwiązywanie problemów z](media-services-troubleshooting-live-streaming.md) tematu, aby uzyskać wskazówki.</span><span class="sxs-lookup"><span data-stu-id="20d59-187">Please see the [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>  

## <a name="create-a-program"></a><span data-ttu-id="20d59-188">Utwórz program</span><span class="sxs-lookup"><span data-stu-id="20d59-188">Create a program</span></span>
1. <span data-ttu-id="20d59-189">Po potwierdzeniu kanału odtwarzania, tworzenia programu.</span><span class="sxs-lookup"><span data-stu-id="20d59-189">Once channel playback is confirmed, create a program.</span></span> <span data-ttu-id="20d59-190">W obszarze **Live** w przy użyciu narzędzia AMSE, kliknij prawym przyciskiem myszy w obszarze program i wybierz **utworzyć nowy Program**.</span><span class="sxs-lookup"><span data-stu-id="20d59-190">Under the **Live** tab in the AMSE tool, right click within the program area and select **Create New Program**.</span></span>  

    ![tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster9.png)
2. <span data-ttu-id="20d59-192">Nazwa programu, a w razie potrzeby dostosuj **długość okna archiwum** (który domyślnie 4 godziny).</span><span class="sxs-lookup"><span data-stu-id="20d59-192">Name the program and, if needed, adjust the **Archive Window Length** (which defaults to 4 hours).</span></span> <span data-ttu-id="20d59-193">Można także określić miejsce przechowywania lub pozostaw domyślnie.</span><span class="sxs-lookup"><span data-stu-id="20d59-193">You can also specify a storage location or leave as the default.</span></span>  
3. <span data-ttu-id="20d59-194">Sprawdź **teraz uruchomić Program** pole.</span><span class="sxs-lookup"><span data-stu-id="20d59-194">Check the **Start the Program now** box.</span></span>
4. <span data-ttu-id="20d59-195">Kliknij przycisk **utworzyć Program**.</span><span class="sxs-lookup"><span data-stu-id="20d59-195">Click **Create Program**.</span></span>  

    >[!NOTE]
    ><span data-ttu-id="20d59-196">Tworzenie programu zajmuje mniej czasu niż tworzenie kanału.</span><span class="sxs-lookup"><span data-stu-id="20d59-196">Program creation takes less time than channel creation.</span></span>
        
5. <span data-ttu-id="20d59-197">Po uruchomieniu programu potwierdzić odtwarzania przez kliknięcie prawym przyciskiem myszy program i przechodząc do **odtwarzania programach** , a następnie wybierając **z usługi Azure Media Player**.</span><span class="sxs-lookup"><span data-stu-id="20d59-197">Once the program is running, confirm playback by right clicking the program and navigating to **Playback the program(s)** and then selecting **with Azure Media Player**.</span></span>  
6. <span data-ttu-id="20d59-198">Po potwierdzeniu, kliknij prawym przyciskiem myszy program ponownie i wybierz **skopiuj dane wyjściowe adres URL do Schowka** (lub pobrać tych informacji z **programu informacji i ustawień** opcji z menu).</span><span class="sxs-lookup"><span data-stu-id="20d59-198">Once confirmed, right click the program again and select **Copy the Output URL to Clipboard** (or retrieve this information from the **Program information and settings** option from the menu).</span></span>

<span data-ttu-id="20d59-199">Strumień jest teraz gotowy do osadzonego w odtwarzacza lub dystrybuowane do odbiorców w celu wyświetlenia na żywo.</span><span class="sxs-lookup"><span data-stu-id="20d59-199">The stream is now ready to be embedded in a player, or distributed to an audience for live viewing.</span></span>  

## <a name="troubleshooting"></a><span data-ttu-id="20d59-200">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="20d59-200">Troubleshooting</span></span>
<span data-ttu-id="20d59-201">Zobacz [Rozwiązywanie problemów z](media-services-troubleshooting-live-streaming.md) tematu, aby uzyskać wskazówki.</span><span class="sxs-lookup"><span data-stu-id="20d59-201">Please see the [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>

## <a name="next-step"></a><span data-ttu-id="20d59-202">Następny krok</span><span class="sxs-lookup"><span data-stu-id="20d59-202">Next step</span></span>
<span data-ttu-id="20d59-203">Przejrzyj ścieżki szkoleniowe dotyczące usługi Media Services.</span><span class="sxs-lookup"><span data-stu-id="20d59-203">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="20d59-204">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="20d59-204">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
