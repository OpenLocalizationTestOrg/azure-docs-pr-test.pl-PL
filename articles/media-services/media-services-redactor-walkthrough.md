---
title: "Redagowanie krojów z przewodnikiem analizy multimediów Azure | Dokumentacja firmy Microsoft"
description: "W tym temacie przedstawiono instrukcje krok po kroku na temat uruchamiania redakcyjne pełnego przepływu pracy przy użyciu usługi Azure Media Services Explorer (AMSE) i Azure Media Redactor Visualizer (narzędzie typu open source)."
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
ms.openlocfilehash: c0c622237f8cdca65fb6933f14cc21e9eb9ac036
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="redact-faces-with-azure-media-analytics-walkthrough"></a><span data-ttu-id="ae6ad-103">Redagowanie krojów z przewodnikiem analizy multimediów Azure</span><span class="sxs-lookup"><span data-stu-id="ae6ad-103">Redact faces with Azure Media Analytics walkthrough</span></span>

## <a name="overview"></a><span data-ttu-id="ae6ad-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="ae6ad-104">Overview</span></span>

<span data-ttu-id="ae6ad-105">**Azure Media Redactor** jest [analizy multimediów Azure](media-services-analytics-overview.md) procesor multimediów (MP) oferuje skalowalne krój redakcyjne w chmurze.</span><span class="sxs-lookup"><span data-stu-id="ae6ad-105">**Azure Media Redactor** is an [Azure Media Analytics](media-services-analytics-overview.md) media processor (MP) that offers scalable face redaction in the cloud.</span></span> <span data-ttu-id="ae6ad-106">Redakcyjne krój umożliwia modyfikowanie wideo do rozmycia kroje wybrane osoby.</span><span class="sxs-lookup"><span data-stu-id="ae6ad-106">Face redaction enables you to modify your video in order to blur faces of selected individuals.</span></span> <span data-ttu-id="ae6ad-107">Można korzystać z usługi redakcyjne krój w publicznych scenariusze bezpieczeństwa i nośnika wiadomości.</span><span class="sxs-lookup"><span data-stu-id="ae6ad-107">You may want to use the face redaction service in public safety and news media scenarios.</span></span> <span data-ttu-id="ae6ad-108">Kilka minut najmniejszym zawiera wiele kroje może zająć godzin redagowanie ręcznie, ale z tą usługą krój redakcyjne wymagany wykonanie kilku prostych krokach.</span><span class="sxs-lookup"><span data-stu-id="ae6ad-108">A few minutes of footage that contains multiple faces can take hours to redact manually, but with this service the face redaction process will require just a few simple steps.</span></span> <span data-ttu-id="ae6ad-109">Aby uzyskać więcej informacji, zobacz [to](https://azure.microsoft.com/blog/azure-media-redactor/) blogu.</span><span class="sxs-lookup"><span data-stu-id="ae6ad-109">For  more information, see [this](https://azure.microsoft.com/blog/azure-media-redactor/) blog.</span></span>

<span data-ttu-id="ae6ad-110">Szczegółowe informacje o **Azure Media Redactor**, zobacz [omówienie redakcyjne krój](media-services-face-redaction.md) tematu.</span><span class="sxs-lookup"><span data-stu-id="ae6ad-110">For details about  **Azure Media Redactor**, see the [Face redaction overview](media-services-face-redaction.md) topic.</span></span>

<span data-ttu-id="ae6ad-111">W tym temacie przedstawiono instrukcje krok po kroku na temat uruchamiania redakcyjne pełnego przepływu pracy przy użyciu usługi Azure Media Services Explorer (AMSE) i Azure Media Redactor Visualizer (narzędzie typu open source).</span><span class="sxs-lookup"><span data-stu-id="ae6ad-111">This topic shows step by step instructions on how to run a full redaction workflow using Azure Media Services Explorer (AMSE) and Azure Media Redactor Visualizer (open source tool).</span></span>

<span data-ttu-id="ae6ad-112">**Azure Media Redactor** pakiet administracyjny jest obecnie w przeglądzie.</span><span class="sxs-lookup"><span data-stu-id="ae6ad-112">The **Azure Media Redactor** MP is currently in Preview.</span></span> <span data-ttu-id="ae6ad-113">Jest ona dostępna w wszystkich publicznych regiony platformy Azure, a także centrach danych instytucji rządowych Stanów Zjednoczonych i Chinach.</span><span class="sxs-lookup"><span data-stu-id="ae6ad-113">It is available in all public Azure regions as well as US Government and China data centers.</span></span> <span data-ttu-id="ae6ad-114">Ta wersja zapoznawcza jest obecnie bezpłatnie.</span><span class="sxs-lookup"><span data-stu-id="ae6ad-114">This preview is currently free of charge.</span></span> <span data-ttu-id="ae6ad-115">W bieżącej wersji ma limitu 10 minut na przetworzonych długość wideo.</span><span class="sxs-lookup"><span data-stu-id="ae6ad-115">In the current release, there is a 10 minute limit on processed video length.</span></span>

<span data-ttu-id="ae6ad-116">Aby uzyskać więcej informacji, zobacz [to](https://azure.microsoft.com/en-us/blog/redaction-preview-available-globally) blogu.</span><span class="sxs-lookup"><span data-stu-id="ae6ad-116">For more information, see [this](https://azure.microsoft.com/en-us/blog/redaction-preview-available-globally) blog.</span></span>

## <a name="azure-media-services-explorer-workflow"></a><span data-ttu-id="ae6ad-117">Azure Media Services Explorer przepływu pracy</span><span class="sxs-lookup"><span data-stu-id="ae6ad-117">Azure Media Services Explorer workflow</span></span>

<span data-ttu-id="ae6ad-118">Najłatwiejszym sposobem na szybkie wprowadzenie Redactor jest narzędzie AMSE typu open source w witrynie github.</span><span class="sxs-lookup"><span data-stu-id="ae6ad-118">The easiest way to get started with Redactor is to use the open source AMSE tool on github.</span></span> <span data-ttu-id="ae6ad-119">Możesz uruchomić uproszczony przepływu pracy za pośrednictwem **łączyć** tryb, jeśli nie jest potrzebny dostęp do json adnotacji ani krój obrazów jpg.</span><span class="sxs-lookup"><span data-stu-id="ae6ad-119">You can run a simplified workflow via **combined** mode if you don’t need access to the annotation json or the face jpg images.</span></span>

### <a name="download-and-setup"></a><span data-ttu-id="ae6ad-120">Pobierania i instalacji</span><span class="sxs-lookup"><span data-stu-id="ae6ad-120">Download and setup</span></span>

1. <span data-ttu-id="ae6ad-121">Pobierz narzędzie AMSE z [tutaj](https://github.com/Azure/Azure-Media-Services-Explorer).</span><span class="sxs-lookup"><span data-stu-id="ae6ad-121">Download the AMSE tool from [here](https://github.com/Azure/Azure-Media-Services-Explorer).</span></span>
1. <span data-ttu-id="ae6ad-122">Zaloguj się do konta usługi Media Services przy użyciu klucza usługi.</span><span class="sxs-lookup"><span data-stu-id="ae6ad-122">Log in to your Media Services account using your service key.</span></span>

    <span data-ttu-id="ae6ad-123">Aby uzyskać informacje o kluczu i nazwie konta, przejdź do witryny [Azure Portal](https://portal.azure.com/) i wybierz swoje konto AMS.</span><span class="sxs-lookup"><span data-stu-id="ae6ad-123">To obtain the account name and key information, go to the [Azure portal](https://portal.azure.com/) and select your AMS account.</span></span> <span data-ttu-id="ae6ad-124">Wybierz ustawienia > klucze.</span><span class="sxs-lookup"><span data-stu-id="ae6ad-124">Then, select Settings > Keys.</span></span> <span data-ttu-id="ae6ad-125">W oknie Zarządzanie kluczami widoczna jest nazwa konta oraz wyświetlane są klucze podstawowe i pomocnicze.</span><span class="sxs-lookup"><span data-stu-id="ae6ad-125">The Manage keys windows shows the account name and the primary and secondary keys is displayed.</span></span> <span data-ttu-id="ae6ad-126">Skopiuj wartości nazwy konta i klucza podstawowego.</span><span class="sxs-lookup"><span data-stu-id="ae6ad-126">Copy values of the account name and the primary key.</span></span>

![Redakcja twarzy](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough001.png)

### <a name="first-pass--analyze-mode"></a><span data-ttu-id="ae6ad-128">Najpierw przekazać — analizowanie tryb</span><span class="sxs-lookup"><span data-stu-id="ae6ad-128">First pass – analyze mode</span></span>

1. <span data-ttu-id="ae6ad-129">Przekazywanie pliku multimediów za pośrednictwem zasobów –> przekazywania, lub za pośrednictwem operacji przeciągania i upuszczania.</span><span class="sxs-lookup"><span data-stu-id="ae6ad-129">Upload your media file through Asset –> Upload, or via drag and drop.</span></span> 
1. <span data-ttu-id="ae6ad-130">Kliknij prawym przyciskiem myszy i przetwarzanie pliku nośnika, przy użyciu analizy multimediów Azure Media Redactor –> –> Tryb analizy.</span><span class="sxs-lookup"><span data-stu-id="ae6ad-130">Right click and process your media file using Media Analytics –> Azure Media Redactor –> Analyze mode.</span></span> 


![Redakcja twarzy](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough002.png)

![Redakcja twarzy](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough003.png)

<span data-ttu-id="ae6ad-133">Dane wyjściowe będzie zawierać plik json adnotacje z danych lokalizacji krój, a także jpg każdego wykrytego powierzchni.</span><span class="sxs-lookup"><span data-stu-id="ae6ad-133">The output will include an annotations json file with face location data, as well as a jpg of each detected face.</span></span> 

![Redakcja twarzy](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough004.png)

###<a name="second-pass--redact-mode"></a><span data-ttu-id="ae6ad-135">Drugi przekazać — redagowanie tryb</span><span class="sxs-lookup"><span data-stu-id="ae6ad-135">Second pass – redact mode</span></span>

1. <span data-ttu-id="ae6ad-136">Wyślij oryginalnej zawartości wideo dane wyjściowe z pierwszego przejścia i Ustaw jako podstawowy zasobów.</span><span class="sxs-lookup"><span data-stu-id="ae6ad-136">Upload your original video asset to the output from the first pass and set as a primary asset.</span></span> 

    ![Redakcja twarzy](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough005.png)

2. <span data-ttu-id="ae6ad-138">(Opcjonalnie) Przekaż plik "Dance_idlist.txt", który zawiera listę identyfikatorów chcesz redagowanie rozdzielone znakami nowego wiersza.</span><span class="sxs-lookup"><span data-stu-id="ae6ad-138">(Optional) Upload a 'Dance_idlist.txt' file which includes a newline delimited list of the IDs you wish to redact.</span></span> 

    ![Redakcja twarzy](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough006.png)

3. <span data-ttu-id="ae6ad-140">(Opcjonalnie) Wprowadź zmiany w pliku annotations.json, takich jak zwiększenie ograniczający granice pola.</span><span class="sxs-lookup"><span data-stu-id="ae6ad-140">(Optional) Make any edits to the annotations.json file such as increasing the bounding box boundaries.</span></span> 
4. <span data-ttu-id="ae6ad-141">Kliknij prawym przyciskiem myszy elementu zawartości wyjściowej z pierwszego przejścia, wybierz Redactor i uruchom z **Redact** tryb.</span><span class="sxs-lookup"><span data-stu-id="ae6ad-141">Right click the output asset from the first pass, select the Redactor, and run with the **Redact** mode.</span></span> 

    ![Redakcja twarzy](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough007.png)

5. <span data-ttu-id="ae6ad-143">Pobieranie i udostępnianie zasobów zredagowanym pliku wyjściowego.</span><span class="sxs-lookup"><span data-stu-id="ae6ad-143">Download or share the final redacted output asset.</span></span> 

    ![Redakcja twarzy](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough008.png)

##<a name="azure-media-redactor-visualizer-open-source-tool"></a><span data-ttu-id="ae6ad-145">Azure Media Redactor wizualizatora typu open source narzędzia</span><span class="sxs-lookup"><span data-stu-id="ae6ad-145">Azure Media Redactor Visualizer open source tool</span></span>

<span data-ttu-id="ae6ad-146">Typu open source [narzędzie wizualizatora](https://github.com/Microsoft/azure-media-redactor-visualizer) ułatwia deweloperom uruchamiana z formatem adnotacje z analizy i przy użyciu danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="ae6ad-146">An open source [visualizer tool](https://github.com/Microsoft/azure-media-redactor-visualizer) is designed to help developers just starting with the annotations format with parsing and using the output.</span></span>

<span data-ttu-id="ae6ad-147">Po można sklonować repozytorium, aby można było uruchomić projekt, musisz pobrać FFMPEG z ich [oficjalna witryna](https://ffmpeg.org/download.html).</span><span class="sxs-lookup"><span data-stu-id="ae6ad-147">After you clone the repo, in order to run the project, you will need to download FFMPEG from their [official site](https://ffmpeg.org/download.html).</span></span>

<span data-ttu-id="ae6ad-148">Jeśli jesteś deweloperem próby przeprowadzenia analizy danych JSON adnotacji, poszukaj wewnątrz Models.MetaData przykłady kodu przykładowej.</span><span class="sxs-lookup"><span data-stu-id="ae6ad-148">If you are a developer trying to parse the JSON annotation data, look inside Models.MetaData for sample code examples.</span></span>

### <a name="set-up-the-tool"></a><span data-ttu-id="ae6ad-149">Konfigurowanie narzędzia</span><span class="sxs-lookup"><span data-stu-id="ae6ad-149">Set up the tool</span></span>

1.  <span data-ttu-id="ae6ad-150">Pobierz i skompiluj całe rozwiązanie.</span><span class="sxs-lookup"><span data-stu-id="ae6ad-150">Download and build the entire solution.</span></span> 

    ![Redakcja twarzy](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough009.png)

2.  <span data-ttu-id="ae6ad-152">Pobierz FFMPEG z [tutaj](https://ffmpeg.org/download.html).</span><span class="sxs-lookup"><span data-stu-id="ae6ad-152">Download FFMPEG from [here](https://ffmpeg.org/download.html).</span></span> <span data-ttu-id="ae6ad-153">Ten projekt pierwotnie został opracowany z wersji be1d324 (2016-10-04) z statycznego łączenia.</span><span class="sxs-lookup"><span data-stu-id="ae6ad-153">This project was originally developed with version be1d324 (2016-10-04) with static linking.</span></span> 
3.  <span data-ttu-id="ae6ad-154">Skopiuj ffmpeg.exe i ffprobe.exe do tego samego folderu wyjściowego jako AzureMediaRedactor.exe.</span><span class="sxs-lookup"><span data-stu-id="ae6ad-154">Copy ffmpeg.exe and ffprobe.exe to the same output folder as AzureMediaRedactor.exe.</span></span> 

    ![Redakcja twarzy](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough010.png)

4. <span data-ttu-id="ae6ad-156">Uruchom AzureMediaRedactor.exe.</span><span class="sxs-lookup"><span data-stu-id="ae6ad-156">Run AzureMediaRedactor.exe.</span></span> 

### <a name="use-the-tool"></a><span data-ttu-id="ae6ad-157">Użyj narzędzia</span><span class="sxs-lookup"><span data-stu-id="ae6ad-157">Use the tool</span></span>

1. <span data-ttu-id="ae6ad-158">Przetwarzanie wideo na koncie usługi Azure Media Services z Redactor MP na tryb analizy.</span><span class="sxs-lookup"><span data-stu-id="ae6ad-158">Process your video in your Azure Media Services account with the Redactor MP on Analyze mode.</span></span> 
2. <span data-ttu-id="ae6ad-159">Pobierz zarówno oryginalny plik wideo, jak i dane wyjściowe redakcyjne — analizowanie zadania.</span><span class="sxs-lookup"><span data-stu-id="ae6ad-159">Download both the original video file and the output of the Redaction - Analyze job.</span></span> 
3. <span data-ttu-id="ae6ad-160">Uruchom aplikację wizualizatora i wybierz pliki powyżej.</span><span class="sxs-lookup"><span data-stu-id="ae6ad-160">Run the visualizer application and choose the files above.</span></span> 

    ![Redakcja twarzy](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough011.png)

4. <span data-ttu-id="ae6ad-162">Wyświetl podgląd pliku.</span><span class="sxs-lookup"><span data-stu-id="ae6ad-162">Preview your file.</span></span> <span data-ttu-id="ae6ad-163">Wybierz kroje, które chcesz rozmycia za pomocą paska bocznego po prawej stronie.</span><span class="sxs-lookup"><span data-stu-id="ae6ad-163">Select which faces you'd like to blur via the sidebar on the right.</span></span> 
    
    ![Redakcja twarzy](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough012.png)

5.  <span data-ttu-id="ae6ad-165">Pole tekstowe dolnej zaktualizuje kroju identyfikatorów.</span><span class="sxs-lookup"><span data-stu-id="ae6ad-165">The bottom text field will update with the face IDs.</span></span> <span data-ttu-id="ae6ad-166">Utwórz plik o nazwie "idlist.txt" te identyfikatory jako listę rozdzielone znakami nowego wiersza.</span><span class="sxs-lookup"><span data-stu-id="ae6ad-166">Create a file called "idlist.txt" with these IDs as a newline delimited list.</span></span> 

    >[!NOTE]
    > <span data-ttu-id="ae6ad-167">Idlist.txt powinny być zapisane w formacie ANSI.</span><span class="sxs-lookup"><span data-stu-id="ae6ad-167">The idlist.txt should be saved in ANSI.</span></span> <span data-ttu-id="ae6ad-168">Notatnik umożliwia zapisywanie w formacie ANSI.</span><span class="sxs-lookup"><span data-stu-id="ae6ad-168">You can use notepad to save in ANSI.</span></span>
    
6.  <span data-ttu-id="ae6ad-169">Przekazywanie tego pliku do elementu zawartości wyjściowej z kroku 1.</span><span class="sxs-lookup"><span data-stu-id="ae6ad-169">Upload this file to the output asset from step 1.</span></span> <span data-ttu-id="ae6ad-170">Przekazywanie oryginalnego wideo do trwałego również i Ustaw jako podstawowy zasobów.</span><span class="sxs-lookup"><span data-stu-id="ae6ad-170">Upload the original video to this asset as well and set as primary asset.</span></span> 
7.  <span data-ttu-id="ae6ad-171">Uruchom zadanie redakcyjne ten zasób w trybie "Redact" można uzyskać końcowa zredagowanego wideo.</span><span class="sxs-lookup"><span data-stu-id="ae6ad-171">Run Redaction job on this asset with "Redact" mode to get the final redacted video.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="ae6ad-172">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ae6ad-172">Next steps</span></span> 

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="ae6ad-173">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="ae6ad-173">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="ae6ad-174">Powiązane linki</span><span class="sxs-lookup"><span data-stu-id="ae6ad-174">Related links</span></span>
[<span data-ttu-id="ae6ad-175">Przegląd analiz usługi Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="ae6ad-175">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

[<span data-ttu-id="ae6ad-176">W trakcie analizy multimediów Azure</span><span class="sxs-lookup"><span data-stu-id="ae6ad-176">Azure Media Analytics demos</span></span>](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

[<span data-ttu-id="ae6ad-177">Anonsowanie redakcyjne krój na potrzeby analizy multimediów Azure</span><span class="sxs-lookup"><span data-stu-id="ae6ad-177">Announcing Face Redaction for Azure Media Analytics</span></span>](https://azure.microsoft.com/blog/azure-media-redactor/)
