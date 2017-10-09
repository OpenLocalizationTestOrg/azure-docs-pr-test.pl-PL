---
title: "aaaAzure Active Directory Identity Protection — jak użytkownicy toounblock | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak odblokować użytkowników, które zostały zablokowane przez zasady usługi Azure Active Directory Identity Protection."
services: active-directory
keywords: "ochronę tożsamości usługi Azure active directory, Odblokuj użytkownika"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: a953d425-a3ef-41f8-a55d-0202c3f250a7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: cdda2808822888f76aa75cf46478738c94df51a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-identity-protection---how-toounblock-users"></a>Azure Active Directory Identity Protection — jak toounblock użytkowników
Azure Active Directory ochronę tożsamości można skonfigurować zasady, które użytkownicy tooblock skonfigurowanie hello warunki są spełnione. Zazwyczaj zablokowany użytkownik kontaktów pomocy technicznej toobecome odblokowany. Tematy to wyjaśniono również hello można wykonywać toounblock zablokowany użytkownik.

## <a name="determine-hello-reason-for-blocking"></a>Określ przyczynę hello dotyczące blokowania
Jako pierwszy krok toounblock użytkownika należy toodetermine hello typ zasad, który zablokował hello użytkownika, ponieważ Twoje następne kroki są od niego zależne.
Azure Active Directory Identity Protection użytkownik może zostać albo zablokowana przez zasady logowania ryzyko lub zasad ryzyka dla użytkownika.

Można pobrać typu hello zasady, które zablokował użytkownika z pozycji hello w oknie dialogowym hello, który został przedstawiony toohello użytkowników podczas prób logowania:

| Zasady | Okno dialogowe użytkownika |
| --- | --- |
| Ryzyko logowania |![Zablokowane logowania](./media/active-directory-identityprotection-unblock-howto/02.png) |
| Ryzyko użytkownika |![Konto zablokowane](./media/active-directory-identityprotection-unblock-howto/104.png) |

Użytkownik, który jest zablokowany przez:

* Zasady logowania ryzyko jest także znana jako podejrzane logowania
* Zasad ryzyka dla użytkownika jest także znana jako konto na ryzyko

## <a name="unblocking-suspicious-sign-ins"></a>Odblokowywanie podejrzane logowania
toounblock podejrzane logowanie, masz hello następujące opcje:

1. **Logowania z lokalizacji znanych lub urządzenia** -typową przyczyną zablokowanych podejrzane logowania są próby logowania z nieznanych lokalizacji lub urządzeń. Użytkownicy może szybko określić, czy jest to hello blokuje Przyczyna podejmując toosign w znanych lokalizacji lub urządzenia.
2. **Wyklucz z zasad** — Jeśli uważasz, że hello bieżącej konfiguracji zasad logowania powoduje problemy dotyczące konkretnych użytkowników, użytkownicy hello można wykluczyć z niej. Zobacz [Azure Active Directory Identity Protection](active-directory-identityprotection.md) więcej szczegółów.
3. **Wyłącz zasady** — Jeśli uważasz, że konfigurację zasad powoduje problemy dotyczące wszystkich użytkowników, możesz wyłączyć hello zasad. Zobacz [Azure Active Directory Identity Protection](active-directory-identityprotection.md) więcej szczegółów.

## <a name="unblocking-accounts-at-risk"></a>Odblokowywanie kont na ryzyko
toounblock konta zagrożone, masz hello następujące opcje:

1. **Zresetuj hasło** — można zresetować hasło użytkownika hello. Zobacz [resetowania ręcznego bezpiecznego hasła](active-directory-identityprotection.md#manual-secure-password-reset) więcej szczegółów.
2. **Odrzuć wszystkie zdarzenia o podwyższonym ryzyku** -zasad ryzyka użytkownika hello blokuje użytkownika, jeśli został osiągnięty poziom ryzyka użytkownika hello skonfigurowany do blokowania dostępu. Użytkownik może zmniejszyć jego poziom ryzyka przez ręczne zamknięcie zgłoszone zdarzenia ryzyka. Aby uzyskać więcej informacji, zobacz [zamknięcie zdarzenia o podwyższonym ryzyku ręcznie](active-directory-identityprotection.md#closing-risk-events-manually).
3. **Wyklucz z zasad** — Jeśli uważasz, że hello bieżącej konfiguracji zasad logowania powoduje problemy dotyczące konkretnych użytkowników, użytkownicy hello można wykluczyć z niej. Zobacz [Azure Active Directory Identity Protection](active-directory-identityprotection.md) więcej szczegółów.
4. **Wyłącz zasady** — Jeśli uważasz, że konfigurację zasad powoduje problemy dotyczące wszystkich użytkowników, możesz wyłączyć hello zasad. Zobacz [Azure Active Directory Identity Protection](active-directory-identityprotection.md) więcej szczegółów.

## <a name="next-steps"></a>Następne kroki
 Czy chcesz, aby tooknow więcej informacji na temat usługi Azure AD Identity Protection? Zapoznaj się z [Azure Active Directory Identity Protection](active-directory-identityprotection.md).
