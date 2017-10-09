---
title: aaaUsing castLabs toodeliver Widevine licencje tooAzure Media Services | Dokumentacja firmy Microsoft
description: "W tym artykule opisano, jak używasz usługi Azure Media Services (AMS) toodeliver dynamicznie szyfrowanych przez AMS z PlayReady i Widevine DRMs strumienia. licencji PlayReady Hello pochodzi z serwera licencji Media Services PlayReady i licencji Widevine jest dostarczany przez serwer licencji castLabs."
services: media-services
documentationcenter: 
author: Mingfeiy
manager: cfowler
editor: 
ms.assetid: 2a9a408a-a995-49e1-8d8f-ac5b51e17d40
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: Mingfeiy;willzhan;Juliako
ms.openlocfilehash: 80d2778fb283a96361e7e511990a36c2f551a310
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="using-castlabs-toodeliver-widevine-licenses-tooazure-media-services"></a><span data-ttu-id="7c56d-104">Przy użyciu castLabs toodeliver Widevine licencji tooAzure Media Services</span><span class="sxs-lookup"><span data-stu-id="7c56d-104">Using castLabs toodeliver Widevine licenses tooAzure Media Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7c56d-105">Axinom</span><span class="sxs-lookup"><span data-stu-id="7c56d-105">Axinom</span></span>](media-services-axinom-integration.md)
> * [<span data-ttu-id="7c56d-106">castLabs</span><span class="sxs-lookup"><span data-stu-id="7c56d-106">castLabs</span></span>](media-services-castlabs-integration.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="7c56d-107">Omówienie</span><span class="sxs-lookup"><span data-stu-id="7c56d-107">Overview</span></span>
<span data-ttu-id="7c56d-108">W tym artykule opisano, jak używasz usługi Azure Media Services (AMS) toodeliver dynamicznie szyfrowanych przez AMS z PlayReady i Widevine DRMs strumienia.</span><span class="sxs-lookup"><span data-stu-id="7c56d-108">This article describes how you can use Azure Media Services (AMS) toodeliver a stream that is dynamically encrypted by AMS with both PlayReady and Widevine DRMs.</span></span> <span data-ttu-id="7c56d-109">licencji PlayReady Hello pochodzi z serwera licencji Media Services PlayReady i licencji Widevine jest dostarczany przez **castLabs** serwera licencji.</span><span class="sxs-lookup"><span data-stu-id="7c56d-109">hello PlayReady license comes from Media Services PlayReady license server and Widevine license is delivered by **castLabs** license server.</span></span>

<span data-ttu-id="7c56d-110">tooplayback przesyłania strumieniowego zawartości chronionej przez CENC (PlayReady i Widevine), możesz użyć [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span><span class="sxs-lookup"><span data-stu-id="7c56d-110">tooplayback streaming content protected by CENC (PlayReady and/or Widevine), you can use  [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span> <span data-ttu-id="7c56d-111">Zobacz [dokumentu AMP](http://amp.azure.net/libs/amp/latest/docs/) szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="7c56d-111">See [AMP document](http://amp.azure.net/libs/amp/latest/docs/) for details.</span></span>

<span data-ttu-id="7c56d-112">powitania po diagram przedstawia wysokiego poziomu architektury integracji usługi Azure Media Services i castLabs.</span><span class="sxs-lookup"><span data-stu-id="7c56d-112">hello following diagram demonstrates a high-level Azure Media Services and castLabs integration architecture.</span></span>

![Integracja](./media/media-services-castlabs-integration/media-services-castlabs-integration.png)

## <a name="typical-system-set-up"></a><span data-ttu-id="7c56d-114">Typowy systemem</span><span class="sxs-lookup"><span data-stu-id="7c56d-114">Typical system set up</span></span>
* <span data-ttu-id="7c56d-115">Nośnik zawartość jest przechowywana w AMS.</span><span class="sxs-lookup"><span data-stu-id="7c56d-115">Media content is stored in AMS.</span></span>
* <span data-ttu-id="7c56d-116">Identyfikatory klucz zawartości kluczy są przechowywane w castLabs i AMS.</span><span class="sxs-lookup"><span data-stu-id="7c56d-116">Key IDs of content keys are stored in both castLabs and AMS.</span></span>
* <span data-ttu-id="7c56d-117">castLabs i AMS ma token uwierzytelniania wbudowane.</span><span class="sxs-lookup"><span data-stu-id="7c56d-117">castLabs and AMS both have token authentication built in.</span></span> <span data-ttu-id="7c56d-118">Hello w następujących sekcjach omówiono w nim tokeny uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="7c56d-118">hello following sections discuss authentication tokens.</span></span> 
* <span data-ttu-id="7c56d-119">Gdy klient żąda toostream hello wideo, zawartość hello dynamicznie jest szyfrowana za **Common Encryption** (CENC) i dynamicznie opakowane przez AMS tooSmooth przesyłania strumieniowego i KRESKI.</span><span class="sxs-lookup"><span data-stu-id="7c56d-119">When a client requests toostream hello video, hello content is dynamically encrypted with **Common Encryption** (CENC) and dynamically packaged by AMS tooSmooth Streaming and DASH.</span></span> <span data-ttu-id="7c56d-120">Możemy również zapewniać PlayReady M2TS podstawowe strumienia szyfrowania dla protokołu HLS protokołu przesyłania strumieniowego.</span><span class="sxs-lookup"><span data-stu-id="7c56d-120">We also deliver PlayReady M2TS elementary stream encryption for HLS streaming protocol.</span></span>
* <span data-ttu-id="7c56d-121">Licencja PlayReady są pobierane z serwera licencji usług AMS i licencji Widevine są pobierane z serwera licencji castLabs.</span><span class="sxs-lookup"><span data-stu-id="7c56d-121">PlayReady license is retrieved from AMS license server and Widevine license is retrieved from castLabs license server.</span></span> 
* <span data-ttu-id="7c56d-122">Odtwarzacz automatycznie decyduje, które toofetch licencji, w oparciu o możliwości platformy powitania klienta.</span><span class="sxs-lookup"><span data-stu-id="7c56d-122">Media Player automatically decides which license toofetch based on hello client platform capability.</span></span> 

## <a name="authentication-token-generation-for-getting-a-license"></a><span data-ttu-id="7c56d-123">Generowanie tokenu uwierzytelniania dla pobierania licencji</span><span class="sxs-lookup"><span data-stu-id="7c56d-123">Authentication token generation for getting a license</span></span>
<span data-ttu-id="7c56d-124">Zarówno castLabs, jak i AMS obsługuje tooauthorize używany format tokenu JWT (JSON Web Token) licencji.</span><span class="sxs-lookup"><span data-stu-id="7c56d-124">Both castLabs and AMS support JWT (JSON Web Token) token format used tooauthorize a license.</span></span> 

### <a name="jwt-token-in-ams"></a><span data-ttu-id="7c56d-125">Token JWT w AMS</span><span class="sxs-lookup"><span data-stu-id="7c56d-125">JWT token in AMS</span></span>
<span data-ttu-id="7c56d-126">Witaj w poniższej tabeli opisano tokenu JWT w AMS.</span><span class="sxs-lookup"><span data-stu-id="7c56d-126">hello following table describes JWT token in AMS.</span></span> 

| <span data-ttu-id="7c56d-127">Wystawcy</span><span class="sxs-lookup"><span data-stu-id="7c56d-127">Issuer</span></span> | <span data-ttu-id="7c56d-128">Ciąg wystawcy z hello wybrany Secure Token Service (STS)</span><span class="sxs-lookup"><span data-stu-id="7c56d-128">Issuer string from hello chosen Secure Token Service (STS)</span></span> |
| --- | --- |
| <span data-ttu-id="7c56d-129">Grupy odbiorców</span><span class="sxs-lookup"><span data-stu-id="7c56d-129">Audience</span></span> |<span data-ttu-id="7c56d-130">Ciąg odbiorców z hello używany STS</span><span class="sxs-lookup"><span data-stu-id="7c56d-130">Audience string from hello used STS</span></span> |
| <span data-ttu-id="7c56d-131">Oświadczenia</span><span class="sxs-lookup"><span data-stu-id="7c56d-131">Claims</span></span> |<span data-ttu-id="7c56d-132">Zestaw oświadczeń</span><span class="sxs-lookup"><span data-stu-id="7c56d-132">A set of claims</span></span> |
| <span data-ttu-id="7c56d-133">Nie wcześniej niż</span><span class="sxs-lookup"><span data-stu-id="7c56d-133">NotBefore</span></span> |<span data-ttu-id="7c56d-134">Ważność tokenu hello Start</span><span class="sxs-lookup"><span data-stu-id="7c56d-134">Start validity of hello token</span></span> |
| <span data-ttu-id="7c56d-135">Wygasa</span><span class="sxs-lookup"><span data-stu-id="7c56d-135">Expires</span></span> |<span data-ttu-id="7c56d-136">Ważność tokenu hello zakończenia</span><span class="sxs-lookup"><span data-stu-id="7c56d-136">End validity of hello token</span></span> |
| <span data-ttu-id="7c56d-137">Elementu SigningCredentials</span><span class="sxs-lookup"><span data-stu-id="7c56d-137">SigningCredentials</span></span> |<span data-ttu-id="7c56d-138">klucz Hello, użytkowany przez serwer licencji PlayReady, castLabs serwera licencji i STS, może to być klucz konfiguracji symetrycznej lub asymetrycznej.</span><span class="sxs-lookup"><span data-stu-id="7c56d-138">hello key that is shared among PlayReady License Server, castLabs License Server and STS, it could be either symmetric or asymmetric key.</span></span> |

### <a name="jwt-token-in-castlabs"></a><span data-ttu-id="7c56d-139">Token JWT w castLabs</span><span class="sxs-lookup"><span data-stu-id="7c56d-139">JWT token in castLabs</span></span>
<span data-ttu-id="7c56d-140">Witaj w poniższej tabeli opisano tokenu JWT w castLabs.</span><span class="sxs-lookup"><span data-stu-id="7c56d-140">hello following table describes JWT token in castLabs.</span></span> 

| <span data-ttu-id="7c56d-141">Nazwa</span><span class="sxs-lookup"><span data-stu-id="7c56d-141">Name</span></span> | <span data-ttu-id="7c56d-142">Opis</span><span class="sxs-lookup"><span data-stu-id="7c56d-142">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7c56d-143">optData</span><span class="sxs-lookup"><span data-stu-id="7c56d-143">optData</span></span> |<span data-ttu-id="7c56d-144">Ciąg JSON zawierający informacje o Tobie.</span><span class="sxs-lookup"><span data-stu-id="7c56d-144">A JSON string containing information about you.</span></span> |
| <span data-ttu-id="7c56d-145">CRT</span><span class="sxs-lookup"><span data-stu-id="7c56d-145">crt</span></span> |<span data-ttu-id="7c56d-146">JSON ciąg zawierający informacje o hello zasobów, jego informacje o i odtwarzania praw licencyjnych.</span><span class="sxs-lookup"><span data-stu-id="7c56d-146">A JSON string containing information about hello asset, its license info and playback rights.</span></span> |
| <span data-ttu-id="7c56d-147">IAT</span><span class="sxs-lookup"><span data-stu-id="7c56d-147">iat</span></span> |<span data-ttu-id="7c56d-148">Hello bieżącej daty/godziny w epoki.</span><span class="sxs-lookup"><span data-stu-id="7c56d-148">hello current datetime in epoch.</span></span> |
| <span data-ttu-id="7c56d-149">jti</span><span class="sxs-lookup"><span data-stu-id="7c56d-149">jti</span></span> |<span data-ttu-id="7c56d-150">Unikatowy identyfikator o token (token, co może być użyte tylko raz w systemie castLabs hello).</span><span class="sxs-lookup"><span data-stu-id="7c56d-150">A unique identifier about this token (every token can only be used once in hello castLabs system).</span></span> |

## <a name="sample-solution-set-up"></a><span data-ttu-id="7c56d-151">Przykładowe rozwiązanie — Konfiguracja</span><span class="sxs-lookup"><span data-stu-id="7c56d-151">Sample solution set up</span></span>
<span data-ttu-id="7c56d-152">Witaj [przykładowe rozwiązanie](https://github.com/AzureMediaServicesSamples/CastlabsIntegration) składa się z dwóch projektów:</span><span class="sxs-lookup"><span data-stu-id="7c56d-152">hello [sample solution](https://github.com/AzureMediaServicesSamples/CastlabsIntegration) consists of two projects:</span></span>

* <span data-ttu-id="7c56d-153">Aplikacja konsoli, które mogą być używane tooset DRM ograniczenia zasób już pozyskiwane PlayReady i Widevine.</span><span class="sxs-lookup"><span data-stu-id="7c56d-153">A console app that can be used tooset DRM restrictions on an already ingested asset, for both PlayReady and Widevine.</span></span>
* <span data-ttu-id="7c56d-154">Aplikacja sieci Web, która przekazuje limit tokeny, których może być traktowany jako bardzo uproszczonej wersji usługi tokenu Zabezpieczającego.</span><span class="sxs-lookup"><span data-stu-id="7c56d-154">A Web Application that hands out tokens, which could be seen as a VERY SIMPLIFIED version of an STS.</span></span>

<span data-ttu-id="7c56d-155">Aplikacja konsolowa hello toouse:</span><span class="sxs-lookup"><span data-stu-id="7c56d-155">toouse hello console application:</span></span>

1. <span data-ttu-id="7c56d-156">Zmień hello app.config toosetup AMS poświadczeń, poświadczenia castLabs, konfiguracji usługi STS i klucza wspólnego.</span><span class="sxs-lookup"><span data-stu-id="7c56d-156">Change hello app.config toosetup AMS credentials, castLabs credentials, STS configuration and shared key.</span></span>
2. <span data-ttu-id="7c56d-157">Przekaż zasób do AMS.</span><span class="sxs-lookup"><span data-stu-id="7c56d-157">Upload an Asset into AMS.</span></span>
3. <span data-ttu-id="7c56d-158">Get hello UUID z hello przekazywane zasobów i zmienić 32 wiersz w pliku Program.cs hello:</span><span class="sxs-lookup"><span data-stu-id="7c56d-158">Get hello UUID from hello uploaded Asset, and change Line 32 in hello Program.cs file:</span></span>
   
      <span data-ttu-id="7c56d-159">var objIAsset = _kontekstu. Assets.Where (x = > x.Id == "nb:cid:UUID:dac53a5d-1500-80bd-b864-f1e4b62594cf"). FirstOrDefault();</span><span class="sxs-lookup"><span data-stu-id="7c56d-159">var objIAsset = _context.Assets.Where(x => x.Id == "nb:cid:UUID:dac53a5d-1500-80bd-b864-f1e4b62594cf").FirstOrDefault();</span></span>
4. <span data-ttu-id="7c56d-160">Użyj IDśrodkaTrwałego nazewnictwa hello zasobów w systemie castLabs hello (44 wiersz w pliku Program.cs hello).</span><span class="sxs-lookup"><span data-stu-id="7c56d-160">Use an AssetId for naming hello asset in hello castLabs system (Line 44 in hello Program.cs file).</span></span>
   
   <span data-ttu-id="7c56d-161">Należy ustawić IDśrodkaTrwałego dla **castLabs**; musi on toobe unikatowy ciąg alfanumeryczny.</span><span class="sxs-lookup"><span data-stu-id="7c56d-161">You must set AssetId for **castLabs**; it needs toobe a unique alphanumeric string.</span></span>
5. <span data-ttu-id="7c56d-162">Uruchom hello program.</span><span class="sxs-lookup"><span data-stu-id="7c56d-162">Run hello program.</span></span>

<span data-ttu-id="7c56d-163">Witaj toouse aplikacji sieci Web (STS):</span><span class="sxs-lookup"><span data-stu-id="7c56d-163">toouse hello Web Application (STS):</span></span>

1. <span data-ttu-id="7c56d-164">Zmień hello web.config toosetup castlabs sprzedawcy Identyfikatora, konfiguracji usługi STS hello i hello klucza wspólnego.</span><span class="sxs-lookup"><span data-stu-id="7c56d-164">Change hello web.config toosetup castlabs merchant ID, hello STS configuration and hello shared key.</span></span>
2. <span data-ttu-id="7c56d-165">Wdróż tooAzure witryn sieci Web.</span><span class="sxs-lookup"><span data-stu-id="7c56d-165">Deploy tooAzure Websites.</span></span>
3. <span data-ttu-id="7c56d-166">Przejdź toohello witryny sieci Web.</span><span class="sxs-lookup"><span data-stu-id="7c56d-166">Navigate toohello website.</span></span>

## <a name="playing-back-a-video"></a><span data-ttu-id="7c56d-167">Odtwarzanie wideo</span><span class="sxs-lookup"><span data-stu-id="7c56d-167">Playing back a video</span></span>
<span data-ttu-id="7c56d-168">tooplayback wideo zaszyfrowane za pomocą wspólnego szyfrowania (PlayReady i Widevine), możesz użyć hello [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span><span class="sxs-lookup"><span data-stu-id="7c56d-168">tooplayback a video encrypted with common encryption (PlayReady and/or Widevine), you can use hello [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span> <span data-ttu-id="7c56d-169">Podczas uruchamiania aplikacji konsoli hello, powtarzana hello Identyfikatora klucza zawartości i hello manifestu adresu URL.</span><span class="sxs-lookup"><span data-stu-id="7c56d-169">When running hello console app, hello Content Key ID and hello Manifest URL are echoed.</span></span>

1. <span data-ttu-id="7c56d-170">Otwórz nową kartę, a następnie uruchom z STS: http://[yourStsName].azurewebsites.net/api/token/assetid/[yourCastLabsAssetId]/contentkeyid/[thecontentkeyid].</span><span class="sxs-lookup"><span data-stu-id="7c56d-170">Open a new tab and launch your STS: http://[yourStsName].azurewebsites.net/api/token/assetid/[yourCastLabsAssetId]/contentkeyid/[thecontentkeyid].</span></span>
2. <span data-ttu-id="7c56d-171">Przejdź za[Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span><span class="sxs-lookup"><span data-stu-id="7c56d-171">Go too[Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).</span></span>
3. <span data-ttu-id="7c56d-172">Wklej hello URL przesyłania strumieniowego.</span><span class="sxs-lookup"><span data-stu-id="7c56d-172">Paste in hello streaming URL.</span></span>
4. <span data-ttu-id="7c56d-173">Kliknij przycisk hello **zaawansowane opcje** wyboru.</span><span class="sxs-lookup"><span data-stu-id="7c56d-173">Click hello **Advanced Options** checkbox.</span></span>
5. <span data-ttu-id="7c56d-174">W hello **ochrony** listy rozwijanej wybierz PlayReady i Widevine.</span><span class="sxs-lookup"><span data-stu-id="7c56d-174">In hello **Protection** dropdown, select PlayReady and/or Widevine.</span></span>
6. <span data-ttu-id="7c56d-175">Wklej token hello, pochodzący z sieci usługi STS w polu tekstowym Token hello.</span><span class="sxs-lookup"><span data-stu-id="7c56d-175">Paste hello token that you got from your STS in hello Token textbox.</span></span> 
   
   <span data-ttu-id="7c56d-176">serwer licencji castLab Hello nie jest konieczne hello "Bearer =" prefiks przed hello tokenu.</span><span class="sxs-lookup"><span data-stu-id="7c56d-176">hello castLab license server does not need hello “Bearer=” prefix in front of hello token.</span></span> <span data-ttu-id="7c56d-177">Dlatego należy usunąć przed przesłaniem hello token.</span><span class="sxs-lookup"><span data-stu-id="7c56d-177">So please remove that before submitting hello token.</span></span>
7. <span data-ttu-id="7c56d-178">Aktualizacja hello player.</span><span class="sxs-lookup"><span data-stu-id="7c56d-178">Update hello player.</span></span>
8. <span data-ttu-id="7c56d-179">powinien być odtwarzanie Hello wideo.</span><span class="sxs-lookup"><span data-stu-id="7c56d-179">hello video should be playing.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="7c56d-180">Ścieżki szkoleniowe dotyczące usługi Media Services</span><span class="sxs-lookup"><span data-stu-id="7c56d-180">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="7c56d-181">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="7c56d-181">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

