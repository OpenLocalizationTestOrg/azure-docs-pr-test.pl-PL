---
title: aaaUsing castLabs toodeliver Widevine licencje tooAzure Media Services | Dokumentacja firmy Microsoft
description: "W tym artykule opisano, jak używasz usługi Azure Media Services (AMS) toodeliver dynamicznie szyfrowanych przez AMS z PlayReady i Widevine DRMs strumienia. licencji PlayReady Hello pochodzi z serwera licencji Media Services PlayReady i licencji Widevine jest dostarczany przez serwer licencji castLabs."
services: media-services
documentationcenter: 
author: Mingfeiy
manager: cfowler
editor: 
ms.assetid: 2a9a408a-a995-49e1-8d8f-ac5b51e17d40
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: Mingfeiy;willzhan;Juliako
ms.openlocfilehash: 80d2778fb283a96361e7e511990a36c2f551a310
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="using-castlabs-toodeliver-widevine-licenses-tooazure-media-services"></a>Przy użyciu castLabs toodeliver Widevine licencji tooAzure Media Services
> [!div class="op_single_selector"]
> * [Axinom](media-services-axinom-integration.md)
> * [castLabs](media-services-castlabs-integration.md)
> 
> 

## <a name="overview"></a>Omówienie
W tym artykule opisano, jak używasz usługi Azure Media Services (AMS) toodeliver dynamicznie szyfrowanych przez AMS z PlayReady i Widevine DRMs strumienia. licencji PlayReady Hello pochodzi z serwera licencji Media Services PlayReady i licencji Widevine jest dostarczany przez **castLabs** serwera licencji.

tooplayback przesyłania strumieniowego zawartości chronionej przez CENC (PlayReady i Widevine), możesz użyć [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html). Zobacz [dokumentu AMP](http://amp.azure.net/libs/amp/latest/docs/) szczegółowe informacje.

powitania po diagram przedstawia wysokiego poziomu architektury integracji usługi Azure Media Services i castLabs.

![Integracja](./media/media-services-castlabs-integration/media-services-castlabs-integration.png)

## <a name="typical-system-set-up"></a>Typowy systemem
* Nośnik zawartość jest przechowywana w AMS.
* Identyfikatory klucz zawartości kluczy są przechowywane w castLabs i AMS.
* castLabs i AMS ma token uwierzytelniania wbudowane. Hello w następujących sekcjach omówiono w nim tokeny uwierzytelniania. 
* Gdy klient żąda toostream hello wideo, zawartość hello dynamicznie jest szyfrowana za **Common Encryption** (CENC) i dynamicznie opakowane przez AMS tooSmooth przesyłania strumieniowego i KRESKI. Możemy również zapewniać PlayReady M2TS podstawowe strumienia szyfrowania dla protokołu HLS protokołu przesyłania strumieniowego.
* Licencja PlayReady są pobierane z serwera licencji usług AMS i licencji Widevine są pobierane z serwera licencji castLabs. 
* Odtwarzacz automatycznie decyduje, które toofetch licencji, w oparciu o możliwości platformy powitania klienta. 

## <a name="authentication-token-generation-for-getting-a-license"></a>Generowanie tokenu uwierzytelniania dla pobierania licencji
Zarówno castLabs, jak i AMS obsługuje tooauthorize używany format tokenu JWT (JSON Web Token) licencji. 

### <a name="jwt-token-in-ams"></a>Token JWT w AMS
Witaj w poniższej tabeli opisano tokenu JWT w AMS. 

| Wystawcy | Ciąg wystawcy z hello wybrany Secure Token Service (STS) |
| --- | --- |
| Grupy odbiorców |Ciąg odbiorców z hello używany STS |
| Oświadczenia |Zestaw oświadczeń |
| Nie wcześniej niż |Ważność tokenu hello Start |
| Wygasa |Ważność tokenu hello zakończenia |
| Elementu SigningCredentials |klucz Hello, użytkowany przez serwer licencji PlayReady, castLabs serwera licencji i STS, może to być klucz konfiguracji symetrycznej lub asymetrycznej. |

### <a name="jwt-token-in-castlabs"></a>Token JWT w castLabs
Witaj w poniższej tabeli opisano tokenu JWT w castLabs. 

| Nazwa | Opis |
| --- | --- |
| optData |Ciąg JSON zawierający informacje o Tobie. |
| CRT |JSON ciąg zawierający informacje o hello zasobów, jego informacje o i odtwarzania praw licencyjnych. |
| IAT |Hello bieżącej daty/godziny w epoki. |
| jti |Unikatowy identyfikator o token (token, co może być użyte tylko raz w systemie castLabs hello). |

## <a name="sample-solution-set-up"></a>Przykładowe rozwiązanie — Konfiguracja
Witaj [przykładowe rozwiązanie](https://github.com/AzureMediaServicesSamples/CastlabsIntegration) składa się z dwóch projektów:

* Aplikacja konsoli, które mogą być używane tooset DRM ograniczenia zasób już pozyskiwane PlayReady i Widevine.
* Aplikacja sieci Web, która przekazuje limit tokeny, których może być traktowany jako bardzo uproszczonej wersji usługi tokenu Zabezpieczającego.

Aplikacja konsolowa hello toouse:

1. Zmień hello app.config toosetup AMS poświadczeń, poświadczenia castLabs, konfiguracji usługi STS i klucza wspólnego.
2. Przekaż zasób do AMS.
3. Get hello UUID z hello przekazywane zasobów i zmienić 32 wiersz w pliku Program.cs hello:
   
      var objIAsset = _kontekstu. Assets.Where (x = > x.Id == "nb:cid:UUID:dac53a5d-1500-80bd-b864-f1e4b62594cf"). FirstOrDefault();
4. Użyj IDśrodkaTrwałego nazewnictwa hello zasobów w systemie castLabs hello (44 wiersz w pliku Program.cs hello).
   
   Należy ustawić IDśrodkaTrwałego dla **castLabs**; musi on toobe unikatowy ciąg alfanumeryczny.
5. Uruchom hello program.

Witaj toouse aplikacji sieci Web (STS):

1. Zmień hello web.config toosetup castlabs sprzedawcy Identyfikatora, konfiguracji usługi STS hello i hello klucza wspólnego.
2. Wdróż tooAzure witryn sieci Web.
3. Przejdź toohello witryny sieci Web.

## <a name="playing-back-a-video"></a>Odtwarzanie wideo
tooplayback wideo zaszyfrowane za pomocą wspólnego szyfrowania (PlayReady i Widevine), możesz użyć hello [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html). Podczas uruchamiania aplikacji konsoli hello, powtarzana hello Identyfikatora klucza zawartości i hello manifestu adresu URL.

1. Otwórz nową kartę, a następnie uruchom z STS: http://[yourStsName].azurewebsites.net/api/token/assetid/[yourCastLabsAssetId]/contentkeyid/[thecontentkeyid].
2. Przejdź za[Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).
3. Wklej hello URL przesyłania strumieniowego.
4. Kliknij przycisk hello **zaawansowane opcje** wyboru.
5. W hello **ochrony** listy rozwijanej wybierz PlayReady i Widevine.
6. Wklej token hello, pochodzący z sieci usługi STS w polu tekstowym Token hello. 
   
   serwer licencji castLab Hello nie jest konieczne hello "Bearer =" prefiks przed hello tokenu. Dlatego należy usunąć przed przesłaniem hello token.
7. Aktualizacja hello player.
8. powinien być odtwarzanie Hello wideo.

## <a name="media-services-learning-paths"></a>Ścieżki szkoleniowe dotyczące usługi Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Przekazywanie opinii
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

