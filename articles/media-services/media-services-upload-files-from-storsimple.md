---
title: "Przekazywanie plików na konto usługi Azure Media Services z rozwiązania Azure StorSimple | Microsoft Docs"
description: "Ten artykuł zawiera krótkie omówienie usługi Azure StorSimple Data Manager. Artykuł zawiera również linki do samouczków, które przedstawiają sposób wyodrębniania danych z rozwiązania StorSimple i przekazywania ich jako elementów zawartości na konto usługi Azure Media Services."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 1dd09328-262b-43ef-8099-73241b49a925
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/27/2017
ms.author: juliako
ms.openlocfilehash: 636d55c15aa383208ffb39d5224123831af962c9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="upload-files-into-an-azure-media-services-account-from-azure-storsimple"></a><span data-ttu-id="2bddc-104">Przekazywanie plików na konto usługi Azure Media Services z rozwiązania Azure StorSimple</span><span class="sxs-lookup"><span data-stu-id="2bddc-104">Upload files into an Azure Media Services account from Azure StorSimple</span></span>

<span data-ttu-id="2bddc-105">Ten artykuł zawiera krótkie omówienie usługi Azure StorSimple Data Manager.</span><span class="sxs-lookup"><span data-stu-id="2bddc-105">This article gives a brief overview of Azure StorSimple Data Manager.</span></span> <span data-ttu-id="2bddc-106">Artykuł zawiera również linki do samouczków, które przedstawiają sposób wyodrębniania danych z rozwiązania StorSimple i przekazywania ich jako elementów zawartości na konto usługi Azure Media Services (AMS).</span><span class="sxs-lookup"><span data-stu-id="2bddc-106">The article also links to tutorials that show you how to extract data from StorSimple and upload this data as assets to an Azure Media Services (AMS) account.</span></span>

> 
> [!NOTE]
> <span data-ttu-id="2bddc-107">Usługa Azure StorSimple Data Manager jest obecnie dostępna w prywatnej wersji zapoznawczej.</span><span class="sxs-lookup"><span data-stu-id="2bddc-107">Azure StorSimple Data Manager is currently in private preview.</span></span> 
> 

## <a name="overview"></a><span data-ttu-id="2bddc-108">Omówienie</span><span class="sxs-lookup"><span data-stu-id="2bddc-108">Overview</span></span>

<span data-ttu-id="2bddc-109">Za pomocą usługi Media Services można przekazać pliki cyfrowe do elementu zawartości.</span><span class="sxs-lookup"><span data-stu-id="2bddc-109">In Media Services, you upload your digital files into an asset.</span></span> <span data-ttu-id="2bddc-110">Element zawartości może zawierać pliki wideo, audio, obrazy, kolekcje miniatur, ścieżki tekstowe i pliki napisów (oraz metadane dotyczące tych plików). Po przekazaniu plików zawartość jest bezpiecznie przechowywana w chmurze, na potrzeby dalszego przetwarzania i przesyłania strumieniowego.</span><span class="sxs-lookup"><span data-stu-id="2bddc-110">The Asset  can contain video, audio, images, thumbnail collections, text tracks and closed caption files (and the metadata about these files.) Once the files are uploaded, your content is stored securely in the cloud for further processing and streaming.</span></span>

<span data-ttu-id="2bddc-111">Usługa [Azure StorSimple](https://docs.microsoft.com/azure/storsimple/) używa magazynu w chmurze jako rozszerzenia rozwiązania lokalnego i automatycznie tworzy warstwy danych w magazynie lokalnym oraz magazynie w chmurze.</span><span class="sxs-lookup"><span data-stu-id="2bddc-111">[Azure StorSimple](https://docs.microsoft.com/azure/storsimple/) uses cloud storage as an extension of the on-premises solution and automatically tiers data across the on-premises storage and cloud storage.</span></span> <span data-ttu-id="2bddc-112">Urządzenie StorSimple usuwa duplikaty i kompresuje dane przed wysłaniem ich do chmury, dzięki czemu wysyłanie dużych plików do chmury staje się bardzo wydajne.</span><span class="sxs-lookup"><span data-stu-id="2bddc-112">The StorSimple device dedupes and compresses your data before sending it to the cloud making it very efficient for sending large files to the cloud.</span></span> <span data-ttu-id="2bddc-113">Usługa [StorSimple Data Manager](../storsimple/storsimple-data-manager-overview.md) oferuje interfejsy API, które umożliwiają wyodrębnianie danych z rozwiązania StorSimple i przedstawianie ich w postaci elementów zawartości usługi AMS.</span><span class="sxs-lookup"><span data-stu-id="2bddc-113">The [StorSimple Data Manager](../storsimple/storsimple-data-manager-overview.md) service provides APIs that enable you to extract data from StorSimple and present it as AMS assets.</span></span>

## <a name="get-started"></a><span data-ttu-id="2bddc-114">Rozpoczęcie pracy</span><span class="sxs-lookup"><span data-stu-id="2bddc-114">Get started</span></span>

1. <span data-ttu-id="2bddc-115">[Utwórz konto usługi Media Services](media-services-portal-create-account.md) , do którego chcesz przenieść elementy zawartości.</span><span class="sxs-lookup"><span data-stu-id="2bddc-115">[Create a Media Services account](media-services-portal-create-account.md) into which you want to transfer the assets.</span></span>
2. <span data-ttu-id="2bddc-116">Utwórz nowe konto wersji zapoznawczej usługi Data Manager, zgodnie z opisem w artykule [StorSimple Data Manager](../storsimple/storsimple-data-manager-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2bddc-116">Sign up for Data Manager preview, as described in the [StorSimple Data Manager](../storsimple/storsimple-data-manager-overview.md) article.</span></span>
3. <span data-ttu-id="2bddc-117">Utwórz konto usługi StorSimple Data Manager.</span><span class="sxs-lookup"><span data-stu-id="2bddc-117">Create a StorSimple Data Manager account.</span></span>
4. <span data-ttu-id="2bddc-118">Utwórz zadanie przekształcania danych, które po uruchomieniu wyodrębnia dane z urządzenia StorSimple i przekazuje je na konto usługi AMS jako elementy zawartości.</span><span class="sxs-lookup"><span data-stu-id="2bddc-118">Create a data transformation job that when runs, extracts data from a StorSimple device and transfers it into an AMS account as assets.</span></span> 

    <span data-ttu-id="2bddc-119">Gdy zadanie zacznie działać, zostanie utworzona kolejka magazynu.</span><span class="sxs-lookup"><span data-stu-id="2bddc-119">When the job starts running, a storage queue is created.</span></span> <span data-ttu-id="2bddc-120">Jest ona wypełniana przy użyciu komunikatów dotyczących przekształconych obiektów blob, gdy będą gotowe.</span><span class="sxs-lookup"><span data-stu-id="2bddc-120">This queue is populated with messages about transformed blobs as they are ready.</span></span> <span data-ttu-id="2bddc-121">Nazwa tej kolejki jest taka sama jak nazwa definicji zadania.</span><span class="sxs-lookup"><span data-stu-id="2bddc-121">The name of this queue is the same as the name of the job definition.</span></span> <span data-ttu-id="2bddc-122">Za pomocą tej kolejki można określić, czy element zawartości jest gotowy i wywołać żądaną operację usługi Media Services do uruchomienia w jego obrębie.</span><span class="sxs-lookup"><span data-stu-id="2bddc-122">You can use this queue to determine when as asset is ready and call your desired Media Services operation to run on it.</span></span> <span data-ttu-id="2bddc-123">Tej kolejki można na przykład użyć do wyzwalania funkcji Azure Function, która zawiera niezbędny kod usługi Media Services.</span><span class="sxs-lookup"><span data-stu-id="2bddc-123">For example, you can use this queue to trigger an Azure Function that has the necessary Media Services code in it.</span></span>

## <a name="see-also"></a><span data-ttu-id="2bddc-124">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="2bddc-124">See also</span></span>

[<span data-ttu-id="2bddc-125">Wyzwalanie zadań usługi Data Manager przy użyciu zestawu .Net SDK</span><span class="sxs-lookup"><span data-stu-id="2bddc-125">Use the .Net SDK to trigger jobs in the Data Manager</span></span>](../storsimple/storsimple-data-manager-dotnet-jobs.md)

## <a name="media-services-learning-paths"></a><span data-ttu-id="2bddc-126">Ścieżki szkoleniowe dotyczące usługi Media Services</span><span class="sxs-lookup"><span data-stu-id="2bddc-126">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="2bddc-127">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="2bddc-127">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a><span data-ttu-id="2bddc-128">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="2bddc-128">Next steps</span></span>

<span data-ttu-id="2bddc-129">Teraz możesz zakodować przekazane elementy zawartości.</span><span class="sxs-lookup"><span data-stu-id="2bddc-129">You can now encode your uploaded assets.</span></span> <span data-ttu-id="2bddc-130">Więcej informacji znajduje się na stronie [Kodowanie elementów zawartości](media-services-portal-encode.md).</span><span class="sxs-lookup"><span data-stu-id="2bddc-130">For more information, see [Encode assets](media-services-portal-encode.md).</span></span>
