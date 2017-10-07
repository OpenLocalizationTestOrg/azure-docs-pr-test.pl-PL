---
title: aaaDevelop aplikacji odtwarzacza wideo
description: "Hello temacie zamieszczono linki tooPlayer platform i wtyczek, których można używać toodevelop własnych aplikacji klienckich, które multimediów strumieniowych dostarczanych z usługi Media Services."
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 55e419fc-4c39-4902-9c62-f41cfcd86c6c
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: juliako
ms.openlocfilehash: a66daa4f006a1f05271cc9ed6a02ea7ee460321d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="develop-video-player-applications"></a>Opracowywanie aplikacji odtwarzacza wideo
## <a name="overview"></a>Omówienie
Usługa Azure Media Services udostępnia hello narzędzi można muszą sformatowanego toocreate aplikacji dynamicznej klienckich odtwarzacza dla większości platform, w tym: iOS urządzeń, urządzenia z systemem Android, Windows, Windows Phone, Xbox i dekodera pola. Ten temat zawiera również linki tooSDKs oraz struktur odtwarzaczy, których można używać toodevelop własnych aplikacji klienckich, które multimediów strumieniowych dostarczanych z usługą Azure Media Services.

>[!NOTE]
>Po utworzeniu konta usługi AMS **domyślne** punktu końcowego przesyłania strumieniowego w brzmieniu konta tooyour hello **zatrzymane** stanu. przesyłanie strumieniowe zawartości i podejmij korzyści z dynamicznego tworzenia pakietów i dynamicznego szyfrowania toostart hello punktu końcowego przesyłania strumieniowego, z którego mają zostać toostream zawartość ma toobe w hello **systemem** stanu. 
 
## <a name="azure-media-player"></a>Azure Media Player
[Azure Media Player](http://aka.ms/ampinfo) odtwarzacza wideo w sieci web składa się zawartości multimedialnej wstecz tooplay z usługi Microsoft Azure Media Services na różnych przeglądarkach i urządzeniach. Azure Media Player wykorzystuje standardy branżowe, takie jak tooprovide nośnika źródłowego rozszerzenia (MSE), szyfrowane nośnika rozszerzenia (EME) i HTML5 wzbogaconego adaptacyjną obsługi przesyłania strumieniowego. Jeśli te standardy są niedostępne na urządzeniu lub w przeglądarce, Azure Media Player używa Flash i Silverlight jako rezerwowy technologii. Niezależnie od technologii odtwarzania hello używany deweloperzy mają ujednoliconego tooaccess interfejsu JavaScript API. Dzięki temu obsługiwanej przez usługi Azure Media Services toobe odtwarzane w zakresie sieci, urządzeń i przeglądarki bez żadnych dodatkowych nakładów zawartości.

Microsoft Azure Media Services umożliwia zawartości toobe obsługiwane z DASH, Smooth Streaming i przesyłania strumieniowego tooplay formatów HLS kopię zawartości. Azure Media Player uwzględnia tych różnych formatach i automatycznie odtwarza hello łączy najlepsze hello możliwości platformy/przeglądarki. Microsoft Azure Media Services umożliwia również szyfrowania dynamicznego zasobów z szyfrowaniem PlayReady lub AES-128-bitowego szyfrowania koperty. Azure Media Player umożliwia odszyfrowanie PlayReady i AES-128-bitowego zaszyfrowaną zawartość, gdy jest skonfigurowany prawidłowo. 

Więcej informacji:

* [Azure Media Player](http://aka.ms/ampinfo)
* [Azure Media Player dokumentacji](http://aka.ms/ampdocs) 
* [Azure Media Player pobieranie rozpoczęto blogu](https://azure.microsoft.com/blog/2015/04/15/announcing-azure-media-player/)
* [Zarejestruj się toostay się toodate z hello najnowszych z usługi Azure Media Player](http://aka.ms/ampsignup)
* [Dodaj nowe żądania dotyczące funkcji, pomysły, opinie](http://aka.ms/ampuservoice) 

## <a name="other-tools-for-creating-player-applications"></a>Inne narzędzia do tworzenia aplikacji odtwarzacza
Można również użyć dowolnego z następujących zestawów SDK hello:

* [Smooth Streaming Client w zestawie SDK](http://www.iis.net/downloads/microsoft/smooth-streaming) 
* [Płynnego przesyłania strumieniowego aplikacji ze Sklepu Windows](media-services-build-smooth-streaming-apps.md)
* [Platformy Media firmy Microsoft: Framework Player](http://playerframework.codeplex.com/) 
* [HTML5 Dokumentację Framework Player](http://playerframework.codeplex.com/wikipage?title=HTML5%20Player&referringTitle=Documentation) 
* [Microsoft Smooth Streaming wtyczki dla OSMF](https://www.microsoft.com/download/details.aspx?id=36057) 
* [Licencjonowania Microsoft® Smooth Streaming Client Eksportowanie zestawu](http://aka.ms/sspk) 
* [Projektowanie aplikacji wideo XBOX](http://xbox.create.msdn.com/) 

## <a name="advertising"></a>Anonsowanie
Usługa Azure Media Services obsługuje wstawiania reklam za pośrednictwem platformy Media Windows hello: struktur odtwarzaczy. Struktur odtwarzaczy z obsługą ad są dostępne dla urządzeń z systemem Windows 8, Silverlight, Windows Phone 8 i iOS. Każdy framework player zawiera przykładowy kod, przedstawiający sposób tooimplement aplikacja odtwarzacza. Istnieją trzy różne rodzaje reklamy, które można wstawić do multimediów:

Liniowy — reklam pełne ramki Wstrzymaj hello głównego wideo

Rożne — nakładki reklamy, które są wyświetlane podczas odtwarzania wideo głównego hello, zwykle logo lub innego obrazu statycznych, umieszczony hello player

Pomocnik — reklam wyświetlanych poza hello player

Usługa AD można umieścić w dowolnym momencie hello wideo głównych osi czasu. Gdy tooplay hello ad, które należy wskazać hello player tooplay reklam. Jest to realizowane przy użyciu zestawu standardowych plików opartych na języku XML: wideo Ad Service szablonu (VAST), cyfrowy wideo wielu Ad listy odtwarzania (VMAP) nośnika abstrakcyjny sekwencjonowania szablonu (MASZTÓW) i cyfrowy wideo Player Ad interfejsu definicji (VPAID). Pliki PRZEWAŻAJĄCA określają, jakie toodisplay reklam. Pliki VMAP Określ, kiedy tooplay różnych reklam i zawierać PRZEWAŻAJĄCA XML. Pliki MASZTÓW są inny sposób toosequence reklam, które również mogą zawierać PRZEWAŻAJĄCA XML. Pliki VPAID zdefiniuj interfejs między hello odtwarzacza wideo i hello ad lub serwera usługi ad. Aby uzyskać więcej informacji, zobacz [wstawiania reklam](https://msdn.microsoft.com/library/dn387398.aspx).

Informacje o kodowane i obsługę reklam w wideo transmisji strumieniowej na żywo, zobacz [obsługiwane kodowane i standardy wstawiania Ad](https://msdn.microsoft.com/library/c49e0b4d-357e-4cca-95e5-2288924d1ff3#caption_ad).

## <a name="media-services-learning-paths"></a>Ścieżki szkoleniowe dotyczące usługi Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Przekazywanie opinii
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>Zobacz też
[Osadzanie plików wideo adaptacyjnego przesyłania strumieniowego MPEG-DASH w aplikacji HTML5 z implementacją DASH.js](media-services-embed-mpeg-dash-in-html5.md)

[Repozytorium GitHub dash.js](https://github.com/Dash-Industry-Forum/dash.js)

