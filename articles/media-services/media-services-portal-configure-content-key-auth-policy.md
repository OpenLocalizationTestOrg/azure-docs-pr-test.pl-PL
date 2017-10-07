---
title: "przy użyciu zasad autoryzacji klucza zawartości aaaConfigure hello portalu Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure zasady autoryzacji klucza zawartości."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: ee82a3fa-c34b-48f2-a108-8ba321f1691e
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako
ms.openlocfilehash: 157fb691b7f71f4889228817e1dc64555e327d48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-content-key-authorization-policy"></a>Skonfiguruj zasady autoryzacji klucza zawartości
[!INCLUDE [media-services-selector-content-key-auth-policy](../../includes/media-services-selector-content-key-auth-policy.md)]

## <a name="overview"></a>Omówienie
Microsoft Azure Media Services umożliwia toodeliver MPEG-DASH, Smooth Streaming i strumieni HTTP-Live-Streaming (HLS) chronionych przy Standard AES (Advanced Encryption) (przy użyciu kluczy szyfrowania 128-bitowego) lub [Microsoft PlayReady DRM](https://www.microsoft.com/playready/overview/). AMS umożliwia również należy toodeliver strumienie DASH korzystających zaszyfrowane za pomocą Widevine DRM. Zarówno PlayReady i Widevine są szyfrowane na powitania specyfikacją Common Encryption (ISO/IEC CENC 23001-7).

Media Services udostępnia również **usługi dostarczania licencji/klucz** z których klienci mogą uzyskać kluczy AES lub tooplay licencji PlayReady/Widevine hello zaszyfrowaną zawartość.

W tym temacie przedstawiono sposób toouse hello zasady autoryzacji klucza zawartości hello tooconfigure portalu Azure. później można użyć klucza Hello toodynamically szyfrowania zawartości. Należy pamiętać, że obecnie można zaszyfrować hello następujących formatów przesyłania strumieniowego: HLS, MPEG DASH i Smooth Streaming. Nie można zaszyfrować pobierania progresywnego.

Gdy odtwarzacza zażąda strumienia, który jest ustawiony toobe dynamicznie zaszyfrowany, Media Services używa hello skonfigurowane klucza toodynamically szyfrowania zawartości przy użyciu szyfrowania AES lub DRM. toodecrypt hello strumienia, hello odtwarzacza zażąda hello klucza z usługi dostarczania klucza hello. toodecide czy hello użytkownik jest autoryzowany tooget hello klucza, usługi hello ocenia zasady autoryzacji hello określonych hello klucza.

Jeśli plan toohave wiele kluczy zawartości lub mają toospecify **usługi dostarczania licencji/klucz** adres URL innych niż hello usługi dostarczania klucza usługi Media Services, użyj .NET SDK usługi Media Services lub interfejsów API REST.

[Skonfiguruj zasady autoryzacji klucza zawartości przy użyciu zestawu .NET SDK usługi multimediów](media-services-dotnet-configure-content-key-auth-policy.md)

[Skonfiguruj zasady autoryzacji klucza zawartości przy użyciu interfejsu API REST usługi multimediów](media-services-rest-configure-content-key-auth-policy.md)

### <a name="some-considerations-apply"></a>Zagadnienia do rozważenia:
* Po utworzeniu konta usługi AMS **domyślne** punktu końcowego przesyłania strumieniowego w brzmieniu konta tooyour hello **zatrzymane** stanu. toostart przesyłania strumieniowego zawartości i podejmij korzyści z dynamicznego tworzenia pakietów i dynamicznego szyfrowania, punkt końcowy przesyłania strumieniowego ma toobe w hello **systemem** stanu. 
* Zawartości musi zawierać zestaw o adaptacyjnej szybkości bitowej MP4s lub pliki Smooth Streaming adaptacyjną szybkością transmisji bitów. Aby uzyskać więcej informacji, zobacz [kodowanie elementu zawartości](media-services-encode-asset.md).
* Hello usługi dostarczania klucza buforuje ContentKeyAuthorizationPolicy i jego obiektów pokrewnych (opcje zasad i ograniczeń) przez 15 minut.  Jeśli tworzenie ContentKeyAuthorizationPolicy i określ toouse ograniczenie 'Token', a następnie ją przetestować, a następnie zaktualizuj zasad hello zbyt "Otwórz" ograniczeń, potrwa około 15 minut przed hello przełączniki toohello "Otwórz" Wersja zasad hello zasad.

## <a name="how-to-configure-hello-key-authorization-policy"></a>Porady: Konfigurowanie zasad autoryzacji klucza hello
zasady autoryzacji klucza hello tooconfigure, wybierz opcję hello **ochrony zawartości** strony.

Usługa Media Services obsługuje wiele sposobów uwierzytelniania użytkowników, którzy tworzą żądania klucza. zasady autoryzacji klucza zawartości Hello może mieć **Otwórz**, **tokenu**, lub **IP** ograniczenia autoryzacji (**IP** można skonfigurować za pomocą REST lub zestawu .NET SDK).

### <a name="open-restriction"></a>Ograniczenie otwarte
Witaj **Otwórz** ograniczeń oznacza hello system będzie dostarczać hello tooanyone klucza, który wysyła żądanie klucza. To ograniczenie może być przydatna do celów testowych.

![OpenPolicy][open_policy]

### <a name="token-restriction"></a>Ograniczenia tokenu
toochoose hello token ograniczone zasad, naciśnij klawisz hello **TOKENU** przycisku.

Witaj **tokenu** zasady ograniczające musi towarzyszyć token wystawiony przez **Secure Token Service** (STS). Usługa Media Services obsługuje tokenów w hello **proste tokenów sieci Web** ([SWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2)) format i **JSON Web Token** formatu (JWT). Aby uzyskać informacje, zobacz [uwierzytelniania tokenu JWT](http://www.gtrifonov.com/2015/01/03/jwt-token-authentication-in-azure-media-services-and-dynamic-encryption/).

Usługa Media Services dostarcza **Secure Token usługi**. Można utworzyć niestandardowy STS lub korzystać z usługi Microsoft Azure ACS tooissue tokenów. Witaj STS musi być skonfigurowany toocreate podpisany token hello określony klucz i wystawianie oświadczeń, określonych w konfiguracji ograniczenia tokenu hello. Witaj usługa Media Services klucza dostawy zwróci klienta toohello klucza szyfrowania hello Jeśli hello token jest prawidłowy i hello oświadczenia w tokenie hello pasują hello klucza zawartości. Aby uzyskać więcej informacji, zobacz [tokenów tooissue ACS Azure użyj](http://mingfeiy.com/acs-with-key-services).

Podczas konfigurowania hello **TOKENU** zasady ograniczające, należy ustawić wartości dla **klucza weryfikacji**, **wystawcy** i **odbiorców**. klucz podstawowy weryfikacji Hello zawiera hello klucza, że hello token została podpisana z, wystawcy hello bezpiecznego tokenu usługi, która wystawia hello token. odbiorców Hello (nazywane również zakres) opisano hello celem hello token lub hello zasobów hello tokenu zezwala na dostęp do. Hello usługa Media Services klucza dostawy weryfikuje, czy te wartości w tokenie hello są takie same wartości hello hello szablonu.

### <a name="playready"></a>PlayReady
Podczas ochrony zawartości przy użyciu **PlayReady**, jednego z elementów hello potrzebnych toospecify w zasadach autoryzacji jest ciąg XML, który definiuje szablon licencji PlayReady hello. Domyślnie jest ustawiona hello następujące zasady:

<PlayReadyLicenseResponseTemplate xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/PlayReadyTemplate/v1"><LicenseTemplates> <PlayReadyLicenseTemplate> <AllowTestDevices>true</AllowTestDevices> <ContentKey i:type="ContentEncryptionKeyFromHeader" /> <LicenseType>Nonpersistent</LicenseType> <PlayRight> <AllowPassingVideoContentToUnknownOutput>dozwolone</AllowPassingVideoContentToUnknownOutput> </PlayRight> </PlayReadyLicenseTemplate> </LicenseTemplates></PlayReadyLicenseResponseTemplate>

Możesz kliknąć hello **zaimportować pliku xml zasady** przycisk i podaj inny kod XML, który odpowiada toohello definicja schematu XML [tutaj](media-services-playready-license-template-overview.md).

## <a name="next-step"></a>Następny krok
Przejrzyj ścieżki szkoleniowe dotyczące usługi Media Services.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Przekazywanie opinii
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

[open_policy]: ./media/media-services-portal-configure-content-key-auth-policy/media-services-protect-content-with-open-restriction.png
[token_policy]: ./media/media-services-key-authorization-policy/media-services-protect-content-with-token-restriction.png

