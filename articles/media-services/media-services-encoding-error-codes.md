---
title: "kodowanie kody błędów usługi Media Services aaaAzure | Dokumentacja firmy Microsoft"
description: "Ten temat zawiera listę kodów błędów, które mogą być zwracane w przypadku Napotkano błąd podczas hello kodowanie wykonywania zadania."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: ce4e939f-5aee-41f9-859d-e4429815e9f2
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako
ms.openlocfilehash: b69b6abee797c40c9b8b8f23bf2398273c170e7f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="encoding-error-codes"></a><span data-ttu-id="3ba55-103">Kodowanie kody błędów</span><span class="sxs-lookup"><span data-stu-id="3ba55-103">Encoding error codes</span></span>

<span data-ttu-id="3ba55-104">Witaj następującej tabeli opisano kody błędów, które mogą być zwracane w przypadku Napotkano błąd podczas hello kodowanie wykonywania zadania.</span><span class="sxs-lookup"><span data-stu-id="3ba55-104">hello following table lists error codes that could be returned in case an error was encountered during hello encoding task execution.</span></span>  <span data-ttu-id="3ba55-105">Szczegóły błędu tooget w kodzie .NET, użyj hello [szczegóły błędu](http://msdn.microsoft.com/library/microsoft.windowsazure.mediaservices.client.errordetail.aspx) klasy.</span><span class="sxs-lookup"><span data-stu-id="3ba55-105">tooget error details in your .NET code, use hello [ErrorDetails](http://msdn.microsoft.com/library/microsoft.windowsazure.mediaservices.client.errordetail.aspx) class.</span></span> <span data-ttu-id="3ba55-106">Szczegóły błędu tooget w kodzie REST, użyj hello [ErrorDetail](https://msdn.microsoft.com/library/jj853026.aspx) interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="3ba55-106">tooget error details in your REST code, use hello [ErrorDetail](https://msdn.microsoft.com/library/jj853026.aspx) REST API.</span></span>

| <span data-ttu-id="3ba55-107">ErrorDetail.Code</span><span class="sxs-lookup"><span data-stu-id="3ba55-107">ErrorDetail.Code</span></span> | <span data-ttu-id="3ba55-108">Możliwe przyczyny błędu</span><span class="sxs-lookup"><span data-stu-id="3ba55-108">Possible causes for error</span></span> |
| --- | --- |
| <span data-ttu-id="3ba55-109">Nieznany</span><span class="sxs-lookup"><span data-stu-id="3ba55-109">Unknown</span></span> |<span data-ttu-id="3ba55-110">Wystąpił nieznany błąd podczas wykonywania zadania hello</span><span class="sxs-lookup"><span data-stu-id="3ba55-110">Unknown error while executing hello task</span></span> |
| <span data-ttu-id="3ba55-111">ErrorDownloadingInputAssetMalformedContent</span><span class="sxs-lookup"><span data-stu-id="3ba55-111">ErrorDownloadingInputAssetMalformedContent</span></span> |<span data-ttu-id="3ba55-112">Kategorii błędów, który obejmuje błędy w czasie pobierania wejściowych zasobów, takich jak nazwy uszkodzonych plików, zero pliki o długości, niepoprawny formatuje i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="3ba55-112">Category of errors that covers errors in downloading input asset such as bad file names, zero length files, incorrect formats and so on.</span></span> |
| <span data-ttu-id="3ba55-113">ErrorDownloadingInputAssetServiceFailure</span><span class="sxs-lookup"><span data-stu-id="3ba55-113">ErrorDownloadingInputAssetServiceFailure</span></span> |<span data-ttu-id="3ba55-114">Kategoria błędów, który obejmuje problemów po stronie usługi hello — na przykład sieci lub magazynu błędy podczas pobierania.</span><span class="sxs-lookup"><span data-stu-id="3ba55-114">Category of errors that covers problems on hello service side - for example network or storage errors while downloading.</span></span> |
| <span data-ttu-id="3ba55-115">ErrorParsingConfiguration</span><span class="sxs-lookup"><span data-stu-id="3ba55-115">ErrorParsingConfiguration</span></span> |<span data-ttu-id="3ba55-116">Kategoria błędów, gdy zadanie <see cref="MediaTask.PrivateData"/> (Konfiguracja) jest nieprawidłowa, na przykład hello konfiguracji nie jest poprawnym systemem ustawienia wstępnego lub zawiera nieprawidłowy kod XML.</span><span class="sxs-lookup"><span data-stu-id="3ba55-116">Category of errors where task <see cref="MediaTask.PrivateData"/> (configuration) is not valid, for example hello configuration is not a valid system preset or it contains invalid XML.</span></span> |
| <span data-ttu-id="3ba55-117">ErrorExecutingTaskMalformedContent</span><span class="sxs-lookup"><span data-stu-id="3ba55-117">ErrorExecutingTaskMalformedContent</span></span> |<span data-ttu-id="3ba55-118">Kategoria błędy podczas wykonywania hello hello zadania, których problemów wewnątrz hello wejściowej plików multimedialnych spowodować niepowodzenie.</span><span class="sxs-lookup"><span data-stu-id="3ba55-118">Category of errors during hello execution of hello task where issues inside hello input media files cause failure.</span></span> |
| <span data-ttu-id="3ba55-119">ErrorExecutingTaskUnsupportedFormat</span><span class="sxs-lookup"><span data-stu-id="3ba55-119">ErrorExecutingTaskUnsupportedFormat</span></span> |<span data-ttu-id="3ba55-120">Kategoria błędy, gdy procesor multimediów hello nie może przetworzyć plików hello — formatu media nie obsługiwany lub nie odpowiada hello konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="3ba55-120">Category of errors where hello media processor cannot process hello files provided - media format not supported, or does not match hello Configuration.</span></span> <span data-ttu-id="3ba55-121">Na przykład w trakcie tooproduce tylko dźwięk dane wyjściowe z zasobu, który zawiera tylko wideo</span><span class="sxs-lookup"><span data-stu-id="3ba55-121">For example, trying tooproduce an audio-only output from an asset that has only video</span></span> |
| <span data-ttu-id="3ba55-122">ErrorProcessingTask</span><span class="sxs-lookup"><span data-stu-id="3ba55-122">ErrorProcessingTask</span></span> |<span data-ttu-id="3ba55-123">Podczas przetwarzania hello hello zadanie, które są toocontent niepowiązanych napotka kategorii innych błędów, które hello procesor multimediów.</span><span class="sxs-lookup"><span data-stu-id="3ba55-123">Category of other errors that hello media processor encounters during hello processing of hello task that are unrelated toocontent.</span></span> |
| <span data-ttu-id="3ba55-124">ErrorUploadingOutputAsset</span><span class="sxs-lookup"><span data-stu-id="3ba55-124">ErrorUploadingOutputAsset</span></span> |<span data-ttu-id="3ba55-125">Kategoria błędy podczas wysyłania zawartości wyjściowej hello</span><span class="sxs-lookup"><span data-stu-id="3ba55-125">Category of errors when uploading hello output asset</span></span> |
| <span data-ttu-id="3ba55-126">ErrorCancelingTask</span><span class="sxs-lookup"><span data-stu-id="3ba55-126">ErrorCancelingTask</span></span> |<span data-ttu-id="3ba55-127">Kategoria niepowodzeń toocover błędy podczas próby hello toocancel zadań</span><span class="sxs-lookup"><span data-stu-id="3ba55-127">Category of errors toocover failures when attempting toocancel hello Task</span></span> |
| <span data-ttu-id="3ba55-128">TransientError</span><span class="sxs-lookup"><span data-stu-id="3ba55-128">TransientError</span></span> |<span data-ttu-id="3ba55-129">Kategoria błędy toocover przejściowych problemów (np.)</span><span class="sxs-lookup"><span data-stu-id="3ba55-129">Category of errors toocover transient issues (eg.</span></span> <span data-ttu-id="3ba55-130">tymczasowe problemy z siecią z usługą Azure Storage)</span><span class="sxs-lookup"><span data-stu-id="3ba55-130">temporary networking issues with Azure Storage)</span></span> |

<span data-ttu-id="3ba55-131">Pomoc tooget od hello **Media Services** zespół, otwórz [obsługuje biletu](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span><span class="sxs-lookup"><span data-stu-id="3ba55-131">tooget help from hello **Media Services** team, open a [support ticket](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="3ba55-132">Ścieżki szkoleniowe dotyczące usługi Media Services</span><span class="sxs-lookup"><span data-stu-id="3ba55-132">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="3ba55-133">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="3ba55-133">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-articles"></a><span data-ttu-id="3ba55-134">Pokrewne artykuły:</span><span class="sxs-lookup"><span data-stu-id="3ba55-134">Related articles</span></span>
* [<span data-ttu-id="3ba55-135">Wykonywania zaawansowanych zadań kodowania dostosowując ustawienia standardu Media Encoder Standard</span><span class="sxs-lookup"><span data-stu-id="3ba55-135">Perform advanced encoding tasks by customizing Media Encoder Standard presets</span></span>](media-services-custom-mes-presets-with-dotnet.md)
* [<span data-ttu-id="3ba55-136">Przydziały i ograniczenia</span><span class="sxs-lookup"><span data-stu-id="3ba55-136">Quotas and Limitations</span></span>](media-services-quotas-and-limitations.md)

<!--Reference links in article-->
[1]: http://azure.microsoft.com/pricing/details/media-services/
