---
title: "Wykrywanie twarzy na obrazie i emocji z analizy multimediów Azure | Dokumentacja firmy Microsoft"
description: "W tym temacie przedstawiono sposób wykrywania kroje i emocji z analizy multimediów Azure."
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
ms.openlocfilehash: d7f3bc6c0d21db7adbb0c16c752d4ce49e99da5a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="detect-face-and-emotion-with-azure-media-analytics"></a><span data-ttu-id="97980-103">Wykrywanie twarzy na obrazie i emocji z analizy multimediów Azure</span><span class="sxs-lookup"><span data-stu-id="97980-103">Detect Face and Emotion with Azure Media Analytics</span></span>
## <a name="overview"></a><span data-ttu-id="97980-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="97980-104">Overview</span></span>
<span data-ttu-id="97980-105">**Azure Media krój detektora** procesor multimediów (MP) umożliwia count, śledzić przeniesień i nawet określić udział odbiorców i reakcji za pośrednictwem twarzy.</span><span class="sxs-lookup"><span data-stu-id="97980-105">The **Azure Media Face Detector** media processor (MP) enables you to count, track movements, and even gauge audience participation and reaction via facial expressions.</span></span> <span data-ttu-id="97980-106">Ta usługa zawiera dwie funkcje:</span><span class="sxs-lookup"><span data-stu-id="97980-106">This service contains two features:</span></span> 

* <span data-ttu-id="97980-107">**Wykrywanie twarzy na obrazie**</span><span class="sxs-lookup"><span data-stu-id="97980-107">**Face detection**</span></span>
  
    <span data-ttu-id="97980-108">Wykrywanie twarzy na obrazie znajduje i śledzi człowieka kroje w pliku wideo.</span><span class="sxs-lookup"><span data-stu-id="97980-108">Face detection finds and tracks human faces within a video.</span></span> <span data-ttu-id="97980-109">Wiele powierzchni mogą być wykrywane i następnie śledzenia przechodzą wokół, czas i lokalizację metadanymi zwrócił w pliku JSON.</span><span class="sxs-lookup"><span data-stu-id="97980-109">Multiple faces can be detected and subsequently be tracked as they move around, with the time and location metadata returned in a JSON file.</span></span> <span data-ttu-id="97980-110">Podczas śledzenia podejmie ma zostać przypisany do tej samej kroju spójny identyfikator, gdy osoba jest przenoszenia na ekranie, nawet jeśli są zablokowane lub pozostaw krótko ramki.</span><span class="sxs-lookup"><span data-stu-id="97980-110">During tracking, it will attempt to give a consistent ID to the same face while the person is moving around on screen, even if they are obstructed or briefly leave the frame.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="97980-111">Ta usługa nie przeprowadza rozpoznawanie twarzy.</span><span class="sxs-lookup"><span data-stu-id="97980-111">This service does not perform facial recognition.</span></span> <span data-ttu-id="97980-112">Osoba, która pozostawia ramki lub staje się blokować dla zbyt długo będzie mógł skorzystać z nowym Identyfikatorem gdy zwracają.</span><span class="sxs-lookup"><span data-stu-id="97980-112">An individual who leaves the frame or becomes obstructed for too long will be given a new ID when they return.</span></span>
  > 
  > 
* <span data-ttu-id="97980-113">**Wykrywanie emocji**</span><span class="sxs-lookup"><span data-stu-id="97980-113">**Emotion detection**</span></span>
  
    <span data-ttu-id="97980-114">Wykrywanie emocji jest opcjonalnym składnikiem procesor multimediów wykrywania twarzy na obrazie, które zwraca analizy na wiele atrybutów emocjonalne kroje wykryte, w tym szczęście, sadness, obawy i gniew.</span><span class="sxs-lookup"><span data-stu-id="97980-114">Emotion Detection is an optional component of the Face Detection Media Processor that returns analysis on multiple emotional attributes from the faces detected, including happiness, sadness, fear, anger, and more.</span></span> 

<span data-ttu-id="97980-115">**Azure Media krój detektora** pakiet administracyjny jest obecnie w przeglądzie.</span><span class="sxs-lookup"><span data-stu-id="97980-115">The **Azure Media Face Detector** MP is currently in Preview.</span></span>

<span data-ttu-id="97980-116">Ten temat zawiera szczegółowe informacje o **Azure Media krój detektora** i pokazuje, jak z niego korzystać z zestawu SDK usługi Media Services dla platformy .NET.</span><span class="sxs-lookup"><span data-stu-id="97980-116">This topic gives details about  **Azure Media Face Detector** and shows how to use it with Media Services SDK for .NET.</span></span>

## <a name="face-detector-input-files"></a><span data-ttu-id="97980-117">Stają przed detektora plików wejściowych</span><span class="sxs-lookup"><span data-stu-id="97980-117">Face Detector input files</span></span>
<span data-ttu-id="97980-118">Pliki wideo.</span><span class="sxs-lookup"><span data-stu-id="97980-118">Video files.</span></span> <span data-ttu-id="97980-119">Obecnie obsługiwane są następujące formaty: MP4, MOV i WMV.</span><span class="sxs-lookup"><span data-stu-id="97980-119">Currently, the following formats are supported: MP4, MOV, and WMV.</span></span>

## <a name="face-detector-output-files"></a><span data-ttu-id="97980-120">Stają przed detektora pliki wyjściowe</span><span class="sxs-lookup"><span data-stu-id="97980-120">Face Detector output files</span></span>
<span data-ttu-id="97980-121">Interfejsu API śledzenia i wykrywania twarzy na obrazie zapewnia wysokiej precyzji krój lokalizacji wykrywania i śledzenia wykrywające maksymalnie 64 kroje człowieka wideo.</span><span class="sxs-lookup"><span data-stu-id="97980-121">The face detection and tracking API provides high precision face location detection and tracking that can detect up to 64 human faces in a video.</span></span> <span data-ttu-id="97980-122">Kroje czołowego Podaj najlepsze wyniki, podczas boczne i w małych kroje (mniejsze niż lub równe 24 x 24 piksele) może nie być tak dokładne.</span><span class="sxs-lookup"><span data-stu-id="97980-122">Frontal faces provide the best results, while side faces and small faces (less than or equal to 24x24 pixels) might not be as accurate.</span></span>

<span data-ttu-id="97980-123">Kroje wykryte i śledzonych są zwracane z współrzędne (po lewej, top, szerokość i wysokość) wskazujący lokalizację kroje obrazu w pikselach, a także numer identyfikacyjny krój, wskazując śledzenia tej osoby.</span><span class="sxs-lookup"><span data-stu-id="97980-123">The detected and tracked faces are returned with coordinates (left, top, width, and height) indicating the location of faces in the image in pixels, as well as a face ID number indicating the tracking of that individual.</span></span> <span data-ttu-id="97980-124">Numery identyfikatorów krój są podatne na zresetować w sytuacji, gdy czołowego kroju zostanie utracony lub pokrywający się w ramce spowodować, że niektóre osoby pobierania przypisanych wiele identyfikatorów.</span><span class="sxs-lookup"><span data-stu-id="97980-124">Face ID numbers are prone to reset under circumstances when the frontal face is lost or overlapped in the frame, resulting in some individuals getting assigned multiple IDs.</span></span>

## <span data-ttu-id="97980-125"><a id="output_elements"></a>Elementy pliku wyjściowego w formacie JSON</span><span class="sxs-lookup"><span data-stu-id="97980-125"><a id="output_elements"></a>Elements of the output JSON file</span></span>

[!INCLUDE [media-services-analytics-output-json](../../includes/media-services-analytics-output-json.md)]

<span data-ttu-id="97980-126">Wykrywanie twarzy na obrazie używa technik fragmentacji (gdzie metadanych można podzielić w oparte na czasie fragmentów i można pobrać tylko potrzebnych) i segmentacji (gdzie zdarzenia są podzielony na wypadek, gdyby otrzymują zbyt duży).</span><span class="sxs-lookup"><span data-stu-id="97980-126">Face Detector uses techniques of fragmentation (where the metadata can be broken up in time-based chunks and you can download only what you need), and segmentation (where the events are broken up in case they get too large).</span></span> <span data-ttu-id="97980-127">Niektórych prostych obliczeń może pomóc przekształcania danych.</span><span class="sxs-lookup"><span data-stu-id="97980-127">Some simple calculations can help you transform the data.</span></span> <span data-ttu-id="97980-128">Na przykład, jeśli zdarzenie rozpoczęty o godzinie 6300 (znaczniki) z skali czasu 2997 (Takty/s) i szybkość klatek z 29,97 (ramek na sekundę), następnie:</span><span class="sxs-lookup"><span data-stu-id="97980-128">For example, if an event started at 6300 (ticks), with a timescale of 2997 (ticks/sec) and framerate of 29.97 (frames/sec), then:</span></span>

* <span data-ttu-id="97980-129">Start/skali czasu = sekund 2.1</span><span class="sxs-lookup"><span data-stu-id="97980-129">Start/Timescale = 2.1 seconds</span></span>
* <span data-ttu-id="97980-130">Sekundy x Framerate = 63 ramki</span><span class="sxs-lookup"><span data-stu-id="97980-130">Seconds x Framerate = 63 frames</span></span>

## <a name="face-detection-input-and-output-example"></a><span data-ttu-id="97980-131">Dostęp do danych wejściowych wykrywania i przykład danych wyjściowych</span><span class="sxs-lookup"><span data-stu-id="97980-131">Face detection input and output example</span></span>
### <a name="input-video"></a><span data-ttu-id="97980-132">Wejściowy plik wideo</span><span class="sxs-lookup"><span data-stu-id="97980-132">Input video</span></span>
[<span data-ttu-id="97980-133">Wejściowy plik wideo</span><span class="sxs-lookup"><span data-stu-id="97980-133">Input Video</span></span>](http://ampdemo.azureedge.net/azuremediaplayer.html?url=https%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fc8834d9f-0b49-4b38-bcaf-ece2746f1972%2FMicrosoft%20Convergence%202015%20%20Keynote%20Highlights.ism%2Fmanifest&amp;autoplay=false)

### <a name="task-configuration-preset"></a><span data-ttu-id="97980-134">Konfiguracja zadania (ustawienia domyślne)</span><span class="sxs-lookup"><span data-stu-id="97980-134">Task configuration (preset)</span></span>
<span data-ttu-id="97980-135">Podczas tworzenia zadania z **Azure Media krój detektora**, należy określić ustawienia domyślne konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="97980-135">When creating a task with **Azure Media Face Detector**, you must specify a configuration preset.</span></span> <span data-ttu-id="97980-136">Następujące ustawienie konfiguracji jest tylko do wykrywania twarzy na obrazie.</span><span class="sxs-lookup"><span data-stu-id="97980-136">The following configuration preset is just for face detection.</span></span>

    {
      "version":"1.0",
      "options":{
          "TrackingMode": "Fast"
      }
    }

#### <a name="attribute-descriptions"></a><span data-ttu-id="97980-137">Opisy atrybutów</span><span class="sxs-lookup"><span data-stu-id="97980-137">Attribute descriptions</span></span>
| <span data-ttu-id="97980-138">Nazwa atrybutu</span><span class="sxs-lookup"><span data-stu-id="97980-138">Attribute name</span></span> | <span data-ttu-id="97980-139">Opis</span><span class="sxs-lookup"><span data-stu-id="97980-139">Description</span></span> |
| --- | --- |
| <span data-ttu-id="97980-140">Tryb</span><span class="sxs-lookup"><span data-stu-id="97980-140">Mode</span></span> |<span data-ttu-id="97980-141">Fast — szybkiego przetwarzania szybkości, ale mniej dokładne (ustawienie domyślne).</span><span class="sxs-lookup"><span data-stu-id="97980-141">Fast - fast processing speed, but less accurate (default).</span></span>|

### <a name="json-output"></a><span data-ttu-id="97980-142">Dane wyjściowe JSON</span><span class="sxs-lookup"><span data-stu-id="97980-142">JSON output</span></span>
<span data-ttu-id="97980-143">Poniższy przykład danych wyjściowych JSON została obcięta.</span><span class="sxs-lookup"><span data-stu-id="97980-143">The following example of JSON output was truncated.</span></span>

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

## <a name="emotion-detection-input-and-output-example"></a><span data-ttu-id="97980-144">Wykrywanie emocji wejściowa i wyjściowa przykład</span><span class="sxs-lookup"><span data-stu-id="97980-144">Emotion detection input and output example</span></span>
### <a name="input-video"></a><span data-ttu-id="97980-145">Wejściowy plik wideo</span><span class="sxs-lookup"><span data-stu-id="97980-145">Input video</span></span>
[<span data-ttu-id="97980-146">Wejściowy plik wideo</span><span class="sxs-lookup"><span data-stu-id="97980-146">Input Video</span></span>](http://ampdemo.azureedge.net/azuremediaplayer.html?url=https%3A%2F%2Freferencestream-samplestream.streaming.mediaservices.windows.net%2Fc8834d9f-0b49-4b38-bcaf-ece2746f1972%2FMicrosoft%20Convergence%202015%20%20Keynote%20Highlights.ism%2Fmanifest&amp;autoplay=false)

### <a name="task-configuration-preset"></a><span data-ttu-id="97980-147">Konfiguracja zadania (ustawienia domyślne)</span><span class="sxs-lookup"><span data-stu-id="97980-147">Task configuration (preset)</span></span>
<span data-ttu-id="97980-148">Podczas tworzenia zadania z **Azure Media krój detektora**, należy określić ustawienia domyślne konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="97980-148">When creating a task with **Azure Media Face Detector**, you must specify a configuration preset.</span></span> <span data-ttu-id="97980-149">Określa następujące ustawienie konfiguracji można utworzyć oparty na wykrywaniu emocji JSON.</span><span class="sxs-lookup"><span data-stu-id="97980-149">The following configuration preset specifies to create JSON based on the emotion detection.</span></span>

    {
      "version": "1.0",
      "options": {
        "aggregateEmotionWindowMs": "987",
        "mode": "aggregateEmotion",
        "aggregateEmotionIntervalMs": "342"
      }
    }


#### <a name="attribute-descriptions"></a><span data-ttu-id="97980-150">Opisy atrybutów</span><span class="sxs-lookup"><span data-stu-id="97980-150">Attribute descriptions</span></span>
| <span data-ttu-id="97980-151">Nazwa atrybutu</span><span class="sxs-lookup"><span data-stu-id="97980-151">Attribute name</span></span> | <span data-ttu-id="97980-152">Opis</span><span class="sxs-lookup"><span data-stu-id="97980-152">Description</span></span> |
| --- | --- |
| <span data-ttu-id="97980-153">Tryb</span><span class="sxs-lookup"><span data-stu-id="97980-153">Mode</span></span> |<span data-ttu-id="97980-154">Kroje: Tylko stają przed wykrywania.</span><span class="sxs-lookup"><span data-stu-id="97980-154">Faces: Only face detection.</span></span><br/><span data-ttu-id="97980-155">PerFaceEmotion: Zwraca emocji osobno dla każdej wykrywania twarzy na obrazie.</span><span class="sxs-lookup"><span data-stu-id="97980-155">PerFaceEmotion: Return emotion independently for each face detection.</span></span><br/><span data-ttu-id="97980-156">AggregateEmotion: Wartości zwracane emocji średni wszystkie powierzchnie w ramce.</span><span class="sxs-lookup"><span data-stu-id="97980-156">AggregateEmotion: Return average emotion values for all faces in frame.</span></span> |
| <span data-ttu-id="97980-157">AggregateEmotionWindowMs</span><span class="sxs-lookup"><span data-stu-id="97980-157">AggregateEmotionWindowMs</span></span> |<span data-ttu-id="97980-158">Użyj, jeśli wybrany tryb AggregateEmotion.</span><span class="sxs-lookup"><span data-stu-id="97980-158">Use if AggregateEmotion mode selected.</span></span> <span data-ttu-id="97980-159">Określa długość wideo użyta do wyprodukowania każdy łączny wynik, w milisekundach.</span><span class="sxs-lookup"><span data-stu-id="97980-159">Specifies the length of video used to produce each aggregate result, in milliseconds.</span></span> |
| <span data-ttu-id="97980-160">AggregateEmotionIntervalMs</span><span class="sxs-lookup"><span data-stu-id="97980-160">AggregateEmotionIntervalMs</span></span> |<span data-ttu-id="97980-161">Użyj, jeśli wybrany tryb AggregateEmotion.</span><span class="sxs-lookup"><span data-stu-id="97980-161">Use if AggregateEmotion mode selected.</span></span> <span data-ttu-id="97980-162">Określa częstotliwość dostarczyło wyników agregacji.</span><span class="sxs-lookup"><span data-stu-id="97980-162">Specifies with what frequency to produce aggregate results.</span></span> |

#### <a name="aggregate-defaults"></a><span data-ttu-id="97980-163">Łączny wartości domyślnych</span><span class="sxs-lookup"><span data-stu-id="97980-163">Aggregate defaults</span></span>
<span data-ttu-id="97980-164">Poniżej są zalecane wartości ustawień okna i interwał agregacji.</span><span class="sxs-lookup"><span data-stu-id="97980-164">Below are recommended values for the aggregate window and interval settings.</span></span> <span data-ttu-id="97980-165">AggregateEmotionWindowMs powinien być dłuższy niż AggregateEmotionIntervalMs.</span><span class="sxs-lookup"><span data-stu-id="97980-165">AggregateEmotionWindowMs should be longer than AggregateEmotionIntervalMs.</span></span>

|| <span data-ttu-id="97980-166">Ustawienia domyślne (s)</span><span class="sxs-lookup"><span data-stu-id="97980-166">Defaults(s)</span></span> | <span data-ttu-id="97980-167">Min(s)</span><span class="sxs-lookup"><span data-stu-id="97980-167">Min(s)</span></span> | <span data-ttu-id="97980-168">MAX(s)</span><span class="sxs-lookup"><span data-stu-id="97980-168">Max(s)</span></span> |
|--- | --- | --- | --- |
| <span data-ttu-id="97980-169">AggregateEmotionWindowMs</span><span class="sxs-lookup"><span data-stu-id="97980-169">AggregateEmotionWindowMs</span></span> |<span data-ttu-id="97980-170">0.5</span><span class="sxs-lookup"><span data-stu-id="97980-170">0.5</span></span> |<span data-ttu-id="97980-171">2</span><span class="sxs-lookup"><span data-stu-id="97980-171">2</span></span> |<span data-ttu-id="97980-172">0.25</span><span class="sxs-lookup"><span data-stu-id="97980-172">0.25</span></span>|
| <span data-ttu-id="97980-173">AggregateEmotionIntervalMs</span><span class="sxs-lookup"><span data-stu-id="97980-173">AggregateEmotionIntervalMs</span></span> |<span data-ttu-id="97980-174">0.5</span><span class="sxs-lookup"><span data-stu-id="97980-174">0.5</span></span> |<span data-ttu-id="97980-175">1</span><span class="sxs-lookup"><span data-stu-id="97980-175">1</span></span> |<span data-ttu-id="97980-176">0.25</span><span class="sxs-lookup"><span data-stu-id="97980-176">0.25</span></span>|

### <a name="json-output"></a><span data-ttu-id="97980-177">Dane wyjściowe JSON</span><span class="sxs-lookup"><span data-stu-id="97980-177">JSON output</span></span>
<span data-ttu-id="97980-178">Dane wyjściowe dla agregacji emocji (obcięty) JSON:</span><span class="sxs-lookup"><span data-stu-id="97980-178">JSON output for aggregate emotion (truncated):</span></span>

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

## <a name="limitations"></a><span data-ttu-id="97980-179">Ograniczenia</span><span class="sxs-lookup"><span data-stu-id="97980-179">Limitations</span></span>
* <span data-ttu-id="97980-180">Obsługiwane formaty wideo wejściowych obejmują MP4, MOV i WMV.</span><span class="sxs-lookup"><span data-stu-id="97980-180">The supported input video formats include MP4, MOV, and WMV.</span></span>
* <span data-ttu-id="97980-181">Zakres rozmiaru wykrywalny krój jest 24 x 24 do 2048 x 2048 pikseli.</span><span class="sxs-lookup"><span data-stu-id="97980-181">The detectable face size range is 24x24 to 2048x2048 pixels.</span></span> <span data-ttu-id="97980-182">Nie są wykrywane kroje poza tym zakresem.</span><span class="sxs-lookup"><span data-stu-id="97980-182">The faces out of this range will not be detected.</span></span>
* <span data-ttu-id="97980-183">Dla każdego wideo maksymalna liczba kroje zwrócił wynosi 64.</span><span class="sxs-lookup"><span data-stu-id="97980-183">For each video, the maximum number of faces returned is 64.</span></span>
* <span data-ttu-id="97980-184">Niektóre kroje mogą nie być wykrywane z powodu problemów technicznych; np. w przypadku bardzo dużych kąty przedniej (head ułożenia) i dużych zamknięcia.</span><span class="sxs-lookup"><span data-stu-id="97980-184">Some faces may not be detected due to technical challenges; e.g. very large face angles (head-pose), and large occlusion.</span></span> <span data-ttu-id="97980-185">Kroje czołowego i niemal czołowego mieć najlepsze wyniki.</span><span class="sxs-lookup"><span data-stu-id="97980-185">Frontal and near-frontal faces have the best results.</span></span>

## <a name="net-sample-code"></a><span data-ttu-id="97980-186">.NET przykładowy kod</span><span class="sxs-lookup"><span data-stu-id="97980-186">.NET sample code</span></span>

<span data-ttu-id="97980-187">Następujących programów przedstawiono sposób:</span><span class="sxs-lookup"><span data-stu-id="97980-187">The following program shows how to:</span></span>

1. <span data-ttu-id="97980-188">Utworzenie elementu zawartości i przesyłanie pliku multimediów do elementu zawartości.</span><span class="sxs-lookup"><span data-stu-id="97980-188">Create an asset and upload a media file into the asset.</span></span>
2. <span data-ttu-id="97980-189">Utwórz zadanie z zadania wykrywania twarzy na obrazie w zależności od pliku konfiguracji, który zawiera następujące ustawienie json.</span><span class="sxs-lookup"><span data-stu-id="97980-189">Create a job with a face detection task based on a configuration file that contains the following json preset.</span></span> 
   
        {
            "version": "1.0"
        }
3. <span data-ttu-id="97980-190">Pobierz pliki danych wyjściowych w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="97980-190">Download the output JSON files.</span></span> 

#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="97980-191">Tworzenie i konfigurowanie projektu programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="97980-191">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="97980-192">Skonfiguruj środowisko projektowe i wypełnij plik app.config przy użyciu informacji dotyczących połączenia, zgodnie z opisem w sekcji [Projektowanie usługi Media Services na platformie .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="97980-192">Set up your development environment and populate the app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="97980-193">Przykład</span><span class="sxs-lookup"><span data-stu-id="97980-193">Example</span></span>

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

                // Run the FaceDetection job.
                var asset = RunFaceDetectionJob(@"C:\supportFiles\FaceDetection\BigBuckBunny.mp4",
                                            @"C:\supportFiles\FaceDetection\config.json");

                // Download the job output asset.
                DownloadAsset(asset, @"C:\supportFiles\FaceDetection\Output");
            }

            static IAsset RunFaceDetectionJob(string inputMediaFilePath, string configurationFile)
            {
                // Create an asset and upload the input media file to storage.
                IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
                    "My Face Detection Input Asset",
                    AssetCreationOptions.None);

                // Declare a new job.
                IJob job = _context.Jobs.Create("My Face Detection Job");

                // Get a reference to Azure Media Face Detector.
                string MediaProcessorName = "Azure Media Face Detector";

                var processor = GetLatestMediaProcessorByName(MediaProcessorName);

                // Read configuration from the specified file.
                string configuration = File.ReadAllText(configurationFile);

                // Create a task with the encoding details, using a string preset.
                ITask task = job.Tasks.AddNew("My Face Detection Task",
                    processor,
                    configuration,
                    TaskOptions.None);

                // Specify the input asset.
                task.InputAssets.Add(asset);

                // Add an output asset to contain the results of the job.
                task.OutputAssets.AddNew("My Face Detectoion Output Asset", AssetCreationOptions.None);

                // Use the following event handler to check job progress.  
                job.StateChanged += new EventHandler<JobStateChangedEventArgs>(StateChanged);

                // Launch the job.
                job.Submit();

                // Check job execution and wait for job to finish.
                Task progressJobTask = job.GetExecutionProgressTask(CancellationToken.None);

                progressJobTask.Wait();

                // If job state is Error, the event handling
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

## <a name="media-services-learning-paths"></a><span data-ttu-id="97980-194">Ścieżki szkoleniowe dotyczące usługi Media Services</span><span class="sxs-lookup"><span data-stu-id="97980-194">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="97980-195">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="97980-195">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="97980-196">Powiązane linki</span><span class="sxs-lookup"><span data-stu-id="97980-196">Related links</span></span>
[<span data-ttu-id="97980-197">Przegląd analiz usługi Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="97980-197">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

[<span data-ttu-id="97980-198">W trakcie analizy multimediów Azure</span><span class="sxs-lookup"><span data-stu-id="97980-198">Azure Media Analytics demos</span></span>](http://amslabs.azurewebsites.net/demos/Analytics.html)

