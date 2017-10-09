---
title: "często zadawane pytania dotyczące usługi Media Services aaaAzure | Dokumentacja firmy Microsoft"
description: "Często zadawane pytania (FAQ)"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 5374f7f4-c189-43ef-8b7f-f2f4141e2748
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: juliako
ms.openlocfilehash: 6d48a5c1291f3c2559d8445921d571718d0a0a6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions"></a>Często zadawane pytania

W tym artykule opisano często zadawane pytania zgłoszone przez społeczność użytkowników programu hello Azure Media Services (AMS).

## <a name="general-ams-faqs"></a>Często zadawane pytania ogólne AMS
Pytanie: jak można skalować, indeksowania?

A: jednostki zarezerwowane hello są hello tego samego kodowanie i zadania indeksowania. Postępuj zgodnie z instrukcjami wyświetlanymi [jak tooScale kodowanie jednostki zarezerwowanego](media-services-scale-media-processing-overview.md). **Uwaga** czy wydajność indeksatora nie ma wpływu na typ jednostki zarezerwowane.

Pytanie: I przekazany, zakodowany i publikowane wideo. Jakie byłyby hello Przyczyna hello wideo nie jest odtwarzany podczas toostream go?

Odpowiedź: jeden hello najczęściej powodów, dla których jest hello, z którym próbujesz tooplayback w hello punktu końcowego przesyłania strumieniowego nie ma **systemem** stanu.  

Pytanie: czy można składania na strumień na żywo?

A: składania na strumienie na żywo aktualnie nie jest oferowany usługi Azure Media Services, więc musisz toopre-tworzą na komputerze.

Pytanie: czy za pomocą usługi Azure CDN transmisji strumieniowej na żywo?

Odpowiedź: Media Services obsługuje integrację z usługą Azure CDN (Aby uzyskać więcej informacji, zobacz [jak punkty końcowe przesyłania strumieniowego tooManage w konta usługi Media Services](media-services-portal-manage-streaming-endpoints.md)).  Możesz użyć Live streaming sieci CDN. Azure Media Services udostępnia Smooth Streaming, HLS i MPEG-DASH danych wyjściowych. Wszystkie te formaty do przesyłania danych za pomocą protokołu HTTP i uzyskać korzyści buforowania HTTP. Na żywo, przesyłania strumieniowego audio/wideo dane jest podzielony toofragments i to poszczególne fragmenty pobrać buforowane w sieci CDN. Tylko dane potrzeb toobe odświeżyć jest hello manifestu danych. CDN okresowo odświeża dane manifestu.

Pytanie: jest usługa Azure Media services obsługuje przechowywania obrazów?

Odpowiedź: Jeśli chcesz tylko toostore JPEG lub PNG obrazów, należy przechowywać w magazynie obiektów Blob Azure. Nie ma żadnych tooputting korzyści, które je w usługach nośnika konta, dopóki nie ma tookeep ich skojarzony z wideo lub Audio zasoby. Lub może zajść potrzeba toouse hello obrazów jako nakładki na powitania koder wideo. Media Encoder Standard obsługuje nakładanie obrazów na górze wideo i to, co wyświetlane JPEG lub PNG jako obsługiwane formaty wejściowych. Aby uzyskać więcej informacji, zobacz [tworzenie nakładki](media-services-advanced-encoding-with-mes.md#overlay).

Pytanie: jak kopiowanie zasobów z jednego tooanother konta usługi Media Services.

A: Użyj toocopy zasoby z jednej tooanother konta usługi Media Services przy użyciu platformy .NET, [IAsset.Copy](https://github.com/Azure/azure-sdk-for-media-services-extensions/blob/dev/MediaServices.Client.Extensions/IAssetExtensions.cs#L354) — metoda rozszerzenia dostępne w hello [rozszerzenia SDK .NET usługi Azure Media Services](https://github.com/Azure/azure-sdk-for-media-services-extensions/) repozytorium. Aby uzyskać więcej informacji, zobacz [to](https://social.msdn.microsoft.com/Forums/azure/28912d5d-6733-41c1-b27d-5d5dff2695ca/migrate-media-services-across-subscription?forum=MediaServices) forum wątku.

Pytanie: jakie są hello obsługiwane znaki nazewnictwa plików podczas pracy z AMS?

A: Media Services używa wartości hello hello właściwość IAssetFile.Name podczas kompilowania adresów URL dla hello przesyłania strumieniowego zawartości (na przykład http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) Z tego powodu kodowania procent jest niedozwolone. Hello wartość hello **nazwa** właściwość nie może mieć jedną z następujących przyczyn hello [procent kodowanie zarezerwowanych znaków](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters):! * "();: @& = + $, /? [] % #". Ponadto może istnieć tylko jeden "." dla hello rozszerzenia nazwy pliku.

Pytanie: jak przy użyciu tooconnect REST?

Odp.: Aby uzyskać informacje dotyczące tooconnect toohello AMS interfejsu API, zobacz temat [hello dostępu do interfejsu API usługi Azure Media Services przy użyciu uwierzytelniania usługi Azure AD](media-services-use-aad-auth-to-access-ams-api.md). Po pomyślnym połączeniu toohttps://media.windows.net, otrzymasz 301 przekierowanie, określając inny identyfikator URI usługi multimediów. Należy wykonać kolejne wywołania toohello nowy identyfikator URI. 

Pytanie: jak obrócić wideo podczas hello kodowanie procesu.

A: Witaj [Media Encoder Standard](media-services-dotnet-encode-with-media-encoder-standard.md) obsługuje obrotu kątami 90/180/270. Witaj domyślne zachowanie to "Auto", gdy próbuje toodetect hello obrotu metadane w pliku MP4/MOV przychodzących hello i kompensacji go. Uwzględnij następujące elementy hello **źródeł** tooone element hello json ustawień zdefiniowanych [tutaj](media-services-mes-presets-overview.md):

    "Version": 1.0,
    "Sources": [
    {
      "Streams": [],
      "Filters": {
        "Rotation": "90"
      }
    }
    ],
    "Codecs": [

    ...


## <a name="media-services-learning-paths"></a>Ścieżki szkoleniowe dotyczące usługi Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Przekazywanie opinii
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
