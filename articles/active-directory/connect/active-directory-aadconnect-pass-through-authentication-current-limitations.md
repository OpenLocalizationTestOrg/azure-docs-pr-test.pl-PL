---
title: "Azure AD Connect: Przekazywanego uwierzytelniania - bieżące ograniczenia | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano bieżące ograniczenia uwierzytelniania przekazywanego usługi Azure Active Directory (Azure AD)"
services: active-directory
keywords: "Azure AD Connect przekazywanego uwierzytelniania, instalacji usługi Active Directory, wymaganych składników dla usługi Azure AD, SSO, Single Sign-on"
documentationcenter: 
author: swkrish
manager: mtillman
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2018
ms.author: billmath
ms.openlocfilehash: aee90f278476a899e0d47fc572c4f375bf926de2
ms.sourcegitcommit: 71fa59e97b01b65f25bcae318d834358fea5224a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/11/2018
---
# <a name="azure-active-directory-pass-through-authentication-current-limitations"></a>Usługi Azure Active Directory przekazywanego uwierzytelniania: Bieżące ograniczenia

>[!IMPORTANT]
>Azure Active Directory (Azure AD) przekazywanego uwierzytelniania jest funkcją wolne, i nie wymagają żadnych wersji płatnej usługi Azure AD z niego korzystać. Przekazywanego uwierzytelniania jest dostępna w wystąpieniu na całym świecie usługi Azure AD, a nie na tylko [chmury Microsoft Azure Niemcy](http://www.microsoft.de/cloud-deutschland) lub [chmury Microsoft Azure dla instytucji rządowych](https://azure.microsoft.com/features/gov/).

## <a name="supported-scenarios"></a>Obsługiwane scenariusze

Pełni są obsługiwane następujące scenariusze:

- Logowania użytkownika do wszystkich aplikacji opartej na przeglądarce sieci web
- Logowania użytkownika do aplikacji pakietu Office, które obsługują [nowoczesnego uwierzytelniania](https://aka.ms/modernauthga): pakiet Office 2016 i Office 2013 _z_ nowoczesnego uwierzytelniania
- Użytkownik logowania do usługi Skype dla firm tego Obsługa nowoczesnego uwierzytelniania, w tym Online i hybrydowych topologii. Dowiedz się więcej na temat obsługiwanych topologii [tutaj](https://technet.microsoft.com/library/mt803262.aspx).
- Dołącza domenowych Azure AD dla urządzeń z systemem Windows 10
- Obsługa programu Exchange ActiveSync

## <a name="unsupported-scenarios"></a>Nieobsługiwane scenariusze

Poniższe scenariusze są _nie_ obsługiwane:

- Logowania użytkownika do starszych aplikacjach klienckich pakietu Office: pakiet Office 2010 i Office 2013 _bez_ nowoczesnego uwierzytelniania. Organizacje zaleca się przełączyć do nowoczesnego uwierzytelniania, jeśli to możliwe. Umożliwia obsługę uwierzytelniania przekazywanego nowoczesnego uwierzytelniania. Pomaga również Zabezpieczanie kont użytkowników przy użyciu [dostępu warunkowego](../active-directory-conditional-access-azure-portal.md) funkcje, takie jak uwierzytelnianie wieloskładnikowe Azure.
- Użytkownik logowania do usługi Skype dla firm aplikacje klienckie _bez_ nowoczesnego uwierzytelniania.
- Użytkownik logowania do programu PowerShell w wersji 1.0. Firma Microsoft zaleca użycie programu PowerShell w wersji 2.0.
- Hasła aplikacji w usłudze Multi-Factor Authentication.
- Wykrywanie użytkownikom [ujawnione poświadczenia](../active-directory-reporting-risk-events.md#leaked-credentials).
- Usługi domenowe Azure AD wymaga synchronizacji skrótu hasła w dzierżawie. W związku z tym dzierżawcami, które korzystają z uwierzytelniania przekazywanego _tylko_ nie działa w przypadku scenariuszy, które wymagają usług domenowych Azure AD.
- Przekazywanego uwierzytelniania nie jest zintegrowany z [Azure AD Connect Health](../connect-health/active-directory-aadconnect-health.md).
- Apple Device Enrollment Program (DEP firmy Apple) nie obsługuje nowoczesnego uwierzytelniania.  Urządzeń DEP firmy Apple nie będzie można zarejestrować w usłudze Intune dla domen przy użyciu uwierzytelniania przekazywanego.

>[!IMPORTANT]
>Jako obejścia nieobsługiwane scenariusze _tylko_, włączanie synchronizacji skrótów haseł na [funkcje opcjonalne](active-directory-aadconnect-get-started-custom.md#optional-features) strony kreatora programu Azure AD Connect.

>[!NOTE]
Włączanie synchronizacji skrótów haseł umożliwia uwierzytelnianie trybu failover, jeśli jest zakłócona infrastruktury lokalnej. Ten tryb failover z uwierzytelniania przekazywanego synchronizacji skrótu hasła usługi Active Directory nie jest automatyczna. Musisz przełączyć metoda logowania ręcznie za pomocą usługi Azure AD Connect. Jeśli serwer z systemem Azure AD Connect ulegnie awarii, potrzebna pomoc od firmy Microsoft Support wyłączyć uwierzytelniania przekazywanego.

## <a name="next-steps"></a>Kolejne kroki
- [Szybki start](active-directory-aadconnect-pass-through-authentication-quick-start.md): szybkim rozpoczynaniu pracy związanej z usługi Azure AD przekazywanego uwierzytelniania.
- [Inteligentne blokady](active-directory-aadconnect-pass-through-authentication-smart-lockout.md): informacje o sposobie konfigurowania funkcji blokady inteligentnej na swojej dzierżawy, aby chronić kont użytkowników.
- [Nowości techniczne](active-directory-aadconnect-pass-through-authentication-how-it-works.md): zrozumieć sposób działania funkcji uwierzytelniania przekazywanego.
- [Często zadawane pytania](active-directory-aadconnect-pass-through-authentication-faq.md): odpowiedzi na często zadawane pytania dotyczące funkcji uwierzytelniania przekazywanego.
- [Rozwiązywanie problemów z](active-directory-aadconnect-troubleshoot-pass-through-authentication.md): Dowiedz się, jak rozwiązać typowe problemy z funkcją uwierzytelniania przekazywanego.
- [Nowości zabezpieczeń](active-directory-aadconnect-pass-through-authentication-security-deep-dive.md): uzyskiwanie informacji głębokość technicznych dotyczących funkcji uwierzytelniania przekazywanego.
- [Azure AD SSO bezproblemowe](active-directory-aadconnect-sso.md): Dowiedz się więcej o tej funkcji uzupełniające.
- [UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect): plik nowego żądania funkcji za pomocą na Forum usługi Azure Active Directory.

