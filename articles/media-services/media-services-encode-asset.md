---
title: "aaaOverview i porównanie Azure na żądanie koderów nośnika | Dokumentacja firmy Microsoft"
description: "Ten temat zawiera omówienie i porównanie Azure na żądanie koderów nośnika."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: e6bfc068-fa46-4d68-b1ce-9092c8f3a3c9
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/10/2017
ms.author: juliako
ms.openlocfilehash: 24a3e0a16162b1bebfcde290b6baf2dd8dbfff17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="overview-and-comparison-of-azure-on-demand-media-encoders"></a>Omówienie i porównanie Azure na żądanie nośnika koderów
## <a name="encoding-overview"></a>Omówienie kodowania
Azure Media Services udostępnia wiele opcji hello kodowania nośnika w chmurze hello.

Podczas uruchamiania z programem Media Services, jest ważne toounderstand hello różnica między koderów-dekoderów i plik formatu.
Kodery-dekodery hello oprogramowania, które implementuje algorytmy kompresji i dekompresji hello formatów plików są kontenery zawierających hello skompresowane wideo.

Usługa Media Services udostępnia funkcję dynamicznego tworzenia pakietów, co pozwala toodeliver Twojego o adaptacyjnej szybkości bitowej MP4 lub Smooth Streaming zakodowane zawartości w formatach transmisji strumieniowej obsługiwanych przez usługę Media Services (MPEG DASH, HLS, Smooth Streaming) bez konieczności toore pakietów w tych formatach transmisji strumieniowej.

>[!NOTE]
>Po utworzeniu konta usługi AMS **domyślne** punktu końcowego przesyłania strumieniowego w brzmieniu konta tooyour hello **zatrzymane** stanu. przesyłanie strumieniowe zawartości i podejmij korzyści z dynamicznego tworzenia pakietów i dynamicznego szyfrowania toostart hello punktu końcowego przesyłania strumieniowego, z którego mają zostać toostream zawartość ma toobe w hello **systemem** stanu. Zaletą tootake [dynamicznego tworzenia pakietów](media-services-dynamic-packaging-overview.md), należy toodo hello poniżej:
>
>Ponadto kodowanie pliku źródłowego do zestawu plików MP4 lub pliki Smooth Streaming adaptacyjną szybkością transmisji bitów (kroki kodowania hello przedstawiono w dalszej części tego samouczka).

Usługa Media Services obsługuje następujące hello na koderów żądanie, które zostały opisane w tym artykule:

* [Usługa Media Encoder Standard](media-services-encode-asset.md#media-encoder-standard)
* [Przepływ pracy usługi Media Encoder w warstwie Premium](media-services-encode-asset.md#media-encoder-premium-workflow)

Ten artykuł zawiera krótki przegląd na żądanie koderów nośnika i zapewnia tooarticles łącza, które zapewniają bardziej szczegółowe informacje. Witaj temat zawiera również porównania koderów hello.

>[!NOTE]
>Domyślnie wszystkie konta usługi Media Services może mieć aktywne zadania kodowania w czasie. Jednostki kodowania, które pozwalają toohave może zarezerwować wielu zadań kodowania uruchomione jednocześnie, po jednej dla każdego kodowania jednostka zarezerwowanego zakupu. Aby uzyskać informacje, zobacz [skalowania jednostki kodowania](media-services-scale-media-processing-overview.md).

## <a name="media-encoder-standard"></a>Usługa Media Encoder Standard
### <a name="how-toouse"></a>Jak toouse
[Jak tooencode przy użyciu Media Encoder Standard](media-services-dotnet-encode-with-media-encoder-standard.md)

### <a name="formats"></a>Formaty
[Koderów-dekoderów i formaty](media-services-media-encoder-standard-formats.md)

### <a name="presets"></a>Ustawienia
Media Encoder Standard została skonfigurowana przy użyciu jednego ustawień kodera hello opisane [tutaj](http://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409).

### <a name="input-and-output-metadata"></a>Wejście i wyjście metadanych
Hello metadanych wejściowych koderów opisano [tutaj](media-services-input-metadata-schema.md).

Hello koderów dane wyjściowe metadanych opisano [tutaj](media-services-output-metadata-schema.md).

### <a name="generate-thumbnails"></a>Generowanie miniatur
Aby uzyskać informacje, zobacz [jak miniatur toogenerate przy użyciu standardu Media Encoder Standard](media-services-advanced-encoding-with-mes.md#thumbnails).

### <a name="trim-videos-clipping"></a>TRIM wideo (wycinka)
Aby uzyskać informacje, zobacz [jak tootrim pliki wideo przy użyciu standardu Media Encoder Standard](media-services-advanced-encoding-with-mes.md#trim_video).

### <a name="create-overlays"></a>Utwórz nakładki
Aby uzyskać informacje, zobacz [jak nakładki toocreate przy użyciu standardu Media Encoder Standard](media-services-advanced-encoding-with-mes.md#overlay).

### <a name="see-also"></a>Zobacz też
[blog usługi Media Services Hello](https://azure.microsoft.com/blog/2015/07/16/announcing-the-general-availability-of-media-encoder-standard/)

## <a name="media-encoder-premium-workflow"></a>Przepływ pracy usługi Media Encoder w warstwie Premium
### <a name="overview"></a>Omówienie
[Wprowadzenie do kodowania w Azure Media Services w wersji Premium](https://azure.microsoft.com/blog/2015/03/05/introducing-premium-encoding-in-azure-media-services/)

### <a name="how-toouse"></a>Jak toouse
Media Encoder Premium w przepływie pracy jest skonfigurowana przy użyciu złożonych przepływów pracy. Pliki przepływu pracy może zostać utworzony i zaktualizować przy użyciu hello [projektanta przepływów pracy](media-services-workflow-designer.md) narzędzia.

[Jak tooUse Premium kodowania w usłudze Azure Media Services](https://azure.microsoft.com/blog/2015/03/06/how-to-use-premium-encoding-in-azure-media-services/)

### <a name="known-issues"></a>Znane problemy
Jeśli wejściowy plik wideo nie zawiera kodowane, hello wyjściowe zasobów nadal będzie zawierać pusty plik TTML.


## <a name="media-services-learning-paths"></a>Ścieżki szkoleniowe dotyczące usługi Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Przekazywanie opinii
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-articles"></a>Pokrewne artykuły:
* [Wykonywania zaawansowanych zadań kodowania dostosowując ustawienia standardu Media Encoder Standard](media-services-custom-mes-presets-with-dotnet.md)
* [Przydziały i ograniczenia](media-services-quotas-and-limitations.md)

<!--Reference links in article-->
[1]: http://azure.microsoft.com/pricing/details/media-services/
