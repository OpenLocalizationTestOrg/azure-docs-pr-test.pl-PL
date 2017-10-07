---
title: "aaaDetect krój i emocji z analizy multimediów Azure | Dokumentacja firmy Microsoft"
description: "W tym temacie przedstawiono sposób skierowany toodetect i emocji z analizy multimediów Azure."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 5ca4692c-23f1-451d-9d82-cbc8bf0fd707
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/18/2017
ms.author: milanga;juliako;
ms.openlocfilehash: f58d81d82dde08a694cdb4d92c6bab6a40a9c157
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="detect-face-and-emotion-with-azure-media-analytics"></a><span data-ttu-id="409ae-103">Wykrywanie twarzy na obrazie i emocji z analizy multimediów Azure</span><span class="sxs-lookup"><span data-stu-id="409ae-103">Detect Face and Emotion with Azure Media Analytics</span></span>
## <a name="overview"></a><span data-ttu-id="409ae-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="409ae-104">Overview</span></span>
<span data-ttu-id="409ae-105">Witaj **Azure Media krój detektora** procesor multimediów (MP) pozwala toocount, przeniesień Śledź i nawet miernika odbiorców udziału i reakcji za pośrednictwem twarzy.</span><span class="sxs-lookup"><span data-stu-id="409ae-105">hello **Azure Media Face Detector** media processor (MP) enables you toocount, track movements, and even gauge audience participation and reaction via facial expressions.</span></span> <span data-ttu-id="409ae-106">Ta usługa zawiera dwie funkcje:</span><span class="sxs-lookup"><span data-stu-id="409ae-106">This service contains two features:</span></span> 

* <span data-ttu-id="409ae-107">**Wykrywanie twarzy na obrazie**</span><span class="sxs-lookup"><span data-stu-id="409ae-107">**Face detection**</span></span>
  
    <span data-ttu-id="409ae-108">Wykrywanie twarzy na obrazie znajduje i śledzi człowieka kroje w pliku wideo.</span><span class="sxs-lookup"><span data-stu-id="409ae-108">Face detection finds and tracks human faces within a video.</span></span> <span data-ttu-id="409ae-109">Wiele powierzchni mogą być wykrywane i następnie śledzenia przechodzą wokół, hello czas i lokalizację metadane zwrócony w pliku JSON.</span><span class="sxs-lookup"><span data-stu-id="409ae-109">Multiple faces can be detected and subsequently be tracked as they move around, with hello time and location metadata returned in a JSON file.</span></span> <span data-ttu-id="409ae-110">Podczas śledzenia podejmie toogive spójne toohello identyfikator sam stają przed podczas osoby hello jest przenoszenia na ekranie, nawet jeśli są zablokowane lub pozostaw krótko hello ramki.</span><span class="sxs-lookup"><span data-stu-id="409ae-110">During tracking, it will attempt toogive a consistent ID toohello same face while hello person is moving around on screen, even if they are obstructed or briefly leave hello frame.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="409ae-111">Ta usługa nie przeprowadza rozpoznawanie twarzy.</span><span class="sxs-lookup"><span data-stu-id="409ae-111">This service does not perform facial recognition.</span></span> <span data-ttu-id="409ae-112">Osoba, która pozostawia ramki hello lub staje się blokować dla zbyt długo będzie mógł skorzystać z nowym Identyfikatorem gdy zwracają.</span><span class="sxs-lookup"><span data-stu-id="409ae-112">An individual who leaves hello frame or becomes obstructed for too long will be given a new ID when they return.</span></span>
  > 
  > 
* <span data-ttu-id="409ae-113">**Wykrywanie emocji**</span><span class="sxs-lookup"><span data-stu-id="409ae-113">**Emotion detection**</span></span>
  
    <span data-ttu-id="409ae-114">Wykrywanie emocji jest opcjonalnym składnikiem hello procesor multimediów wykrywania twarzy na obrazie, które zwraca analizy na wiele atrybutów emocjonalne kroje hello wykryte, w tym szczęście, sadness, obawy i gniew.</span><span class="sxs-lookup"><span data-stu-id="409ae-114">Emotion Detection is an optional component of hello Face Detection Media Processor that returns analysis on multiple emotional attributes from hello faces detected, including happiness, sadness, fear, anger, and more.</span></span> 

<span data-ttu-id="409ae-115">Witaj **Azure Media krój detektora** pakiet administracyjny jest obecnie w przeglądzie.</span><span class="sxs-lookup"><span data-stu-id="409ae-115">hello **Azure Media Face Detector** MP is currently in Preview.</span></span>

<span data-ttu-id="409ae-116">Ten temat zawiera szczegółowe informacje o **Azure Media krój detektora** i przedstawia sposób toouse go przy użyciu zestawu SDK usługi Media Services dla platformy .NET.</span><span class="sxs-lookup"><span data-stu-id="409ae-116">This topic gives details about  **Azure Media Face Detector** and shows how toouse it with Media Services SDK for .NET.</span></span>

## <a name="face-detector-input-files"></a><span data-ttu-id="409ae-117">Stają przed detektora plików wejściowych</span><span class="sxs-lookup"><span data-stu-id="409ae-117">Face Detector input files</span></span>
<span data-ttu-id="409ae-118">Pliki wideo.</span><span class="sxs-lookup"><span data-stu-id="409ae-118">Video files.</span></span> <span data-ttu-id="409ae-119">Obecnie są obsługiwane następujące formaty hello: MP4, MOV i WMV.</span><span class="sxs-lookup"><span data-stu-id="409ae-119">Currently, hello following formats are supported: MP4, MOV, and WMV.</span></span>

## <a name="face-detector-output-files"></a><span data-ttu-id="409ae-120">Stają przed detektora pliki wyjściowe</span><span class="sxs-lookup"><span data-stu-id="409ae-120">Face Detector output files</span></span>
<span data-ttu-id="409ae-121">Hello krój wykrywania i śledzenia interfejsu API zapewnia wysokiej precyzji krój lokalizacji wykrywania i śledzenia wykrywające się too64 człowieka powierzchni wideo.</span><span class="sxs-lookup"><span data-stu-id="409ae-121">hello face detection and tracking API provides high precision face location detection and tracking that can detect up too64 human faces in a video.</span></span> <span data-ttu-id="409ae-122">Czołowego kroje Podaj hello uzyskać jak najlepsze rezultaty, podczas boczne i małych powierzchni (mniej niż lub równa too24x24 pikseli) nie może być tak dokładne.</span><span class="sxs-lookup"><span data-stu-id="409ae-122">Frontal faces provide hello best results, while side faces and small faces (less than or equal too24x24 pixels) might not be as accurate.</span></span>

<span data-ttu-id="409ae-123">Hello kroje wykryte i śledzonych są zwracane z współrzędne (po lewej, top, szerokość i wysokość) wskazujący lokalizację hello kroje hello obrazu w pikselach, a także krój identyfikator liczba wskazująca hello śledzenia tej osoby.</span><span class="sxs-lookup"><span data-stu-id="409ae-123">hello detected and tracked faces are returned with coordinates (left, top, width, and height) indicating hello location of faces in hello image in pixels, as well as a face ID number indicating hello tracking of that individual.</span></span> <span data-ttu-id="409ae-124">Numery identyfikatorów krój są podatne tooreset czynników podczas krój czołowego hello zostanie utracony lub pokrywający się w ramce hello spowodować, że niektóre osoby pobierania przypisanych wiele identyfikatorów.</span><span class="sxs-lookup"><span data-stu-id="409ae-124">Face ID numbers are prone tooreset under circumstances when hello frontal face is lost or overlapped in hello frame, resulting in some individuals getting assigned multiple IDs.</span></span>

## <span data-ttu-id="409ae-125"><a id="output_elements"></a>Elementy hello pliku wyjściowego w formacie JSON</span><span class="sxs-lookup"><span data-stu-id="409ae-125"><a id="output_elements"></a>Elements of hello output JSON file</span></span>

[!INCLUDE [media-services-analytics-output-json](../../includes/media-services-analytics-output-json.md)]

<span data-ttu-id="409ae-126">Wykrywanie twarzy na obrazie używa technik fragmentacji (gdzie hello metadanych można podzielić w oparte na czasie fragmentów i można pobrać tylko potrzebnych) i segmentacji (gdzie hello zdarzenia są podzielony na wypadek, gdyby otrzymują zbyt duży).</span><span class="sxs-lookup"><span data-stu-id="409ae-126">Face Detector uses techniques of fragmentation (where hello metadata can be broken up in time-based chunks and you can download only what you need), and segmentation (where hello events are broken up in case they get too large).</span></span> <span data-ttu-id="409ae-127">Niektórych prostych obliczeń może pomóc przekształcania danych hello.</span><span class="sxs-lookup"><span data-stu-id="409ae-127">Some simple calculations can help you transform hello data.</span></span> <span data-ttu-id="409ae-128">Na przykład, jeśli zdarzenie rozpoczęty o godzinie 6300 (znaczniki) z skali czasu 2997 (Takty/s) i szybkość klatek z 29,97 (ramek na sekundę), następnie:</span><span class="sxs-lookup"><span data-stu-id="409ae-128">For example, if an event started at 6300 (ticks), with a timescale of 2997 (ticks/sec) and framerate of 29.97 (frames/sec), then:</span></span>

* <span data-ttu-id="409ae-129">Start/skali czasu = sekund 2.1</span><span class="sxs-lookup"><span data-stu-id="409ae-129">Start/Timescale = 2.1 seconds</span></span>
* <span data-ttu-id="409ae-130">Sekundy x Framerate = 63 ramki</span><span class="sxs-lookup"><span data-stu-id="409ae-130">Seconds x Framerate = 63 frames</span></span>

## <a name="face-detection-input-and-output-example"></a><span data-ttu-id="409ae-131">Dostęp do danych wejściowych wykrywania i przykład danych wyjściowych</span><span class="sxs-lookup"><span data-stu-id="409ae-131">Face detection input and output example</span></span>
### <a name="input-video"></a><span data-ttu-id="409ae-132">Wejściowy plik wideo</span><span class="sxs-lookup"><span data-stu-id="409ae-132">Input video</span></span>
[<span data-ttu-id="409ae-133">Wejściowy plik wideo</span><span class="sxs-lookup"><span data-stu-id="409ae-133">Input Video</span></span>](http://ampdemo.azureedge.net/azuremediaplayer.html?url=https%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fc8834d9f-0b49-4b38-bcaf-ece2746f1972%2FMicrosoft%20Convergence%202015%20%20Keynote%20Highlights.ism%2Fmanifest&amp;autoplay=false)

### <a name="task-configuration-preset"></a><span data-ttu-id="409ae-134">Konfiguracja zadania (ustawienia domyślne)</span><span class="sxs-lookup"><span data-stu-id="409ae-134">Task configuration (preset)</span></span>
<span data-ttu-id="409ae-135">Podczas tworzenia zadania z **Azure Media krój detektora**, należy określić ustawienia domyślne konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="409ae-135">When creating a task with **Azure Media Face Detector**, you must specify a configuration preset.</span></span> <span data-ttu-id="409ae-136">Witaj następujące ustawienie konfiguracji jest tylko do wykrywania twarzy na obrazie.</span><span class="sxs-lookup"><span data-stu-id="409ae-136">hello following configuration preset is just for face detection.</span></span>

    {
      "version":"1.0",
      "options":{
          "TrackingMode": "Fast"
      }
    }

#### <a name="attribute-descriptions"></a><span data-ttu-id="409ae-137">Opisy atrybutów</span><span class="sxs-lookup"><span data-stu-id="409ae-137">Attribute descriptions</span></span>
| <span data-ttu-id="409ae-138">Nazwa atrybutu</span><span class="sxs-lookup"><span data-stu-id="409ae-138">Attribute name</span></span> | <span data-ttu-id="409ae-139">Opis</span><span class="sxs-lookup"><span data-stu-id="409ae-139">Description</span></span> |
| --- | --- |
| <span data-ttu-id="409ae-140">Tryb</span><span class="sxs-lookup"><span data-stu-id="409ae-140">Mode</span></span> |<span data-ttu-id="409ae-141">Fast — szybkiego przetwarzania szybkości, ale mniej dokładne (ustawienie domyślne).</span><span class="sxs-lookup"><span data-stu-id="409ae-141">Fast - fast processing speed, but less accurate (default).</span></span>|

### <a name="json-output"></a><span data-ttu-id="409ae-142">Dane wyjściowe JSON</span><span class="sxs-lookup"><span data-stu-id="409ae-142">JSON output</span></span>
<span data-ttu-id="409ae-143">Poniższy przykład danych wyjściowych JSON Hello została obcięta.</span><span class="sxs-lookup"><span data-stu-id="409ae-143">hello following example of JSON output was truncated.</span></span>

    {
    "version": 1,
    "timescale": 30000,
    "offset": 0,
    "framerate": 29.97,
    "width": 1280,
    "height": 720,
    "fragments": [
        {
        "start": 0,
        "duration": 60060
        },
        {
        "start": 60060,
        "duration": 60060,
        "interval": 1001,
        "events": [
            [
            {
                "id": 0,
                "x": 0.519531,
                "y": 0.180556,
                "width": 0.0867188,
                "height": 0.154167
            }
            ],
            [
            {
                "id": 0,
                "x": 0.517969,
                "y": 0.181944,
                "width": 0.0867188,
                "height": 0.154167
            }
            ],
            [
            {
                "id": 0,
                "x": 0.517187,
                "y": 0.183333,
                "width": 0.0851562,
                "height": 0.151389
            }
            ],

        . . . 

## <a name="emotion-detection-input-and-output-example"></a><span data-ttu-id="409ae-144">Wykrywanie emocji wejściowa i wyjściowa przykład</span><span class="sxs-lookup"><span data-stu-id="409ae-144">Emotion detection input and output example</span></span>
### <a name="input-video"></a><span data-ttu-id="409ae-145">Wejściowy plik wideo</span><span class="sxs-lookup"><span data-stu-id="409ae-145">Input video</span></span>
[<span data-ttu-id="409ae-146">Wejściowy plik wideo</span><span class="sxs-lookup"><span data-stu-id="409ae-146">Input Video</span></span>](http://ampdemo.azureedge.net/azuremediaplayer.html?url=https%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fc8834d9f-0b49-4b38-bcaf-ece2746f1972%2FMicrosoft%20Convergence%202015%20%20Keynote%20Highlights.ism%2Fmanifest&amp;autoplay=false)

### <a name="task-configuration-preset"></a><span data-ttu-id="409ae-147">Konfiguracja zadania (ustawienia domyślne)</span><span class="sxs-lookup"><span data-stu-id="409ae-147">Task configuration (preset)</span></span>
<span data-ttu-id="409ae-148">Podczas tworzenia zadania z **Azure Media krój detektora**, należy określić ustawienia domyślne konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="409ae-148">When creating a task with **Azure Media Face Detector**, you must specify a configuration preset.</span></span> <span data-ttu-id="409ae-149">Witaj następujące ustawienie konfiguracji określa toocreate JSON oparta na powitania emocji wykrywania.</span><span class="sxs-lookup"><span data-stu-id="409ae-149">hello following configuration preset specifies toocreate JSON based on hello emotion detection.</span></span>

    {
      "version": "1.0",
      "options": {
        "aggregateEmotionWindowMs": "987",
        "mode": "aggregateEmotion",
        "aggregateEmotionIntervalMs": "342"
      }
    }


#### <a name="attribute-descriptions"></a><span data-ttu-id="409ae-150">Opisy atrybutów</span><span class="sxs-lookup"><span data-stu-id="409ae-150">Attribute descriptions</span></span>
| <span data-ttu-id="409ae-151">Nazwa atrybutu</span><span class="sxs-lookup"><span data-stu-id="409ae-151">Attribute name</span></span> | <span data-ttu-id="409ae-152">Opis</span><span class="sxs-lookup"><span data-stu-id="409ae-152">Description</span></span> |
| --- | --- |
| <span data-ttu-id="409ae-153">Tryb</span><span class="sxs-lookup"><span data-stu-id="409ae-153">Mode</span></span> |<span data-ttu-id="409ae-154">Kroje: Tylko stają przed wykrywania.</span><span class="sxs-lookup"><span data-stu-id="409ae-154">Faces: Only face detection.</span></span><br/><span data-ttu-id="409ae-155">PerFaceEmotion: Zwraca emocji osobno dla każdej wykrywania twarzy na obrazie.</span><span class="sxs-lookup"><span data-stu-id="409ae-155">PerFaceEmotion: Return emotion independently for each face detection.</span></span><br/><span data-ttu-id="409ae-156">AggregateEmotion: Wartości zwracane emocji średni wszystkie powierzchnie w ramce.</span><span class="sxs-lookup"><span data-stu-id="409ae-156">AggregateEmotion: Return average emotion values for all faces in frame.</span></span> |
| <span data-ttu-id="409ae-157">AggregateEmotionWindowMs</span><span class="sxs-lookup"><span data-stu-id="409ae-157">AggregateEmotionWindowMs</span></span> |<span data-ttu-id="409ae-158">Użyj, jeśli wybrany tryb AggregateEmotion.</span><span class="sxs-lookup"><span data-stu-id="409ae-158">Use if AggregateEmotion mode selected.</span></span> <span data-ttu-id="409ae-159">Określa długość hello wideo tooproduce używane łączny wynik, w milisekundach.</span><span class="sxs-lookup"><span data-stu-id="409ae-159">Specifies hello length of video used tooproduce each aggregate result, in milliseconds.</span></span> |
| <span data-ttu-id="409ae-160">AggregateEmotionIntervalMs</span><span class="sxs-lookup"><span data-stu-id="409ae-160">AggregateEmotionIntervalMs</span></span> |<span data-ttu-id="409ae-161">Użyj, jeśli wybrany tryb AggregateEmotion.</span><span class="sxs-lookup"><span data-stu-id="409ae-161">Use if AggregateEmotion mode selected.</span></span> <span data-ttu-id="409ae-162">Określa, z jakiego agregacji tooproduce częstotliwość powoduje.</span><span class="sxs-lookup"><span data-stu-id="409ae-162">Specifies with what frequency tooproduce aggregate results.</span></span> |

#### <a name="aggregate-defaults"></a><span data-ttu-id="409ae-163">Łączny wartości domyślnych</span><span class="sxs-lookup"><span data-stu-id="409ae-163">Aggregate defaults</span></span>
<span data-ttu-id="409ae-164">Poniżej są zalecane wartości hello okna agregacji i ustawienia interwału.</span><span class="sxs-lookup"><span data-stu-id="409ae-164">Below are recommended values for hello aggregate window and interval settings.</span></span> <span data-ttu-id="409ae-165">AggregateEmotionWindowMs powinien być dłuższy niż AggregateEmotionIntervalMs.</span><span class="sxs-lookup"><span data-stu-id="409ae-165">AggregateEmotionWindowMs should be longer than AggregateEmotionIntervalMs.</span></span>

|| <span data-ttu-id="409ae-166">Ustawienia domyślne (s)</span><span class="sxs-lookup"><span data-stu-id="409ae-166">Defaults(s)</span></span> | <span data-ttu-id="409ae-167">Min(s)</span><span class="sxs-lookup"><span data-stu-id="409ae-167">Min(s)</span></span> | <span data-ttu-id="409ae-168">MAX(s)</span><span class="sxs-lookup"><span data-stu-id="409ae-168">Max(s)</span></span> |
|--- | --- | --- | --- |
| <span data-ttu-id="409ae-169">AggregateEmotionWindowMs</span><span class="sxs-lookup"><span data-stu-id="409ae-169">AggregateEmotionWindowMs</span></span> |<span data-ttu-id="409ae-170">0.5</span><span class="sxs-lookup"><span data-stu-id="409ae-170">0.5</span></span> |<span data-ttu-id="409ae-171">2</span><span class="sxs-lookup"><span data-stu-id="409ae-171">2</span></span> |<span data-ttu-id="409ae-172">0.25</span><span class="sxs-lookup"><span data-stu-id="409ae-172">0.25</span></span>|
| <span data-ttu-id="409ae-173">AggregateEmotionIntervalMs</span><span class="sxs-lookup"><span data-stu-id="409ae-173">AggregateEmotionIntervalMs</span></span> |<span data-ttu-id="409ae-174">0.5</span><span class="sxs-lookup"><span data-stu-id="409ae-174">0.5</span></span> |<span data-ttu-id="409ae-175">1</span><span class="sxs-lookup"><span data-stu-id="409ae-175">1</span></span> |<span data-ttu-id="409ae-176">0.25</span><span class="sxs-lookup"><span data-stu-id="409ae-176">0.25</span></span>|

### <a name="json-output"></a><span data-ttu-id="409ae-177">Dane wyjściowe JSON</span><span class="sxs-lookup"><span data-stu-id="409ae-177">JSON output</span></span>
<span data-ttu-id="409ae-178">Dane wyjściowe dla agregacji emocji (obcięty) JSON:</span><span class="sxs-lookup"><span data-stu-id="409ae-178">JSON output for aggregate emotion (truncated):</span></span>

    {
     "version": 1,
     "timescale": 30000,
     "offset": 0,
     "framerate": 29.97,
     "width": 1280,
     "height": 720,
     "fragments": [
       {
         "start": 0,
         "duration": 60060,
         "interval": 15015,
         "events": [
           [
             {
               "windowFaceDistribution": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               },
               "windowMeanScores": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               }
             }
           ],
           [
             {
               "windowFaceDistribution": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               },
               "windowMeanScores": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               }
             }
           ],
           [
             {
               "windowFaceDistribution": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               },
               "windowMeanScores": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               }
             }
           ],
           [
             {
               "windowFaceDistribution": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               },
               "windowMeanScores": {
                 "neutral": 0,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               }
             }
           ]
         ]
       },
       {
         "start": 60060,
         "duration": 60060,
         "interval": 15015,
         "events": [
           [
             {
               "windowFaceDistribution": {
                 "neutral": 1,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,
                 "contempt": 0
               },
               "windowMeanScores": {
                 "neutral": 0.688541,
                 "happiness": 0.0586323,
                 "surprise": 0.227184,
                 "sadness": 0.00945675,
                 "anger": 0.00592107,
                 "disgust": 0.00154993,
                 "fear": 0.00450447,
                 "contempt": 0.0042109
               }
             }
           ],
           [
             {
               "windowFaceDistribution": {
                 "neutral": 1,
                 "happiness": 0,
                 "surprise": 0,
                 "sadness": 0,
                 "anger": 0,
                 "disgust": 0,
                 "fear": 0,

## <a name="limitations"></a><span data-ttu-id="409ae-179">Ograniczenia</span><span class="sxs-lookup"><span data-stu-id="409ae-179">Limitations</span></span>
* <span data-ttu-id="409ae-180">formatów wejściowych wideo Hello obsługiwane obejmują MP4, MOV i WMV.</span><span class="sxs-lookup"><span data-stu-id="409ae-180">hello supported input video formats include MP4, MOV, and WMV.</span></span>
* <span data-ttu-id="409ae-181">Witaj wykrywalny krój rozmiar zakres jest 24 x 24 too2048x2048 piksele.</span><span class="sxs-lookup"><span data-stu-id="409ae-181">hello detectable face size range is 24x24 too2048x2048 pixels.</span></span> <span data-ttu-id="409ae-182">nie są wykrywane kroje Hello poza tym zakresem.</span><span class="sxs-lookup"><span data-stu-id="409ae-182">hello faces out of this range will not be detected.</span></span>
* <span data-ttu-id="409ae-183">Dla każdego wideo hello maksymalna liczba kroje zwrócił wynosi 64.</span><span class="sxs-lookup"><span data-stu-id="409ae-183">For each video, hello maximum number of faces returned is 64.</span></span>
* <span data-ttu-id="409ae-184">Niektóre kroje mogą nie być wykrywane powodu wyzwania tootechnical; np. w przypadku bardzo dużych kąty przedniej (head ułożenia) i dużych zamknięcia.</span><span class="sxs-lookup"><span data-stu-id="409ae-184">Some faces may not be detected due tootechnical challenges; e.g. very large face angles (head-pose), and large occlusion.</span></span> <span data-ttu-id="409ae-185">Kroje czołowego i niemal czołowego ma hello najlepsze wyniki.</span><span class="sxs-lookup"><span data-stu-id="409ae-185">Frontal and near-frontal faces have hello best results.</span></span>

## <a name="net-sample-code"></a><span data-ttu-id="409ae-186">.NET przykładowy kod</span><span class="sxs-lookup"><span data-stu-id="409ae-186">.NET sample code</span></span>

<span data-ttu-id="409ae-187">następujące Hello program pokazuje sposób:</span><span class="sxs-lookup"><span data-stu-id="409ae-187">hello following program shows how to:</span></span>

1. <span data-ttu-id="409ae-188">Utworzenie elementu zawartości i przesyłanie pliku multimediów do hello zawartości.</span><span class="sxs-lookup"><span data-stu-id="409ae-188">Create an asset and upload a media file into hello asset.</span></span>
2. <span data-ttu-id="409ae-189">Utwórz zadanie z zadania wykrywania twarzy na obrazie w zależności od pliku konfiguracji, który zawiera hello następujące ustawienie wstępne json.</span><span class="sxs-lookup"><span data-stu-id="409ae-189">Create a job with a face detection task based on a configuration file that contains hello following json preset.</span></span> 
   
        {
            "version": "1.0"
        }
3. <span data-ttu-id="409ae-190">Pobierz pliki w formacie JSON dane wyjściowe hello.</span><span class="sxs-lookup"><span data-stu-id="409ae-190">Download hello output JSON files.</span></span> 

#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="409ae-191">Tworzenie i konfigurowanie projektu programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="409ae-191">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="409ae-192">Konfigurowanie środowiska projektowego i wypełnić plik app.config hello o informacje dotyczące połączenia, zgodnie z opisem w [tworzenia usługi Media Services z platformą .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="409ae-192">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="409ae-193">Przykład</span><span class="sxs-lookup"><span data-stu-id="409ae-193">Example</span></span>

    using System;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Threading;
    using System.Threading.Tasks;

    namespace FaceDetection
    {
        class Program
        {
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

                // Run hello FaceDetection job.
                var asset = RunFaceDetectionJob(@"C:\supportFiles\FaceDetection\BigBuckBunny.mp4",
                                            @"C:\supportFiles\FaceDetection\config.json");

                // Download hello job output asset.
                DownloadAsset(asset, @"C:\supportFiles\FaceDetection\Output");
            }

            static IAsset RunFaceDetectionJob(string inputMediaFilePath, string configurationFile)
            {
                // Create an asset and upload hello input media file toostorage.
                IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
                    "My Face Detection Input Asset",
                    AssetCreationOptions.None);

                // Declare a new job.
                IJob job = _context.Jobs.Create("My Face Detection Job");

                // Get a reference tooAzure Media Face Detector.
                string MediaProcessorName = "Azure Media Face Detector";

                var processor = GetLatestMediaProcessorByName(MediaProcessorName);

                // Read configuration from hello specified file.
                string configuration = File.ReadAllText(configurationFile);

                // Create a task with hello encoding details, using a string preset.
                ITask task = job.Tasks.AddNew("My Face Detection Task",
                    processor,
                    configuration,
                    TaskOptions.None);

                // Specify hello input asset.
                task.InputAssets.Add(asset);

                // Add an output asset toocontain hello results of hello job.
                task.OutputAssets.AddNew("My Face Detectoion Output Asset", AssetCreationOptions.None);

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

## <a name="media-services-learning-paths"></a><span data-ttu-id="409ae-194">Ścieżki szkoleniowe dotyczące usługi Media Services</span><span class="sxs-lookup"><span data-stu-id="409ae-194">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="409ae-195">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="409ae-195">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="409ae-196">Powiązane linki</span><span class="sxs-lookup"><span data-stu-id="409ae-196">Related links</span></span>
[<span data-ttu-id="409ae-197">Przegląd analiz usługi Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="409ae-197">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

[<span data-ttu-id="409ae-198">W trakcie analizy multimediów Azure</span><span class="sxs-lookup"><span data-stu-id="409ae-198">Azure Media Analytics demos</span></span>](http://amslabs.azurewebsites.net/demos/Analytics.html)

