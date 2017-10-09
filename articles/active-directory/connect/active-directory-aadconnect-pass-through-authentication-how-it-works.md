---
title: "Azure AD Connect: Uwierzytelniania przekazywanego — jak to działa? | Microsoft Docs"
description: "W tym artykule opisano, jak działa uwierzytelniania przekazywanego Azure Active Directory."
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
ms.date: 07/27/2017
ms.author: billmath
ms.openlocfilehash: ffcebee572a9ba2840e81250651dea45599d65d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-pass-through-authentication-technical-deep-dive"></a>Azure przekazywanego uwierzytelnianie usługi Active Directory: Techniczne nowości

>[!IMPORTANT]
>Azure AD przekazywanego uwierzytelniania jest obecnie w przeglądzie. 

## <a name="how-does-azure-active-directory-pass-through-authentication-work"></a>Jak działa uwierzytelniania przekazywanego Azure Active Directory?

Gdy użytkownik próbuje toosign do aplikacji zabezpieczonej przez usługi Azure Active Directory (Azure AD) i włączenie uwierzytelniania przekazywanego dzierżawcy hello hello są wykonywane następujące czynności:

1. Witaj użytkownik spróbuje tooaccess aplikacji (na przykład Witaj aplikacji Outlook Web App - https://outlook.office365.com/owa/).
2. Jeśli użytkownik hello nie jest już zalogowany, użytkownika hello jest strony logowania usługi Azure AD toohello przekierowane.
3. Hello użytkownik wprowadza nazwę użytkownika i hasło do strony logowania usługi Azure AD hello i kliknie przycisk "Zaloguj" hello.
4. Usługi Azure AD na powitania logowania żądania odbierania umieszcza hello nazwy użytkownika i hasła (zaszyfrowane przy użyciu klucza publicznego) w kolejce.
5. Agent uwierzytelniania przekazywanego lokalnymi sprawia, że kolejka toohello wywołań wychodzących i pobiera hello nazwy użytkownika i hasła szyfrowane.
6. Hello agent odszyfrowuje hello hasła przy użyciu jego klucz prywatny.
7. Hello agent sprawdza następnie hello nazwy użytkownika i hasła w usłudze Active Directory przy użyciu standardowych interfejsów API systemu Windows (podobne toowhat mechanizm jest używany przez usługi federacyjne Active Directory). Witaj nazwa użytkownika może być albo hello lokalnymi domyślna nazwa użytkownika (zwykle `userPrincipalName`) lub inny atrybut skonfigurowane w programie Azure AD Connect (nazywane `Alternate ID`).
8. Witaj lokalnego kontrolera domeny Active Directory (DC), a następnie oblicza hello żądania i zwraca hello właściwą odpowiedź (Powodzenie, Niepowodzenie, hasło wygasło lub użytkownika zablokowane) toohello agenta.
9. Hello agent zwraca z kolei tej odpowiedzi tooAzure wstecz AD.
10. Usługi Azure AD ocenia hello odpowiedzi i odpowiada toohello użytkowników zależnie od potrzeb — na przykład jego zalogowaniu użytkownika hello natychmiast albo żądań uwierzytelniania wieloskładnikowego (MFA).
11. Jeśli logowanie użytkownika hello zakończy się pomyślnie, użytkownik hello jest aplikacji hello tooaccess stanie.

Witaj poniższym diagramie przedstawiono wszystkie składniki hello i hello etapy.

![Uwierzytelnianie przekazywane](./media/active-directory-aadconnect-pass-through-authentication/pta2.png)

## <a name="next-steps"></a>Następne kroki
- [**Bieżące ograniczenia** ](active-directory-aadconnect-pass-through-authentication-current-limitations.md) — ta funkcja jest obecnie w przeglądzie. Dowiedz się, jakie scenariusze są obsługiwane i zostały.
- [**Szybki Start** ](active-directory-aadconnect-pass-through-authentication-quick-start.md) — Uzyskaj i systemem Azure AD przekazywanego uwierzytelniania.
- [**Często zadawane pytania** ](active-directory-aadconnect-pass-through-authentication-faq.md) -odpowiedzi toofrequently zadawane pytania.
- [**Rozwiązywanie problemów z** ](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) — Dowiedz się, jak tooresolve typowe problemy związane z funkcją hello.
- [**Azure AD SSO bezproblemowe** ](active-directory-aadconnect-sso.md) — Dowiedz się więcej o tej funkcji uzupełniające.
- [**UserVoice** ](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) — w przypadku zgłoszenia żądania nowych funkcji.
