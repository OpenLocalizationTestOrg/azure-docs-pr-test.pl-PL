---
title: "aaaImprove wydajności przez kompresowanie plików w usłudze Azure CDN | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak transfer plików tooimprove szybkości i zwiększa wydajność obciążenia strony przez kompresowanie plików w usłudze Azure CDN."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: af1cddff-78d8-476b-a9d0-8c2164e4de5d
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 9a1698b6c29233c2e2e6fb17cdd8e919ae8bfa1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="improve-performance-by-compressing-files-in-azure-cdn"></a><span data-ttu-id="14a0b-103">Zwiększenie wydajności przez kompresowanie plików w usłudze Azure CDN</span><span class="sxs-lookup"><span data-stu-id="14a0b-103">Improve performance by compressing files in Azure CDN</span></span>
<span data-ttu-id="14a0b-104">Jest to prosta i skuteczna metoda szybkości transferu plików tooimprove i zwiększyć strony obciążenia wydajność przez zmniejszenie rozmiaru pliku przed są wysyłane z serwera hello.</span><span class="sxs-lookup"><span data-stu-id="14a0b-104">Compression is a simple and effective method tooimprove file transfer speed and increase page load performance by reducing file size before it is sent from hello server.</span></span> <span data-ttu-id="14a0b-105">Zmniejsza kosztów przepustowości i zapewnia bardziej odpowiednie dla użytkowników.</span><span class="sxs-lookup"><span data-stu-id="14a0b-105">It reduces bandwidth costs and provides a more responsive experience for your users.</span></span>

<span data-ttu-id="14a0b-106">Istnieją dwa sposoby tooenable kompresji:</span><span class="sxs-lookup"><span data-stu-id="14a0b-106">There are two ways tooenable compression:</span></span>

* <span data-ttu-id="14a0b-107">W takim przypadku hello CDN przechodzą hello skompresowane pliki i dostarczać tooclients skompresowane pliki, które ich zażądać, można włączyć kompresję na serwerze pochodzenia.</span><span class="sxs-lookup"><span data-stu-id="14a0b-107">You can enable compression on your origin server, in which case hello CDN passes through hello compressed files and deliver compressed files tooclients that request them.</span></span>
* <span data-ttu-id="14a0b-108">Można włączyć kompresję bezpośrednio w sieci CDN krawędzi serwerów, w których wielkość hello CDN kompresuje hello plików i obsługujących je tooend użytkowników, nawet jeśli nie są kompresowane przez powitania serwera źródłowego.</span><span class="sxs-lookup"><span data-stu-id="14a0b-108">You can enable compression directly on CDN edge servers, in which case hello CDN compresses hello files and serve them tooend users, even if they are not compressed by hello origin server.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="14a0b-109">Zmiany konfiguracji sieci CDN w warstwie podjąć pewne toopropagate czas za pośrednictwem sieci hello.</span><span class="sxs-lookup"><span data-stu-id="14a0b-109">CDN configuration changes take some time toopropagate through hello network.</span></span>  <span data-ttu-id="14a0b-110">Aby uzyskać <b>Azure CDN from Akamai</b> profile, propagacji zazwyczaj kończy w obszarze jednej minuty.</span><span class="sxs-lookup"><span data-stu-id="14a0b-110">For <b>Azure CDN from Akamai</b> profiles, propagation usually completes in under one minute.</span></span>  <span data-ttu-id="14a0b-111">Aby uzyskać <b>Azure CDN from Verizon</b> profile, zwykle widoczne zmiany w ciągu 90 minut.</span><span class="sxs-lookup"><span data-stu-id="14a0b-111">For <b>Azure CDN from Verizon</b> profiles, you will usually see your changes apply within 90 minutes.</span></span>  <span data-ttu-id="14a0b-112">Jeśli jest to powitania po raz pierwszy po skonfigurowaniu kompresji dla punktu końcowego CDN, należy rozważyć oczekuje się, że ustawienia kompresji hello zostaną rozpropagowane POP toohello przed rozpoczęciem rozwiązywania toobe 1 – 2 godz.</span><span class="sxs-lookup"><span data-stu-id="14a0b-112">If this is hello first time you've set up compression for your CDN endpoint, you should consider waiting 1-2 hours toobe sure hello compression settings have propagated toohello POPs before troubleshooting</span></span>
> 
> 

## <a name="enabling-compression"></a><span data-ttu-id="14a0b-113">Włączanie kompresji</span><span class="sxs-lookup"><span data-stu-id="14a0b-113">Enabling compression</span></span>
> [!NOTE]
> <span data-ttu-id="14a0b-114">Witaj warstwy standardowa i Premium CDN Podaj hello tę samą funkcjonalność kompresji, ale hello interfejs użytkownika różni się.</span><span class="sxs-lookup"><span data-stu-id="14a0b-114">hello Standard and Premium CDN tiers provide hello same compression functionality, but hello user interface differs.</span></span>  <span data-ttu-id="14a0b-115">Aby uzyskać więcej informacji o różnicach hello warstwy standardowa i Premium usługi CDN, zobacz [Omówienie usługi Azure CDN](cdn-overview.md).</span><span class="sxs-lookup"><span data-stu-id="14a0b-115">For more information about hello differences between Standard and Premium CDN tiers, see [Azure CDN Overview](cdn-overview.md).</span></span>
> 
> 

### <a name="standard-tier"></a><span data-ttu-id="14a0b-116">Warstwa standardowa</span><span class="sxs-lookup"><span data-stu-id="14a0b-116">Standard tier</span></span>
> [!NOTE]
> <span data-ttu-id="14a0b-117">Ta sekcja dotyczy zbyt**Azure CDN Standard from Verizon** i **Azure CDN Standard from Akamai** profilów.</span><span class="sxs-lookup"><span data-stu-id="14a0b-117">This section applies too**Azure CDN Standard from Verizon** and **Azure CDN Standard from Akamai** profiles.</span></span>
> 
> 

1. <span data-ttu-id="14a0b-118">Strony profilu CDN hello kliknij punkt końcowy CDN hello mają toomanage.</span><span class="sxs-lookup"><span data-stu-id="14a0b-118">From hello CDN profile page, click hello CDN endpoint you wish toomanage.</span></span>
   
    ![Punkty końcowe strony profilu CDN](./media/cdn-file-compression/cdn-endpoints.png)
   
    <span data-ttu-id="14a0b-120">zostanie otwarta strona punktu końcowego CDN Hello.</span><span class="sxs-lookup"><span data-stu-id="14a0b-120">hello CDN endpoint page opens.</span></span>
2. <span data-ttu-id="14a0b-121">Kliknij przycisk hello **Konfiguruj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="14a0b-121">Click hello **Configure** button.</span></span>
   
    ![Przycisk Zarządzaj strony profilu CDN](./media/cdn-file-compression/cdn-config-btn.png)
   
    <span data-ttu-id="14a0b-123">zostanie otwarta strona konfiguracji CDN Hello.</span><span class="sxs-lookup"><span data-stu-id="14a0b-123">hello CDN Configuration page opens.</span></span>
3. <span data-ttu-id="14a0b-124">Włącz **kompresji**.</span><span class="sxs-lookup"><span data-stu-id="14a0b-124">Turn on **Compression**.</span></span>
   
    ![Opcje kompresji CDN](./media/cdn-file-compression/cdn-compress-standard.png)
4. <span data-ttu-id="14a0b-126">Użyj typów domyślnych hello lub zmodyfikuj listę hello usuwając lub dodając typów plików.</span><span class="sxs-lookup"><span data-stu-id="14a0b-126">Use hello default types, or modify hello list by removing or adding file types.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="14a0b-127">Czas jest to możliwe, nie zaleca się tooapply toocompressed kompresji, takich jak ZIP, MP3, MP4, JPG itp.</span><span class="sxs-lookup"><span data-stu-id="14a0b-127">While possible, it is not recommended tooapply compression toocompressed formats, such as ZIP, MP3, MP4, JPG, etc.</span></span>
   > 
   > 
5. <span data-ttu-id="14a0b-128">Po wprowadzeniu zmian, kliknij przycisk hello **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="14a0b-128">After making your changes, click hello **Save** button.</span></span>

### <a name="premium-tier"></a><span data-ttu-id="14a0b-129">Warstwa Premium</span><span class="sxs-lookup"><span data-stu-id="14a0b-129">Premium tier</span></span>
> [!NOTE]
> <span data-ttu-id="14a0b-130">Ta sekcja dotyczy zbyt**Azure CDN Premium from Verizon** profilów.</span><span class="sxs-lookup"><span data-stu-id="14a0b-130">This section applies too**Azure CDN Premium from Verizon** profiles.</span></span>
> 
> 

1. <span data-ttu-id="14a0b-131">Ze strony profilu CDN hello, kliknij przycisk hello **Zarządzaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="14a0b-131">From hello CDN profile page, click hello **Manage** button.</span></span>
   
    ![Przycisk Zarządzaj strony profilu CDN](./media/cdn-file-compression/cdn-manage-btn.png)
   
    <span data-ttu-id="14a0b-133">Otwiera portalu zarządzania Hello CDN.</span><span class="sxs-lookup"><span data-stu-id="14a0b-133">hello CDN management portal opens.</span></span>
2. <span data-ttu-id="14a0b-134">Przesuń kursor myszy hello **HTTP dużych** kartę, a następnie przesuń kursor myszy hello **ustawienia pamięci podręcznej** wysuwane okno.</span><span class="sxs-lookup"><span data-stu-id="14a0b-134">Hover over hello **HTTP Large** tab, then hover over hello **Cache Settings** flyout.</span></span>  <span data-ttu-id="14a0b-135">Polecenie **kompresji**.</span><span class="sxs-lookup"><span data-stu-id="14a0b-135">Click on **Compression**.</span></span>

    ![Wybieranie pliku kompresji](./media/cdn-file-compression/cdn-compress-select.png)
   
    <span data-ttu-id="14a0b-137">Opcje kompresji są wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="14a0b-137">Compression options are displayed.</span></span>
   
    ![Kompresja plików](./media/cdn-file-compression/cdn-compress-files.png)
3. <span data-ttu-id="14a0b-139">Włącz kompresję, klikając hello **włączyć kompresji,** przycisk radiowy.</span><span class="sxs-lookup"><span data-stu-id="14a0b-139">Enable compression by clicking hello **Compression Enabled** radio button.</span></span>  <span data-ttu-id="14a0b-140">Wprowadź typy MIME hello mają toocompress jako listę rozdzielanych przecinkami (bez spacji) w hello **typów plików** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="14a0b-140">Enter hello MIME types you wish toocompress as a comma-delimited list (no spaces) in hello **File Types** textbox.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="14a0b-141">Czas jest to możliwe, nie zaleca się tooapply toocompressed kompresji, takich jak ZIP, MP3, MP4, JPG itp.</span><span class="sxs-lookup"><span data-stu-id="14a0b-141">While possible, it is not recommended tooapply compression toocompressed formats, such as ZIP, MP3, MP4, JPG, etc.</span></span> 
   > 
   > 
4. <span data-ttu-id="14a0b-142">Po wprowadzeniu zmian, kliknij przycisk hello **aktualizacji** przycisku.</span><span class="sxs-lookup"><span data-stu-id="14a0b-142">After making your changes, click hello **Update** button.</span></span>

## <a name="compression-rules"></a><span data-ttu-id="14a0b-143">Reguły kompresji</span><span class="sxs-lookup"><span data-stu-id="14a0b-143">Compression rules</span></span>
<span data-ttu-id="14a0b-144">Te tabele zawierają opis usługi Azure CDN kompresji zachowanie dla każdego scenariusza.</span><span class="sxs-lookup"><span data-stu-id="14a0b-144">These tables describe Azure CDN compression behavior for every scenario.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="14a0b-145">Aby uzyskać **Azure CDN from Verizon** są kompresowane tylko odpowiednich plików (Standard i Premium).</span><span class="sxs-lookup"><span data-stu-id="14a0b-145">For **Azure CDN from Verizon** (Standard and Premium), only eligible files are compressed.</span></span>  <span data-ttu-id="14a0b-146">toobe kwalifikuje się do kompresji, pliku, musi:</span><span class="sxs-lookup"><span data-stu-id="14a0b-146">toobe eligible for compression, a file must:</span></span>
> 
> * <span data-ttu-id="14a0b-147">Być większa niż 128 bajtów.</span><span class="sxs-lookup"><span data-stu-id="14a0b-147">Be larger than 128 bytes.</span></span>
> * <span data-ttu-id="14a0b-148">Być mniejszy niż 1 MB.</span><span class="sxs-lookup"><span data-stu-id="14a0b-148">Be smaller than 1 MB.</span></span>
> 
> <span data-ttu-id="14a0b-149">Aby uzyskać **Azure CDN from Akamai**, wszystkie pliki kwalifikują się do kompresji.</span><span class="sxs-lookup"><span data-stu-id="14a0b-149">For **Azure CDN from Akamai**, all files are eligible for compression.</span></span>
> 
> <span data-ttu-id="14a0b-150">Dla wszystkich produktów Azure CDN, plik musi być typ MIME, który został [skonfigurowane kompresji](#enabling-compression).</span><span class="sxs-lookup"><span data-stu-id="14a0b-150">For all Azure CDN products, a file must be a MIME type that has been [configured for compression](#enabling-compression).</span></span>
> 
> <span data-ttu-id="14a0b-151">**Usługi Azure CDN from Verizon** profile pomocy technicznej (Standard i Premium) **gzip** (GNU zip), **deflate**, **bzip2**, lub **br** kodowania (Brotli).</span><span class="sxs-lookup"><span data-stu-id="14a0b-151">**Azure CDN from Verizon** profiles (Standard and Premium) support **gzip** (GNU zip), **deflate**, **bzip2**, or  **br** (Brotli) encoding.</span></span> <span data-ttu-id="14a0b-152">Brotli kodowania, kompresji hello odbywa się tylko na powitania krawędzi.</span><span class="sxs-lookup"><span data-stu-id="14a0b-152">For Brotli encoding, hello compression is done only at hello edge.</span></span> <span data-ttu-id="14a0b-153">przeglądarka klienta Hello musi wysłać żądanie hello Brotli kodowania i zasobów skompresowany hello musi skompresowane po stronie źródła hello najpierw.</span><span class="sxs-lookup"><span data-stu-id="14a0b-153">hello client/browser must send hello request for Brotli encoding and hello compressed asset must have been compressed on hello origin side first.</span></span> 
>
><span data-ttu-id="14a0b-154">**Azure CDN from Akamai** profile obsługują tylko **gzip** kodowania.</span><span class="sxs-lookup"><span data-stu-id="14a0b-154">**Azure CDN from Akamai** profiles support only **gzip** encoding.</span></span>
> 
> <span data-ttu-id="14a0b-155">**Azure CDN from Akamai** punkty końcowe zawsze żądania **gzip** pliki pochodzenia hello, niezależnie od tego, żądania klienta hello algorytmem.</span><span class="sxs-lookup"><span data-stu-id="14a0b-155">**Azure CDN from Akamai** endpoints always request **gzip** encoded files from hello origin, regardless of hello client request.</span></span> 

### <a name="compression-disabled-or-file-is-ineligible-for-compression"></a><span data-ttu-id="14a0b-156">Kompresja wyłączona lub plik nie kwalifikuje się do kompresji</span><span class="sxs-lookup"><span data-stu-id="14a0b-156">Compression disabled or file is ineligible for compression</span></span>
| <span data-ttu-id="14a0b-157">Żądany format klienta (za pośrednictwem nagłówka Accept-Encoding)</span><span class="sxs-lookup"><span data-stu-id="14a0b-157">Client requested format (via Accept-Encoding header)</span></span> | <span data-ttu-id="14a0b-158">Format pliku pamięci podręcznej</span><span class="sxs-lookup"><span data-stu-id="14a0b-158">Cached file format</span></span> | <span data-ttu-id="14a0b-159">Klient toohello odpowiedzi CDN</span><span class="sxs-lookup"><span data-stu-id="14a0b-159">CDN response toohello client</span></span> | <span data-ttu-id="14a0b-160">Uwagi</span><span class="sxs-lookup"><span data-stu-id="14a0b-160">Notes</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="14a0b-161">Skompresowane</span><span class="sxs-lookup"><span data-stu-id="14a0b-161">Compressed</span></span> |<span data-ttu-id="14a0b-162">Skompresowane</span><span class="sxs-lookup"><span data-stu-id="14a0b-162">Compressed</span></span> |<span data-ttu-id="14a0b-163">Skompresowane</span><span class="sxs-lookup"><span data-stu-id="14a0b-163">Compressed</span></span> | |
| <span data-ttu-id="14a0b-164">Skompresowane</span><span class="sxs-lookup"><span data-stu-id="14a0b-164">Compressed</span></span> |<span data-ttu-id="14a0b-165">Nieskompresowanych</span><span class="sxs-lookup"><span data-stu-id="14a0b-165">Uncompressed</span></span> |<span data-ttu-id="14a0b-166">Nieskompresowanych</span><span class="sxs-lookup"><span data-stu-id="14a0b-166">Uncompressed</span></span> | |
| <span data-ttu-id="14a0b-167">Skompresowane</span><span class="sxs-lookup"><span data-stu-id="14a0b-167">Compressed</span></span> |<span data-ttu-id="14a0b-168">Nie w pamięci podręcznej</span><span class="sxs-lookup"><span data-stu-id="14a0b-168">Not cached</span></span> |<span data-ttu-id="14a0b-169">Skompresowane lub nieskompresowane</span><span class="sxs-lookup"><span data-stu-id="14a0b-169">Compressed or Uncompressed</span></span> |<span data-ttu-id="14a0b-170">Zależy od źródła odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="14a0b-170">Depends on origin response</span></span> |
| <span data-ttu-id="14a0b-171">Nieskompresowanych</span><span class="sxs-lookup"><span data-stu-id="14a0b-171">Uncompressed</span></span> |<span data-ttu-id="14a0b-172">Skompresowane</span><span class="sxs-lookup"><span data-stu-id="14a0b-172">Compressed</span></span> |<span data-ttu-id="14a0b-173">Nieskompresowanych</span><span class="sxs-lookup"><span data-stu-id="14a0b-173">Uncompressed</span></span> | |
| <span data-ttu-id="14a0b-174">Nieskompresowanych</span><span class="sxs-lookup"><span data-stu-id="14a0b-174">Uncompressed</span></span> |<span data-ttu-id="14a0b-175">Nieskompresowanych</span><span class="sxs-lookup"><span data-stu-id="14a0b-175">Uncompressed</span></span> |<span data-ttu-id="14a0b-176">Nieskompresowanych</span><span class="sxs-lookup"><span data-stu-id="14a0b-176">Uncompressed</span></span> | |
| <span data-ttu-id="14a0b-177">Nieskompresowanych</span><span class="sxs-lookup"><span data-stu-id="14a0b-177">Uncompressed</span></span> |<span data-ttu-id="14a0b-178">Nie w pamięci podręcznej</span><span class="sxs-lookup"><span data-stu-id="14a0b-178">Not cached</span></span> |<span data-ttu-id="14a0b-179">Nieskompresowanych</span><span class="sxs-lookup"><span data-stu-id="14a0b-179">Uncompressed</span></span> | |

### <a name="compression-enabled-and-file-is-eligible-for-compression"></a><span data-ttu-id="14a0b-180">Kompresja włączona i pliku nie kwalifikuje się do kompresji</span><span class="sxs-lookup"><span data-stu-id="14a0b-180">Compression enabled and file is eligible for compression</span></span>
| <span data-ttu-id="14a0b-181">Żądany format klienta (za pośrednictwem nagłówka Accept-Encoding)</span><span class="sxs-lookup"><span data-stu-id="14a0b-181">Client requested format (via Accept-Encoding header)</span></span> | <span data-ttu-id="14a0b-182">Format pliku pamięci podręcznej</span><span class="sxs-lookup"><span data-stu-id="14a0b-182">Cached file format</span></span> | <span data-ttu-id="14a0b-183">Klient toohello odpowiedzi CDN</span><span class="sxs-lookup"><span data-stu-id="14a0b-183">CDN response toohello client</span></span> | <span data-ttu-id="14a0b-184">Uwagi</span><span class="sxs-lookup"><span data-stu-id="14a0b-184">Notes</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="14a0b-185">Skompresowane</span><span class="sxs-lookup"><span data-stu-id="14a0b-185">Compressed</span></span> |<span data-ttu-id="14a0b-186">Skompresowane</span><span class="sxs-lookup"><span data-stu-id="14a0b-186">Compressed</span></span> |<span data-ttu-id="14a0b-187">Skompresowane</span><span class="sxs-lookup"><span data-stu-id="14a0b-187">Compressed</span></span> |<span data-ttu-id="14a0b-188">Transcodes CDN pomiędzy obsługiwanych formatów</span><span class="sxs-lookup"><span data-stu-id="14a0b-188">CDN transcodes between supported formats</span></span> |
| <span data-ttu-id="14a0b-189">Skompresowane</span><span class="sxs-lookup"><span data-stu-id="14a0b-189">Compressed</span></span> |<span data-ttu-id="14a0b-190">Nieskompresowanych</span><span class="sxs-lookup"><span data-stu-id="14a0b-190">Uncompressed</span></span> |<span data-ttu-id="14a0b-191">Skompresowane</span><span class="sxs-lookup"><span data-stu-id="14a0b-191">Compressed</span></span> |<span data-ttu-id="14a0b-192">CDN wykonuje kompresji</span><span class="sxs-lookup"><span data-stu-id="14a0b-192">CDN performs compression</span></span> |
| <span data-ttu-id="14a0b-193">Skompresowane</span><span class="sxs-lookup"><span data-stu-id="14a0b-193">Compressed</span></span> |<span data-ttu-id="14a0b-194">Nie w pamięci podręcznej</span><span class="sxs-lookup"><span data-stu-id="14a0b-194">Not cached</span></span> |<span data-ttu-id="14a0b-195">Skompresowane</span><span class="sxs-lookup"><span data-stu-id="14a0b-195">Compressed</span></span> |<span data-ttu-id="14a0b-196">Jeśli punkt początkowy zwraca nieskompresowanych, CDN wykonuje kompresji.</span><span class="sxs-lookup"><span data-stu-id="14a0b-196">CDN performs compression if origin returns uncompressed.</span></span>  <span data-ttu-id="14a0b-197">**Usługi Azure CDN from Verizon** przekazuje hello nieskompresowanego pliku na pierwsze Żądanie hello, a następnie kompresuje i pamięci podręczne hello pliku dla kolejnych żądań.</span><span class="sxs-lookup"><span data-stu-id="14a0b-197">**Azure CDN from Verizon** passes hello uncompressed file on hello first request and then compresses and caches hello file for subsequent requests.</span></span>  <span data-ttu-id="14a0b-198">Pliki z `Cache-Control: no-cache` nagłówka nigdy nie zostanie skompresowany.</span><span class="sxs-lookup"><span data-stu-id="14a0b-198">Files with `Cache-Control: no-cache` header will never be compressed.</span></span> |
| <span data-ttu-id="14a0b-199">Nieskompresowanych</span><span class="sxs-lookup"><span data-stu-id="14a0b-199">Uncompressed</span></span> |<span data-ttu-id="14a0b-200">Skompresowane</span><span class="sxs-lookup"><span data-stu-id="14a0b-200">Compressed</span></span> |<span data-ttu-id="14a0b-201">Nieskompresowanych</span><span class="sxs-lookup"><span data-stu-id="14a0b-201">Uncompressed</span></span> |<span data-ttu-id="14a0b-202">Dekompresja wykonuje CDN</span><span class="sxs-lookup"><span data-stu-id="14a0b-202">CDN performs decompression</span></span> |
| <span data-ttu-id="14a0b-203">Nieskompresowanych</span><span class="sxs-lookup"><span data-stu-id="14a0b-203">Uncompressed</span></span> |<span data-ttu-id="14a0b-204">Nieskompresowanych</span><span class="sxs-lookup"><span data-stu-id="14a0b-204">Uncompressed</span></span> |<span data-ttu-id="14a0b-205">Nieskompresowanych</span><span class="sxs-lookup"><span data-stu-id="14a0b-205">Uncompressed</span></span> | |
| <span data-ttu-id="14a0b-206">Nieskompresowanych</span><span class="sxs-lookup"><span data-stu-id="14a0b-206">Uncompressed</span></span> |<span data-ttu-id="14a0b-207">Nie w pamięci podręcznej</span><span class="sxs-lookup"><span data-stu-id="14a0b-207">Not cached</span></span> |<span data-ttu-id="14a0b-208">Nieskompresowanych</span><span class="sxs-lookup"><span data-stu-id="14a0b-208">Uncompressed</span></span> | |

## <a name="media-services-cdn-compression"></a><span data-ttu-id="14a0b-209">Kompresja CDN usługi multimediów</span><span class="sxs-lookup"><span data-stu-id="14a0b-209">Media Services CDN Compression</span></span>
<span data-ttu-id="14a0b-210">Usługi multimediów w sieci CDN włączona punktów końcowych przesyłania strumieniowego, kompresji jest domyślnie włączona dla hello następujące typy zawartości: application/vnd.ms-sstr + xml, application/dash+xml,application/vnd.apple.mpegurl, aplikacji/f4m + xml.</span><span class="sxs-lookup"><span data-stu-id="14a0b-210">For Media Services CDN enabled streaming endpoints, compression is enabled by default for hello following content types: application/vnd.ms-sstr+xml, application/dash+xml,application/vnd.apple.mpegurl, application/f4m+xml.</span></span> <span data-ttu-id="14a0b-211">Użytkownik nie Włączanie/wyłączanie kompresji hello wymienionych typów za pomocą hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="14a0b-211">You cannot enable/disable compression for hello mentioned types using hello Azure portal.</span></span>  

## <a name="see-also"></a><span data-ttu-id="14a0b-212">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="14a0b-212">See also</span></span>
* [<span data-ttu-id="14a0b-213">Rozwiązywanie problemów związanych z kompresją pliku CDN</span><span class="sxs-lookup"><span data-stu-id="14a0b-213">Troubleshooting CDN file compression</span></span>](cdn-troubleshoot-compression.md)    

