---
title: "aaaLicensing Microsoft® Smooth Streaming klienta Eksportowanie zestawu"
description: "Więcej informacji na temat sposobu toolicensing hello Microsoft® Smooth Streaming klienta Eksportowanie zestawu."
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
ms.openlocfilehash: 56c3dccda73dd02207bb4dbe8109ba6fda917a6b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="licensing-microsoft-smooth-streaming-client-porting-kit"></a><span data-ttu-id="06987-103">Licencjonowania Microsoft® Smooth Streaming Client Eksportowanie zestawu</span><span class="sxs-lookup"><span data-stu-id="06987-103">Licensing Microsoft® Smooth Streaming Client Porting Kit</span></span>
## <a name="overview"></a><span data-ttu-id="06987-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="06987-104">Overview</span></span>
<span data-ttu-id="06987-105">Microsoft Smooth Streaming klienta Eksportowanie zestawu (**SSPK** skrócie) jest Smooth Streaming implementacji klienta, który jest zoptymalizowany toohelp osadzonych producentów, kabel i operatorów komórkowych, zawartości usługodawcy, słuchawki producenci, niezależnym dostawcom oprogramowania (ISV) i rozwiązania dostawców toocreate produktów i usług do przesyłania strumieniowego z adaptacyjną przesyłania strumieniowego zawartości w formacie Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="06987-105">Microsoft Smooth Streaming Client Porting Kit (**SSPK** for short) is a Smooth Streaming client implementation that is optimized toohelp embedded device manufacturers, cable and mobile operators, content service providers, handset manufacturers, independent software vendors (ISVs), and solution providers toocreate products and services for streaming adaptive streaming content in Smooth Streaming format.</span></span> <span data-ttu-id="06987-106">SSPK jest platforma i urządzenie niezależnie od implementacji klienta Smooth Streaming, które mogą być przenoszone hello Licencjobiorcy tooany urządzeń i platform.</span><span class="sxs-lookup"><span data-stu-id="06987-106">SSPK is a device and platform independent implementation of Smooth Streaming client that can be ported by hello licensee tooany device and platform.</span></span> 

<span data-ttu-id="06987-107">Przedstawionym poniżej jest Architektura wysokiego poziomu, a pole IIS Smooth Streaming Eksportowanie zestawu jest obsługiwane przez firmę Microsoft implementacją Smooth Streaming Client hello zawiera całą logikę core hello do odtwarzania zawartości Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="06987-107">Included below is a high level architecture and IIS Smooth Streaming Porting Kit box is hello Smooth Streaming Client implementation provided by Microsoft and includes all hello core logic for playback of Smooth Streaming content.</span></span> <span data-ttu-id="06987-108">Jest to następnie przenoszone przez partnerów dla określonego urządzenia lub platformy zaimplementowanie odpowiednich interfejsów.</span><span class="sxs-lookup"><span data-stu-id="06987-108">This is then ported by partners for a specific device or platform by implementing appropriate interfaces.</span></span> 

![SSPK](./media/media-services-sspk/sspk-arch.png)

## <a name="description"></a><span data-ttu-id="06987-110">Opis</span><span class="sxs-lookup"><span data-stu-id="06987-110">Description</span></span>
<span data-ttu-id="06987-111">SSPK jest licencjonowana na warunkach, które oferuje doskonałą biznesu.</span><span class="sxs-lookup"><span data-stu-id="06987-111">SSPK is licensed on terms that offer excellent business value.</span></span> <span data-ttu-id="06987-112">Licencja SSPK zapewnia branży hello:</span><span class="sxs-lookup"><span data-stu-id="06987-112">SSPK license provides hello industry with:</span></span>

* <span data-ttu-id="06987-113">Smooth Streaming Eksportowanie zestawu źródła w języku C++</span><span class="sxs-lookup"><span data-stu-id="06987-113">Smooth Streaming Porting Kit source in C++</span></span> 
  * <span data-ttu-id="06987-114">implementuje funkcje Smooth Streaming Client</span><span class="sxs-lookup"><span data-stu-id="06987-114">implements Smooth Streaming Client functionality</span></span>
  * <span data-ttu-id="06987-115">dodaje format analizowania heurystyki buforowanie logiki itp.</span><span class="sxs-lookup"><span data-stu-id="06987-115">adds format parsing, heuristics, buffering logic, etc.</span></span>
* <span data-ttu-id="06987-116">Aplikacja odtwarzacza interfejsów API</span><span class="sxs-lookup"><span data-stu-id="06987-116">Player application APIs</span></span> 
  * <span data-ttu-id="06987-117">interfejsy programowania do interakcji z aplikacją media player</span><span class="sxs-lookup"><span data-stu-id="06987-117">programming interfaces for interaction with a media player application</span></span>
* <span data-ttu-id="06987-118">Interfejs (PAL) warstwy abstrakcji platformy</span><span class="sxs-lookup"><span data-stu-id="06987-118">Platform Abstraction Layer (PAL) Interface</span></span> 
  * <span data-ttu-id="06987-119">interfejsy programowania do interakcji z systemem operacyjnym hello (wątki, sockets)</span><span class="sxs-lookup"><span data-stu-id="06987-119">programming interfaces for interaction with hello operating system (threads, sockets)</span></span>
* <span data-ttu-id="06987-120">Interfejs (HAL) warstwy abstrakcji sprzętu</span><span class="sxs-lookup"><span data-stu-id="06987-120">Hardware Abstraction Layer (HAL) Interface</span></span> 
  * <span data-ttu-id="06987-121">interfejsy do interakcji z urządzenia, A / V dekodery (dekodowania, renderowania)</span><span class="sxs-lookup"><span data-stu-id="06987-121">programming interfaces for interaction with hardware A/V decoders (decoding, rendering)</span></span>
* <span data-ttu-id="06987-122">Interfejs zarządzania (prawami cyfrowymi DRM) prawami cyfrowymi</span><span class="sxs-lookup"><span data-stu-id="06987-122">Digital Rights Management (DRM) Interface</span></span> 
  * <span data-ttu-id="06987-123">interfejsy programowania obsługi DRM za pośrednictwem hello warstwę abstrakcji DRM (DAL)</span><span class="sxs-lookup"><span data-stu-id="06987-123">programming interfaces for handling DRM through hello DRM Abstraction Layer (DAL)</span></span>
  * <span data-ttu-id="06987-124">Microsoft PlayReady eksportowanie Kit jest dostarczany oddzielnie, ale integruje się za pośrednictwem tego interfejsu.</span><span class="sxs-lookup"><span data-stu-id="06987-124">Microsoft PlayReady Porting Kit ships separately but integrates through this interface.</span></span> <span data-ttu-id="06987-125">Więcej szczegółów dotyczących licencji firmy Microsoft PlayReady Device, kliknij przycisk [tutaj](http://www.microsoft.com/playready/licensing/device_technology.mspx#pddipdl).</span><span class="sxs-lookup"><span data-stu-id="06987-125">For more details on Microsoft PlayReady Device licensing, click [here](http://www.microsoft.com/playready/licensing/device_technology.mspx#pddipdl).</span></span>
* <span data-ttu-id="06987-126">Przykłady implementacji</span><span class="sxs-lookup"><span data-stu-id="06987-126">Implementation samples</span></span> 
  * <span data-ttu-id="06987-127">Przykładowe zastosowanie PAL dla systemu Linux</span><span class="sxs-lookup"><span data-stu-id="06987-127">sample PAL implementation for Linux</span></span>
  * <span data-ttu-id="06987-128">Przykładowe zastosowanie HAL dla GStreamer</span><span class="sxs-lookup"><span data-stu-id="06987-128">sample HAL implementation for GStreamer</span></span>

## <a name="licensing-options"></a><span data-ttu-id="06987-129">Opcje licencjonowania</span><span class="sxs-lookup"><span data-stu-id="06987-129">Licensing Options</span></span>
<span data-ttu-id="06987-130">Microsoft Smooth Streaming klienta eksportowanie Kit jest dokonane toolicensees dostępne w dwóch umów licencyjnych distinct: jeden dla rozwoju Smooth produktów przejściowej klienta przesyłania strumieniowego i drugi dla dystrybucji Smooth Streaming klienta produktów końcowych tooend użytkowników.</span><span class="sxs-lookup"><span data-stu-id="06987-130">Microsoft Smooth Streaming Client Porting Kit is made available toolicensees under two distinct license agreements: one for developing Smooth Streaming Client Interim Products and another for distributing Smooth Streaming Client Final Products tooend users.</span></span>

* <span data-ttu-id="06987-131">Mikroukładem producentów, niezależnie od oprogramowania i integratorów systemów. platforma dostawcy (ISV), którzy potrzebują Eksportowanie kodu źródłowego zestaw toodevelop produktów przejściowej Microsoft Smooth Streaming klienta Eksportowanie zestawu **licencji produktu przejściowej** powinien być wykonywany.</span><span class="sxs-lookup"><span data-stu-id="06987-131">For chipset manufacturers, system integrators, or independent software vendors (ISVs) who require a source code porting kit toodevelop Interim Products, a Microsoft Smooth Streaming Client Porting Kit **Interim Product License** should be executed.</span></span>
* <span data-ttu-id="06987-132">Dla producentów lub niezależnym dostawcom oprogramowania wymagających praw dystrybucji dla użytkowników tooend Smooth Streaming klienta produktów końcowych, hello Microsoft Smooth Streaming klienta Eksportowanie zestawu **końcowej licencji produktu** mają zostać wykonane.</span><span class="sxs-lookup"><span data-stu-id="06987-132">For device manufacturers or ISVs who require distribution rights for Smooth Streaming Client Final Products tooend users, hello Microsoft Smooth Streaming Client Porting Kit **Final Product License** should be executed.</span></span>

### <a name="microsoft-smooth-streaming-client-porting-kit-interim-product-license"></a><span data-ttu-id="06987-133">Microsoft Smooth Streaming Client Eksportowanie zestawu przejściowej licencji produktu</span><span class="sxs-lookup"><span data-stu-id="06987-133">Microsoft Smooth Streaming Client Porting Kit Interim Product License</span></span>
<span data-ttu-id="06987-134">W ramach tej licencji firmy Microsoft oferuje Smooth Streaming klienta Eksportowanie zestawu hello toodevelop prawa własności intelektualnej niezbędne i dystrybuować Smooth produktów przejściowej klienta przesyłania strumieniowego tooother Smooth Streaming klienta Eksportowanie zestawu urządzeń licencjobiorców który Dystrybuuj Smooth Streaming klienta produktów końcowych.</span><span class="sxs-lookup"><span data-stu-id="06987-134">Under this license, Microsoft offers a Smooth Streaming Client Porting Kit and hello necessary intellectual property rights toodevelop and distribute Smooth Streaming Client Interim Products tooother Smooth Streaming Client Porting Kit device licensees that distribute Smooth Streaming Client Final Products.</span></span>

#### <a name="fee-structure"></a><span data-ttu-id="06987-135">Opłata — struktura</span><span class="sxs-lookup"><span data-stu-id="06987-135">Fee structure</span></span>
<span data-ttu-id="06987-136">Opłata jednorazowej licencji USA $ 50 000 zapewnia dostęp toohello Smooth Streaming klienta Eksportowanie zestawu.</span><span class="sxs-lookup"><span data-stu-id="06987-136">A U.S. $50,000 one-time license fee provides access toohello Smooth Streaming Client Porting Kit.</span></span> 

### <a name="microsoft-smooth-streaming-client-porting-kit-final-product-license"></a><span data-ttu-id="06987-137">Microsoft Smooth Streaming Client Eksportowanie zestawu końcowa licencji produktu</span><span class="sxs-lookup"><span data-stu-id="06987-137">Microsoft Smooth Streaming Client Porting Kit Final Product License</span></span>
<span data-ttu-id="06987-138">W ramach tej licencji firma Microsoft oferuje wszystkie niezbędne tooreceive prawa własności intelektualnej Smooth produktów przejściowej klienta przesyłania strumieniowego z innych licencjobiorców Smooth Streaming klienta Eksportowanie zestawu i toodistribute znakowaniem firmowym Smooth Streaming klienta końcowego Użytkownicy tooend produktów.</span><span class="sxs-lookup"><span data-stu-id="06987-138">Under this license, Microsoft offers all necessary intellectual property rights tooreceive Smooth Streaming Client Interim Products from other Smooth Streaming Client Porting Kit licensees and toodistribute company-branded Smooth Streaming Client Final Products tooend users.</span></span>

#### <a name="fee-structure"></a><span data-ttu-id="06987-139">Opłata — struktura</span><span class="sxs-lookup"><span data-stu-id="06987-139">Fee structure</span></span>
<span data-ttu-id="06987-140">Witaj Smooth Streaming klienta produktu końcowego jest oferowanych w ramach jako model licencjonowanych w ramach:</span><span class="sxs-lookup"><span data-stu-id="06987-140">hello Smooth Streaming Client Final Product is offered under a royalty model as under:</span></span>

* <span data-ttu-id="06987-141">wysłane 0.10 $ dla wdrożenia urządzenia</span><span class="sxs-lookup"><span data-stu-id="06987-141">$0.10 per device implementation shipped</span></span>
* <span data-ttu-id="06987-142">Licencjonowani Hello jest ograniczone do 50 000 $ każdego roku</span><span class="sxs-lookup"><span data-stu-id="06987-142">hello royalty is capped at $50,000 each year</span></span>
* <span data-ttu-id="06987-143">Nie licencjonowanych w pierwszych 10 000 urządzeń implementacji każdego roku</span><span class="sxs-lookup"><span data-stu-id="06987-143">No royalty for first 10,000 device implementations each year</span></span> 

## <a name="licensing-procedure-and-sspk-access"></a><span data-ttu-id="06987-144">Procedurę licencjonowania i SSPK dostępu</span><span class="sxs-lookup"><span data-stu-id="06987-144">Licensing Procedure and SSPK access</span></span>
<span data-ttu-id="06987-145">Wyślij wiadomość e-mail [ sspkinfo@microsoft.com ](mailto:sspkinfo@microsoft.com) dla wszystkich licencjonowania zapytania.</span><span class="sxs-lookup"><span data-stu-id="06987-145">Please email [sspkinfo@microsoft.com](mailto:sspkinfo@microsoft.com) for all licensing queries.</span></span>

<span data-ttu-id="06987-146">Witaj [portal dystrybucji SSPK](https://microsoft.sharepoint.com/teams/SSPKDOWNLOAD/) jest dostępny tooregistered licencjobiorców przejściowej.</span><span class="sxs-lookup"><span data-stu-id="06987-146">hello [SSPK Distribution portal](https://microsoft.sharepoint.com/teams/SSPKDOWNLOAD/) is accessible tooregistered Interim licensees.</span></span>

<span data-ttu-id="06987-147">Licencjobiorców przejściowej i końcowe SSPK mogą przesyłać pytania techniczne zbyt[smoothpk@microsoft.com](mailto:smoothpk@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="06987-147">Interim and Final SSPK licensees can submit technical questions too[smoothpk@microsoft.com](mailto:smoothpk@microsoft.com).</span></span>

## <a name="microsoft-smooth-streaming-client-interim-product-agreement-licensees"></a><span data-ttu-id="06987-148">Microsoft Smooth Streaming licencjobiorców umowy tymczasowe produktu klienta</span><span class="sxs-lookup"><span data-stu-id="06987-148">Microsoft Smooth Streaming Client Interim Product Agreement Licensees</span></span>
* <span data-ttu-id="06987-149">Adroit rozwiązań biznesowych, Inc</span><span class="sxs-lookup"><span data-stu-id="06987-149">Adroit Business Solutions, Inc</span></span>
* <span data-ttu-id="06987-150">Zaawansowane cyfrowy emisji SA</span><span class="sxs-lookup"><span data-stu-id="06987-150">Advanced Digital Broadcast SA</span></span>
* <span data-ttu-id="06987-151">AirTies Kablosuz Iletism Sanayive Dis Ticaret A.S.</span><span class="sxs-lookup"><span data-stu-id="06987-151">AirTies Kablosuz Iletism Sanayive Dis Ticaret A.S.</span></span>
* <span data-ttu-id="06987-152">Albis technologii Ltd.</span><span class="sxs-lookup"><span data-stu-id="06987-152">Albis Technologies Ltd.</span></span>
* <span data-ttu-id="06987-153">Alticast Corporation</span><span class="sxs-lookup"><span data-stu-id="06987-153">Alticast Corporation</span></span>
* <span data-ttu-id="06987-154">Cyfrowy Amazon usług, Inc.</span><span class="sxs-lookup"><span data-stu-id="06987-154">Amazon Digital Services, Inc.</span></span>
* <span data-ttu-id="06987-155">Technologia Arion, Inc.</span><span class="sxs-lookup"><span data-stu-id="06987-155">Arion Technology, Inc.</span></span>
* <span data-ttu-id="06987-156">Oprogramowanie Multimedia AVC Company, Ltd.</span><span class="sxs-lookup"><span data-stu-id="06987-156">AVC Multimedia Software Co., Ltd.</span></span>
* <span data-ttu-id="06987-157">Cavium, Inc.</span><span class="sxs-lookup"><span data-stu-id="06987-157">Cavium, Inc.</span></span>
* <span data-ttu-id="06987-158">EchoStar Corporation zakupu</span><span class="sxs-lookup"><span data-stu-id="06987-158">EchoStar Purchasing Corporation</span></span>
* <span data-ttu-id="06987-159">Enseo, Inc.</span><span class="sxs-lookup"><span data-stu-id="06987-159">Enseo, Inc.</span></span>
* <span data-ttu-id="06987-160">Fluendo SA</span><span class="sxs-lookup"><span data-stu-id="06987-160">Fluendo S.A.</span></span>
* <span data-ttu-id="06987-161">BroadInfoCom HANDAN Company, Ltd.</span><span class="sxs-lookup"><span data-stu-id="06987-161">HANDAN BroadInfoCom Co., Ltd.</span></span>
* <span data-ttu-id="06987-162">Infomir GMBH</span><span class="sxs-lookup"><span data-stu-id="06987-162">Infomir GMBH</span></span>
* <span data-ttu-id="06987-163">Irdeto USA Inc.</span><span class="sxs-lookup"><span data-stu-id="06987-163">Irdeto USA Inc.</span></span>
* <span data-ttu-id="06987-164">iWEDIA SA</span><span class="sxs-lookup"><span data-stu-id="06987-164">iWEDIA S.A.</span></span> 
* <span data-ttu-id="06987-165">Liberty globalne BV usług</span><span class="sxs-lookup"><span data-stu-id="06987-165">Liberty Global Services BV</span></span>
* <span data-ttu-id="06987-166">MediaTek Inc.</span><span class="sxs-lookup"><span data-stu-id="06987-166">MediaTek Inc.</span></span>
* <span data-ttu-id="06987-167">MStar Co, Ltd.</span><span class="sxs-lookup"><span data-stu-id="06987-167">MStar Co, Ltd</span></span>
* <span data-ttu-id="06987-168">Nintendo Company, Ltd.</span><span class="sxs-lookup"><span data-stu-id="06987-168">Nintendo Co., Ltd.</span></span>
* <span data-ttu-id="06987-169">OpenTV, Inc.</span><span class="sxs-lookup"><span data-stu-id="06987-169">OpenTV, Inc.</span></span>
* <span data-ttu-id="06987-170">Ograniczone cyfrowy szafran</span><span class="sxs-lookup"><span data-stu-id="06987-170">Saffron Digital Limited</span></span>
* <span data-ttu-id="06987-171">Elektrycznego Changhong prowincji Syczuan Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="06987-171">Sichuan Changhong Electric Co., Ltd</span></span>
* <span data-ttu-id="06987-172">SoftAtHome</span><span class="sxs-lookup"><span data-stu-id="06987-172">SoftAtHome</span></span>
* <span data-ttu-id="06987-173">Sony Corporation</span><span class="sxs-lookup"><span data-stu-id="06987-173">Sony Corporation</span></span>
* <span data-ttu-id="06987-174">Tatung technologii Inc.</span><span class="sxs-lookup"><span data-stu-id="06987-174">Tatung Technology Inc.</span></span>
* <span data-ttu-id="06987-175">Electronics Technoly (Huizhou) TCL Company, Ltd.</span><span class="sxs-lookup"><span data-stu-id="06987-175">TCL Technoly Electronics (Huizhou) Co., Ltd.</span></span>
* <span data-ttu-id="06987-176">TOP zwycięstwa inwestycji, Ltd.</span><span class="sxs-lookup"><span data-stu-id="06987-176">Top Victory Investments, Ltd.</span></span>
* <span data-ttu-id="06987-177">Pisz Vestel Elektronik Sanayi Ticaret A.S.</span><span class="sxs-lookup"><span data-stu-id="06987-177">Vestel Elektronik Sanayi ve Ticaret A.S.</span></span>
* <span data-ttu-id="06987-178">VisualOn, Inc.</span><span class="sxs-lookup"><span data-stu-id="06987-178">VisualOn, Inc.</span></span>
* <span data-ttu-id="06987-179">ZTE Corporation</span><span class="sxs-lookup"><span data-stu-id="06987-179">ZTE Corporation</span></span>

## <a name="microsoft-smooth-streaming-client-final-product-agreement-licensees"></a><span data-ttu-id="06987-180">Microsoft Smooth Streaming licencjobiorców umowy produktu końcowego klienta</span><span class="sxs-lookup"><span data-stu-id="06987-180">Microsoft Smooth Streaming Client Final Product Agreement Licensees</span></span>
* <span data-ttu-id="06987-181">Zaawansowane cyfrowy emisji SA</span><span class="sxs-lookup"><span data-stu-id="06987-181">Advanced Digital Broadcast SA</span></span>
* <span data-ttu-id="06987-182">AirTies Kablosuz Iletism Sanayive Dis Ticaret A.S.</span><span class="sxs-lookup"><span data-stu-id="06987-182">AirTies Kablosuz Iletism Sanayive Dis Ticaret A.S.</span></span>
* <span data-ttu-id="06987-183">Albis technologii Ltd.</span><span class="sxs-lookup"><span data-stu-id="06987-183">Albis Technologies Ltd.</span></span>
* <span data-ttu-id="06987-184">Cyfrowy Amazon usług, Inc.</span><span class="sxs-lookup"><span data-stu-id="06987-184">Amazon Digital Services, Inc.</span></span>
* <span data-ttu-id="06987-185">Technologia AmTRAN Company, Ltd.</span><span class="sxs-lookup"><span data-stu-id="06987-185">AmTRAN Technology Co., Ltd.</span></span>
* <span data-ttu-id="06987-186">Arcadyan technologii Corporation</span><span class="sxs-lookup"><span data-stu-id="06987-186">Arcadyan Technology Corporation</span></span>
* <span data-ttu-id="06987-187">Technologia Arion, Inc.</span><span class="sxs-lookup"><span data-stu-id="06987-187">Arion Technology, Inc.</span></span>
* <span data-ttu-id="06987-188">ATMACA ELEKTRONİK SIECI SAN.</span><span class="sxs-lookup"><span data-stu-id="06987-188">ATMACA ELEKTRONİK SAN.</span></span> <span data-ttu-id="06987-189">PISZ TİC.</span><span class="sxs-lookup"><span data-stu-id="06987-189">VE TİC.</span></span> <span data-ttu-id="06987-190">A.Ş</span><span class="sxs-lookup"><span data-stu-id="06987-190">A.Ş</span></span>
* <span data-ttu-id="06987-191">Brytyjskie niebo emisji ograniczone</span><span class="sxs-lookup"><span data-stu-id="06987-191">British Sky Broadcasting Limited</span></span>
* <span data-ttu-id="06987-192">Technologia CastPal, Inc., Shenzhen</span><span class="sxs-lookup"><span data-stu-id="06987-192">CastPal Technology Inc., Shenzhen</span></span>
* <span data-ttu-id="06987-193">Compal Electronics, Inc.</span><span class="sxs-lookup"><span data-stu-id="06987-193">Compal Electronics, Inc.</span></span>
* <span data-ttu-id="06987-194">Dongguan cyfrowy AV technologii Corp., Ltd.</span><span class="sxs-lookup"><span data-stu-id="06987-194">Dongguan Digital AV Technology Corp., Ltd.</span></span>
* <span data-ttu-id="06987-195">EchoStar Corporation zakupu</span><span class="sxs-lookup"><span data-stu-id="06987-195">EchoStar Purchasing Corporation</span></span>
* <span data-ttu-id="06987-196">Enseo, Inc.</span><span class="sxs-lookup"><span data-stu-id="06987-196">Enseo, Inc.</span></span>
* <span data-ttu-id="06987-197">Ograniczone filmów Filmflex</span><span class="sxs-lookup"><span data-stu-id="06987-197">Filmflex Movies Limited</span></span>
* <span data-ttu-id="06987-198">Fluendo SA</span><span class="sxs-lookup"><span data-stu-id="06987-198">Fluendo S.A.</span></span>
* <span data-ttu-id="06987-199">Ograniczone innowacje Gibson</span><span class="sxs-lookup"><span data-stu-id="06987-199">Gibson Innovations Limited</span></span>
* <span data-ttu-id="06987-200">Haier informacji Applicantion S.R.L</span><span class="sxs-lookup"><span data-stu-id="06987-200">Haier Information Applicantion S.R.L</span></span>
* <span data-ttu-id="06987-201">BroadInfoCom HANDAN Company, Ltd.</span><span class="sxs-lookup"><span data-stu-id="06987-201">HANDAN BroadInfoCom Co., Ltd.</span></span>
* <span data-ttu-id="06987-202">Międzynarodowe Hisense Company, Ltd.</span><span class="sxs-lookup"><span data-stu-id="06987-202">Hisense International Co., Ltd.</span></span> 
* <span data-ttu-id="06987-203">Homecast Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="06987-203">Homecast Co.,Ltd</span></span>
* <span data-ttu-id="06987-204">HON Hai dokładności branży Company, Ltd.</span><span class="sxs-lookup"><span data-stu-id="06987-204">Hon Hai Precision Industry Co., Ltd.</span></span>
* <span data-ttu-id="06987-205">Infomir GMBH</span><span class="sxs-lookup"><span data-stu-id="06987-205">Infomir GMBH</span></span>
* <span data-ttu-id="06987-206">Kaonmedia Company, Ltd.</span><span class="sxs-lookup"><span data-stu-id="06987-206">Kaonmedia Co., Ltd.</span></span>
* <span data-ttu-id="06987-207">KDDI Corporation</span><span class="sxs-lookup"><span data-stu-id="06987-207">KDDI Corporation</span></span>
* <span data-ttu-id="06987-208">Nintendo Company, Ltd.</span><span class="sxs-lookup"><span data-stu-id="06987-208">Nintendo Co., Ltd.</span></span>
* <span data-ttu-id="06987-209">Kolor pomarańczowy SA</span><span class="sxs-lookup"><span data-stu-id="06987-209">Orange SA</span></span>
* <span data-ttu-id="06987-210">Ograniczone cyfrowy szafran</span><span class="sxs-lookup"><span data-stu-id="06987-210">Saffron Digital Limited</span></span>
* <span data-ttu-id="06987-211">Połączenie szerokopasmowe Sagemcom SAS</span><span class="sxs-lookup"><span data-stu-id="06987-211">Sagemcom Broadband SAS</span></span>
* <span data-ttu-id="06987-212">Shenzhen Coship Electronics CO., Ltd.</span><span class="sxs-lookup"><span data-stu-id="06987-212">Shenzhen Coship Electronics CO., LTD</span></span>
* <span data-ttu-id="06987-213">Elektrycznego Jiuzhou Shenzhen Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="06987-213">Shenzhen Jiuzhou Electric Co.,Ltd</span></span>
* <span data-ttu-id="06987-214">Shenzhen Skyworth cyfrowy technologii Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="06987-214">Shenzhen Skyworth Digital Technology Co., Ltd</span></span>
* <span data-ttu-id="06987-215">Elektrycznego Changhong prowincji Syczuan Company, Ltd.</span><span class="sxs-lookup"><span data-stu-id="06987-215">Sichuan Changhong Electric Co., Ltd.</span></span>
* <span data-ttu-id="06987-216">Skardin przemysłowej Corp.</span><span class="sxs-lookup"><span data-stu-id="06987-216">Skardin Industrial Corp.</span></span>
* <span data-ttu-id="06987-217">Niebo Deutschland Fernsehen GmbH & Co. KG</span><span class="sxs-lookup"><span data-stu-id="06987-217">Sky Deutschland Fernsehen GmbH & Co. KG</span></span>
* <span data-ttu-id="06987-218">SmarDTV SA</span><span class="sxs-lookup"><span data-stu-id="06987-218">SmarDTV S.A.</span></span>
* <span data-ttu-id="06987-219">SoftAtHome</span><span class="sxs-lookup"><span data-stu-id="06987-219">SoftAtHome</span></span>
* <span data-ttu-id="06987-220">Sony Corporation</span><span class="sxs-lookup"><span data-stu-id="06987-220">Sony Corporation</span></span>
* <span data-ttu-id="06987-221">Ograniczone TCL zamorskich Marketing (urządzeniach oddalonych od brzegu komercyjnej Makau SAR)</span><span class="sxs-lookup"><span data-stu-id="06987-221">TCL Overseas Marketing (Macao Commercial Offshore) Limited</span></span>
* <span data-ttu-id="06987-222">Technicolor dostarczanie technologii, SAS</span><span class="sxs-lookup"><span data-stu-id="06987-222">Technicolor Delivery Technologies, SAS</span></span>
* <span data-ttu-id="06987-223">Tongfang Ltd. globalne</span><span class="sxs-lookup"><span data-stu-id="06987-223">Tongfang Global Ltd.</span></span>
* <span data-ttu-id="06987-224">TOP zwycięstwa inwestycji, Ltd.</span><span class="sxs-lookup"><span data-stu-id="06987-224">Top Victory Investments, Ltd.</span></span>
* <span data-ttu-id="06987-225">Toshiba Lifestyle produktów i usług firma</span><span class="sxs-lookup"><span data-stu-id="06987-225">Toshiba Lifestyle Products & Services Corporation</span></span>
* <span data-ttu-id="06987-226">S.r.o. /Slovakia/ uniwersalnej Corporation nośnika</span><span class="sxs-lookup"><span data-stu-id="06987-226">Universal Media Corporation /Slovakia/ s.r.o.</span></span>
* <span data-ttu-id="06987-227">VIZIO, Inc.</span><span class="sxs-lookup"><span data-stu-id="06987-227">VIZIO, Inc.</span></span>
* <span data-ttu-id="06987-228">Wistron Corporation</span><span class="sxs-lookup"><span data-stu-id="06987-228">Wistron Corporation</span></span>
* <span data-ttu-id="06987-229">ZTE Corporation</span><span class="sxs-lookup"><span data-stu-id="06987-229">ZTE Corporation</span></span>


## <a name="media-services-learning-paths"></a><span data-ttu-id="06987-230">Ścieżki szkoleniowe dotyczące usługi Media Services</span><span class="sxs-lookup"><span data-stu-id="06987-230">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="06987-231">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="06987-231">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

