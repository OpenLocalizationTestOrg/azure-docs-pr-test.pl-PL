---
title: "Ruchy aaaDetect z analizy multimediów Azure | Dokumentacja firmy Microsoft"
description: "Witaj umożliwia procesora (MP) nośnika czujnik ruchu Azure Media tooefficiently można zidentyfikować sekcje zawierają informacje przydatne w wideo w innym przypadku długich i procesu."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: d144f813-1a55-442f-a895-5c4cb6d0aeae
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/31/2017
ms.author: milanga;juliako;
ms.openlocfilehash: cb431375c92222053ed2239dd4e45767524dab68
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="detect-motions-with-azure-media-analytics"></a><span data-ttu-id="59287-103">Wykrywanie ruchów z analizy multimediów Azure</span><span class="sxs-lookup"><span data-stu-id="59287-103">Detect Motions with Azure Media Analytics</span></span>
## <a name="overview"></a><span data-ttu-id="59287-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="59287-104">Overview</span></span>
<span data-ttu-id="59287-105">Witaj **czujnik ruchu Azure Media** nośnika procesora (MP) umożliwia tooefficiently można zidentyfikować sekcje zawierają informacje przydatne w wideo w innym przypadku długich i procesu.</span><span class="sxs-lookup"><span data-stu-id="59287-105">hello **Azure Media Motion Detector** media processor (MP) enables you tooefficiently identify sections of interest within an otherwise long and uneventful video.</span></span> <span data-ttu-id="59287-106">Wykrywanie ruchu może służyć na statycznych aparatu materiał tooidentify sekcje wideo hello gdzie występuje ruchu.</span><span class="sxs-lookup"><span data-stu-id="59287-106">Motion detection can be used on static camera footage tooidentify sections of hello video where motion occurs.</span></span> <span data-ttu-id="59287-107">Generuje plik JSON zawierający metadane z sygnatury czasowe i hello ograniczenia regionu, w którym wystąpiło zdarzenie hello.</span><span class="sxs-lookup"><span data-stu-id="59287-107">It generates a JSON file containing a metadata with timestamps and hello bounding region where hello event occurred.</span></span>

<span data-ttu-id="59287-108">Docelowe do źródła wideo zabezpieczeń, ta technologia jest możliwe toocategorize ruchu na odpowiednie zdarzenia i fałszywych alarmów, takie jak cieni i zmian oświetlenia.</span><span class="sxs-lookup"><span data-stu-id="59287-108">Targeted towards security video feeds, this technology is able toocategorize motion into relevant events and false positives such as shadows and lighting changes.</span></span> <span data-ttu-id="59287-109">Dzięki temu można toogenerate alertów zabezpieczeń z aparatu fotograficznego źródła danych bez otrzymywania wiadomości-śmieci nieskończone zdarzenia nie ma znaczenia, będąc chwil stanie tooextract płynących z bardzo długi nadzoru wideo.</span><span class="sxs-lookup"><span data-stu-id="59287-109">This allows you toogenerate security alerts from camera feeds without being spammed with endless irrelevant events, while being able tooextract moments of interest from extremely long surveillance videos.</span></span>

<span data-ttu-id="59287-110">Witaj **czujnik ruchu Azure Media** pakiet administracyjny jest obecnie w przeglądzie.</span><span class="sxs-lookup"><span data-stu-id="59287-110">hello **Azure Media Motion Detector** MP is currently in Preview.</span></span>

<span data-ttu-id="59287-111">Ten temat zawiera szczegółowe informacje o **czujnik ruchu Azure Media** i przedstawia sposób toouse go przy użyciu zestawu SDK usługi Media Services dla platformy .NET</span><span class="sxs-lookup"><span data-stu-id="59287-111">This topic gives details about  **Azure Media Motion Detector** and shows how toouse it with Media Services SDK for .NET</span></span>

## <a name="motion-detector-input-files"></a><span data-ttu-id="59287-112">Pliki wejściowe wykrywanie ruchu</span><span class="sxs-lookup"><span data-stu-id="59287-112">Motion Detector input files</span></span>
<span data-ttu-id="59287-113">Pliki wideo.</span><span class="sxs-lookup"><span data-stu-id="59287-113">Video files.</span></span> <span data-ttu-id="59287-114">Obecnie są obsługiwane następujące formaty hello: MP4, MOV i WMV.</span><span class="sxs-lookup"><span data-stu-id="59287-114">Currently, hello following formats are supported: MP4, MOV, and WMV.</span></span>

## <a name="task-configuration-preset"></a><span data-ttu-id="59287-115">Konfiguracja zadania (ustawienia domyślne)</span><span class="sxs-lookup"><span data-stu-id="59287-115">Task configuration (preset)</span></span>
<span data-ttu-id="59287-116">Podczas tworzenia zadania z **czujnik ruchu Azure Media**, należy określić ustawienia domyślne konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="59287-116">When creating a task with **Azure Media Motion Detector**, you must specify a configuration preset.</span></span> 

### <a name="parameters"></a><span data-ttu-id="59287-117">Parametry</span><span class="sxs-lookup"><span data-stu-id="59287-117">Parameters</span></span>
<span data-ttu-id="59287-118">Program hello następujące parametry:</span><span class="sxs-lookup"><span data-stu-id="59287-118">You can use hello following parameters:</span></span>

| <span data-ttu-id="59287-119">Nazwa</span><span class="sxs-lookup"><span data-stu-id="59287-119">Name</span></span> | <span data-ttu-id="59287-120">Opcje</span><span class="sxs-lookup"><span data-stu-id="59287-120">Options</span></span> | <span data-ttu-id="59287-121">Opis</span><span class="sxs-lookup"><span data-stu-id="59287-121">Description</span></span> | <span data-ttu-id="59287-122">Domyślne</span><span class="sxs-lookup"><span data-stu-id="59287-122">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="59287-123">sensitivityLevel</span><span class="sxs-lookup"><span data-stu-id="59287-123">sensitivityLevel</span></span> |<span data-ttu-id="59287-124">Ciąg: "Niski", "medium',"Wysoki"</span><span class="sxs-lookup"><span data-stu-id="59287-124">String:'low', 'medium', 'high'</span></span> |<span data-ttu-id="59287-125">Ustawia poziom czułości hello na ruchy, która jest raportowana.</span><span class="sxs-lookup"><span data-stu-id="59287-125">Sets hello sensitivity level at which motions is reported.</span></span> <span data-ttu-id="59287-126">Dostosuj tooadjust ilość fałszywych alarmów.</span><span class="sxs-lookup"><span data-stu-id="59287-126">Adjust this tooadjust amount of false positives.</span></span> |<span data-ttu-id="59287-127">"Średni"</span><span class="sxs-lookup"><span data-stu-id="59287-127">'medium'</span></span> |
| <span data-ttu-id="59287-128">frameSamplingValue</span><span class="sxs-lookup"><span data-stu-id="59287-128">frameSamplingValue</span></span> |<span data-ttu-id="59287-129">Dodatnia liczba całkowita</span><span class="sxs-lookup"><span data-stu-id="59287-129">Positive integer</span></span> |<span data-ttu-id="59287-130">Ustawia częstotliwość hello, w której działa algorytmu.</span><span class="sxs-lookup"><span data-stu-id="59287-130">Sets hello frequency at which algorithm runs.</span></span> <span data-ttu-id="59287-131">Każdy ramki jest równa 1, 2 oznacza, że każdy ramki 2 i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="59287-131">1 equals every frame, 2 means every 2nd frame, and so on.</span></span> |<span data-ttu-id="59287-132">1</span><span class="sxs-lookup"><span data-stu-id="59287-132">1</span></span> |
| <span data-ttu-id="59287-133">detectLightChange</span><span class="sxs-lookup"><span data-stu-id="59287-133">detectLightChange</span></span> |<span data-ttu-id="59287-134">Wartość logiczna: "prawda", "fałsz"</span><span class="sxs-lookup"><span data-stu-id="59287-134">Boolean:'true', 'false'</span></span> |<span data-ttu-id="59287-135">Określa, czy zmiany światła są podane w wynikach hello</span><span class="sxs-lookup"><span data-stu-id="59287-135">Sets whether light changes are reported in hello results</span></span> |<span data-ttu-id="59287-136">"Fałsz"</span><span class="sxs-lookup"><span data-stu-id="59287-136">'False'</span></span> |
| <span data-ttu-id="59287-137">mergeTimeThreshold</span><span class="sxs-lookup"><span data-stu-id="59287-137">mergeTimeThreshold</span></span> |<span data-ttu-id="59287-138">Czas xs: Hh: mm:</span><span class="sxs-lookup"><span data-stu-id="59287-138">Xs-time: Hh:mm:ss</span></span><br/><span data-ttu-id="59287-139">Przykład: 00:00:03</span><span class="sxs-lookup"><span data-stu-id="59287-139">Example: 00:00:03</span></span> |<span data-ttu-id="59287-140">Określa hello przedział czasu między zdarzeniami ruchu, gdzie łączyć i zgłaszane jako 1 2 zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="59287-140">Specifies hello time window between motion events where 2 events will be combined and reported as 1.</span></span> |<span data-ttu-id="59287-141">00:00:00</span><span class="sxs-lookup"><span data-stu-id="59287-141">00:00:00</span></span> |
| <span data-ttu-id="59287-142">detectionZones</span><span class="sxs-lookup"><span data-stu-id="59287-142">detectionZones</span></span> |<span data-ttu-id="59287-143">Tablica wykrywania stref:</span><span class="sxs-lookup"><span data-stu-id="59287-143">An array of detection zones:</span></span><br/><span data-ttu-id="59287-144">-Wykrywania strefy jest tablicą 3 lub więcej punktów</span><span class="sxs-lookup"><span data-stu-id="59287-144">- Detection Zone is an array of 3 or more points</span></span><br/><span data-ttu-id="59287-145">— Punkt jest x i y Współrzędna z 0 too1.</span><span class="sxs-lookup"><span data-stu-id="59287-145">- Point is a x and y coordinate from 0 too1.</span></span> |<span data-ttu-id="59287-146">W tym artykule opisano hello lista wykrywania wielobocznych stref toobe używane.</span><span class="sxs-lookup"><span data-stu-id="59287-146">Describes hello list of polygonal detection zones toobe used.</span></span><br/><span data-ttu-id="59287-147">Wyniki będą raportowane ze strefami hello jako identyfikator z hello pierwszy z nich jest 'id': 0</span><span class="sxs-lookup"><span data-stu-id="59287-147">Results will be reported with hello zones as an ID, with hello first one being 'id':0</span></span> |<span data-ttu-id="59287-148">Jednej strefie, która obejmuje całą ramkę hello.</span><span class="sxs-lookup"><span data-stu-id="59287-148">Single zone which covers hello entire frame.</span></span> |

### <a name="json-example"></a><span data-ttu-id="59287-149">Przykład JSON</span><span class="sxs-lookup"><span data-stu-id="59287-149">JSON example</span></span>
    {
      "version": "1.0",
      "options": {
        "sensitivityLevel": "medium",
        "frameSamplingValue": 1,
        "detectLightChange": "False",
        "mergeTimeThreshold":
        "00:00:02",
        "detectionZones": [
          [
            {"x": 0, "y": 0},
            {"x": 0.5, "y": 0},
            {"x": 0, "y": 1}
           ],
          [
            {"x": 0.3, "y": 0.3},
            {"x": 0.55, "y": 0.3},
            {"x": 0.8, "y": 0.3},
            {"x": 0.8, "y": 0.55},
            {"x": 0.8, "y": 0.8},
            {"x": 0.55, "y": 0.8},
            {"x": 0.3, "y": 0.8},
            {"x": 0.3, "y": 0.55}
          ]
        ]
      }
    }


## <a name="motion-detector-output-files"></a><span data-ttu-id="59287-150">Pliki wyjściowe wykrywanie ruchu</span><span class="sxs-lookup"><span data-stu-id="59287-150">Motion Detector output files</span></span>
<span data-ttu-id="59287-151">Zadanie wykrywania ruchu zwróci pliku JSON w zawartości wyjściowej hello opisującą hello ruchu alertów i ich w kategorie hello wideo.</span><span class="sxs-lookup"><span data-stu-id="59287-151">A motion detection job will return a JSON file in hello output asset which describes hello motion alerts, and their categories, within hello video.</span></span> <span data-ttu-id="59287-152">Witaj plik będzie zawierać informacje o hello czas i czas trwania ruchu wykryte w hello wideo.</span><span class="sxs-lookup"><span data-stu-id="59287-152">hello file will contain information about hello time and duration of motion detected in hello video.</span></span>

<span data-ttu-id="59287-153">Hello API wykrywanie ruchu zawiera wskaźniki po ruchu w stałej tło w formie wideo (np. nadzoru, wideo) są obiekty.</span><span class="sxs-lookup"><span data-stu-id="59287-153">hello Motion Detector API provides indicators once there are objects in motion in a fixed background video (e.g. a surveillance video).</span></span> <span data-ttu-id="59287-154">Hello czujnik ruchu jest fałszywe alarmy przeszkolone tooreduce, takie jak oświetlenia i zmiany w tle.</span><span class="sxs-lookup"><span data-stu-id="59287-154">hello Motion Detector is trained tooreduce false alarms, such as lighting and shadow changes.</span></span> <span data-ttu-id="59287-155">Bieżące ograniczenia hello algorytmy obejmują nocy wizji wideo, półprzezroczyste obiektów i małych obiektów.</span><span class="sxs-lookup"><span data-stu-id="59287-155">Current limitations of hello algorithms include night vision videos, semi-transparent objects, and small objects.</span></span>

### <span data-ttu-id="59287-156"><a id="output_elements"></a>Elementy hello pliku wyjściowego w formacie JSON</span><span class="sxs-lookup"><span data-stu-id="59287-156"><a id="output_elements"></a>Elements of hello output JSON file</span></span>
> [!NOTE]
> <span data-ttu-id="59287-157">W najnowszej wersji hello formacie JSON dane wyjściowe hello została zmieniona, może reprezentować istotne zmiany w przypadku niektórych klientów.</span><span class="sxs-lookup"><span data-stu-id="59287-157">In hello latest release, hello Output JSON format has changed and may represent a breaking change for some customers.</span></span>
> 
> 

<span data-ttu-id="59287-158">Witaj poniższej tabeli opisano elementy hello pliku wyjściowego w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="59287-158">hello following table describes elements of hello output JSON file.</span></span>

| <span data-ttu-id="59287-159">Element</span><span class="sxs-lookup"><span data-stu-id="59287-159">Element</span></span> | <span data-ttu-id="59287-160">Opis</span><span class="sxs-lookup"><span data-stu-id="59287-160">Description</span></span> |
| --- | --- |
| <span data-ttu-id="59287-161">Wersja</span><span class="sxs-lookup"><span data-stu-id="59287-161">Version</span></span> |<span data-ttu-id="59287-162">Odnosi się wersja toohello hello wideo interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="59287-162">This refers toohello version of hello Video API.</span></span> <span data-ttu-id="59287-163">Witaj bieżąca wersja to 2.</span><span class="sxs-lookup"><span data-stu-id="59287-163">hello current version is 2.</span></span> |
| <span data-ttu-id="59287-164">skali czasu</span><span class="sxs-lookup"><span data-stu-id="59287-164">Timescale</span></span> |<span data-ttu-id="59287-165">"Impulsów" na sekundę hello wideo.</span><span class="sxs-lookup"><span data-stu-id="59287-165">"Ticks" per second of hello video.</span></span> |
| <span data-ttu-id="59287-166">Przesunięcie</span><span class="sxs-lookup"><span data-stu-id="59287-166">Offset</span></span> |<span data-ttu-id="59287-167">Przesunięcie czasu Hello sygnatur czasowych w parametrem "ticks".</span><span class="sxs-lookup"><span data-stu-id="59287-167">hello time offset for timestamps in "ticks".</span></span> <span data-ttu-id="59287-168">W wersji 1.0 interfejsów API, wideo ta będzie zawsze równa 0.</span><span class="sxs-lookup"><span data-stu-id="59287-168">In version 1.0 of Video APIs, this will always be 0.</span></span> <span data-ttu-id="59287-169">W przyszłości scenariusze, które firma Microsoft obsługuje, ta wartość może zmienić.</span><span class="sxs-lookup"><span data-stu-id="59287-169">In future scenarios we support, this value may change.</span></span> |
| <span data-ttu-id="59287-170">szybkość klatek</span><span class="sxs-lookup"><span data-stu-id="59287-170">Framerate</span></span> |<span data-ttu-id="59287-171">Klatek na sekundę hello wideo.</span><span class="sxs-lookup"><span data-stu-id="59287-171">Frames per second of hello video.</span></span> |
| <span data-ttu-id="59287-172">Szerokość, wysokość</span><span class="sxs-lookup"><span data-stu-id="59287-172">Width, Height</span></span> |<span data-ttu-id="59287-173">Odwołuje się toohello szerokość i wysokość hello wideo w pikselach.</span><span class="sxs-lookup"><span data-stu-id="59287-173">Refers toohello width and height of hello video in pixels.</span></span> |
| <span data-ttu-id="59287-174">Uruchamianie</span><span class="sxs-lookup"><span data-stu-id="59287-174">Start</span></span> |<span data-ttu-id="59287-175">Witaj start sygnaturą czasową w parametrem "ticks".</span><span class="sxs-lookup"><span data-stu-id="59287-175">hello start timestamp in "ticks".</span></span> |
| <span data-ttu-id="59287-176">Czas trwania</span><span class="sxs-lookup"><span data-stu-id="59287-176">Duration</span></span> |<span data-ttu-id="59287-177">Długość Hello zdarzenia hello w parametrem "ticks".</span><span class="sxs-lookup"><span data-stu-id="59287-177">hello length of hello event, in "ticks".</span></span> |
| <span data-ttu-id="59287-178">Interwał</span><span class="sxs-lookup"><span data-stu-id="59287-178">Interval</span></span> |<span data-ttu-id="59287-179">Interwał powitania każdego wpisu w przypadku hello w parametrem "ticks".</span><span class="sxs-lookup"><span data-stu-id="59287-179">hello interval of each entry in hello event, in "ticks".</span></span> |
| <span data-ttu-id="59287-180">Zdarzenia</span><span class="sxs-lookup"><span data-stu-id="59287-180">Events</span></span> |<span data-ttu-id="59287-181">Każdy fragment zdarzenia zawiera ruchu hello wykryty w tym czas trwania.</span><span class="sxs-lookup"><span data-stu-id="59287-181">Each event fragment contains hello motion detected within that time duration.</span></span> |
| <span data-ttu-id="59287-182">Typ</span><span class="sxs-lookup"><span data-stu-id="59287-182">Type</span></span> |<span data-ttu-id="59287-183">W bieżącej wersji hello jest to zawsze "2" dla ogólnego ruchu.</span><span class="sxs-lookup"><span data-stu-id="59287-183">In hello current version, this is always ‘2’ for generic motion.</span></span> <span data-ttu-id="59287-184">Etykieta udostępnia interfejsy API wideo hello elastyczność toocategorize ruchu w przyszłych wersjach.</span><span class="sxs-lookup"><span data-stu-id="59287-184">This label gives Video APIs hello flexibility toocategorize motion in future versions.</span></span> |
| <span data-ttu-id="59287-185">RegionID</span><span class="sxs-lookup"><span data-stu-id="59287-185">RegionID</span></span> |<span data-ttu-id="59287-186">Zgodnie z powyższymi wskazówkami, ta będzie zawsze równa 0 w tej wersji.</span><span class="sxs-lookup"><span data-stu-id="59287-186">As explained above, this will always be 0 in this version.</span></span> <span data-ttu-id="59287-187">Etykieta daje API wideo hello elastyczność toofind ruchu w różnych regionach w przyszłych wersjach.</span><span class="sxs-lookup"><span data-stu-id="59287-187">This label gives Video API hello flexibility toofind motion in various regions in future versions.</span></span> |
| <span data-ttu-id="59287-188">Regiony</span><span class="sxs-lookup"><span data-stu-id="59287-188">Regions</span></span> |<span data-ttu-id="59287-189">Odwołuje się toohello obszar wideo gdzie interesujących ruchu.</span><span class="sxs-lookup"><span data-stu-id="59287-189">Refers toohello area in your video where you care about motion.</span></span> <br/><br/><span data-ttu-id="59287-190">-"id" reprezentuje obszar region hello — w tej wersji jest tylko jeden, identyfikator: 0.</span><span class="sxs-lookup"><span data-stu-id="59287-190">-"id" represents hello region area – in this version there is only one, ID 0.</span></span> <br/><span data-ttu-id="59287-191">-"type" reprezentuje hello kształt obszaru hello interesujących dla ruchu.</span><span class="sxs-lookup"><span data-stu-id="59287-191">-"type" represents hello shape of hello region you care about for motion.</span></span> <span data-ttu-id="59287-192">"Prostokąt" i "wielokąta" są obecnie obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="59287-192">Currently, "rectangle" and "polygon" are supported.</span></span><br/> <span data-ttu-id="59287-193">Jeśli określono "prostokąt" hello region ma wymiarów w X, Y, szerokość i wysokość.</span><span class="sxs-lookup"><span data-stu-id="59287-193">If you specified "rectangle", hello region has dimensions in X, Y, Width, and Height.</span></span> <span data-ttu-id="59287-194">Witaj X i Y współrzędne reprezentują współrzędnych XY lewy górny hello hello regionu w skali znormalizowane 0.0 too1.0.</span><span class="sxs-lookup"><span data-stu-id="59287-194">hello X and Y coordinates represent hello upper left hand XY coordinates of hello region in a normalized scale of 0.0 too1.0.</span></span> <span data-ttu-id="59287-195">Hello szerokości i wysokości reprezentuje rozmiar hello hello regionu w skali znormalizowane 0.0 too1.0.</span><span class="sxs-lookup"><span data-stu-id="59287-195">hello width and height represent hello size of hello region in a normalized scale of 0.0 too1.0.</span></span> <span data-ttu-id="59287-196">W bieżącej wersji hello X, Y, szerokość i wysokość jest zawsze ustalone na 0, 0 i 1, 1.</span><span class="sxs-lookup"><span data-stu-id="59287-196">In hello current version, X, Y, Width, and Height are always fixed at 0, 0 and 1, 1.</span></span> <br/><span data-ttu-id="59287-197">Jeśli określono "wielokąta" hello region ma wymiarów w punktach.</span><span class="sxs-lookup"><span data-stu-id="59287-197">If you specified "polygon", hello region has dimensions in points.</span></span> <br/> |
| <span data-ttu-id="59287-198">fragmenty</span><span class="sxs-lookup"><span data-stu-id="59287-198">Fragments</span></span> |<span data-ttu-id="59287-199">metadane Hello jest fragmentaryczne się w różnych segmentach fragmenty.</span><span class="sxs-lookup"><span data-stu-id="59287-199">hello metadata is chunked up into different segments called fragments.</span></span> <span data-ttu-id="59287-200">Każdy fragmentu zawiera rozpoczęcia, czas trwania, liczba interwałów i zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="59287-200">Each fragment contains a start, duration, interval number, and event(s).</span></span> <span data-ttu-id="59287-201">Fragment ze zdarzeniami nie oznacza, że ruch nie został wykryty podczas tej godziny rozpoczęcia i czas trwania.</span><span class="sxs-lookup"><span data-stu-id="59287-201">A fragment with no events means that no motion was detected during that start time and duration.</span></span> |
| <span data-ttu-id="59287-202">Nawiasy kwadratowe]</span><span class="sxs-lookup"><span data-stu-id="59287-202">Brackets []</span></span> |<span data-ttu-id="59287-203">Każdy nawiasu reprezentuje jeden interwał w zdarzeniu hello.</span><span class="sxs-lookup"><span data-stu-id="59287-203">Each bracket represents one interval in hello event.</span></span> <span data-ttu-id="59287-204">Puste nawiasy dla tego przedziału oznacza, że ruch nie została wykryta.</span><span class="sxs-lookup"><span data-stu-id="59287-204">Empty brackets for that interval means that no motion was detected.</span></span> |
| <span data-ttu-id="59287-205">Lokalizacje</span><span class="sxs-lookup"><span data-stu-id="59287-205">locations</span></span> |<span data-ttu-id="59287-206">Ten nowy wpis w polu zdarzenia wymieniono hello lokalizacji, gdzie wystąpił hello ruchu.</span><span class="sxs-lookup"><span data-stu-id="59287-206">This new entry under events lists hello location where hello motion occurred.</span></span> <span data-ttu-id="59287-207">Jest to bardziej szczegółowy niż hello wykrywania strefy.</span><span class="sxs-lookup"><span data-stu-id="59287-207">This is more specific than hello detection zones.</span></span> |

<span data-ttu-id="59287-208">Witaj poniżej przedstawiono przykładowe dane wyjściowe JSON</span><span class="sxs-lookup"><span data-stu-id="59287-208">hello following is a JSON output example</span></span>

    {
      "version": 2,
      "timescale": 23976,
      "offset": 0,
      "framerate": 24,
      "width": 1280,
      "height": 720,
      "regions": [
        {
          "id": 0,
          "type": "polygon",
          "points": [{'x': 0, 'y': 0},
            {'x': 0.5, 'y': 0},
            {'x': 0, 'y': 1}]
        }
      ],
      "fragments": [
        {
          "start": 0,
          "duration": 226765
        },
        {
          "start": 226765,
          "duration": 47952,
          "interval": 999,
          "events": [
            [
              {
                "type": 2,
                "typeName": "motion",
                "locations": [
                  {
                    "x": 0.004184,
                    "y": 0.007463,
                    "width": 0.991667,
                    "height": 0.985185
                  }
                ],
                "regionId": 0
              }
            ],

    …
## <a name="limitations"></a><span data-ttu-id="59287-209">Ograniczenia</span><span class="sxs-lookup"><span data-stu-id="59287-209">Limitations</span></span>
* <span data-ttu-id="59287-210">formatów wejściowych wideo Hello obsługiwane obejmują MP4, MOV i WMV.</span><span class="sxs-lookup"><span data-stu-id="59287-210">hello supported input video formats include MP4, MOV, and WMV.</span></span>
* <span data-ttu-id="59287-211">Wykrywanie ruchu jest zoptymalizowana pod kątem wideo nieruchomy tła.</span><span class="sxs-lookup"><span data-stu-id="59287-211">Motion Detection is optimized for stationary background videos.</span></span> <span data-ttu-id="59287-212">Algorytm Hello koncentruje się na zmniejszenie fałszywe alarmy, takie jak zmiany oświetlenia i cieni.</span><span class="sxs-lookup"><span data-stu-id="59287-212">hello algorithm focuses on reducing false alarms, such as lighting changes, and shadows.</span></span>
* <span data-ttu-id="59287-213">Niektóre ruchu mogą nie być wykrywane powodu wyzwania tootechnical; np. nocy wizji wideo, półprzezroczyste obiektów i małych obiektów.</span><span class="sxs-lookup"><span data-stu-id="59287-213">Some motion may not be detected due tootechnical challenges; e.g. night vision videos, semi-transparent objects, and small objects.</span></span>

## <a name="net-sample-code"></a><span data-ttu-id="59287-214">.NET przykładowy kod</span><span class="sxs-lookup"><span data-stu-id="59287-214">.NET sample code</span></span>

<span data-ttu-id="59287-215">następujące Hello program pokazuje sposób:</span><span class="sxs-lookup"><span data-stu-id="59287-215">hello following program shows how to:</span></span>

1. <span data-ttu-id="59287-216">Utworzenie elementu zawartości i przesyłanie pliku multimediów do hello zawartości.</span><span class="sxs-lookup"><span data-stu-id="59287-216">Create an asset and upload a media file into hello asset.</span></span>
2. <span data-ttu-id="59287-217">Utwórz zadanie z zadania wykrywania ruchu na obrazie wideo w zależności od pliku konfiguracji, który zawiera hello następujące ustawienie wstępne json.</span><span class="sxs-lookup"><span data-stu-id="59287-217">Create a job with a video motion detection task based on a configuration file that contains hello following json preset.</span></span> 
   
        {
          "Version": "1.0",
          "Options": {
            "SensitivityLevel": "medium",
            "FrameSamplingValue": 1,
            "DetectLightChange": "False",
            "MergeTimeThreshold":
            "00:00:02",
            "DetectionZones": [
              [
                {"x": 0, "y": 0},
                {"x": 0.5, "y": 0},
                {"x": 0, "y": 1}
               ],
              [
                {"x": 0.3, "y": 0.3},
                {"x": 0.55, "y": 0.3},
                {"x": 0.8, "y": 0.3},
                {"x": 0.8, "y": 0.55},
                {"x": 0.8, "y": 0.8},
                {"x": 0.55, "y": 0.8},
                {"x": 0.3, "y": 0.8},
                {"x": 0.3, "y": 0.55}
              ]
            ]
          }
        }
3. <span data-ttu-id="59287-218">Pobierz pliki w formacie JSON dane wyjściowe hello.</span><span class="sxs-lookup"><span data-stu-id="59287-218">Download hello output JSON files.</span></span> 

#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="59287-219">Tworzenie i konfigurowanie projektu programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="59287-219">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="59287-220">Konfigurowanie środowiska projektowego i wypełnić plik app.config hello o informacje dotyczące połączenia, zgodnie z opisem w [tworzenia usługi Media Services z platformą .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="59287-220">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="59287-221">Przykład</span><span class="sxs-lookup"><span data-stu-id="59287-221">Example</span></span>


    using System;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Threading;
    using System.Threading.Tasks;

    namespace VideoMotionDetection
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

                // Run hello VideoMotionDetection job.
                var asset = RunVideoMotionDetectionJob(@"C:\supportFiles\VideoMotionDetection\BigBuckBunny.mp4",
                                            @"C:\supportFiles\VideoMotionDetection\config.json");

                // Download hello job output asset.
                DownloadAsset(asset, @"C:\supportFiles\VideoMotionDetection\Output");
            }

            static IAsset RunVideoMotionDetectionJob(string inputMediaFilePath, string configurationFile)
            {
                // Create an asset and upload hello input media file toostorage.
                IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
                    "My Video Motion Detection Input Asset",
                    AssetCreationOptions.None);

                // Declare a new job.
                IJob job = _context.Jobs.Create("My Video Motion Detection Job");

                // Get a reference tooAzure Media Motion Detector.
                string MediaProcessorName = "Azure Media Motion Detector";

                var processor = GetLatestMediaProcessorByName(MediaProcessorName);

                // Read configuration from hello specified file.
                string configuration = File.ReadAllText(configurationFile);

                // Create a task with hello encoding details, using a string preset.
                ITask task = job.Tasks.AddNew("My Video Motion Detection Task",
                    processor,
                    configuration,
                    TaskOptions.None);

                // Specify hello input asset.
                task.InputAssets.Add(asset);

                // Add an output asset toocontain hello results of hello job.
                task.OutputAssets.AddNew("My Video Motion Detectoion Output Asset", AssetCreationOptions.None);

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

## <a name="media-services-learning-paths"></a><span data-ttu-id="59287-222">Ścieżki szkoleniowe dotyczące usługi Media Services</span><span class="sxs-lookup"><span data-stu-id="59287-222">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="59287-223">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="59287-223">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="59287-224">Powiązane linki</span><span class="sxs-lookup"><span data-stu-id="59287-224">Related links</span></span>
[<span data-ttu-id="59287-225">Blog Azure Media Services ruchu detektora</span><span class="sxs-lookup"><span data-stu-id="59287-225">Azure Media Services Motion Detector blog</span></span>](https://azure.microsoft.com/blog/motion-detector-update/)

[<span data-ttu-id="59287-226">Przegląd analiz usługi Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="59287-226">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

[<span data-ttu-id="59287-227">W trakcie analizy multimediów Azure</span><span class="sxs-lookup"><span data-stu-id="59287-227">Azure Media Analytics demos</span></span>](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

