---
title: "Usługa Azure Media Services encoding kody błędów | Dokumentacja firmy Microsoft"
description: "Ten temat zawiera listę kodów błędów, które mogą być zwracane w przypadku Napotkano błąd podczas wykonywania zadania kodowania."
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
ms.openlocfilehash: f4fd2212d19f89148dde08c75c5a48cdd322d029
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="encoding-error-codes"></a><span data-ttu-id="358e6-103">Kodowanie kody błędów</span><span class="sxs-lookup"><span data-stu-id="358e6-103">Encoding error codes</span></span>

<span data-ttu-id="358e6-104">W poniższej tabeli przedstawiono kody błędów, które mogą być zwracane w przypadku Napotkano błąd podczas wykonywania zadania kodowania.</span><span class="sxs-lookup"><span data-stu-id="358e6-104">The following table lists error codes that could be returned in case an error was encountered during the encoding task execution.</span></span>  <span data-ttu-id="358e6-105">Aby uzyskać szczegóły błędu w kodzie .NET, należy użyć [szczegóły błędu](http://msdn.microsoft.com/library/microsoft.windowsazure.mediaservices.client.errordetail.aspx) klasy.</span><span class="sxs-lookup"><span data-stu-id="358e6-105">To get error details in your .NET code, use the [ErrorDetails](http://msdn.microsoft.com/library/microsoft.windowsazure.mediaservices.client.errordetail.aspx) class.</span></span> <span data-ttu-id="358e6-106">Aby uzyskać szczegóły błędu w kodzie REST, należy użyć [ErrorDetail](https://msdn.microsoft.com/library/jj853026.aspx) interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="358e6-106">To get error details in your REST code, use the [ErrorDetail](https://msdn.microsoft.com/library/jj853026.aspx) REST API.</span></span>

| <span data-ttu-id="358e6-107">ErrorDetail.Code</span><span class="sxs-lookup"><span data-stu-id="358e6-107">ErrorDetail.Code</span></span> | <span data-ttu-id="358e6-108">Możliwe przyczyny błędu</span><span class="sxs-lookup"><span data-stu-id="358e6-108">Possible causes for error</span></span> |
| --- | --- |
| <span data-ttu-id="358e6-109">Nieznany</span><span class="sxs-lookup"><span data-stu-id="358e6-109">Unknown</span></span> |<span data-ttu-id="358e6-110">Wystąpił nieznany błąd podczas wykonywania zadania</span><span class="sxs-lookup"><span data-stu-id="358e6-110">Unknown error while executing the task</span></span> |
| <span data-ttu-id="358e6-111">ErrorDownloadingInputAssetMalformedContent</span><span class="sxs-lookup"><span data-stu-id="358e6-111">ErrorDownloadingInputAssetMalformedContent</span></span> |<span data-ttu-id="358e6-112">Kategorii błędów, który obejmuje błędy w czasie pobierania wejściowych zasobów, takich jak nazwy uszkodzonych plików, zero pliki o długości, niepoprawny formatuje i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="358e6-112">Category of errors that covers errors in downloading input asset such as bad file names, zero length files, incorrect formats and so on.</span></span> |
| <span data-ttu-id="358e6-113">ErrorDownloadingInputAssetServiceFailure</span><span class="sxs-lookup"><span data-stu-id="358e6-113">ErrorDownloadingInputAssetServiceFailure</span></span> |<span data-ttu-id="358e6-114">Kategoria błędów obejmuje problemów po stronie usługi — na przykład sieci lub magazynu błędy podczas pobierania.</span><span class="sxs-lookup"><span data-stu-id="358e6-114">Category of errors that covers problems on the service side - for example network or storage errors while downloading.</span></span> |
| <span data-ttu-id="358e6-115">ErrorParsingConfiguration</span><span class="sxs-lookup"><span data-stu-id="358e6-115">ErrorParsingConfiguration</span></span> |<span data-ttu-id="358e6-116">Kategoria błędów, gdy zadanie <see cref="MediaTask.PrivateData"/> (Konfiguracja) jest nieprawidłowa, na przykład konfiguracji nie jest poprawnym systemem ustawienia wstępnego lub zawiera nieprawidłowy kod XML.</span><span class="sxs-lookup"><span data-stu-id="358e6-116">Category of errors where task <see cref="MediaTask.PrivateData"/> (configuration) is not valid, for example the configuration is not a valid system preset or it contains invalid XML.</span></span> |
| <span data-ttu-id="358e6-117">ErrorExecutingTaskMalformedContent</span><span class="sxs-lookup"><span data-stu-id="358e6-117">ErrorExecutingTaskMalformedContent</span></span> |<span data-ttu-id="358e6-118">Kategoria błędy podczas wykonywania zadań, gdy problemy wewnątrz multimedialnych plików wejściowych spowodować niepowodzenie.</span><span class="sxs-lookup"><span data-stu-id="358e6-118">Category of errors during the execution of the task where issues inside the input media files cause failure.</span></span> |
| <span data-ttu-id="358e6-119">ErrorExecutingTaskUnsupportedFormat</span><span class="sxs-lookup"><span data-stu-id="358e6-119">ErrorExecutingTaskUnsupportedFormat</span></span> |<span data-ttu-id="358e6-120">Kategoria błędy, gdy procesor multimediów nie może przetworzyć pliki udostępniane — formatu media nie obsługiwany lub nie jest zgodna z konfiguracją.</span><span class="sxs-lookup"><span data-stu-id="358e6-120">Category of errors where the media processor cannot process the files provided - media format not supported, or does not match the Configuration.</span></span> <span data-ttu-id="358e6-121">Na przykład w trakcie generowania tylko dźwięk danych wyjściowych z zasobu, który zawiera tylko wideo</span><span class="sxs-lookup"><span data-stu-id="358e6-121">For example, trying to produce an audio-only output from an asset that has only video</span></span> |
| <span data-ttu-id="358e6-122">ErrorProcessingTask</span><span class="sxs-lookup"><span data-stu-id="358e6-122">ErrorProcessingTask</span></span> |<span data-ttu-id="358e6-123">Kategoria innych błędów, które procesor multimediów napotka podczas przetwarzania zadania niezwiązane zawartości.</span><span class="sxs-lookup"><span data-stu-id="358e6-123">Category of other errors that the media processor encounters during the processing of the task that are unrelated to content.</span></span> |
| <span data-ttu-id="358e6-124">ErrorUploadingOutputAsset</span><span class="sxs-lookup"><span data-stu-id="358e6-124">ErrorUploadingOutputAsset</span></span> |<span data-ttu-id="358e6-125">Kategoria błędy podczas przekazywania elementu zawartości wyjściowej</span><span class="sxs-lookup"><span data-stu-id="358e6-125">Category of errors when uploading the output asset</span></span> |
| <span data-ttu-id="358e6-126">ErrorCancelingTask</span><span class="sxs-lookup"><span data-stu-id="358e6-126">ErrorCancelingTask</span></span> |<span data-ttu-id="358e6-127">Kategoria błędów, aby pokrywał błędy przy próbie anulowania zadania</span><span class="sxs-lookup"><span data-stu-id="358e6-127">Category of errors to cover failures when attempting to cancel the Task</span></span> |
| <span data-ttu-id="358e6-128">TransientError</span><span class="sxs-lookup"><span data-stu-id="358e6-128">TransientError</span></span> |<span data-ttu-id="358e6-129">Kategoria błędów, aby pokrywał przejściowych problemów (np.)</span><span class="sxs-lookup"><span data-stu-id="358e6-129">Category of errors to cover transient issues (eg.</span></span> <span data-ttu-id="358e6-130">tymczasowe problemy z siecią z usługą Azure Storage)</span><span class="sxs-lookup"><span data-stu-id="358e6-130">temporary networking issues with Azure Storage)</span></span> |

<span data-ttu-id="358e6-131">Aby uzyskać pomoc od **Media Services** zespół, otwórz [obsługuje biletu](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span><span class="sxs-lookup"><span data-stu-id="358e6-131">To get help from the **Media Services** team, open a [support ticket](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="358e6-132">Ścieżki szkoleniowe dotyczące usługi Media Services</span><span class="sxs-lookup"><span data-stu-id="358e6-132">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="358e6-133">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="358e6-133">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-articles"></a><span data-ttu-id="358e6-134">Pokrewne artykuły:</span><span class="sxs-lookup"><span data-stu-id="358e6-134">Related articles</span></span>
* [<span data-ttu-id="358e6-135">Wykonywania zaawansowanych zadań kodowania dostosowując ustawienia standardu Media Encoder Standard</span><span class="sxs-lookup"><span data-stu-id="358e6-135">Perform advanced encoding tasks by customizing Media Encoder Standard presets</span></span>](media-services-custom-mes-presets-with-dotnet.md)
* [<span data-ttu-id="358e6-136">Przydziały i ograniczenia</span><span class="sxs-lookup"><span data-stu-id="358e6-136">Quotas and Limitations</span></span>](media-services-quotas-and-limitations.md)

<!--Reference links in article-->
[1]: http://azure.microsoft.com/pricing/details/media-services/
