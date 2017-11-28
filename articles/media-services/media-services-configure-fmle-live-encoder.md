---
title: "aaaConfigure hello toosend koder FMLE strumień na żywo o pojedynczej szybkości transmisji bitów | Dokumentacja firmy Microsoft"
description: "W tym temacie przedstawiono sposób tooconfigure hello interfejsu Flash Media na żywo kodera (FMLE) koder toosend kanałami tooAMS strumienia pojedynczej szybkości transmisji bitów, obsługującymi kodowanie na żywo."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 3113f333-517a-47a1-a1b3-57e200c6b2a2
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 01/05/2017
ms.author: juliako;cenkdin;anilmur
ms.openlocfilehash: 780d911c5186ec09c784264f9a0d0c3f8059d305
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-fmle-encoder-toosend-a-single-bitrate-live-stream"></a><span data-ttu-id="fd76e-103">Użyj hello FMLE koder toosend strumień na żywo o pojedynczej szybkości transmisji bitów</span><span class="sxs-lookup"><span data-stu-id="fd76e-103">Use hello FMLE encoder toosend a single bitrate live stream</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="fd76e-104">FMLE</span><span class="sxs-lookup"><span data-stu-id="fd76e-104">FMLE</span></span>](media-services-configure-fmle-live-encoder.md)
> * [<span data-ttu-id="fd76e-105">Elemental na żywo</span><span class="sxs-lookup"><span data-stu-id="fd76e-105">Elemental Live</span></span>](media-services-configure-elemental-live-encoder.md)
> * [<span data-ttu-id="fd76e-106">Tricaster</span><span class="sxs-lookup"><span data-stu-id="fd76e-106">Tricaster</span></span>](media-services-configure-tricaster-live-encoder.md)
> * [<span data-ttu-id="fd76e-107">Wirecast</span><span class="sxs-lookup"><span data-stu-id="fd76e-107">Wirecast</span></span>](media-services-configure-wirecast-live-encoder.md)
>
>

<span data-ttu-id="fd76e-108">W tym temacie przedstawiono sposób tooconfigure hello [Flash Media Live Encoder](http://www.adobe.com/products/flash-media-encoder.html) toosend kodera (FMLE) tooAMS kanałów, które są włączone kodowanie na żywo strumienia pojedynczej szybkości transmisji bitów.</span><span class="sxs-lookup"><span data-stu-id="fd76e-108">This topic shows how tooconfigure hello [Flash Media Live Encoder](http://www.adobe.com/products/flash-media-encoder.html) (FMLE) encoder toosend a single bitrate stream tooAMS channels that are enabled for live encoding.</span></span> <span data-ttu-id="fd76e-109">Aby uzyskać więcej informacji, zobacz [Praca z kanałami, że włączono tooPerform Live kodowania za pomocą usługi Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).</span><span class="sxs-lookup"><span data-stu-id="fd76e-109">For more information, see [Working with Channels that are Enabled tooPerform Live Encoding with Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).</span></span>

<span data-ttu-id="fd76e-110">Ten samouczek pokazuje, jak toomanage usługi Azure Media Services (AMS) za pomocą narzędzia Azure Media Services Explorer (AMSE).</span><span class="sxs-lookup"><span data-stu-id="fd76e-110">This tutorial shows how toomanage Azure Media Services (AMS) with Azure Media Services Explorer (AMSE) tool.</span></span> <span data-ttu-id="fd76e-111">To narzędzie jest uruchamiane tylko na komputerze z systemem Windows.</span><span class="sxs-lookup"><span data-stu-id="fd76e-111">This tool only runs on Windows PC.</span></span> <span data-ttu-id="fd76e-112">Mac lub Linux, za pomocą hello Azure portalu toocreate [kanałów](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) i [programy](media-services-portal-creating-live-encoder-enabled-channel.md).</span><span class="sxs-lookup"><span data-stu-id="fd76e-112">If you are on Mac or Linux, use hello Azure portal toocreate [channels](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) and [programs](media-services-portal-creating-live-encoder-enabled-channel.md).</span></span>

<span data-ttu-id="fd76e-113">Należy pamiętać, że w tym samouczku opisano przy użyciu AAC.</span><span class="sxs-lookup"><span data-stu-id="fd76e-113">Note that this tutorial describes using AAC.</span></span> <span data-ttu-id="fd76e-114">FMLE nie obsługuje jednak AAC domyślnie.</span><span class="sxs-lookup"><span data-stu-id="fd76e-114">However, FMLE doesn’t supports AAC by default.</span></span> <span data-ttu-id="fd76e-115">Będzie potrzebny toopurchase wtyczki do kodowania AAC przykład MainConcept: [AAC wtyczki](http://www.mainconcept.com/products/plug-ins/plug-ins-for-adobe/aac-encoder-fmle.html)</span><span class="sxs-lookup"><span data-stu-id="fd76e-115">You would need toopurchase a plugin for AAC encoding such as from MainConcept: [AAC plugin](http://www.mainconcept.com/products/plug-ins/plug-ins-for-adobe/aac-encoder-fmle.html)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fd76e-116">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="fd76e-116">Prerequisites</span></span>
* [<span data-ttu-id="fd76e-117">Tworzenie konta usługi Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="fd76e-117">Create an Azure Media Services account</span></span>](media-services-portal-create-account.md)
* <span data-ttu-id="fd76e-118">Upewnij się, brak punktu końcowego przesyłania strumieniowego uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="fd76e-118">Ensure there is a Streaming Endpoint running.</span></span> <span data-ttu-id="fd76e-119">Aby uzyskać więcej informacji, zobacz [zarządzanie punktami końcowymi przesyłania strumieniowego w konta usługi Media Services](media-services-portal-manage-streaming-endpoints.md)</span><span class="sxs-lookup"><span data-stu-id="fd76e-119">For more information, see [Manage Streaming Endpoints in a Media Services Account](media-services-portal-manage-streaming-endpoints.md)</span></span>
* <span data-ttu-id="fd76e-120">Zainstaluj najnowszą wersję hello hello [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) narzędzia.</span><span class="sxs-lookup"><span data-stu-id="fd76e-120">Install hello latest version of hello [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) tool.</span></span>
* <span data-ttu-id="fd76e-121">Uruchom narzędzie hello i Połącz konto tooyour AMS.</span><span class="sxs-lookup"><span data-stu-id="fd76e-121">Launch hello tool and connect tooyour AMS account.</span></span>

## <a name="tips"></a><span data-ttu-id="fd76e-122">Porady</span><span class="sxs-lookup"><span data-stu-id="fd76e-122">Tips</span></span>
* <span data-ttu-id="fd76e-123">Jeśli to możliwe, użyj połączenia internetowego hardwired.</span><span class="sxs-lookup"><span data-stu-id="fd76e-123">Whenever possible, use a hardwired internet connection.</span></span>
* <span data-ttu-id="fd76e-124">Regułą podczas określania wymaganiach odnośnie do przepustowości jest hello toodouble przesyłania strumieniowego szybkości transmisji bitów.</span><span class="sxs-lookup"><span data-stu-id="fd76e-124">A good rule of thumb when determining bandwidth requirements is toodouble hello streaming bitrates.</span></span> <span data-ttu-id="fd76e-125">Chociaż nie jest to wymagane, może pomóc zmniejszyć wpływ hello sieci przeciążona.</span><span class="sxs-lookup"><span data-stu-id="fd76e-125">While this is not a mandatory requirement, it will help mitigate hello impact of network congestion.</span></span>
* <span data-ttu-id="fd76e-126">Gdy za pomocą oprogramowania na podstawie koderów, zamknij wszystkie zbędne programy.</span><span class="sxs-lookup"><span data-stu-id="fd76e-126">When using software based encoders, close out any unnecessary programs.</span></span>

## <a name="create-a-channel"></a><span data-ttu-id="fd76e-127">Tworzenie kanału</span><span class="sxs-lookup"><span data-stu-id="fd76e-127">Create a channel</span></span>
1. <span data-ttu-id="fd76e-128">Narzędzie AMSE hello Przejdź toohello **Live** karcie, a następnie kliknij prawym przyciskiem myszy w obszarze kanału hello.</span><span class="sxs-lookup"><span data-stu-id="fd76e-128">In hello AMSE tool, navigate toohello **Live** tab, and right click within hello channel area.</span></span> <span data-ttu-id="fd76e-129">Wybierz **Utwórz kanał...**</span><span class="sxs-lookup"><span data-stu-id="fd76e-129">Select **Create channel…**</span></span> <span data-ttu-id="fd76e-130">z hello menu.</span><span class="sxs-lookup"><span data-stu-id="fd76e-130">from hello menu.</span></span>

    ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle1.png)

2. <span data-ttu-id="fd76e-132">Określ nazwę kanału hello pole opisu jest opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="fd76e-132">Specify a channel name, hello description field is optional.</span></span> <span data-ttu-id="fd76e-133">W ustawieniach kanału, wybierz **standardowe** dla hello opcji kodowanie na żywo z hello wprowadzania ustawiony protokół zbyt**RTMP**.</span><span class="sxs-lookup"><span data-stu-id="fd76e-133">Under Channel Settings, select **Standard** for hello Live Encoding option, with hello Input Protocol set too**RTMP**.</span></span> <span data-ttu-id="fd76e-134">Możesz pozostawić wszystkie inne ustawienia, ponieważ jest.</span><span class="sxs-lookup"><span data-stu-id="fd76e-134">You can leave all other settings as is.</span></span>

    <span data-ttu-id="fd76e-135">Upewnij się, że hello **Start hello nowy kanał teraz** jest zaznaczone.</span><span class="sxs-lookup"><span data-stu-id="fd76e-135">Make sure hello **Start hello new channel now** is selected.</span></span>

3. <span data-ttu-id="fd76e-136">Kliknij przycisk **utworzyć kanał**.</span><span class="sxs-lookup"><span data-stu-id="fd76e-136">Click **Create Channel**.</span></span>

   ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle2.png)

> [!NOTE]
> <span data-ttu-id="fd76e-138">kanał Hello może zająć toostart 20 minut.</span><span class="sxs-lookup"><span data-stu-id="fd76e-138">hello channel can take as long as 20 minutes toostart.</span></span>
>
>

<span data-ttu-id="fd76e-139">Podczas uruchamiania kanału hello można [skonfigurować koder hello](media-services-configure-fmle-live-encoder.md#configure_fmle_rtmp).</span><span class="sxs-lookup"><span data-stu-id="fd76e-139">While hello channel is starting you can [configure hello encoder](media-services-configure-fmle-live-encoder.md#configure_fmle_rtmp).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fd76e-140">Należy pamiętać, że rozliczanie zaczyna się jak kanału przechodzi do stanu gotowości.</span><span class="sxs-lookup"><span data-stu-id="fd76e-140">Note that billing starts as soon as Channel goes into a ready state.</span></span> <span data-ttu-id="fd76e-141">Aby uzyskać więcej informacji, zobacz [stanów kanału](media-services-manage-live-encoder-enabled-channels.md#states).</span><span class="sxs-lookup"><span data-stu-id="fd76e-141">For more information, see [Channel's states](media-services-manage-live-encoder-enabled-channels.md#states).</span></span>
>
>

## <span data-ttu-id="fd76e-142"><a id=configure_fmle_rtmp></a>Skonfiguruj hello FMLE kodera</span><span class="sxs-lookup"><span data-stu-id="fd76e-142"><a id=configure_fmle_rtmp></a>Configure hello FMLE encoder</span></span>
<span data-ttu-id="fd76e-143">W tym samouczek hello są używane następujące ustawienia danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="fd76e-143">In this tutorial hello following output settings are used.</span></span> <span data-ttu-id="fd76e-144">Hello pozostałej części tej sekcji opisano kroki konfiguracji szczegółowo.</span><span class="sxs-lookup"><span data-stu-id="fd76e-144">hello rest of this section describes configuration steps in more detail.</span></span>

<span data-ttu-id="fd76e-145">**Wideo**:</span><span class="sxs-lookup"><span data-stu-id="fd76e-145">**Video**:</span></span>

* <span data-ttu-id="fd76e-146">Koder-dekoder: H.264</span><span class="sxs-lookup"><span data-stu-id="fd76e-146">Codec: H.264</span></span>
* <span data-ttu-id="fd76e-147">Profil: Wysoki (poziom 4.0)</span><span class="sxs-lookup"><span data-stu-id="fd76e-147">Profile: High (Level 4.0)</span></span>
* <span data-ttu-id="fd76e-148">Szybkość transmisji bitów: 5000 KB/s</span><span class="sxs-lookup"><span data-stu-id="fd76e-148">Bitrate: 5000 kbps</span></span>
* <span data-ttu-id="fd76e-149">Klatki kluczowej: 2 sekundy (60 sekund)</span><span class="sxs-lookup"><span data-stu-id="fd76e-149">Keyframe: 2 seconds (60 seconds)</span></span>
* <span data-ttu-id="fd76e-150">Szybkość klatek: 30</span><span class="sxs-lookup"><span data-stu-id="fd76e-150">Frame Rate: 30</span></span>

<span data-ttu-id="fd76e-151">**Audio**:</span><span class="sxs-lookup"><span data-stu-id="fd76e-151">**Audio**:</span></span>

* <span data-ttu-id="fd76e-152">Koder-dekoder: AAC (LC —)</span><span class="sxs-lookup"><span data-stu-id="fd76e-152">Codec: AAC (LC)</span></span>
* <span data-ttu-id="fd76e-153">Szybkość transmisji bitów: 192 kb/s</span><span class="sxs-lookup"><span data-stu-id="fd76e-153">Bitrate: 192 kbps</span></span>
* <span data-ttu-id="fd76e-154">Częstotliwość próbkowania: 44,1 kHz</span><span class="sxs-lookup"><span data-stu-id="fd76e-154">Sample Rate: 44.1 kHz</span></span>

### <a name="configuration-steps"></a><span data-ttu-id="fd76e-155">Kroki konfiguracji</span><span class="sxs-lookup"><span data-stu-id="fd76e-155">Configuration steps</span></span>
1. <span data-ttu-id="fd76e-156">Przejdź toohello, który interfejs Flash Media na żywo kodera (FMLE) na maszynie hello jest używany.</span><span class="sxs-lookup"><span data-stu-id="fd76e-156">Navigate toohello Flash Media Live Encoder’s (FMLE) interface on hello machine being used.</span></span>

    <span data-ttu-id="fd76e-157">Interfejs Hello jest jednej strony głównej ustawień.</span><span class="sxs-lookup"><span data-stu-id="fd76e-157">hello interface is one main page of settings.</span></span> <span data-ttu-id="fd76e-158">Poświęć należy wziąć pod uwagę następujące hello zalecane ustawienia tooget wprowadzenie do przesyłania strumieniowego przy użyciu FMLE.</span><span class="sxs-lookup"><span data-stu-id="fd76e-158">Please take note of hello following recommended settings tooget started with streaming using FMLE.</span></span>

   * <span data-ttu-id="fd76e-159">Format: Szybkość klatek H.264: 30,00</span><span class="sxs-lookup"><span data-stu-id="fd76e-159">Format: H.264 Frame Rate: 30.00</span></span>
   * <span data-ttu-id="fd76e-160">Rozmiar wejściowe: 1280 x 720</span><span class="sxs-lookup"><span data-stu-id="fd76e-160">Input Size: 1280 x 720</span></span>
   * <span data-ttu-id="fd76e-161">Szybkość transmisji bitów: 5000 KB/s (może być określany na podstawie ograniczenia sieci)</span><span class="sxs-lookup"><span data-stu-id="fd76e-161">Bit Rate: 5000 Kbps (Can be adjusted based on network limitations)</span></span>  

     ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle3.png)

     <span data-ttu-id="fd76e-163">Przy użyciu naprzemiennych źródeł, skontaktuj się z hello znacznikiem wyboru opcji "Opcji Usuń przeplot"</span><span class="sxs-lookup"><span data-stu-id="fd76e-163">When using interlaced sources, please checkmark hello “Deinterlace” option</span></span>
2. <span data-ttu-id="fd76e-164">Klucz hello wybierz ikonę tooFormat dalej, te dodatkowe ustawienia powinny być:</span><span class="sxs-lookup"><span data-stu-id="fd76e-164">Select hello wrench icon next tooFormat, these additional settings should be:</span></span>

   * <span data-ttu-id="fd76e-165">Profil: Main</span><span class="sxs-lookup"><span data-stu-id="fd76e-165">Profile: Main</span></span>
   * <span data-ttu-id="fd76e-166">Poziom: 4.0</span><span class="sxs-lookup"><span data-stu-id="fd76e-166">Level: 4.0</span></span>
   * <span data-ttu-id="fd76e-167">Częstotliwość klatki kluczowej: 2 sekundy.</span><span class="sxs-lookup"><span data-stu-id="fd76e-167">Keyframe Frequency: 2 seconds</span></span>

     ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle4.png)
3. <span data-ttu-id="fd76e-169">Ustaw następujące istotne ustawienia audio hello:</span><span class="sxs-lookup"><span data-stu-id="fd76e-169">Set hello following important audio setting:</span></span>

   * <span data-ttu-id="fd76e-170">Format: AAC</span><span class="sxs-lookup"><span data-stu-id="fd76e-170">Format: AAC</span></span>
   * <span data-ttu-id="fd76e-171">Częstotliwość próbkowania: Hz 44100 b</span><span class="sxs-lookup"><span data-stu-id="fd76e-171">Sample Rate: 44100 Hz</span></span>
   * <span data-ttu-id="fd76e-172">Szybkość transmisji bitów: 192 kb/s</span><span class="sxs-lookup"><span data-stu-id="fd76e-172">Bitrate: 192 Kbps</span></span>

     ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle5.png)
4. <span data-ttu-id="fd76e-174">Pobierz hello kanał wejściowy adres URL w kolejności tooassign on toohello FMLE **punktu końcowego protokołu RTMP**.</span><span class="sxs-lookup"><span data-stu-id="fd76e-174">Get hello channel's input URL in order tooassign it toohello FMLE's **RTMP Endpoint**.</span></span>

    <span data-ttu-id="fd76e-175">Przejdź wstecz toohello narzędzie AMSE i sprawdzić stan ukończenia hello kanału.</span><span class="sxs-lookup"><span data-stu-id="fd76e-175">Navigate back toohello AMSE tool, and check on hello channel completion status.</span></span> <span data-ttu-id="fd76e-176">Po hello stan został zmieniony z **uruchamianie** za**systemem**, możesz uzyskać hello wejściowy adres URL.</span><span class="sxs-lookup"><span data-stu-id="fd76e-176">Once hello State has changed from **Starting** too**Running**, you can get hello input URL.</span></span>

    <span data-ttu-id="fd76e-177">Gdy kanał hello jest uruchomiona, kliknij prawym przyciskiem myszy nazwę kanału hello, przechodzenia toohover za pośrednictwem **tooclipboard kopia danych wejściowych URL** , a następnie wybierz **podstawowego adresu URL danych wejściowych**.</span><span class="sxs-lookup"><span data-stu-id="fd76e-177">When hello channel is running, right click hello channel name, navigate down toohover over **Copy Input URL tooclipboard** and then select **Primary Input  URL**.</span></span>  

    ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle6.png)
5. <span data-ttu-id="fd76e-179">Wklej te informacje w hello **FMS URL** pole hello dane wyjściowe sekcji, a następnie przypisz nazwę strumienia.</span><span class="sxs-lookup"><span data-stu-id="fd76e-179">Paste this information in hello **FMS URL** field of hello output section, and assign a stream name.</span></span>

    ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle7.png)

    <span data-ttu-id="fd76e-181">Dodatkowe nadmiarowości Powtórz te czynności z hello dodatkowej wprowadzania adresu URL.</span><span class="sxs-lookup"><span data-stu-id="fd76e-181">For extra redundancy, repeat these steps with hello Secondary Input URL.</span></span>
6. <span data-ttu-id="fd76e-182">Wybierz przycisk **Połącz**.</span><span class="sxs-lookup"><span data-stu-id="fd76e-182">Select **Connect**.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fd76e-183">Przed kliknięciem przycisku **Connect**, możesz **musi** upewnij się, że kanał hello jest gotowy.</span><span class="sxs-lookup"><span data-stu-id="fd76e-183">Before you click **Connect**, you **must** ensure that hello Channel is ready.</span></span>
> <span data-ttu-id="fd76e-184">Sprawdź także, czy nie tooleave hello kanału w stanie Gotowe bez wprowadzania wkład źródła danych przez czas dłuższy niż > 15 minut.</span><span class="sxs-lookup"><span data-stu-id="fd76e-184">Also, make sure not tooleave hello Channel in a ready state without an input contribution feed for longer than > 15 minutes.</span></span>
>
>

## <a name="test-playback"></a><span data-ttu-id="fd76e-185">Podczas odtwarzania testu</span><span class="sxs-lookup"><span data-stu-id="fd76e-185">Test playback</span></span>

<span data-ttu-id="fd76e-186">Przejdź narzędzie AMSE toohello, a następnie kliknij prawym przyciskiem myszy toobe kanału hello przetestowane.</span><span class="sxs-lookup"><span data-stu-id="fd76e-186">Navigate toohello AMSE tool, and right click hello channel toobe tested.</span></span> <span data-ttu-id="fd76e-187">Z hello menu, umieść kursor nad **hello odtwarzania podglądu** i wybierz **z usługi Azure Media Player**.</span><span class="sxs-lookup"><span data-stu-id="fd76e-187">From hello menu, hover over **Playback hello Preview** and select **with Azure Media Player**.</span></span>  

    ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle8.png)

<span data-ttu-id="fd76e-188">Czy strumienia hello znajduje się w hello player, koder hello został tooAMS tooconnect poprawnie skonfigurowana.</span><span class="sxs-lookup"><span data-stu-id="fd76e-188">If hello stream appears in hello player, then hello encoder has been properly configured tooconnect tooAMS.</span></span>

<span data-ttu-id="fd76e-189">Jeśli błąd kanału hello należy toobe resetowania i koder zmienić ustawienia.</span><span class="sxs-lookup"><span data-stu-id="fd76e-189">If an error is received, hello channel will need toobe reset and encoder settings adjusted.</span></span> <span data-ttu-id="fd76e-190">Zobacz hello [Rozwiązywanie problemów z](media-services-troubleshooting-live-streaming.md) tematu, aby uzyskać wskazówki.</span><span class="sxs-lookup"><span data-stu-id="fd76e-190">Please see hello [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>  

## <a name="create-a-program"></a><span data-ttu-id="fd76e-191">Utwórz program</span><span class="sxs-lookup"><span data-stu-id="fd76e-191">Create a program</span></span>
1. <span data-ttu-id="fd76e-192">Po potwierdzeniu kanału odtwarzania, tworzenia programu.</span><span class="sxs-lookup"><span data-stu-id="fd76e-192">Once channel playback is confirmed, create a program.</span></span> <span data-ttu-id="fd76e-193">W obszarze hello **Live** narzędzia AMSE hello, kliknij prawym przyciskiem myszy w obszarze program hello i wybierz **utworzyć nowy Program**.</span><span class="sxs-lookup"><span data-stu-id="fd76e-193">Under hello **Live** tab in hello AMSE tool, right click within hello program area and select **Create New Program**.</span></span>  

    ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle9.png)
2. <span data-ttu-id="fd76e-195">Nazwy hello program i w razie potrzeby dostosuj hello **długość okna archiwum** (domyślne ustawienia too4 godzin, w których).</span><span class="sxs-lookup"><span data-stu-id="fd76e-195">Name hello program and, if needed, adjust hello **Archive Window Length** (which defaults too4 hours).</span></span> <span data-ttu-id="fd76e-196">Można także określić miejsce przechowywania lub pozostaw domyślne hello.</span><span class="sxs-lookup"><span data-stu-id="fd76e-196">You can also specify a storage location or leave as hello default.</span></span>  
3. <span data-ttu-id="fd76e-197">Sprawdź hello **Start hello Program teraz** pole.</span><span class="sxs-lookup"><span data-stu-id="fd76e-197">Check hello **Start hello Program now** box.</span></span>
4. <span data-ttu-id="fd76e-198">Kliknij przycisk **utworzyć Program**.</span><span class="sxs-lookup"><span data-stu-id="fd76e-198">Click **Create Program**.</span></span>  

    >[!NOTE]
    ><span data-ttu-id="fd76e-199">Tworzenie programu zajmuje mniej czasu niż tworzenie kanału.</span><span class="sxs-lookup"><span data-stu-id="fd76e-199">Program creation takes less time than channel creation.</span></span>
        
5. <span data-ttu-id="fd76e-200">Po uruchomieniu hello program potwierdzić odtwarzania przez kliknięcie prawym przyciskiem myszy hello program i przechodząc zbyt**programach hello odtwarzania** , a następnie wybierając **z usługi Azure Media Player**.</span><span class="sxs-lookup"><span data-stu-id="fd76e-200">Once hello program is running, confirm playback by right clicking hello program and navigating too**Playback hello program(s)** and then selecting **with Azure Media Player**.</span></span>  
6. <span data-ttu-id="fd76e-201">Po potwierdzeniu, kliknij prawym przyciskiem myszy hello program ponownie i wybierz **skopiuj hello adresu URL danych wyjściowych tooClipboard** (lub pobrać te informacje z hello **programu informacji i ustawień** opcji z hello menu).</span><span class="sxs-lookup"><span data-stu-id="fd76e-201">Once confirmed, right click hello program again and select **Copy hello Output URL tooClipboard** (or retrieve this information from hello **Program information and settings** option from hello menu).</span></span>

<span data-ttu-id="fd76e-202">strumień Hello jest teraz gotowy toobe osadzony w odtwarzacza lub odbiorcami tooan rozproszone na żywo wyświetlanie.</span><span class="sxs-lookup"><span data-stu-id="fd76e-202">hello stream is now ready toobe embedded in a player, or distributed tooan audience for live viewing.</span></span>  

## <a name="troubleshooting"></a><span data-ttu-id="fd76e-203">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="fd76e-203">Troubleshooting</span></span>
<span data-ttu-id="fd76e-204">Zobacz hello [Rozwiązywanie problemów z](media-services-troubleshooting-live-streaming.md) tematu, aby uzyskać wskazówki.</span><span class="sxs-lookup"><span data-stu-id="fd76e-204">Please see hello [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="fd76e-205">Ścieżki szkoleniowe dotyczące usługi Media Services</span><span class="sxs-lookup"><span data-stu-id="fd76e-205">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="fd76e-206">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="fd76e-206">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
