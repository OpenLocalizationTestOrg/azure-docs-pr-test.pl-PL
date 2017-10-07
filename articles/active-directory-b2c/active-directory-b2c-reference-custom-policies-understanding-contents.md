---
title: "Usługa Azure Active Directory B2C: Opis zasad niestandardowych hello początkowego pakietu | Dokumentacja firmy Microsoft"
description: "Temat dotyczący zasad niestandardowych usługi Azure Active Directory B2C"
services: active-directory-b2c
documentationcenter: 
author: rojasja
manager: krassk
editor: rojasja
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 04/25/2017
ms.author: joroja
ms.openlocfilehash: 3484e8cc6fa6a9d57c2aa14c0cc9616065892d10
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-hello-custom-policies-of-hello-azure-ad-b2c-custom-policy-starter-pack"></a>Opis zasad niestandardowych hello hello Azure AD B2C zasady niestandardowe początkowego pakietu

Ta sekcja zawiera listę wszystkich elementów podstawowych hello hello B2C_1A_base zasady, które pochodzą z hello **pakiet początkowy** i która jest wykorzystywana do tworzenia własnych zasad za pomocą hello dziedziczenie hello *B2C_1A_base_ rozszerzenia zasad*.

Tak on więcej szczególnie skupia się na powitania już zdefiniowane oświadczeń, typów, przekształcenia oświadczeń, definicje zawartości, dostawców oświadczeń z ich profile technicznych i hello podróże użytkownika core.

> [!IMPORTANT]
> Microsoft nie udziela żadnych gwarancji, wyrażonych lub domniemanych, względem toohello informacje podane poniżej. Zmiany mogą być wprowadzane w dowolnym momencie przed upływem terminu GA w czasie GA lub po.

Zarówno własnych zasad i hello B2C_1A_base_extensions zasad można zastąpić te definicje i rozszerzyć te zasady nadrzędnego zgodnie z potrzebami, podając te dodatkowe.

Witaj podstawowe elementy hello *zasad B2C_1A_base* są typy oświadczeń, przekształcenia oświadczeń i definicje zawartości. Te elementy można toobe wrażliwych, do którego odwołuje się własnych zasad, a także jak hello *zasad B2C_1A_base_extensions*.

## <a name="claims-schemas"></a>Schematy oświadczeń

Oświadczenia to schematów jest podzielone na trzy części:

1.  Pierwsza sekcja Lista oświadczeń minimalna hello, które są wymagane dla toowork podróże użytkownika hello poprawnie.
2.  Druga sekcja list hello oświadczenia wymagane dla parametrów ciągu zapytania, a inne toobe specjalne parametry przekazane tooother dostawców oświadczeń, szczególnie login.microsoftonline.com do uwierzytelniania. **Nie Modyfikuj tych oświadczeń**.
3.  I po pewnym czasie trzeci sekcja, która wyświetla wszelkie dodatkowe, opcjonalne oświadczenia, które mogą być zbierane od użytkownika hello przechowywanych w katalogu hello i wysłane w tokenach podczas logowania. W tej sekcji można dodawać nowych oświadczeń toobe typu zbierane od użytkownika hello i/lub wysyłane w tokenie hello.

> [!IMPORTANT]
> Schemat oświadczeń Hello zawiera ograniczenia dotyczące określonych oświadczeń, takich jak nazwy użytkowników i hasła. Hello zasady zaufania Framework (TF) traktuje usługi Azure AD jako innego dostawcy oświadczeń i wszystkie jego ograniczenia są modelowany w hello premium zasad. Zasady można być zmodyfikowane tooadd więcej ograniczeń, lub użyj innego dostawcy oświadczeń do magazynu poświadczeń, który ma własną ograniczenia.

Poniżej przedstawiono typy oświadczeń dostępne Hello.

### <a name="claims-that-are-required-for-hello-user-journeys"></a>Oświadczenia, które są wymagane dla hello podróże użytkownika

powitania po oświadczenia są wymagane dla użytkownika podróże toowork prawidłowo:

| Typ oświadczenia | Opis |
|-------------|-------------|
| *Nazwa użytkownika* | Nazwa użytkownika |
| *signInName* | Zaloguj się w nazwie |
| *dla identyfikatora dzierżawcy* | Identyfikator dzierżawy (ID) hello obiektu użytkownika w usłudze Azure AD B2C w warstwie Premium |
| *Identyfikator obiektu* | Identyfikator obiektu (ID) hello obiektu użytkownika w usłudze Azure AD B2C w warstwie Premium |
| *hasło* | Hasło |
| *NoweHasło* | |
| *reenterPassword* | |
| *passwordPolicies* | Zasady haseł używanych przez siły hasła toodetermine Premium usługi Azure AD B2C, wygaśnięcia itp. |
| *Sub* | |
| *alternativeSecurityId* | |
| *identityProvider* | |
| *Nazwa wyświetlana* | |
| *strongAuthenticationPhoneNumber* | Numer telefonu użytkownika |
| *Verified.strongAuthenticationPhoneNumber* | |
| *Adres e-mail* | Adres e-mail, które mogą być używane toocontact hello użytkownika |
| *signInNamesInfo.emailAddress* | Adres e-mail, który hello użytkownika można użyć toosign w |
| *otherMails* | Adresy e-mail, które mogą być używane toocontact hello użytkownika |
| *userPrincipalName* | Nazwa użytkownika zapisaną w hello Premium usługi Azure AD B2C |
| *upnUserName* | Nazwa użytkownika do tworzenia głównej nazwy użytkownika |
| *mailNickName* | Nazwa użytkownika poczty nick zapisanymi hello Premium usługi Azure AD B2C |
| *newUser* | |
| *Wykonano SelfAsserted — dane wejściowe* | Oświadczenie, które określa, czy atrybuty zostały pobrane z hello użytkownika |
| *Wykonano PhoneFactor — dane wejściowe* | Oświadczenie, które określa, czy nowy numer telefonu został zebrany hello użytkownika |
| *authenticationSource* | Określa, czy uwierzytelnienia użytkownika hello społecznościowych dostawcy tożsamości, login.microsoftonline.com lub konto lokalne |

### <a name="claims-required-for-query-string-parameters-and-other-special-parameters"></a>Oświadczenia wymagane w celu parametrów ciągu zapytania i inne parametry specjalne

Witaj następujące oświadczenia są wymagane toopass na dostawców oświadczeń tooother specjalne parametry (w tym niektórych parametrów ciągu zapytania):

| Typ oświadczenia | Opis |
|-------------|-------------|
| *nux* | Specjalne parametr przekazany do konta lokalnego uwierzytelniania toologin.microsoftonline.com |
| *Asystent łączności sieciowej* | Specjalne parametr przekazany do konta lokalnego uwierzytelniania toologin.microsoftonline.com |
| *wiersz* | Specjalne parametr przekazany do konta lokalnego uwierzytelniania toologin.microsoftonline.com |
| *mkt* | Specjalne parametr przekazany do konta lokalnego uwierzytelniania toologin.microsoftonline.com |
| *LC* | Specjalne parametr przekazany do konta lokalnego uwierzytelniania toologin.microsoftonline.com |
| *Typ grant_type* | Specjalne parametr przekazany do konta lokalnego uwierzytelniania toologin.microsoftonline.com |
| *zakres* | Specjalne parametr przekazany do konta lokalnego uwierzytelniania toologin.microsoftonline.com |
| *client_id* | Specjalne parametr przekazany do konta lokalnego uwierzytelniania toologin.microsoftonline.com |
| *objectIdFromSession* | Parametr systemu hello domyślne sesji zarządzania dostawcy tooindicate który hello identyfikator obiektu ma zostały pobrane z sesji rejestracji Jednokrotnej |
| *isActiveMFASession* | Parametr dostarczanej przez hello MFA sesji zarządzania tooindicate, które użytkownik hello ma aktywnej sesji usługi MFA |

### <a name="additional-optional-claims-that-can-be-collected"></a>Dodatkowe oświadczenia (opcjonalnie), które mogą być zbierane

następujące Hello oświadczeń są dodatkowe oświadczenia, które mogą być zbierane od użytkowników hello przechowywanych w katalogu hello i wysyłane w tokenie hello. Zgodnie z opisem przed, dodatkowe oświadczenia mogą być dodawane toothis listy.

| Typ oświadczenia | Opis |
|-------------|-------------|
| *Imię* | Imię użytkownika (znanej także jako nazwa pierwszej) |
| *nazwisko* | Nazwisko użytkownika (znanej także jako nazwa rodziny lub nazwisko) |
| *Extension_picture* | Obraz użytkownika z społecznego |

## <a name="claim-transformations"></a>Przekształcenia oświadczeń

przekształcenia oświadczeń dostępnych Hello są wymienione poniżej.

| Przekształcania oświadczeń | Opis |
|----------------------|-------------|
| *CreateOtherMailsFromEmail* | |
| *CreateRandomUPNUserName* | |
| *CreateUserPrincipalName* | |
| *CreateSubjectClaimFromObjectID* | |
| *CreateSubjectClaimFromAlternativeSecurityId* | |
| *CreateAlternativeSecurityId* | |

## <a name="content-definitions"></a>Definicje zawartości

W tej sekcji opisano hello definicje zawartości już zadeklarowany w hello *B2C_1A_base* zasad. Te definicje zawartości są podatne toobe odwołania, przesłonięcia i/lub rozszerzony zgodnie z potrzebami w własnych zasad, a także jak hello *B2C_1A_base_extensions* zasad.

| Dostawcy oświadczeń | Opis |
|-----------------|-------------|
| *Facebook* | |
| *Logowanie konta lokalnego* | |
| *PhoneFactor* | |
| *Azure Active Directory* | |
| *Samodzielnie potwierdzony* | |
| *Konto lokalne* | |
| *Zarządzanie sesjami* | |
| *Aparat zasad Trustframework* | |
| *TechnicalProfiles* | |
| *Wystawca tokenu* | |

## <a name="technical-profiles"></a>Profile techniczne

W tej sekcji przedstawiono hello profile techniczne już zadeklarowana dla dostawcy oświadczeń w hello *B2C_1A_base* zasad. Te profile techniczne są wrażliwych toobe dalsze odwołuje się do, przesłonięcia i/lub rozszerzony zgodnie z potrzebami w własnych zasad, a także jak hello *B2C_1A_base_extensions* zasad.

### <a name="technical-profiles-for-facebook"></a>Profile techniczne dla usługi Facebook

| Profil techniczne | Opis |
|-------------------|-------------|
| *Facebook OAUTH* | |

### <a name="technical-profiles-for-local-account-signin"></a>Profile techniczne dla lokalnego konta logowanie

| Profil techniczne | Opis |
|-------------------|-------------|
| *Logowania nieinterakcyjnego* | |

### <a name="technical-profiles-for-phone-factor"></a>Profile techniczne dla aplikacji Phone Factor

| Profil techniczne | Opis |
|-------------------|-------------|
| *Dane wejściowe PhoneFactor* | |
| *PhoneFactor InputOrVerify* | |
| *Sprawdź PhoneFactor* | |

### <a name="technical-profiles-for-azure-active-directory"></a>Profile techniczne dotyczące usługi Azure Active Directory

| Profil techniczne | Opis |
|-------------------|-------------|
| *Typowe usługi AAD* | Profil techniczne uwzględnionych hello innych profilów techniczne AAD xxx |
| *UserWriteUsingAlternativeSecurityId usługi AAD* | Profil techniczne dla logowania społecznościowych |
| *UserReadUsingAlternativeSecurityId usługi AAD* | Profil techniczne dla logowania społecznościowych |
| *AAD-UserReadUsingAlternativeSecurityId-brak błędu* | Profil techniczne dla logowania społecznościowych |
| *UserWritePasswordUsingLogonEmail usługi AAD* | Profil techniczne dla kont lokalnych |
| *UserReadUsingEmailAddress usługi AAD* | Profil techniczne dla kont lokalnych |
| *UserWriteProfileUsingObjectId usługi AAD* | Profil techniczne aktualizowania rekordu użytkownika przy użyciu objectId |
| *UserWritePhoneNumberUsingObjectId usługi AAD* | Profil techniczne aktualizowania rekordu użytkownika przy użyciu objectId |
| *UserWritePasswordUsingObjectId usługi AAD* | Profil techniczne aktualizowania rekordu użytkownika przy użyciu objectId |
| *UserReadUsingObjectId usługi AAD* | Techniczne profilu jest używane tooread danych po uwierzytelnia użytkownika |

### <a name="technical-profiles-for-self-asserted"></a>Profile techniczne dla potwierdzone samoobsługowego

| Profil techniczne | Opis |
|-------------------|-------------|
| *Społecznego SelfAsserted* | |
| *SelfAsserted ProfileUpdate* | |

### <a name="technical-profiles-for-local-account"></a>Profile techniczne dla lokalnego konta

| Profil techniczne | Opis |
|-------------------|-------------|
| *LocalAccountSignUpWithLogonEmail* | |

### <a name="technical-profiles-for-session-management"></a>Profile techniczne dla sesji zarządzania

| Profil techniczne | Opis |
|-------------------|-------------|
| *Operacja SM* | |
| *SM AAD* | |
| *SM SocialSignup* | Nazwa profilu jest są używane toodisambiguate AAD sesji między logowania się i zaloguj się |
| *SM SocialLogin* | |
| *UWIERZYTELNIANIE WIELOSKŁADNIKOWE SM* | |

### <a name="technical-profiles-for-trustframework-policy-engine-technicalprofiles"></a>Profile techniczne dla TechnicalProfiles aparatu zasad Trustframework

Obecnie brak techniczne profilów są definiowane dla hello **TechnicalProfiles aparatu zasad Trustframework** dostawcy oświadczeń.

### <a name="technical-profiles-for-token-issuer"></a>Profile techniczne dla wystawcy tokenów

| Profil techniczne | Opis |
|-------------------|-------------|
| *JwtIssuer* | |

## <a name="user-journeys"></a>Podróże użytkownika

W tej sekcji przedstawiono podróże użytkownika hello już zadeklarowany w hello *B2C_1A_base* zasad. Te podróże użytkownika są wrażliwych toobe dalsze odwołuje się do, przesłonięcia i/lub rozszerzony zgodnie z potrzebami w własnych zasad, a także jak hello *B2C_1A_base_extensions* zasad.

| Przebieg użytkownika | Opis |
|--------------|-------------|
| *Rejestracja* | |
| *Logowanie* | |
| *SignUpOrSignIn* | |
| *EditProfile* | |
| *PasswordReset* | |
