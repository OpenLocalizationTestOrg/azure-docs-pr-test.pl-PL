---
title: "aaaAnalyze przy użyciu nośnika hello portalu Azure | Dokumentacja firmy Microsoft"
description: "W tym temacie omówiono sposób tooprocess multimediów procesory multimediów usługi analiza multimediów (MP) przy użyciu hello portalu Azure."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 18213fc1-74f5-4074-a32b-02846fe90601
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: juliako
ms.openlocfilehash: d549c0315cd58c3771420379316b4f2ad3c2cea6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-your-media-using-hello-azure-portal"></a><span data-ttu-id="c6ede-103">Analiza multimediów przy użyciu hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="c6ede-103">Analyze your media using hello Azure portal</span></span>
> [!NOTE]
> <span data-ttu-id="c6ede-104">toocomplete tego samouczka jest potrzebne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c6ede-104">toocomplete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="c6ede-105">Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c6ede-105">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
> 
> 

## <a name="overview"></a><span data-ttu-id="c6ede-106">Omówienie</span><span class="sxs-lookup"><span data-stu-id="c6ede-106">Overview</span></span>
<span data-ttu-id="c6ede-107">Azure Media Services Analytics to kolekcja składników mowy i obrazu (w skali przedsiębiorstwa, zgodności i zabezpieczeń globalne), które ułatwiają przydatnych wyników analiz tooderive organizacjom i przedsiębiorstwom podstawie posiadanych plików wideo.</span><span class="sxs-lookup"><span data-stu-id="c6ede-107">Azure Media Services Analytics is a collection of speech and vision components (at enterprise scale, compliance, security and global reach) that make it easier for organizations and enterprises tooderive actionable insights from their video files.</span></span> <span data-ttu-id="c6ede-108">Aby uzyskać bardziej szczegółowe omówienie usługi Azure Media Services Analytics zobacz [to](media-services-analytics-overview.md) tematu.</span><span class="sxs-lookup"><span data-stu-id="c6ede-108">For more detailed overview of Azure Media Services Analytics see [this](media-services-analytics-overview.md) topic.</span></span> 

<span data-ttu-id="c6ede-109">W tym temacie omówiono sposób tooprocess multimediów procesory multimediów usługi analiza multimediów (MP) przy użyciu hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="c6ede-109">This topic discusses how tooprocess your media with Media Analytics media processors (MPs) using hello Azure portal.</span></span> <span data-ttu-id="c6ede-110">Pakiety MP analizy multimediów tworzą pliki MP4 lub pliki w formacie JSON.</span><span class="sxs-lookup"><span data-stu-id="c6ede-110">Media Analytics MPs produce MP4 files or JSON files.</span></span> <span data-ttu-id="c6ede-111">Plik MP4 utworzony przez procesor multimediów można pobrać progresywnie hello pliku.</span><span class="sxs-lookup"><span data-stu-id="c6ede-111">If a media processor produced an MP4 file, you can progressively download hello file.</span></span> <span data-ttu-id="c6ede-112">Plik JSON utworzony przez procesor multimediów można pobrać pliku hello z hello magazynu obiektów blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c6ede-112">If a media processor produced a JSON file, you can download hello file from hello Azure blob storage.</span></span> 

## <a name="choose-an-asset-that-you-want-tooanalyze"></a><span data-ttu-id="c6ede-113">Wybierz zasób, które mają tooanalyze</span><span class="sxs-lookup"><span data-stu-id="c6ede-113">Choose an asset that you want tooanalyze</span></span>
1. <span data-ttu-id="c6ede-114">W hello [portalu Azure](https://portal.azure.com/), wybierz konto usługi Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="c6ede-114">In hello [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="c6ede-115">W hello **ustawienia** wybierz **zasoby**.</span><span class="sxs-lookup"><span data-stu-id="c6ede-115">In hello **Settings** window, select **Assets**.</span></span>  
   <span data-ttu-id="c6ede-116">.</span><span class="sxs-lookup"><span data-stu-id="c6ede-116">.</span></span>
    <span data-ttu-id="c6ede-117">![Analizowanie plików wideo](./media/media-services-portal-analyze/media-services-portal-analyze001.png)</span><span class="sxs-lookup"><span data-stu-id="c6ede-117">![Analyze videos](./media/media-services-portal-analyze/media-services-portal-analyze001.png)</span></span>
3. <span data-ttu-id="c6ede-118">Wybierz hello zawartości, który chcesz hello tooanalyze i naciśnij klawisz **Analizuj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="c6ede-118">Select hello asset that you would like tooanalyze and press hello **Analyze** button.</span></span>
   
    ![Analizowanie plików wideo](./media/media-services-portal-analyze/media-services-portal-analyze002.png)
4. <span data-ttu-id="c6ede-120">W hello **procesu multimedialnej z analizy multimediów** okna, wybierz hello procesora.</span><span class="sxs-lookup"><span data-stu-id="c6ede-120">In hello **Process media asset with  Media Analytics** window, select hello processor.</span></span> 
   
    <span data-ttu-id="c6ede-121">rest Hello artykułu hello wyjaśnia, dlaczego i w jaki sposób toouse każdego procesora.</span><span class="sxs-lookup"><span data-stu-id="c6ede-121">hello rest of hello article explains why and how toouse each processor.</span></span> 
5. <span data-ttu-id="c6ede-122">Naciśnij klawisz **Utwórz** toohello uruchomić zadanie.</span><span class="sxs-lookup"><span data-stu-id="c6ede-122">Press **Create** toohello start a job.</span></span>

## <a name="azure-media-indexer"></a><span data-ttu-id="c6ede-123">Azure Media Indexer</span><span class="sxs-lookup"><span data-stu-id="c6ede-123">Azure Media Indexer</span></span>
<span data-ttu-id="c6ede-124">Witaj **Azure Media indeksatora** procesor multimediów umożliwia toomake plików multimedialnych i zawartości można wyszukiwać, również generowanie zamkniętego śledzi podpisów.</span><span class="sxs-lookup"><span data-stu-id="c6ede-124">hello **Azure Media Indexer** media processor enables you toomake media files and content searchable, as well as generate closed captioning tracks.</span></span> <span data-ttu-id="c6ede-125">Tej sekcji szczegółowo opisano niektóre opcje, które można określić dla tego pakietu administracyjnego.</span><span class="sxs-lookup"><span data-stu-id="c6ede-125">This sections gives some details about options that you can specify for this MP.</span></span>

![Analizowanie plików wideo](./media/media-services-portal-analyze/media-services-portal-analyze003.png)

### <a name="language"></a><span data-ttu-id="c6ede-127">Język</span><span class="sxs-lookup"><span data-stu-id="c6ede-127">Language</span></span>
<span data-ttu-id="c6ede-128">Witaj w pliku multimedialnym hello toobe języka naturalnego.</span><span class="sxs-lookup"><span data-stu-id="c6ede-128">hello natural language toobe recognized in hello multimedia file.</span></span> <span data-ttu-id="c6ede-129">Na przykład w języku angielskim i hiszpańskim.</span><span class="sxs-lookup"><span data-stu-id="c6ede-129">For example, English or Spanish.</span></span> 

### <a name="captions"></a><span data-ttu-id="c6ede-130">Podpisy</span><span class="sxs-lookup"><span data-stu-id="c6ede-130">Captions</span></span>
<span data-ttu-id="c6ede-131">Można wybrać formatu podpisu, który zostanie wygenerowane z zawartości.</span><span class="sxs-lookup"><span data-stu-id="c6ede-131">You can choose a caption format that will be generated from your content.</span></span> <span data-ttu-id="c6ede-132">Zadania indeksowania mogą generować pliki napisów w hello następujących formatów:</span><span class="sxs-lookup"><span data-stu-id="c6ede-132">An indexing job can generate closed caption files in hello following formats:</span></span>  

* <span data-ttu-id="c6ede-133">**SAMI**</span><span class="sxs-lookup"><span data-stu-id="c6ede-133">**SAMI**</span></span>
* <span data-ttu-id="c6ede-134">**TTML**</span><span class="sxs-lookup"><span data-stu-id="c6ede-134">**TTML**</span></span>
* <span data-ttu-id="c6ede-135">**WebVTT**</span><span class="sxs-lookup"><span data-stu-id="c6ede-135">**WebVTT**</span></span>

<span data-ttu-id="c6ede-136">Zamkniętych plikach podpis (DW) w tych formatach może być używane toomake audio i wideo pliki dostępny toopeople niepełnosprawne przesłuchanie.</span><span class="sxs-lookup"><span data-stu-id="c6ede-136">Closed Caption (CC) files in these formats can be used toomake audio and video files accessible toopeople with hearing disability.</span></span>

### <a name="aib-file"></a><span data-ttu-id="c6ede-137">Plik AIB</span><span class="sxs-lookup"><span data-stu-id="c6ede-137">AIB file</span></span>
<span data-ttu-id="c6ede-138">Wybierz tę opcję, jeśli takie jak pliku Blob indeksu Audio hello toogenerate do użytku z będzie można hello niestandardowych IFilter serwera SQL.</span><span class="sxs-lookup"><span data-stu-id="c6ede-138">Select this option if you would like toogenerate hello Audio Index Blob file for use with hello custom SQL Server IFilter.</span></span> <span data-ttu-id="c6ede-139">Aby uzyskać więcej informacji, zobacz [to](https://azure.microsoft.com/blog/using-aib-files-with-azure-media-indexer-and-sql-server/) blogu.</span><span class="sxs-lookup"><span data-stu-id="c6ede-139">For more information, see [this](https://azure.microsoft.com/blog/using-aib-files-with-azure-media-indexer-and-sql-server/) blog.</span></span>

### <a name="keywords"></a><span data-ttu-id="c6ede-140">Słowa kluczowe</span><span class="sxs-lookup"><span data-stu-id="c6ede-140">Keywords</span></span>
<span data-ttu-id="c6ede-141">Wybierz tę opcję, jeśli chcesz toogenerate pliku XML słów kluczowych.</span><span class="sxs-lookup"><span data-stu-id="c6ede-141">Select this option if you would like toogenerate a keywords XML file.</span></span> <span data-ttu-id="c6ede-142">Ten plik zawiera słowa kluczowe wyodrębnione z zawartości mowy hello, częstotliwości i przesunięcia informacje.</span><span class="sxs-lookup"><span data-stu-id="c6ede-142">This file contains keywords extracted from hello speech content, with frequency and offset information.</span></span>

### <a name="job-name"></a><span data-ttu-id="c6ede-143">Nazwa zadania</span><span class="sxs-lookup"><span data-stu-id="c6ede-143">Job name</span></span>
<span data-ttu-id="c6ede-144">Przyjazna nazwa umożliwia identyfikowanie hello zadania.</span><span class="sxs-lookup"><span data-stu-id="c6ede-144">A friendly name that lets you identify hello job.</span></span> <span data-ttu-id="c6ede-145">[To](media-services-portal-check-job-progress.md) artykule opisano, jak można monitorować postęp hello zadania.</span><span class="sxs-lookup"><span data-stu-id="c6ede-145">[This](media-services-portal-check-job-progress.md) article describes how you can monitor hello progress of a job.</span></span> 

### <a name="output-file"></a><span data-ttu-id="c6ede-146">Plik wyjściowy</span><span class="sxs-lookup"><span data-stu-id="c6ede-146">Output file</span></span>
<span data-ttu-id="c6ede-147">Przyjazna nazwa umożliwia zidentyfikowanie hello zawartości danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="c6ede-147">A friendly name that lets you identify hello output content.</span></span> 

## <a name="azure-media-hyperlapse"></a><span data-ttu-id="c6ede-148">Azure Media Hyperlapse</span><span class="sxs-lookup"><span data-stu-id="c6ede-148">Azure Media Hyperlapse</span></span>
<span data-ttu-id="c6ede-149">Azure Media Hyperlapse jest MP tworzącą smooth czas, jaki upłynął wideo z pierwszą osobą lub akcji aparatu zawartości.</span><span class="sxs-lookup"><span data-stu-id="c6ede-149">Azure Media Hyperlapse is an MP that creates smooth time-lapsed videos from first-person or action-camera content.</span></span>  <span data-ttu-id="c6ede-150">Aby uzyskać więcej informacji, zobacz [ten](media-services-hyperlapse-content.md) temat.</span><span class="sxs-lookup"><span data-stu-id="c6ede-150">For more information, see [this](media-services-hyperlapse-content.md) topic.</span></span> <span data-ttu-id="c6ede-151">Tej sekcji szczegółowo opisano niektóre opcje, które można określić dla tego pakietu administracyjnego.</span><span class="sxs-lookup"><span data-stu-id="c6ede-151">This sections gives some details about options that you can specify for this MP.</span></span>

![Analizowanie plików wideo](./media/media-services-portal-analyze/media-services-portal-analyze004.png)

### <a name="speed"></a><span data-ttu-id="c6ede-153">Szybkość</span><span class="sxs-lookup"><span data-stu-id="c6ede-153">Speed</span></span>
<span data-ttu-id="c6ede-154">Określ szybkość hello z których toospeed się hello wejściowy plik wideo.</span><span class="sxs-lookup"><span data-stu-id="c6ede-154">Specify hello speed with which toospeed up hello input video.</span></span> <span data-ttu-id="c6ede-155">dane wyjściowe Hello jest stabilnych i czas, jaki upłynął dobór hello wejściowy plik wideo.</span><span class="sxs-lookup"><span data-stu-id="c6ede-155">hello output is a stabilized and time-lapsed rendition of hello input video.</span></span>

### <a name="job-name"></a><span data-ttu-id="c6ede-156">Nazwa zadania</span><span class="sxs-lookup"><span data-stu-id="c6ede-156">Job name</span></span>
<span data-ttu-id="c6ede-157">Przyjazna nazwa umożliwia identyfikowanie hello zadania.</span><span class="sxs-lookup"><span data-stu-id="c6ede-157">A friendly name that lets you identify hello job.</span></span> <span data-ttu-id="c6ede-158">[To](media-services-portal-check-job-progress.md) artykule opisano, jak można monitorować postęp hello zadania.</span><span class="sxs-lookup"><span data-stu-id="c6ede-158">[This](media-services-portal-check-job-progress.md) article describes how you can monitor hello progress of a job.</span></span> 

### <a name="output-file"></a><span data-ttu-id="c6ede-159">Plik wyjściowy</span><span class="sxs-lookup"><span data-stu-id="c6ede-159">Output file</span></span>
<span data-ttu-id="c6ede-160">Przyjazna nazwa umożliwia zidentyfikowanie hello zawartości danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="c6ede-160">A friendly name that lets you identify hello output content.</span></span> 

## <a name="azure-media-face-detector"></a><span data-ttu-id="c6ede-161">Azure Media Face Detector</span><span class="sxs-lookup"><span data-stu-id="c6ede-161">Azure Media Face Detector</span></span>
<span data-ttu-id="c6ede-162">Witaj **Azure Media krój detektora** procesor multimediów (MP) pozwala toocount, przeniesień Śledź i nawet miernika odbiorców udziału i reakcji za pośrednictwem twarzy.</span><span class="sxs-lookup"><span data-stu-id="c6ede-162">hello **Azure Media Face Detector** media processor (MP) enables you toocount, track movements, and even gauge audience participation and reaction via facial expressions.</span></span> <span data-ttu-id="c6ede-163">Ta usługa zawiera dwie funkcje:</span><span class="sxs-lookup"><span data-stu-id="c6ede-163">This service contains two features:</span></span> 

* <span data-ttu-id="c6ede-164">**Wykrywanie twarzy na obrazie**</span><span class="sxs-lookup"><span data-stu-id="c6ede-164">**Face detection**</span></span>
  
    <span data-ttu-id="c6ede-165">Wykrywanie twarzy na obrazie znajduje i śledzi człowieka kroje w pliku wideo.</span><span class="sxs-lookup"><span data-stu-id="c6ede-165">Face detection finds and tracks human faces within a video.</span></span> <span data-ttu-id="c6ede-166">Wiele powierzchni mogą być wykrywane i następnie śledzenia przechodzą wokół, hello czas i lokalizację metadane zwrócony w pliku JSON.</span><span class="sxs-lookup"><span data-stu-id="c6ede-166">Multiple faces can be detected and subsequently be tracked as they move around, with hello time and location metadata returned in a JSON file.</span></span> <span data-ttu-id="c6ede-167">Podczas śledzenia podejmie toogive spójne toohello identyfikator sam stają przed podczas osoby hello jest przenoszenia na ekranie, nawet jeśli są zablokowane lub pozostaw krótko hello ramki.</span><span class="sxs-lookup"><span data-stu-id="c6ede-167">During tracking, it will attempt toogive a consistent ID toohello same face while hello person is moving around on screen, even if they are obstructed or briefly leave hello frame.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="c6ede-168">Tej usługi nie przeprowadza rozpoznawanie twarzy.</span><span class="sxs-lookup"><span data-stu-id="c6ede-168">This services does not perform facial recognition.</span></span> <span data-ttu-id="c6ede-169">Osoba, która pozostawia ramki hello lub staje się blokować dla zbyt długo będzie mógł skorzystać z nowym Identyfikatorem gdy zwracają.</span><span class="sxs-lookup"><span data-stu-id="c6ede-169">An individual who leaves hello frame or becomes obstructed for too long will be given a new ID when they return.</span></span>
  > 
  > 
* <span data-ttu-id="c6ede-170">**Wykrywanie emocji**</span><span class="sxs-lookup"><span data-stu-id="c6ede-170">**Emotion detection**</span></span>
  
    <span data-ttu-id="c6ede-171">Wykrywanie emocji jest opcjonalnym składnikiem hello procesor multimediów wykrywania twarzy na obrazie, które zwraca analizy na wiele atrybutów emocjonalne kroje hello wykryte, w tym szczęście, sadness, obawy i gniew.</span><span class="sxs-lookup"><span data-stu-id="c6ede-171">Emotion Detection is an optional component of hello Face Detection Media Processor that returns analysis on multiple emotional attributes from hello faces detected, including happiness, sadness, fear, anger, and more.</span></span> 

![Analizowanie plików wideo](./media/media-services-portal-analyze/media-services-portal-analyze005.png)

### <a name="detection-mode"></a><span data-ttu-id="c6ede-173">Tryb wykrywania</span><span class="sxs-lookup"><span data-stu-id="c6ede-173">Detection mode</span></span>
<span data-ttu-id="c6ede-174">Jeden z następujących trybów hello można przez procesor hello:</span><span class="sxs-lookup"><span data-stu-id="c6ede-174">One of hello following modes can be used by hello processor:</span></span>

* <span data-ttu-id="c6ede-175">wykrywanie twarzy na obrazie</span><span class="sxs-lookup"><span data-stu-id="c6ede-175">face detection</span></span>
* <span data-ttu-id="c6ede-176">na powierzchni emocji wykrywania</span><span class="sxs-lookup"><span data-stu-id="c6ede-176">per face emotion detection</span></span>
* <span data-ttu-id="c6ede-177">wykrywanie emocji agregacji</span><span class="sxs-lookup"><span data-stu-id="c6ede-177">aggregate emotion detection</span></span>

### <a name="job-name"></a><span data-ttu-id="c6ede-178">Nazwa zadania</span><span class="sxs-lookup"><span data-stu-id="c6ede-178">Job name</span></span>
<span data-ttu-id="c6ede-179">Przyjazna nazwa umożliwia identyfikowanie hello zadania.</span><span class="sxs-lookup"><span data-stu-id="c6ede-179">A friendly name that lets you identify hello job.</span></span> <span data-ttu-id="c6ede-180">[To](media-services-portal-check-job-progress.md) artykule opisano, jak można monitorować postęp hello zadania.</span><span class="sxs-lookup"><span data-stu-id="c6ede-180">[This](media-services-portal-check-job-progress.md) article describes how you can monitor hello progress of a job.</span></span> 

### <a name="output-file"></a><span data-ttu-id="c6ede-181">Plik wyjściowy</span><span class="sxs-lookup"><span data-stu-id="c6ede-181">Output file</span></span>
<span data-ttu-id="c6ede-182">Przyjazna nazwa umożliwia zidentyfikowanie hello zawartości danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="c6ede-182">A friendly name that lets you identify hello output content.</span></span> 

## <a name="azure-media-motion-detector"></a><span data-ttu-id="c6ede-183">Azure Media Motion Detector</span><span class="sxs-lookup"><span data-stu-id="c6ede-183">Azure Media Motion Detector</span></span>
<span data-ttu-id="c6ede-184">Witaj **czujnik ruchu Azure Media** nośnika procesora (MP) umożliwia tooefficiently można zidentyfikować sekcje zawierają informacje przydatne w wideo w innym przypadku długich i procesu.</span><span class="sxs-lookup"><span data-stu-id="c6ede-184">hello **Azure Media Motion Detector** media processor (MP) enables you tooefficiently identify sections of interest within an otherwise long and uneventful video.</span></span> <span data-ttu-id="c6ede-185">Wykrywanie ruchu może służyć na statycznych aparatu materiał tooidentify sekcje wideo hello gdzie występuje ruchu.</span><span class="sxs-lookup"><span data-stu-id="c6ede-185">Motion detection can be used on static camera footage tooidentify sections of hello video where motion occurs.</span></span> <span data-ttu-id="c6ede-186">Generuje plik JSON zawierający metadane z sygnatury czasowe i hello ograniczenia regionu, w którym wystąpiło zdarzenie hello.</span><span class="sxs-lookup"><span data-stu-id="c6ede-186">It generates a JSON file containing a metadata with timestamps and hello bounding region where hello event occurred.</span></span>

<span data-ttu-id="c6ede-187">Docelowe do źródła wideo zabezpieczeń, ta technologia jest możliwe toocategorize ruchu na odpowiednie zdarzenia i fałszywych alarmów, takie jak cieni i zmian oświetlenia.</span><span class="sxs-lookup"><span data-stu-id="c6ede-187">Targeted towards security video feeds, this technology is able toocategorize motion into relevant events and false positives such as shadows and lighting changes.</span></span> <span data-ttu-id="c6ede-188">Dzięki temu można toogenerate alertów zabezpieczeń z aparatu fotograficznego źródła danych bez otrzymywania wiadomości-śmieci nieskończone zdarzenia nie ma znaczenia, będąc chwil stanie tooextract płynących z bardzo długi nadzoru wideo.</span><span class="sxs-lookup"><span data-stu-id="c6ede-188">This allows you toogenerate security alerts from camera feeds without being spammed with endless irrelevant events, while being able tooextract moments of interest from extremely long surveillance videos.</span></span>

![Analizowanie plików wideo](./media/media-services-portal-analyze/media-services-portal-analyze006.png)

## <a name="azure-media-video-thumbnails"></a><span data-ttu-id="c6ede-190">Azure Media Video Thumbnails</span><span class="sxs-lookup"><span data-stu-id="c6ede-190">Azure Media Video Thumbnails</span></span>
<span data-ttu-id="c6ede-191">Tego procesora mogą pomóc tworzyć podsumowania długich filmów wideo, wybierając automatycznie interesujące wstawki z hello źródła wideo.</span><span class="sxs-lookup"><span data-stu-id="c6ede-191">This processor can help you create summaries of long videos by automatically selecting interesting snippets from hello source video.</span></span> <span data-ttu-id="c6ede-192">Jest to przydatne, należy tooprovide szybki przegląd tooexpect które długie wideo.</span><span class="sxs-lookup"><span data-stu-id="c6ede-192">This is useful when you want tooprovide a quick overview of what tooexpect in a long video.</span></span> <span data-ttu-id="c6ede-193">Aby uzyskać szczegółowe informacje i przykłady, zobacz [tooCreate miniatur wideo multimediów Azure Użyj podsumowań wideo](media-services-video-summarization.md)</span><span class="sxs-lookup"><span data-stu-id="c6ede-193">For detailed information and examples, see [Use Azure Media Video Thumbnails tooCreate a Video Summarization](media-services-video-summarization.md)</span></span>

![Analizowanie plików wideo](./media/media-services-portal-analyze/media-services-portal-analyze008.png)

### <a name="job-name"></a><span data-ttu-id="c6ede-195">Nazwa zadania</span><span class="sxs-lookup"><span data-stu-id="c6ede-195">Job name</span></span>
<span data-ttu-id="c6ede-196">Przyjazna nazwa umożliwia identyfikowanie hello zadania.</span><span class="sxs-lookup"><span data-stu-id="c6ede-196">A friendly name that lets you identify hello job.</span></span> <span data-ttu-id="c6ede-197">[To](media-services-portal-check-job-progress.md) artykule opisano, jak można monitorować postęp hello zadania.</span><span class="sxs-lookup"><span data-stu-id="c6ede-197">[This](media-services-portal-check-job-progress.md) article describes how you can monitor hello progress of a job.</span></span> 

### <a name="output-file"></a><span data-ttu-id="c6ede-198">Plik wyjściowy</span><span class="sxs-lookup"><span data-stu-id="c6ede-198">Output file</span></span>
<span data-ttu-id="c6ede-199">Przyjazna nazwa umożliwia zidentyfikowanie hello zawartości danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="c6ede-199">A friendly name that lets you identify hello output content.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="c6ede-200">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c6ede-200">Next steps</span></span>
<span data-ttu-id="c6ede-201">Ścieżki szkoleniowe dotyczące usługi Media widoku.</span><span class="sxs-lookup"><span data-stu-id="c6ede-201">View Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="c6ede-202">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="c6ede-202">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

