---
title: "aaaProtect zawartości przy użyciu usługi Azure Media Services | Dokumentacja firmy Microsoft"
description: "W tym artykule nadaj Omówienie ochrony zawartości z usługi Media Services."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 81bc00e1-dcda-4d69-b9ab-8768b793422b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: juliako
ms.openlocfilehash: abab7602d71d7357a692976420ca9a988c0d096f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="protecting-content-overview"></a>Ochrona zawartości — omówienie
Microsoft Azure Media Services umożliwia toosecure możesz z hello razem, gdy opuszczą komputera za pośrednictwem przechowywania, przetwarzania i dostarczania multimediów. Usługa Media Services umożliwia toodeliver zawartości na żywo i na żądanie dynamicznie szyfrowany za pomocą Standard AES (Advanced Encryption) (przy użyciu kluczy szyfrowania 128-bitowego) lub jedną z głównych DRMs hello: Microsoft PlayReady, Google Widevine i FairPlay firmy Apple. Usługa Media Services udostępnia usługę dostarczania kluczy AES i klientów tooauthorized udziela licencji DRM (PlayReady, Widevine i FairPlay). 

powitania po obraz pokazuje hello przepływów pracy ochrony zawartości, które obsługuje AMS. 

![Ochrona za pomocą PlayReady](./media/media-services-content-protection-overview/media-services-content-protection-with-multi-drm.png)

>[!NOTE]
>Po utworzeniu konta usługi AMS **domyślne** punktu końcowego przesyłania strumieniowego w brzmieniu konta tooyour hello **zatrzymane** stanu. przesyłanie strumieniowe zawartości i podejmij korzyści z dynamicznego tworzenia pakietów i dynamicznego szyfrowania toostart hello punktu końcowego przesyłania strumieniowego, z którego mają zostać toostream zawartość ma toobe w hello **systemem** stanu. 

W tym temacie opisano [pojęcia i terminologię](media-services-content-protection-overview.md) odpowiednich toounderstanding ochrony zawartości przy użyciu usługi AMS. Witaj zawiera on również [łącza](media-services-content-protection-overview.md#common-scenarios) tootopics, które pokazują, jak tooachieve zawartości zadania ochrony. 

## <a name="dynamic-encryption"></a>Szyfrowania dynamicznego
Microsoft Azure Media Services umożliwia toodeliver zawartości dynamicznie szyfrowany za pomocą szyfrowania DRM lub wyczyść klucza AES: Microsoft PlayReady, Google Widevine i FairPlay firmy Apple.

Obecnie można zaszyfrować hello następujących formatów przesyłania strumieniowego: HLS, MPEG DASH i Smooth Streaming. Nie można zaszyfrować pobierania progresywnego.

Jeśli chcesz dla usługi Media Services tooencrypt zasób, należy tooassociate klucza szyfrowania (CommonEncryption lub EnvelopeEncryption) z zawartości i również skonfigurować zasady autoryzacji klucza hello.

Należy również zasady dostarczania tooconfigure hello zasobów. Toostream zasób zaszyfrowanych magazynu, należy się toospecify sposób toodeliver jej Konfigurowanie zasad dostarczania elementów zawartości.

Gdy odtwarzacza zażąda strumienia, usługa Media Services używa hello określony toodynamically klucza szyfrowania z zawartości przy użyciu klucza czyszczenia AES lub szyfrowania DRM. toodecrypt hello strumienia, hello odtwarzacza zażąda hello klucza z usługi dostarczania klucza hello. toodecide czy hello użytkownik jest autoryzowany tooget hello klucza, usługi hello ocenia zasady autoryzacji hello określonych hello klucza.


## <a name="storage-encryption"></a>Szyfrowanie magazynu
Użyj tooencrypt szyfrowania magazynu zawartości lokalnie za pomocą AES 256-bitowego, a następnie przekaż tooAzure magazynu, w którym są przechowywane szyfrowane, gdy. Elementy zawartości chronione przy użyciu szyfrowania magazynu są automatycznie bez szyfrowania i umieszczana w poprzednich tooencoding systemu szyfrowania plików i opcjonalnie ponownie szyfrowane przed toouploading zwrotnym w formie nowego elementu zawartości wyjściowej. Witaj pierwotnym zastosowaniem szyfrowania magazynu jest toosecure Twojego wysokiej jakości multimedialnych plików wejściowych pomocą silnego szyfrowania rest na dysku.

W kolejności toodeliver zasób zaszyfrowanych magazynu należy skonfigurować zasady dostarczania zasobów hello będzie wówczas traktował Media Services sposób toodeliver zawartości. Aby mogła być przesłana strumieniowo zawartości, hello i przesyłania strumieniowego szyfrowania magazynu hello usuwa strumieni zawartości przy użyciu hello określone zasady dostarczania (na przykład AES, wspólnego szyfrowania lub bez szyfrowania).

## <a name="common-encryption-cenc"></a>Szyfrowania Common encryption (CENC)
Typowe szyfrowania jest używane do szyfrowania zawartości przy użyciu PlayReady lub / i Widewine.

## <a name="using-cbcs-aapl-encryption"></a>Przy użyciu szyfrowania cbcs-aapl
Cbcs-aapl jest używane do szyfrowania zawartości przy użyciu FairPlay.

## <a name="envelope-encryption"></a>Szyfrowanie koperty
Użyj tej opcji, jeśli chcesz tooprotect zawartości z AES-128, klucz niezaszyfrowany. Jeśli chcesz bardziej bezpieczna, wybierz jedną z hello DRMs wymienione w tym temacie. 

## <a name="licenses-and-keys-delivery-service"></a>Usługi dostarczania licencji i kluczy
Usługa Media Services udostępnia usługę dostarczania licencji DRM (PlayReady, Widevine, FairPlay) i AES wyczyść klucze tooauthorized klientów. Można użyć [hello portalu Azure](media-services-portal-protect-content.md), interfejsu API REST lub zestawu SDK usługi Media Services dla platformy .NET zasad autoryzacji i uwierzytelnianie tooconfigure licencji i kluczy.

## <a name="token-restriction"></a>Ograniczenia tokenu
Witaj zasady autoryzacji klucza zawartości może mieć jeden lub więcej ograniczeń: otwarte lub ograniczenie tokenu. Witaj zasadzie ograniczenia tokenu musi towarzyszyć token wystawiony przez Secure Token Service (STS). Usługa Media Services obsługuje tokenów w i hello proste tokenów sieci Web (SWT) format tokenu Web JSON (JWT). Usługi Media Services nie zapewnia bezpieczny tokenu usługi. Można utworzyć niestandardowy STS lub korzystać z usługi Microsoft Azure ACS tooissue tokenów. Witaj STS musi być skonfigurowany toocreate podpisany token hello określony klucz i wystawianie oświadczeń, określonych w konfiguracji ograniczenia tokenu hello. Hello Media Services, który zwróci usługi dostarczania klucza żądanej powitania klienta toohello (licencji lub klucza) Jeśli hello token jest prawidłowy i hello oświadczenia w hello token dopasowania tych skonfigurowane dla hello (licencji lub klucza).

Podczas konfigurowania hello zasadzie ograniczenia tokenu, należy określić klucz podstawowy weryfikacji hello, wystawcy i parametry odbiorców. klucz podstawowy weryfikacji Hello zawiera hello klucza, że hello token została podpisana z, wystawcy hello bezpiecznego tokenu usługi, która wystawia hello token. odbiorców Hello (nazywane również zakres) opisano hello celem hello token lub hello zasobów hello tokenu zezwala na dostęp do. Hello usługa Media Services klucza dostawy weryfikuje, czy te wartości w tokenie hello są takie same wartości hello hello szablonu.

## <a name="streaming-urls"></a>Adresy URL przesyłania strumieniowego
Jeśli zawartości została zaszyfrowana z więcej niż jeden DRM, należy użyć tag szyfrowania w hello URL przesyłania strumieniowego: (format = "m3u8-aapl, szyfrowanie = 'xxx').

Zastosuj Hello następujące zagadnienia:

* Można określić tylko zero lub jeden typ szyfrowania.
* Typ szyfrowania nie ma toobe określona w adresie url hello, jeśli tylko jeden szyfrowania został zastosowany toohello zasobów.
* Typ szyfrowania jest uwzględniana wielkość liter.
* można określić Hello następujące typy szyfrowania:  
  * **cenc**: szyfrowania Common encryption (Playready lub Widevine)
  * **cbcs-aapl**: Fairplay
  * **CBC**: szyfrowanie AES envelope.

## <a name="common-scenarios"></a>Typowe scenariusze
Witaj poniższe tematy pokazują, jak tooprotect zawartości w magazynie, dostarczanie dynamicznie szyfrowany przesyłania strumieniowego multimediów, użyj usługi dostarczania klucz/licencjonowania AMS

* [Chroń za pomocą AES](media-services-protect-with-aes128.md) 
* [Chroń za pomocą PlayReady i Widevine](media-services-protect-with-drm.md)
* [Strumienia z HLS chronione zawartości z FairPlay firmy Apple i/lub PlayReady](media-services-protect-hls-with-fairplay.md)

### <a name="additional-scenarios"></a>Dodatkowe scenariusze
* [Jak usługa toointegrate licencji PlayReady Azure z własnych serwer przesyłania strumieniowego/modułu szyfrującego](http://mingfeiy.com/integrate-azure-playready-license-service-encryptorstreaming-server).
* [Przy użyciu castLabs toodeliver DRM licencji tooAzure Media Services](media-services-castlabs-integration.md)

>[!NOTE]
>Scenariusz, w której jest używany DRM server(technology) zewnętrzne i strumień AMS nie jest obecnie obsługiwane.


## <a name="media-services-learning-paths"></a>Ścieżki szkoleniowe dotyczące usługi Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Przekazywanie opinii
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a>Linki pokrewne
[Anonsowanie PlayReady jako usługę i dynamicznego szyfrowania AES w usłudze Azure Media Services](http://mingfeiy.com/playready)

[Wyjaśniono cennik dostarczania licencji PlayReady usługi multimediów Azure](http://mingfeiy.com/playready-pricing-explained-in-azure-media-services)

[Jak toodebug dla AES szyfrowane strumienia w usłudze Azure Media Services](http://mingfeiy.com/debug-aes-encrypted-stream-azure-media-services)

[Authenitcation tokenu JWT](http://www.gtrifonov.com/2015/01/03/jwt-token-authentication-in-azure-media-services-and-dynamic-encryption/)

[Integracja aplikacji na podstawie Azure Media Services OWIN MVC z usługi Azure Active Directory i ograniczenie klucza dostarczania zawartości na podstawie oświadczeń JWT](http://www.gtrifonov.com/2015/01/24/mvc-owin-azure-media-services-ad-integration/).

[Używaj tokenów tooissue Azure ACS](http://mingfeiy.com/acs-with-key-services).

[content-protection]: ./media/media-services-content-protection-overview/media-services-content-protection.png
