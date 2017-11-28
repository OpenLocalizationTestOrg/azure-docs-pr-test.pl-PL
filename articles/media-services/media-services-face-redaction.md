---
title: "aaaRedact krojów z analizy multimediów Azure | Dokumentacja firmy Microsoft"
description: "W tym temacie przedstawiono sposób tooredact skierowany z analizy multimediów Azure."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 5b6d8b8c-5f4d-4fef-b3d6-dc22c6b5a0f5
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/31/2017
ms.author: juliako;
ms.openlocfilehash: 1f5688a8c6374151c526a9c702b904d8c3e46164
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="redact-faces-with-azure-media-analytics"></a><span data-ttu-id="a04c0-103">Redagowanie krojów z analizy multimediów Azure</span><span class="sxs-lookup"><span data-stu-id="a04c0-103">Redact faces with Azure Media Analytics</span></span>
## <a name="overview"></a><span data-ttu-id="a04c0-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="a04c0-104">Overview</span></span>
<span data-ttu-id="a04c0-105">**Azure Media Redactor** jest [analizy multimediów Azure](media-services-analytics-overview.md) procesor multimediów (MP) oferuje skalowalne krój redakcyjne w chmurze hello.</span><span class="sxs-lookup"><span data-stu-id="a04c0-105">**Azure Media Redactor** is an [Azure Media Analytics](media-services-analytics-overview.md) media processor (MP) that offers scalable face redaction in hello cloud.</span></span> <span data-ttu-id="a04c0-106">Redakcyjne krój umożliwia możesz toomodify wideo w kolejności tooblur kroje wybrane osoby.</span><span class="sxs-lookup"><span data-stu-id="a04c0-106">Face redaction enables you toomodify your video in order tooblur faces of selected individuals.</span></span> <span data-ttu-id="a04c0-107">Możesz toouse hello krój redakcyjne usługi w publicznych scenariusze bezpieczeństwa i nośnika wiadomości.</span><span class="sxs-lookup"><span data-stu-id="a04c0-107">You may want toouse hello face redaction service in public safety and news media scenarios.</span></span> <span data-ttu-id="a04c0-108">Kilka minut najmniejszym zawiera wiele kroje może zająć godziny tooredact ręcznie, ale z tej usługi hello powierzchni procesu redakcyjne wymaga kilku prostych krokach.</span><span class="sxs-lookup"><span data-stu-id="a04c0-108">A few minutes of footage that contains multiple faces can take hours tooredact manually, but with this service hello face redaction process will require just a few simple steps.</span></span> <span data-ttu-id="a04c0-109">Aby uzyskać więcej informacji, zobacz [to](https://azure.microsoft.com/blog/azure-media-redactor/) blogu.</span><span class="sxs-lookup"><span data-stu-id="a04c0-109">For  more information, see [this](https://azure.microsoft.com/blog/azure-media-redactor/) blog.</span></span>

<span data-ttu-id="a04c0-110">Ten temat zawiera szczegółowe informacje o **Azure Media Redactor** i przedstawia sposób toouse go przy użyciu zestawu SDK usługi Media Services dla platformy .NET.</span><span class="sxs-lookup"><span data-stu-id="a04c0-110">This topic gives details about **Azure Media Redactor** and shows how toouse it with Media Services SDK for .NET.</span></span>

<span data-ttu-id="a04c0-111">Witaj **Azure Media Redactor** pakiet administracyjny jest obecnie w przeglądzie.</span><span class="sxs-lookup"><span data-stu-id="a04c0-111">hello **Azure Media Redactor** MP is currently in Preview.</span></span> <span data-ttu-id="a04c0-112">Jest ona dostępna w wszystkich publicznych regiony platformy Azure, a także centrach danych instytucji rządowych Stanów Zjednoczonych i Chinach.</span><span class="sxs-lookup"><span data-stu-id="a04c0-112">It is available in all public Azure regions as well as US Government and China data centers.</span></span> <span data-ttu-id="a04c0-113">Ta wersja zapoznawcza jest obecnie bezpłatnie.</span><span class="sxs-lookup"><span data-stu-id="a04c0-113">This preview is currently free of charge.</span></span> 

## <a name="face-redaction-modes"></a><span data-ttu-id="a04c0-114">Tryby redakcyjne krój</span><span class="sxs-lookup"><span data-stu-id="a04c0-114">Face redaction modes</span></span>
<span data-ttu-id="a04c0-115">Działa twarzy redakcyjne wykrywanie kroje w każdej ramce wideo i śledząc krój hello obiekt, zarówno przodu i do tyłu w czasie, tak aby hello tej samej osoby mogą być rozmyciu z innych kątów również.</span><span class="sxs-lookup"><span data-stu-id="a04c0-115">Facial redaction works by detecting faces in every frame of video and tracking hello face object both forwards and backwards in time, so that hello same individual can be blurred from other angles as well.</span></span> <span data-ttu-id="a04c0-116">Witaj redakcyjne zautomatyzowanych procesów jest bardzo skomplikowane i nie zawsze 100% żądanego wyniku, z tego powodu analizy multimediów udostępnia kilka sposobów hello toomodify pliku wyjściowego.</span><span class="sxs-lookup"><span data-stu-id="a04c0-116">hello automated redaction process is very complex and does not always produce 100% of desired output, for this reason Media Analytics provides you with a couple of ways toomodify hello final output.</span></span>

<span data-ttu-id="a04c0-117">Dodanie tooa pełni automatycznym ma dwa przebiegu przepływu pracy, dzięki czemu hello wyboru/dezaktywuje-selection z znaleziono kroje za pomocą listy identyfikatorów.</span><span class="sxs-lookup"><span data-stu-id="a04c0-117">In addition tooa fully automatic mode, there is a two-pass workflow which allows hello selection/de-selection of found faces via a list of IDs.</span></span> <span data-ttu-id="a04c0-118">Toomake dowolnego na ramki dostosowań hello MP używa również, plik metadanych w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="a04c0-118">Also, toomake arbitrary per frame adjustments hello MP uses a metadata file in JSON format.</span></span> <span data-ttu-id="a04c0-119">Ten przepływ pracy jest podzielony na **Analizuj** i **Redact** trybów.</span><span class="sxs-lookup"><span data-stu-id="a04c0-119">This workflow is split into **Analyze** and **Redact** modes.</span></span> <span data-ttu-id="a04c0-120">Możesz połączyć ze sobą dwa tryby hello w jednym przebiegu uruchomioną obu zadań w jedno zadanie. Ten tryb jest nazywany **nomenklatury**.</span><span class="sxs-lookup"><span data-stu-id="a04c0-120">You can combine hello two modes in a single pass that runs both tasks in one job; this mode is called **Combined**.</span></span>

### <a name="combined-mode"></a><span data-ttu-id="a04c0-121">Tryb połączone</span><span class="sxs-lookup"><span data-stu-id="a04c0-121">Combined mode</span></span>
<span data-ttu-id="a04c0-122">Spowoduje to utworzenie zredagowanym mp4 automatycznie bez żadnych ręcznego wprowadzania.</span><span class="sxs-lookup"><span data-stu-id="a04c0-122">This will produce a redacted mp4 automatically without any manual input.</span></span>

| <span data-ttu-id="a04c0-123">Etap</span><span class="sxs-lookup"><span data-stu-id="a04c0-123">Stage</span></span> | <span data-ttu-id="a04c0-124">Nazwa pliku</span><span class="sxs-lookup"><span data-stu-id="a04c0-124">File Name</span></span> | <span data-ttu-id="a04c0-125">Uwagi</span><span class="sxs-lookup"><span data-stu-id="a04c0-125">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a04c0-126">Wejściowy zasobów</span><span class="sxs-lookup"><span data-stu-id="a04c0-126">Input asset</span></span> |<span data-ttu-id="a04c0-127">foo.bar</span><span class="sxs-lookup"><span data-stu-id="a04c0-127">foo.bar</span></span> |<span data-ttu-id="a04c0-128">Wideo w formacie WMV, MOV lub MP4</span><span class="sxs-lookup"><span data-stu-id="a04c0-128">Video in WMV, MOV, or MP4 format</span></span> |
| <span data-ttu-id="a04c0-129">Dane wejściowe konfiguracji</span><span class="sxs-lookup"><span data-stu-id="a04c0-129">Input config</span></span> |<span data-ttu-id="a04c0-130">Zadania konfiguracji ustawień wstępnych.</span><span class="sxs-lookup"><span data-stu-id="a04c0-130">Job configuration preset</span></span> |<span data-ttu-id="a04c0-131">{"version": "1.0", "Opcje": {'mode': "łączyć"}}</span><span class="sxs-lookup"><span data-stu-id="a04c0-131">{'version':'1.0', 'options': {'mode':'combined'}}</span></span> |
| <span data-ttu-id="a04c0-132">Dane wyjściowe zasobów</span><span class="sxs-lookup"><span data-stu-id="a04c0-132">Output asset</span></span> |<span data-ttu-id="a04c0-133">foo_redacted.mp4</span><span class="sxs-lookup"><span data-stu-id="a04c0-133">foo_redacted.mp4</span></span> |<span data-ttu-id="a04c0-134">Wideo z rozmycia stosowane</span><span class="sxs-lookup"><span data-stu-id="a04c0-134">Video with blurring applied</span></span> |

#### <a name="input-example"></a><span data-ttu-id="a04c0-135">Przykład wejściowych:</span><span class="sxs-lookup"><span data-stu-id="a04c0-135">Input example:</span></span>
[<span data-ttu-id="a04c0-136">Wyświetl ten film</span><span class="sxs-lookup"><span data-stu-id="a04c0-136">view this video</span></span>](http://ampdemo.azureedge.net/?url=http%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fed99001d-72ee-4f91-9fc0-cd530d0adbbc%2FDancing.mp4)

#### <a name="output-example"></a><span data-ttu-id="a04c0-137">Przykład danych wyjściowych:</span><span class="sxs-lookup"><span data-stu-id="a04c0-137">Output example:</span></span>
[<span data-ttu-id="a04c0-138">Wyświetl ten film</span><span class="sxs-lookup"><span data-stu-id="a04c0-138">view this video</span></span>](http://ampdemo.azureedge.net/?url=http%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fc6608001-e5da-429b-9ec8-d69d8f3bfc79%2Fdance_redacted.mp4)

### <a name="analyze-mode"></a><span data-ttu-id="a04c0-139">Analizowanie tryb</span><span class="sxs-lookup"><span data-stu-id="a04c0-139">Analyze mode</span></span>
<span data-ttu-id="a04c0-140">Witaj **analizowanie** przebieg przepływu pracy Przekaż dwa hello przyjmuje wejście wideo i tworzy plik JSON krój lokalizacji i obrazów jpg każdego wykryto twarzy na obrazie.</span><span class="sxs-lookup"><span data-stu-id="a04c0-140">hello **analyze** pass of hello two-pass workflow takes a video input and produces a JSON file of face locations, and jpg images of each detected face.</span></span>

| <span data-ttu-id="a04c0-141">Etap</span><span class="sxs-lookup"><span data-stu-id="a04c0-141">Stage</span></span> | <span data-ttu-id="a04c0-142">Nazwa pliku</span><span class="sxs-lookup"><span data-stu-id="a04c0-142">File Name</span></span> | <span data-ttu-id="a04c0-143">Uwagi</span><span class="sxs-lookup"><span data-stu-id="a04c0-143">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a04c0-144">Wejściowy zasobów</span><span class="sxs-lookup"><span data-stu-id="a04c0-144">Input asset</span></span> |<span data-ttu-id="a04c0-145">foo.bar</span><span class="sxs-lookup"><span data-stu-id="a04c0-145">foo.bar</span></span> |<span data-ttu-id="a04c0-146">Wideo w formacie WMV, MPV lub MP4</span><span class="sxs-lookup"><span data-stu-id="a04c0-146">Video in WMV, MPV, or MP4 format</span></span> |
| <span data-ttu-id="a04c0-147">Dane wejściowe konfiguracji</span><span class="sxs-lookup"><span data-stu-id="a04c0-147">Input config</span></span> |<span data-ttu-id="a04c0-148">Zadania konfiguracji ustawień wstępnych.</span><span class="sxs-lookup"><span data-stu-id="a04c0-148">Job configuration preset</span></span> |<span data-ttu-id="a04c0-149">{"version": "1.0", "Opcje": {'mode': "analizowanie"}}</span><span class="sxs-lookup"><span data-stu-id="a04c0-149">{'version':'1.0', 'options': {'mode':'analyze'}}</span></span> |
| <span data-ttu-id="a04c0-150">Dane wyjściowe zasobów</span><span class="sxs-lookup"><span data-stu-id="a04c0-150">Output asset</span></span> |<span data-ttu-id="a04c0-151">foo_annotations.JSON</span><span class="sxs-lookup"><span data-stu-id="a04c0-151">foo_annotations.json</span></span> |<span data-ttu-id="a04c0-152">Adnotacja danych lokalizacji krój w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="a04c0-152">Annotation data of face locations in JSON format.</span></span> <span data-ttu-id="a04c0-153">To mogą je edytować hello użytkownika toomodify hello rozmycia ograniczenia pola.</span><span class="sxs-lookup"><span data-stu-id="a04c0-153">This can be edited by hello user toomodify hello blurring bounding boxes.</span></span> <span data-ttu-id="a04c0-154">Zobacz poniższy przykład.</span><span class="sxs-lookup"><span data-stu-id="a04c0-154">See sample below.</span></span> |
| <span data-ttu-id="a04c0-155">Dane wyjściowe zasobów</span><span class="sxs-lookup"><span data-stu-id="a04c0-155">Output asset</span></span> |<span data-ttu-id="a04c0-156">foo_thumb%06d.jpg [foo_thumb000001.jpg, foo_thumb000002.jpg]</span><span class="sxs-lookup"><span data-stu-id="a04c0-156">foo_thumb%06d.jpg [foo_thumb000001.jpg, foo_thumb000002.jpg]</span></span> |<span data-ttu-id="a04c0-157">Przycięty jpg każdego wykryto krój, gdzie numer hello wskazuje etykiety hello hello powierzchni</span><span class="sxs-lookup"><span data-stu-id="a04c0-157">A cropped jpg of each detected face, where hello number indicates hello labelId of hello face</span></span> |

#### <a name="output-example"></a><span data-ttu-id="a04c0-158">Przykład danych wyjściowych:</span><span class="sxs-lookup"><span data-stu-id="a04c0-158">Output example:</span></span>

    {
      "version": 1,
      "timescale": 24000,
      "offset": 0,
      "framerate": 23.976,
      "width": 1280,
      "height": 720,
      "fragments": [
        {
          "start": 0,
          "duration": 48048,
          "interval": 1001,
          "events": [
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [],
            [
              {
                "index": 13,
                "id": 1138,
                "x": 0.29537,
                "y": -0.18987,
                "width": 0.36239,
                "height": 0.80335
              },
              {
                "index": 13,
                "id": 2028,
                "x": 0.60427,
                "y": 0.16098,
                "width": 0.26958,
                "height": 0.57943
              }
            ],

    … truncated

### <a name="redact-mode"></a><span data-ttu-id="a04c0-159">Redagowanie tryb</span><span class="sxs-lookup"><span data-stu-id="a04c0-159">Redact mode</span></span>
<span data-ttu-id="a04c0-160">drugi przebieg przepływu pracy hello Hello ma większą liczbę wejść, które muszą być połączone w jeden zasobów.</span><span class="sxs-lookup"><span data-stu-id="a04c0-160">hello second pass of hello workflow takes a larger number of inputs that must be combined into a single asset.</span></span>

<span data-ttu-id="a04c0-161">W tym listę identyfikatorów tooblur hello oryginalnego wideo i adnotacje hello JSON.</span><span class="sxs-lookup"><span data-stu-id="a04c0-161">This includes a list of IDs tooblur, hello original video, and hello annotations JSON.</span></span> <span data-ttu-id="a04c0-162">W tym trybie używa hello adnotacje tooapply rozmycia na powitania wejściowy plik wideo.</span><span class="sxs-lookup"><span data-stu-id="a04c0-162">This mode uses hello annotations tooapply blurring on hello input video.</span></span>

<span data-ttu-id="a04c0-163">Witaj dane wyjściowe z przebiegu Analizuj hello nie obejmuje hello oryginalnego wideo.</span><span class="sxs-lookup"><span data-stu-id="a04c0-163">hello output from hello Analyze pass does not include hello original video.</span></span> <span data-ttu-id="a04c0-164">Witaj wideo musi toobe przekazany do zasobów wejściowych hello hello Redact tryb zadania i wybranych jako plik podstawowy hello.</span><span class="sxs-lookup"><span data-stu-id="a04c0-164">hello video needs toobe uploaded into hello input asset for hello Redact mode task and selected as hello primary file.</span></span>

| <span data-ttu-id="a04c0-165">Etap</span><span class="sxs-lookup"><span data-stu-id="a04c0-165">Stage</span></span> | <span data-ttu-id="a04c0-166">Nazwa pliku</span><span class="sxs-lookup"><span data-stu-id="a04c0-166">File Name</span></span> | <span data-ttu-id="a04c0-167">Uwagi</span><span class="sxs-lookup"><span data-stu-id="a04c0-167">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a04c0-168">Wejściowy zasobów</span><span class="sxs-lookup"><span data-stu-id="a04c0-168">Input asset</span></span> |<span data-ttu-id="a04c0-169">foo.bar</span><span class="sxs-lookup"><span data-stu-id="a04c0-169">foo.bar</span></span> |<span data-ttu-id="a04c0-170">Wideo w formacie WMV, MPV lub MP4.</span><span class="sxs-lookup"><span data-stu-id="a04c0-170">Video in WMV, MPV, or MP4 format.</span></span> <span data-ttu-id="a04c0-171">Taka sama jak w kroku 1 wideo.</span><span class="sxs-lookup"><span data-stu-id="a04c0-171">Same video as in step 1.</span></span> |
| <span data-ttu-id="a04c0-172">Wejściowy zasobów</span><span class="sxs-lookup"><span data-stu-id="a04c0-172">Input asset</span></span> |<span data-ttu-id="a04c0-173">foo_annotations.JSON</span><span class="sxs-lookup"><span data-stu-id="a04c0-173">foo_annotations.json</span></span> |<span data-ttu-id="a04c0-174">Plik metadanych adnotacje z fazy, bez modyfikacji opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="a04c0-174">annotations metadata file from phase one, with optional modifications.</span></span> |
| <span data-ttu-id="a04c0-175">Wejściowy zasobów</span><span class="sxs-lookup"><span data-stu-id="a04c0-175">Input asset</span></span> |<span data-ttu-id="a04c0-176">foo_IDList.txt (opcjonalnie)</span><span class="sxs-lookup"><span data-stu-id="a04c0-176">foo_IDList.txt (Optional)</span></span> |<span data-ttu-id="a04c0-177">Lista krój tooredact identyfikatorów rozdzielonych opcjonalne nowy wiersz.</span><span class="sxs-lookup"><span data-stu-id="a04c0-177">Optional new line separated list of face IDs tooredact.</span></span> <span data-ttu-id="a04c0-178">Jeśli pole pozostanie puste, to rozmywa wszystkich powierzchni.</span><span class="sxs-lookup"><span data-stu-id="a04c0-178">If left blank, this blurs all faces.</span></span> |
| <span data-ttu-id="a04c0-179">Dane wejściowe konfiguracji</span><span class="sxs-lookup"><span data-stu-id="a04c0-179">Input config</span></span> |<span data-ttu-id="a04c0-180">Zadania konfiguracji ustawień wstępnych.</span><span class="sxs-lookup"><span data-stu-id="a04c0-180">Job configuration preset</span></span> |<span data-ttu-id="a04c0-181">{"version": "1.0", "Opcje": {'mode': "redagowanie"}}</span><span class="sxs-lookup"><span data-stu-id="a04c0-181">{'version':'1.0', 'options': {'mode':'redact'}}</span></span> |
| <span data-ttu-id="a04c0-182">Dane wyjściowe zasobów</span><span class="sxs-lookup"><span data-stu-id="a04c0-182">Output asset</span></span> |<span data-ttu-id="a04c0-183">foo_redacted.mp4</span><span class="sxs-lookup"><span data-stu-id="a04c0-183">foo_redacted.mp4</span></span> |<span data-ttu-id="a04c0-184">Wideo z rozmycia stosowane w oparciu adnotacji</span><span class="sxs-lookup"><span data-stu-id="a04c0-184">Video with blurring applied based on annotations</span></span> |

#### <a name="example-output"></a><span data-ttu-id="a04c0-185">Przykładowe dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="a04c0-185">Example output</span></span>
<span data-ttu-id="a04c0-186">Jest to hello IDList z jednego Identyfikatora zaznaczone dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="a04c0-186">This is hello output from an IDList with one ID selected.</span></span>

[<span data-ttu-id="a04c0-187">Wyświetl ten film</span><span class="sxs-lookup"><span data-stu-id="a04c0-187">view this video</span></span>](http://ampdemo.azureedge.net/?url=http%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fad6e24a2-4f9c-46ee-9fa7-bf05e20d19ac%2Fdance_redacted1.mp4)

<span data-ttu-id="a04c0-188">Przykład foo_IDList.txt</span><span class="sxs-lookup"><span data-stu-id="a04c0-188">Example foo_IDList.txt</span></span>
 
     1
     2
     3

## <a name="blur-types"></a><span data-ttu-id="a04c0-189">Rozmywa typów</span><span class="sxs-lookup"><span data-stu-id="a04c0-189">Blur types</span></span>

<span data-ttu-id="a04c0-190">W hello **nomenklatury** lub **Redact** trybie 5 tryby różnych rozmycia są dostępne za pośrednictwem wejściowych konfiguracji JSON hello: **małej**, **Med**, **Wysokiej**, **debugowania**, i **czarne**.</span><span class="sxs-lookup"><span data-stu-id="a04c0-190">In hello **Combined** or **Redact** mode, there are 5 different blur modes you can choose from via hello JSON input configuration: **Low**, **Med**, **High**, **Debug**, and **Black**.</span></span> <span data-ttu-id="a04c0-191">Domyślnie **Med** jest używany.</span><span class="sxs-lookup"><span data-stu-id="a04c0-191">By default **Med** is used.</span></span>

<span data-ttu-id="a04c0-192">Można okaże się, że przykłady hello rozmycia typy poniżej.</span><span class="sxs-lookup"><span data-stu-id="a04c0-192">You can find samples of hello blur types below.</span></span>

### <a name="example-json"></a><span data-ttu-id="a04c0-193">Przykład JSON:</span><span class="sxs-lookup"><span data-stu-id="a04c0-193">Example JSON:</span></span>

    {'version':'1.0', 'options': {'Mode': 'Combined', 'BlurType': 'High'}}

#### <a name="low"></a><span data-ttu-id="a04c0-194">Niska</span><span class="sxs-lookup"><span data-stu-id="a04c0-194">Low</span></span>

![Niska](./media/media-services-face-redaction/blur1.png)
 
#### <a name="med"></a><span data-ttu-id="a04c0-196">MED</span><span class="sxs-lookup"><span data-stu-id="a04c0-196">Med</span></span>

![MED](./media/media-services-face-redaction/blur2.png)

#### <a name="high"></a><span data-ttu-id="a04c0-198">Wysoka</span><span class="sxs-lookup"><span data-stu-id="a04c0-198">High</span></span>

![Wysoka](./media/media-services-face-redaction/blur3.png)

#### <a name="debug"></a><span data-ttu-id="a04c0-200">Debugowanie</span><span class="sxs-lookup"><span data-stu-id="a04c0-200">Debug</span></span>

![Debugowanie](./media/media-services-face-redaction/blur4.png)

#### <a name="black"></a><span data-ttu-id="a04c0-202">Czarny</span><span class="sxs-lookup"><span data-stu-id="a04c0-202">Black</span></span>

![Czarny](./media/media-services-face-redaction/blur5.png)

## <a name="elements-of-hello-output-json-file"></a><span data-ttu-id="a04c0-204">Elementy hello pliku wyjściowego w formacie JSON</span><span class="sxs-lookup"><span data-stu-id="a04c0-204">Elements of hello output JSON file</span></span>

<span data-ttu-id="a04c0-205">Hello redakcyjne pakiet administracyjny zawiera wysokiej precyzji krój lokalizacji wykrywania i śledzenia, która wykrywa się too64 kroje ludzkich w ramce wideo.</span><span class="sxs-lookup"><span data-stu-id="a04c0-205">hello Redaction MP provides high precision face location detection and tracking that can detect up too64 human faces in a video frame.</span></span> <span data-ttu-id="a04c0-206">Kroje czołowego Podaj hello uzyskać jak najlepsze rezultaty, podczas boczne i małych powierzchni (mniej niż lub równa too24x24 pikseli) są trudne.</span><span class="sxs-lookup"><span data-stu-id="a04c0-206">Frontal faces provide hello best results, while side faces and small faces (less than or equal too24x24 pixels) are challenging.</span></span>

[!INCLUDE [media-services-analytics-output-json](../../includes/media-services-analytics-output-json.md)]

## <a name="net-sample-code"></a><span data-ttu-id="a04c0-207">.NET przykładowy kod</span><span class="sxs-lookup"><span data-stu-id="a04c0-207">.NET sample code</span></span>

<span data-ttu-id="a04c0-208">następujące Hello program pokazuje sposób:</span><span class="sxs-lookup"><span data-stu-id="a04c0-208">hello following program shows how to:</span></span>

1. <span data-ttu-id="a04c0-209">Utworzenie elementu zawartości i przesyłanie pliku multimediów do hello zawartości.</span><span class="sxs-lookup"><span data-stu-id="a04c0-209">Create an asset and upload a media file into hello asset.</span></span>
2. <span data-ttu-id="a04c0-210">Utwórz zadanie z zadaniem redakcyjne krój oparty na pliku konfiguracji, który zawiera hello następujące ustawienie wstępne json.</span><span class="sxs-lookup"><span data-stu-id="a04c0-210">Create a job with a face redaction task based on a configuration file that contains hello following json preset.</span></span> 
   
        {'version':'1.0', 'options': {'mode':'combined'}}
3. <span data-ttu-id="a04c0-211">Pobierz pliki w formacie JSON dane wyjściowe hello.</span><span class="sxs-lookup"><span data-stu-id="a04c0-211">Download hello output JSON files.</span></span> 

#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="a04c0-212">Tworzenie i konfigurowanie projektu programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a04c0-212">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="a04c0-213">Konfigurowanie środowiska projektowego i wypełnić plik app.config hello o informacje dotyczące połączenia, zgodnie z opisem w [tworzenia usługi Media Services z platformą .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="a04c0-213">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="a04c0-214">Przykład</span><span class="sxs-lookup"><span data-stu-id="a04c0-214">Example</span></span>

    using System;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Threading;
    using System.Threading.Tasks;

    namespace FaceRedaction
    {
        class Program
        {
        // Read values from hello App.config file.
        private static readonly string _AADTenantDomain =
            ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
            ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

        // Field for service context.
        private static CloudMediaContext _context = null;

        static void Main(string[] args)
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);

            // Run hello FaceRedaction job.
            var asset = RunFaceRedactionJob(@"C:\supportFiles\FaceRedaction\SomeFootage.mp4",
                        @"C:\supportFiles\FaceRedaction\config.json");

            // Download hello job output asset.
            DownloadAsset(asset, @"C:\supportFiles\FaceRedaction\Output");
        }

        static IAsset RunFaceRedactionJob(string inputMediaFilePath, string configurationFile)
        {
            // Create an asset and upload hello input media file toostorage.
            IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
            "My Face Redaction Input Asset",
            AssetCreationOptions.None);

            // Declare a new job.
            IJob job = _context.Jobs.Create("My Face Redaction Job");

            // Get a reference tooAzure Media Redactor.
            string MediaProcessorName = "Azure Media Redactor";

            var processor = GetLatestMediaProcessorByName(MediaProcessorName);

            // Read configuration from hello specified file.
            string configuration = File.ReadAllText(configurationFile);

            // Create a task with hello encoding details, using a string preset.
            ITask task = job.Tasks.AddNew("My Face Redaction Task",
            processor,
            configuration,
            TaskOptions.None);

            // Specify hello input asset.
            task.InputAssets.Add(asset);

            // Add an output asset toocontain hello results of hello job.
            task.OutputAssets.AddNew("My Face Redaction Output Asset", AssetCreationOptions.None);

            // Use hello following event handler toocheck job progress.  
            job.StateChanged += new EventHandler<JobStateChangedEventArgs>(StateChanged);

            // Launch hello job.
            job.Submit();

            // Check job execution and wait for job toofinish.
            Task progressJobTask = job.GetExecutionProgressTask(CancellationToken.None);

            progressJobTask.Wait();

            // If job state is Error, hello event handling
            // method for job progress should log errors.  Here we check
            // for error state and exit if needed.
            if (job.State == JobState.Error)
            {
            ErrorDetail error = job.Tasks.First().ErrorDetails.First();
            Console.WriteLine(string.Format("Error: {0}. {1}",
                            error.Code,
                            error.Message));
            return null;
            }

            return job.OutputMediaAssets[0];
        }

        static IAsset CreateAssetAndUploadSingleFile(string filePath, string assetName, AssetCreationOptions options)
        {
            IAsset asset = _context.Assets.Create(assetName, options);

            var assetFile = asset.AssetFiles.Create(Path.GetFileName(filePath));
            assetFile.Upload(filePath);

            return asset;
        }

        static void DownloadAsset(IAsset asset, string outputDirectory)
        {
            foreach (IAssetFile file in asset.AssetFiles)
            {
            file.Download(Path.Combine(outputDirectory, file.Name));
            }
        }

        static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
        {
            var processor = _context.MediaProcessors
            .Where(p => p.Name == mediaProcessorName)
            .ToList()
            .OrderBy(p => new Version(p.Version))
            .LastOrDefault();

            if (processor == null)
            throw new ArgumentException(string.Format("Unknown media processor",
                                   mediaProcessorName));

            return processor;
        }

        static private void StateChanged(object sender, JobStateChangedEventArgs e)
        {
            Console.WriteLine("Job state changed event:");
            Console.WriteLine("  Previous state: " + e.PreviousState);
            Console.WriteLine("  Current state: " + e.CurrentState);

            switch (e.CurrentState)
            {
            case JobState.Finished:
                Console.WriteLine();
                Console.WriteLine("Job is finished.");
                Console.WriteLine();
                break;
            case JobState.Canceling:
            case JobState.Queued:
            case JobState.Scheduled:
            case JobState.Processing:
                Console.WriteLine("Please wait...\n");
                break;
            case JobState.Canceled:
            case JobState.Error:
                // Cast sender as a job.
                IJob job = (IJob)sender;
                // Display or log error details as needed.
                // LogJobStop(job.Id);
                break;
            default:
                break;
            }
        }
        }
    }

## <a name="next-steps"></a><span data-ttu-id="a04c0-215">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a04c0-215">Next steps</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="a04c0-216">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="a04c0-216">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="a04c0-217">Powiązane linki</span><span class="sxs-lookup"><span data-stu-id="a04c0-217">Related links</span></span>
[<span data-ttu-id="a04c0-218">Przegląd analiz usługi Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="a04c0-218">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

[<span data-ttu-id="a04c0-219">W trakcie analizy multimediów Azure</span><span class="sxs-lookup"><span data-stu-id="a04c0-219">Azure Media Analytics demos</span></span>](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

