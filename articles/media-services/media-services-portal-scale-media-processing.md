---
title: "Skalowania przetwarzania nośnika przy użyciu portalu Azure | Dokumentacja firmy Microsoft"
description: "Ten samouczek przedstawia kroki nośnika skalowania przetwarzania przy użyciu portalu Azure."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: e500f733-68aa-450c-b212-cf717c0d15da
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/04/2017
ms.author: juliako
ms.openlocfilehash: 46ca29d3e66701f2abcb185791089e94761984e8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="change-the-reserved-unit-type"></a><span data-ttu-id="1d937-103">Zmiana typu jednostki zarezerwowanej</span><span class="sxs-lookup"><span data-stu-id="1d937-103">Change the reserved unit type</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1d937-104">.NET</span><span class="sxs-lookup"><span data-stu-id="1d937-104">.NET</span></span>](media-services-dotnet-encoding-units.md)
> * [<span data-ttu-id="1d937-105">Portal</span><span class="sxs-lookup"><span data-stu-id="1d937-105">Portal</span></span>](media-services-portal-scale-media-processing.md)
> * [<span data-ttu-id="1d937-106">REST</span><span class="sxs-lookup"><span data-stu-id="1d937-106">REST</span></span>](https://docs.microsoft.com/rest/api/media/operations/encodingreservedunittype)
> * [<span data-ttu-id="1d937-107">Java</span><span class="sxs-lookup"><span data-stu-id="1d937-107">Java</span></span>](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [<span data-ttu-id="1d937-108">PHP</span><span class="sxs-lookup"><span data-stu-id="1d937-108">PHP</span></span>](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
> 
> 

## <a name="overview"></a><span data-ttu-id="1d937-109">Omówienie</span><span class="sxs-lookup"><span data-stu-id="1d937-109">Overview</span></span>

<span data-ttu-id="1d937-110">Konto usługi Media Services jest skojarzone z typem jednostki zarezerwowanej określającym szybkość, z jaką są przetwarzane zadania przetwarzania multimediów.</span><span class="sxs-lookup"><span data-stu-id="1d937-110">A Media Services account is associated with a Reserved Unit Type, which determines the speed with which your media processing tasks are processed.</span></span> <span data-ttu-id="1d937-111">Można wybrać jeden z następujących typów jednostki zarezerwowanej: **S1**, **S2** lub **S3**.</span><span class="sxs-lookup"><span data-stu-id="1d937-111">You can pick between the following reserved unit types: **S1**, **S2**, or **S3**.</span></span> <span data-ttu-id="1d937-112">Na przykład to samo zadanie kodowania jest wykonywane szybciej przy użyciu typu jednostki zarezerwowanej **S2** niż w przypadku użycia typu **S1**.</span><span class="sxs-lookup"><span data-stu-id="1d937-112">For example, the same encoding job runs faster when you use the **S2** reserved unit type compare to the **S1** type.</span></span>

<span data-ttu-id="1d937-113">Oprócz określenia typu jednostki zarezerwowanej można określić aprowizację swojego konta przy użyciu **jednostek zarezerwowanych** (RU, Reserved Unit).</span><span class="sxs-lookup"><span data-stu-id="1d937-113">In addition to specifying the reserved unit type, you can specify to provision your account with **Reserved Units** (RUs).</span></span> <span data-ttu-id="1d937-114">Liczba zainicjowanych jednostek zarezerwowanych określa liczbę zadań multimedialnych, które mogą być przetwarzane jednocześnie w ramach danego konta.</span><span class="sxs-lookup"><span data-stu-id="1d937-114">The number of provisioned RUs determines the number of media tasks that can be processed concurrently in a given account.</span></span>

>[!NOTE]
><span data-ttu-id="1d937-115">Jednostki zarezerwowane przekształcają wszystkie operacje przetwarzania multimediów do postaci równoległej, uwzględniając zadania Indeksowania za pomocą usługi Azure Media Indexer.</span><span class="sxs-lookup"><span data-stu-id="1d937-115">RUs work for parallelizing all media processing, including indexing jobs using Azure Media Indexer.</span></span> <span data-ttu-id="1d937-116">Jednak w przeciwieństwie do kodowania zadania indeksowania nie są przetwarzane szybciej przy użyciu szybszych jednostek zarezerwowanych.</span><span class="sxs-lookup"><span data-stu-id="1d937-116">However, unlike encoding, indexing jobs do not get processed faster with faster reserved units.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1d937-117">Upewnij się przejrzeć [omówienie](media-services-scale-media-processing-overview.md) tematu, aby uzyskać więcej informacji na temat skalowania przetwarzania tematu nośnika.</span><span class="sxs-lookup"><span data-stu-id="1d937-117">Make sure to review the [overview](media-services-scale-media-processing-overview.md) topic to get more information about scaling media processing topic.</span></span>
> 
> 

## <a name="scale-media-processing"></a><span data-ttu-id="1d937-118">Skalowanie przetwarzania multimediów</span><span class="sxs-lookup"><span data-stu-id="1d937-118">Scale media processing</span></span>
<span data-ttu-id="1d937-119">Aby zmienić typ jednostki zarezerwowane i liczbę jednostek zarezerwowanego, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="1d937-119">To change the reserved unit type and the number of reserved units, do the following:</span></span>

1. <span data-ttu-id="1d937-120">W witrynie [Azure Portal](https://portal.azure.com/) wybierz swoje konto usługi Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="1d937-120">In the [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="1d937-121">W **ustawienia** wybierz **jednostki zarezerwowane multimediów**.</span><span class="sxs-lookup"><span data-stu-id="1d937-121">In the **Settings** window, select **Media reserved units**.</span></span>
   
    <span data-ttu-id="1d937-122">Aby zmienić liczbę jednostek zarezerwowanego dla typu wybranej jednostki zarezerwowane, użyj **jednostki obsługiwanej nośnika** suwaka.</span><span class="sxs-lookup"><span data-stu-id="1d937-122">To change the number of reserved units for the selected reserved unit type, use the **Media Served Units** slider.</span></span>
   
    <span data-ttu-id="1d937-123">Aby zmienić **typ jednostki zarezerwowane**, naciśnij klawisz S1, S2 lub S3.</span><span class="sxs-lookup"><span data-stu-id="1d937-123">To change the **RESERVED UNIT TYPE**, press S1, S2, or S3.</span></span>
   
    ![Strona procesorów](./media/media-services-portal-scale-media-processing/media-services-scale-media-processing.png)
3. <span data-ttu-id="1d937-125">Kliknij przycisk ZAPISZ, aby zapisać zmiany.</span><span class="sxs-lookup"><span data-stu-id="1d937-125">Press the SAVE button to save your changes.</span></span>
   
    <span data-ttu-id="1d937-126">Nowe zastrzeżone jednostki są przydzielane po naciśnięciu przycisku ZAPISZ.</span><span class="sxs-lookup"><span data-stu-id="1d937-126">The new reserved units are allocated when you press SAVE.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1d937-127">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1d937-127">Next steps</span></span>
<span data-ttu-id="1d937-128">Przejrzyj ścieżki szkoleniowe dotyczące usługi Media Services.</span><span class="sxs-lookup"><span data-stu-id="1d937-128">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="1d937-129">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="1d937-129">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

