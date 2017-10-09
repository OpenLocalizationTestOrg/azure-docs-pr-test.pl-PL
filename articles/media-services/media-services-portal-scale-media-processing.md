---
title: "przetwarzanie przy użyciu nośnika aaaScale hello portalu Azure | Dokumentacja firmy Microsoft"
description: "Ten samouczek przedstawia kroki hello nośnika skalowania przetwarzania przy użyciu hello portalu Azure."
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
ms.openlocfilehash: 89240c6f7579b8795e7b47f2b1c398b1d5477e20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-reserved-unit-type"></a><span data-ttu-id="a49e3-103">Typ jednostki zmiany hello zastrzeżone</span><span class="sxs-lookup"><span data-stu-id="a49e3-103">Change hello reserved unit type</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a49e3-104">.NET</span><span class="sxs-lookup"><span data-stu-id="a49e3-104">.NET</span></span>](media-services-dotnet-encoding-units.md)
> * [<span data-ttu-id="a49e3-105">Portal</span><span class="sxs-lookup"><span data-stu-id="a49e3-105">Portal</span></span>](media-services-portal-scale-media-processing.md)
> * [<span data-ttu-id="a49e3-106">REST</span><span class="sxs-lookup"><span data-stu-id="a49e3-106">REST</span></span>](https://docs.microsoft.com/rest/api/media/operations/encodingreservedunittype)
> * [<span data-ttu-id="a49e3-107">Java</span><span class="sxs-lookup"><span data-stu-id="a49e3-107">Java</span></span>](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [<span data-ttu-id="a49e3-108">PHP</span><span class="sxs-lookup"><span data-stu-id="a49e3-108">PHP</span></span>](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
> 
> 

## <a name="overview"></a><span data-ttu-id="a49e3-109">Omówienie</span><span class="sxs-lookup"><span data-stu-id="a49e3-109">Overview</span></span>

<span data-ttu-id="a49e3-110">Konto usługi Media Services jest skojarzony z zarezerwowanych typu jednostki, który określa szybkość hello przetwarzania zadania przetwarzania multimediów.</span><span class="sxs-lookup"><span data-stu-id="a49e3-110">A Media Services account is associated with a Reserved Unit Type, which determines hello speed with which your media processing tasks are processed.</span></span> <span data-ttu-id="a49e3-111">Można wybrać między hello następujące typy jednostek zarezerwowanych: **S1**, **S2**, lub **S3**.</span><span class="sxs-lookup"><span data-stu-id="a49e3-111">You can pick between hello following reserved unit types: **S1**, **S2**, or **S3**.</span></span> <span data-ttu-id="a49e3-112">Na przykład hello tego samego zadania kodowania działa szybciej, gdy używasz hello **S2** jednostka zarezerwowanego typ porównania toohello **S1** typu.</span><span class="sxs-lookup"><span data-stu-id="a49e3-112">For example, hello same encoding job runs faster when you use hello **S2** reserved unit type compare toohello **S1** type.</span></span>

<span data-ttu-id="a49e3-113">Ponadto toospecifying hello zastrzeżone typ jednostki, można określić tooprovision Twojego konta z **jednostki zarezerwowanego** (RUs).</span><span class="sxs-lookup"><span data-stu-id="a49e3-113">In addition toospecifying hello reserved unit type, you can specify tooprovision your account with **Reserved Units** (RUs).</span></span> <span data-ttu-id="a49e3-114">Liczba Hello elastycznie RUs określa hello liczbę zadań nośnika, które mogą być jednocześnie przetwarzane w ramach danego konta.</span><span class="sxs-lookup"><span data-stu-id="a49e3-114">hello number of provisioned RUs determines hello number of media tasks that can be processed concurrently in a given account.</span></span>

>[!NOTE]
><span data-ttu-id="a49e3-115">Jednostki zarezerwowane przekształcają wszystkie operacje przetwarzania multimediów do postaci równoległej, uwzględniając zadania Indeksowania za pomocą usługi Azure Media Indexer.</span><span class="sxs-lookup"><span data-stu-id="a49e3-115">RUs work for parallelizing all media processing, including indexing jobs using Azure Media Indexer.</span></span> <span data-ttu-id="a49e3-116">Jednak w przeciwieństwie do kodowania zadania indeksowania nie są przetwarzane szybciej przy użyciu szybszych jednostek zarezerwowanych.</span><span class="sxs-lookup"><span data-stu-id="a49e3-116">However, unlike encoding, indexing jobs do not get processed faster with faster reserved units.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a49e3-117">Upewnij się, że hello tooreview [omówienie](media-services-scale-media-processing-overview.md) tooget tematu więcej informacji na temat skalowania przetwarzania tematu nośnika.</span><span class="sxs-lookup"><span data-stu-id="a49e3-117">Make sure tooreview hello [overview](media-services-scale-media-processing-overview.md) topic tooget more information about scaling media processing topic.</span></span>
> 
> 

## <a name="scale-media-processing"></a><span data-ttu-id="a49e3-118">Skalowanie przetwarzania multimediów</span><span class="sxs-lookup"><span data-stu-id="a49e3-118">Scale media processing</span></span>
<span data-ttu-id="a49e3-119">toochange hello zastrzeżone jednostki typu i hello liczbę jednostek zarezerwowanego hello następujące:</span><span class="sxs-lookup"><span data-stu-id="a49e3-119">toochange hello reserved unit type and hello number of reserved units, do hello following:</span></span>

1. <span data-ttu-id="a49e3-120">W hello [portalu Azure](https://portal.azure.com/), wybierz konto usługi Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="a49e3-120">In hello [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="a49e3-121">W hello **ustawienia** wybierz **jednostki zarezerwowane multimediów**.</span><span class="sxs-lookup"><span data-stu-id="a49e3-121">In hello **Settings** window, select **Media reserved units**.</span></span>
   
    <span data-ttu-id="a49e3-122">toochange hello liczba zarezerwowanych jednostek hello wybranego typu jednostka zarezerwowanego, użyj hello **jednostki obsługiwanej nośnika** suwaka.</span><span class="sxs-lookup"><span data-stu-id="a49e3-122">toochange hello number of reserved units for hello selected reserved unit type, use hello **Media Served Units** slider.</span></span>
   
    <span data-ttu-id="a49e3-123">Witaj toochange **typ jednostki zarezerwowane**, naciśnij klawisz S1, S2 lub S3.</span><span class="sxs-lookup"><span data-stu-id="a49e3-123">toochange hello **RESERVED UNIT TYPE**, press S1, S2, or S3.</span></span>
   
    ![Strona procesorów](./media/media-services-portal-scale-media-processing/media-services-scale-media-processing.png)
3. <span data-ttu-id="a49e3-125">Naciśnij klawisz hello ZAPISAĆ toosave przycisk zmiany.</span><span class="sxs-lookup"><span data-stu-id="a49e3-125">Press hello SAVE button toosave your changes.</span></span>
   
    <span data-ttu-id="a49e3-126">nowe jednostki zarezerwowanego Hello są przydzielane po naciśnięciu ZAPISZ.</span><span class="sxs-lookup"><span data-stu-id="a49e3-126">hello new reserved units are allocated when you press SAVE.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a49e3-127">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a49e3-127">Next steps</span></span>
<span data-ttu-id="a49e3-128">Przejrzyj ścieżki szkoleniowe dotyczące usługi Media Services.</span><span class="sxs-lookup"><span data-stu-id="a49e3-128">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="a49e3-129">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="a49e3-129">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

