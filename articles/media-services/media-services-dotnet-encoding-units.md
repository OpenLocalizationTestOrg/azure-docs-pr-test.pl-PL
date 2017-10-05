---
title: Skalowanie przetwarzania przez dodanie jednostek kodowania - Azure media |  Dokumentacja firmy Microsoft
description: "Dowiedz się, jak sposób dodawania kodowania jednostki z platformą .NET"
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
ms.openlocfilehash: 72a8729d22a9e76c8076d7a3347619a2163e4f09
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-scale-encoding-with-net-sdk"></a><span data-ttu-id="25cf0-103">Skalowanie kodowania za pomocą zestawu .NET SDK</span><span class="sxs-lookup"><span data-stu-id="25cf0-103">How to scale encoding with .NET SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="25cf0-104">Portal</span><span class="sxs-lookup"><span data-stu-id="25cf0-104">Portal</span></span>](media-services-portal-scale-media-processing.md)
> * [<span data-ttu-id="25cf0-105">.NET</span><span class="sxs-lookup"><span data-stu-id="25cf0-105">.NET</span></span>](media-services-dotnet-encoding-units.md)
> * [<span data-ttu-id="25cf0-106">REST</span><span class="sxs-lookup"><span data-stu-id="25cf0-106">REST</span></span>](https://docs.microsoft.com/rest/api/media/operations/encodingreservedunittype)
> * [<span data-ttu-id="25cf0-107">Java</span><span class="sxs-lookup"><span data-stu-id="25cf0-107">Java</span></span>](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [<span data-ttu-id="25cf0-108">PHP</span><span class="sxs-lookup"><span data-stu-id="25cf0-108">PHP</span></span>](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
> 
> 

## <a name="overview"></a><span data-ttu-id="25cf0-109">Omówienie</span><span class="sxs-lookup"><span data-stu-id="25cf0-109">Overview</span></span>
> [!IMPORTANT]
> <span data-ttu-id="25cf0-110">Upewnij się przejrzeć [omówienie](media-services-scale-media-processing-overview.md) tematu, aby uzyskać więcej informacji na temat skalowania przetwarzania tematu nośnika.</span><span class="sxs-lookup"><span data-stu-id="25cf0-110">Make sure to review the [overview](media-services-scale-media-processing-overview.md) topic to get more information about scaling media processing topic.</span></span>
> 
> 

<span data-ttu-id="25cf0-111">Aby zmienić typ jednostki zarezerwowane i liczba zastrzeżone jednostki przy użyciu zestawu .NET SDK kodowania, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="25cf0-111">To change the reserved unit type and the number of encoding reserved units using .NET SDK, do the following:</span></span>

    IEncodingReservedUnit encodingS1ReservedUnit = _context.EncodingReservedUnits.FirstOrDefault();
    encodingS1ReservedUnit.ReservedUnitType = ReservedUnitType.Basic; // Corresponds to S1
    encodingS1ReservedUnit.Update();
    Console.WriteLine("Reserved Unit Type: {0}", encodingS1ReservedUnit.ReservedUnitType);

    encodingS1ReservedUnit.CurrentReservedUnits = 2;
    encodingS1ReservedUnit.Update();

    Console.WriteLine("Number of reserved units: {0}", encodingS1ReservedUnit.CurrentReservedUnits);

## <a name="opening-a-support-ticket"></a><span data-ttu-id="25cf0-112">Otwarcie biletu pomocy technicznej</span><span class="sxs-lookup"><span data-stu-id="25cf0-112">Opening a Support Ticket</span></span>
<span data-ttu-id="25cf0-113">Domyślnie co konto usługi Media Services można skalować do maksymalnie 25, kodowanie i 5 na żądanie jednostek zarezerwowanego przesyłania strumieniowego.</span><span class="sxs-lookup"><span data-stu-id="25cf0-113">By default every Media Services account can scale to up to 25 Encoding and 5 On-Demand Streaming Reserved Units.</span></span> <span data-ttu-id="25cf0-114">Wyższy limit mogą żądać przez otwarcie biletu pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="25cf0-114">You can request a higher limit by opening a support ticket.</span></span>

### <a name="open-a-support-ticket"></a><span data-ttu-id="25cf0-115">Otwórz bilet pomocy technicznej</span><span class="sxs-lookup"><span data-stu-id="25cf0-115">Open a support ticket</span></span>
<span data-ttu-id="25cf0-116">Aby otworzyć obsługi biletów, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="25cf0-116">To open a support ticket do the following:</span></span>

1. <span data-ttu-id="25cf0-117">Kliknij przycisk [uzyskać pomoc techniczną](https://manage.windowsazure.com/?getsupport=true).</span><span class="sxs-lookup"><span data-stu-id="25cf0-117">Click [Get Support](https://manage.windowsazure.com/?getsupport=true).</span></span> <span data-ttu-id="25cf0-118">Jeśli użytkownik nie jest zalogowany, pojawi się monit o podanie poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="25cf0-118">If you are not logged in, you will be prompted to enter your credentials.</span></span>
2. <span data-ttu-id="25cf0-119">Wybierz subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="25cf0-119">Select your subscription.</span></span>
3. <span data-ttu-id="25cf0-120">Wybierz pozycję "Technical" w obszarze typu pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="25cf0-120">Under support type, select "Technical".</span></span>
4. <span data-ttu-id="25cf0-121">Kliknij pozycję "Utwórz bilet".</span><span class="sxs-lookup"><span data-stu-id="25cf0-121">Click on "Create Ticket".</span></span>
5. <span data-ttu-id="25cf0-122">Wybierz "Azure Media Services" w liście produktów wyświetlone na następnej stronie.</span><span class="sxs-lookup"><span data-stu-id="25cf0-122">Select "Azure Media Services" in the product list presented on the next page.</span></span>
6. <span data-ttu-id="25cf0-123">Wybierz opcję "Typ problemu" odpowiednią dla tego problemu.</span><span class="sxs-lookup"><span data-stu-id="25cf0-123">Select a "Problem type" that is appropriate for your issue.</span></span>
7. <span data-ttu-id="25cf0-124">Kliknij przycisk Kontynuuj.</span><span class="sxs-lookup"><span data-stu-id="25cf0-124">Click Continue.</span></span>
8. <span data-ttu-id="25cf0-125">Postępuj zgodnie z instrukcjami wyświetlanymi na następnej stronie, a następnie wprowadź szczegóły problemu.</span><span class="sxs-lookup"><span data-stu-id="25cf0-125">Follow instructions on next page and then enter details about your issue.</span></span>
9. <span data-ttu-id="25cf0-126">Kliknij przycisk Zatwierdź, aby otworzyć bilet.</span><span class="sxs-lookup"><span data-stu-id="25cf0-126">Click submit to open the ticket.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="25cf0-127">Ścieżki szkoleniowe dotyczące usługi Media Services</span><span class="sxs-lookup"><span data-stu-id="25cf0-127">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="25cf0-128">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="25cf0-128">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

