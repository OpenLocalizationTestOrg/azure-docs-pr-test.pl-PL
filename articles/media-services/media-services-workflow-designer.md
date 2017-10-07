---
title: "aaaCreate Zaawansowane kodowanie przepływów pracy za pomocą projektanta przepływów pracy | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat sposobu toocreate zaawansowane kodowania przepływów pracy za pomocą projektanta przepływów pracy."
services: media-services
documentationcenter: 
author: anilmur
manager: cfowler
editor: 
ms.assetid: 004815f2-0761-4706-87a1-675ba36e0322
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: juliako;johndeu;anilmur
ms.openlocfilehash: 3744cde54c78bec7c7b586962ec1a8fe9529c1d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-advanced-encoding-workflows-with-workflow-designer"></a>Tworzenie zaawansowanych przepływów pracy kodowania za pomocą projektanta przepływu pracy
## <a name="overview"></a>Omówienie
Witaj **projektanta przepływów pracy** jest narzędziem pulpitu systemu Windows, które jest używane toodesign kompilacji niestandardowe przepływy pracy i do kodowania z **Media Encoder Premium w przepływie pracy**.
Przy użyciu zasilania hello narzędzia projektanta workflow hello, projektowania i tworzenia złożonych przepływów pracy, które będą uruchamiane w **Media Encoder Premium**.  

Przepływy pracy mogą zawierać logiki decyzji klienta i rozgałęzianie na podstawie pliku źródła danych wejściowych hello właściwości. Można tworzyć przepływy pracy z możliwością przesłonięcia właściwości i wartości dynamiczne toomake hello nawet najbardziej złożoną kodowania zadań łatwe toorepeat i dostosowywać w chmurze hello.

Przykład przepływy pracy, które możesz utworzyć obejmują:

* Przepływy pracy, które kontrolują hello źródła zawartości do rozpoznania i kodowanie tylko hello potrzebne dane wyjściowe śledzi oparte na decyzji.  Jest to helfpul przez wyeliminowanie śledzi hello niewykorzystana, wygenerowanych przez upscaling inadvertantly zawartości hello źródła.
* Wiele plików wejściowych mogą być używane toosupport podpisów, nakładki i łączenie zawartości razem. 

To narzędzie można też używane toomodify żadnego z naszych [opublikowane przepływy pracy](media-services-workflow-designer.md#existing_workflows). 

> [!NOTE]
> tooget kopii hello narzędzia projektanta przepływów pracy, skontaktuj się z mepd@microsoft.com.
> 
> 

Po utworzeniu pliku przepływu pracy mogą być przekazywane jako zasób, a następnie używany do kodowania plików multimedialnych. Aby uzyskać informacje na temat tooencode z **Media Encoder Premium w przepływie pracy** przy użyciu **.NET**, zobacz [zaawansowane kodowania w przepływie pracy Premium kodera multimediów](media-services-encode-with-premium-workflow.md).

## <a id="existing_workflows"></a>Modyfikowanie istniejących przepływów pracy
Witaj domyślne [opublikowane przepływy pracy](media-services-workflow-designer.md#existing_workflows) można modyfikować przy użyciu narzędzia Projektant hello. Można uzyskać domyślnego hello pliki przepływu pracy [tutaj](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows). Hello folder zawiera również opis hello tych plików.

Witaj następujące filmy wideo pokazują, jak toouse hello projektanta.

### <a name="day-1--getting-started"></a>Dzień 1 — wprowadzenie
Obejmuje 1 dzień wideo:

* Omówienie projektanta
* Podstawowych przepływów pracy — "Hello World"
* Tworzenie wielu wyjściowe pliki MP4 używane przez usługi Azure Media Services przesyłania strumieniowego

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-Premium-Encoder-Workflow-Designer-Training-Videos-Day-1/player]
> 
> 

### <a name="day-2"></a>Dzień 2
Wideo dzień 2 obejmuje:

* Różne scenariusze źródła plików — Obsługa audio
* Przepływy pracy z logiką zaawansowane
* Etapy wykresu

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-Premium-Encoder-Workflow-Designer-Training-Videos-Day-2/player]
> 
> 

### <a name="day-3"></a>3 dni
Obejmuje 3 dni wideo:

* Wykonywanie skryptów wewnątrz przepływy pracy/plany
* Ograniczenia z hello bieżącego kodera
* FUNKCJA PYTANIA I ODPOWIEDZI

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-Premium-Encoder-Workflow-Designer-Training-Videos-Day-3/player]
> 
> 

## <a name="next-step"></a>Następny krok
Przejrzyj ścieżki szkoleniowe dotyczące usługi Media Services.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Przekazywanie opinii
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

Jeśli muszą obsługiwać lub pytań na temat tworzenia niestandardowych przepływów pracy w narzędziu Projektant hello przepływu pracy, Wyślij wiadomość e-mail toomepd@microsoft.com.

## <a name="see-also"></a>Zobacz też
[Filmy szkoleniowe projektanta przepływu pracy kodera Azure — warstwa Premium](http://johndeutscher.com/2015/07/06/azure-premium-encoder-workflow-designer-training-videos/)

