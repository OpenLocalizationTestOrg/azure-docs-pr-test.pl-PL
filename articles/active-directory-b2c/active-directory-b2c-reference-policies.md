---
title: "Usługi Azure Active Directory B2C: Wbudowane zasady | Dokumentacja firmy Microsoft"
description: "Temat na powitania rozszerzona platforma zasad usługi Azure Active Directory B2C i jak toocreate różne typy zasad"
services: active-directory-b2c
documentationcenter: 
author: sama
manager: mbaldwin
editor: PatAltimore
ms.assetid: 0d453e72-7f70-4aa2-953d-938d2814d5a9
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/26/2017
ms.author: sama
ms.openlocfilehash: 24bb85eba30f888c6ea7d0401e05235e8eb6ea79
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-built-in-policies"></a>Usługi Azure Active Directory B2C: Wbudowane zasady


Witaj rozszerzona platforma zasad usługi Azure Active Directory (Azure AD) B2C jest siły core hello hello usługi. Zasady pełni opisano funkcje tożsamości konsumentów takich jak konta, logowania lub edytowanie profilu. Na przykład zasad rejestracji umożliwia zachowania toocontrol konfigurując hello następujące ustawienia:

* Typy (kont społecznościowych takimi jak Facebook) lub kont lokalnych, takie jak adresy e-mail użytkowników za pomocą toosign dla aplikacji hello konta
* Atrybuty (na przykład imię, kod pocztowy i rozmiarze buta) toobe zebrane z klienta na powitania podczas tworzenia konta
* Korzystanie z usługi Azure Multi-Factor Authentication
* Witaj wygląd i działanie wszystkie strony
* Informacje (który manifesty jako oświadczenia w tokenie) hello aplikacji otrzymuje po zakończeniu uruchom zasad hello

Można utworzyć wiele zasad o różnych typach w dzierżawie i używać ich w aplikacji, zgodnie z potrzebami. Zasady mogą być ponownie używane w aplikacjach. Tego rodzaju elastyczności umożliwia deweloperom toodefine i zmodyfikuj środowiska tożsamości użytkownika z minimalnym lub żaden kod tootheir zmiany.

Zasady są dostępne do użycia przy użyciu interfejsu dewelopera proste. Wyzwala zasady przy użyciu standardowego żądania uwierzytelniania HTTP (przekazywanie parametru zasad w żądaniu hello) i otrzymuje token dostosowane odpowiedzi aplikacji. Na przykład hello jedyną różnicą między żądań, które wywołują zasad logowania i żądań, które wywołują zasad rejestracji jest hello nazwę zasady, który jest używany w parametru ciągu zapytania "p" hello:

```

https://login.microsoftonline.com/contosob2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=2d4d11a2-f814-46a7-890a-274a72a7309e      // Your registered Application ID
&redirect_uri=https%3A%2F%2Flocalhost%3A44321%2F    // Your registered Reply URL, url encoded
&response_mode=form_post                            // 'query', 'form_post' or 'fragment'
&response_type=id_token
&scope=openid
&nonce=dummy
&state=12345                                        // Any value provided by your application
&p=b2c_1_siup                                       // Your sign-up policy

```

```

https://login.microsoftonline.com/contosob2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=2d4d11a2-f814-46a7-890a-274a72a7309e      // Your registered Application ID
&redirect_uri=https%3A%2F%2Flocalhost%3A44321%2F    // Your registered Reply URL, url encoded
&response_mode=form_post                            // 'query', 'form_post' or 'fragment'
&response_type=id_token
&scope=openid
&nonce=dummy
&state=12345                                        // Any value provided by your application
&p=b2c_1_siin                                       // Your sign-in policy

```

Aby uzyskać więcej informacji na temat hello platformy zasad, zobacz [ten wpis w blogu dotyczące usługi Azure AD B2C na powitania pakietu Enterprise Mobility and Security Blog](http://blogs.technet.com/b/ad/archive/2015/11/02/a-look-inside-azuread-b2c-with-kim-cameron.aspx).

## <a name="create-a-sign-up-or-sign-in-policy"></a>Tworzenie zasad rejestracji i logowania

Ta zasada obsługuje zarówno konsumenta rejestracji i logowania, korzystając z pojedynczą konfiguracją. Konsumenci są przeprowadzony hello prawidłową ścieżkę (rejestracji lub logowania) w zależności od kontekstu hello w dół. Omówiono także zawartość hello tokenów otrzymujących aplikacji hello po pomyślnym napędza rejestracje lub logowania.  Przykład kodu dla zasad rejestracji i logowania hello jest [dostępne tutaj](active-directory-b2c-devquickstarts-web-dotnet-susi.md).  Jest zalecane w przypadku użycia tej zasady protokołu zasad rejestracji i logowania zasad.  

[!INCLUDE [active-directory-b2c-create-sign-in-sign-up-policy](../../includes/active-directory-b2c-create-sign-in-sign-up-policy.md)]

## <a name="create-a-sign-up-policy"></a>Tworzenie zasad rejestracji

[!INCLUDE [active-directory-b2c-create-sign-up-policy](../../includes/active-directory-b2c-create-sign-up-policy.md)]

## <a name="create-a-sign-in-policy"></a>Tworzenie zasad logowania

[!INCLUDE [active-directory-b2c-create-sign-in-policy](../../includes/active-directory-b2c-create-sign-in-policy.md)]

## <a name="create-a-profile-editing-policy"></a>Utwórz profil edytowanie zasad

[!INCLUDE [active-directory-b2c-create-profile-editing-policy](../../includes/active-directory-b2c-create-profile-editing-policy.md)]

## <a name="create-a-password-reset-policy"></a>Utwórz zasady resetowania hasła

[!INCLUDE [active-directory-b2c-create-password-reset-policy](../../includes/active-directory-b2c-create-password-reset-policy.md)]

## <a name="frequently-asked-questions"></a>Często zadawane pytania

### <a name="how-do-i-link-a-sign-up-or-sign-in-policy-with-a-password-reset-policy"></a>Jak połączyć zasady rejestracji lub logowania za pomocą zasad resetowania hasła
Podczas tworzenia zasady rejestracji i logowania (za pomocą kont lokalnych), zobacz **nie pamiętam hasła?** łącza na pierwszej stronie powitania hello środowisko. Kliknięcie tego łącza nie automatycznie wyzwalacza hasła zasady resetowania. 

Witaj, kod błędu:  **`AADB2C90118`**  jest zwracany tooyour aplikacji. Twoja aplikacja powinna toohandle tego kodu błędu za pomocą zasad resetowania określonego hasła. Aby uzyskać więcej informacji, zobacz [program hello podejście łączenie zasad](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-DotNet-SUSI).

### <a name="should-i-use-a-sign-up-or-sign-in-policy-or-a-sign-up-policy-and-a-sign-in-policy"></a>Należy użyć zasad rejestracji i logowania lub zasad rejestracji i logowania zasady?
Zalecane jest użycie zasad rejestracji lub logowania za pośrednictwem zasad rejestracji i logowania zasad.  

zasady rejestracji i logowania Hello ma więcej możliwości niż hello zasad logowania. Ponadto umożliwia dostosowywanie interfejsu użytkownika strony toouse i ma lepszą obsługę lokalizacji. 

zasad logowania Hello zaleca się, jeśli nie potrzebujesz toolocalize zasad, tylko potrzebna jest funkcja personalizacji znakowania i mają hasło resetowania wbudowanych.

## <a name="next-steps"></a>Następne kroki
* [Token sesji i konfiguracji rejestracji jednokrotnej](active-directory-b2c-token-session-sso.md)
* [Wyłączyć weryfikację wiadomości e-mail podczas tworzenia konta użytkownika](active-directory-b2c-reference-disable-ev.md)

