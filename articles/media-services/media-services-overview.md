---
title: "Omówienie usługi Media Services aaaAzure | Dokumentacja firmy Microsoft"
description: "Ten temat zawiera omówienie usługi Azure Media Services"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 7a5e9723-c379-446b-b4d6-d0e41bd7d31f
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/04/2017
ms.author: juliako;anilmur
ms.openlocfilehash: 81f9f4d9ff75effea30c10fd09449e9d2025f377
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-media-services-overview"></a><span data-ttu-id="27c0a-103">Omówienie usługi Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="27c0a-103">Azure Media Services overview</span></span> 

<span data-ttu-id="27c0a-104">Microsoft Azure Media Services to rozszerzalna platforma oparte na chmurze, która umożliwia deweloperom toobuild nośnika skalowalne zarządzanie i dostarczania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="27c0a-104">Microsoft Azure Media Services is an extensible cloud-based platform that enables developers toobuild scalable media management and delivery applications.</span></span> <span data-ttu-id="27c0a-105">Media Services są oparte na interfejsach API REST umożliwiające przekazywanie toosecurely, przechowywanie, kodowanie i pakietów zawartości wideo lub audio zarówno na żądanie i na żywo przesyłania strumieniowego dostarczania toovarious klientów (na przykład TV, PC i urządzeń przenośnych).</span><span class="sxs-lookup"><span data-stu-id="27c0a-105">Media Services is based on REST APIs that enable you toosecurely upload, store, encode, and package video or audio content for both on-demand and live streaming delivery toovarious clients (for example, TV, PC, and mobile devices).</span></span>

<span data-ttu-id="27c0a-106">Korzystając wyłącznie z usługi Media Services, można tworzyć kompleksowe przepływy pracy.</span><span class="sxs-lookup"><span data-stu-id="27c0a-106">You can build end-to-end workflows using entirely Media Services.</span></span> <span data-ttu-id="27c0a-107">Możesz również toouse składników innych firm dla niektórych części przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="27c0a-107">You can also choose toouse third-party components for some parts of your workflow.</span></span> <span data-ttu-id="27c0a-108">Na przykład kodowanie można wykonać przy użyciu kodera innego producenta.</span><span class="sxs-lookup"><span data-stu-id="27c0a-108">For example, encode using a third-party encoder.</span></span> <span data-ttu-id="27c0a-109">Natomiast przekazywanie, zabezpieczanie, tworzenie pakietów i dostarczanie można realizować za pomocą usługi Media Services.</span><span class="sxs-lookup"><span data-stu-id="27c0a-109">Then, upload, protect, package, deliver using Media Services.</span></span>

<span data-ttu-id="27c0a-110">Możesz wybrać toostream zawartości na żywo lub dostarczanie zawartości na żądanie.</span><span class="sxs-lookup"><span data-stu-id="27c0a-110">You can choose toostream your content live or deliver content on-demand.</span></span> <span data-ttu-id="27c0a-111">Witaj temat zawiera także linki tooother powiązanych tematów.</span><span class="sxs-lookup"><span data-stu-id="27c0a-111">hello topic also links tooother relevant topics.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="27c0a-112">Ścieżki szkoleniowe dotyczące usługi Media Services</span><span class="sxs-lookup"><span data-stu-id="27c0a-112">Media Services learning paths</span></span>
<span data-ttu-id="27c0a-113">Ścieżki szkoleniowe dotyczące usługi AMS można zobaczyć tutaj:</span><span class="sxs-lookup"><span data-stu-id="27c0a-113">You can view AMS learning paths here:</span></span>

* [<span data-ttu-id="27c0a-114">Przepływ pracy transmisji strumieniowej na żywo usługi AMS</span><span class="sxs-lookup"><span data-stu-id="27c0a-114">AMS Live Streaming Workflow</span></span>](https://azure.microsoft.com/documentation/learning-paths/media-services-streaming-live/)
* [<span data-ttu-id="27c0a-115">Przepływ pracy transmisji strumieniowej na żądanie usługi AMS</span><span class="sxs-lookup"><span data-stu-id="27c0a-115">AMS on-Demand Streaming Workflow</span></span>](https://azure.microsoft.com/documentation/learning-paths/media-services-streaming-on-demand/)

## <a name="prerequisites"></a><span data-ttu-id="27c0a-116">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="27c0a-116">Prerequisites</span></span>

<span data-ttu-id="27c0a-117">toostart przy użyciu usługi Azure Media Services, powinien mieć następujące hello:</span><span class="sxs-lookup"><span data-stu-id="27c0a-117">toostart using Azure Media Services, you should have hello following:</span></span>

* <span data-ttu-id="27c0a-118">Konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="27c0a-118">An Azure account.</span></span> <span data-ttu-id="27c0a-119">Jeśli jej nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="27c0a-119">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="27c0a-120">Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="27c0a-120">For details, see [Azure Free Trial](https://azure.microsoft.com).</span></span>
* <span data-ttu-id="27c0a-121">Konto usługi Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="27c0a-121">An Azure Media Services account.</span></span> <span data-ttu-id="27c0a-122">Aby uzyskać więcej informacji, zobacz temat [Tworzenie konta](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="27c0a-122">For more information, see [Create Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="27c0a-123">(Opcjonalnie) Konfigurowanie środowiska deweloperskiego.</span><span class="sxs-lookup"><span data-stu-id="27c0a-123">(Optional) Set up development environment.</span></span> <span data-ttu-id="27c0a-124">Wybierz platformę .NET lub interfejs API REST dla środowiska deweloperskiego.</span><span class="sxs-lookup"><span data-stu-id="27c0a-124">Choose .NET or REST API for your development environment.</span></span> <span data-ttu-id="27c0a-125">Aby uzyskać więcej informacji, zobacz temat [Konfigurowanie środowiska](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="27c0a-125">For more information, see [Set up environment](media-services-dotnet-how-to-use.md).</span></span>

    <span data-ttu-id="27c0a-126">Poznaj także sposób zbyt[połączenie programowe tooAMS interfejsu API](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="27c0a-126">Also, learn how too[connect  programmatically tooAMS API](media-services-use-aad-auth-to-access-ams-api.md).</span></span>
* <span data-ttu-id="27c0a-127">Punkt końcowy przesyłania strumieniowego (standardowy lub Premium) w stanie uruchomionym.</span><span class="sxs-lookup"><span data-stu-id="27c0a-127">A standard or premium streaming endpoint in started state.</span></span>  <span data-ttu-id="27c0a-128">Aby uzyskać więcej informacji, zobacz [Zarządzanie punktami końcowymi przesyłania strumieniowego](media-services-portal-manage-streaming-endpoints.md)</span><span class="sxs-lookup"><span data-stu-id="27c0a-128">For more information, see [Managing streaming endpoints](media-services-portal-manage-streaming-endpoints.md)</span></span>

## <a name="sdks-and-tools"></a><span data-ttu-id="27c0a-129">Zestawy SDK i narzędzia</span><span class="sxs-lookup"><span data-stu-id="27c0a-129">SDKs and tools</span></span>

<span data-ttu-id="27c0a-130">toobuild rozwiązań Media Services, można użyć:</span><span class="sxs-lookup"><span data-stu-id="27c0a-130">toobuild Media Services solutions, you can use:</span></span>

* [<span data-ttu-id="27c0a-131">Interfejs API REST usługi Media Services</span><span class="sxs-lookup"><span data-stu-id="27c0a-131">Media Services REST API</span></span>](https://docs.microsoft.com/rest/api/media/operations/azure-media-services-rest-api-reference)
* <span data-ttu-id="27c0a-132">Jeden z zestawów SDK klienta dostępne hello:</span><span class="sxs-lookup"><span data-stu-id="27c0a-132">One of hello available client SDKs:</span></span>
    * <span data-ttu-id="27c0a-133">[Zestaw SDK usługi Azure Media Services dla platformy .NET](https://github.com/Azure/azure-sdk-for-media-services)</span><span class="sxs-lookup"><span data-stu-id="27c0a-133">[Azure Media Services SDK for .NET](https://github.com/Azure/azure-sdk-for-media-services),</span></span>
    * <span data-ttu-id="27c0a-134">[Zestaw Azure SDK dla języka Java](https://github.com/Azure/azure-sdk-for-java)</span><span class="sxs-lookup"><span data-stu-id="27c0a-134">[Azure SDK for Java](https://github.com/Azure/azure-sdk-for-java),</span></span>
    * <span data-ttu-id="27c0a-135">[Zestaw Azure PHP SDK](https://github.com/Azure/azure-sdk-for-php)</span><span class="sxs-lookup"><span data-stu-id="27c0a-135">[Azure PHP SDK](https://github.com/Azure/azure-sdk-for-php),</span></span>
    * <span data-ttu-id="27c0a-136">[Azure Media Services dla środowiska Node.js](https://github.com/michelle-becker/node-ams-sdk/blob/master/lib/request.js) (Jest to wersja zestawu Node.js SDK firmy innej niż Microsoft.</span><span class="sxs-lookup"><span data-stu-id="27c0a-136">[Azure Media Services for Node.js](https://github.com/michelle-becker/node-ams-sdk/blob/master/lib/request.js) (This is a non-Microsoft version of a Node.js SDK.</span></span> <span data-ttu-id="27c0a-137">On obsługiwany przez społeczność i aktualnie nie ma 100 pokrycie hello interfejsów API usług AMS).</span><span class="sxs-lookup"><span data-stu-id="27c0a-137">It is maintained by a community and currently does not have a 100% coverage of hello AMS APIs).</span></span>
* <span data-ttu-id="27c0a-138">Istniejące narzędzia:</span><span class="sxs-lookup"><span data-stu-id="27c0a-138">Existing tools:</span></span>
    * [<span data-ttu-id="27c0a-139">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="27c0a-139">Azure portal</span></span>](https://portal.azure.com/)
    * <span data-ttu-id="27c0a-140">[Azure-Media-Services-Explorer](https://github.com/Azure/Azure-Media-Services-Explorer) (Azure Media Services Explorer (AMSE) to aplikacja Winforms/C# dla systemu Windows)</span><span class="sxs-lookup"><span data-stu-id="27c0a-140">[Azure-Media-Services-Explorer](https://github.com/Azure/Azure-Media-Services-Explorer) (Azure Media Services Explorer (AMSE) is a Winforms/C# application for Windows)</span></span>

## <a name="concepts-and-overview"></a><span data-ttu-id="27c0a-141">Pojęcia i omówienie</span><span class="sxs-lookup"><span data-stu-id="27c0a-141">Concepts and overview</span></span>
<span data-ttu-id="27c0a-142">Pojęcia związane z usługą Azure Media Services zostały przedstawione w temacie [Pojęcia](media-services-concepts.md).</span><span class="sxs-lookup"><span data-stu-id="27c0a-142">For Azure Media Services concepts, see [Concepts](media-services-concepts.md).</span></span>

<span data-ttu-id="27c0a-143">Aby uzyskać jak tooseries wprowadzającej tooall hello głównymi składnikami usługi Azure Media Services, zobacz [samouczki krok po kroku Azure Media Services](https://docs.com/fukushima-shigeyuki/3439/english-azure-media-services-step-by-step-series).</span><span class="sxs-lookup"><span data-stu-id="27c0a-143">For a how-tooseries that introduces you tooall hello main components of Azure Media Services, see [Azure Media Services Step-by-Step tutorials](https://docs.com/fukushima-shigeyuki/3439/english-azure-media-services-step-by-step-series).</span></span> <span data-ttu-id="27c0a-144">Seria zawiera wszechstronne omówienie pojęć i używa zadań toodemonstrate AMS narzędzia AMSE hello.</span><span class="sxs-lookup"><span data-stu-id="27c0a-144">This series has a great overview of concepts and it uses hello AMSE tool toodemonstrate AMS tasks.</span></span> <span data-ttu-id="27c0a-145">AMSE to narzędzie systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="27c0a-145">AMSE tool is a Windows tool.</span></span> <span data-ttu-id="27c0a-146">To narzędzie obsługuje większość zadań hello można wykonać programowo przy użyciu [AMS SDK dla platformy .NET](https://github.com/Azure/azure-sdk-for-media-services), [zestawu Azure SDK dla języka Java](https://github.com/Azure/azure-sdk-for-java), lub [Azure PHP SDK](https://github.com/Azure/azure-sdk-for-php).</span><span class="sxs-lookup"><span data-stu-id="27c0a-146">This tool supports most of hello tasks you can achieve programmatically with [AMS SDK for .NET](https://github.com/Azure/azure-sdk-for-media-services), [Azure SDK for Java](https://github.com/Azure/azure-sdk-for-java), or  [Azure PHP SDK](https://github.com/Azure/azure-sdk-for-php).</span></span>

## <a name="supported-scenarios-and-availability-of-media-services-across-data-centers"></a><span data-ttu-id="27c0a-147">Obsługiwane scenariusze i dostępność usługi Media Services w centrach danych</span><span class="sxs-lookup"><span data-stu-id="27c0a-147">Supported scenarios and availability of Media Services across data centers</span></span>

<span data-ttu-id="27c0a-148">Aby uzyskać szczegółowe informacje, zobacz temat [Scenariusze oraz dostępność funkcji i usług AMS w centrach danych](scenarios-and-availability.md).</span><span class="sxs-lookup"><span data-stu-id="27c0a-148">For detailed information, see [AMS scenarios and availability of features and services across data centers](scenarios-and-availability.md).</span></span>

## <a name="service-level-agreement-sla"></a><span data-ttu-id="27c0a-149">Umowa dotycząca poziomu usług (SLA)</span><span class="sxs-lookup"><span data-stu-id="27c0a-149">Service Level Agreement (SLA)</span></span>

* <span data-ttu-id="27c0a-150">W przypadku usługi Media Services Encoding gwarantujemy dostępność transakcji interfejsu API REST na poziomie 99,9%.</span><span class="sxs-lookup"><span data-stu-id="27c0a-150">For Media Services Encoding, we guarantee 99.9% availability of REST API transactions.</span></span>
* <span data-ttu-id="27c0a-151">W zakresie przesyłania strumieniowego zapewniamy pomyślną obsługę żądań z gwarancją dostępności na poziomie 99,9% dla istniejącej zawartości multimedialnej w przypadku zakupu standardowego punktu końcowego przesyłania strumieniowego lub punktu końcowego przesyłania strumieniowego Premium.</span><span class="sxs-lookup"><span data-stu-id="27c0a-151">For Streaming, we will successfully service requests with a 99.9% availability guarantee for existing media content when a standard or premium streaming endpoint is purchased.</span></span>
* <span data-ttu-id="27c0a-152">Dla kanałów na żywo gwarantujemy, że uruchomione kanały będą utrzymywać łączność zewnętrzną co najmniej 99,9% czasu hello.</span><span class="sxs-lookup"><span data-stu-id="27c0a-152">For Live Channels, we guarantee that running Channels will have external connectivity at least 99.9% of hello time.</span></span>
* <span data-ttu-id="27c0a-153">Content Protection gwarantujemy, że pomyślną realizację żądań kluczy co najmniej 99,9% czasu hello.</span><span class="sxs-lookup"><span data-stu-id="27c0a-153">For Content Protection, we guarantee that we will successfully fulfill key requests at least 99.9% of hello time.</span></span>
* <span data-ttu-id="27c0a-154">Dla odniesieniu do indeksatora zapewniamy pomyślną realizację żądań zadań indeksatora przetwarzanych z zastrzeżone kodowanie jednostki 99,9% czasu hello.</span><span class="sxs-lookup"><span data-stu-id="27c0a-154">For Indexer, we will successfully service Indexer Task requests processed with an Encoding Reserved Unit 99.9% of hello time.</span></span>

<span data-ttu-id="27c0a-155">Aby uzyskać więcej informacji, zobacz temat [Umowy dotyczące poziomu usług platformy Microsoft Azure](https://azure.microsoft.com/support/legal/sla/).</span><span class="sxs-lookup"><span data-stu-id="27c0a-155">For more information, see [Microsoft Azure SLA](https://azure.microsoft.com/support/legal/sla/).</span></span>

<span data-ttu-id="27c0a-156">Aby uzyskać informacje na temat dostępności w centrach danych, zobacz hello [Avaiability](scenarios-and-availability.md#availability) sekcji.</span><span class="sxs-lookup"><span data-stu-id="27c0a-156">For information about availability in datacenters, see hello [Avaiability](scenarios-and-availability.md#availability) section.</span></span>

## <a name="support"></a><span data-ttu-id="27c0a-157">Pomoc techniczna</span><span class="sxs-lookup"><span data-stu-id="27c0a-157">Support</span></span>

<span data-ttu-id="27c0a-158">[Pomoc techniczna platformy Azure](https://azure.microsoft.com/support/options/) zapewnia opcje wsparcia technicznego dla platformy Azure, w tym dla usługi Media Services.</span><span class="sxs-lookup"><span data-stu-id="27c0a-158">[Azure Support](https://azure.microsoft.com/support/options/) provides support options for Azure, including Media Services.</span></span>

## <a name="provide-feedback"></a><span data-ttu-id="27c0a-159">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="27c0a-159">Provide feedback</span></span>

[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
