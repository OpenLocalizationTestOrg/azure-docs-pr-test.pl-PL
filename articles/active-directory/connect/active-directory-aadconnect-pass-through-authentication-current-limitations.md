---
title: "Azure AD Connect: Przekazywanego uwierzytelniania - bieżące ograniczenia | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano hello bieżących ograniczeń uwierzytelniania przekazywanego usługi Azure Active Directory (Azure AD)."
services: active-directory
keywords: "Azure AD Connect przekazywanego uwierzytelniania, instalacji usługi Active Directory, wymaganych składników dla usługi Azure AD, SSO, Single Sign-on"
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/03/2017
ms.author: billmath
ms.openlocfilehash: 2933745d071aae205c44659e6ea92697f390effb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-pass-through-authentication-current-limitations"></a>Usługi Azure Active Directory przekazywanego uwierzytelniania: Bieżące ograniczenia

>[!IMPORTANT]
>Azure AD przekazywanego uwierzytelniania jest obecnie w przeglądzie. Jest bezpłatna funkcji i nie wymagają żadnych płatnej wersji usługi Azure AD toouse go. Przekazywanego uwierzytelniania jest dostępna tylko w Witaj świecie wystąpienia usługi Azure AD, a nie na [Niemcy Microsoft Cloud](http://www.microsoft.de/cloud-deutschland) i [Microsoft Azure dla instytucji rządowych Cloud](https://azure.microsoft.com/features/gov/).

## <a name="supported-scenarios"></a>Obsługiwane scenariusze

Hello następujące scenariusze są obsługiwane w wersji zapoznawczej:

- Użytkownik logowania do wszystkich aplikacji opartej na przeglądarce sieci web.
- Logowania użytkownika do aplikacji klienta usługi Office 365, które obsługują [nowoczesnego uwierzytelniania](https://aka.ms/modernauthga).
- Azure AD Join dla urządzeń z systemem Windows 10.
- Obsługa programu Exchange ActiveSync.

## <a name="unsupported-scenarios"></a>Nieobsługiwane scenariusze

Hello są następujące scenariusze _nie_ obsługiwane w wersji zapoznawczej:

- Użytkownik logowania do aplikacji klienta starszej wersji pakietu Office (Office 2013 lub starszym). Organizacje są zachęcani tooswitch toomodern uwierzytelniania, jeśli to możliwe. Umożliwia obsługę uwierzytelniania przekazywanego nowoczesnego uwierzytelniania, ale również pomaga zabezpieczyć użytkownika kont przy użyciu narzędzia [dostępu warunkowego](../active-directory-conditional-access.md) funkcje takie jak uwierzytelnianie wieloskładnikowe (MFA).
- Użytkownik logowania do usługi Skype dla firm klienta aplikacji, w tym usługi Skype dla firm 2016.
- Użytkownik logowania do programu PowerShell w wersji 1.0. Zalecane jest, użyj programu PowerShell w wersji 2.0.

>[!IMPORTANT]
>Jako obejście nieobsługiwanych scenariuszy, Włącz synchronizacji skrótu hasła na powitania [funkcje opcjonalne](active-directory-aadconnect-get-started-custom.md#optional-features) w kreatorze Połącz hello Azure AD. Synchronizacja skrótów haseł działa jako rezerwowe dla hello poprzedzających scenariusze _tylko_ (i _nie_ jako ogólnego tooPass do uwierzytelniania rezerwowego). Jeśli nie potrzebujesz tych scenariuszy, wyłącz synchronizacji skrótu hasła.

## <a name="next-steps"></a>Następne kroki
- [**Szybki Start** ](active-directory-aadconnect-pass-through-authentication-quick-start.md) — Uzyskaj i systemem Azure AD przekazywanego uwierzytelniania.
- [**Nowości techniczne** ](active-directory-aadconnect-pass-through-authentication-how-it-works.md) -zrozumieć sposób działania tej funkcji.
- [**Często zadawane pytania** ](active-directory-aadconnect-pass-through-authentication-faq.md) -odpowiedzi toofrequently zadawane pytania.
- [**Rozwiązywanie problemów z** ](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) — Dowiedz się, jak tooresolve typowe problemy związane z funkcją hello.
- [**Azure AD SSO bezproblemowe** ](active-directory-aadconnect-sso.md) — Dowiedz się więcej o tej funkcji uzupełniające.
- [**UserVoice** ](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) — w przypadku zgłoszenia żądania nowych funkcji.
