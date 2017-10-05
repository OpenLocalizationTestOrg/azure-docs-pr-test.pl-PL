---
title: "Rozwiązywanie problemów z kompresji plików w usłudze Azure CDN | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 5ef8a8262eb40aa827161764f03a63d031e43273
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-cdn-file-compression"></a><span data-ttu-id="a3f7d-103">Rozwiązywanie problemów związanych z kompresją pliku CDN</span><span class="sxs-lookup"><span data-stu-id="a3f7d-103">Troubleshooting CDN file compression</span></span>
<span data-ttu-id="a3f7d-104">Ten artykuł ułatwia rozwiązywanie problemów z [kompresji plików CDN](cdn-improve-performance.md).</span><span class="sxs-lookup"><span data-stu-id="a3f7d-104">This article helps you troubleshoot issues with [CDN file compression](cdn-improve-performance.md).</span></span>

<span data-ttu-id="a3f7d-105">Jeśli potrzebujesz więcej pomocy w dowolnym momencie, w tym artykule, możesz skontaktować się ekspertów platformy Azure na [MSDN Azure i fora przepełnienie stosu](https://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="a3f7d-105">If you need more help at any point in this article, you can contact the Azure experts on [the MSDN Azure and the Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="a3f7d-106">Alternatywnie można również pliku zdarzenia pomocy technicznej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="a3f7d-106">Alternatively, you can also file an Azure support incident.</span></span> <span data-ttu-id="a3f7d-107">Przejdź do [witrynę pomocy technicznej platformy Azure](https://azure.microsoft.com/support/options/) i kliknij przycisk **Get Support**.</span><span class="sxs-lookup"><span data-stu-id="a3f7d-107">Go to the [Azure Support site](https://azure.microsoft.com/support/options/) and click **Get Support**.</span></span>

## <a name="symptom"></a><span data-ttu-id="a3f7d-108">Objaw</span><span class="sxs-lookup"><span data-stu-id="a3f7d-108">Symptom</span></span>
<span data-ttu-id="a3f7d-109">Kompresja dla punktu końcowego jest włączona, ale pliki są zwracane nieskompresowane.</span><span class="sxs-lookup"><span data-stu-id="a3f7d-109">Compression for your endpoint is enabled, but files are being returned uncompressed.</span></span>

> [!TIP]
> <span data-ttu-id="a3f7d-110">Aby sprawdzić, czy pliki zostały zwrócone skompresowany, należy użyć narzędzia, takiego jak [Fiddler](http://www.telerik.com/fiddler) lub przeglądarki [narzędzia dla deweloperów](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/).</span><span class="sxs-lookup"><span data-stu-id="a3f7d-110">To check whether your files are being returned compressed, you need to use a tool like [Fiddler](http://www.telerik.com/fiddler) or your browser's [developer tools](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/).</span></span>  <span data-ttu-id="a3f7d-111">Nagłówki odpowiedzi HTTP wyboru zwrócone z sieci CDN pamięci podręcznej zawartości.</span><span class="sxs-lookup"><span data-stu-id="a3f7d-111">Check the HTTP response headers returned with your cached CDN content.</span></span>  <span data-ttu-id="a3f7d-112">Jeśli istnieje nagłówek o nazwie `Content-Encoding` o wartości **gzip**, **bzip2**, lub **deflate**, jest skompresowana zawartość.</span><span class="sxs-lookup"><span data-stu-id="a3f7d-112">If there is a header named `Content-Encoding` with a value of **gzip**, **bzip2**, or **deflate**, your content is compressed.</span></span>
> 
> ![Kodowanie zawartości nagłówka](./media/cdn-troubleshoot-compression/cdn-content-header.png)
> 
> 

## <a name="cause"></a><span data-ttu-id="a3f7d-114">Przyczyna</span><span class="sxs-lookup"><span data-stu-id="a3f7d-114">Cause</span></span>
<span data-ttu-id="a3f7d-115">Istnieje kilka możliwych przyczyn, w tym:</span><span class="sxs-lookup"><span data-stu-id="a3f7d-115">There are several possible causes, including:</span></span>

* <span data-ttu-id="a3f7d-116">Żądana zawartość nie jest uprawniony do kompresji.</span><span class="sxs-lookup"><span data-stu-id="a3f7d-116">The requested content is not eligible for compression.</span></span>
* <span data-ttu-id="a3f7d-117">Kompresja nie jest włączona na żądany typ pliku.</span><span class="sxs-lookup"><span data-stu-id="a3f7d-117">Compression is not enabled for the requested file type.</span></span>
* <span data-ttu-id="a3f7d-118">Żądanie HTTP nie zawiera nagłówka zażądał typu prawidłowy kompresji.</span><span class="sxs-lookup"><span data-stu-id="a3f7d-118">The HTTP request did not include a header requesting a valid compression type.</span></span>

## <a name="troubleshooting-steps"></a><span data-ttu-id="a3f7d-119">Kroki rozwiązywania problemów</span><span class="sxs-lookup"><span data-stu-id="a3f7d-119">Troubleshooting steps</span></span>
> [!TIP]
> <span data-ttu-id="a3f7d-120">Podobnie jak w przypadku wdrażania nowych punktów końcowych, zmiany w konfiguracji sieci CDN zająć trochę czasu propagację za pośrednictwem sieci.</span><span class="sxs-lookup"><span data-stu-id="a3f7d-120">As with deploying new endpoints, CDN configuration changes take some time to propagate through the network.</span></span>  <span data-ttu-id="a3f7d-121">Zwykle zmiany zostaną zastosowane w ciągu 90 minut.</span><span class="sxs-lookup"><span data-stu-id="a3f7d-121">Usually, changes are applied within 90 minutes.</span></span>  <span data-ttu-id="a3f7d-122">Jeśli jest to po raz pierwszy po skonfigurowaniu kompresji dla punktu końcowego CDN, należy rozważyć oczekiwania 1 – 2 godz. Aby upewnić się, że ustawienia zostaną rozpropagowane do lokalizacji POP kompresji.</span><span class="sxs-lookup"><span data-stu-id="a3f7d-122">If this is the first time you've set up compression for your CDN endpoint, you should consider waiting 1-2 hours to be sure the compression settings have propagated to the POPs.</span></span> 
> 
> 

### <a name="verify-the-request"></a><span data-ttu-id="a3f7d-123">Sprawdź żądania</span><span class="sxs-lookup"><span data-stu-id="a3f7d-123">Verify the request</span></span>
<span data-ttu-id="a3f7d-124">Najpierw należy wykonać związane z poprawnością szybkie sprawdzenie żądanie.</span><span class="sxs-lookup"><span data-stu-id="a3f7d-124">First, we should do a quick sanity check on the request.</span></span>  <span data-ttu-id="a3f7d-125">Można użyć przeglądarki [narzędzia dla deweloperów](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/) Przeglądanie żądań wysyłanych.</span><span class="sxs-lookup"><span data-stu-id="a3f7d-125">You can use your browser's [developer tools](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/) to view the requests being made.</span></span>

* <span data-ttu-id="a3f7d-126">Sprawdź, żądanie jest wysyłane na adres URL punktu końcowego `<endpointname>.azureedge.net`, a nie źródła.</span><span class="sxs-lookup"><span data-stu-id="a3f7d-126">Verify the request is being sent to your endpoint URL, `<endpointname>.azureedge.net`, and not your origin.</span></span>
* <span data-ttu-id="a3f7d-127">Sprawdź żądanie zawiera **Accept-Encoding** zawiera nagłówek i wartość tego nagłówka **gzip**, **deflate**, lub **bzip2**.</span><span class="sxs-lookup"><span data-stu-id="a3f7d-127">Verify the request contains an **Accept-Encoding** header, and the value for that header contains **gzip**, **deflate**, or **bzip2**.</span></span>

> [!NOTE]
> <span data-ttu-id="a3f7d-128">**Azure CDN from Akamai** profile obsługują tylko **gzip** kodowania.</span><span class="sxs-lookup"><span data-stu-id="a3f7d-128">**Azure CDN from Akamai** profiles only support **gzip** encoding.</span></span>
> 
> 

![Nagłówki żądania CDN](./media/cdn-troubleshoot-compression/cdn-request-headers.png)

### <a name="verify-compression-settings-standard-cdn-profile"></a><span data-ttu-id="a3f7d-130">Sprawdź ustawienia kompresji (profilu sieci CDN w warstwie standardowa)</span><span class="sxs-lookup"><span data-stu-id="a3f7d-130">Verify compression settings (Standard CDN profile)</span></span>
> [!NOTE]
> <span data-ttu-id="a3f7d-131">Ten krok ma zastosowanie tylko, jeśli profil CDN jest **Azure CDN Standard from Verizon** lub **Azure CDN Standard from Akamai** profilu.</span><span class="sxs-lookup"><span data-stu-id="a3f7d-131">This step only applies if your CDN profile is an **Azure CDN Standard from Verizon** or **Azure CDN Standard from Akamai** profile.</span></span> 
> 
> 

<span data-ttu-id="a3f7d-132">Przejdź do punktu końcowego w [portalu Azure](https://portal.azure.com) i kliknij przycisk **Konfiguruj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="a3f7d-132">Navigate to your endpoint in the [Azure portal](https://portal.azure.com) and click the **Configure** button.</span></span>

* <span data-ttu-id="a3f7d-133">Sprawdź, czy kompresja jest włączona.</span><span class="sxs-lookup"><span data-stu-id="a3f7d-133">Verify compression is enabled.</span></span>
* <span data-ttu-id="a3f7d-134">Sprawdź, czy typ MIME dla zawartości do skompresowania jest uwzględniony na liście formatów skompresowane.</span><span class="sxs-lookup"><span data-stu-id="a3f7d-134">Verify the MIME type for the content to be compressed is included in the list of compressed formats.</span></span>

![Ustawienia kompresji CDN](./media/cdn-troubleshoot-compression/cdn-compression-settings.png)

### <a name="verify-compression-settings-premium-cdn-profile"></a><span data-ttu-id="a3f7d-136">Sprawdź ustawienia kompresji (profilu sieci CDN w warstwie Premium)</span><span class="sxs-lookup"><span data-stu-id="a3f7d-136">Verify compression settings (Premium CDN profile)</span></span>
> [!NOTE]
> <span data-ttu-id="a3f7d-137">Ten krok ma zastosowanie tylko, jeśli profil CDN jest **Azure CDN Premium from Verizon** profilu.</span><span class="sxs-lookup"><span data-stu-id="a3f7d-137">This step only applies if your CDN profile is an **Azure CDN Premium from Verizon** profile.</span></span>
> 
> 

<span data-ttu-id="a3f7d-138">Przejdź do punktu końcowego w [portalu Azure](https://portal.azure.com) i kliknij przycisk **Zarządzaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="a3f7d-138">Navigate to your endpoint in the [Azure portal](https://portal.azure.com) and click the **Manage** button.</span></span>  <span data-ttu-id="a3f7d-139">Zostanie otwarty w portalu dodatkowym.</span><span class="sxs-lookup"><span data-stu-id="a3f7d-139">The supplemental portal will open.</span></span>  <span data-ttu-id="a3f7d-140">Umieść kursor nad **HTTP dużych** , a następnie umieść kursor nad **ustawienia pamięci podręcznej** wysuwane okno.</span><span class="sxs-lookup"><span data-stu-id="a3f7d-140">Hover over the **HTTP Large** tab, then hover over the **Cache Settings** flyout.</span></span>  <span data-ttu-id="a3f7d-141">Kliknij przycisk **kompresji**.</span><span class="sxs-lookup"><span data-stu-id="a3f7d-141">Click **Compression**.</span></span> 

* <span data-ttu-id="a3f7d-142">Sprawdź, czy kompresja jest włączona.</span><span class="sxs-lookup"><span data-stu-id="a3f7d-142">Verify compression is enabled.</span></span>
* <span data-ttu-id="a3f7d-143">Sprawdź **typów plików** lista zawiera listę rozdzielanych przecinkami (bez spacji) typów MIME.</span><span class="sxs-lookup"><span data-stu-id="a3f7d-143">Verify the **File Types** list contains a comma-separated list (no spaces) of MIME types.</span></span>
* <span data-ttu-id="a3f7d-144">Sprawdź, czy typ MIME dla zawartości do skompresowania jest uwzględniony na liście formatów skompresowane.</span><span class="sxs-lookup"><span data-stu-id="a3f7d-144">Verify the MIME type for the content to be compressed is included in the list of compressed formats.</span></span>

![Ustawienia kompresji sieci CDN w warstwie premium](./media/cdn-troubleshoot-compression/cdn-compression-settings-premium.png)

### <a name="verify-the-content-is-cached"></a><span data-ttu-id="a3f7d-146">Sprawdź, czy zawartość jest buforowana</span><span class="sxs-lookup"><span data-stu-id="a3f7d-146">Verify the content is cached</span></span>
> [!NOTE]
> <span data-ttu-id="a3f7d-147">Ten krok ma zastosowanie tylko, jeśli profil CDN jest **Azure CDN from Verizon** profilu (standardowy lub Premium).</span><span class="sxs-lookup"><span data-stu-id="a3f7d-147">This step only applies if your CDN profile is an **Azure CDN from Verizon** profile (Standard or Premium).</span></span>
> 
> 

<span data-ttu-id="a3f7d-148">Przy użyciu narzędzia dla deweloperów w przeglądarce, sprawdź nagłówków odpowiedzi, aby upewnić się, że plik jest buforowany w regionie, w którym jest on wymagany.</span><span class="sxs-lookup"><span data-stu-id="a3f7d-148">Using your browser's developer tools, check the response headers to ensure the file is cached in the region where it is being requested.</span></span>

* <span data-ttu-id="a3f7d-149">Sprawdź **serwera** nagłówka odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="a3f7d-149">Check the **Server** response header.</span></span>  <span data-ttu-id="a3f7d-150">Nagłówek powinna mieć format **platformy (serwer protokołu POP/ID)**, jak pokazano w poniższym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="a3f7d-150">The header should have the format **Platform (POP/Server ID)**, as seen in the following example.</span></span>
* <span data-ttu-id="a3f7d-151">Sprawdź **pamięci podręcznej X** nagłówka odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="a3f7d-151">Check the **X-Cache** response header.</span></span>  <span data-ttu-id="a3f7d-152">Nagłówek należy przeczytać **TRAFIEŃ**.</span><span class="sxs-lookup"><span data-stu-id="a3f7d-152">The header should read **HIT**.</span></span>  

![Nagłówki odpowiedzi CDN](./media/cdn-troubleshoot-compression/cdn-response-headers.png)

### <a name="verify-the-file-meets-the-size-requirements"></a><span data-ttu-id="a3f7d-154">Sprawdź, czy plik spełnia wymagania dotyczące rozmiaru</span><span class="sxs-lookup"><span data-stu-id="a3f7d-154">Verify the file meets the size requirements</span></span>
> [!NOTE]
> <span data-ttu-id="a3f7d-155">Ten krok ma zastosowanie tylko, jeśli profil CDN jest **Azure CDN from Verizon** profilu (standardowy lub Premium).</span><span class="sxs-lookup"><span data-stu-id="a3f7d-155">This step only applies if your CDN profile is an **Azure CDN from Verizon** profile (Standard or Premium).</span></span>
> 
> 

<span data-ttu-id="a3f7d-156">Aby kwalifikować się do kompresji, plik musi spełniać następujące wymagania rozmiar:</span><span class="sxs-lookup"><span data-stu-id="a3f7d-156">To be eligible for compression, a file must meet the following size requirements:</span></span>

* <span data-ttu-id="a3f7d-157">Większe niż 128 bajtów.</span><span class="sxs-lookup"><span data-stu-id="a3f7d-157">Larger than 128 bytes.</span></span>
* <span data-ttu-id="a3f7d-158">Mniejszy niż 1 MB.</span><span class="sxs-lookup"><span data-stu-id="a3f7d-158">Smaller than 1 MB.</span></span>

### <a name="check-the-request-at-the-origin-server-for-a-via-header"></a><span data-ttu-id="a3f7d-159">Sprawdzanie żądania na serwerze źródłowym dla **za pośrednictwem** nagłówka</span><span class="sxs-lookup"><span data-stu-id="a3f7d-159">Check the request at the origin server for a **Via** header</span></span>
<span data-ttu-id="a3f7d-160">**Za pośrednictwem** nagłówka HTTP wskazuje na serwerze sieci web, czy żądanie jest przekazywany przez serwer proxy.</span><span class="sxs-lookup"><span data-stu-id="a3f7d-160">The **Via** HTTP header indicates to the web server that the request is being passed by a proxy server.</span></span>  <span data-ttu-id="a3f7d-161">Serwery sieci web Microsoft IIS domyślnie nie Kompresuj odpowiedzi, jeśli żądanie zawiera **za pośrednictwem** nagłówka.</span><span class="sxs-lookup"><span data-stu-id="a3f7d-161">Microsoft IIS web servers by default do not compress responses when the request contains a **Via** header.</span></span>  <span data-ttu-id="a3f7d-162">Aby zmienić to zachowanie, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="a3f7d-162">To override this behavior, perform the following:</span></span>

* <span data-ttu-id="a3f7d-163">**IIS 6**: [ustawić HcNoCompressionForProxies = "FALSE" we właściwościach metabazy usług IIS](https://msdn.microsoft.com/library/ms525390.aspx)</span><span class="sxs-lookup"><span data-stu-id="a3f7d-163">**IIS 6**: [Set HcNoCompressionForProxies="FALSE" in the IIS Metabase properties](https://msdn.microsoft.com/library/ms525390.aspx)</span></span>
* <span data-ttu-id="a3f7d-164">**Usługi IIS 7 i nowsze**: [wartość **noCompressionForHttp10** i **noCompressionForProxies** na wartość False w konfiguracji serwera](http://www.iis.net/configreference/system.webserver/httpcompression)</span><span class="sxs-lookup"><span data-stu-id="a3f7d-164">**IIS 7 and up**: [Set both **noCompressionForHttp10** and **noCompressionForProxies** to False in the server configuration](http://www.iis.net/configreference/system.webserver/httpcompression)</span></span>

