---
title: przetwarzanie przez dodanie jednostek kodowania - Azure media aaaScale |  Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toohow tooadd kodowania jednostki z platformą .NET"
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 33f7625a-966a-4f06-bc09-bccd6e2a42b5
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako;milangada;
ms.openlocfilehash: b9f71a6487c5d136319a38a1598d60edfaa81b9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooscale-encoding-with-net-sdk"></a><span data-ttu-id="2c8f3-103">Jak tooscale kodowanie przy użyciu zestawu .NET SDK</span><span class="sxs-lookup"><span data-stu-id="2c8f3-103">How tooscale encoding with .NET SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2c8f3-104">Portal</span><span class="sxs-lookup"><span data-stu-id="2c8f3-104">Portal</span></span>](media-services-portal-scale-media-processing.md)
> * [<span data-ttu-id="2c8f3-105">.NET</span><span class="sxs-lookup"><span data-stu-id="2c8f3-105">.NET</span></span>](media-services-dotnet-encoding-units.md)
> * [<span data-ttu-id="2c8f3-106">REST</span><span class="sxs-lookup"><span data-stu-id="2c8f3-106">REST</span></span>](https://docs.microsoft.com/rest/api/media/operations/encodingreservedunittype)
> * [<span data-ttu-id="2c8f3-107">Java</span><span class="sxs-lookup"><span data-stu-id="2c8f3-107">Java</span></span>](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [<span data-ttu-id="2c8f3-108">PHP</span><span class="sxs-lookup"><span data-stu-id="2c8f3-108">PHP</span></span>](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
> 
> 

## <a name="overview"></a><span data-ttu-id="2c8f3-109">Omówienie</span><span class="sxs-lookup"><span data-stu-id="2c8f3-109">Overview</span></span>
> [!IMPORTANT]
> <span data-ttu-id="2c8f3-110">Upewnij się, że hello tooreview [omówienie](media-services-scale-media-processing-overview.md) tooget tematu więcej informacji na temat skalowania przetwarzania tematu nośnika.</span><span class="sxs-lookup"><span data-stu-id="2c8f3-110">Make sure tooreview hello [overview](media-services-scale-media-processing-overview.md) topic tooget more information about scaling media processing topic.</span></span>
> 
> 

<span data-ttu-id="2c8f3-111">toochange hello zastrzeżone jednostki typu i hello liczbę zastrzeżone jednostki przy użyciu zestawu .NET SDK kodowania hello następujące:</span><span class="sxs-lookup"><span data-stu-id="2c8f3-111">toochange hello reserved unit type and hello number of encoding reserved units using .NET SDK, do hello following:</span></span>

    IEncodingReservedUnit encodingS1ReservedUnit = _context.EncodingReservedUnits.FirstOrDefault();
    encodingS1ReservedUnit.ReservedUnitType = ReservedUnitType.Basic; // Corresponds tooS1
    encodingS1ReservedUnit.Update();
    Console.WriteLine("Reserved Unit Type: {0}", encodingS1ReservedUnit.ReservedUnitType);

    encodingS1ReservedUnit.CurrentReservedUnits = 2;
    encodingS1ReservedUnit.Update();

    Console.WriteLine("Number of reserved units: {0}", encodingS1ReservedUnit.CurrentReservedUnits);

## <a name="opening-a-support-ticket"></a><span data-ttu-id="2c8f3-112">Otwarcie biletu pomocy technicznej</span><span class="sxs-lookup"><span data-stu-id="2c8f3-112">Opening a Support Ticket</span></span>
<span data-ttu-id="2c8f3-113">Domyślnie co konto usługi Media Services można skalować tooup too25 kodowania i 5 na żądanie jednostek zarezerwowanego przesyłania strumieniowego.</span><span class="sxs-lookup"><span data-stu-id="2c8f3-113">By default every Media Services account can scale tooup too25 Encoding and 5 On-Demand Streaming Reserved Units.</span></span> <span data-ttu-id="2c8f3-114">Wyższy limit mogą żądać przez otwarcie biletu pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="2c8f3-114">You can request a higher limit by opening a support ticket.</span></span>

### <a name="open-a-support-ticket"></a><span data-ttu-id="2c8f3-115">Otwórz bilet pomocy technicznej</span><span class="sxs-lookup"><span data-stu-id="2c8f3-115">Open a support ticket</span></span>
<span data-ttu-id="2c8f3-116">tooopen biletu pomocy technicznej hello następujące:</span><span class="sxs-lookup"><span data-stu-id="2c8f3-116">tooopen a support ticket do hello following:</span></span>

1. <span data-ttu-id="2c8f3-117">Kliknij przycisk [uzyskać pomoc techniczną](https://manage.windowsazure.com/?getsupport=true).</span><span class="sxs-lookup"><span data-stu-id="2c8f3-117">Click [Get Support](https://manage.windowsazure.com/?getsupport=true).</span></span> <span data-ttu-id="2c8f3-118">Jeśli użytkownik nie jest zalogowany, będzie można tooenter zostanie wyświetlony monit o poświadczenia.</span><span class="sxs-lookup"><span data-stu-id="2c8f3-118">If you are not logged in, you will be prompted tooenter your credentials.</span></span>
2. <span data-ttu-id="2c8f3-119">Wybierz subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="2c8f3-119">Select your subscription.</span></span>
3. <span data-ttu-id="2c8f3-120">Wybierz pozycję "Technical" w obszarze typu pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="2c8f3-120">Under support type, select "Technical".</span></span>
4. <span data-ttu-id="2c8f3-121">Kliknij pozycję "Utwórz bilet".</span><span class="sxs-lookup"><span data-stu-id="2c8f3-121">Click on "Create Ticket".</span></span>
5. <span data-ttu-id="2c8f3-122">Wybierz "Azure Media Services" w liście produktów hello wyświetlone na następnej stronie powitania.</span><span class="sxs-lookup"><span data-stu-id="2c8f3-122">Select "Azure Media Services" in hello product list presented on hello next page.</span></span>
6. <span data-ttu-id="2c8f3-123">Wybierz opcję "Typ problemu" odpowiednią dla tego problemu.</span><span class="sxs-lookup"><span data-stu-id="2c8f3-123">Select a "Problem type" that is appropriate for your issue.</span></span>
7. <span data-ttu-id="2c8f3-124">Kliknij przycisk Kontynuuj.</span><span class="sxs-lookup"><span data-stu-id="2c8f3-124">Click Continue.</span></span>
8. <span data-ttu-id="2c8f3-125">Postępuj zgodnie z instrukcjami wyświetlanymi na następnej stronie, a następnie wprowadź szczegóły problemu.</span><span class="sxs-lookup"><span data-stu-id="2c8f3-125">Follow instructions on next page and then enter details about your issue.</span></span>
9. <span data-ttu-id="2c8f3-126">Kliknij przycisk Zatwierdź tooopen hello biletu.</span><span class="sxs-lookup"><span data-stu-id="2c8f3-126">Click submit tooopen hello ticket.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="2c8f3-127">Ścieżki szkoleniowe dotyczące usługi Media Services</span><span class="sxs-lookup"><span data-stu-id="2c8f3-127">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="2c8f3-128">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="2c8f3-128">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

