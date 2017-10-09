---
title: "Projekt aaaHybrid subsystem(s) DRM przy użyciu usługi Azure Media Services | Dokumentacja firmy Microsoft"
description: "W tym temacie omówiono hybrydowego projekt subsystem(s) DRM przy użyciu usługi Azure Media Services."
services: media-services
documentationcenter: 
author: willzhan
manager: cfowler
editor: 
ms.assetid: 18213fc1-74f5-4074-a32b-02846fe90601
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: willzhan;juliako
ms.openlocfilehash: 4206248420ccd4dbfc9a87a86f4763534c6254a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="hybrid-design-of-drm-subsystems"></a><span data-ttu-id="63e7c-103">Projekt hybrydowego DRM subsystem(s)</span><span class="sxs-lookup"><span data-stu-id="63e7c-103">Hybrid design of DRM subsystem(s)</span></span>

<span data-ttu-id="63e7c-104">W tym temacie omówiono hybrydowego projekt subsystem(s) DRM przy użyciu usługi Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="63e7c-104">This topic discusses hybrid design of DRM subsystem(s) using Azure Media Services.</span></span>

## <a name="overview"></a><span data-ttu-id="63e7c-105">Omówienie</span><span class="sxs-lookup"><span data-stu-id="63e7c-105">Overview</span></span>

<span data-ttu-id="63e7c-106">Azure Media Services obsługuje następujące trzy systemu DRM hello:</span><span class="sxs-lookup"><span data-stu-id="63e7c-106">Azure Media Services provides support for hello following three DRM system:</span></span>

* <span data-ttu-id="63e7c-107">PlayReady</span><span class="sxs-lookup"><span data-stu-id="63e7c-107">PlayReady</span></span>
* <span data-ttu-id="63e7c-108">Widevine (moduły)</span><span class="sxs-lookup"><span data-stu-id="63e7c-108">Widevine (Modular)</span></span>
* <span data-ttu-id="63e7c-109">FairPlay</span><span class="sxs-lookup"><span data-stu-id="63e7c-109">FairPlay</span></span>

<span data-ttu-id="63e7c-110">Obsługa DRM Hello obejmuje szyfrowania DRM (dynamicznego szyfrowania) i dostarczania licencji przy użyciu usługi Azure Media Player obsługi wszystkich DRMs 3 jako odtwarzacza przeglądarkę zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="63e7c-110">hello DRM support includes DRM encryption (dynamic encryption) and license delivery, with Azure Media Player supporting all 3 DRMs as a browser player SDK.</span></span>

<span data-ttu-id="63e7c-111">Szczegółowe traktowania DRM/CENC podsystemu projekt i implementację, zobacz dokument hello zatytułowany [CENC z wieloma DRM i kontrolą dostępu](media-services-cenc-with-multidrm-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="63e7c-111">For a detailed treatment of DRM/CENC subsystem design and implementation, please see hello document titled [CENC with Multi-DRM and Access Control](media-services-cenc-with-multidrm-access-control.md).</span></span>

<span data-ttu-id="63e7c-112">Mimo że firma Microsoft oferuje pełnej obsługi dla trzech systemach DRM, czasami klienci muszą toouse różnych części własnej infrastruktury i podsystemy w dodanie tooAzure Media Services toobuild hybrydowego Podsystem DRM.</span><span class="sxs-lookup"><span data-stu-id="63e7c-112">Although we offer complete support for three DRM systems, sometimes customers need toouse various parts of their own infrastructure/subsystems in addition tooAzure Media Services toobuild a hybrid DRM subsystem.</span></span>

<span data-ttu-id="63e7c-113">Poniżej są często zadawane pytania poprosił o ponowne klientów:</span><span class="sxs-lookup"><span data-stu-id="63e7c-113">Below are some common questions asked by customers:</span></span>

* <span data-ttu-id="63e7c-114">"Czy za pomocą własnych serwerów licencji DRM?"</span><span class="sxs-lookup"><span data-stu-id="63e7c-114">"Can I use my own DRM license servers?"</span></span> <span data-ttu-id="63e7c-115">(W tym przypadku klienci ma zainwestowały w farmie serwerów licencji DRM z logiki biznesowej osadzonych).</span><span class="sxs-lookup"><span data-stu-id="63e7c-115">(In this case, customers have invested in DRM license server farm with embedded business logic).</span></span>
* <span data-ttu-id="63e7c-116">"Czy za pomocą tylko z dostarczania licencji DRM w usłudze Azure Media Services bez hostowanie zawartości w AMS?"</span><span class="sxs-lookup"><span data-stu-id="63e7c-116">"Can I use only your DRM license delivery in Azure Media Services without hosting content in AMS?"</span></span>

## <a name="modularity-of-hello-ams-drm-platform"></a><span data-ttu-id="63e7c-117">Modułowość hello platformy AMS DRM</span><span class="sxs-lookup"><span data-stu-id="63e7c-117">Modularity of hello AMS DRM platform</span></span>

<span data-ttu-id="63e7c-118">W ramach kompleksowe wideo platformy w chmurze usługi Azure Media Services DRM ma projektu z elastyczność i Modułowość pamiętać.</span><span class="sxs-lookup"><span data-stu-id="63e7c-118">As part of a comprehensive cloud video platform, Azure Media Services DRM has a design with flexibility and modularity in mind.</span></span> <span data-ttu-id="63e7c-119">Za pomocą dowolnego z powitania po różnych kombinacji opisane w tabeli hello poniżej (wyjaśnienie notacji hello używany w tabeli hello następuje), można użyć usługi Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="63e7c-119">You can use Azure Media Services with any of hello following different combinations described in hello table below (an explanation of hello notation used in hello table follows).</span></span> 

|<span data-ttu-id="63e7c-120">**Hosting zawartości i źródła**</span><span class="sxs-lookup"><span data-stu-id="63e7c-120">**Content hosting & origin**</span></span>|<span data-ttu-id="63e7c-121">**Szyfrowanie zawartości**</span><span class="sxs-lookup"><span data-stu-id="63e7c-121">**Content encryption**</span></span>|<span data-ttu-id="63e7c-122">**Dostarczanie licencji DRM**</span><span class="sxs-lookup"><span data-stu-id="63e7c-122">**DRM license delivery**</span></span>|
|---|---|---|
|<span data-ttu-id="63e7c-123">AMS</span><span class="sxs-lookup"><span data-stu-id="63e7c-123">AMS</span></span>|<span data-ttu-id="63e7c-124">AMS</span><span class="sxs-lookup"><span data-stu-id="63e7c-124">AMS</span></span>|<span data-ttu-id="63e7c-125">AMS</span><span class="sxs-lookup"><span data-stu-id="63e7c-125">AMS</span></span>|
|<span data-ttu-id="63e7c-126">AMS</span><span class="sxs-lookup"><span data-stu-id="63e7c-126">AMS</span></span>|<span data-ttu-id="63e7c-127">AMS</span><span class="sxs-lookup"><span data-stu-id="63e7c-127">AMS</span></span>|<span data-ttu-id="63e7c-128">Innych firm</span><span class="sxs-lookup"><span data-stu-id="63e7c-128">Third-party</span></span>|
|<span data-ttu-id="63e7c-129">AMS</span><span class="sxs-lookup"><span data-stu-id="63e7c-129">AMS</span></span>|<span data-ttu-id="63e7c-130">Innych firm</span><span class="sxs-lookup"><span data-stu-id="63e7c-130">Third-party</span></span>|<span data-ttu-id="63e7c-131">AMS</span><span class="sxs-lookup"><span data-stu-id="63e7c-131">AMS</span></span>|
|<span data-ttu-id="63e7c-132">AMS</span><span class="sxs-lookup"><span data-stu-id="63e7c-132">AMS</span></span>|<span data-ttu-id="63e7c-133">Innych firm</span><span class="sxs-lookup"><span data-stu-id="63e7c-133">Third-party</span></span>|<span data-ttu-id="63e7c-134">Innych firm</span><span class="sxs-lookup"><span data-stu-id="63e7c-134">Third-party</span></span>|
|<span data-ttu-id="63e7c-135">Innych firm</span><span class="sxs-lookup"><span data-stu-id="63e7c-135">Third-party</span></span>|<span data-ttu-id="63e7c-136">Innych firm</span><span class="sxs-lookup"><span data-stu-id="63e7c-136">Third-party</span></span>|<span data-ttu-id="63e7c-137">AMS</span><span class="sxs-lookup"><span data-stu-id="63e7c-137">AMS</span></span>|

### <a name="content-hosting--origin"></a><span data-ttu-id="63e7c-138">Hosting zawartości i źródła</span><span class="sxs-lookup"><span data-stu-id="63e7c-138">Content hosting & origin</span></span>

* <span data-ttu-id="63e7c-139">AMS: zawartości wideo jest obsługiwana w AMS i przesyłania strumieniowego odbywa się za pośrednictwem usługi AMS punktów końcowych przesyłania strumieniowego (ale nie zawsze dynamicznego tworzenia pakietów).</span><span class="sxs-lookup"><span data-stu-id="63e7c-139">AMS: video asset is hosted in AMS and streaming is through AMS streaming endpoints (but not necessarily dynamic packaging).</span></span>
* <span data-ttu-id="63e7c-140">Innych firm: wideo jest obsługiwana i dostarczane na platformie przesyłania strumieniowego innych firm poza AMS.</span><span class="sxs-lookup"><span data-stu-id="63e7c-140">Third-party: video is hosted and delivered on a third-party streaming platform outside of AMS.</span></span>

### <a name="content-encryption"></a><span data-ttu-id="63e7c-141">Szyfrowanie zawartości</span><span class="sxs-lookup"><span data-stu-id="63e7c-141">Content encryption</span></span>

* <span data-ttu-id="63e7c-142">AMS: szyfrowanie zawartości jest wykonywane dynamicznie/na żądanie za pomocą szyfrowania dynamicznego AMS.</span><span class="sxs-lookup"><span data-stu-id="63e7c-142">AMS: content encryption is performed dynamically/on-demand by AMS dynamic encryption.</span></span>
* <span data-ttu-id="63e7c-143">Innych firm: szyfrowanie zawartości jest wykonywane poza AMS przy użyciu przetwarzania wstępnego przepływ pracy.</span><span class="sxs-lookup"><span data-stu-id="63e7c-143">Third-party: content encryption is performed outside of AMS using a pre-processing workflow.</span></span>

### <a name="drm-license-delivery"></a><span data-ttu-id="63e7c-144">Dostarczanie licencji DRM</span><span class="sxs-lookup"><span data-stu-id="63e7c-144">DRM license delivery</span></span>

* <span data-ttu-id="63e7c-145">AMS: Licencji DRM są dostarczane przez usługę dostarczania licencji AMS.</span><span class="sxs-lookup"><span data-stu-id="63e7c-145">AMS: DRM license is delivered by AMS license delivery service.</span></span>
* <span data-ttu-id="63e7c-146">Innych firm: Licencji DRM są dostarczane przez serwer licencji DRM innych firm, poza AMS.</span><span class="sxs-lookup"><span data-stu-id="63e7c-146">Third-party: DRM license is delivered by a third-party DRM license server outside of AMS.</span></span>

## <a name="configure-based-on-your-hybrid-scenario"></a><span data-ttu-id="63e7c-147">Skonfiguruj oparte na danego scenariusza hybrydowego</span><span class="sxs-lookup"><span data-stu-id="63e7c-147">Configure based on your hybrid scenario</span></span>

### <a name="content-key"></a><span data-ttu-id="63e7c-148">Klucz zawartości</span><span class="sxs-lookup"><span data-stu-id="63e7c-148">Content key</span></span>

<span data-ttu-id="63e7c-149">Poprzez konfigurację klucz zawartości można kontrolować następujące atrybuty AMS szyfrowania dynamicznego i usługi dostarczania licencji AMS hello:</span><span class="sxs-lookup"><span data-stu-id="63e7c-149">Through configuration of a content key, you can control hello following attributes of both AMS dynamic encryption and AMS license delivery service:</span></span>

* <span data-ttu-id="63e7c-150">klucz zawartości Hello używany do szyfrowania dynamicznego DRM.</span><span class="sxs-lookup"><span data-stu-id="63e7c-150">hello content key used for dynamic DRM encryption.</span></span>
* <span data-ttu-id="63e7c-151">Toobe zawartości licencji DRM dostarczane przez usługi dostarczania licencji: klucz zawartości, ograniczenia i uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="63e7c-151">DRM license content toobe delivered by license delivery services: rights, content key and restrictions.</span></span>
* <span data-ttu-id="63e7c-152">Typ **ograniczenia zasad autoryzacji klucza zawartości**: Otwórz adres IP lub ograniczenie tokenu.</span><span class="sxs-lookup"><span data-stu-id="63e7c-152">Type of **content key authorization policy restriction**: open, IP, or token restriction.</span></span>
* <span data-ttu-id="63e7c-153">Jeśli **tokenu** typu **ograniczenia zasad autoryzacji klucza zawartości jest używany**, hello **ograniczenia zasad autoryzacji klucza zawartości** muszą zostać spełnione przed wystawieniem licencji.</span><span class="sxs-lookup"><span data-stu-id="63e7c-153">If **token** type of **content key authorization policy restriction is used**, hello **content key authorization policy restriction** must be met before a license is issued.</span></span>

### <a name="asset-delivery-policy"></a><span data-ttu-id="63e7c-154">Zasady dostarczania elementu zawartości</span><span class="sxs-lookup"><span data-stu-id="63e7c-154">Asset delivery policy</span></span>

<span data-ttu-id="63e7c-155">Za pomocą konfiguracji zasad dostarczania elementów zawartości można kontrolować następujące atrybuty używany przez dynamiczne Pakowarka AMS i dynamicznego szyfrowania AMS punktu końcowego przesyłania strumieniowego hello:</span><span class="sxs-lookup"><span data-stu-id="63e7c-155">Through configuration of an asset delivery policy, you can control hello following attributes used by AMS dynamic packager and dynamic encryption of an AMS streaming endpoint:</span></span>

* <span data-ttu-id="63e7c-156">Protokół i kombinacja szyfrowania DRM przesyłania strumieniowego, takich jak ŁĄCZNIKI w obszarze CENC (PlayReady i Widevine), funkcje smooth streaming w obszarze PlayReady, HLS w ramach Widevine lub PlayReady.</span><span class="sxs-lookup"><span data-stu-id="63e7c-156">Streaming protocol and DRM encryption combination, such as DASH under CENC (PlayReady and Widevine), smooth streaming under PlayReady, HLS under Widevine or PlayReady.</span></span>
* <span data-ttu-id="63e7c-157">Hello domyślne/osadzonych licencji dostarczania adresów URL dla każdego hello zaangażowane DRMs.</span><span class="sxs-lookup"><span data-stu-id="63e7c-157">hello default/embedded license delivery URLs for each of hello involved DRMs.</span></span>
* <span data-ttu-id="63e7c-158">Określa, czy licencję adresy URL pozyskiwania (LA_URLs) w DASH MPD lub HLS odtwarzania zawierają ciąg zapytania klucza identyfikator (KĄCIK) Widevine i FairPlay, odpowiednio.</span><span class="sxs-lookup"><span data-stu-id="63e7c-158">Whether license acquisition URLs (LA_URLs) in DASH MPD or HLS playlist contain query string of key ID (KID) for Widevine and FairPlay, respectively.</span></span>

## <a name="scenarios-and-samples"></a><span data-ttu-id="63e7c-159">Scenariusze i przykłady</span><span class="sxs-lookup"><span data-stu-id="63e7c-159">Scenarios and samples</span></span>

<span data-ttu-id="63e7c-160">W oparciu o wyjaśnienia hello w poprzedniej sekcji hello, hello następujące pięć scenariuszy hybrydowych użyć odpowiednich **klucz zawartości**-**zasad dostarczania elementów zawartości** kombinacje konfiguracji (hello Przykłady wymienionych w ostatniej kolumnie hello wykonaj tabeli hello):</span><span class="sxs-lookup"><span data-stu-id="63e7c-160">Based on hello explanations in hello previous section, hello following five hybrid scenarios use respective **Content key**-**Asset delivery policy** configuration combinations (hello samples mentioned in hello last column follow hello table):</span></span>

|<span data-ttu-id="63e7c-161">**Hosting zawartości i źródła**</span><span class="sxs-lookup"><span data-stu-id="63e7c-161">**Content hosting & origin**</span></span>|<span data-ttu-id="63e7c-162">**Szyfrowanie DRM**</span><span class="sxs-lookup"><span data-stu-id="63e7c-162">**DRM encryption**</span></span>|<span data-ttu-id="63e7c-163">**Dostarczanie licencji DRM**</span><span class="sxs-lookup"><span data-stu-id="63e7c-163">**DRM license delivery**</span></span>|<span data-ttu-id="63e7c-164">**Skonfiguruj klucz zawartości**</span><span class="sxs-lookup"><span data-stu-id="63e7c-164">**Configure content key**</span></span>|<span data-ttu-id="63e7c-165">**Konfigurowanie zasad dostarczania elementów zawartości**</span><span class="sxs-lookup"><span data-stu-id="63e7c-165">**Configure asset delivery policy**</span></span>|<span data-ttu-id="63e7c-166">**Próbki**</span><span class="sxs-lookup"><span data-stu-id="63e7c-166">**Sample**</span></span>|
|---|---|---|---|---|---|
|<span data-ttu-id="63e7c-167">AMS</span><span class="sxs-lookup"><span data-stu-id="63e7c-167">AMS</span></span>|<span data-ttu-id="63e7c-168">AMS</span><span class="sxs-lookup"><span data-stu-id="63e7c-168">AMS</span></span>|<span data-ttu-id="63e7c-169">AMS</span><span class="sxs-lookup"><span data-stu-id="63e7c-169">AMS</span></span>|<span data-ttu-id="63e7c-170">Tak</span><span class="sxs-lookup"><span data-stu-id="63e7c-170">Yes</span></span>|<span data-ttu-id="63e7c-171">Tak</span><span class="sxs-lookup"><span data-stu-id="63e7c-171">Yes</span></span>|<span data-ttu-id="63e7c-172">Przykład 1</span><span class="sxs-lookup"><span data-stu-id="63e7c-172">Sample 1</span></span>|
|<span data-ttu-id="63e7c-173">AMS</span><span class="sxs-lookup"><span data-stu-id="63e7c-173">AMS</span></span>|<span data-ttu-id="63e7c-174">AMS</span><span class="sxs-lookup"><span data-stu-id="63e7c-174">AMS</span></span>|<span data-ttu-id="63e7c-175">Innych firm</span><span class="sxs-lookup"><span data-stu-id="63e7c-175">Third-party</span></span>|<span data-ttu-id="63e7c-176">Tak</span><span class="sxs-lookup"><span data-stu-id="63e7c-176">Yes</span></span>|<span data-ttu-id="63e7c-177">Tak</span><span class="sxs-lookup"><span data-stu-id="63e7c-177">Yes</span></span>|<span data-ttu-id="63e7c-178">Przykład 2</span><span class="sxs-lookup"><span data-stu-id="63e7c-178">Sample 2</span></span>|
|<span data-ttu-id="63e7c-179">AMS</span><span class="sxs-lookup"><span data-stu-id="63e7c-179">AMS</span></span>|<span data-ttu-id="63e7c-180">Innych firm</span><span class="sxs-lookup"><span data-stu-id="63e7c-180">Third-party</span></span>|<span data-ttu-id="63e7c-181">AMS</span><span class="sxs-lookup"><span data-stu-id="63e7c-181">AMS</span></span>|<span data-ttu-id="63e7c-182">Tak</span><span class="sxs-lookup"><span data-stu-id="63e7c-182">Yes</span></span>|<span data-ttu-id="63e7c-183">Nie</span><span class="sxs-lookup"><span data-stu-id="63e7c-183">No</span></span>|<span data-ttu-id="63e7c-184">Przykład 3</span><span class="sxs-lookup"><span data-stu-id="63e7c-184">Sample 3</span></span>|
|<span data-ttu-id="63e7c-185">AMS</span><span class="sxs-lookup"><span data-stu-id="63e7c-185">AMS</span></span>|<span data-ttu-id="63e7c-186">Innych firm</span><span class="sxs-lookup"><span data-stu-id="63e7c-186">Third-party</span></span>|<span data-ttu-id="63e7c-187">Poza</span><span class="sxs-lookup"><span data-stu-id="63e7c-187">Outside</span></span>|<span data-ttu-id="63e7c-188">Nie</span><span class="sxs-lookup"><span data-stu-id="63e7c-188">No</span></span>|<span data-ttu-id="63e7c-189">Nie</span><span class="sxs-lookup"><span data-stu-id="63e7c-189">No</span></span>|<span data-ttu-id="63e7c-190">Przykład 4</span><span class="sxs-lookup"><span data-stu-id="63e7c-190">Sample 4</span></span>|
|<span data-ttu-id="63e7c-191">Innych firm</span><span class="sxs-lookup"><span data-stu-id="63e7c-191">Third-party</span></span>|<span data-ttu-id="63e7c-192">Innych firm</span><span class="sxs-lookup"><span data-stu-id="63e7c-192">Third-party</span></span>|<span data-ttu-id="63e7c-193">AMS</span><span class="sxs-lookup"><span data-stu-id="63e7c-193">AMS</span></span>|<span data-ttu-id="63e7c-194">Tak</span><span class="sxs-lookup"><span data-stu-id="63e7c-194">Yes</span></span>|<span data-ttu-id="63e7c-195">Nie</span><span class="sxs-lookup"><span data-stu-id="63e7c-195">No</span></span>|    

<span data-ttu-id="63e7c-196">W próbkach hello działa ochrona PlayReady kreska i smooth streaming.</span><span class="sxs-lookup"><span data-stu-id="63e7c-196">In hello samples, PlayReady protection works for both DASH and smooth streaming.</span></span> <span data-ttu-id="63e7c-197">Witaj wideo poniżej część adresy URL są smooth streaming adresów URL.</span><span class="sxs-lookup"><span data-stu-id="63e7c-197">hello video URLs below are smooth streaming URLs.</span></span> <span data-ttu-id="63e7c-198">tooget hello odpowiednie PAUZY adresów URL, po prostu Dołącz "(format = mpd-time-csf)".</span><span class="sxs-lookup"><span data-stu-id="63e7c-198">tooget hello corresponding DASH URLs, just append "(format=mpd-time-csf)".</span></span> <span data-ttu-id="63e7c-199">Można użyć hello [azure media test player](http://aka.ms/amtest) tootest w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="63e7c-199">You could use hello [azure media test player](http://aka.ms/amtest) tootest in a browser.</span></span> <span data-ttu-id="63e7c-200">Umożliwia tooconfigure który przesyłania strumieniowego toouse protokół, w których techniczna.</span><span class="sxs-lookup"><span data-stu-id="63e7c-200">It allows you tooconfigure which streaming protocol toouse, under which tech.</span></span> <span data-ttu-id="63e7c-201">Obsługuje PlayReady za pośrednictwem EME, IE11 i MS Edge w systemie Windows 10.</span><span class="sxs-lookup"><span data-stu-id="63e7c-201">IE11 and MS Edge on Windows 10 support PlayReady through EME.</span></span> <span data-ttu-id="63e7c-202">Aby uzyskać więcej informacji, zobacz [szczegóły hello testu narzędzia](https://blogs.msdn.microsoft.com/playready4/2016/02/28/azure-media-test-tool/).</span><span class="sxs-lookup"><span data-stu-id="63e7c-202">For more information, see [details about hello test tool](https://blogs.msdn.microsoft.com/playready4/2016/02/28/azure-media-test-tool/).</span></span>

### <a name="sample-1"></a><span data-ttu-id="63e7c-203">Przykład 1</span><span class="sxs-lookup"><span data-stu-id="63e7c-203">Sample 1</span></span>

* <span data-ttu-id="63e7c-204">Źródłowy adres URL (podstawowy): https://willzhanmswest.streaming.mediaservices.windows.net/1efbd6bb-1e66-4e53-88c3-f7e5657a9bbd/RussianWaltz.ism/manifest</span><span class="sxs-lookup"><span data-stu-id="63e7c-204">Source (base) URL: https://willzhanmswest.streaming.mediaservices.windows.net/1efbd6bb-1e66-4e53-88c3-f7e5657a9bbd/RussianWaltz.ism/manifest</span></span> 
* <span data-ttu-id="63e7c-205">PlayReady LA_URL (DASH & smooth): https://willzhanmswest.keydelivery.mediaservices.windows.net/PlayReady/</span><span class="sxs-lookup"><span data-stu-id="63e7c-205">PlayReady LA_URL (DASH & smooth): https://willzhanmswest.keydelivery.mediaservices.windows.net/PlayReady/</span></span> 
* <span data-ttu-id="63e7c-206">Widevine LA_URL (kreska): https://willzhanmswest.keydelivery.mediaservices.windows.net/Widevine/?kid=78de73ae-6d0f-470a-8f13-5c91f7c4</span><span class="sxs-lookup"><span data-stu-id="63e7c-206">Widevine LA_URL (DASH): https://willzhanmswest.keydelivery.mediaservices.windows.net/Widevine/?kid=78de73ae-6d0f-470a-8f13-5c91f7c4</span></span> 
* <span data-ttu-id="63e7c-207">LA_URL FairPlay (HLS): https://willzhanmswest.keydelivery.mediaservices.windows.net/FairPlay/?kid=ba7e8fb0-ee22-4291-9654-6222ac611bd8</span><span class="sxs-lookup"><span data-stu-id="63e7c-207">FairPlay LA_URL (HLS): https://willzhanmswest.keydelivery.mediaservices.windows.net/FairPlay/?kid=ba7e8fb0-ee22-4291-9654-6222ac611bd8</span></span> 

### <a name="sample-2"></a><span data-ttu-id="63e7c-208">Przykład 2</span><span class="sxs-lookup"><span data-stu-id="63e7c-208">Sample 2</span></span>

* <span data-ttu-id="63e7c-209">Źródłowy adres URL (podstawowy): http://willzhanmswest.streaming.mediaservices.windows.net/1a670626-4515-49ee-9e7f-cd50853e41d8/Microsoft_HoloLens_TransformYourWorld_816p23.ism/Manifest</span><span class="sxs-lookup"><span data-stu-id="63e7c-209">Source (base) URL: http://willzhanmswest.streaming.mediaservices.windows.net/1a670626-4515-49ee-9e7f-cd50853e41d8/Microsoft_HoloLens_TransformYourWorld_816p23.ism/Manifest</span></span> 
* <span data-ttu-id="63e7c-210">PlayReady LA_URL (DASH & smooth): http://willzhan12.cloudapp.net/PlayReady/RightsManager.asmx</span><span class="sxs-lookup"><span data-stu-id="63e7c-210">PlayReady LA_URL (DASH & smooth): http://willzhan12.cloudapp.net/PlayReady/RightsManager.asmx</span></span> 

### <a name="sample-3"></a><span data-ttu-id="63e7c-211">Przykład 3</span><span class="sxs-lookup"><span data-stu-id="63e7c-211">Sample 3</span></span>

* <span data-ttu-id="63e7c-212">Źródłowy adres URL: https://willzhanmswest.streaming.mediaservices.windows.net/8d078cf8-d621-406c-84ca-88e6b9454acc/20150807-bridges-2500.ism/manifest</span><span class="sxs-lookup"><span data-stu-id="63e7c-212">Source URL: https://willzhanmswest.streaming.mediaservices.windows.net/8d078cf8-d621-406c-84ca-88e6b9454acc/20150807-bridges-2500.ism/manifest</span></span> 
* <span data-ttu-id="63e7c-213">PlayReady LA_URL (DASH & smooth): https://willzhanmswest.keydelivery.mediaservices.windows.net/PlayReady/</span><span class="sxs-lookup"><span data-stu-id="63e7c-213">PlayReady LA_URL (DASH & smooth): https://willzhanmswest.keydelivery.mediaservices.windows.net/PlayReady/</span></span> 

### <a name="sample-4"></a><span data-ttu-id="63e7c-214">Przykład 4</span><span class="sxs-lookup"><span data-stu-id="63e7c-214">Sample 4</span></span>

* <span data-ttu-id="63e7c-215">Źródłowy adres URL: https://willzhanmswest.streaming.mediaservices.windows.net/7c085a59-ae9a-411e-842c-ef10f96c3f89/20150807-bridges-2500.ism/manifest</span><span class="sxs-lookup"><span data-stu-id="63e7c-215">Source URL: https://willzhanmswest.streaming.mediaservices.windows.net/7c085a59-ae9a-411e-842c-ef10f96c3f89/20150807-bridges-2500.ism/manifest</span></span> 
* <span data-ttu-id="63e7c-216">PlayReady LA_URL (DASH & smooth): https://willzhan12.cloudapp.net/playready/rightsmanager.asmx</span><span class="sxs-lookup"><span data-stu-id="63e7c-216">PlayReady LA_URL (DASH & smooth): https://willzhan12.cloudapp.net/playready/rightsmanager.asmx</span></span> 

## <a name="summary"></a><span data-ttu-id="63e7c-217">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="63e7c-217">Summary</span></span>

<span data-ttu-id="63e7c-218">Podsumowując składniki usługi Azure Media Services DRM są elastyczne, możesz użyć ich w scenariuszu hybrydowym odpowiednio konfigurując klucz zawartości i zasady dostarczania elementu zawartości, zgodnie z opisem w tym temacie.</span><span class="sxs-lookup"><span data-stu-id="63e7c-218">In summary, Azure Media Services DRM components are flexible, you can use them in a hybrid scenario by properly configuring content key and asset delivery policy, as described in this topic.</span></span>

## <a name="next-steps"></a><span data-ttu-id="63e7c-219">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="63e7c-219">Next steps</span></span>
<span data-ttu-id="63e7c-220">Ścieżki szkoleniowe dotyczące usługi Media widoku.</span><span class="sxs-lookup"><span data-stu-id="63e7c-220">View Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="63e7c-221">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="63e7c-221">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

