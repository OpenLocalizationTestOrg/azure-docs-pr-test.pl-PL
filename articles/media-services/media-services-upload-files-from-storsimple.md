---
title: "pliki aaaUpload do konta usługi Azure Media Services z Azure StorSimple | Dokumentacja firmy Microsoft"
description: "Ten artykuł zawiera krótkie omówienie usługi Azure StorSimple Data Manager. Artykuł Hello zawiera również linki tootutorials, który przedstawia sposób tooextract danych z StorSimple i przekaż go jako tooan zasobów konta usługi Azure Media Services."
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
ms.openlocfilehash: 7e9712aa480106bbd5fcc63eaecf0418b24a8bef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-into-an-azure-media-services-account-from-azure-storsimple"></a><span data-ttu-id="ace17-104">Przekazywanie plików na konto usługi Azure Media Services z rozwiązania Azure StorSimple</span><span class="sxs-lookup"><span data-stu-id="ace17-104">Upload files into an Azure Media Services account from Azure StorSimple</span></span>

<span data-ttu-id="ace17-105">Ten artykuł zawiera krótkie omówienie usługi Azure StorSimple Data Manager.</span><span class="sxs-lookup"><span data-stu-id="ace17-105">This article gives a brief overview of Azure StorSimple Data Manager.</span></span> <span data-ttu-id="ace17-106">Artykuł Hello zawiera również linki tootutorials, który przedstawia sposób tooextract danych z StorSimple i przekazać te dane jako tooan zasobów konta usługi Azure Media Services (AMS).</span><span class="sxs-lookup"><span data-stu-id="ace17-106">hello article also links tootutorials that show you how tooextract data from StorSimple and upload this data as assets tooan Azure Media Services (AMS) account.</span></span>

> 
> [!NOTE]
> <span data-ttu-id="ace17-107">Usługa Azure StorSimple Data Manager jest obecnie dostępna w prywatnej wersji zapoznawczej.</span><span class="sxs-lookup"><span data-stu-id="ace17-107">Azure StorSimple Data Manager is currently in private preview.</span></span> 
> 

## <a name="overview"></a><span data-ttu-id="ace17-108">Omówienie</span><span class="sxs-lookup"><span data-stu-id="ace17-108">Overview</span></span>

<span data-ttu-id="ace17-109">Za pomocą usługi Media Services można przekazać pliki cyfrowe do elementu zawartości.</span><span class="sxs-lookup"><span data-stu-id="ace17-109">In Media Services, you upload your digital files into an asset.</span></span> <span data-ttu-id="ace17-110">Witaj zasobów może zawierać wideo, audio, obrazy, kolekcje miniatur, tekst ścieżek i napisów plików (i hello metadane dotyczące tych plików.) Po przekazaniu plików hello zawartość jest bezpiecznie przechowywana w chmurze powitania dla dalszego przetwarzania i przesyłania strumieniowego.</span><span class="sxs-lookup"><span data-stu-id="ace17-110">hello Asset  can contain video, audio, images, thumbnail collections, text tracks and closed caption files (and hello metadata about these files.) Once hello files are uploaded, your content is stored securely in hello cloud for further processing and streaming.</span></span>

<span data-ttu-id="ace17-111">[Azure StorSimple](https://docs.microsoft.com/azure/storsimple/) używa magazynu w chmurze jako rozszerzenie hello lokalnego rozwiązania i automatycznie warstwy danych przez Magazyn lokalne powitania i magazynu w chmurze.</span><span class="sxs-lookup"><span data-stu-id="ace17-111">[Azure StorSimple](https://docs.microsoft.com/azure/storsimple/) uses cloud storage as an extension of hello on-premises solution and automatically tiers data across hello on-premises storage and cloud storage.</span></span> <span data-ttu-id="ace17-112">urządzenie StorSimple Hello dedupes i kompresuje dane przed wysłaniem toohello chmury, dzięki czemu bardzo wydajny wysyłania dużych plików toohello chmury.</span><span class="sxs-lookup"><span data-stu-id="ace17-112">hello StorSimple device dedupes and compresses your data before sending it toohello cloud making it very efficient for sending large files toohello cloud.</span></span> <span data-ttu-id="ace17-113">Witaj [Menedżer StorSimple danych](../storsimple/storsimple-data-manager-overview.md) usługi udostępnia interfejsy API, Włącz możesz tooextract danych z StorSimple i prezentować jako zasoby AMS.</span><span class="sxs-lookup"><span data-stu-id="ace17-113">hello [StorSimple Data Manager](../storsimple/storsimple-data-manager-overview.md) service provides APIs that enable you tooextract data from StorSimple and present it as AMS assets.</span></span>

## <a name="get-started"></a><span data-ttu-id="ace17-114">Rozpoczęcie pracy</span><span class="sxs-lookup"><span data-stu-id="ace17-114">Get started</span></span>

1. <span data-ttu-id="ace17-115">[Utwórz konto usługi Media Services](media-services-portal-create-account.md) do którego będzie tootransfer hello zasoby.</span><span class="sxs-lookup"><span data-stu-id="ace17-115">[Create a Media Services account](media-services-portal-create-account.md) into which you want tootransfer hello assets.</span></span>
2. <span data-ttu-id="ace17-116">Załóż Data Manager w wersji zapoznawczej, zgodnie z opisem w hello [Menedżer StorSimple danych](../storsimple/storsimple-data-manager-overview.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="ace17-116">Sign up for Data Manager preview, as described in hello [StorSimple Data Manager](../storsimple/storsimple-data-manager-overview.md) article.</span></span>
3. <span data-ttu-id="ace17-117">Utwórz konto usługi StorSimple Data Manager.</span><span class="sxs-lookup"><span data-stu-id="ace17-117">Create a StorSimple Data Manager account.</span></span>
4. <span data-ttu-id="ace17-118">Utwórz zadanie przekształcania danych, które po uruchomieniu wyodrębnia dane z urządzenia StorSimple i przekazuje je na konto usługi AMS jako elementy zawartości.</span><span class="sxs-lookup"><span data-stu-id="ace17-118">Create a data transformation job that when runs, extracts data from a StorSimple device and transfers it into an AMS account as assets.</span></span> 

    <span data-ttu-id="ace17-119">Po uruchomieniu zadania hello systemem kolejki magazynu jest tworzony.</span><span class="sxs-lookup"><span data-stu-id="ace17-119">When hello job starts running, a storage queue is created.</span></span> <span data-ttu-id="ace17-120">Jest ona wypełniana przy użyciu komunikatów dotyczących przekształconych obiektów blob, gdy będą gotowe.</span><span class="sxs-lookup"><span data-stu-id="ace17-120">This queue is populated with messages about transformed blobs as they are ready.</span></span> <span data-ttu-id="ace17-121">Nazwa Hello tej kolejki jest hello taka sama jak nazwa hello hello definicji zadania.</span><span class="sxs-lookup"><span data-stu-id="ace17-121">hello name of this queue is hello same as hello name of hello job definition.</span></span> <span data-ttu-id="ace17-122">Można użyć tej kolejki toodetermine po zawartości jest gotowe i wywołać z żądaną toorun operacji usługi Media Services.</span><span class="sxs-lookup"><span data-stu-id="ace17-122">You can use this queue toodetermine when as asset is ready and call your desired Media Services operation toorun on it.</span></span> <span data-ttu-id="ace17-123">Na przykład można użyć tej kolejki tootrigger funkcji platformy Azure, która ma hello niezbędne usługi Media Services kodu w nim.</span><span class="sxs-lookup"><span data-stu-id="ace17-123">For example, you can use this queue tootrigger an Azure Function that has hello necessary Media Services code in it.</span></span>

## <a name="see-also"></a><span data-ttu-id="ace17-124">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="ace17-124">See also</span></span>

[<span data-ttu-id="ace17-125">Użyj hello .net SDK tootrigger zadania w hello Data Manager</span><span class="sxs-lookup"><span data-stu-id="ace17-125">Use hello .Net SDK tootrigger jobs in hello Data Manager</span></span>](../storsimple/storsimple-data-manager-dotnet-jobs.md)

## <a name="media-services-learning-paths"></a><span data-ttu-id="ace17-126">Ścieżki szkoleniowe dotyczące usługi Media Services</span><span class="sxs-lookup"><span data-stu-id="ace17-126">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="ace17-127">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="ace17-127">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a><span data-ttu-id="ace17-128">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ace17-128">Next steps</span></span>

<span data-ttu-id="ace17-129">Teraz możesz zakodować przekazane elementy zawartości.</span><span class="sxs-lookup"><span data-stu-id="ace17-129">You can now encode your uploaded assets.</span></span> <span data-ttu-id="ace17-130">Więcej informacji znajduje się na stronie [Kodowanie elementów zawartości](media-services-portal-encode.md).</span><span class="sxs-lookup"><span data-stu-id="ace17-130">For more information, see [Encode assets](media-services-portal-encode.md).</span></span>
