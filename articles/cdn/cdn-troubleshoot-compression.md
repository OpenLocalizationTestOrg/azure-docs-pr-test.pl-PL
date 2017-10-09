---
title: "aaaTroubleshooting kompresji plików w usłudze Azure CDN | Dokumentacja firmy Microsoft"
description: "Rozwiązywanie problemów z kompresji plików Azure CDN."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: a6624e65-1a77-4486-b473-8d720ce28f8b
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: f00b98beaf6b3b3cd30108ece65a8191edc06ff5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-cdn-file-compression"></a><span data-ttu-id="bb7c4-103">Rozwiązywanie problemów związanych z kompresją pliku CDN</span><span class="sxs-lookup"><span data-stu-id="bb7c4-103">Troubleshooting CDN file compression</span></span>
<span data-ttu-id="bb7c4-104">Ten artykuł ułatwia rozwiązywanie problemów z [kompresji plików CDN](cdn-improve-performance.md).</span><span class="sxs-lookup"><span data-stu-id="bb7c4-104">This article helps you troubleshoot issues with [CDN file compression](cdn-improve-performance.md).</span></span>

<span data-ttu-id="bb7c4-105">Jeśli potrzebujesz więcej pomocy w dowolnym momencie, w tym artykule, możesz skontaktować się hello ekspertów platformy Azure na [hello MSDN Azure i hello przepełnienie stosu fora](https://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="bb7c4-105">If you need more help at any point in this article, you can contact hello Azure experts on [hello MSDN Azure and hello Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="bb7c4-106">Alternatywnie można również pliku zdarzenia pomocy technicznej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="bb7c4-106">Alternatively, you can also file an Azure support incident.</span></span> <span data-ttu-id="bb7c4-107">Przejdź toohello [witrynę pomocy technicznej platformy Azure](https://azure.microsoft.com/support/options/) i kliknij przycisk **Get Support**.</span><span class="sxs-lookup"><span data-stu-id="bb7c4-107">Go toohello [Azure Support site](https://azure.microsoft.com/support/options/) and click **Get Support**.</span></span>

## <a name="symptom"></a><span data-ttu-id="bb7c4-108">Objaw</span><span class="sxs-lookup"><span data-stu-id="bb7c4-108">Symptom</span></span>
<span data-ttu-id="bb7c4-109">Kompresja dla punktu końcowego jest włączona, ale pliki są zwracane nieskompresowane.</span><span class="sxs-lookup"><span data-stu-id="bb7c4-109">Compression for your endpoint is enabled, but files are being returned uncompressed.</span></span>

> [!TIP]
> <span data-ttu-id="bb7c4-110">toocheck czy pliki zostały zwrócone skompresowany, potrzebujesz toouse, takich jak narzędzie [Fiddler](http://www.telerik.com/fiddler) lub przeglądarki [narzędzia dla deweloperów](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/).</span><span class="sxs-lookup"><span data-stu-id="bb7c4-110">toocheck whether your files are being returned compressed, you need toouse a tool like [Fiddler](http://www.telerik.com/fiddler) or your browser's [developer tools](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/).</span></span>  <span data-ttu-id="bb7c4-111">Nagłówki odpowiedzi hello HTTP wyboru zwrócone z sieci CDN pamięci podręcznej zawartości.</span><span class="sxs-lookup"><span data-stu-id="bb7c4-111">Check hello HTTP response headers returned with your cached CDN content.</span></span>  <span data-ttu-id="bb7c4-112">Jeśli istnieje nagłówek o nazwie `Content-Encoding` o wartości **gzip**, **bzip2**, lub **deflate**, jest skompresowana zawartość.</span><span class="sxs-lookup"><span data-stu-id="bb7c4-112">If there is a header named `Content-Encoding` with a value of **gzip**, **bzip2**, or **deflate**, your content is compressed.</span></span>
> 
> ![Kodowanie zawartości nagłówka](./media/cdn-troubleshoot-compression/cdn-content-header.png)
> 
> 

## <a name="cause"></a><span data-ttu-id="bb7c4-114">Przyczyna</span><span class="sxs-lookup"><span data-stu-id="bb7c4-114">Cause</span></span>
<span data-ttu-id="bb7c4-115">Istnieje kilka możliwych przyczyn, w tym:</span><span class="sxs-lookup"><span data-stu-id="bb7c4-115">There are several possible causes, including:</span></span>

* <span data-ttu-id="bb7c4-116">Witaj zażądał zawartości nie jest uprawniony do kompresji.</span><span class="sxs-lookup"><span data-stu-id="bb7c4-116">hello requested content is not eligible for compression.</span></span>
* <span data-ttu-id="bb7c4-117">Nie włączono kompresję hello żądany typ pliku.</span><span class="sxs-lookup"><span data-stu-id="bb7c4-117">Compression is not enabled for hello requested file type.</span></span>
* <span data-ttu-id="bb7c4-118">Hello żądania HTTP nie zawiera nagłówka zażądał typu prawidłowy kompresji.</span><span class="sxs-lookup"><span data-stu-id="bb7c4-118">hello HTTP request did not include a header requesting a valid compression type.</span></span>

## <a name="troubleshooting-steps"></a><span data-ttu-id="bb7c4-119">Kroki rozwiązywania problemów</span><span class="sxs-lookup"><span data-stu-id="bb7c4-119">Troubleshooting steps</span></span>
> [!TIP]
> <span data-ttu-id="bb7c4-120">Podobnie jak w przypadku wdrażania nowych punktów końcowych, zmiany w konfiguracji sieci CDN zająć niektórych toopropagate czas za pośrednictwem sieci hello.</span><span class="sxs-lookup"><span data-stu-id="bb7c4-120">As with deploying new endpoints, CDN configuration changes take some time toopropagate through hello network.</span></span>  <span data-ttu-id="bb7c4-121">Zwykle zmiany zostaną zastosowane w ciągu 90 minut.</span><span class="sxs-lookup"><span data-stu-id="bb7c4-121">Usually, changes are applied within 90 minutes.</span></span>  <span data-ttu-id="bb7c4-122">Jeśli jest to powitania po skonfigurowaniu kompresji dla punktu końcowego CDN po raz pierwszy, należy rozważyć oczekuje się, że ustawienia kompresji hello zostaną rozpropagowane POP toohello toobe 1 – 2 godz.</span><span class="sxs-lookup"><span data-stu-id="bb7c4-122">If this is hello first time you've set up compression for your CDN endpoint, you should consider waiting 1-2 hours toobe sure hello compression settings have propagated toohello POPs.</span></span> 
> 
> 

### <a name="verify-hello-request"></a><span data-ttu-id="bb7c4-123">Sprawdź hello żądania</span><span class="sxs-lookup"><span data-stu-id="bb7c4-123">Verify hello request</span></span>
<span data-ttu-id="bb7c4-124">Najpierw należy wykonać związane z poprawnością szybkie sprawdzenie hello żądania.</span><span class="sxs-lookup"><span data-stu-id="bb7c4-124">First, we should do a quick sanity check on hello request.</span></span>  <span data-ttu-id="bb7c4-125">Można użyć przeglądarki [narzędzia dla deweloperów](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/) tooview hello żądań wysyłanych.</span><span class="sxs-lookup"><span data-stu-id="bb7c4-125">You can use your browser's [developer tools](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/) tooview hello requests being made.</span></span>

* <span data-ttu-id="bb7c4-126">Sprawdź wysyłanie żądania hello tooyour adres URL punktu końcowego, `<endpointname>.azureedge.net`, a nie źródła.</span><span class="sxs-lookup"><span data-stu-id="bb7c4-126">Verify hello request is being sent tooyour endpoint URL, `<endpointname>.azureedge.net`, and not your origin.</span></span>
* <span data-ttu-id="bb7c4-127">Sprawdź Żądanie hello zawiera **Accept-Encoding** nagłówka i hello wartość dla nagłówka zawiera **gzip**, **deflate**, lub **bzip2** .</span><span class="sxs-lookup"><span data-stu-id="bb7c4-127">Verify hello request contains an **Accept-Encoding** header, and hello value for that header contains **gzip**, **deflate**, or **bzip2**.</span></span>

> [!NOTE]
> <span data-ttu-id="bb7c4-128">**Azure CDN from Akamai** profile obsługują tylko **gzip** kodowania.</span><span class="sxs-lookup"><span data-stu-id="bb7c4-128">**Azure CDN from Akamai** profiles only support **gzip** encoding.</span></span>
> 
> 

![Nagłówki żądania CDN](./media/cdn-troubleshoot-compression/cdn-request-headers.png)

### <a name="verify-compression-settings-standard-cdn-profile"></a><span data-ttu-id="bb7c4-130">Sprawdź ustawienia kompresji (profilu sieci CDN w warstwie standardowa)</span><span class="sxs-lookup"><span data-stu-id="bb7c4-130">Verify compression settings (Standard CDN profile)</span></span>
> [!NOTE]
> <span data-ttu-id="bb7c4-131">Ten krok ma zastosowanie tylko, jeśli profil CDN jest **Azure CDN Standard from Verizon** lub **Azure CDN Standard from Akamai** profilu.</span><span class="sxs-lookup"><span data-stu-id="bb7c4-131">This step only applies if your CDN profile is an **Azure CDN Standard from Verizon** or **Azure CDN Standard from Akamai** profile.</span></span> 
> 
> 

<span data-ttu-id="bb7c4-132">Przejdź do punktu końcowego tooyour w hello [portalu Azure](https://portal.azure.com) i kliknij przycisk hello **Konfiguruj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="bb7c4-132">Navigate tooyour endpoint in hello [Azure portal](https://portal.azure.com) and click hello **Configure** button.</span></span>

* <span data-ttu-id="bb7c4-133">Sprawdź, czy kompresja jest włączona.</span><span class="sxs-lookup"><span data-stu-id="bb7c4-133">Verify compression is enabled.</span></span>
* <span data-ttu-id="bb7c4-134">Sprawdź hello typ MIME dla zawartości toobe skompresowane jest uwzględniona w hello listy formatów skompresowany hello.</span><span class="sxs-lookup"><span data-stu-id="bb7c4-134">Verify hello MIME type for hello content toobe compressed is included in hello list of compressed formats.</span></span>

![Ustawienia kompresji CDN](./media/cdn-troubleshoot-compression/cdn-compression-settings.png)

### <a name="verify-compression-settings-premium-cdn-profile"></a><span data-ttu-id="bb7c4-136">Sprawdź ustawienia kompresji (profilu sieci CDN w warstwie Premium)</span><span class="sxs-lookup"><span data-stu-id="bb7c4-136">Verify compression settings (Premium CDN profile)</span></span>
> [!NOTE]
> <span data-ttu-id="bb7c4-137">Ten krok ma zastosowanie tylko, jeśli profil CDN jest **Azure CDN Premium from Verizon** profilu.</span><span class="sxs-lookup"><span data-stu-id="bb7c4-137">This step only applies if your CDN profile is an **Azure CDN Premium from Verizon** profile.</span></span>
> 
> 

<span data-ttu-id="bb7c4-138">Przejdź do punktu końcowego tooyour w hello [portalu Azure](https://portal.azure.com) i kliknij przycisk hello **Zarządzaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="bb7c4-138">Navigate tooyour endpoint in hello [Azure portal](https://portal.azure.com) and click hello **Manage** button.</span></span>  <span data-ttu-id="bb7c4-139">zostanie otwarta Hello portalu dodatkowym.</span><span class="sxs-lookup"><span data-stu-id="bb7c4-139">hello supplemental portal will open.</span></span>  <span data-ttu-id="bb7c4-140">Przesuń kursor myszy hello **HTTP dużych** kartę, a następnie przesuń kursor myszy hello **ustawienia pamięci podręcznej** wysuwane okno.</span><span class="sxs-lookup"><span data-stu-id="bb7c4-140">Hover over hello **HTTP Large** tab, then hover over hello **Cache Settings** flyout.</span></span>  <span data-ttu-id="bb7c4-141">Kliknij przycisk **kompresji**.</span><span class="sxs-lookup"><span data-stu-id="bb7c4-141">Click **Compression**.</span></span> 

* <span data-ttu-id="bb7c4-142">Sprawdź, czy kompresja jest włączona.</span><span class="sxs-lookup"><span data-stu-id="bb7c4-142">Verify compression is enabled.</span></span>
* <span data-ttu-id="bb7c4-143">Sprawdź hello **typów plików** lista zawiera listę rozdzielanych przecinkami (bez spacji) typów MIME.</span><span class="sxs-lookup"><span data-stu-id="bb7c4-143">Verify hello **File Types** list contains a comma-separated list (no spaces) of MIME types.</span></span>
* <span data-ttu-id="bb7c4-144">Sprawdź hello typ MIME dla zawartości toobe skompresowane jest uwzględniona w hello listy formatów skompresowany hello.</span><span class="sxs-lookup"><span data-stu-id="bb7c4-144">Verify hello MIME type for hello content toobe compressed is included in hello list of compressed formats.</span></span>

![Ustawienia kompresji sieci CDN w warstwie premium](./media/cdn-troubleshoot-compression/cdn-compression-settings-premium.png)

### <a name="verify-hello-content-is-cached"></a><span data-ttu-id="bb7c4-146">Sprawdź, czy hello zawartość jest buforowana</span><span class="sxs-lookup"><span data-stu-id="bb7c4-146">Verify hello content is cached</span></span>
> [!NOTE]
> <span data-ttu-id="bb7c4-147">Ten krok ma zastosowanie tylko, jeśli profil CDN jest **Azure CDN from Verizon** profilu (standardowy lub Premium).</span><span class="sxs-lookup"><span data-stu-id="bb7c4-147">This step only applies if your CDN profile is an **Azure CDN from Verizon** profile (Standard or Premium).</span></span>
> 
> 

<span data-ttu-id="bb7c4-148">Przy użyciu narzędzia dla deweloperów w przeglądarce, sprawdź, czy hello odpowiedzi nagłówki tooensure hello plików jest buforowana w regionie hello, w którym jest on wymagany.</span><span class="sxs-lookup"><span data-stu-id="bb7c4-148">Using your browser's developer tools, check hello response headers tooensure hello file is cached in hello region where it is being requested.</span></span>

* <span data-ttu-id="bb7c4-149">Sprawdź hello **serwera** nagłówka odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="bb7c4-149">Check hello **Server** response header.</span></span>  <span data-ttu-id="bb7c4-150">Nagłówek Hello musi mieć hello format **platformy (serwer protokołu POP/ID)**, jak pokazano w hello poniższy przykład.</span><span class="sxs-lookup"><span data-stu-id="bb7c4-150">hello header should have hello format **Platform (POP/Server ID)**, as seen in hello following example.</span></span>
* <span data-ttu-id="bb7c4-151">Sprawdź hello **pamięci podręcznej X** nagłówka odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="bb7c4-151">Check hello **X-Cache** response header.</span></span>  <span data-ttu-id="bb7c4-152">należy odczytać nagłówka Hello **TRAFIEŃ**.</span><span class="sxs-lookup"><span data-stu-id="bb7c4-152">hello header should read **HIT**.</span></span>  

![Nagłówki odpowiedzi CDN](./media/cdn-troubleshoot-compression/cdn-response-headers.png)

### <a name="verify-hello-file-meets-hello-size-requirements"></a><span data-ttu-id="bb7c4-154">Sprawdź, czy plik hello spełnia wymagania dotyczące rozmiaru hello</span><span class="sxs-lookup"><span data-stu-id="bb7c4-154">Verify hello file meets hello size requirements</span></span>
> [!NOTE]
> <span data-ttu-id="bb7c4-155">Ten krok ma zastosowanie tylko, jeśli profil CDN jest **Azure CDN from Verizon** profilu (standardowy lub Premium).</span><span class="sxs-lookup"><span data-stu-id="bb7c4-155">This step only applies if your CDN profile is an **Azure CDN from Verizon** profile (Standard or Premium).</span></span>
> 
> 

<span data-ttu-id="bb7c4-156">toobe kwalifikuje się do kompresji, plik musi spełniać następujące wymagania dotyczące rozmiaru hello:</span><span class="sxs-lookup"><span data-stu-id="bb7c4-156">toobe eligible for compression, a file must meet hello following size requirements:</span></span>

* <span data-ttu-id="bb7c4-157">Większe niż 128 bajtów.</span><span class="sxs-lookup"><span data-stu-id="bb7c4-157">Larger than 128 bytes.</span></span>
* <span data-ttu-id="bb7c4-158">Mniejszy niż 1 MB.</span><span class="sxs-lookup"><span data-stu-id="bb7c4-158">Smaller than 1 MB.</span></span>

### <a name="check-hello-request-at-hello-origin-server-for-a-via-header"></a><span data-ttu-id="bb7c4-159">Sprawdzanie hello żądania na serwerze pochodzenia hello **za pośrednictwem** nagłówka</span><span class="sxs-lookup"><span data-stu-id="bb7c4-159">Check hello request at hello origin server for a **Via** header</span></span>
<span data-ttu-id="bb7c4-160">Witaj **za pośrednictwem** wskazuje nagłówka HTTP serwera sieci web toohello hello żądania jest przekazywany przez serwer proxy.</span><span class="sxs-lookup"><span data-stu-id="bb7c4-160">hello **Via** HTTP header indicates toohello web server that hello request is being passed by a proxy server.</span></span>  <span data-ttu-id="bb7c4-161">Serwery sieci web Microsoft IIS domyślnie nie Kompresuj odpowiedzi, gdy Żądanie hello zawiera **za pośrednictwem** nagłówka.</span><span class="sxs-lookup"><span data-stu-id="bb7c4-161">Microsoft IIS web servers by default do not compress responses when hello request contains a **Via** header.</span></span>  <span data-ttu-id="bb7c4-162">toooverride to zachowanie, wykonaj następujące hello:</span><span class="sxs-lookup"><span data-stu-id="bb7c4-162">toooverride this behavior, perform hello following:</span></span>

* <span data-ttu-id="bb7c4-163">**IIS 6**: [ustawić HcNoCompressionForProxies = "FALSE" hello właściwości metabazy usług IIS](https://msdn.microsoft.com/library/ms525390.aspx)</span><span class="sxs-lookup"><span data-stu-id="bb7c4-163">**IIS 6**: [Set HcNoCompressionForProxies="FALSE" in hello IIS Metabase properties](https://msdn.microsoft.com/library/ms525390.aspx)</span></span>
* <span data-ttu-id="bb7c4-164">**Usługi IIS 7 i nowsze**: [wartość **noCompressionForHttp10** i **noCompressionForProxies** tooFalse w konfiguracji serwera hello](http://www.iis.net/configreference/system.webserver/httpcompression)</span><span class="sxs-lookup"><span data-stu-id="bb7c4-164">**IIS 7 and up**: [Set both **noCompressionForHttp10** and **noCompressionForProxies** tooFalse in hello server configuration](http://www.iis.net/configreference/system.webserver/httpcompression)</span></span>

