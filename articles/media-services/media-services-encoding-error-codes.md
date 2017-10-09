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
# <a name="encoding-error-codes"></a>Kodowanie kody błędów

Witaj następującej tabeli opisano kody błędów, które mogą być zwracane w przypadku Napotkano błąd podczas hello kodowanie wykonywania zadania.  Szczegóły błędu tooget w kodzie .NET, użyj hello [szczegóły błędu](http://msdn.microsoft.com/library/microsoft.windowsazure.mediaservices.client.errordetail.aspx) klasy. Szczegóły błędu tooget w kodzie REST, użyj hello [ErrorDetail](https://msdn.microsoft.com/library/jj853026.aspx) interfejsu API REST.

| ErrorDetail.Code | Możliwe przyczyny błędu |
| --- | --- |
| Nieznany |Wystąpił nieznany błąd podczas wykonywania zadania hello |
| ErrorDownloadingInputAssetMalformedContent |Kategorii błędów, który obejmuje błędy w czasie pobierania wejściowych zasobów, takich jak nazwy uszkodzonych plików, zero pliki o długości, niepoprawny formatuje i tak dalej. |
| ErrorDownloadingInputAssetServiceFailure |Kategoria błędów, który obejmuje problemów po stronie usługi hello — na przykład sieci lub magazynu błędy podczas pobierania. |
| ErrorParsingConfiguration |Kategoria błędów, gdy zadanie <see cref="MediaTask.PrivateData"/> (Konfiguracja) jest nieprawidłowa, na przykład hello konfiguracji nie jest poprawnym systemem ustawienia wstępnego lub zawiera nieprawidłowy kod XML. |
| ErrorExecutingTaskMalformedContent |Kategoria błędy podczas wykonywania hello hello zadania, których problemów wewnątrz hello wejściowej plików multimedialnych spowodować niepowodzenie. |
| ErrorExecutingTaskUnsupportedFormat |Kategoria błędy, gdy procesor multimediów hello nie może przetworzyć plików hello — formatu media nie obsługiwany lub nie odpowiada hello konfiguracji. Na przykład w trakcie tooproduce tylko dźwięk dane wyjściowe z zasobu, który zawiera tylko wideo |
| ErrorProcessingTask |Podczas przetwarzania hello hello zadanie, które są toocontent niepowiązanych napotka kategorii innych błędów, które hello procesor multimediów. |
| ErrorUploadingOutputAsset |Kategoria błędy podczas wysyłania zawartości wyjściowej hello |
| ErrorCancelingTask |Kategoria niepowodzeń toocover błędy podczas próby hello toocancel zadań |
| TransientError |Kategoria błędy toocover przejściowych problemów (np.) tymczasowe problemy z siecią z usługą Azure Storage) |

Pomoc tooget od hello **Media Services** zespół, otwórz [obsługuje biletu](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade).

## <a name="media-services-learning-paths"></a>Ścieżki szkoleniowe dotyczące usługi Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Przekazywanie opinii
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-articles"></a>Pokrewne artykuły:
* [Wykonywania zaawansowanych zadań kodowania dostosowując ustawienia standardu Media Encoder Standard](media-services-custom-mes-presets-with-dotnet.md)
* [Przydziały i ograniczenia](media-services-quotas-and-limitations.md)

<!--Reference links in article-->
[1]: http://azure.microsoft.com/pricing/details/media-services/
