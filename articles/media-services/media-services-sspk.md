---
title: "Licencjonowania Microsoft® Smooth Streaming Client Eksportowanie zestawu"
description: "Dowiedz się więcej o tym, jak dotyczące licencjonowania Microsoft® Smooth Streaming klienta Eksportowanie zestawu."
services: media-services
documentationcenter: 
author: xpouyat
manager: cfowler
editor: 
ms.assetid: e3b488e7-8428-4c10-a072-eb3af46c82ad
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: xpouyat
ms.openlocfilehash: b5a36ac6771bef220afe29446cd56c1b65a498d9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="licensing-microsoft-smooth-streaming-client-porting-kit"></a><span data-ttu-id="66985-103">Licencjonowania Microsoft® Smooth Streaming Client Eksportowanie zestawu</span><span class="sxs-lookup"><span data-stu-id="66985-103">Licensing Microsoft® Smooth Streaming Client Porting Kit</span></span>
## <a name="overview"></a><span data-ttu-id="66985-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="66985-104">Overview</span></span>
<span data-ttu-id="66985-105">Microsoft Smooth Streaming klienta Eksportowanie zestawu (**SSPK** skrócie) jest Smooth Streaming implementacji klienta, który jest zoptymalizowany do pomocy producenci urządzeń osadzonych, kabel i operatorów komórkowych, dostawców usług zawartości, słuchawki producenci, niezależnym dostawcom oprogramowania (ISV) i dostawców rozwiązań do utworzenia produktów i usług do przesyłania strumieniowego z adaptacyjną przesyłania strumieniowego zawartości w formacie Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="66985-105">Microsoft Smooth Streaming Client Porting Kit (**SSPK** for short) is a Smooth Streaming client implementation that is optimized to help embedded device manufacturers, cable and mobile operators, content service providers, handset manufacturers, independent software vendors (ISVs), and solution providers to create products and services for streaming adaptive streaming content in Smooth Streaming format.</span></span> <span data-ttu-id="66985-106">SSPK jest platforma i urządzenie niezależnie od implementacji klienta Smooth Streaming, które mogą być przenoszone przez licencjobiorcę do dowolnego urządzenia i platformy.</span><span class="sxs-lookup"><span data-stu-id="66985-106">SSPK is a device and platform independent implementation of Smooth Streaming client that can be ported by the licensee to any device and platform.</span></span> 

<span data-ttu-id="66985-107">Przedstawionym poniżej jest wysokiego poziomu architektury i pole IIS Smooth Streaming Eksportowanie zestawu implementacji Smooth Streaming Client obsługiwane przez firmę Microsoft i zawiera całą logikę core odtwarzanie zawartości Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="66985-107">Included below is a high level architecture and IIS Smooth Streaming Porting Kit box is the Smooth Streaming Client implementation provided by Microsoft and includes all the core logic for playback of Smooth Streaming content.</span></span> <span data-ttu-id="66985-108">Jest to następnie przenoszone przez partnerów dla określonego urządzenia lub platformy zaimplementowanie odpowiednich interfejsów.</span><span class="sxs-lookup"><span data-stu-id="66985-108">This is then ported by partners for a specific device or platform by implementing appropriate interfaces.</span></span> 

![SSPK](./media/media-services-sspk/sspk-arch.png)

## <a name="description"></a><span data-ttu-id="66985-110">Opis</span><span class="sxs-lookup"><span data-stu-id="66985-110">Description</span></span>
<span data-ttu-id="66985-111">SSPK jest licencjonowana na warunkach, które oferuje doskonałą biznesu.</span><span class="sxs-lookup"><span data-stu-id="66985-111">SSPK is licensed on terms that offer excellent business value.</span></span> <span data-ttu-id="66985-112">SSPK licencji zawiera z branży:</span><span class="sxs-lookup"><span data-stu-id="66985-112">SSPK license provides the industry with:</span></span>

* <span data-ttu-id="66985-113">Smooth Streaming Eksportowanie zestawu źródła w języku C++</span><span class="sxs-lookup"><span data-stu-id="66985-113">Smooth Streaming Porting Kit source in C++</span></span> 
  * <span data-ttu-id="66985-114">implementuje funkcje Smooth Streaming Client</span><span class="sxs-lookup"><span data-stu-id="66985-114">implements Smooth Streaming Client functionality</span></span>
  * <span data-ttu-id="66985-115">dodaje format analizowania heurystyki buforowanie logiki itp.</span><span class="sxs-lookup"><span data-stu-id="66985-115">adds format parsing, heuristics, buffering logic, etc.</span></span>
* <span data-ttu-id="66985-116">Aplikacja odtwarzacza interfejsów API</span><span class="sxs-lookup"><span data-stu-id="66985-116">Player application APIs</span></span> 
  * <span data-ttu-id="66985-117">interfejsy programowania do interakcji z aplikacją media player</span><span class="sxs-lookup"><span data-stu-id="66985-117">programming interfaces for interaction with a media player application</span></span>
* <span data-ttu-id="66985-118">Interfejs (PAL) warstwy abstrakcji platformy</span><span class="sxs-lookup"><span data-stu-id="66985-118">Platform Abstraction Layer (PAL) Interface</span></span> 
  * <span data-ttu-id="66985-119">interfejsy programowania do interakcji z systemem operacyjnym (wątki, sockets)</span><span class="sxs-lookup"><span data-stu-id="66985-119">programming interfaces for interaction with the operating system (threads, sockets)</span></span>
* <span data-ttu-id="66985-120">Interfejs (HAL) warstwy abstrakcji sprzętu</span><span class="sxs-lookup"><span data-stu-id="66985-120">Hardware Abstraction Layer (HAL) Interface</span></span> 
  * <span data-ttu-id="66985-121">interfejsy do interakcji z urządzenia, A / V dekodery (dekodowania, renderowania)</span><span class="sxs-lookup"><span data-stu-id="66985-121">programming interfaces for interaction with hardware A/V decoders (decoding, rendering)</span></span>
* <span data-ttu-id="66985-122">Interfejs zarządzania (prawami cyfrowymi DRM) prawami cyfrowymi</span><span class="sxs-lookup"><span data-stu-id="66985-122">Digital Rights Management (DRM) Interface</span></span> 
  * <span data-ttu-id="66985-123">interfejsy programowania obsługi DRM przez warstwę abstrakcji DRM (DAL)</span><span class="sxs-lookup"><span data-stu-id="66985-123">programming interfaces for handling DRM through the DRM Abstraction Layer (DAL)</span></span>
  * <span data-ttu-id="66985-124">Microsoft PlayReady eksportowanie Kit jest dostarczany oddzielnie, ale integruje się za pośrednictwem tego interfejsu.</span><span class="sxs-lookup"><span data-stu-id="66985-124">Microsoft PlayReady Porting Kit ships separately but integrates through this interface.</span></span> <span data-ttu-id="66985-125">Więcej szczegółów dotyczących licencji firmy Microsoft PlayReady Device, kliknij przycisk [tutaj](http://www.microsoft.com/playready/licensing/device_technology.mspx#pddipdl).</span><span class="sxs-lookup"><span data-stu-id="66985-125">For more details on Microsoft PlayReady Device licensing, click [here](http://www.microsoft.com/playready/licensing/device_technology.mspx#pddipdl).</span></span>
* <span data-ttu-id="66985-126">Przykłady implementacji</span><span class="sxs-lookup"><span data-stu-id="66985-126">Implementation samples</span></span> 
  * <span data-ttu-id="66985-127">Przykładowe zastosowanie PAL dla systemu Linux</span><span class="sxs-lookup"><span data-stu-id="66985-127">sample PAL implementation for Linux</span></span>
  * <span data-ttu-id="66985-128">Przykładowe zastosowanie HAL dla GStreamer</span><span class="sxs-lookup"><span data-stu-id="66985-128">sample HAL implementation for GStreamer</span></span>

## <a name="licensing-options"></a><span data-ttu-id="66985-129">Opcje licencjonowania</span><span class="sxs-lookup"><span data-stu-id="66985-129">Licensing Options</span></span>
<span data-ttu-id="66985-130">Microsoft Smooth Streaming klienta Eksportowanie zestawu będą dostępne dla licencjobiorców w dwóch umów licencyjnych distinct: jeden dla rozwoju Smooth produktów przejściowej klienta przesyłania strumieniowego i drugi dla dystrybucji Smooth Streaming klienta produktów końcowych dla użytkowników końcowych.</span><span class="sxs-lookup"><span data-stu-id="66985-130">Microsoft Smooth Streaming Client Porting Kit is made available to licensees under two distinct license agreements: one for developing Smooth Streaming Client Interim Products and another for distributing Smooth Streaming Client Final Products to end users.</span></span>

* <span data-ttu-id="66985-131">Mikroukładem producentów, niezależnie od oprogramowania i integratorów systemów. platforma dostawcy (ISV), którzy muszą mieć źródło kodu zestawu przenoszenia do rozwoju produktów przejściowej, Microsoft Smooth Streaming klienta Eksportowanie zestawu **licencji produktu przejściowej** powinien być wykonywany.</span><span class="sxs-lookup"><span data-stu-id="66985-131">For chipset manufacturers, system integrators, or independent software vendors (ISVs) who require a source code porting kit to develop Interim Products, a Microsoft Smooth Streaming Client Porting Kit **Interim Product License** should be executed.</span></span>
* <span data-ttu-id="66985-132">Dla producentów lub niezależnym dostawcom oprogramowania wymagających praw dystrybucji Smooth Streaming klienta produktów końcowych dla użytkowników końcowych, Microsoft Smooth Streaming klienta Eksportowanie zestawu **końcowej licencji produktu** mają zostać wykonane.</span><span class="sxs-lookup"><span data-stu-id="66985-132">For device manufacturers or ISVs who require distribution rights for Smooth Streaming Client Final Products to end users, the Microsoft Smooth Streaming Client Porting Kit **Final Product License** should be executed.</span></span>

### <a name="microsoft-smooth-streaming-client-porting-kit-interim-product-license"></a><span data-ttu-id="66985-133">Microsoft Smooth Streaming Client Eksportowanie zestawu przejściowej licencji produktu</span><span class="sxs-lookup"><span data-stu-id="66985-133">Microsoft Smooth Streaming Client Porting Kit Interim Product License</span></span>
<span data-ttu-id="66985-134">W ramach tej licencji, firma Microsoft oferuje Smooth Streaming klienta Eksportowanie zestawu i prawa własności intelektualnej niezbędne do opracować i rozpowszechnić Smooth produktów przejściowej klienta przesyłania strumieniowego innym licencjobiorcom urządzenia Smooth Streaming klienta Eksportowanie zestawu który Dystrybuuj Smooth Streaming klienta produktów końcowych.</span><span class="sxs-lookup"><span data-stu-id="66985-134">Under this license, Microsoft offers a Smooth Streaming Client Porting Kit and the necessary intellectual property rights to develop and distribute Smooth Streaming Client Interim Products to other Smooth Streaming Client Porting Kit device licensees that distribute Smooth Streaming Client Final Products.</span></span>

#### <a name="fee-structure"></a><span data-ttu-id="66985-135">Opłata — struktura</span><span class="sxs-lookup"><span data-stu-id="66985-135">Fee structure</span></span>
<span data-ttu-id="66985-136">Opłata jednorazowej licencji USA $ 50 000 zapewnia dostęp do Smooth Streaming klienta Eksportowanie zestawu.</span><span class="sxs-lookup"><span data-stu-id="66985-136">A U.S. $50,000 one-time license fee provides access to the Smooth Streaming Client Porting Kit.</span></span> 

### <a name="microsoft-smooth-streaming-client-porting-kit-final-product-license"></a><span data-ttu-id="66985-137">Microsoft Smooth Streaming Client Eksportowanie zestawu końcowa licencji produktu</span><span class="sxs-lookup"><span data-stu-id="66985-137">Microsoft Smooth Streaming Client Porting Kit Final Product License</span></span>
<span data-ttu-id="66985-138">W ramach tej licencji firma Microsoft oferuje wszystkie prawa własności intelektualnej niezbędne do odbierania Smooth produktów przejściowej klienta przesyłania strumieniowego z innym licencjobiorcom Smooth Streaming klienta Eksportowanie zestawu oraz do dystrybucji znakowaniem firmowym Smooth Streaming klienta końcowego Produkty dla użytkowników końcowych.</span><span class="sxs-lookup"><span data-stu-id="66985-138">Under this license, Microsoft offers all necessary intellectual property rights to receive Smooth Streaming Client Interim Products from other Smooth Streaming Client Porting Kit licensees and to distribute company-branded Smooth Streaming Client Final Products to end users.</span></span>

#### <a name="fee-structure"></a><span data-ttu-id="66985-139">Opłata — struktura</span><span class="sxs-lookup"><span data-stu-id="66985-139">Fee structure</span></span>
<span data-ttu-id="66985-140">Smooth Streaming klienta produktu końcowego jest oferowanych w ramach jako model licencjonowanych w ramach:</span><span class="sxs-lookup"><span data-stu-id="66985-140">The Smooth Streaming Client Final Product is offered under a royalty model as under:</span></span>

* <span data-ttu-id="66985-141">wysłane 0.10 $ dla wdrożenia urządzenia</span><span class="sxs-lookup"><span data-stu-id="66985-141">$0.10 per device implementation shipped</span></span>
* <span data-ttu-id="66985-142">Licencjonowani jest ograniczone do 50 000 $ każdego roku</span><span class="sxs-lookup"><span data-stu-id="66985-142">The royalty is capped at $50,000 each year</span></span>
* <span data-ttu-id="66985-143">Nie licencjonowanych w pierwszych 10 000 urządzeń implementacji każdego roku</span><span class="sxs-lookup"><span data-stu-id="66985-143">No royalty for first 10,000 device implementations each year</span></span> 

## <a name="licensing-procedure-and-sspk-access"></a><span data-ttu-id="66985-144">Procedurę licencjonowania i SSPK dostępu</span><span class="sxs-lookup"><span data-stu-id="66985-144">Licensing Procedure and SSPK access</span></span>
<span data-ttu-id="66985-145">Wyślij wiadomość e-mail [ sspkinfo@microsoft.com ](mailto:sspkinfo@microsoft.com) dla wszystkich licencjonowania zapytania.</span><span class="sxs-lookup"><span data-stu-id="66985-145">Please email [sspkinfo@microsoft.com](mailto:sspkinfo@microsoft.com) for all licensing queries.</span></span>

<span data-ttu-id="66985-146">[Portal dystrybucji SSPK](https://microsoft.sharepoint.com/teams/SSPKDOWNLOAD/) jest dostępny dla zarejestrowanego licencjobiorców przejściowej.</span><span class="sxs-lookup"><span data-stu-id="66985-146">The [SSPK Distribution portal](https://microsoft.sharepoint.com/teams/SSPKDOWNLOAD/) is accessible to registered Interim licensees.</span></span>

<span data-ttu-id="66985-147">Licencjobiorców przejściowej i końcowe SSPK mogą przesyłać pytania techniczne [ smoothpk@microsoft.com ](mailto:smoothpk@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="66985-147">Interim and Final SSPK licensees can submit technical questions to [smoothpk@microsoft.com](mailto:smoothpk@microsoft.com).</span></span>

## <a name="microsoft-smooth-streaming-client-interim-product-agreement-licensees"></a><span data-ttu-id="66985-148">Microsoft Smooth Streaming licencjobiorców umowy tymczasowe produktu klienta</span><span class="sxs-lookup"><span data-stu-id="66985-148">Microsoft Smooth Streaming Client Interim Product Agreement Licensees</span></span>
* <span data-ttu-id="66985-149">Adroit rozwiązań biznesowych, Inc</span><span class="sxs-lookup"><span data-stu-id="66985-149">Adroit Business Solutions, Inc</span></span>
* <span data-ttu-id="66985-150">Zaawansowane cyfrowy emisji SA</span><span class="sxs-lookup"><span data-stu-id="66985-150">Advanced Digital Broadcast SA</span></span>
* <span data-ttu-id="66985-151">AirTies Kablosuz Iletism Sanayive Dis Ticaret A.S.</span><span class="sxs-lookup"><span data-stu-id="66985-151">AirTies Kablosuz Iletism Sanayive Dis Ticaret A.S.</span></span>
* <span data-ttu-id="66985-152">Albis technologii Ltd.</span><span class="sxs-lookup"><span data-stu-id="66985-152">Albis Technologies Ltd.</span></span>
* <span data-ttu-id="66985-153">Alticast Corporation</span><span class="sxs-lookup"><span data-stu-id="66985-153">Alticast Corporation</span></span>
* <span data-ttu-id="66985-154">Cyfrowy Amazon usług, Inc.</span><span class="sxs-lookup"><span data-stu-id="66985-154">Amazon Digital Services, Inc.</span></span>
* <span data-ttu-id="66985-155">Technologia Arion, Inc.</span><span class="sxs-lookup"><span data-stu-id="66985-155">Arion Technology, Inc.</span></span>
* <span data-ttu-id="66985-156">Oprogramowanie Multimedia AVC Company, Ltd.</span><span class="sxs-lookup"><span data-stu-id="66985-156">AVC Multimedia Software Co., Ltd.</span></span>
* <span data-ttu-id="66985-157">Cavium, Inc.</span><span class="sxs-lookup"><span data-stu-id="66985-157">Cavium, Inc.</span></span>
* <span data-ttu-id="66985-158">EchoStar Corporation zakupu</span><span class="sxs-lookup"><span data-stu-id="66985-158">EchoStar Purchasing Corporation</span></span>
* <span data-ttu-id="66985-159">Enseo, Inc.</span><span class="sxs-lookup"><span data-stu-id="66985-159">Enseo, Inc.</span></span>
* <span data-ttu-id="66985-160">Fluendo SA</span><span class="sxs-lookup"><span data-stu-id="66985-160">Fluendo S.A.</span></span>
* <span data-ttu-id="66985-161">BroadInfoCom HANDAN Company, Ltd.</span><span class="sxs-lookup"><span data-stu-id="66985-161">HANDAN BroadInfoCom Co., Ltd.</span></span>
* <span data-ttu-id="66985-162">Infomir GMBH</span><span class="sxs-lookup"><span data-stu-id="66985-162">Infomir GMBH</span></span>
* <span data-ttu-id="66985-163">Irdeto USA Inc.</span><span class="sxs-lookup"><span data-stu-id="66985-163">Irdeto USA Inc.</span></span>
* <span data-ttu-id="66985-164">iWEDIA SA</span><span class="sxs-lookup"><span data-stu-id="66985-164">iWEDIA S.A.</span></span> 
* <span data-ttu-id="66985-165">Liberty globalne BV usług</span><span class="sxs-lookup"><span data-stu-id="66985-165">Liberty Global Services BV</span></span>
* <span data-ttu-id="66985-166">MediaTek Inc.</span><span class="sxs-lookup"><span data-stu-id="66985-166">MediaTek Inc.</span></span>
* <span data-ttu-id="66985-167">MStar Co, Ltd.</span><span class="sxs-lookup"><span data-stu-id="66985-167">MStar Co, Ltd</span></span>
* <span data-ttu-id="66985-168">Nintendo Company, Ltd.</span><span class="sxs-lookup"><span data-stu-id="66985-168">Nintendo Co., Ltd.</span></span>
* <span data-ttu-id="66985-169">OpenTV, Inc.</span><span class="sxs-lookup"><span data-stu-id="66985-169">OpenTV, Inc.</span></span>
* <span data-ttu-id="66985-170">Ograniczone cyfrowy szafran</span><span class="sxs-lookup"><span data-stu-id="66985-170">Saffron Digital Limited</span></span>
* <span data-ttu-id="66985-171">Elektrycznego Changhong prowincji Syczuan Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="66985-171">Sichuan Changhong Electric Co., Ltd</span></span>
* <span data-ttu-id="66985-172">SoftAtHome</span><span class="sxs-lookup"><span data-stu-id="66985-172">SoftAtHome</span></span>
* <span data-ttu-id="66985-173">Sony Corporation</span><span class="sxs-lookup"><span data-stu-id="66985-173">Sony Corporation</span></span>
* <span data-ttu-id="66985-174">Tatung technologii Inc.</span><span class="sxs-lookup"><span data-stu-id="66985-174">Tatung Technology Inc.</span></span>
* <span data-ttu-id="66985-175">Electronics Technoly (Huizhou) TCL Company, Ltd.</span><span class="sxs-lookup"><span data-stu-id="66985-175">TCL Technoly Electronics (Huizhou) Co., Ltd.</span></span>
* <span data-ttu-id="66985-176">TOP zwycięstwa inwestycji, Ltd.</span><span class="sxs-lookup"><span data-stu-id="66985-176">Top Victory Investments, Ltd.</span></span>
* <span data-ttu-id="66985-177">Pisz Vestel Elektronik Sanayi Ticaret A.S.</span><span class="sxs-lookup"><span data-stu-id="66985-177">Vestel Elektronik Sanayi ve Ticaret A.S.</span></span>
* <span data-ttu-id="66985-178">VisualOn, Inc.</span><span class="sxs-lookup"><span data-stu-id="66985-178">VisualOn, Inc.</span></span>
* <span data-ttu-id="66985-179">ZTE Corporation</span><span class="sxs-lookup"><span data-stu-id="66985-179">ZTE Corporation</span></span>

## <a name="microsoft-smooth-streaming-client-final-product-agreement-licensees"></a><span data-ttu-id="66985-180">Microsoft Smooth Streaming licencjobiorców umowy produktu końcowego klienta</span><span class="sxs-lookup"><span data-stu-id="66985-180">Microsoft Smooth Streaming Client Final Product Agreement Licensees</span></span>
* <span data-ttu-id="66985-181">Zaawansowane cyfrowy emisji SA</span><span class="sxs-lookup"><span data-stu-id="66985-181">Advanced Digital Broadcast SA</span></span>
* <span data-ttu-id="66985-182">AirTies Kablosuz Iletism Sanayive Dis Ticaret A.S.</span><span class="sxs-lookup"><span data-stu-id="66985-182">AirTies Kablosuz Iletism Sanayive Dis Ticaret A.S.</span></span>
* <span data-ttu-id="66985-183">Albis technologii Ltd.</span><span class="sxs-lookup"><span data-stu-id="66985-183">Albis Technologies Ltd.</span></span>
* <span data-ttu-id="66985-184">Cyfrowy Amazon usług, Inc.</span><span class="sxs-lookup"><span data-stu-id="66985-184">Amazon Digital Services, Inc.</span></span>
* <span data-ttu-id="66985-185">Technologia AmTRAN Company, Ltd.</span><span class="sxs-lookup"><span data-stu-id="66985-185">AmTRAN Technology Co., Ltd.</span></span>
* <span data-ttu-id="66985-186">Arcadyan technologii Corporation</span><span class="sxs-lookup"><span data-stu-id="66985-186">Arcadyan Technology Corporation</span></span>
* <span data-ttu-id="66985-187">Technologia Arion, Inc.</span><span class="sxs-lookup"><span data-stu-id="66985-187">Arion Technology, Inc.</span></span>
* <span data-ttu-id="66985-188">ATMACA ELEKTRONİK SIECI SAN.</span><span class="sxs-lookup"><span data-stu-id="66985-188">ATMACA ELEKTRONİK SAN.</span></span> <span data-ttu-id="66985-189">PISZ TİC.</span><span class="sxs-lookup"><span data-stu-id="66985-189">VE TİC.</span></span> <span data-ttu-id="66985-190">A.Ş</span><span class="sxs-lookup"><span data-stu-id="66985-190">A.Ş</span></span>
* <span data-ttu-id="66985-191">Brytyjskie niebo emisji ograniczone</span><span class="sxs-lookup"><span data-stu-id="66985-191">British Sky Broadcasting Limited</span></span>
* <span data-ttu-id="66985-192">Technologia CastPal, Inc., Shenzhen</span><span class="sxs-lookup"><span data-stu-id="66985-192">CastPal Technology Inc., Shenzhen</span></span>
* <span data-ttu-id="66985-193">Compal Electronics, Inc.</span><span class="sxs-lookup"><span data-stu-id="66985-193">Compal Electronics, Inc.</span></span>
* <span data-ttu-id="66985-194">Dongguan cyfrowy AV technologii Corp., Ltd.</span><span class="sxs-lookup"><span data-stu-id="66985-194">Dongguan Digital AV Technology Corp., Ltd.</span></span>
* <span data-ttu-id="66985-195">EchoStar Corporation zakupu</span><span class="sxs-lookup"><span data-stu-id="66985-195">EchoStar Purchasing Corporation</span></span>
* <span data-ttu-id="66985-196">Enseo, Inc.</span><span class="sxs-lookup"><span data-stu-id="66985-196">Enseo, Inc.</span></span>
* <span data-ttu-id="66985-197">Ograniczone filmów Filmflex</span><span class="sxs-lookup"><span data-stu-id="66985-197">Filmflex Movies Limited</span></span>
* <span data-ttu-id="66985-198">Fluendo SA</span><span class="sxs-lookup"><span data-stu-id="66985-198">Fluendo S.A.</span></span>
* <span data-ttu-id="66985-199">Ograniczone innowacje Gibson</span><span class="sxs-lookup"><span data-stu-id="66985-199">Gibson Innovations Limited</span></span>
* <span data-ttu-id="66985-200">Haier informacji Applicantion S.R.L</span><span class="sxs-lookup"><span data-stu-id="66985-200">Haier Information Applicantion S.R.L</span></span>
* <span data-ttu-id="66985-201">BroadInfoCom HANDAN Company, Ltd.</span><span class="sxs-lookup"><span data-stu-id="66985-201">HANDAN BroadInfoCom Co., Ltd.</span></span>
* <span data-ttu-id="66985-202">Międzynarodowe Hisense Company, Ltd.</span><span class="sxs-lookup"><span data-stu-id="66985-202">Hisense International Co., Ltd.</span></span> 
* <span data-ttu-id="66985-203">Homecast Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="66985-203">Homecast Co.,Ltd</span></span>
* <span data-ttu-id="66985-204">HON Hai dokładności branży Company, Ltd.</span><span class="sxs-lookup"><span data-stu-id="66985-204">Hon Hai Precision Industry Co., Ltd.</span></span>
* <span data-ttu-id="66985-205">Infomir GMBH</span><span class="sxs-lookup"><span data-stu-id="66985-205">Infomir GMBH</span></span>
* <span data-ttu-id="66985-206">Kaonmedia Company, Ltd.</span><span class="sxs-lookup"><span data-stu-id="66985-206">Kaonmedia Co., Ltd.</span></span>
* <span data-ttu-id="66985-207">KDDI Corporation</span><span class="sxs-lookup"><span data-stu-id="66985-207">KDDI Corporation</span></span>
* <span data-ttu-id="66985-208">Nintendo Company, Ltd.</span><span class="sxs-lookup"><span data-stu-id="66985-208">Nintendo Co., Ltd.</span></span>
* <span data-ttu-id="66985-209">Kolor pomarańczowy SA</span><span class="sxs-lookup"><span data-stu-id="66985-209">Orange SA</span></span>
* <span data-ttu-id="66985-210">Ograniczone cyfrowy szafran</span><span class="sxs-lookup"><span data-stu-id="66985-210">Saffron Digital Limited</span></span>
* <span data-ttu-id="66985-211">Połączenie szerokopasmowe Sagemcom SAS</span><span class="sxs-lookup"><span data-stu-id="66985-211">Sagemcom Broadband SAS</span></span>
* <span data-ttu-id="66985-212">Shenzhen Coship Electronics CO., Ltd.</span><span class="sxs-lookup"><span data-stu-id="66985-212">Shenzhen Coship Electronics CO., LTD</span></span>
* <span data-ttu-id="66985-213">Elektrycznego Jiuzhou Shenzhen Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="66985-213">Shenzhen Jiuzhou Electric Co.,Ltd</span></span>
* <span data-ttu-id="66985-214">Shenzhen Skyworth cyfrowy technologii Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="66985-214">Shenzhen Skyworth Digital Technology Co., Ltd</span></span>
* <span data-ttu-id="66985-215">Elektrycznego Changhong prowincji Syczuan Company, Ltd.</span><span class="sxs-lookup"><span data-stu-id="66985-215">Sichuan Changhong Electric Co., Ltd.</span></span>
* <span data-ttu-id="66985-216">Skardin przemysłowej Corp.</span><span class="sxs-lookup"><span data-stu-id="66985-216">Skardin Industrial Corp.</span></span>
* <span data-ttu-id="66985-217">Niebo Deutschland Fernsehen GmbH & Co. KG</span><span class="sxs-lookup"><span data-stu-id="66985-217">Sky Deutschland Fernsehen GmbH & Co. KG</span></span>
* <span data-ttu-id="66985-218">SmarDTV SA</span><span class="sxs-lookup"><span data-stu-id="66985-218">SmarDTV S.A.</span></span>
* <span data-ttu-id="66985-219">SoftAtHome</span><span class="sxs-lookup"><span data-stu-id="66985-219">SoftAtHome</span></span>
* <span data-ttu-id="66985-220">Sony Corporation</span><span class="sxs-lookup"><span data-stu-id="66985-220">Sony Corporation</span></span>
* <span data-ttu-id="66985-221">Ograniczone TCL zamorskich Marketing (urządzeniach oddalonych od brzegu komercyjnej Makau SAR)</span><span class="sxs-lookup"><span data-stu-id="66985-221">TCL Overseas Marketing (Macao Commercial Offshore) Limited</span></span>
* <span data-ttu-id="66985-222">Technicolor dostarczanie technologii, SAS</span><span class="sxs-lookup"><span data-stu-id="66985-222">Technicolor Delivery Technologies, SAS</span></span>
* <span data-ttu-id="66985-223">Tongfang Ltd. globalne</span><span class="sxs-lookup"><span data-stu-id="66985-223">Tongfang Global Ltd.</span></span>
* <span data-ttu-id="66985-224">TOP zwycięstwa inwestycji, Ltd.</span><span class="sxs-lookup"><span data-stu-id="66985-224">Top Victory Investments, Ltd.</span></span>
* <span data-ttu-id="66985-225">Toshiba Lifestyle produktów i usług firma</span><span class="sxs-lookup"><span data-stu-id="66985-225">Toshiba Lifestyle Products & Services Corporation</span></span>
* <span data-ttu-id="66985-226">S.r.o. /Slovakia/ uniwersalnej Corporation nośnika</span><span class="sxs-lookup"><span data-stu-id="66985-226">Universal Media Corporation /Slovakia/ s.r.o.</span></span>
* <span data-ttu-id="66985-227">VIZIO, Inc.</span><span class="sxs-lookup"><span data-stu-id="66985-227">VIZIO, Inc.</span></span>
* <span data-ttu-id="66985-228">Wistron Corporation</span><span class="sxs-lookup"><span data-stu-id="66985-228">Wistron Corporation</span></span>
* <span data-ttu-id="66985-229">ZTE Corporation</span><span class="sxs-lookup"><span data-stu-id="66985-229">ZTE Corporation</span></span>


## <a name="media-services-learning-paths"></a><span data-ttu-id="66985-230">Ścieżki szkoleniowe dotyczące usługi Media Services</span><span class="sxs-lookup"><span data-stu-id="66985-230">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="66985-231">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="66985-231">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

