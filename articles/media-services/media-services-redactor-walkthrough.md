---
title: "aaaRedact krojów z przewodnikiem analizy multimediów Azure | Dokumentacja firmy Microsoft"
description: "W tym temacie przedstawiono instrukcje krok po kroku na temat toorun redakcyjne pełnego przepływu pracy przy użyciu usługi Azure Media Services Explorer (AMSE) i Azure Media Redactor Visualizer (narzędzie typu open source)."
services: media-services
documentationcenter: 
author: Lichard
manager: cfowler
editor: 
ms.assetid: d6fa21b8-d80a-41b7-80c1-ff1761bc68f2
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 04/03/2017
ms.author: rli; juliako;
ms.openlocfilehash: ab28f4052b73fdb74fcd5766235eab35402a0c9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="redact-faces-with-azure-media-analytics-walkthrough"></a><span data-ttu-id="d53b4-103">Redagowanie krojów z przewodnikiem analizy multimediów Azure</span><span class="sxs-lookup"><span data-stu-id="d53b4-103">Redact faces with Azure Media Analytics walkthrough</span></span>

## <a name="overview"></a><span data-ttu-id="d53b4-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="d53b4-104">Overview</span></span>

<span data-ttu-id="d53b4-105">**Azure Media Redactor** jest [analizy multimediów Azure](media-services-analytics-overview.md) procesor multimediów (MP) oferuje skalowalne krój redakcyjne w chmurze hello.</span><span class="sxs-lookup"><span data-stu-id="d53b4-105">**Azure Media Redactor** is an [Azure Media Analytics](media-services-analytics-overview.md) media processor (MP) that offers scalable face redaction in hello cloud.</span></span> <span data-ttu-id="d53b4-106">Redakcyjne krój umożliwia możesz toomodify wideo w kolejności tooblur kroje wybrane osoby.</span><span class="sxs-lookup"><span data-stu-id="d53b4-106">Face redaction enables you toomodify your video in order tooblur faces of selected individuals.</span></span> <span data-ttu-id="d53b4-107">Możesz toouse hello krój redakcyjne usługi w publicznych scenariusze bezpieczeństwa i nośnika wiadomości.</span><span class="sxs-lookup"><span data-stu-id="d53b4-107">You may want toouse hello face redaction service in public safety and news media scenarios.</span></span> <span data-ttu-id="d53b4-108">Kilka minut najmniejszym zawiera wiele kroje może zająć godziny tooredact ręcznie, ale z tej usługi hello powierzchni procesu redakcyjne wymaga kilku prostych krokach.</span><span class="sxs-lookup"><span data-stu-id="d53b4-108">A few minutes of footage that contains multiple faces can take hours tooredact manually, but with this service hello face redaction process will require just a few simple steps.</span></span> <span data-ttu-id="d53b4-109">Aby uzyskać więcej informacji, zobacz [to](https://azure.microsoft.com/blog/azure-media-redactor/) blogu.</span><span class="sxs-lookup"><span data-stu-id="d53b4-109">For  more information, see [this](https://azure.microsoft.com/blog/azure-media-redactor/) blog.</span></span>

<span data-ttu-id="d53b4-110">Szczegółowe informacje o **Azure Media Redactor**, zobacz hello [omówienie redakcyjne krój](media-services-face-redaction.md) tematu.</span><span class="sxs-lookup"><span data-stu-id="d53b4-110">For details about  **Azure Media Redactor**, see hello [Face redaction overview](media-services-face-redaction.md) topic.</span></span>

<span data-ttu-id="d53b4-111">W tym temacie przedstawiono instrukcje krok po kroku na temat toorun redakcyjne pełnego przepływu pracy przy użyciu usługi Azure Media Services Explorer (AMSE) i Azure Media Redactor Visualizer (narzędzie typu open source).</span><span class="sxs-lookup"><span data-stu-id="d53b4-111">This topic shows step by step instructions on how toorun a full redaction workflow using Azure Media Services Explorer (AMSE) and Azure Media Redactor Visualizer (open source tool).</span></span>

<span data-ttu-id="d53b4-112">Witaj **Azure Media Redactor** pakiet administracyjny jest obecnie w przeglądzie.</span><span class="sxs-lookup"><span data-stu-id="d53b4-112">hello **Azure Media Redactor** MP is currently in Preview.</span></span> <span data-ttu-id="d53b4-113">Jest ona dostępna w wszystkich publicznych regiony platformy Azure, a także centrach danych instytucji rządowych Stanów Zjednoczonych i Chinach.</span><span class="sxs-lookup"><span data-stu-id="d53b4-113">It is available in all public Azure regions as well as US Government and China data centers.</span></span> <span data-ttu-id="d53b4-114">Ta wersja zapoznawcza jest obecnie bezpłatnie.</span><span class="sxs-lookup"><span data-stu-id="d53b4-114">This preview is currently free of charge.</span></span> <span data-ttu-id="d53b4-115">W bieżącej wersji hello istnieje limit 10 minut na przetworzonych długość wideo.</span><span class="sxs-lookup"><span data-stu-id="d53b4-115">In hello current release, there is a 10 minute limit on processed video length.</span></span>

<span data-ttu-id="d53b4-116">Aby uzyskać więcej informacji, zobacz [to](https://azure.microsoft.com/en-us/blog/redaction-preview-available-globally) blogu.</span><span class="sxs-lookup"><span data-stu-id="d53b4-116">For more information, see [this](https://azure.microsoft.com/en-us/blog/redaction-preview-available-globally) blog.</span></span>

## <a name="azure-media-services-explorer-workflow"></a><span data-ttu-id="d53b4-117">Azure Media Services Explorer przepływu pracy</span><span class="sxs-lookup"><span data-stu-id="d53b4-117">Azure Media Services Explorer workflow</span></span>

<span data-ttu-id="d53b4-118">Witaj najprostszym tooget sposób pracy z Redactor jest narzędzie AMSE toouse hello typu open source w witrynie github.</span><span class="sxs-lookup"><span data-stu-id="d53b4-118">hello easiest way tooget started with Redactor is toouse hello open source AMSE tool on github.</span></span> <span data-ttu-id="d53b4-119">Możesz uruchomić uproszczony przepływu pracy za pośrednictwem **łączyć** tryb, jeśli nie wymagają dostępu toohello adnotacji json lub hello krój obrazów jpg.</span><span class="sxs-lookup"><span data-stu-id="d53b4-119">You can run a simplified workflow via **combined** mode if you don’t need access toohello annotation json or hello face jpg images.</span></span>

### <a name="download-and-setup"></a><span data-ttu-id="d53b4-120">Pobierania i instalacji</span><span class="sxs-lookup"><span data-stu-id="d53b4-120">Download and setup</span></span>

1. <span data-ttu-id="d53b4-121">Pobierz narzędzie AMSE hello [tutaj](https://github.com/Azure/Azure-Media-Services-Explorer).</span><span class="sxs-lookup"><span data-stu-id="d53b4-121">Download hello AMSE tool from [here](https://github.com/Azure/Azure-Media-Services-Explorer).</span></span>
1. <span data-ttu-id="d53b4-122">Zaloguj się za tooyour konta usługi Media Services przy użyciu klucza usługi.</span><span class="sxs-lookup"><span data-stu-id="d53b4-122">Log in tooyour Media Services account using your service key.</span></span>

    <span data-ttu-id="d53b4-123">Witaj tooobtain nazwę konta i informacje o kluczu, przejdź toohello [portalu Azure](https://portal.azure.com/) i wybierz konto usługi AMS.</span><span class="sxs-lookup"><span data-stu-id="d53b4-123">tooobtain hello account name and key information, go toohello [Azure portal](https://portal.azure.com/) and select your AMS account.</span></span> <span data-ttu-id="d53b4-124">Wybierz ustawienia > klucze.</span><span class="sxs-lookup"><span data-stu-id="d53b4-124">Then, select Settings > Keys.</span></span> <span data-ttu-id="d53b4-125">Hello Zarządzaj kluczami w systemie windows zawiera nazwę konta hello i klucze podstawowe i pomocnicze hello jest wyświetlany.</span><span class="sxs-lookup"><span data-stu-id="d53b4-125">hello Manage keys windows shows hello account name and hello primary and secondary keys is displayed.</span></span> <span data-ttu-id="d53b4-126">Skopiuj wartości hello nazwę konta i klucz podstawowy hello.</span><span class="sxs-lookup"><span data-stu-id="d53b4-126">Copy values of hello account name and hello primary key.</span></span>

![Redakcja twarzy](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough001.png)

### <a name="first-pass--analyze-mode"></a><span data-ttu-id="d53b4-128">Najpierw przekazać — analizowanie tryb</span><span class="sxs-lookup"><span data-stu-id="d53b4-128">First pass – analyze mode</span></span>

1. <span data-ttu-id="d53b4-129">Przekazywanie pliku multimediów za pośrednictwem zasobów –> przekazywania, lub za pośrednictwem operacji przeciągania i upuszczania.</span><span class="sxs-lookup"><span data-stu-id="d53b4-129">Upload your media file through Asset –> Upload, or via drag and drop.</span></span> 
1. <span data-ttu-id="d53b4-130">Kliknij prawym przyciskiem myszy i przetwarzanie pliku nośnika, przy użyciu analizy multimediów Azure Media Redactor –> –> Tryb analizy.</span><span class="sxs-lookup"><span data-stu-id="d53b4-130">Right click and process your media file using Media Analytics –> Azure Media Redactor –> Analyze mode.</span></span> 


![Redakcja twarzy](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough002.png)

![Redakcja twarzy](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough003.png)

<span data-ttu-id="d53b4-133">dane wyjściowe Hello będzie zawierać plik json adnotacje z danych lokalizacji krój, a także jpg każdego wykrytego powierzchni.</span><span class="sxs-lookup"><span data-stu-id="d53b4-133">hello output will include an annotations json file with face location data, as well as a jpg of each detected face.</span></span> 

![Redakcja twarzy](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough004.png)

###<a name="second-pass--redact-mode"></a><span data-ttu-id="d53b4-135">Drugi przekazać — redagowanie tryb</span><span class="sxs-lookup"><span data-stu-id="d53b4-135">Second pass – redact mode</span></span>

1. <span data-ttu-id="d53b4-136">Przekaż oryginalnego toohello zawartości wideo dane wyjściowe z pierwszym przebiegu hello i Ustaw jako podstawowy zasobów.</span><span class="sxs-lookup"><span data-stu-id="d53b4-136">Upload your original video asset toohello output from hello first pass and set as a primary asset.</span></span> 

    ![Redakcja twarzy](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough005.png)

2. <span data-ttu-id="d53b4-138">(Opcjonalnie) Przekaż plik "Dance_idlist.txt", który zawiera listę hello identyfikatory mają tooredact rozdzielone znakami nowego wiersza.</span><span class="sxs-lookup"><span data-stu-id="d53b4-138">(Optional) Upload a 'Dance_idlist.txt' file which includes a newline delimited list of hello IDs you wish tooredact.</span></span> 

    ![Redakcja twarzy](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough006.png)

3. <span data-ttu-id="d53b4-140">(Opcjonalnie) Należy każdego edycji toohello annotations.json pliku, takich jak zwiększenie hello ograniczający granice pola.</span><span class="sxs-lookup"><span data-stu-id="d53b4-140">(Optional) Make any edits toohello annotations.json file such as increasing hello bounding box boundaries.</span></span> 
4. <span data-ttu-id="d53b4-141">Witaj zawartości wyjściowej z pierwszym przebiegu hello kliknij prawym przyciskiem myszy, wybierz hello Redactor i uruchom z hello **Redact** tryb.</span><span class="sxs-lookup"><span data-stu-id="d53b4-141">Right click hello output asset from hello first pass, select hello Redactor, and run with hello **Redact** mode.</span></span> 

    ![Redakcja twarzy](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough007.png)

5. <span data-ttu-id="d53b4-143">Pobieranie i udostępnianie zasobów ostateczne dane wyjściowe zredagowanym hello.</span><span class="sxs-lookup"><span data-stu-id="d53b4-143">Download or share hello final redacted output asset.</span></span> 

    ![Redakcja twarzy](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough008.png)

##<a name="azure-media-redactor-visualizer-open-source-tool"></a><span data-ttu-id="d53b4-145">Azure Media Redactor wizualizatora typu open source narzędzia</span><span class="sxs-lookup"><span data-stu-id="d53b4-145">Azure Media Redactor Visualizer open source tool</span></span>

<span data-ttu-id="d53b4-146">Typu open source [narzędzie wizualizatora](https://github.com/Microsoft/azure-media-redactor-visualizer) jest uruchamiana z formatem adnotacje hello z analizy i przy użyciu danych wyjściowych hello deweloperzy toohelp zaprojektowane.</span><span class="sxs-lookup"><span data-stu-id="d53b4-146">An open source [visualizer tool](https://github.com/Microsoft/azure-media-redactor-visualizer) is designed toohelp developers just starting with hello annotations format with parsing and using hello output.</span></span>

<span data-ttu-id="d53b4-147">Po sklonować repozytorium hello, w projekcie hello toorun kolejności, konieczne będzie toodownload FFMPEG z ich [oficjalna witryna](https://ffmpeg.org/download.html).</span><span class="sxs-lookup"><span data-stu-id="d53b4-147">After you clone hello repo, in order toorun hello project, you will need toodownload FFMPEG from their [official site](https://ffmpeg.org/download.html).</span></span>

<span data-ttu-id="d53b4-148">Jeśli jesteś deweloperem hello tooparse JSON adnotacji danych w trakcie, poszukaj wewnątrz Models.MetaData przykłady kodu przykładowej.</span><span class="sxs-lookup"><span data-stu-id="d53b4-148">If you are a developer trying tooparse hello JSON annotation data, look inside Models.MetaData for sample code examples.</span></span>

### <a name="set-up-hello-tool"></a><span data-ttu-id="d53b4-149">Konfigurowanie narzędzia hello</span><span class="sxs-lookup"><span data-stu-id="d53b4-149">Set up hello tool</span></span>

1.  <span data-ttu-id="d53b4-150">Pobieranie i tworzenie hello całego rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="d53b4-150">Download and build hello entire solution.</span></span> 

    ![Redakcja twarzy](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough009.png)

2.  <span data-ttu-id="d53b4-152">Pobierz FFMPEG z [tutaj](https://ffmpeg.org/download.html).</span><span class="sxs-lookup"><span data-stu-id="d53b4-152">Download FFMPEG from [here](https://ffmpeg.org/download.html).</span></span> <span data-ttu-id="d53b4-153">Ten projekt pierwotnie został opracowany z wersji be1d324 (2016-10-04) z statycznego łączenia.</span><span class="sxs-lookup"><span data-stu-id="d53b4-153">This project was originally developed with version be1d324 (2016-10-04) with static linking.</span></span> 
3.  <span data-ttu-id="d53b4-154">Skopiuj toohello ffmpeg.exe i ffprobe.exe tego samego folderu wyjściowego jako AzureMediaRedactor.exe.</span><span class="sxs-lookup"><span data-stu-id="d53b4-154">Copy ffmpeg.exe and ffprobe.exe toohello same output folder as AzureMediaRedactor.exe.</span></span> 

    ![Redakcja twarzy](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough010.png)

4. <span data-ttu-id="d53b4-156">Uruchom AzureMediaRedactor.exe.</span><span class="sxs-lookup"><span data-stu-id="d53b4-156">Run AzureMediaRedactor.exe.</span></span> 

### <a name="use-hello-tool"></a><span data-ttu-id="d53b4-157">Użyj narzędzia hello</span><span class="sxs-lookup"><span data-stu-id="d53b4-157">Use hello tool</span></span>

1. <span data-ttu-id="d53b4-158">Przetwarzanie wideo na koncie usługi Azure Media Services z hello Redactor MP na tryb analizy.</span><span class="sxs-lookup"><span data-stu-id="d53b4-158">Process your video in your Azure Media Services account with hello Redactor MP on Analyze mode.</span></span> 
2. <span data-ttu-id="d53b4-159">Pobierz hello oryginalny plik wideo i na wyjściu hello hello redakcyjne — analizowanie zadania.</span><span class="sxs-lookup"><span data-stu-id="d53b4-159">Download both hello original video file and hello output of hello Redaction - Analyze job.</span></span> 
3. <span data-ttu-id="d53b4-160">Uruchom aplikację wizualizatora hello i wybierz pliki hello powyżej.</span><span class="sxs-lookup"><span data-stu-id="d53b4-160">Run hello visualizer application and choose hello files above.</span></span> 

    ![Redakcja twarzy](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough011.png)

4. <span data-ttu-id="d53b4-162">Wyświetl podgląd pliku.</span><span class="sxs-lookup"><span data-stu-id="d53b4-162">Preview your file.</span></span> <span data-ttu-id="d53b4-163">SELECT, która zostanie skierowany chcieliby tooblur za pomocą paska bocznego hello na powitania prawo.</span><span class="sxs-lookup"><span data-stu-id="d53b4-163">Select which faces you'd like tooblur via hello sidebar on hello right.</span></span> 
    
    ![Redakcja twarzy](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough012.png)

5.  <span data-ttu-id="d53b4-165">pole tekstowe dolnej Hello zaktualizuje krój hello identyfikatorów.</span><span class="sxs-lookup"><span data-stu-id="d53b4-165">hello bottom text field will update with hello face IDs.</span></span> <span data-ttu-id="d53b4-166">Utwórz plik o nazwie "idlist.txt" te identyfikatory jako listę rozdzielone znakami nowego wiersza.</span><span class="sxs-lookup"><span data-stu-id="d53b4-166">Create a file called "idlist.txt" with these IDs as a newline delimited list.</span></span> 

    >[!NOTE]
    > <span data-ttu-id="d53b4-167">Witaj idlist.txt powinny być zapisane w formacie ANSI.</span><span class="sxs-lookup"><span data-stu-id="d53b4-167">hello idlist.txt should be saved in ANSI.</span></span> <span data-ttu-id="d53b4-168">Można użyć toosave Notatnik w formacie ANSI.</span><span class="sxs-lookup"><span data-stu-id="d53b4-168">You can use notepad toosave in ANSI.</span></span>
    
6.  <span data-ttu-id="d53b4-169">Przekazywanie zawartości wyjściowej toohello tego pliku z kroku 1.</span><span class="sxs-lookup"><span data-stu-id="d53b4-169">Upload this file toohello output asset from step 1.</span></span> <span data-ttu-id="d53b4-170">Przekaż hello wideo toothis oryginału również i Ustaw jako podstawowy zasobów.</span><span class="sxs-lookup"><span data-stu-id="d53b4-170">Upload hello original video toothis asset as well and set as primary asset.</span></span> 
7.  <span data-ttu-id="d53b4-171">Uruchom zadanie redakcyjne ten zasób z "Redact" Tryb tooget hello końcowego zredagowanym wideo.</span><span class="sxs-lookup"><span data-stu-id="d53b4-171">Run Redaction job on this asset with "Redact" mode tooget hello final redacted video.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="d53b4-172">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d53b4-172">Next steps</span></span> 

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="d53b4-173">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="d53b4-173">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="d53b4-174">Powiązane linki</span><span class="sxs-lookup"><span data-stu-id="d53b4-174">Related links</span></span>
[<span data-ttu-id="d53b4-175">Przegląd analiz usługi Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="d53b4-175">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

[<span data-ttu-id="d53b4-176">W trakcie analizy multimediów Azure</span><span class="sxs-lookup"><span data-stu-id="d53b4-176">Azure Media Analytics demos</span></span>](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

[<span data-ttu-id="d53b4-177">Anonsowanie redakcyjne krój na potrzeby analizy multimediów Azure</span><span class="sxs-lookup"><span data-stu-id="d53b4-177">Announcing Face Redaction for Azure Media Analytics</span></span>](https://azure.microsoft.com/blog/azure-media-redactor/)
