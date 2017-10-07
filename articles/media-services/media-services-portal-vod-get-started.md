---
title: "wprowadzenie do dostarczania VoD przy użyciu portalu Azure hello aaaGet | Dokumentacja firmy Microsoft"
description: "Ten samouczek przedstawia kroki wdrażania podstawowej usługi dostarczania zawartości wideo na żądanie (VoD) z aplikacją Azure Media Services (AMS) przy użyciu portalu Azure hello hello."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 6c98fcfa-39e6-43a5-83a5-d4954788f8a4
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/07/2017
ms.author: juliako
ms.openlocfilehash: 5c1c1b1f74ec1f1301120fe8e5a5ae183fe0338f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-delivering-content-on-demand-using-hello-azure-portal"></a><span data-ttu-id="a1d0d-103">Wprowadzenie do dostarczania zawartości na żądanie przy użyciu hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="a1d0d-103">Get started with delivering content on demand using hello Azure portal</span></span>
[!INCLUDE [media-services-selector-get-started](../../includes/media-services-selector-get-started.md)]

<span data-ttu-id="a1d0d-104">Ten samouczek przedstawia kroki wdrażania podstawowej usługi dostarczania zawartości wideo na żądanie (VoD) z aplikacją Azure Media Services (AMS) przy użyciu portalu Azure hello hello.</span><span class="sxs-lookup"><span data-stu-id="a1d0d-104">This tutorial walks you through hello steps of implementing a basic Video-on-Demand (VoD) content delivery service with Azure Media Services (AMS) application using hello Azure portal.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a1d0d-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="a1d0d-105">Prerequisites</span></span>
<span data-ttu-id="a1d0d-106">Samouczek hello toocomplete wymagane są następujące Hello:</span><span class="sxs-lookup"><span data-stu-id="a1d0d-106">hello following are required toocomplete hello tutorial:</span></span>

* <span data-ttu-id="a1d0d-107">Konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="a1d0d-107">An Azure account.</span></span> <span data-ttu-id="a1d0d-108">Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a1d0d-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
* <span data-ttu-id="a1d0d-109">Konto usługi Media Services.</span><span class="sxs-lookup"><span data-stu-id="a1d0d-109">A Media Services account.</span></span> <span data-ttu-id="a1d0d-110">Zobacz toocreate konto usługi Media Services [jak tooCreate konta usługi Media Services](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="a1d0d-110">toocreate a Media Services account, see [How tooCreate a Media Services Account](media-services-portal-create-account.md).</span></span>

<span data-ttu-id="a1d0d-111">W tym samouczku opisano hello następujące zadania:</span><span class="sxs-lookup"><span data-stu-id="a1d0d-111">This tutorial includes hello following tasks:</span></span>

1. <span data-ttu-id="a1d0d-112">Uruchamianie punktu końcowego przesyłania strumieniowego.</span><span class="sxs-lookup"><span data-stu-id="a1d0d-112">Start streaming endpoint.</span></span>
2. <span data-ttu-id="a1d0d-113">Ładowanie pliku wideo.</span><span class="sxs-lookup"><span data-stu-id="a1d0d-113">Upload a video file.</span></span>
3. <span data-ttu-id="a1d0d-114">Kodowanie pliku źródłowego hello do zestawu plików MP4 z adaptacyjną szybkością transmisji bitów.</span><span class="sxs-lookup"><span data-stu-id="a1d0d-114">Encode hello source file into a set of adaptive bitrate MP4 files.</span></span>
4. <span data-ttu-id="a1d0d-115">Publikowanie zawartości hello i get przesyłania strumieniowego i pobierania progresywnego adresów URL.</span><span class="sxs-lookup"><span data-stu-id="a1d0d-115">Publish hello asset and get streaming and progressive download URLs.</span></span>  
5. <span data-ttu-id="a1d0d-116">Odtwarzanie zawartości.</span><span class="sxs-lookup"><span data-stu-id="a1d0d-116">Play your content.</span></span>

## <a name="start-streaming-endpoints"></a><span data-ttu-id="a1d0d-117">Uruchamianie punktu końcowego przesyłania strumieniowego</span><span class="sxs-lookup"><span data-stu-id="a1d0d-117">Start streaming endpoints</span></span> 

<span data-ttu-id="a1d0d-118">Podczas pracy w usłudze Azure Media Services jednym z hello najbardziej typowych scenariuszy jest dostarczanie plików wideo przy użyciu przesyłania strumieniowego adaptacyjną szybkością transmisji bitów.</span><span class="sxs-lookup"><span data-stu-id="a1d0d-118">When working with Azure Media Services one of hello most common scenarios is delivering video via adaptive bitrate streaming.</span></span> <span data-ttu-id="a1d0d-119">Usługa Media Services udostępnia funkcję dynamicznego tworzenia pakietów, co pozwala toodeliver adaptacyjnej szybkości bitowej MP4 zakodowane zawartości w formatach transmisji strumieniowej obsługiwanych przez usługi Media Services (MPEG DASH, HLS, Smooth Streaming) just-in-time, bez konieczności toostore wstępnie umieszczone wersje każdego z tych formatach.</span><span class="sxs-lookup"><span data-stu-id="a1d0d-119">Media Services provides dynamic packaging, which allows you toodeliver your adaptive bitrate MP4 encoded content in streaming formats supported by Media Services (MPEG DASH, HLS, Smooth Streaming) just-in-time, without you having toostore pre-packaged versions of each of these streaming formats.</span></span>

>[!NOTE]
><span data-ttu-id="a1d0d-120">Po utworzeniu konta usługi AMS **domyślne** punktu końcowego przesyłania strumieniowego w brzmieniu konta tooyour hello **zatrzymane** stanu.</span><span class="sxs-lookup"><span data-stu-id="a1d0d-120">When your AMS account is created a **default** streaming endpoint is added tooyour account in hello **Stopped** state.</span></span> <span data-ttu-id="a1d0d-121">przesyłanie strumieniowe zawartości i podejmij korzyści z dynamicznego tworzenia pakietów i dynamicznego szyfrowania toostart hello punktu końcowego przesyłania strumieniowego, z którego mają zostać toostream zawartość ma toobe w hello **systemem** stanu.</span><span class="sxs-lookup"><span data-stu-id="a1d0d-121">toostart streaming your content and take advantage of dynamic packaging and dynamic encryption, hello streaming endpoint from which you want toostream content has toobe in hello **Running** state.</span></span> 

<span data-ttu-id="a1d0d-122">toostart hello punktu końcowego przesyłania strumieniowego, hello następujące:</span><span class="sxs-lookup"><span data-stu-id="a1d0d-122">toostart hello streaming endpoint, do hello following:</span></span>

1. <span data-ttu-id="a1d0d-123">Zaloguj się w hello [portalu Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="a1d0d-123">Log in at hello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="a1d0d-124">W oknie Ustawienia powitania kliknij punkty końcowe przesyłania strumieniowego.</span><span class="sxs-lookup"><span data-stu-id="a1d0d-124">In hello Settings window, click Streaming endpoints.</span></span> 
3. <span data-ttu-id="a1d0d-125">Kliknij przycisk domyślny hello punktu końcowego przesyłania strumieniowego.</span><span class="sxs-lookup"><span data-stu-id="a1d0d-125">Click hello default streaming endpoint.</span></span> 

    <span data-ttu-id="a1d0d-126">zostanie wyświetlone okno Szczegóły punktu KOŃCOWEGO przesyłania STRUMIENIOWEGO domyślne Hello.</span><span class="sxs-lookup"><span data-stu-id="a1d0d-126">hello DEFAULT STREAMING ENDPOINT DETAILS window appears.</span></span>

4. <span data-ttu-id="a1d0d-127">Kliknij ikonę Start hello.</span><span class="sxs-lookup"><span data-stu-id="a1d0d-127">Click hello Start icon.</span></span>
5. <span data-ttu-id="a1d0d-128">Kliknij przycisk toosave przycisk Zapisz hello zmiany.</span><span class="sxs-lookup"><span data-stu-id="a1d0d-128">Click hello Save button toosave your changes.</span></span>

## <a name="upload-files"></a><span data-ttu-id="a1d0d-129">Przekazywanie plików</span><span class="sxs-lookup"><span data-stu-id="a1d0d-129">Upload files</span></span>
<span data-ttu-id="a1d0d-130">toostream wideo przy użyciu usługi Azure Media Services, potrzebne tooupload hello źródłowe pliki wideo, zakodować je do wielokrotnych szybkości transmisji bitów i opublikuj hello wynik.</span><span class="sxs-lookup"><span data-stu-id="a1d0d-130">toostream videos using Azure Media Services, you need tooupload hello source videos, encode them into multiple bitrates, and publish hello result.</span></span> <span data-ttu-id="a1d0d-131">pierwszym krokiem Hello zostało opisane w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="a1d0d-131">hello first step is covered in this section.</span></span> 

1. <span data-ttu-id="a1d0d-132">W hello **ustawienie** okna, kliknij przycisk **zasoby**.</span><span class="sxs-lookup"><span data-stu-id="a1d0d-132">In hello **Setting** window, click **Assets**.</span></span>
   
    ![Przekazywanie plików](./media/media-services-portal-vod-get-started/media-services-upload.png)
2. <span data-ttu-id="a1d0d-134">Kliknij przycisk hello **przekazać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="a1d0d-134">Click hello **Upload** button.</span></span>
   
    <span data-ttu-id="a1d0d-135">Witaj **przekazywanie zawartości wideo** zostanie wyświetlone okno.</span><span class="sxs-lookup"><span data-stu-id="a1d0d-135">hello **Upload a video asset** window appears.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="a1d0d-136">Nie ma żadnego limitu rozmiaru pliku.</span><span class="sxs-lookup"><span data-stu-id="a1d0d-136">There is no file size limitation.</span></span>
   > 
   > 
3. <span data-ttu-id="a1d0d-137">Przeglądaj toohello potrzeby wideo na komputerze, zaznacz go i kliknij przycisk OK.</span><span class="sxs-lookup"><span data-stu-id="a1d0d-137">Browse toohello desired video on your computer, select it, and hit OK.</span></span>  
   
    <span data-ttu-id="a1d0d-138">rozpocznie się przekazywanie Hello, aby zobaczyć postęp hello pod nazwą pliku hello.</span><span class="sxs-lookup"><span data-stu-id="a1d0d-138">hello upload starts and you can see hello progress under hello file name.</span></span>  

<span data-ttu-id="a1d0d-139">Po ukończeniu przekazywania hello Zobacz hello nowy element zawartości na liście hello **zasoby** okna.</span><span class="sxs-lookup"><span data-stu-id="a1d0d-139">Once hello upload completes, you see hello new asset listed in hello **Assets** window.</span></span> 

## <a name="encode-assets"></a><span data-ttu-id="a1d0d-140">Kodowanie elementów zawartości</span><span class="sxs-lookup"><span data-stu-id="a1d0d-140">Encode assets</span></span>

<span data-ttu-id="a1d0d-141">Podczas pracy w usłudze Azure Media Services jednym z hello najbardziej typowych scenariuszy jest dostarczanie przesyłania strumieniowego klientów tooyour adaptacyjną szybkością transmisji bitów.</span><span class="sxs-lookup"><span data-stu-id="a1d0d-141">When working with Azure Media Services one of hello most common scenarios is delivering adaptive bitrate streaming tooyour clients.</span></span> <span data-ttu-id="a1d0d-142">Usługa Media Services obsługuje hello następujące technologie przesyłania strumieniowego adaptacyjną szybkością transmisji bitów: HTTP Live Streaming (HLS), Smooth Streaming, MPEG DASH.</span><span class="sxs-lookup"><span data-stu-id="a1d0d-142">Media Services supports hello following adaptive bitrate streaming technologies: HTTP Live Streaming (HLS), Smooth Streaming, MPEG DASH.</span></span> <span data-ttu-id="a1d0d-143">tooprepare pliki wideo do przesyłania strumieniowego o adaptacyjnej szybkości bitowej, należy tooencode źródła wideo do plików o różnych szybkościach transmisji bitów.</span><span class="sxs-lookup"><span data-stu-id="a1d0d-143">tooprepare your videos for adaptive bitrate streaming, you need tooencode your source video into multi-bitrate files.</span></span> <span data-ttu-id="a1d0d-144">Należy używać hello **Media Encoder Standard** tooencode koder wideo.</span><span class="sxs-lookup"><span data-stu-id="a1d0d-144">You should use hello **Media Encoder Standard** encoder tooencode your videos.</span></span>  

<span data-ttu-id="a1d0d-145">Media Services udostępnia również funkcję dynamicznego tworzenia pakietów, co pozwala toodeliver Twojego MP4s wielokrotnej szybkości transmisji bitów w następujących formatów przesyłania strumieniowego hello: MPEG DASH, HLS, Smooth Streaming, bez konieczności toorepackage w tych formatach.</span><span class="sxs-lookup"><span data-stu-id="a1d0d-145">Media Services also provides dynamic packaging, which allows you toodeliver your multi-bitrate MP4s in hello following streaming formats: MPEG DASH, HLS, Smooth Streaming, without you having toorepackage into these streaming formats.</span></span> <span data-ttu-id="a1d0d-146">Dzięki funkcji dynamicznego tworzenia pakietów, wystarczy toostore i płatności hello pliki w jednym formacie magazynu, a usługa Media Services, tworzy i służy hello właściwą odpowiedź na podstawie żądań klienta.</span><span class="sxs-lookup"><span data-stu-id="a1d0d-146">With dynamic packaging, you only need toostore and pay for hello files in single storage format and Media Services builds and serves hello appropriate response based on requests from a client.</span></span>

<span data-ttu-id="a1d0d-147">tootake korzyści z dynamicznego tworzenia pakietów, należy tooencode pliku źródłowego do zestawu plików MP4 wielokrotnej szybkości transmisji bitów (kroki kodowania hello przedstawiono w dalszej części tej sekcji).</span><span class="sxs-lookup"><span data-stu-id="a1d0d-147">tootake advantage of dynamic packaging, you need tooencode your source file into a set of multi-bitrate MP4 files (hello encoding steps are demonstrated later in this section).</span></span>

### <a name="toouse-hello-portal-tooencode"></a><span data-ttu-id="a1d0d-148">tooencode portalu hello toouse</span><span class="sxs-lookup"><span data-stu-id="a1d0d-148">toouse hello portal tooencode</span></span>
<span data-ttu-id="a1d0d-149">W tej sekcji opisano kroki hello może zająć tooencode zawartości przy użyciu standardu Media Encoder Standard.</span><span class="sxs-lookup"><span data-stu-id="a1d0d-149">This section describes hello steps you can take tooencode your content with Media Encoder Standard.</span></span>

1. <span data-ttu-id="a1d0d-150">W hello **ustawienia** wybierz **zasoby**.</span><span class="sxs-lookup"><span data-stu-id="a1d0d-150">In hello **Settings** window, select **Assets**.</span></span>  
2. <span data-ttu-id="a1d0d-151">W hello **zasoby** okna, wybierz hello zasobów chcesz tooencode.</span><span class="sxs-lookup"><span data-stu-id="a1d0d-151">In hello **Assets** window, select hello asset that you would like tooencode.</span></span>
3. <span data-ttu-id="a1d0d-152">Naciśnij klawisz hello **Koduj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="a1d0d-152">Press hello **Encode** button.</span></span>
4. <span data-ttu-id="a1d0d-153">W hello **kodowanie elementu zawartości** okna, hello wybierz procesor "Media Encoder Standard" oraz ustawienie wstępne.</span><span class="sxs-lookup"><span data-stu-id="a1d0d-153">In hello **Encode an asset** window, select hello "Media Encoder Standard" processor and a preset.</span></span> <span data-ttu-id="a1d0d-154">Aby uzyskać informacje o ustawieniach wstępnych, zobacz [Automatyczne generowanie drabiny szybkości transmisji bitów](media-services-autogen-bitrate-ladder-with-mes.md) i [Ustawienia wstępne zadań usługi MES](media-services-mes-presets-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a1d0d-154">For information about presets, see [auto-generate a bitrate ladder](media-services-autogen-bitrate-ladder-with-mes.md) and [Task Presets for MES](media-services-mes-presets-overview.md).</span></span> <span data-ttu-id="a1d0d-155">Jeśli planujesz toocontrol które kodowania ustawienia wstępnego pamiętać to: koniecznie tooselect hello ustawienia wstępnego najbardziej odpowiednie dla wejściowego pliku wideo.</span><span class="sxs-lookup"><span data-stu-id="a1d0d-155">If you plan toocontrol which encoding preset is used, keep this in mind: it is important tooselect hello preset that is most appropriate for your input video.</span></span> <span data-ttu-id="a1d0d-156">Na przykład, jeśli znasz wejściowy plik wideo ma rozdzielczość 1920 x 1080 pikseli, następnie można hello "H264 szybkość transmisji bitów 1080p" wstępnie zdefiniowane.</span><span class="sxs-lookup"><span data-stu-id="a1d0d-156">For example, if you know your input video has a resolution of 1920x1080 pixels, then you could use hello "H264 Multiple Bitrate 1080p" preset.</span></span> <span data-ttu-id="a1d0d-157">Jeśli wideo jest w niskiej rozdzielczości (640 x 360), nie używaj ustawienia wstępnego „Wielokrotna szybkość transmisji bitów H264 1080p”.</span><span class="sxs-lookup"><span data-stu-id="a1d0d-157">If you have a low resolution (640x360) video, then you should not be using "H264 Multiple Bitrate 1080p" preset.</span></span>
   
   <span data-ttu-id="a1d0d-158">Aby ułatwić zarządzanie istnieje możliwość edytowania hello nazwę zawartości wyjściowej hello i nazwę hello hello zadania.</span><span class="sxs-lookup"><span data-stu-id="a1d0d-158">For easier management, you have an option of editing hello name of hello output asset, and hello name of hello job.</span></span>
   
   ![Kodowanie elementów zawartości](./media/media-services-portal-vod-get-started/media-services-encode1.png)
5. <span data-ttu-id="a1d0d-160">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="a1d0d-160">Press **Create**.</span></span>

### <a name="monitor-encoding-job-progress"></a><span data-ttu-id="a1d0d-161">Monitorowanie postępu zadania kodowania</span><span class="sxs-lookup"><span data-stu-id="a1d0d-161">Monitor encoding job progress</span></span>
<span data-ttu-id="a1d0d-162">postęp hello toomonitor hello kodowanie zadania, kliknij przycisk **ustawienia** (u góry hello hello strony), a następnie wybierz **zadania**.</span><span class="sxs-lookup"><span data-stu-id="a1d0d-162">toomonitor hello progress of hello encoding job, click **Settings** (at hello top of hello page) and then select **Jobs**.</span></span>

![Zadania](./media/media-services-portal-vod-get-started/media-services-jobs.png)

## <a name="publish-content"></a><span data-ttu-id="a1d0d-164">Publikowanie zawartości</span><span class="sxs-lookup"><span data-stu-id="a1d0d-164">Publish content</span></span>
<span data-ttu-id="a1d0d-165">tooprovide użytkownika przy użyciu adresu URL, który może być używane toostream lub pobierania zawartości, należy najpierw należy zbyt "Publikuj" zawartości, tworząc Lokalizator.</span><span class="sxs-lookup"><span data-stu-id="a1d0d-165">tooprovide your user with a  URL that can be used toostream or download your content, you first need too"publish" your asset by creating a locator.</span></span> <span data-ttu-id="a1d0d-166">Lokalizatory zapewniają toofiles dostępu do zawartych w hello zasobów.</span><span class="sxs-lookup"><span data-stu-id="a1d0d-166">Locators provide access toofiles contained in hello asset.</span></span> <span data-ttu-id="a1d0d-167">Usługa Media Services obsługuje dwa typy lokalizatorów:</span><span class="sxs-lookup"><span data-stu-id="a1d0d-167">Media Services supports two types of locators:</span></span> 

* <span data-ttu-id="a1d0d-168">Przesyłanie strumieniowe lokalizatory (OnDemandOrigin) używane do adaptacyjnego przesyłania strumieniowego (na przykład toostream MPEG DASH, HLS lub Smooth Streaming).</span><span class="sxs-lookup"><span data-stu-id="a1d0d-168">Streaming (OnDemandOrigin) locators, used for adaptive streaming (for example, toostream MPEG DASH, HLS, or Smooth Streaming).</span></span> <span data-ttu-id="a1d0d-169">toocreate Lokalizator przesyłania strumieniowego zawartości musi zawierać plik .ism.</span><span class="sxs-lookup"><span data-stu-id="a1d0d-169">toocreate a streaming locator your asset must contain an .ism file.</span></span> 
* <span data-ttu-id="a1d0d-170">Progresywne lokalizatory (SAS) używane do dostarczania plików wideo przy użyciu pobierania progresywnego.</span><span class="sxs-lookup"><span data-stu-id="a1d0d-170">Progressive (SAS) locators, used for delivery of video via progressive download.</span></span>

<span data-ttu-id="a1d0d-171">Adresu URL przesyłania strumieniowego ma hello zgodny z formatem i może być używany tooplay Smooth Streaming zasoby.</span><span class="sxs-lookup"><span data-stu-id="a1d0d-171">A streaming URL has hello following format and you can use it tooplay Smooth Streaming assets.</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest

<span data-ttu-id="a1d0d-172">Dołącz toobuild jako HLS URL, przesyłania strumieniowego (format = m3u8-aapl) toohello adresu URL.</span><span class="sxs-lookup"><span data-stu-id="a1d0d-172">toobuild an HLS streaming URL, append (format=m3u8-aapl) toohello URL.</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)

<span data-ttu-id="a1d0d-173">Dołącz toobuild jako MPEG DASH URL, przesyłania strumieniowego (format = mpd-time-csf) toohello adresu URL.</span><span class="sxs-lookup"><span data-stu-id="a1d0d-173">toobuild an  MPEG DASH streaming URL, append (format=mpd-time-csf) toohello URL.</span></span>

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)


<span data-ttu-id="a1d0d-174">Adres URL SAS ma hello zgodny z formatem.</span><span class="sxs-lookup"><span data-stu-id="a1d0d-174">A SAS URL has hello following format.</span></span>

    {blob container name}/{asset name}/{file name}/{SAS signature}

> [!NOTE]
> <span data-ttu-id="a1d0d-175">Jeśli używasz hello portalu toocreate lokalizatorów przed marcem 2015 r., zostały utworzone lokalizatory z okresem wygaśnięcia dwa lata.</span><span class="sxs-lookup"><span data-stu-id="a1d0d-175">If you used hello portal toocreate locators before March 2015, locators with a two-year expiration date were created.</span></span>  
> 
> 

<span data-ttu-id="a1d0d-176">tooupdate Data wygaśnięcia na lokalizatorze użyj [REST](https://docs.microsoft.com/rest/api/media/operations/locator#update_a_locator) lub [.NET](http://go.microsoft.com/fwlink/?LinkID=533259) interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="a1d0d-176">tooupdate an expiration date on a locator, use [REST](https://docs.microsoft.com/rest/api/media/operations/locator#update_a_locator) or [.NET](http://go.microsoft.com/fwlink/?LinkID=533259) APIs.</span></span> <span data-ttu-id="a1d0d-177">Po zaktualizowaniu daty wygaśnięcia lokalizatora SAS hello zmienia hello adresu URL.</span><span class="sxs-lookup"><span data-stu-id="a1d0d-177">When you update hello expiration date of a SAS locator, hello URL changes.</span></span>

### <a name="toouse-hello-portal-toopublish-an-asset"></a><span data-ttu-id="a1d0d-178">toouse hello portalu toopublish zasobów</span><span class="sxs-lookup"><span data-stu-id="a1d0d-178">toouse hello portal toopublish an asset</span></span>
<span data-ttu-id="a1d0d-179">toouse hello portalu toopublish zasobów hello następujące:</span><span class="sxs-lookup"><span data-stu-id="a1d0d-179">toouse hello portal toopublish an asset, do hello following:</span></span>

1. <span data-ttu-id="a1d0d-180">Wybierz kolejno pozycje **Ustawienia** > **Elementy zawartości**.</span><span class="sxs-lookup"><span data-stu-id="a1d0d-180">Select **Settings** > **Assets**.</span></span>
2. <span data-ttu-id="a1d0d-181">Wybierz hello zasobów, które mają toopublish.</span><span class="sxs-lookup"><span data-stu-id="a1d0d-181">Select hello asset that you want toopublish.</span></span>
3. <span data-ttu-id="a1d0d-182">Kliknij przycisk hello **publikowania** przycisku.</span><span class="sxs-lookup"><span data-stu-id="a1d0d-182">Click hello **Publish** button.</span></span>
4. <span data-ttu-id="a1d0d-183">Wybierz typ lokalizatora hello.</span><span class="sxs-lookup"><span data-stu-id="a1d0d-183">Select hello locator type.</span></span>
5. <span data-ttu-id="a1d0d-184">Kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="a1d0d-184">Press **Add**.</span></span>
   
    ![Publikowanie](./media/media-services-portal-vod-get-started/media-services-publish1.png)

<span data-ttu-id="a1d0d-186">adres URL Hello jest dodawany listy toohello **publikowane adresy URL**.</span><span class="sxs-lookup"><span data-stu-id="a1d0d-186">hello URL is added toohello list of **Published URLs**.</span></span>

## <a name="play-content-from-hello-portal"></a><span data-ttu-id="a1d0d-187">Odtwarzanie zawartości z portalu hello</span><span class="sxs-lookup"><span data-stu-id="a1d0d-187">Play content from hello portal</span></span>
<span data-ttu-id="a1d0d-188">Witaj Azure portal udostępnia odtwarzacz zawartości możesz za pomocą tootest wideo.</span><span class="sxs-lookup"><span data-stu-id="a1d0d-188">hello Azure portal provides a content player that you can use tootest your video.</span></span>

<span data-ttu-id="a1d0d-189">Kliknij żądany hello wideo, a następnie kliknij przycisk hello **odtwarzanie** przycisku.</span><span class="sxs-lookup"><span data-stu-id="a1d0d-189">Click hello desired video and then click hello **Play** button.</span></span>

![Publikowanie](./media/media-services-portal-vod-get-started/media-services-play.png)

<span data-ttu-id="a1d0d-191">Zagadnienia do rozważenia:</span><span class="sxs-lookup"><span data-stu-id="a1d0d-191">Some considerations apply:</span></span>

* <span data-ttu-id="a1d0d-192">toobegin przesyłania strumieniowego, uruchom uruchomionych hello **domyślne** punktu końcowego przesyłania strumieniowego.</span><span class="sxs-lookup"><span data-stu-id="a1d0d-192">toobegin streaming, start running hello **default** streaming endpoint.</span></span>
* <span data-ttu-id="a1d0d-193">Upewnij się, że hello wideo został opublikowany.</span><span class="sxs-lookup"><span data-stu-id="a1d0d-193">Make sure hello video has been published.</span></span>
* <span data-ttu-id="a1d0d-194">To **Media player** odtwarza z domyślnego hello punktu końcowego przesyłania strumieniowego.</span><span class="sxs-lookup"><span data-stu-id="a1d0d-194">This **Media player** plays from hello default streaming endpoint.</span></span> <span data-ttu-id="a1d0d-195">Jeśli chcesz, aby tooplay z innych niż domyślne przesyłania strumieniowego punktu końcowego, kliknij adres URL hello toocopy i użyć innego odtwarzacza.</span><span class="sxs-lookup"><span data-stu-id="a1d0d-195">If you want tooplay from a non-default streaming endpoint, click toocopy hello URL and use another player.</span></span> <span data-ttu-id="a1d0d-196">(np. [Azure Media Services Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html)).</span><span class="sxs-lookup"><span data-stu-id="a1d0d-196">For example, [Azure Media Services Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a1d0d-197">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a1d0d-197">Next steps</span></span>
<span data-ttu-id="a1d0d-198">Przejrzyj ścieżki szkoleniowe dotyczące usługi Media Services.</span><span class="sxs-lookup"><span data-stu-id="a1d0d-198">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="a1d0d-199">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="a1d0d-199">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

