---
title: "tekst aaaDigitize Rozpoznawania analizy multimediów Azure | Dokumentacja firmy Microsoft"
description: "Azure Media Rozpoznawania Analytics (OCR) umożliwia tooconvert zawartości tekstowej w plikach wideo na tekst cyfrowy można edytować, wyszukiwanie.  Dzięki temu tooautomate wyodrębniania hello łatwy do rozpoznania metadanych z hello sygnału wideo multimediów."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 307c196e-3a50-4f4b-b982-51585448ffc6
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/31/2017
ms.author: juliako
ms.openlocfilehash: 0476c3ba3942b2c5182a34a429909adbf5c75ac9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-media-analytics-tooconvert-text-content-in-video-files-into-digital-text"></a><span data-ttu-id="fae2e-104">Użycie zawartości tekstowej tooconvert analizy multimediów Azure w plikach wideo na cyfrowe tekst</span><span class="sxs-lookup"><span data-stu-id="fae2e-104">Use Azure Media Analytics tooconvert text content in video files into digital text</span></span>
## <a name="overview"></a><span data-ttu-id="fae2e-105">Omówienie</span><span class="sxs-lookup"><span data-stu-id="fae2e-105">Overview</span></span>
<span data-ttu-id="fae2e-106">Jeśli należy tekst tooextract zawartości od plików wideo i generowanie tekstu cyfrowego można edytować, wyszukiwanie, należy użyć Rozpoznawania analizy multimediów Azure (OCR).</span><span class="sxs-lookup"><span data-stu-id="fae2e-106">If you need tooextract text content from your video files and generate an editable, searchable digital text, you should use Azure Media Analytics OCR (optical character recognition).</span></span> <span data-ttu-id="fae2e-107">Ten procesor multimediów Azure wykrywa zawartości tekstowej w plikach wideo i generuje pliki tekstowe do użycia.</span><span class="sxs-lookup"><span data-stu-id="fae2e-107">This Azure Media Processor detects text content in your video files and generates text files for your use.</span></span> <span data-ttu-id="fae2e-108">Rozpoznawania umożliwia możesz tooautomate hello wyodrębniania łatwy do rozpoznania metadanych z hello sygnału wideo multimediów.</span><span class="sxs-lookup"><span data-stu-id="fae2e-108">OCR enables you tooautomate hello extraction of meaningful metadata from hello video signal of your media.</span></span>

<span data-ttu-id="fae2e-109">Gdy jest używany w połączeniu z aparatu wyszukiwania, możesz łatwo indeksu multimediów tekst i zwiększyć wykrywalność hello zawartości.</span><span class="sxs-lookup"><span data-stu-id="fae2e-109">When used in conjunction with a search engine, you can easily index your media by text, and enhance hello discoverability of your content.</span></span> <span data-ttu-id="fae2e-110">Jest to bardzo przydatne w dużej tekstową wideo, takich jak nagrywanie wideo lub Przechwytywanie ekranu prezentacji pokazu slajdów.</span><span class="sxs-lookup"><span data-stu-id="fae2e-110">This is extremely useful in highly textual video, like a video recording or screen-capture of a slideshow presentation.</span></span> <span data-ttu-id="fae2e-111">Procesor multimediów Azure Rozpoznawania Hello jest zoptymalizowana pod kątem cyfrowe tekstu.</span><span class="sxs-lookup"><span data-stu-id="fae2e-111">hello Azure OCR Media Processor is optimized for digital text.</span></span>

<span data-ttu-id="fae2e-112">Witaj **Azure Media Rozpoznawania** procesor multimediów jest obecnie w przeglądzie.</span><span class="sxs-lookup"><span data-stu-id="fae2e-112">hello **Azure Media OCR** media processor is currently in Preview.</span></span>

<span data-ttu-id="fae2e-113">Ten temat zawiera szczegółowe informacje o **Azure Media Rozpoznawania** i przedstawia sposób toouse go przy użyciu zestawu SDK usługi Media Services dla platformy .NET.</span><span class="sxs-lookup"><span data-stu-id="fae2e-113">This topic gives details about  **Azure Media OCR** and shows how toouse it with Media Services SDK for .NET.</span></span> <span data-ttu-id="fae2e-114">Aby uzyskać dodatkowe informacje i przykłady, zobacz [ten blog](https://azure.microsoft.com/blog/announcing-video-ocr-public-preview-new-config/).</span><span class="sxs-lookup"><span data-stu-id="fae2e-114">For additional information and examples, see [this blog](https://azure.microsoft.com/blog/announcing-video-ocr-public-preview-new-config/).</span></span>

## <a name="ocr-input-files"></a><span data-ttu-id="fae2e-115">Rozpoznawania plików wejściowych</span><span class="sxs-lookup"><span data-stu-id="fae2e-115">OCR input files</span></span>
<span data-ttu-id="fae2e-116">Pliki wideo.</span><span class="sxs-lookup"><span data-stu-id="fae2e-116">Video files.</span></span> <span data-ttu-id="fae2e-117">Obecnie są obsługiwane następujące formaty hello: MP4, MOV i WMV.</span><span class="sxs-lookup"><span data-stu-id="fae2e-117">Currently, hello following formats are supported: MP4, MOV, and WMV.</span></span>

## <a name="task-configuration"></a><span data-ttu-id="fae2e-118">Konfiguracja zadania</span><span class="sxs-lookup"><span data-stu-id="fae2e-118">Task configuration</span></span>
<span data-ttu-id="fae2e-119">Konfiguracja zadania (ustawienia domyślne).</span><span class="sxs-lookup"><span data-stu-id="fae2e-119">Task configuration (preset).</span></span> <span data-ttu-id="fae2e-120">Podczas tworzenia zadania z **Azure Media Rozpoznawania**, należy określić ustawienia wstępnego za pomocą formatu JSON i XML konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="fae2e-120">When creating a task with **Azure Media OCR**, you must specify a configuration preset using JSON  or XML.</span></span> 

>[!NOTE]
><span data-ttu-id="fae2e-121">Aparat Rozpoznawania Hello przyjmuje tylko obszar obrazu z minimalną pikseli toomaximum 32000 40 pikseli jako prawidłową wartość wejściową w obu wysokość i szerokość.</span><span class="sxs-lookup"><span data-stu-id="fae2e-121">hello OCR engine only takes an image region with minimum 40 pixels toomaximum 32000 pixels as a valid input in both height/width.</span></span>
>

### <a name="attribute-descriptions"></a><span data-ttu-id="fae2e-122">Opisy atrybutów</span><span class="sxs-lookup"><span data-stu-id="fae2e-122">Attribute descriptions</span></span>
| <span data-ttu-id="fae2e-123">Nazwa atrybutu</span><span class="sxs-lookup"><span data-stu-id="fae2e-123">Attribute name</span></span> | <span data-ttu-id="fae2e-124">Opis</span><span class="sxs-lookup"><span data-stu-id="fae2e-124">Description</span></span> |
| --- | --- |
|<span data-ttu-id="fae2e-125">AdvancedOutput</span><span class="sxs-lookup"><span data-stu-id="fae2e-125">AdvancedOutput</span></span>| <span data-ttu-id="fae2e-126">Jeśli ustawisz AdvancedOutput tootrue dane wyjściowe JSON hello zawierają dane pozycyjnych dla każdego pojedynczego wyrazu (w regionach i dodanie toophrases).</span><span class="sxs-lookup"><span data-stu-id="fae2e-126">If you set AdvancedOutput tootrue, hello JSON output will contain positional data for every single word (in addition toophrases and regions).</span></span> <span data-ttu-id="fae2e-127">Jeśli nie chcesz, aby toosee te szczegóły zestawu hello Flaga toofalse.</span><span class="sxs-lookup"><span data-stu-id="fae2e-127">If you do not want toosee these details, set hello flag toofalse.</span></span> <span data-ttu-id="fae2e-128">Witaj wartość domyślna to false.</span><span class="sxs-lookup"><span data-stu-id="fae2e-128">hello default value is false.</span></span> <span data-ttu-id="fae2e-129">Aby uzyskać więcej informacji, zobacz [ten blog](https://azure.microsoft.com/blog/azure-media-ocr-simplified-output/).</span><span class="sxs-lookup"><span data-stu-id="fae2e-129">For more information, see [this blog](https://azure.microsoft.com/blog/azure-media-ocr-simplified-output/).</span></span>|
| <span data-ttu-id="fae2e-130">Język</span><span class="sxs-lookup"><span data-stu-id="fae2e-130">Language</span></span> |<span data-ttu-id="fae2e-131">(opcjonalnie) opisano hello język tekstu, dla których toolook.</span><span class="sxs-lookup"><span data-stu-id="fae2e-131">(optional) describes hello language of text for which toolook.</span></span> <span data-ttu-id="fae2e-132">Jedną z następujących hello: AutoDetect (ustawienie domyślne), arabskiego, ChineseSimplified, ChineseTraditional, czeski, duński, holenderski, angielski, fiński, francuski, niemiecki, grecki, węgierski, włoski, japoński, koreański, norweski, Polski, portugalski, rumuński, rosyjski, SerbianCyrillic, SerbianLatin, słowacki, hiszpański, szwedzki, turecki.</span><span class="sxs-lookup"><span data-stu-id="fae2e-132">One of hello following: AutoDetect (default), Arabic, ChineseSimplified, ChineseTraditional, Czech Danish, Dutch, English, Finnish, French, German,  Greek, Hungarian, Italian, Japanese, Korean, Norwegian, Polish, Portuguese, Romanian, Russian, SerbianCyrillic, SerbianLatin, Slovak, Spanish, Swedish, Turkish.</span></span> |
| <span data-ttu-id="fae2e-133">TextOrientation</span><span class="sxs-lookup"><span data-stu-id="fae2e-133">TextOrientation</span></span> |<span data-ttu-id="fae2e-134">(opcjonalnie) opisano hello orientację tekstu, dla których toolook.</span><span class="sxs-lookup"><span data-stu-id="fae2e-134">(optional) describes hello orientation of text for which toolook.</span></span>  <span data-ttu-id="fae2e-135">"Po lewej stronie" oznacza, że hello początku wszystkie litery są skierowane hello lewej.</span><span class="sxs-lookup"><span data-stu-id="fae2e-135">"Left" means that hello top of all letters are pointed towards hello left.</span></span>  <span data-ttu-id="fae2e-136">Domyślny tekst (na przykład tych, które można znaleźć w księdze) można wywołać "W górę" orientacji.</span><span class="sxs-lookup"><span data-stu-id="fae2e-136">Default text (like that which can be found in a book) can be called "Up" oriented.</span></span>  <span data-ttu-id="fae2e-137">Jedną z następujących hello: AutoDetect (ustawienie domyślne), maksymalnie, prawo, w dół, lewo.</span><span class="sxs-lookup"><span data-stu-id="fae2e-137">One of hello following: AutoDetect (default), Up, Right, Down, Left.</span></span> |
| <span data-ttu-id="fae2e-138">Parametru TimeInterval</span><span class="sxs-lookup"><span data-stu-id="fae2e-138">TimeInterval</span></span> |<span data-ttu-id="fae2e-139">(opcjonalnie) opisano hello próbkowania.</span><span class="sxs-lookup"><span data-stu-id="fae2e-139">(optional) describes hello sampling rate.</span></span>  <span data-ttu-id="fae2e-140">Domyślna to co 1/2 sekundy.</span><span class="sxs-lookup"><span data-stu-id="fae2e-140">Default is every 1/2 second.</span></span><br/><span data-ttu-id="fae2e-141">Format JSON — hh: mm:. SSS (00:00:00.500 domyślne)</span><span class="sxs-lookup"><span data-stu-id="fae2e-141">JSON format – HH:mm:ss.SSS (default 00:00:00.500)</span></span><br/><span data-ttu-id="fae2e-142">Format XML — podstawowy czas trwania W3C XSD (domyślnie PT0.5)</span><span class="sxs-lookup"><span data-stu-id="fae2e-142">XML format – W3C XSD duration primitive (default PT0.5)</span></span> |
| <span data-ttu-id="fae2e-143">DetectRegions</span><span class="sxs-lookup"><span data-stu-id="fae2e-143">DetectRegions</span></span> |<span data-ttu-id="fae2e-144">(opcjonalnie) Tablica obiektów DetectRegion określenie obszarów w ramce wideo hello w tekst, który toodetect.</span><span class="sxs-lookup"><span data-stu-id="fae2e-144">(optional) An array of DetectRegion objects specifying regions within hello video frame in which toodetect text.</span></span><br/><span data-ttu-id="fae2e-145">Obiekt DetectRegion się następujące cztery wartości całkowite hello:</span><span class="sxs-lookup"><span data-stu-id="fae2e-145">A DetectRegion object is made of hello following four integer values:</span></span><br/><span data-ttu-id="fae2e-146">Po lewej — pikseli z powitania od lewego marginesu</span><span class="sxs-lookup"><span data-stu-id="fae2e-146">Left – pixels from hello left-margin</span></span><br/><span data-ttu-id="fae2e-147">TOP — pikseli z margines górny hello</span><span class="sxs-lookup"><span data-stu-id="fae2e-147">Top – pixels from hello top-margin</span></span><br/><span data-ttu-id="fae2e-148">Szerokość — Szerokość hello regionu w pikselach</span><span class="sxs-lookup"><span data-stu-id="fae2e-148">Width – width of hello region in pixels</span></span><br/><span data-ttu-id="fae2e-149">Wysokość — wysokość hello regionu w pikselach</span><span class="sxs-lookup"><span data-stu-id="fae2e-149">Height – height of hello region in pixels</span></span> |

#### <a name="json-preset-example"></a><span data-ttu-id="fae2e-150">Przykład predefiniowanych JSON</span><span class="sxs-lookup"><span data-stu-id="fae2e-150">JSON preset example</span></span>

    {
        "Version":1.0, 
        "Options": 
        {
            "AdvancedOutput":"true",
            "Language":"English", 
            "TimeInterval":"00:00:01.5",
            "TextOrientation":"Up",
            "DetectRegions": [
                    {
                       "Left": 10,
                       "Top": 10,
                       "Width": 100,
                       "Height": 50
                    }
             ]
        }
    }


#### <a name="xml-preset-example"></a><span data-ttu-id="fae2e-151">Przykład wstępnie zdefiniowane w pliku XML</span><span class="sxs-lookup"><span data-stu-id="fae2e-151">XML preset example</span></span>
    <?xml version=""1.0"" encoding=""utf-16""?>
    <VideoOcrPreset xmlns:xsi=""http://www.w3.org/2001/XMLSchema-instance"" xmlns:xsd=""http://www.w3.org/2001/XMLSchema"" Version=""1.0"" xmlns=""http://www.windowsazure.com/media/encoding/Preset/2014/03"">
      <Options>
         <AdvancedOutput>true</AdvancedOutput>
         <Language>English</Language>
         <TimeInterval>PT1.5S</TimeInterval>
         <DetectRegions>
             <DetectRegion>
                   <Left>10</Left>
                   <Top>10</Top>
                   <Width>100</Width>
                   <Height>50</Height>
            </DetectRegion>
       </DetectRegions>
       <TextOrientation>Up</TextOrientation>
      </Options>
    </VideoOcrPreset>

## <a name="ocr-output-files"></a><span data-ttu-id="fae2e-152">Pliki wyjściowe Rozpoznawania</span><span class="sxs-lookup"><span data-stu-id="fae2e-152">OCR output files</span></span>
<span data-ttu-id="fae2e-153">dane wyjściowe Hello procesor multimediów Rozpoznawania hello jest to plik JSON.</span><span class="sxs-lookup"><span data-stu-id="fae2e-153">hello output of hello OCR media processor is a JSON file.</span></span>

### <a name="elements-of-hello-output-json-file"></a><span data-ttu-id="fae2e-154">Elementy hello pliku wyjściowego w formacie JSON</span><span class="sxs-lookup"><span data-stu-id="fae2e-154">Elements of hello output JSON file</span></span>
<span data-ttu-id="fae2e-155">Wyjście wideo Rozpoznawania Hello udostępnia dane segmentem czas na powitania znaków wideo.</span><span class="sxs-lookup"><span data-stu-id="fae2e-155">hello Video OCR output provides time-segmented data on hello characters found in your video.</span></span>  <span data-ttu-id="fae2e-156">Można użyć atrybutów, takich jak języka lub orientacji toohone w dokładnie słowa hello wybrane analizowanie.</span><span class="sxs-lookup"><span data-stu-id="fae2e-156">You can use attributes such as language or orientation toohone-in on exactly hello words that you are interested in analyzing.</span></span> 

<span data-ttu-id="fae2e-157">dane wyjściowe Hello zawierają hello następujące atrybuty:</span><span class="sxs-lookup"><span data-stu-id="fae2e-157">hello output contains hello following attributes:</span></span>

| <span data-ttu-id="fae2e-158">Element</span><span class="sxs-lookup"><span data-stu-id="fae2e-158">Element</span></span> | <span data-ttu-id="fae2e-159">Opis</span><span class="sxs-lookup"><span data-stu-id="fae2e-159">Description</span></span> |
| --- | --- |
| <span data-ttu-id="fae2e-160">skali czasu</span><span class="sxs-lookup"><span data-stu-id="fae2e-160">Timescale</span></span> |<span data-ttu-id="fae2e-161">"Takty" na sekundę hello wideo</span><span class="sxs-lookup"><span data-stu-id="fae2e-161">"ticks" per second of hello video</span></span> |
| <span data-ttu-id="fae2e-162">Przesunięcie</span><span class="sxs-lookup"><span data-stu-id="fae2e-162">Offset</span></span> |<span data-ttu-id="fae2e-163">Czas przesunięcia znaczników czasu.</span><span class="sxs-lookup"><span data-stu-id="fae2e-163">time offset for timestamps.</span></span> <span data-ttu-id="fae2e-164">W wersji 1.0 interfejsów API, wideo ta będzie zawsze równa 0.</span><span class="sxs-lookup"><span data-stu-id="fae2e-164">In version 1.0 of Video APIs, this will always be 0.</span></span> |
| <span data-ttu-id="fae2e-165">szybkość klatek</span><span class="sxs-lookup"><span data-stu-id="fae2e-165">Framerate</span></span> |<span data-ttu-id="fae2e-166">Klatek na sekundę hello wideo</span><span class="sxs-lookup"><span data-stu-id="fae2e-166">Frames per second of hello video</span></span> |
| <span data-ttu-id="fae2e-167">Szerokość</span><span class="sxs-lookup"><span data-stu-id="fae2e-167">width</span></span> |<span data-ttu-id="fae2e-168">szerokość hello wideo w pikselach</span><span class="sxs-lookup"><span data-stu-id="fae2e-168">width of hello video in pixels</span></span> |
| <span data-ttu-id="fae2e-169">Wysokość</span><span class="sxs-lookup"><span data-stu-id="fae2e-169">height</span></span> |<span data-ttu-id="fae2e-170">wysokość hello wideo w pikselach</span><span class="sxs-lookup"><span data-stu-id="fae2e-170">height of hello video in pixels</span></span> |
| <span data-ttu-id="fae2e-171">fragmenty</span><span class="sxs-lookup"><span data-stu-id="fae2e-171">Fragments</span></span> |<span data-ttu-id="fae2e-172">Tablica oparte na czasie fragmentów wideo, w których hello jest fragmentaryczne metadanych</span><span class="sxs-lookup"><span data-stu-id="fae2e-172">array of time-based chunks of video into which hello metadata is chunked</span></span> |
| <span data-ttu-id="fae2e-173">rozpoczynanie</span><span class="sxs-lookup"><span data-stu-id="fae2e-173">start</span></span> |<span data-ttu-id="fae2e-174">uruchomienie fragmentu w parametrem "ticks"</span><span class="sxs-lookup"><span data-stu-id="fae2e-174">start time of a fragment in "ticks"</span></span> |
| <span data-ttu-id="fae2e-175">Czas trwania</span><span class="sxs-lookup"><span data-stu-id="fae2e-175">duration</span></span> |<span data-ttu-id="fae2e-176">Długość fragmentu w parametrem "ticks"</span><span class="sxs-lookup"><span data-stu-id="fae2e-176">length of a fragment in "ticks"</span></span> |
| <span data-ttu-id="fae2e-177">interval</span><span class="sxs-lookup"><span data-stu-id="fae2e-177">interval</span></span> |<span data-ttu-id="fae2e-178">Interwał każdego zdarzenia w ciągu danego fragmentu hello</span><span class="sxs-lookup"><span data-stu-id="fae2e-178">interval of each event within hello given fragment</span></span> |
| <span data-ttu-id="fae2e-179">zdarzenia</span><span class="sxs-lookup"><span data-stu-id="fae2e-179">events</span></span> |<span data-ttu-id="fae2e-180">Tablica zawierająca regionów</span><span class="sxs-lookup"><span data-stu-id="fae2e-180">array containing regions</span></span> |
| <span data-ttu-id="fae2e-181">Region</span><span class="sxs-lookup"><span data-stu-id="fae2e-181">region</span></span> |<span data-ttu-id="fae2e-182">Obiekt reprezentujący wykryto słów ani fraz</span><span class="sxs-lookup"><span data-stu-id="fae2e-182">object representing detected words or phrases</span></span> |
| <span data-ttu-id="fae2e-183">Język</span><span class="sxs-lookup"><span data-stu-id="fae2e-183">language</span></span> |<span data-ttu-id="fae2e-184">język tekstu hello wykryte w obrębie regionu</span><span class="sxs-lookup"><span data-stu-id="fae2e-184">language of hello text detected within a region</span></span> |
| <span data-ttu-id="fae2e-185">Orientacja</span><span class="sxs-lookup"><span data-stu-id="fae2e-185">orientation</span></span> |<span data-ttu-id="fae2e-186">orientację tekstu hello wykryte w obrębie regionu</span><span class="sxs-lookup"><span data-stu-id="fae2e-186">orientation of hello text detected within a region</span></span> |
| <span data-ttu-id="fae2e-187">wiersze</span><span class="sxs-lookup"><span data-stu-id="fae2e-187">lines</span></span> |<span data-ttu-id="fae2e-188">Tablica wierszy tekstu w regionie</span><span class="sxs-lookup"><span data-stu-id="fae2e-188">array of lines of text detected within a region</span></span> |
| <span data-ttu-id="fae2e-189">Tekst</span><span class="sxs-lookup"><span data-stu-id="fae2e-189">text</span></span> |<span data-ttu-id="fae2e-190">Witaj tekstu</span><span class="sxs-lookup"><span data-stu-id="fae2e-190">hello actual text</span></span> |

### <a name="json-output-example"></a><span data-ttu-id="fae2e-191">Przykład danych wyjściowych JSON</span><span class="sxs-lookup"><span data-stu-id="fae2e-191">JSON output example</span></span>
<span data-ttu-id="fae2e-192">Witaj poniższym przykładzie danych wyjściowych zawiera ogólne informacje wideo hello oraz kilka fragmentów wideo.</span><span class="sxs-lookup"><span data-stu-id="fae2e-192">hello following output example contains hello general video information and several video fragments.</span></span> <span data-ttu-id="fae2e-193">W każdym wideo fragmentu zawiera każdego regionu, który jest wykrywany przez pakiet administracyjny Rozpoznawania z językiem hello i orientacji tekstu.</span><span class="sxs-lookup"><span data-stu-id="fae2e-193">In every video fragment, it contains every region which is detected by OCR MP with hello language and its text orientation.</span></span> <span data-ttu-id="fae2e-194">Hello region zawiera także każdy wiersz programu word w tym regionie tekst hello wiersza, pozycja hello wiersza i informacje co word (zawartość programu word, pozycji i zaufania) w tym wierszu.</span><span class="sxs-lookup"><span data-stu-id="fae2e-194">hello region also contains every word line in this region with hello line’s text, hello line’s position, and every word information (word content, position and confidence) in this line.</span></span> <span data-ttu-id="fae2e-195">Hello poniżej przedstawiono przykładowy i umieścić niektóre wbudowane komentarze.</span><span class="sxs-lookup"><span data-stu-id="fae2e-195">hello following is an example, and I put some comments inline.</span></span>

    {
        "version": 1, 
        "timescale": 90000, 
        "offset": 0, 
        "framerate": 30, 
        "width": 640, 
        "height": 480,  // general video information
        "fragments": [
            {
                "start": 0, 
                "duration": 180000, 
                "interval": 90000,  // hello time information about this fragment
                "events": [
                    [
                       { 
                            "region": { // hello detected region array in this fragment 
                                "language": "English",  // region language
                                "orientation": "Up",  // text orientation
                                "lines": [  // line information array in this region, including hello text and hello position
                                    {
                                        "text": "One Two", 
                                        "left": 10, 
                                        "top": 10, 
                                        "right": 210, 
                                        "bottom": 110, 
                                        "word": [  // word information array in this line
                                            {
                                                "text": "One", 
                                                "left": 10, 
                                                "top": 10, 
                                                "right": 110, 
                                                "bottom": 110, 
                                                "confidence": 900
                                            }, 
                                            {
                                                "text": "Two", 
                                                "left": 110, 
                                                "top": 10, 
                                                "right": 210, 
                                                "bottom": 110, 
                                                "confidence": 910
                                            }
                                        ]
                                    }
                                ]
                            }
                        }
                    ]
                ]
            }
        ]
    }

## <a name="net-sample-code"></a><span data-ttu-id="fae2e-196">.NET przykładowy kod</span><span class="sxs-lookup"><span data-stu-id="fae2e-196">.NET sample code</span></span>

<span data-ttu-id="fae2e-197">następujące Hello program pokazuje sposób:</span><span class="sxs-lookup"><span data-stu-id="fae2e-197">hello following program shows how to:</span></span>

1. <span data-ttu-id="fae2e-198">Utworzenie elementu zawartości i przesyłanie pliku multimediów do hello zawartości.</span><span class="sxs-lookup"><span data-stu-id="fae2e-198">Create an asset and upload a media file into hello asset.</span></span>
2. <span data-ttu-id="fae2e-199">Utwórz zadanie przy użyciu pliku konfiguracji/ustawienie wstępne Rozpoznawania.</span><span class="sxs-lookup"><span data-stu-id="fae2e-199">Create a job with an OCR configuration/preset file.</span></span>
3. <span data-ttu-id="fae2e-200">Pobierz pliki w formacie JSON dane wyjściowe hello.</span><span class="sxs-lookup"><span data-stu-id="fae2e-200">Download hello output JSON files.</span></span> 
   
#### <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="fae2e-201">Tworzenie i konfigurowanie projektu programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="fae2e-201">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="fae2e-202">Konfigurowanie środowiska projektowego i wypełnić plik app.config hello o informacje dotyczące połączenia, zgodnie z opisem w [tworzenia usługi Media Services z platformą .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="fae2e-202">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

#### <a name="example"></a><span data-ttu-id="fae2e-203">Przykład</span><span class="sxs-lookup"><span data-stu-id="fae2e-203">Example</span></span>

    using System;
    using System.Configuration;
    using System.IO;
    using System.Linq;
    using Microsoft.WindowsAzure.MediaServices.Client;
    using System.Threading;
    using System.Threading.Tasks;

    namespace OCR
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

                // Run hello OCR job.
                var asset = RunOCRJob(@"C:\supportFiles\OCR\presentation.mp4",
                                            @"C:\supportFiles\OCR\config.json");

                // Download hello job output asset.
                DownloadAsset(asset, @"C:\supportFiles\OCR\Output");
            }

            static IAsset RunOCRJob(string inputMediaFilePath, string configurationFile)
            {
                // Create an asset and upload hello input media file toostorage.
                IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
                    "My OCR Input Asset",
                    AssetCreationOptions.None);

                // Declare a new job.
                IJob job = _context.Jobs.Create("My OCR Job");

                // Get a reference tooAzure Media OCR.
                string MediaProcessorName = "Azure Media OCR";

                var processor = GetLatestMediaProcessorByName(MediaProcessorName);

                // Read configuration from hello specified file.
                string configuration = File.ReadAllText(configurationFile);

                // Create a task with hello encoding details, using a string preset.
                ITask task = job.Tasks.AddNew("My OCR Task",
                    processor,
                    configuration,
                    TaskOptions.None);

                // Specify hello input asset.
                task.InputAssets.Add(asset);

                // Add an output asset toocontain hello results of hello job.
                task.OutputAssets.AddNew("My OCR Output Asset", AssetCreationOptions.None);

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

## <a name="media-services-learning-paths"></a><span data-ttu-id="fae2e-204">Ścieżki szkoleniowe dotyczące usługi Media Services</span><span class="sxs-lookup"><span data-stu-id="fae2e-204">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="fae2e-205">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="fae2e-205">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="fae2e-206">Powiązane linki</span><span class="sxs-lookup"><span data-stu-id="fae2e-206">Related links</span></span>
[<span data-ttu-id="fae2e-207">Przegląd analiz usługi Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="fae2e-207">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

