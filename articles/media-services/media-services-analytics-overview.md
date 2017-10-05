---
title: "Analiza multimediów na platformie Media Services | Dokumentacja firmy Microsoft"
description: "Omówienie publicznej wersji zapoznawczej z analizy multimediów, Kolekcja usług wizji mowy i komputera w skali przedsiębiorstwa, zgodności i zabezpieczeń oraz globalne"
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: c56e3781-8510-4f7f-b5ff-a218c1bb6f4c
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2017
ms.author: milanga;juliako;johndeu
ms.openlocfilehash: c0bbe6f80370515fa783b12757434897fe2221b6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="media-analytics-on-the-media-services-platform"></a><span data-ttu-id="d6212-103">Analiza multimediów na platformie Media Services</span><span class="sxs-lookup"><span data-stu-id="d6212-103">Media Analytics on the Media Services platform</span></span>
## <a name="overview"></a><span data-ttu-id="d6212-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="d6212-104">Overview</span></span>
<span data-ttu-id="d6212-105">Więcej organizacji korzystają wideo jako preferowany średni uczenia pracownikom, zaangażowania klientów i udokumentować znaczenie biznesowe.</span><span class="sxs-lookup"><span data-stu-id="d6212-105">More organizations are using video as the preferred medium to train their employees, engage their customers, and document business functions.</span></span> <span data-ttu-id="d6212-106">Przetwarzania umożliwia przechowywanie, strumienia i dostępu do tych duże pliki multimedialne w chmurze.</span><span class="sxs-lookup"><span data-stu-id="d6212-106">Cloud computing provides a way to store, stream, and access these large media files.</span></span> <span data-ttu-id="d6212-107">Jednak wraz z rozwojem firmy biblioteki zawartości wideo, musi on równie skuteczne środki wyodrębniania wgląd w zawartość.</span><span class="sxs-lookup"><span data-stu-id="d6212-107">But as a company's library of video content grows, it needs an equally effective means of extracting insights from the content.</span></span> 

<span data-ttu-id="d6212-108">Aby rozwiązać ten wzrasta potrzeba, usługi Azure Media Services udostępnia analizy multimediów Azure.</span><span class="sxs-lookup"><span data-stu-id="d6212-108">To address this growing need, Azure Media Services offers Azure Media Analytics.</span></span> <span data-ttu-id="d6212-109">Analiza multimediów to kolekcja składników mowy i obrazu, które ułatwiają organizacjom i przedsiębiorstwom pozyskiwanie przydatnych informacji z posiadanych plików wideo.</span><span class="sxs-lookup"><span data-stu-id="d6212-109">Media Analytics is a collection of speech and vision components that makes it easier for organizations and enterprises to derive actionable insights from their video files.</span></span> <span data-ttu-id="d6212-110">Utworzony przy użyciu podstawowe składniki platformy Media Services, analiza multimediów może obsługiwać nośnika przetwarzania na dużą skalę na jeden dzień.</span><span class="sxs-lookup"><span data-stu-id="d6212-110">Built by using the core Media Services platform components, Media Analytics can handle media processing at scale on day one.</span></span>

<span data-ttu-id="d6212-111">Z analizy multimediów deweloperzy mogą szybko Przełącz zaawansowane funkcje wideo do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d6212-111">With Media Analytics, developers can quickly bring advanced video functionality into applications.</span></span> <span data-ttu-id="d6212-112">Przedsiębiorstw zapewnia skali, zgodności, zabezpieczeń oraz globalne wymagane przez dużych organizacji.</span><span class="sxs-lookup"><span data-stu-id="d6212-112">It provides enterprise environments with the full scale, compliance, security, and global reach required by large organizations.</span></span>

<span data-ttu-id="d6212-113">Na poniższym diagramie przedstawiono analizy multimediów i inne główne elementy platformy Media Services.</span><span class="sxs-lookup"><span data-stu-id="d6212-113">The following diagram shows Media Analytics and other major parts of the Media Services platform.</span></span> 

![Wideo na żądanie — przepływ pracy](./media/media-services-analytics-overview/media-services-analytics-overview01.png)

<span data-ttu-id="d6212-115">Procesory multimediów usługi Analiza multimediów tworzą pliki MP4 lub JSON.</span><span class="sxs-lookup"><span data-stu-id="d6212-115">Media Analytics media processors produce MP4 files or JSON files.</span></span> <span data-ttu-id="d6212-116">Jeśli procesor multimediów tworzy plik MP4, można pobrać progresywnie pliku.</span><span class="sxs-lookup"><span data-stu-id="d6212-116">If a media processor produces an MP4 file, you can progressively download the file.</span></span> <span data-ttu-id="d6212-117">Jeśli procesor multimediów powoduje utworzenie pliku JSON, możesz pobrać plik z magazynu obiektów Blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d6212-117">If a media processor produces a JSON file, you can download the file from Azure Blob storage.</span></span> 

## <a name="media-analytics-services"></a><span data-ttu-id="d6212-118">Usług analizy multimediów</span><span class="sxs-lookup"><span data-stu-id="d6212-118">Media Analytics services</span></span>

### <a name="indexer"></a><span data-ttu-id="d6212-119">Indeksator</span><span class="sxs-lookup"><span data-stu-id="d6212-119">Indexer</span></span>
<span data-ttu-id="d6212-120">Z usługi Azure Media indeksatora możesz wprowadzić zawartości można wyszukiwać i generować-kodowane ścieżki.</span><span class="sxs-lookup"><span data-stu-id="d6212-120">With Azure Media Indexer, you can make content searchable and generate closed-captioning tracks.</span></span> <span data-ttu-id="d6212-121">W porównaniu do poprzednich wersji Preview 2 indeksatora multimediów Azure ma szybciej indeksowania i szerszych języka obsługuje.</span><span class="sxs-lookup"><span data-stu-id="d6212-121">Compared to the previous version, Azure Media Indexer 2 Preview has faster indexing and broader language support.</span></span> <span data-ttu-id="d6212-122">Obsługiwane języki angielski, hiszpański, francuski, niemiecki, włoski, chiński, portugalski i arabski.</span><span class="sxs-lookup"><span data-stu-id="d6212-122">Supported languages include English, Spanish, French, German, Italian, Chinese, Portuguese, and Arabic.</span></span> <span data-ttu-id="d6212-123">Aby uzyskać szczegółowe informacje i przykłady, zobacz [przetwarzanie plików wideo z usługi Azure Media Indexer 2](media-services-process-content-with-indexer2.md).</span><span class="sxs-lookup"><span data-stu-id="d6212-123">For detailed information and examples, see [Process videos with Azure Media Indexer 2](media-services-process-content-with-indexer2.md).</span></span>
### <a name="hyperlapse"></a><span data-ttu-id="d6212-124">Hyperlapse</span><span class="sxs-lookup"><span data-stu-id="d6212-124">Hyperlapse</span></span>
<span data-ttu-id="d6212-125">Microsoft Hyperlapse łączy stabilizacji wideo i ujęć poklatkowych możliwości tworzenia szybkie, eksploatacyjny filmy wideo z zawartości długiej.</span><span class="sxs-lookup"><span data-stu-id="d6212-125">Microsoft Hyperlapse combines video stabilization and time-lapse capability to create quick, consumable videos from your long-form content.</span></span> <span data-ttu-id="d6212-126">Oprócz tworzenia ujęć poklatkowych wideo, przyspieszonych ujęć poklatkowych służy również do tworzenia stabilna filmy wideo z obraz wideo przechwycone przez telefony komórkowe i kamery.</span><span class="sxs-lookup"><span data-stu-id="d6212-126">Besides creating time-lapse video, you can use Hyperlapse to create stable videos from shaky videos captured via cell phones and camcorders.</span></span> <span data-ttu-id="d6212-127">Aby uzyskać szczegółowe informacje i przykłady, zobacz [przyspieszonych ujęć poklatkowych plików multimedialnych na pliki z usługi Azure Media Hyperlapse](media-services-hyperlapse-content.md).</span><span class="sxs-lookup"><span data-stu-id="d6212-127">For detailed information and examples, see [Hyperlapse media files with Azure Media Hyperlapse](media-services-hyperlapse-content.md).</span></span>
### <a name="motion-detector"></a><span data-ttu-id="d6212-128">Wykrywanie ruchu</span><span class="sxs-lookup"><span data-stu-id="d6212-128">Motion Detector</span></span>
<span data-ttu-id="d6212-129">Czujnik ruchu można użyć do wykrywania ruchu na obrazie wideo z nieruchomy tła.</span><span class="sxs-lookup"><span data-stu-id="d6212-129">You can use Motion Detector to detect motion in a video with stationary backgrounds.</span></span> <span data-ttu-id="d6212-130">Dzięki temu można wyszukać fałszywych alarmów zdarzeń ruchu wykrywane przez kamer nadzoru.</span><span class="sxs-lookup"><span data-stu-id="d6212-130">This makes it possible to check for false positives on motion events detected by surveillance cameras.</span></span> <span data-ttu-id="d6212-131">Aby uzyskać szczegółowe informacje i przykłady, zobacz [wykrywanie na potrzeby analizy multimediów Azure ruchu](media-services-motion-detection.md).</span><span class="sxs-lookup"><span data-stu-id="d6212-131">For detailed information and examples, see [Motion detection for Azure Media Analytics](media-services-motion-detection.md).</span></span>
### <a name="face-detector"></a><span data-ttu-id="d6212-132">Wykrywanie twarzy</span><span class="sxs-lookup"><span data-stu-id="d6212-132">Face Detector</span></span>
<span data-ttu-id="d6212-133">Przy użyciu detektora krój, można wykryć powierzchni użytkowników i ich emocji, w tym szczęście, sadness i niespodziewanego.</span><span class="sxs-lookup"><span data-stu-id="d6212-133">By using Face Detector, you can detect people’s faces and their emotions, including happiness, sadness, and surprise.</span></span> <span data-ttu-id="d6212-134">To ma kilka przydatne branży aplikacji, w dalszej części, tym agregowanie i analizowanie danych reakcji uczestników zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="d6212-134">This has several useful industry applications, described later, including aggregating and analyzing reactions of people attending an event.</span></span> <span data-ttu-id="d6212-135">Aby uzyskać szczegółowe informacje i przykłady, zobacz [wykrywania twarzy na obrazie i emocji dla analizy multimediów Azure](media-services-face-and-emotion-detection.md).</span><span class="sxs-lookup"><span data-stu-id="d6212-135">For detailed information and examples, see [Face and emotion detection for Azure Media Analytics](media-services-face-and-emotion-detection.md).</span></span>
### <a name="video-summarization"></a><span data-ttu-id="d6212-136">Podsumowanie wideo</span><span class="sxs-lookup"><span data-stu-id="d6212-136">Video summarization</span></span>
<span data-ttu-id="d6212-137">Podsumowanie wideo mogą pomóc tworzyć podsumowania długich filmów wideo, wybierając automatycznie interesujące fragmenty kodu ze źródła wideo.</span><span class="sxs-lookup"><span data-stu-id="d6212-137">Video summarization can help you create summaries of long videos by automatically selecting interesting snippets from the source video.</span></span> <span data-ttu-id="d6212-138">Ta możliwość jest przydatne, gdy chcesz zapewnić szybki przegląd czego można oczekiwać w długich wideo.</span><span class="sxs-lookup"><span data-stu-id="d6212-138">This ability is useful when you want to provide a quick overview of what to expect in a long video.</span></span> <span data-ttu-id="d6212-139">Aby uzyskać szczegółowe informacje i przykłady, zobacz [miniatur wideo multimediów Azure Użyj utworzyć podsumowanie wideo](media-services-video-summarization.md).</span><span class="sxs-lookup"><span data-stu-id="d6212-139">For detailed information and examples, see [Use Azure Media Video Thumbnails to create video summarization](media-services-video-summarization.md).</span></span>
### <a name="optical-character-recognition"></a><span data-ttu-id="d6212-140">Optyczne rozpoznawanie znaków</span><span class="sxs-lookup"><span data-stu-id="d6212-140">Optical character recognition</span></span>
<span data-ttu-id="d6212-141">Z usługi Azure Media Rozpoznawania (OCR) zawartość tekstu w plikach wideo można przekonwertować na tekst cyfrowy można edytować, wyszukiwanie.</span><span class="sxs-lookup"><span data-stu-id="d6212-141">With Azure Media OCR (optical character recognition), you can convert text content in video files into editable, searchable digital text.</span></span> <span data-ttu-id="d6212-142">Następnie można zautomatyzować wyodrębniania łatwy do rozpoznania metadanych z sygnału wideo multimediów.</span><span class="sxs-lookup"><span data-stu-id="d6212-142">You can then automate the extraction of meaningful metadata from the video signal of your media.</span></span>
### <a name="scalable-face-redaction"></a><span data-ttu-id="d6212-143">Skalowalna krój redakcyjne</span><span class="sxs-lookup"><span data-stu-id="d6212-143">Scalable face redaction</span></span>
<span data-ttu-id="d6212-144">Azure Media Redactor jest procesora nośnika analizy multimediów, które oferuje skalowalne krój redakcyjne w chmurze.</span><span class="sxs-lookup"><span data-stu-id="d6212-144">Azure Media Redactor is a Media Analytics media processor that offers scalable face redaction in the cloud.</span></span> <span data-ttu-id="d6212-145">Za pomocą redakcyjne krój, można zmodyfikować wideo do rozmycia kroje wybrane osoby.</span><span class="sxs-lookup"><span data-stu-id="d6212-145">By using face redaction, you can modify your video to blur faces of selected individuals.</span></span> <span data-ttu-id="d6212-146">Można korzystać z usługi redakcyjne krój, na nośniku wiadomości lub uczestniczy bezpieczeństwa publicznego.</span><span class="sxs-lookup"><span data-stu-id="d6212-146">You might want to use the face redaction service in news media or when public safety is involved.</span></span> <span data-ttu-id="d6212-147">Kilka minut najmniejszym zawiera wiele kroje może zająć godzin redagowanie ręcznie, ale z tą usługą redakcyjne krój trwa tylko kilka prostych kroków.</span><span class="sxs-lookup"><span data-stu-id="d6212-147">A few minutes of footage that contains multiple faces can take hours to redact manually, but with this service, face redaction takes just a few simple steps.</span></span> <span data-ttu-id="d6212-148">Aby uzyskać więcej informacji, zobacz [redagowanie krojów z analizy multimediów Azure](media-services-face-redaction.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="d6212-148">For more information, see the [Redact faces with Azure Media Analytics](media-services-face-redaction.md) article.</span></span>

## <a name="common-scenarios"></a><span data-ttu-id="d6212-149">Typowe scenariusze</span><span class="sxs-lookup"><span data-stu-id="d6212-149">Common scenarios</span></span>
<span data-ttu-id="d6212-150">Analiza multimediów może ułatwić organizacjom i przedsiębiorstwom zgromadzonych nowych danych z wideo i więcej efektywnie zarządzać dużych ilości zawartości wideo.</span><span class="sxs-lookup"><span data-stu-id="d6212-150">Media Analytics can help organizations and enterprises glean new insights from video and more effectively manage large volumes of video content.</span></span> <span data-ttu-id="d6212-151">Poniżej przedstawiono kilka scenariuszy:</span><span class="sxs-lookup"><span data-stu-id="d6212-151">Here are several scenarios:</span></span>

* <span data-ttu-id="d6212-152">**Wywołaj centrów**.</span><span class="sxs-lookup"><span data-stu-id="d6212-152">**Call centers**.</span></span> <span data-ttu-id="d6212-153">Nawet w przypadku pojawienie się mediów społecznościowych odbiorcy biura obsługi ułatwienia nadal znaczną część transakcji obsługi klienta.</span><span class="sxs-lookup"><span data-stu-id="d6212-153">Even with the advent of social media, customer call centers still facilitate a large percentage of customer-service transactions.</span></span> <span data-ttu-id="d6212-154">Zakodowane w tych danych audio jest duża ilość informacji klienta, który można przeprowadzić analizę w celu osiągnięcia wyższej zadowolenia klienta.</span><span class="sxs-lookup"><span data-stu-id="d6212-154">Encoded in this audio data is a large amount of customer information that can be analyzed to achieve higher customer satisfaction.</span></span> <span data-ttu-id="d6212-155">Przy użyciu nośnika indeksatora, organizacje można wyodrębnić tekst i twórz indeksów wyszukiwania i pulpity nawigacyjne.</span><span class="sxs-lookup"><span data-stu-id="d6212-155">By using Media Indexer, organizations can extract text and build search indexes and dashboards.</span></span> <span data-ttu-id="d6212-156">Następnie mogli wyodrębnić informacji dotyczących typowych utrudnień, źródeł utrudnień i inne odpowiednie dane.</span><span class="sxs-lookup"><span data-stu-id="d6212-156">Then they can extract intelligence around common complaints, sources of complaints, and other relevant data.</span></span>
* <span data-ttu-id="d6212-157">**Łagodzenie zawartość wygenerowaną przez użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="d6212-157">**User-generated content moderation**.</span></span> <span data-ttu-id="d6212-158">Z nośnika wiadomości gniazda do działów polecenie w wielu organizacjach istnieją portale publicznych, które akceptują wygenerowaną przez użytkowników nośniki, takie jak pliki wideo i obrazów.</span><span class="sxs-lookup"><span data-stu-id="d6212-158">From news media outlets to police departments, many organizations have public-facing portals that accept user-generated media such as videos and images.</span></span> <span data-ttu-id="d6212-159">Wielkość zawartości można zwiększyć z powodu nieoczekiwanego zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="d6212-159">The volume of content can spike due to unexpected events.</span></span> <span data-ttu-id="d6212-160">W tych scenariuszach jest trudne do przeprowadzenia skuteczne recenzje ręczne zawartości dla właściwości.</span><span class="sxs-lookup"><span data-stu-id="d6212-160">In these scenarios, it is difficult to conduct effective manual reviews of content for appropriateness.</span></span> <span data-ttu-id="d6212-161">Klienci mogą polegać na usługę łagodzenia zawartości, aby skupić się na zawartość, która jest odpowiednia.</span><span class="sxs-lookup"><span data-stu-id="d6212-161">Customers can rely on the content-moderation service to focus on content that is appropriate.</span></span>
* <span data-ttu-id="d6212-162">**Nadzoru**.</span><span class="sxs-lookup"><span data-stu-id="d6212-162">**Surveillance**.</span></span> <span data-ttu-id="d6212-163">Wzrost używany kamer IP pochodzą rosnącym spisu nadzoru wideo.</span><span class="sxs-lookup"><span data-stu-id="d6212-163">With the growth in use of IP cameras comes a growing inventory of surveillance video.</span></span> <span data-ttu-id="d6212-164">Ręcznie recenzowania nadzoru wideo jest czas znacznym i podatne na błędy człowieka.</span><span class="sxs-lookup"><span data-stu-id="d6212-164">Manually reviewing surveillance video is time intensive and prone to human error.</span></span> <span data-ttu-id="d6212-165">Analiza multimediów udostępnia usługi, takie jak wykrywanie ruchu, wykrywania twarzy na obrazie i przyspieszonych ujęć poklatkowych w celu uproszczenia procesu przeglądu, zarządzania i tworzenie pochodnych łatwiejsze.</span><span class="sxs-lookup"><span data-stu-id="d6212-165">Media Analytics provides services such as motion detection, face detection, and Hyperlapse to make the process of reviewing, managing, and creating derivatives easier.</span></span>

## <a name="media-analytics-media-processors"></a><span data-ttu-id="d6212-166">Procesory multimediów usługi analiza multimediów</span><span class="sxs-lookup"><span data-stu-id="d6212-166">Media Analytics media processors</span></span>
<span data-ttu-id="d6212-167">W tej sekcji wymieniono procesory multimediów usługi analiza multimediów i przedstawia sposób użycia platformy .NET lub REST można pobrać obiektu procesora (MP) nośnika.</span><span class="sxs-lookup"><span data-stu-id="d6212-167">This section lists the Media Analytics media processors and shows how to use .NET or REST to get a media processor (MP) object.</span></span>

### <a name="mp-names"></a><span data-ttu-id="d6212-168">Nazwy pakietu administracyjnego</span><span class="sxs-lookup"><span data-stu-id="d6212-168">MP names</span></span>
* <span data-ttu-id="d6212-169">Podgląd indeksatora 2 multimediów Azure</span><span class="sxs-lookup"><span data-stu-id="d6212-169">Azure Media Indexer 2 Preview</span></span>
* <span data-ttu-id="d6212-170">Azure Media Indexer</span><span class="sxs-lookup"><span data-stu-id="d6212-170">Azure Media Indexer</span></span>
* <span data-ttu-id="d6212-171">Azure Media Hyperlapse</span><span class="sxs-lookup"><span data-stu-id="d6212-171">Azure Media Hyperlapse</span></span>
* <span data-ttu-id="d6212-172">Azure Media Face Detector</span><span class="sxs-lookup"><span data-stu-id="d6212-172">Azure Media Face Detector</span></span>
* <span data-ttu-id="d6212-173">Azure Media Motion Detector</span><span class="sxs-lookup"><span data-stu-id="d6212-173">Azure Media Motion Detector</span></span>
* <span data-ttu-id="d6212-174">Azure Media Video Thumbnails</span><span class="sxs-lookup"><span data-stu-id="d6212-174">Azure Media Video Thumbnails</span></span>
* <span data-ttu-id="d6212-175">Azure Media OCR</span><span class="sxs-lookup"><span data-stu-id="d6212-175">Azure Media OCR</span></span>

### <a name="net"></a><span data-ttu-id="d6212-176">.NET</span><span class="sxs-lookup"><span data-stu-id="d6212-176">.NET</span></span>
<span data-ttu-id="d6212-177">Następująca funkcja przyjmuje jeden z określonych nazw pakietu administracyjnego i zwraca obiekt pakietu administracyjnego.</span><span class="sxs-lookup"><span data-stu-id="d6212-177">The following function takes one of the specified MP names and returns an MP object.</span></span>

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


### <a name="rest"></a><span data-ttu-id="d6212-178">REST</span><span class="sxs-lookup"><span data-stu-id="d6212-178">REST</span></span>
<span data-ttu-id="d6212-179">Żądanie:</span><span class="sxs-lookup"><span data-stu-id="d6212-179">Request:</span></span>

    GET https://media.windows.net/api/MediaProcessors()?$filter=Name%20eq%20'Azure%20Media%20OCR' HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer <token>
    x-ms-version: 2.12
    Host: media.windows.net

<span data-ttu-id="d6212-180">Odpowiedź:</span><span class="sxs-lookup"><span data-stu-id="d6212-180">Response:</span></span>

    . . .

    {  
       "odata.metadata":"https://media.windows.net/api/$metadata#MediaProcessors",
       "value":[  
          {  
             "Id":"nb:mpid:UUID:074c3899-d9fb-448f-9ae1-4ebcbe633056",
             "Description":"Azure Media OCR",
             "Name":"Azure Media OCR",
             "Sku":"",
             "Vendor":"Microsoft",
             "Version":"1.1"
          }
       ]
    }

## <a name="demos"></a><span data-ttu-id="d6212-181">Pokazy</span><span class="sxs-lookup"><span data-stu-id="d6212-181">Demos</span></span>
<span data-ttu-id="d6212-182">Zobacz [pokazy analizy multimediów Azure](http://azuremedialabs.azurewebsites.net/demos/Analytics.html).</span><span class="sxs-lookup"><span data-stu-id="d6212-182">See [Azure Media Analytics demos](http://azuremedialabs.azurewebsites.net/demos/Analytics.html).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d6212-183">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d6212-183">Next steps</span></span>
<span data-ttu-id="d6212-184">Przejrzyj ścieżki szkoleniowe dotyczące usługi Media Services.</span><span class="sxs-lookup"><span data-stu-id="d6212-184">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="d6212-185">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="d6212-185">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-articles"></a><span data-ttu-id="d6212-186">Pokrewne artykuły:</span><span class="sxs-lookup"><span data-stu-id="d6212-186">Related articles</span></span>
<span data-ttu-id="d6212-187">Zobacz [anonsu analiza usługi multimediów](https://azure.microsoft.com/blog/introducing-azure-media-analytics/).</span><span class="sxs-lookup"><span data-stu-id="d6212-187">See [Media Services Analytics announcement](https://azure.microsoft.com/blog/introducing-azure-media-analytics/).</span></span>

<!-- Images -->

[overview]: ./media/media-services-video-on-demand-workflow/media-services-video-on-demand.png
