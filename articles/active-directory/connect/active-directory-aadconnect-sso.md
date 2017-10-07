---
title: 'Azure AD Connect: Bezproblemowe logowanie jednokrotne | Dokumentacja firmy Microsoft'
description: "W tym temacie opisano usługi Azure Active Directory (Azure AD) bezproblemowe logowanie jednokrotne i jak umożliwia możesz tooprovide true logowania jednokrotnego do firmowych pulpitów użytkowników w sieci firmowej."
services: active-directory
keywords: "Co to jest usługa Azure AD Connect, zainstaluj usługę Active Directory, wymaganych składników dla usługi Azure AD, SSO, Single Sign-on"
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: billmath
ms.openlocfilehash: 11c778c37ee39866dcc3a14ab648cfcd8e322e47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-seamless-single-sign-on"></a>Usługa Azure Active Directory bezproblemowe logowanie jednokrotne

## <a name="what-is-azure-active-directory-seamless-single-sign-on"></a>Co to jest Azure Active Directory bezproblemowe logowanie jednokrotne?

Azure Active Directory bezproblemowe logowanie jednokrotne (Azure AD bezproblemowe logowanie Jednokrotne) automatycznie podpisuje użytkowników, gdy są w sieci firmowej tooyour podłączonego urządzenia. Po włączeniu użytkowników nie muszą tootype w toosign ich haseł w tooAzure AD, a następnie zazwyczaj nawet wpisz ich nazwami użytkowników. Ta funkcja zapewnia łatwy dostęp użytkowników aplikacji opartych na chmurze tooyour bez konieczności żadnych składników dodatkowych lokalnych.

Bezproblemowe logowanie Jednokrotne można łączyć z obu hello [synchronizacji skrótu hasła](active-directory-aadconnectsync-implement-password-synchronization.md) lub [uwierzytelniania przekazywanego](active-directory-aadconnect-pass-through-authentication.md) metody logowania.

![Bezproblemowe logowanie jednokrotne](./media/active-directory-aadconnect-sso/sso1.png)

>[!IMPORTANT]
>Bezproblemowe rejestracji Jednokrotnej jest obecnie w przeglądzie. Ta funkcja jest _nie_ dotyczy tooActive Directory Federation Services (AD FS).

## <a name="key-benefits"></a>Najważniejsze korzyści

- *Środowisko użytkowników*
  - Użytkownicy zostaną automatycznie wylogowani do zarówno lokalnie, jak i aplikacje oparte na chmurze.
  - Użytkownicy nie mają tooenter haseł wielokrotnie.
- *Łatwe toodeploy & administrowania*
  - Żadne dodatkowe składniki niezbędne toomake lokalnymi tę pracę.
  - Działa przy użyciu dowolnej metody uwierzytelniania w chmurze — [synchronizacji skrótu hasła](active-directory-aadconnectsync-implement-password-synchronization.md) lub [uwierzytelniania przekazywanego](active-directory-aadconnect-pass-through-authentication.md).
  - Mogą być wprowadzanie toosome lub wszystkich użytkowników za pomocą zasad grupy.
  - Rejestrowanie urządzeń z systemem innym niż Windows 10 z usługą Azure AD bez potrzeby hello dowolnej infrastruktury usług AD FS. Ta funkcja wymaga od Ciebie toouse wersji 2.1 lub nowszej hello [Dołącz do miejsca pracy klienta](https://www.microsoft.com/download/details.aspx?id=53554).

## <a name="feature-highlights"></a>Zawiera opis funkcji

- Nazwa logowania użytkownika może być albo hello lokalnymi domyślna nazwa użytkownika (`userPrincipalName`) lub inny atrybut skonfigurowane w programie Azure AD Connect (`Alternate ID`). Użyć zarówno przypadków pracy, ponieważ bezproblemowe logowanie Jednokrotne używa hello `securityIdentifier` oświadczenie toolook biletu Kerberos hello zapasową hello odpowiedniego obiektu użytkownika w usłudze Azure AD.
- Bezproblemowe rejestracji Jednokrotnej jest funkcją oportunistyczne. Jeśli go nie powiedzie się z jakiegokolwiek powodu, środowisko logowania użytkownika hello Przechodzi wstecz zachowanie regularne tooits - tj, hello użytkownik powinien tooenter hasła na powitania strony logowania.
- Jeśli przekazuje aplikacji `domain_hint` (OpenID Connect) lub `whr` parametr (SAML) - identyfikujący dzierżawy, lub `login_hint` parametru - identyfikacji użytkownika hello w jego usługi Azure AD żądania logowania, użytkownicy zostaną automatycznie wylogowani bez nich wprowadzania nazwy użytkownika i hasła.
- Można ją włączyć za pomocą usługi Azure AD Connect.
- Jest bezpłatna funkcji i nie wymagają żadnych płatnej wersji usługi Azure AD toouse go.
- Jest obsługiwana na klientach przeglądarki sieci web i klientom pakietu Office, które obsługują [nowoczesnego uwierzytelniania](https://aka.ms/modernauthga) na różnych platformach i przeglądarki umożliwia uwierzytelnianie Kerberos:

| OS\Browser |Program Internet Explorer|Krawędzi|Google Chrome|Mozilla Firefox|Safari|
| --- | --- |--- | --- | --- | -- 
|Windows 10|Tak|Nie|Tak|Tak\*|Nie dotyczy
|Windows 8.1|Tak|Nie dotyczy|Tak|Tak\*|Nie dotyczy
|Windows 8|Tak|Nie dotyczy|Tak|Tak\*|Nie dotyczy
|Windows 7|Tak|Nie dotyczy|Tak|Tak\*|Nie dotyczy
|Mac OS X|Nie dotyczy|Nie dotyczy|Tak\*|Tak\*|Tak\*

\*Wymaga [dodatkowej konfiguracji](active-directory-aadconnect-sso-quick-start.md#browser-considerations)

>[!IMPORTANT]
>Firma Microsoft niedawno wycofane obsługę tooinvestigate krawędzi problemy zgłoszone przez klienta.

>[!NOTE]
>W systemie Windows 10 hello zaleca toouse [Azure AD Join](../active-directory-azureadjoin-overview.md) hello optymalne pojedynczego logowania jednokrotnego środowisko z usługą Azure AD.

## <a name="next-steps"></a>Następne kroki

- [**Szybki Start** ](active-directory-aadconnect-sso-quick-start.md) — Uzyskaj i systemem Azure AD bezproblemowe Usługa rejestracji Jednokrotnej.
- [**Nowości techniczne** ](active-directory-aadconnect-sso-how-it-works.md) -zrozumieć sposób działania tej funkcji.
- [**Często zadawane pytania** ](active-directory-aadconnect-sso-faq.md) -odpowiedzi toofrequently zadawane pytania.
- [**Rozwiązywanie problemów z** ](active-directory-aadconnect-troubleshoot-sso.md) — Dowiedz się, jak tooresolve typowe problemy związane z funkcją hello.
- [**UserVoice** ](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) — w przypadku zgłoszenia żądania nowych funkcji.
