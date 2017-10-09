---
title: "AAA\"przekazywania plików do konta usługi Media Services przy użyciu hello portalu Azure | Dokumentacja firmy Microsoft\""
description: "Ten samouczek przedstawia kroki hello przekazywania plików do konta usługi Media Services przy użyciu hello portalu Azure"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 3ad3dcea-95be-4711-9aae-a455a32434f6
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/07/2017
ms.author: juliako
ms.openlocfilehash: 4ce1e133c72854532735ba7c72a43c92a75bc240
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-into-a-media-services-account-using-hello-azure-portal"></a><span data-ttu-id="1cda9-103">Przekazywanie plików do konta usługi Media Services przy użyciu hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="1cda9-103">Upload files into a Media Services account using hello Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1cda9-104">Portal</span><span class="sxs-lookup"><span data-stu-id="1cda9-104">Portal</span></span>](media-services-portal-upload-files.md)
> * [<span data-ttu-id="1cda9-105">.NET</span><span class="sxs-lookup"><span data-stu-id="1cda9-105">.NET</span></span>](media-services-dotnet-upload-files.md)
> * [<span data-ttu-id="1cda9-106">REST</span><span class="sxs-lookup"><span data-stu-id="1cda9-106">REST</span></span>](media-services-rest-upload-files.md)
> 
> [!NOTE]
> <span data-ttu-id="1cda9-107">toocomplete tego samouczka jest potrzebne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="1cda9-107">toocomplete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="1cda9-108">Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1cda9-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
> 


<span data-ttu-id="1cda9-109">Za pomocą usługi Media Services można przekazać pliki cyfrowe do elementu zawartości.</span><span class="sxs-lookup"><span data-stu-id="1cda9-109">In Media Services, you upload your digital files into an asset.</span></span> <span data-ttu-id="1cda9-110">Witaj zasobów może zawierać wideo, audio, obrazy, kolekcje miniatur, tekst ścieżek i napisów plików (i hello metadane dotyczące tych plików.) Po przekazaniu plików hello zawartość jest bezpiecznie przechowywana w chmurze powitania dla dalszego przetwarzania i przesyłania strumieniowego.</span><span class="sxs-lookup"><span data-stu-id="1cda9-110">hello Asset  can contain video, audio, images, thumbnail collections, text tracks and closed caption files (and hello metadata about these files.) Once hello files are uploaded, your content is stored securely in hello cloud for further processing and streaming.</span></span>


## <a name="upload-files"></a><span data-ttu-id="1cda9-111">Przekazywanie plików</span><span class="sxs-lookup"><span data-stu-id="1cda9-111">Upload files</span></span>

>[!NOTE]
><span data-ttu-id="1cda9-112">Brak limitu toohello maksymalny obsługiwany rozmiar pliku do przetwarzania w usłudze Media Services.</span><span class="sxs-lookup"><span data-stu-id="1cda9-112">There is a limit toohello maximum file size supported for processing in Media Services.</span></span> <span data-ttu-id="1cda9-113">Zobacz [to](media-services-quotas-and-limitations.md) tematu, aby uzyskać szczegółowe informacje dotyczące limitu rozmiaru pliku hello.</span><span class="sxs-lookup"><span data-stu-id="1cda9-113">Please see [this](media-services-quotas-and-limitations.md) topic for details about hello file size limitation.</span></span>
>

1. <span data-ttu-id="1cda9-114">W hello [portalu Azure](https://portal.azure.com/), wybierz konto usługi Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="1cda9-114">In hello [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="1cda9-115">Na powitania **ustawienia** bloku, kliknij przycisk **zasoby**.</span><span class="sxs-lookup"><span data-stu-id="1cda9-115">On hello **Settings** blade, click **Assets**.</span></span>
   
    ![Przekazywanie plików](./media/media-services-portal-vod-get-started/media-services-upload.png)
3. <span data-ttu-id="1cda9-117">Kliknij przycisk hello **przekazać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="1cda9-117">Click hello **Upload** button.</span></span>
   
    <span data-ttu-id="1cda9-118">Witaj **przekazywanie zawartości wideo** zostanie wyświetlone okno.</span><span class="sxs-lookup"><span data-stu-id="1cda9-118">hello **Upload a video asset** window appears.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="1cda9-119">Nie ma żadnego limitu rozmiaru pliku.</span><span class="sxs-lookup"><span data-stu-id="1cda9-119">There is no file size limitation.</span></span>
   > 
   > 
4. <span data-ttu-id="1cda9-120">Przeglądaj toohello potrzeby wideo na komputerze, zaznacz go i kliknij przycisk OK.</span><span class="sxs-lookup"><span data-stu-id="1cda9-120">Browse toohello desired video on your computer, select it, and hit OK.</span></span>  
   
    <span data-ttu-id="1cda9-121">rozpocznie się przekazywanie Hello, aby zobaczyć postęp hello pod nazwą pliku hello.</span><span class="sxs-lookup"><span data-stu-id="1cda9-121">hello upload starts and you can see hello progress under hello file name.</span></span>  

<span data-ttu-id="1cda9-122">Po ukończeniu przekazywania hello zobaczysz hello nowy element zawartości na liście hello **zasoby** okna.</span><span class="sxs-lookup"><span data-stu-id="1cda9-122">Once hello upload completes, you will see hello new asset listed in hello **Assets** window.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="1cda9-123">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1cda9-123">Next steps</span></span>
<span data-ttu-id="1cda9-124">Teraz możesz zakodować przekazane elementy zawartości.</span><span class="sxs-lookup"><span data-stu-id="1cda9-124">You can now encode your uploaded assets.</span></span> <span data-ttu-id="1cda9-125">Więcej informacji znajduje się na stronie [Kodowanie elementów zawartości](media-services-portal-encode.md).</span><span class="sxs-lookup"><span data-stu-id="1cda9-125">For more information, see [Encode assets](media-services-portal-encode.md).</span></span>

<span data-ttu-id="1cda9-126">Umożliwia także tootrigger usługi Azure Functions zadania kodowania, na podstawie pliku odbieranych w kontenerze hello skonfigurowane.</span><span class="sxs-lookup"><span data-stu-id="1cda9-126">You can also use Azure Functions tootrigger an encoding job based on a file arriving in hello configured container.</span></span> <span data-ttu-id="1cda9-127">Aby uzyskać więcej informacji, zobacz [ten przykład](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ).</span><span class="sxs-lookup"><span data-stu-id="1cda9-127">For more information, see [this sample](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ ).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="1cda9-128">Ścieżki szkoleniowe dotyczące usługi Media Services</span><span class="sxs-lookup"><span data-stu-id="1cda9-128">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="1cda9-129">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="1cda9-129">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

