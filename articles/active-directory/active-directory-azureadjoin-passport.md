---
title: "aaaAuthenticating tożsamości bez hasła przy użyciu usługi Windows Hello dla firm i Azure AD | Dokumentacja firmy Microsoft"
description: "Zawiera omówienie usługi Windows Hello dla firm i dodatkowe informacje na temat wdrażania usługi Windows Hello dla firm."
services: active-directory
documentationcenter: 
author: femila
manager: femila
editor: 
tags: azure-classic-portal
ms.assetid: f907bb90-8776-46ca-9e12-279949af66ff
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: 7c1c52e10b7ab7a89ec3226ffa7cf01896267871
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="authenticating-identities-without-passwords-through-windows-hello-for-business"></a>Uwierzytelnianie tożsamości bez hasła przy użyciu usługi Windows Hello dla firm
Hello bieżącej metody uwierzytelniania przy użyciu haseł wyłącznie nie są wystarczające tookeep użytkownikom bezpieczne. Użytkownicy ponownego wykorzystania i zapomnisz hasła. Hasła są breachable, phishable, toocracks podatnych na błędy i do odgadnięcia. Również uzyskać tooremember trudne i tooattacks podatnych na błędy, takich jak "[przekazywania skrótu hello](https://technet.microsoft.com/dn785092.aspx)".

## <a name="about-windows-hello-for-business"></a>Temat Windows Hello dla firm
Usługi Windows Hello dla firm jest klucza publicznego i prywatnego lub metody uwierzytelniania opartego na certyfikatach dla organizacji i konsumentów wykracza poza hasła. Ta forma uwierzytelniania opiera się na poświadczenia parę kluczy, które można zastąpić hasła i podchodzą toobreaches, thefts i wyłudzaniem informacji.

 Usługi Windows Hello dla firm umożliwia użytkownikowi uwierzytelniania konta Microsoft tooa, konto usługi Active Directory systemu Windows Server, konto Microsoft Azure Active Directory (Azure AD) lub usługa innej firmy niż Microsoft, która obsługuje uwierzytelnianie Fast tożsamości Online (FIDO). Po weryfikacji dwuetapowej początkowej podczas Windows Hello dla firm rejestracji Windows Hello dla firm jest skonfigurowany na urządzeniu użytkownika hello, a użytkownik hello ustawia gestu, który może być Windows Hello lub numeru PIN. Witaj użytkownik podaje tooverify gestu hello swojej tożsamości. Następnie system Windows używa Windows Hello dla firm tooauthenticate hello użytkownika i pomóc im tooaccess chronionych zasobów i usług.

klucz prywatny Hello staje się dostępny wyłącznie za pośrednictwem "gestu użytkownika" jak numer PIN, biometrycznych lub urządzenie zdalne, takie jak karty inteligentnej, który hello użytkownika używa toosign w urządzeniu toohello. Te informacje są połączone tooa certyfikatu lub parę kluczy asymetrycznych. klucz prywatny Hello jest sprzętu zaświadczenia, jeśli urządzenie hello ma układ modułu Trusted Platform Module (TPM). klucz prywatny Hello nigdy nie przekracza hello urządzenia.

Hello klucz publiczny jest zarejestrowany w usłudze Azure Active Directory i usługi Active Directory systemu Windows Server (w przypadku lokalnego). Dostawcy tożsamości (IDPs) sprawdzanie poprawności użytkownika hello przez mapowanie hello klucza publicznego klucza prywatnego toohello hello użytkownika i podaj informacje logowania za pośrednictwem jednego czasu hasła (OTP), PhoneFactor lub mechanizm powiadamiania inną.

## <a name="why-enterprises-should-adopt-windows-hello-for-business"></a>Dlaczego przedsiębiorstwa powinna przyjąć Windows Hello dla firm
Przez włączenie usługi Windows Hello dla firm, przedsiębiorstw ułatwia ich zasobów jeszcze bardziej bezpieczne przez:

* Konfigurowanie usługi Windows Hello dla firm za pomocą opcji preferowane sprzętu. Oznacza to, że klucze będą generowane w moduł TPM 1.2 lub 2.0 modułu TPM, jeśli jest dostępna. W przypadku niedostępności modułu TPM, oprogramowania wygeneruje hello klucza.
* Definiowanie hello złożoność i długość hello PRZYPNIJ, i czy użycia Hello jest włączone w Twojej organizacji.
* Konfigurowanie usługi Windows Hello dla różnych scenariuszy biznesowych toosupport jak karty inteligentnej za pomocą opartego na certyfikatach zaufania.

## <a name="how-windows-hello-for-business-works"></a>Jak Windows Hello dla firm działa
1. Klucze są generowane na sprzęcie hello przez moduł TPM i oprogramowania. Wiele urządzeń ma wbudowany moduł TPM, która zabezpiecza sprzętu hello przy integracji klucze szyfrowania urządzenia. Moduł TPM 1.2 lub 2.0 generuje klucze i certyfikaty, które są tworzone na podstawie hello wygenerowane klucze.
2. Witaj modułu TPM poświadcza te klucze związanych ze sprzętem.
3. Gest unlock pojedynczego odblokowuje hello urządzenia. Ten gest umożliwia dostęp do zasobów toomultiple czy urządzenie hello jest przyłączony do domeny lub Azure przyłączonych do usługi AD.

## <a name="how-hello-windows-hello-for-business-lifecycle-works"></a>Jak działa hello Windows Hello dla firm cykl życia
![Usługi Windows Hello dla firm cykl życia](./media/active-directory-azureadjoin/active-directory-azureadjoin-microsoft-passport.png)

Witaj wcześniejszym diagramie zilustrowano pary klucza publicznego i prywatnego hello i weryfikacji hello przez dostawcę tożsamości hello. Każda z tych czynności jest szczegółowo opisany w tym miejscu:

1. Użytkownik Hello potwierdzające jego tożsamość przez wiele wbudowanych metod sprawdzania pisowni (gesty, fizycznymi kartami inteligentnymi, usługa Multi-Factor authentication) i wysyła ten tooan informacji o dostawcy tożsamości (IDP) jak usługa Azure Active Directory lub lokalnej usługi Active Directory.
2. urządzenie Hello tworzy klucz hello, poświadcza hello klucza, przyjmuje hello publicznej części klucza, dołącza go z instrukcji stacji, podpisuje i wysyła je toohello IDP tooregister hello klucza.
3. Jak hello IDP rejestruje hello publicznej części klucza hello, wyzwania IDP hello hello toosign urządzenia z hello prywatny klucz hello.
4. następnie weryfikuje Hello IDP i problemy hello token uwierzytelniania, umożliwiający hello użytkownika i hello urządzenia dostęp hello chronionych zasobów. IDPs zapisać wieloplatformowych aplikacji lub używać przeglądarki toocreate pomocy technicznej (za pośrednictwem interfejsów API języka JavaScript/Webcrypto) i użyć funkcji Windows Hello dla firm poświadczenia dla użytkowników.

## <a name="hello-deployment-requirements-for-windows-hello-for-business"></a>wymagania dotyczące wdrażania powitania dla systemu Windows Hello dla firm
### <a name="at-hello-enterprise-level"></a>Na poziomie przedsiębiorstwa hello
* Witaj przedsiębiorstwo ma subskrypcji platformy Azure.

### <a name="at-hello-user-level"></a>Na poziomie użytkownika hello
* Hello na komputerze użytkownika działa system Windows 10 Professional lub Enterprise.

Aby uzyskać szczegółowe instrukcje, zobacz [włączyć Windows Hello dla firm w organizacji hello](active-directory-azureadjoin-passport-deployment.md).

## <a name="additional-information"></a>Dodatkowe informacje
* [System Windows 10 dla przedsiębiorstw hello: sposoby toouse urządzenia do pracy](active-directory-azureadjoin-windows10-devices-overview.md)
* [Rozszerzanie chmury możliwości tooWindows 10 urządzeniami za pomocą usługi Azure Active Directory Join](active-directory-azureadjoin-user-upgrade.md)
* [Dowiedz się więcej na temat scenariuszy użycia funkcji Azure AD Join](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [Łączenie urządzeń przyłączonych do domeny tooAzure AD dla systemu Windows 10](active-directory-azureadjoin-devices-group-policy.md)
* [Konfigurowanie funkcji Azure AD Join](active-directory-azureadjoin-setup.md)

