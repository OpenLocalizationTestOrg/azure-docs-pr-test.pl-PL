---
title: "Usługa Azure Active Directory B2C: Tokenu sesji i konfiguracji rejestracji jednokrotnej | Dokumentacja firmy Microsoft"
description: "Token, sesji i Konfiguracja pojedynczego logowania jednokrotnego w usłudze Azure Active Directory B2C"
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: e78e6344-0089-49bf-8c7b-5f634326f58c
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/26/2017
ms.author: swkrish
ms.openlocfilehash: 63325ed97a7363723c97ee3a992046ebb5592662
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-token-session-and-single-sign-on-configuration"></a>Usługa Azure Active Directory B2C: Tokenu sesji i konfiguracji rejestracji jednokrotnej
Ta funkcja umożliwia szczegółową kontrolę na [podstawy-policy](active-directory-b2c-reference-policies.md), z:

1. Okres istnienia tokenów zabezpieczających emitowane przez usługi Azure Active Directory (Azure AD) B2C.
2. Okresy istnienia sesji aplikacji sieci web, zarządzane przez usługę Azure AD B2C.
3. Formaty ważne oświadczenia w tokenach zabezpieczających hello emitowane przez usługę Azure AD B2C.
4. Logowanie jednokrotne (SSO) zachowanie na różnych aplikacji i zasad w dzierżawcy usługi B2C.

Funkcja ta w dzierżawie usługi B2C w następujący sposób:

1. Wykonaj następujące kroki zbyt[przejdź do bloku funkcji toohello B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) na powitania portalu Azure.
2. Kliknij przycisk **zasad logowania**. *Uwaga: Możesz użyć tej funkcji na każdego typu zasad, nie tylko w **zasad logowania***.
3. Otwórz zasadę, klikając go. Na przykład kliknięcie **B2C_1_SiIn**.
4. Kliknij przycisk **Edytuj** u góry bloku hello hello.
5. Kliknij przycisk **Token, sesji i konfiguracji rejestracji jednokrotnej**.
6. Wprowadź żądane zmiany. Więcej informacji na temat dostępnych właściwości w kolejnych sekcjach.
7. Kliknij przycisk **OK**.
8. Kliknij przycisk **zapisać** u góry hello hello bloku.

## <a name="token-lifetimes-configuration"></a>Konfiguracja okresy istnienia tokenu
Usługa Azure AD B2C obsługuje hello [protokół OAuth 2.0](active-directory-b2c-reference-protocols.md) umożliwiający bezpieczny dostęp do zasobów tooprotected. tooimplement ta obsługa usługi Azure AD B2C emituje różnych [tokeny zabezpieczające](active-directory-b2c-reference-tokens.md). Są to toomanage okresy istnienia tokenów zabezpieczających emitowane przez usługę Azure AD B2C można użyć właściwości hello:

* **Dostęp do & Identyfikator tokenu okresy istnienia (w minutach)**: hello okres istnienia tooa dostępu toogain używane tokenu elementu nośnego hello OAuth 2.0 chronionych zasobów. Usługa Azure AD B2C wystawia tylko tokeny Identyfikatora, w tym momencie. Ta wartość powinna zostać zastosowana tokenów tooaccess także, gdy dodamy wsparcia dla nich.
  * Domyślne = 60 minut.
  * Minimalna (włącznie) = 5 minut.
  * Maksymalna (włącznie) = 1440 minut.
* **Okres istnienia tokenu odświeżania (dni)**: hello okres maksymalny czas, przed którym token odświeżania mogą być używane tooacquire nowe dostępu lub identyfikator tokenu (i opcjonalnie nowy token odświeżania, jeśli przyznano aplikacji hello `offline_access` zakresu).
  * Domyślne = 14 dni.
  * Minimalna (włącznie) = 1 dzień.
  * Maksymalna (włącznie) = 90 dni.
* **Odśwież okres istnienia tokenu przesuwanego okna (w dniach)**: po tego użytkownika w czasie upłynięciu tego okresu hello jest wymuszone toore — uwierzytelniania, niezależnie od okresu ważności hello hello uzyskaną przez aplikacji hello najnowszych token odświeżania. Może być udostępniony tylko, jeśli przełącznik hello jest ustawiony za**Bounded**. Wymaga toobe większe lub równe toohello **okres istnienia tokenu odświeżania (dni)** wartość. Jeśli przełącznik hello jest ustawiony za**Unbounded**, nie można podać określoną wartość.
  * Domyślna = 90 dni.
  * Minimalna (włącznie) = 1 dzień.
  * Maksymalna (włącznie) = 365 dni.

Oto kilka przypadków użycia, które można włączyć za pomocą tych właściwości:

* Zezwalaj toostay użytkownika rejestracji w aplikacji mobilnej, jak długo użytkownik jest ciągle aktywne w aplikacji hello. Można to zrobić przez ustawienie hello **odświeżania przesuwanego okna okres istnienia tokenu (dni)** przełącznika zbyt**Unbounded** w zasadach rejestracji.
* Spełnia wymagania dotyczące zabezpieczeń i zgodności z branży ustawiając tokenu okresy istnienia hello odpowiedni dostęp.

    > [!NOTE]
    > Te ustawienia nie są dostępne dla zasady resetowania hasła.
    > 
    > 

## <a name="token-compatibility-settings"></a>Ustawienia zgodności tokenu
Wprowadziliśmy formatowania zmiany tooimportant oświadczenia w tokenach zabezpieczających emitowane przez usługę Azure AD B2C. To gotowe tooimprove technicznej standardowy protokół i lepsze współdziałanie z bibliotek tożsamości innych firm. Jednak tooavoid podziału istniejące aplikacje utworzyliśmy hello następujące właściwości tooallow klientów tooopt w razie potrzeby:

* **Oświadczenia wystawcy (iss)**: identyfikuje dzierżawy hello Azure AD B2C, która wystawiła hello token.
  * `https://login.microsoftonline.com/{B2C tenant GUID}/v2.0/`: To jest wartość domyślna hello.
  * `https://login.microsoftonline.com/tfp/{B2C tenant GUID}/{Policy ID}/v2.0/`: Ta wartość zawiera identyfikatory dla dzierżawy hello B2C i zasady hello używane w hello żądania tokenu. Jeśli aplikację lub biblioteka musi toobe usługi Azure AD B2C zgodne z hello [OpenID Connect 1.0 odnajdywania spec](http://openid.net/specs/openid-connect-discovery-1_0.html), użyj tej wartości.
* **Oświadczenia podmiotu (sub)**: identyfikuje jednostki hello, tj. hello użytkownika, dla których hello token deklaracji rozkazujących informacji.
  * **Identyfikator obiektu**: jest to wartość domyślna hello. Wypełnia identyfikator obiektu hello hello użytkownika w katalogu hello na powitania `sub` oświadczenia w tokenie hello.
  * **Nieobsługiwane**: to tylko zapewnia zgodność z poprzednimi wersjami, nie zaleca się przełączyć zbyt**ObjectID** jak tylko można.
* **Oświadczenia reprezentujący identyfikator zasad**: identyfikuje typ oświadczenia hello, do których hello jest wypełniana użyty w żądaniu tokenu hello Identyfikatora zasad.
  * **tfp**: jest to wartość domyślna hello.
  * **acr**: to tylko zapewnia zgodność z poprzednimi wersjami, nie zaleca się przełączyć zbyt`tfp` jak tylko można.

## <a name="session-behavior"></a>Zachowanie sesji
Usługa Azure AD B2C obsługuje hello [protokołu uwierzytelniania OpenID Connect](active-directory-b2c-reference-oidc.md) umożliwiających tooweb bezpiecznego logowania w aplikacji. Są to hello właściwości można użyć sesji aplikacji sieci web toomanage:

* **Aplikacja sieci Web okres istnienia sesji (w minutach)**: hello czas istnienia pliku cookie sesji usługi Azure AD B2C przechowywany w przeglądarce użytkownika powitania po pomyślnym uwierzytelnieniu.
  * Domyślne = 1440 minut.
  * Minimalna (włącznie) = 15 minut.
  * Maksymalna (włącznie) = 1440 minut.
* **Limit czasu sesji aplikacji sieci Web**: Jeśli ta opcja jest ustawiona zbyt**bezwzględną**, użytkownik hello jest wymuszone toore-uwierzytelniania po hello czasie określonym przez **aplikacji sieci Web okres istnienia sesji (w minutach)** upłynie. Jeśli ta opcja jest ustawiona zbyt**stopniowych** (hello ustawienie domyślne), hello użytkownik pozostanie zalogowany, tak długo, jak długo użytkownik hello jest ciągle aktywne w aplikacji sieci web.

Oto kilka przypadków użycia, które można włączyć za pomocą tych właściwości:

* Spełnia wymagania dotyczące zabezpieczeń i zgodności z branży przez ustawienie sesji aplikacji sieci web odpowiednie hello okresy istnienia.
* Wymusić ponowne uwierzytelnianie po ustawionym okresie podczas interakcji z częścią określającą wysokich zabezpieczeń aplikacji sieci web. 

    > [!NOTE]
    > Te ustawienia nie są dostępne dla zasady resetowania hasła.
    > 
    > 

## <a name="single-sign-on-sso-configuration"></a>Konfiguracja rejestracji jednokrotnej (SSO)
Jeśli masz wiele aplikacji i zasad w dzierżawie usługi B2C można zarządzać interakcji użytkowników między nimi przy użyciu hello **konfiguracji rejestracji jednokrotnej** właściwości. Można ustawić hello tooone właściwości z hello następujące ustawienia:

* **Dzierżawy**: to ustawienie domyślne hello. Za pomocą tego ustawienia zezwala na wiele aplikacji i zasad w dzierżawie usługi B2C tooshare hello tej samej sesji użytkownika. Na przykład gdy użytkownik zaloguje się do aplikacji, zakupów firmy Contoso dany użytkownik może również bezproblemowo Zaloguj się do innego jeden, farmacji firmy Contoso, podczas dostępu do niego.
* **Aplikacja**: umożliwia toomaintain sesję użytkownika wyłącznie dla aplikacji, niezależnie od innych aplikacji. Na przykład, jeśli chcesz, aby toosign użytkownika hello w tooContoso farmacji (z hello tych samych poświadczeń), nawet jeśli użytkownik jest już zarejestrowany do zakupów firmy Contoso, inną aplikację na powitania tej samej dzierżawy B2C. 
* **Zasady**: umożliwia toomaintain sesję użytkownika wyłącznie do zasad, niezależnie od aplikacji hello przy jej użyciu. Na przykład jeśli hello użytkownik ma już zalogowany i ukończyć kroku multi Multi-Factor authentication (MFA), użytkownik może uzyskać części toohigher zabezpieczeń dostęp do wielu aplikacji tak długo, jak zasady toohello sesji powiązane hello nie wygasa.
* **Wyłączone**: wymusza hello toorun użytkownika za pośrednictwem hello przebieg całego użytkownika przy każdym wykonaniu hello zasad. Na przykład dzięki temu wielu użytkowników toosign zapasowej tooyour aplikacji (w udostępnionych scenariuszu pulpitu), nawet podczas jednego użytkownika pozostaje zalogowany w czasie całego hello.

    > [!NOTE]
    > Te ustawienia nie są dostępne dla zasady resetowania hasła.
    > 
    > 

