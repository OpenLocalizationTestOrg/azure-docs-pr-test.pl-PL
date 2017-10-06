---
title: "Azure AD Connect: Bezproblemowe logowanie jednokrotne — jak działa | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak działa hello Azure Active Directory bezproblemowe logowanie jednokrotne funkcji."
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
ms.date: 08/02/2017
ms.author: billmath
ms.openlocfilehash: 17ce35b32832d241068ab878cf7aac42deab74ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-seamless-single-sign-on-technical-deep-dive"></a>Azure Active Directory bezproblemowe logowanie jednokrotne: techniczne nowości

Ten artykuł zawiera szczegółowe informacje techniczne, w sposób działania hello Azure Active Directory bezproblemowe rejestracji jednokrotnej (SSO bezproblemowe) funkcji.

>[!IMPORTANT]
>funkcja logowania jednokrotnego bezproblemowe Hello jest obecnie w przeglądzie.

## <a name="how-does-seamless-sso-work"></a>Jak działa bezproblemowe logowanie Jednokrotne

Ta sekcja zawiera dwa tooit części:
1. Ustawienia funkcji logowania jednokrotnego bezproblemowe hello Hello.
2. Jak pojedynczego użytkownika logowania transakcji współpracuje z bezproblemowe logowania jednokrotnego.

### <a name="how-does-set-up-work"></a>Jak skonfigurować pracy?

Bezproblemowe rejestracji Jednokrotnej jest włączone, za pomocą usługi Azure AD Connect, jak pokazano [tutaj](active-directory-aadconnect-sso-quick-start.md). Podczas włączania funkcji hello, wykonywane hello następujące kroki:
- Konto komputera o nazwie `AZUREADSSOACCT` (reprezentuje usługi Azure AD) jest tworzony w lokalnej usłudze Active Directory (AD).
- klucz odszyfrowujący Kerberos konta komputera Hello jest udostępniony w bezpieczny sposób z usługą Azure AD.
- Ponadto dwóch Kerberos głównej nazwy usługi (SPN) są tworzone toorepresent dwa adresy URL, które są używane podczas logowania w usłudze Azure AD.

>[!NOTE]
> Hello konto komputera i nazwy SPN Kerberos hello są tworzone w każdym lesie usługi AD synchronizacji tooAzure AD (za pomocą usługi Azure AD Connect) oraz dla użytkowników, którzy mają bezproblemowe logowania jednokrotnego. Przenieś hello `AZUREADSSOACCT` tooan konta komputera jednostkę organizacji (OU) gdzie innych kont komputerów są przechowywane tooensure, który jest zarządzany w hello sam sposób i nie zostanie usunięta.

>[!IMPORTANT]
>Zdecydowanie zalecamy, aby użytkownik [Przerzuć klucz odszyfrowujący Kerberos hello](active-directory-aadconnect-sso-faq.md#how-can-i-roll-over-the-kerberos-decryption-key-of-the-azureadssoacct-computer-account) z hello `AZUREADSSOACCT` konta komputera co najmniej 30 dni.

### <a name="how-does-sign-in-with-seamless-sso-work"></a>Jak logowanie SSO bezproblemowe pracy?

Po zakończeniu konfigurowania hello bezproblemowe logowanie Jednokrotne działa hello sam sposób jak inne logowania, która używa zintegrowanego uwierzytelniania systemu Windows (IWA). przebieg Hello jest następujący:

1. Witaj użytkownik spróbuje tooaccess aplikacji (na przykład Witaj aplikacji Outlook Web App - https://outlook.office365.com/owa/) z urządzenia firmowe przyłączonych do domeny w sieci firmowej.
2. Jeśli użytkownik hello nie jest już zalogowany, użytkownika hello jest strony logowania usługi Azure AD toohello przekierowane.

  >[!NOTE]
  >Jeśli żądanie logowania hello Azure AD zawiera `domain_hint` (identyfikowanie dzierżawy — na przykład, contoso.onmicrosoft.com) lub `login_hint` (identyfikacji użytkownika hello — na przykład user@contoso.onmicrosoft.com lub user@contoso.com) parametr, a następnie w kroku 2 jest pomijana.

3. użytkownik wpisze Hello nazwy użytkownika do strony logowania hello Azure AD.
4. Przy użyciu języka JavaScript w tle hello, usługi Azure AD będzie wymagał hello przeglądarki, za pomocą odpowiedzi 401 nieautoryzowane, tooprovide biletu protokołu Kerberos.
5. Przeglądarka Hello z kolei żąda biletu z usługi Active Directory dla hello `AZUREADSSOACCT` konta komputera (co reprezentuje usługi Azure AD).
6. Usługi Active Directory lokalizuje hello konto komputera i zwraca przeglądarki toohello biletu Kerberos zaszyfrowane za pomocą konta komputera hello klucz tajny.
7. Przeglądarka Hello przekazuje on uzyskane z usługi Active Directory tooAzure AD biletu Kerberos hello (na jednym z hello [Azure AD adresy URL wcześniej dodane ustawienia strefy Intranet w przeglądarce toohello](active-directory-aadconnect-sso-quick-start.md#step-3-roll-out-the-feature)).
8. Azure AD odszyfrowywane hello biletu Kerberos, obejmujące hello tożsamości użytkownika hello zalogowaniem się do urządzeń firmowych hello wcześniej przy użyciu hello wspólny klucz.
9. Po dokonaniu oceny usługi Azure AD zwraca aplikacji toohello tyłu tokenu lub zapyta tooperform użytkownika hello dodatkowe dowody, takich jak uwierzytelnianie wieloskładnikowe.
10. Jeśli logowanie użytkownika hello zakończy się pomyślnie, użytkownik hello jest aplikacji hello tooaccess stanie.

Witaj poniższym diagramie przedstawiono wszystkie składniki hello i hello etapy.

![Bezproblemowe logowanie jednokrotne](./media/active-directory-aadconnect-sso/sso2.png)

Bezproblemowe rejestracji Jednokrotnej jest oportunistyczne, co oznacza, że w przypadku niepowodzenia hello logowania powraca zachowanie regularne tooits - tj, hello użytkownik powinien tooenter toosign ich haseł w.

## <a name="next-steps"></a>Następne kroki

- [**Szybki Start** ](active-directory-aadconnect-sso-quick-start.md) — Uzyskaj i systemem Azure AD bezproblemowe Usługa rejestracji Jednokrotnej.
- [**Często zadawane pytania** ](active-directory-aadconnect-sso-faq.md) -odpowiedzi toofrequently zadawane pytania.
- [**Rozwiązywanie problemów z** ](active-directory-aadconnect-troubleshoot-sso.md) — Dowiedz się, jak tooresolve typowe problemy związane z funkcją hello.
- [**UserVoice** ](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) — w przypadku zgłoszenia żądania nowych funkcji.
