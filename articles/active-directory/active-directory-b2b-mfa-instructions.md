---
title: "aaaConditional dostęp do usługi Azure Active Directory B2B współpracy użytkownikom | Dokumentacja firmy Microsoft"
description: "Azure współpracy B2B usługi Active Directory obsługuje uwierzytelnianie wieloskładnikowe (MFA) dla aplikacji firmowych tooyour selektywny dostęp"
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 05/24/2017
ms.author: sasubram
ms.openlocfilehash: 3a05be4393f74ff8e87f32432a222a5fbac9af62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="conditional-access-for-b2b-collaboration-users"></a>Dostęp warunkowy dla użytkowników współpracy B2B

## <a name="multi-factor-authentication-for-b2b-users"></a>Uwierzytelnianie wieloskładnikowe dla użytkowników B2B
Współpracy B2B usługi Azure AD organizacji można wymusić uwierzytelnianie wieloskładnikowe (MFA) zasad dla użytkowników B2B. Te zasady mogą być wymuszane w hello dzierżawy, aplikacji lub na poziomie indywidualnego użytkownika, hello taki sam sposób, że są włączone dla pełnoetatowych pracowników i członków organizacji hello. Zasady MFA są wymuszane na powitania zasobów organizacji.

Przykład:
1. Użytkownik z aplikacji tooan firmy B zaprasza administratora lub informacje pracownika z firmy, A *Foo* w firmie A.
2. Aplikacja *Foo* w firmie, A jest skonfigurowany toorequire MFA na dostęp.
3. Gdy użytkownik hello firmy B próbuje aplikacji tooaccess *Foo* firmy hello dzierżawcy, są one zadawane toocomplete żądanie uwierzytelniania MFA.
4. Witaj użytkownika można skonfigurować ich MFA z firmy A i wybierze opcję ich MFA.
5. W tym scenariuszu działa w przypadku tożsamości (Azure AD lub zarządzanych kont usług, na przykład, jeśli użytkownicy w firmie B uwierzytelniać za pomocą Identyfikatora społecznościowych)
6. Firmy, A musi mieć wystarczającą liczbę licencji usługi Azure AD Premium, które obsługują usługę MFA. Użytkownik Hello firmy B zużywa tej licencji od firmy A.

dzierżawy zaproszenia Hello jest odpowiedzialny za uwierzytelnianie wieloskładnikowe dla użytkowników w organizacji partnera hello, zawsze, nawet w przypadku organizacji partnerskiej hello funkcję MFA.

### <a name="setting-up-mfa-for-b2b-collaboration-users"></a>Konfigurowanie usługi MFA dla użytkowników współpracy B2B
toodiscover, jak łatwo jest tooset się uwierzytelnianie wieloskładnikowe dla użytkowników współpracy B2B, zobacz temat jak w hello następujących wideo:

>[!VIDEO https://channel9.msdn.com/Blogs/Azure/b2b-conditional-access-setup/Player]

### <a name="b2b-users-mfa-experience-for-offer-redemption"></a>Użytkownicy B2B środowisko MFA oferują realizacji
Wyewidencjonuj powitania po animacji toosee hello realizacji środowisko:

>[!VIDEO https://channel9.msdn.com/Blogs/Azure/MFA-redemption/Player]

### <a name="mfa-reset-for-b2b-collaboration-users"></a>Resetuj dla użytkowników współpracy B2B usługi MFA
Obecnie Witaj, Administratorze może wymagać tooproof użytkowników współpracy B2B się ponownie tylko za pomocą następującego polecenia cmdlet programu PowerShell hello:

1. Połącz tooAzure AD

  ```
  $cred = Get-Credential
  Connect-MsolService -Credential $cred
  ```
2. Pobierz wszyscy użytkownicy dowód metod

  ```
  Get-MsolUser | where { $_.StrongAuthenticationMethods} | select UserPrincipalName, @{n="Methods";e={($_.StrongAuthenticationMethods).MethodType}}
  ```
  Oto przykład:

  ```
  PS C:\Users\tjwasserGet-MsolUser | where { $_.StrongAuthenticationMethods} | select UserPrincipalName, @{n="Methods";e={($_.StrongAuthenticationMethods).MethodType}}
  ```

3. Resetuj hello MFA metoda dla określonego użytkownika toorequire hello B2B współpracy użytkownika tooset up dowód metod ponownie. Przykład:

  ```
  Reset-MsolStrongAuthenticationMethodByUpn -UserPrincipalName gsamoogle_gmail.com#EXT#@ WoodGroveAzureAD.onmicrosoft.com
  ```

### <a name="why-do-we-perform-mfa-at-hello-resource-tenancy"></a>Dlaczego możemy wykonywać uwierzytelnianie wieloskładnikowe na powitania zasobów dzierżawy?

W bieżącej wersji hello MFA jest zawsze w hello zasobów dzierżawy, ze względu na przewidywalności. Na przykład załóżmy, że użytkownik Contoso (Zosi) jest tooFabrikam zaproszonych Fabrikam ma włączone uwierzytelnianie wieloskładnikowe dla użytkowników B2B.

Jeżeli Contoso ma włączone zasady MFA na serwerze App1, ale nie App2, jeśli przyjrzymy się hello Contoso MFA oświadczenia w tokenie hello, firma Microsoft może zobacz hello następującego problemu:

* Dzień 1: Użytkownik ma MFA w firmie Contoso i uzyskuje dostęp do komputera App1, a następnie nie dodatkowe uwierzytelnianie wieloskładnikowe monit jest wyświetlany w firmie Fabrikam.

* Dzień 2: hello użytkownik uzyskiwał dostęp do 2 aplikacji w firmie Contoso, więc podczas uzyskiwania dostępu do firmy Fabrikam, muszą zarejestrować dla usługi MFA istnieje.

Ten proces może być trudne i może prowadzić toodrop w zakończeń logowania.

Ponadto nawet jeśli firma Contoso ma możliwość uwierzytelniania MFA, nie zawsze jest hello hello sprawy firma Fabrikam może zaufanie hello zasad MFA firmy Contoso.

Na koniec zasobów dzierżawy MFA działa również MSA i identyfikatory społecznościowych oraz organizacjami partnera, bez konfigurowania uwierzytelniania Wieloskładnikowego.

W związku z tym hello zalecenia dla usługi MFA dla użytkowników B2B jest tooalways wymagają usługi MFA w hello zapraszanie dzierżawy. Ten wymóg może prowadzić toodouble MFA w niektórych przypadkach, ale zawsze, gdy dostęp do dzierżawy zaproszenia hello, środowisko użytkownika końcowego hello jest atrybutem wartości prognozowanych: Zosi musi zarejestrować w usłudze MFA z dzierżawcą zaproszenia hello.

### <a name="device-based-location-based-and-risk-based-conditional-access-for-b2b-users"></a>Oparta na urządzeniach, na podstawie lokalizacji i ryzyka dostępu warunkowego dla użytkowników B2B

Gdy Contoso włącza zasady dostępu warunkowego opartego na urządzenia do danych firmowych, dostępu nie urządzeń, które nie są zarządzane przez firmę Contoso i nie są zgodne z zasadami urządzenia Contoso hello.

Jeśli urządzenie hello B2B użytkownika nie jest zarządzana przez firmy Contoso, dostęp użytkowników B2B z organizacji partnerskiej hello jest zablokowany w dowolnym kontekście te zasady są wymuszane. Jednak Contoso utworzyć wykluczenie list zawierających tooexclude użytkowników partnera hello je z zasad dostępu warunkowego opartego na urządzeniu.

#### <a name="location-based-conditional-access-for-b2b"></a>Na podstawie lokalizacji dostępu warunkowego dla B2B

Jeśli organizacja zaproszenia hello jest możliwe toocreate zaufany zakres adresów IP, który definiuje organizacji partnera można wymuszać zasady dostępu warunkowego na podstawie lokalizacji dla użytkowników B2B.

#### <a name="risk-based-conditional-access-for-b2b"></a>Dostęp warunkowy dla B2B ryzyka

Obecnie zasady oparte na ryzyko logowania nie może być zastosowane tooB2B użytkowników oceny ryzyka hello jest wykonywana w organizacji macierzystej hello B2B użytkownika.

## <a name="next-steps"></a>Następne kroki

Zobacz nasze inne artykuły dotyczące współpracy B2B w usłudze Azure AD:

* [Czym jest współpraca B2B w usłudze Azure AD?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Jak Administratorzy usługi Azure Active Directory dodać użytkowników współpracy B2B?](active-directory-b2b-admin-add-users.md)
* [Jak pracownicy przetwarzający informacje dodać użytkowników współpracy B2B?](active-directory-b2b-iw-add-users.md)
* [elementy Hello hello wiadomość e-mail z zaproszeniem współpracy B2B](active-directory-b2b-invitation-email.md)
* [Realizacji zaproszenia współpracy B2B](active-directory-b2b-redemption-experience.md)
* [Azure licencjonowania współpracy B2B usługi AD](active-directory-b2b-licensing.md)
* [Rozwiązywanie problemów z współpracy usługi Azure Active Directory B2B](active-directory-b2b-troubleshooting.md)
* [Azure współpracy B2B usługi Active Directory — często zadawane pytania (FAQ)](active-directory-b2b-faq.md)
* [Dostosowywanie i Azure Active Directory B2B współpracy interfejsu API](active-directory-b2b-api.md)
* [Dodawanie użytkowników współpracy B2B bez zaproszenia](active-directory-b2b-add-user-without-invite.md)
* [Indeks artykułów dotyczących zarządzania aplikacjami w usłudze Azure Active Directory](active-directory-apps-index.md)
