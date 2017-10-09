---
title: "aaaConfigure hello NewTek TriCaster koder toosend strumień na żywo o pojedynczej szybkości transmisji bitów | Dokumentacja firmy Microsoft"
description: "W tym temacie przedstawiono sposób tooconfigure hello Tricaster live toosend kodera kanałami tooAMS strumienia pojedynczej szybkości transmisji bitów, obsługującymi kodowanie na żywo."
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
ms.openlocfilehash: 57dcf62a6a76b04e69f147a738be78ccb3c3ecdc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-newtek-tricaster-encoder-toosend-a-single-bitrate-live-stream"></a><span data-ttu-id="5d35f-103">Użyj hello NewTek TriCaster koder toosend strumień na żywo o pojedynczej szybkości transmisji bitów</span><span class="sxs-lookup"><span data-stu-id="5d35f-103">Use hello NewTek TriCaster encoder toosend a single bitrate live stream</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5d35f-104">Tricaster</span><span class="sxs-lookup"><span data-stu-id="5d35f-104">Tricaster</span></span>](media-services-configure-tricaster-live-encoder.md)
> * [<span data-ttu-id="5d35f-105">Elemental na żywo</span><span class="sxs-lookup"><span data-stu-id="5d35f-105">Elemental Live</span></span>](media-services-configure-elemental-live-encoder.md)
> * [<span data-ttu-id="5d35f-106">Wirecast</span><span class="sxs-lookup"><span data-stu-id="5d35f-106">Wirecast</span></span>](media-services-configure-wirecast-live-encoder.md)
> * [<span data-ttu-id="5d35f-107">FMLE</span><span class="sxs-lookup"><span data-stu-id="5d35f-107">FMLE</span></span>](media-services-configure-fmle-live-encoder.md)
>
>

<span data-ttu-id="5d35f-108">W tym temacie przedstawiono sposób tooconfigure hello [NewTek TriCaster](http://newtek.com/products/tricaster-40.html) kanałami tooAMS strumienia pojedynczej szybkości transmisji bitów, obsługującymi kodowanie na żywo toosend kodera na żywo.</span><span class="sxs-lookup"><span data-stu-id="5d35f-108">This topic shows how tooconfigure hello [NewTek TriCaster](http://newtek.com/products/tricaster-40.html) live encoder toosend a single bitrate stream tooAMS channels that are enabled for live encoding.</span></span> <span data-ttu-id="5d35f-109">Aby uzyskać więcej informacji, zobacz [Praca z kanałami, że włączono tooPerform Live kodowania za pomocą usługi Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).</span><span class="sxs-lookup"><span data-stu-id="5d35f-109">For more information, see [Working with Channels that are Enabled tooPerform Live Encoding with Azure Media Services](media-services-manage-live-encoder-enabled-channels.md).</span></span>

<span data-ttu-id="5d35f-110">Ten samouczek pokazuje, jak toomanage usługi Azure Media Services (AMS) za pomocą narzędzia Azure Media Services Explorer (AMSE).</span><span class="sxs-lookup"><span data-stu-id="5d35f-110">This tutorial shows how toomanage Azure Media Services (AMS) with Azure Media Services Explorer (AMSE) tool.</span></span> <span data-ttu-id="5d35f-111">To narzędzie jest uruchamiane tylko na komputerze z systemem Windows.</span><span class="sxs-lookup"><span data-stu-id="5d35f-111">This tool only runs on Windows PC.</span></span> <span data-ttu-id="5d35f-112">Mac lub Linux, za pomocą hello Azure portalu toocreate [kanałów](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) i [programy](media-services-portal-creating-live-encoder-enabled-channel.md).</span><span class="sxs-lookup"><span data-stu-id="5d35f-112">If you are on Mac or Linux, use hello Azure portal toocreate [channels](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) and [programs](media-services-portal-creating-live-encoder-enabled-channel.md).</span></span>

> [!NOTE]
> <span data-ttu-id="5d35f-113">Podczas wysyłania w udziale za pomocą Tricaster źródła kanałami tooAMS, obsługującymi kodowanie na żywo, może istnieć błędami występującymi audio/wideo w zdarzenia na żywo w przypadku określonych funkcji Tricaster, takie jak szybka Wycinanie między źródła danych lub przełączanie z typu .</span><span class="sxs-lookup"><span data-stu-id="5d35f-113">When using Tricaster for sending in a contribution feed tooAMS channels that are enabled for live encoding, there can be video/audio glitches in your live event if you use certain features of Tricaster, such as rapid cutting between feeds, or switching to/from slates.</span></span> <span data-ttu-id="5d35f-114">Witaj AMS zespołu działa w rozwiązaniu tych problemów, do tego czasu jest zaleca toouse te funkcje.</span><span class="sxs-lookup"><span data-stu-id="5d35f-114">hello AMS team is working on fixing these issues, until then, it is not recommend toouse these features.</span></span>
>
>

## <a name="prerequisites"></a><span data-ttu-id="5d35f-115">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="5d35f-115">Prerequisites</span></span>
* [<span data-ttu-id="5d35f-116">Tworzenie konta usługi Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="5d35f-116">Create an Azure Media Services account</span></span>](media-services-portal-create-account.md)
* <span data-ttu-id="5d35f-117">Upewnij się, brak punktu końcowego przesyłania strumieniowego uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="5d35f-117">Ensure there is a Streaming Endpoint running.</span></span> <span data-ttu-id="5d35f-118">Aby uzyskać więcej informacji, zobacz [zarządzanie punktami końcowymi przesyłania strumieniowego w konta usługi Media Services](media-services-portal-manage-streaming-endpoints.md)</span><span class="sxs-lookup"><span data-stu-id="5d35f-118">For more information, see [Manage Streaming Endpoints in a Media Services Account](media-services-portal-manage-streaming-endpoints.md)</span></span>
* <span data-ttu-id="5d35f-119">Zainstaluj najnowszą wersję hello hello [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) narzędzia.</span><span class="sxs-lookup"><span data-stu-id="5d35f-119">Install hello latest version of hello [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) tool.</span></span>
* <span data-ttu-id="5d35f-120">Uruchom narzędzie hello i Połącz konto tooyour AMS.</span><span class="sxs-lookup"><span data-stu-id="5d35f-120">Launch hello tool and connect tooyour AMS account.</span></span>

## <a name="tips"></a><span data-ttu-id="5d35f-121">Porady</span><span class="sxs-lookup"><span data-stu-id="5d35f-121">Tips</span></span>
* <span data-ttu-id="5d35f-122">Jeśli to możliwe, użyj połączenia internetowego hardwired.</span><span class="sxs-lookup"><span data-stu-id="5d35f-122">Whenever possible, use a hardwired internet connection.</span></span>
* <span data-ttu-id="5d35f-123">Regułą podczas określania wymaganiach odnośnie do przepustowości jest hello toodouble przesyłania strumieniowego szybkości transmisji bitów.</span><span class="sxs-lookup"><span data-stu-id="5d35f-123">A good rule of thumb when determining bandwidth requirements is toodouble hello streaming bitrates.</span></span> <span data-ttu-id="5d35f-124">Chociaż nie jest to wymagane, może pomóc zmniejszyć wpływ hello sieci przeciążona.</span><span class="sxs-lookup"><span data-stu-id="5d35f-124">While this is not a mandatory requirement, it will help mitigate hello impact of network congestion.</span></span>
* <span data-ttu-id="5d35f-125">Gdy za pomocą oprogramowania na podstawie koderów, zamknij wszystkie zbędne programy.</span><span class="sxs-lookup"><span data-stu-id="5d35f-125">When using software based encoders, close out any unnecessary programs.</span></span>

## <a name="create-a-channel"></a><span data-ttu-id="5d35f-126">Tworzenie kanału</span><span class="sxs-lookup"><span data-stu-id="5d35f-126">Create a channel</span></span>
1. <span data-ttu-id="5d35f-127">Narzędzie AMSE hello Przejdź toohello **Live** karcie, a następnie kliknij prawym przyciskiem myszy w obszarze kanału hello.</span><span class="sxs-lookup"><span data-stu-id="5d35f-127">In hello AMSE tool, navigate toohello **Live** tab, and right click within hello channel area.</span></span> <span data-ttu-id="5d35f-128">Wybierz **Utwórz kanał...**</span><span class="sxs-lookup"><span data-stu-id="5d35f-128">Select **Create channel…**</span></span> <span data-ttu-id="5d35f-129">z hello menu.</span><span class="sxs-lookup"><span data-stu-id="5d35f-129">from hello menu.</span></span>

    ![tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster1.png)

2. <span data-ttu-id="5d35f-131">Określ nazwę kanału hello pole opisu jest opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="5d35f-131">Specify a channel name, hello description field is optional.</span></span> <span data-ttu-id="5d35f-132">W ustawieniach kanału, wybierz **standardowe** dla hello opcji kodowanie na żywo z hello wprowadzania ustawiony protokół zbyt**RTMP**.</span><span class="sxs-lookup"><span data-stu-id="5d35f-132">Under Channel Settings, select **Standard** for hello Live Encoding option, with hello Input Protocol set too**RTMP**.</span></span> <span data-ttu-id="5d35f-133">Możesz pozostawić wszystkie inne ustawienia, ponieważ jest.</span><span class="sxs-lookup"><span data-stu-id="5d35f-133">You can leave all other settings as is.</span></span>

    <span data-ttu-id="5d35f-134">Upewnij się, że hello **Start hello nowy kanał teraz** jest zaznaczone.</span><span class="sxs-lookup"><span data-stu-id="5d35f-134">Make sure hello **Start hello new channel now** is selected.</span></span>

3. <span data-ttu-id="5d35f-135">Kliknij przycisk **utworzyć kanał**.</span><span class="sxs-lookup"><span data-stu-id="5d35f-135">Click **Create Channel**.</span></span>

   ![tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster2.png)

> [!NOTE]
> <span data-ttu-id="5d35f-137">kanał Hello może zająć toostart 20 minut.</span><span class="sxs-lookup"><span data-stu-id="5d35f-137">hello channel can take as long as 20 minutes toostart.</span></span>
>
>

<span data-ttu-id="5d35f-138">Podczas uruchamiania kanału hello można [skonfigurować koder hello](media-services-configure-tricaster-live-encoder.md#configure_tricaster_rtmp).</span><span class="sxs-lookup"><span data-stu-id="5d35f-138">While hello channel is starting you can [configure hello encoder](media-services-configure-tricaster-live-encoder.md#configure_tricaster_rtmp).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5d35f-139">Należy pamiętać, że rozliczanie zaczyna się jak kanału przechodzi do stanu gotowości.</span><span class="sxs-lookup"><span data-stu-id="5d35f-139">Note that billing starts as soon as Channel goes into a ready state.</span></span> <span data-ttu-id="5d35f-140">Aby uzyskać więcej informacji, zobacz [stanów kanału](media-services-manage-live-encoder-enabled-channels.md#states).</span><span class="sxs-lookup"><span data-stu-id="5d35f-140">For more information, see [Channel's states](media-services-manage-live-encoder-enabled-channels.md#states).</span></span>
>
>

## <span data-ttu-id="5d35f-141"><a id=configure_tricaster_rtmp></a>Skonfiguruj hello NewTek TriCaster kodera</span><span class="sxs-lookup"><span data-stu-id="5d35f-141"><a id=configure_tricaster_rtmp></a>Configure hello NewTek TriCaster encoder</span></span>
<span data-ttu-id="5d35f-142">W tym samouczek hello są używane następujące ustawienia danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="5d35f-142">In this tutorial hello following output settings are used.</span></span> <span data-ttu-id="5d35f-143">Hello pozostałej części tej sekcji opisano kroki konfiguracji szczegółowo.</span><span class="sxs-lookup"><span data-stu-id="5d35f-143">hello rest of this section describes configuration steps in more detail.</span></span>

<span data-ttu-id="5d35f-144">**Wideo**:</span><span class="sxs-lookup"><span data-stu-id="5d35f-144">**Video**:</span></span>

* <span data-ttu-id="5d35f-145">Koder-dekoder: H.264</span><span class="sxs-lookup"><span data-stu-id="5d35f-145">Codec: H.264</span></span>
* <span data-ttu-id="5d35f-146">Profil: Wysoki (poziom 4.0)</span><span class="sxs-lookup"><span data-stu-id="5d35f-146">Profile: High (Level 4.0)</span></span>
* <span data-ttu-id="5d35f-147">Szybkość transmisji bitów: 5000 KB/s</span><span class="sxs-lookup"><span data-stu-id="5d35f-147">Bitrate: 5000 kbps</span></span>
* <span data-ttu-id="5d35f-148">Klatki kluczowej: 2 sekundy (60 sekund)</span><span class="sxs-lookup"><span data-stu-id="5d35f-148">Keyframe: 2 seconds (60 seconds)</span></span>
* <span data-ttu-id="5d35f-149">Szybkość klatek: 30</span><span class="sxs-lookup"><span data-stu-id="5d35f-149">Frame Rate: 30</span></span>

<span data-ttu-id="5d35f-150">**Audio**:</span><span class="sxs-lookup"><span data-stu-id="5d35f-150">**Audio**:</span></span>

* <span data-ttu-id="5d35f-151">Koder-dekoder: AAC (LC —)</span><span class="sxs-lookup"><span data-stu-id="5d35f-151">Codec: AAC (LC)</span></span>
* <span data-ttu-id="5d35f-152">Szybkość transmisji bitów: 192 kb/s</span><span class="sxs-lookup"><span data-stu-id="5d35f-152">Bitrate: 192 kbps</span></span>
* <span data-ttu-id="5d35f-153">Częstotliwość próbkowania: 44,1 kHz</span><span class="sxs-lookup"><span data-stu-id="5d35f-153">Sample Rate: 44.1 kHz</span></span>

### <a name="configuration-steps"></a><span data-ttu-id="5d35f-154">Kroki konfiguracji</span><span class="sxs-lookup"><span data-stu-id="5d35f-154">Configuration steps</span></span>
1. <span data-ttu-id="5d35f-155">Utwórz nową **NewTek TriCaster** projektu w zależności od tego, jakie wideo źródło danych wejściowych jest używany.</span><span class="sxs-lookup"><span data-stu-id="5d35f-155">Create a new **NewTek TriCaster** project depending on what video input source is being used.</span></span>
2. <span data-ttu-id="5d35f-156">Raz w ramach tego projektu, Znajdź hello **strumienia** przycisk, a następnie kliknij przycisk hello koło zębate ikonę dalej tooit tooaccess hello strumienia menu konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="5d35f-156">Once within that project, find hello **Stream** button, and click hello gear icon next tooit tooaccess hello stream configuration menu.</span></span>

    ![tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster3.png)
3. <span data-ttu-id="5d35f-158">Po otwarciu hello menu, kliknij przycisk **nowy** hello połączenia pozycji.</span><span class="sxs-lookup"><span data-stu-id="5d35f-158">Once hello menu has opened, click **New** under hello Connection heading.</span></span> <span data-ttu-id="5d35f-159">Po wyświetleniu monitu dla typu połączenia hello, wybierz **Adobe Flash**.</span><span class="sxs-lookup"><span data-stu-id="5d35f-159">When prompted for hello connection type, select **Adobe Flash**.</span></span>

    ![tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster4.png)
4. <span data-ttu-id="5d35f-161">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="5d35f-161">Click **OK**.</span></span>
5. <span data-ttu-id="5d35f-162">Teraz można zaimportować profil FMLE klikając hello strzałkę listy rozwijanej w obszarze **przesyłania strumieniowego profilu** i przechodząc zbyt**Przeglądaj**.</span><span class="sxs-lookup"><span data-stu-id="5d35f-162">An FMLE profile can now be imported by clicking hello drop down arrow under **Streaming Profile** and navigating too**Browse**.</span></span>

    ![tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster5.png)
6. <span data-ttu-id="5d35f-164">Przejdź toowhere hello skonfigurowane FMLE profil został zapisany.</span><span class="sxs-lookup"><span data-stu-id="5d35f-164">Navigate toowhere hello configured FMLE profile was saved.</span></span>
7. <span data-ttu-id="5d35f-165">Wybierz go, a następnie naciśnij klawisz **OK**.</span><span class="sxs-lookup"><span data-stu-id="5d35f-165">Select it, and press **OK**.</span></span>

    <span data-ttu-id="5d35f-166">Po przekazaniu plików profilu hello kontynuować toohello następnego kroku.</span><span class="sxs-lookup"><span data-stu-id="5d35f-166">Once hello profile is uploaded, proceed toohello next step.</span></span>
8. <span data-ttu-id="5d35f-167">Pobierz hello kanał wejściowy adres URL w kolejności tooassign on toohello Tricaster **punktu końcowego protokołu RTMP**.</span><span class="sxs-lookup"><span data-stu-id="5d35f-167">Get hello channel's input URL in order tooassign it toohello Tricaster **RTMP Endpoint**.</span></span>

    <span data-ttu-id="5d35f-168">Przejdź wstecz toohello narzędzie AMSE i sprawdzić stan ukończenia hello kanału.</span><span class="sxs-lookup"><span data-stu-id="5d35f-168">Navigate back toohello AMSE tool, and check on hello channel completion status.</span></span> <span data-ttu-id="5d35f-169">Po hello stan został zmieniony z **uruchamianie** za**systemem**, możesz uzyskać hello wejściowy adres URL.</span><span class="sxs-lookup"><span data-stu-id="5d35f-169">Once hello State has changed from **Starting** too**Running**, you can get hello input URL.</span></span>

    <span data-ttu-id="5d35f-170">Gdy kanał hello jest uruchomiona, kliknij prawym przyciskiem myszy nazwę kanału hello, przechodzenia toohover za pośrednictwem **tooclipboard kopia danych wejściowych URL** , a następnie wybierz **podstawowego adresu URL danych wejściowych**.</span><span class="sxs-lookup"><span data-stu-id="5d35f-170">When hello channel is running, right click hello channel name, navigate down toohover over **Copy Input URL tooclipboard** and then select **Primary Input  URL**.</span></span>  

    ![tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster6.png)
9. <span data-ttu-id="5d35f-172">Wklej te informacje w hello **lokalizacji** pole w obszarze **Flash Server** w ramach hello Tricaster projektu.</span><span class="sxs-lookup"><span data-stu-id="5d35f-172">Paste this information in hello **Location** field under **Flash Server** within hello Tricaster project.</span></span> <span data-ttu-id="5d35f-173">Również przypisać nazwę strumienia w hello **Identyfikator strumienia** pola.</span><span class="sxs-lookup"><span data-stu-id="5d35f-173">Also assign a stream name in hello **Stream ID** field.</span></span>

    <span data-ttu-id="5d35f-174">Jeśli dodano informacje o strumienia toohello FMLE profilu, można również importować go toothis sekcji klikając **importowanie ustawień**, nawigacja profilu FMLE toohello zapisane i klikając pozycję **OK**.</span><span class="sxs-lookup"><span data-stu-id="5d35f-174">If stream information was added toohello FMLE profile, it can also be imported toothis section by clicking **Import Settings**, navigating toohello saved FMLE profile and clicking **OK**.</span></span> <span data-ttu-id="5d35f-175">Hello odpowiednie pola Flash serwera należy wypełnić hello informacje z FMLE.</span><span class="sxs-lookup"><span data-stu-id="5d35f-175">hello relevant Flash Server fields should populate with hello information from FMLE.</span></span>

    ![tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster7.png)
10. <span data-ttu-id="5d35f-177">Gdy skończysz, kliknij przycisk **OK** u dołu hello hello ekranu.</span><span class="sxs-lookup"><span data-stu-id="5d35f-177">When finished, click **OK** at hello bottom of hello screen.</span></span> <span data-ttu-id="5d35f-178">Po zakończeniu dane wejściowe audio i wideo w hello Tricaster rozpocząć przesyłanie strumieniowe tooAMS klikając hello **strumienia** przycisku.</span><span class="sxs-lookup"><span data-stu-id="5d35f-178">When video and audio inputs into hello Tricaster are ready, begin streaming tooAMS by clicking hello **Stream** button.</span></span>

     ![tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster11.png)

> [!IMPORTANT]
> <span data-ttu-id="5d35f-180">Przed kliknięciem przycisku **strumienia**, możesz **musi** upewnij się, że kanał hello jest gotowy.</span><span class="sxs-lookup"><span data-stu-id="5d35f-180">Before you click **Stream**, you **must** ensure that hello Channel is ready.</span></span>
> <span data-ttu-id="5d35f-181">Sprawdź także, czy nie tooleave hello kanału w stanie Gotowe bez wprowadzania wkład źródła danych przez czas dłuższy niż > 15 minut.</span><span class="sxs-lookup"><span data-stu-id="5d35f-181">Also, make sure not tooleave hello Channel in a ready state without an input contribution feed for longer than > 15 minutes.</span></span>
>
>

## <a name="test-playback"></a><span data-ttu-id="5d35f-182">Podczas odtwarzania testu</span><span class="sxs-lookup"><span data-stu-id="5d35f-182">Test playback</span></span>
<span data-ttu-id="5d35f-183">Przejdź narzędzie AMSE toohello, a następnie kliknij prawym przyciskiem myszy toobe kanału hello przetestowane.</span><span class="sxs-lookup"><span data-stu-id="5d35f-183">Navigate toohello AMSE tool, and right click hello channel toobe tested.</span></span> <span data-ttu-id="5d35f-184">Z hello menu, umieść kursor nad **hello odtwarzania podglądu** i wybierz **z usługi Azure Media Player**.</span><span class="sxs-lookup"><span data-stu-id="5d35f-184">From hello menu, hover over **Playback hello Preview** and select **with Azure Media Player**.</span></span>  

    ![tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster8.png)

<span data-ttu-id="5d35f-185">Czy strumienia hello znajduje się w hello player, koder hello został tooAMS tooconnect poprawnie skonfigurowana.</span><span class="sxs-lookup"><span data-stu-id="5d35f-185">If hello stream appears in hello player, then hello encoder has been properly configured tooconnect tooAMS.</span></span>

<span data-ttu-id="5d35f-186">Jeśli błąd kanału hello należy toobe resetowania i koder zmienić ustawienia.</span><span class="sxs-lookup"><span data-stu-id="5d35f-186">If an error is received, hello channel will need toobe reset and encoder settings adjusted.</span></span> <span data-ttu-id="5d35f-187">Zobacz hello [Rozwiązywanie problemów z](media-services-troubleshooting-live-streaming.md) tematu, aby uzyskać wskazówki.</span><span class="sxs-lookup"><span data-stu-id="5d35f-187">Please see hello [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>  

## <a name="create-a-program"></a><span data-ttu-id="5d35f-188">Utwórz program</span><span class="sxs-lookup"><span data-stu-id="5d35f-188">Create a program</span></span>
1. <span data-ttu-id="5d35f-189">Po potwierdzeniu kanału odtwarzania, tworzenia programu.</span><span class="sxs-lookup"><span data-stu-id="5d35f-189">Once channel playback is confirmed, create a program.</span></span> <span data-ttu-id="5d35f-190">W obszarze hello **Live** narzędzia AMSE hello, kliknij prawym przyciskiem myszy w obszarze program hello i wybierz **utworzyć nowy Program**.</span><span class="sxs-lookup"><span data-stu-id="5d35f-190">Under hello **Live** tab in hello AMSE tool, right click within hello program area and select **Create New Program**.</span></span>  

    ![tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster9.png)
2. <span data-ttu-id="5d35f-192">Nazwy hello program i w razie potrzeby dostosuj hello **długość okna archiwum** (domyślne ustawienia too4 godzin, w których).</span><span class="sxs-lookup"><span data-stu-id="5d35f-192">Name hello program and, if needed, adjust hello **Archive Window Length** (which defaults too4 hours).</span></span> <span data-ttu-id="5d35f-193">Można także określić miejsce przechowywania lub pozostaw domyślne hello.</span><span class="sxs-lookup"><span data-stu-id="5d35f-193">You can also specify a storage location or leave as hello default.</span></span>  
3. <span data-ttu-id="5d35f-194">Sprawdź hello **Start hello Program teraz** pole.</span><span class="sxs-lookup"><span data-stu-id="5d35f-194">Check hello **Start hello Program now** box.</span></span>
4. <span data-ttu-id="5d35f-195">Kliknij przycisk **utworzyć Program**.</span><span class="sxs-lookup"><span data-stu-id="5d35f-195">Click **Create Program**.</span></span>  

    >[!NOTE]
    ><span data-ttu-id="5d35f-196">Tworzenie programu zajmuje mniej czasu niż tworzenie kanału.</span><span class="sxs-lookup"><span data-stu-id="5d35f-196">Program creation takes less time than channel creation.</span></span>
        
5. <span data-ttu-id="5d35f-197">Po uruchomieniu hello program potwierdzić odtwarzania przez kliknięcie prawym przyciskiem myszy hello program i przechodząc zbyt**programach hello odtwarzania** , a następnie wybierając **z usługi Azure Media Player**.</span><span class="sxs-lookup"><span data-stu-id="5d35f-197">Once hello program is running, confirm playback by right clicking hello program and navigating too**Playback hello program(s)** and then selecting **with Azure Media Player**.</span></span>  
6. <span data-ttu-id="5d35f-198">Po potwierdzeniu, kliknij prawym przyciskiem myszy hello program ponownie i wybierz **skopiuj hello adresu URL danych wyjściowych tooClipboard** (lub pobrać te informacje z hello **programu informacji i ustawień** opcji z hello menu).</span><span class="sxs-lookup"><span data-stu-id="5d35f-198">Once confirmed, right click hello program again and select **Copy hello Output URL tooClipboard** (or retrieve this information from hello **Program information and settings** option from hello menu).</span></span>

<span data-ttu-id="5d35f-199">strumień Hello jest teraz gotowy toobe osadzony w odtwarzacza lub odbiorcami tooan rozproszone na żywo wyświetlanie.</span><span class="sxs-lookup"><span data-stu-id="5d35f-199">hello stream is now ready toobe embedded in a player, or distributed tooan audience for live viewing.</span></span>  

## <a name="troubleshooting"></a><span data-ttu-id="5d35f-200">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="5d35f-200">Troubleshooting</span></span>
<span data-ttu-id="5d35f-201">Zobacz hello [Rozwiązywanie problemów z](media-services-troubleshooting-live-streaming.md) tematu, aby uzyskać wskazówki.</span><span class="sxs-lookup"><span data-stu-id="5d35f-201">Please see hello [troubleshooting](media-services-troubleshooting-live-streaming.md) topic for guidance.</span></span>

## <a name="next-step"></a><span data-ttu-id="5d35f-202">Następny krok</span><span class="sxs-lookup"><span data-stu-id="5d35f-202">Next step</span></span>
<span data-ttu-id="5d35f-203">Przejrzyj ścieżki szkoleniowe dotyczące usługi Media Services.</span><span class="sxs-lookup"><span data-stu-id="5d35f-203">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="5d35f-204">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="5d35f-204">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
