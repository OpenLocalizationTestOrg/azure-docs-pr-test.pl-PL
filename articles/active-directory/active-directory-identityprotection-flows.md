---
title: "w aaaSign, korzystając z usługi Azure AD Identity Protection | Dokumentacja firmy Microsoft"
description: "Zawiera omówienie hello środowisko użytkownika podczas ochrony tożsamości skorygowane lub skorygowane przez użytkownika lub gdy uwierzytelnianie wieloskładnikowe jest wymagany przez zasady."
services: active-directory
keywords: "ochronę tożsamości usługi Azure active directory, usługa cloud app discovery, zarządzanie aplikacjami, zabezpieczeń, ryzyka, poziom ryzyka, luki w zabezpieczeniach, zasady zabezpieczeń"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: de5bf637-75a7-4104-b6d8-03686372a319
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: fbdca5b86ed93d0a2f2b6df1dd0150da9c0c85c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="sign-in-experiences-with-azure-ad-identity-protection"></a>Logowanie, korzystając z usługi Azure AD Identity Protection
Za pomocą usługi Azure Active Directory Identity Protection można:

* Wymagaj uwierzytelniania wieloskładnikowego tooregister użytkowników
* Obsługa ryzykowne logowania i użytkowników z naruszonymi zabezpieczeniami

odpowiedź Hello hello systemu toothese problemów ma wpływ na środowiska logowania użytkownika, ponieważ tylko bezpośrednio logowanie przez podanie nazwy użytkownika i hasło nie będzie możliwe już. Dodatkowe kroki są wymagane tooget użytkownika bezpiecznie z powrotem do firm.

Ten temat zawiera omówienie środowiska użytkownika logowania dla wszystkich przypadków, które mogą wystąpić.

**Multi-Factor Authentication**

* Uwierzytelnianie wieloskładnikowe rejestracji

**Logowanie na ryzyko**

* Ryzykowne odzyskiwania logowania
* Ryzykowne logowania zablokowane
* Rejestracja usługi Multi-Factor authentication podczas ryzykowne logowanie

**Użytkownik na ryzyko**

* Zagrożone konto odzyskiwania
* Zagrożone Konto zablokowane

## <a name="multi-factor-authentication-registration"></a>Uwierzytelnianie wieloskładnikowe rejestracji
Witaj najlepsze środowisko użytkownika dla obu, hello zagrożone konto przepływu odzyskiwania i hello ryzykowne przepływu logowania, jest, gdy użytkownik hello własnym można odzyskać. Jeśli użytkownicy są zarejestrowani w usłudze Multi-Factor authentication, mają numer telefonu skojarzony z użyciem konta, które mogą być używane toopass trudności. Pomoc techniczna lub administrator udziałów jest wymagane toorecover przed złamaniem konta. W związku z tym zdecydowanie zaleca tooget użytkowników zarejestrowanych w usłudze Multi-Factor authentication. 

Administratorzy mogą:

* Ustaw zasady, które wymaga tooset użytkownikom ich kont do dodatkowej weryfikacji zabezpieczeń. 
* umożliwia pomijanie rejestracji usługi Multi-Factor authentication dla się too30 dni, w przypadku, gdy mają one użytkownikom toogive okres prolongaty przed zarejestrowaniem.

**Witaj rejestracji usługi Multi-Factor authentication ma trzy kroki:**

1. W pierwszym kroku hello hello użytkownik otrzymuje powiadomienie o hello wymaganie tooset hello koncie dla usługi Multi-Factor authentication. 
   
    ![Korygowanie](./media/active-directory-identityprotection-flows/140.png "korygowania")
2. uwierzytelnianie wieloskładnikowe tooset zapasowej, należy toolet hello systemu znać sposób toobe nawiązać z nią kontaktu.
   
    ![Korygowanie](./media/active-directory-identityprotection-flows/141.png "korygowania")
3. Hello system przesyła tooyou żądania i należy toorespond.
   
    ![Korygowanie](./media/active-directory-identityprotection-flows/142.png "korygowania")

## <a name="risky-sign-in-recovery"></a>Ryzykowne odzyskiwania logowania
Jeśli administrator skonfigurował zasady logowania ryzyka, hello wpływ użytkownicy są powiadamiani próbują toosign w. 

**Witaj ryzykowne logowania przepływu obejmuje dwa kroki:** 

1. Witaj, użytkownik jest informowany, nietypowe zachowanie wykryto o ich logowania, takich jak logowanie nastąpiło z nowej lokalizacji, urządzenia lub aplikacji. 
   
    ![Korygowanie](./media/active-directory-identityprotection-flows/120.png "korygowania")
2. Witaj użytkownika jest wymagane tooprove swoją tożsamość przy użyciu testu zabezpieczeń rozwiązywania. Jeśli użytkownik hello jest zarejestrowany w usłudze Multi-Factor authentication muszą tooround podróży służbowej numeru telefonu tootheir kodu zabezpieczeń. Ponieważ jest to tylko ryzykowne logowania i nie zagrożone konto użytkownika hello nie będziesz mieć hasłem hello toochange w tym przepływie. 
   
    ![Korygowanie](./media/active-directory-identityprotection-flows/121.png "korygowania")

## <a name="risky-sign-in-blocked"></a>Ryzykowne logowania zablokowane
Administratorzy mogą również wybrać tooset tooblock zasad ryzyka logowania użytkowników na logowanie się w zależności od poziomu zagrożenia hello. tooget odblokowany, użytkownicy końcowi muszą skontaktuj się z administratorem lub pomocą techniczną lub próbują można logować się z lokalizacji znanych lub urządzenia. Własnym odzyskiwanie przy rozwiązywaniu usługi Multi-Factor authentication nie jest opcją w tym przypadku.

![Korygowanie](./media/active-directory-identityprotection-flows/200.png "korygowania")

## <a name="compromised-account-recovery"></a>Zagrożone konto odzyskiwania
Gdy skonfigurowano zasady zabezpieczeń użytkownika ryzyka, użytkowników, którzy spełniają użytkownika hello ryzyka poziom określonym w zasadach hello (i w związku z tym są uznawane za naruszenia zabezpieczeń) musi przejść hello użytkownika naruszenia odzyskiwania przepływu, przed ich można logowania. 

**Witaj użytkownika naruszenia odzyskiwania przepływu ma trzy kroki:**

1. Witaj, użytkownik jest informowany, że ich bezpieczeństwo konta jest zablokowana z powodu podejrzanej aktywności lub ujawnione poświadczenia.
   
    ![Korygowanie](./media/active-directory-identityprotection-flows/101.png "korygowania")
2. Witaj użytkownika jest wymagane tooprove swoją tożsamość przy użyciu testu zabezpieczeń rozwiązywania. Witaj użytkownik jest zarejestrowany w usłudze Multi-Factor authentication będą oni mogli samodzielnie odzyskiwać złamaniu. Należy tooround podróży służbowej numeru telefonu tootheir kodu zabezpieczeń. 
   
   ![Korygowanie](./media/active-directory-identityprotection-flows/110.png "korygowania")
3. Na koniec hello użytkownika jest wymuszone toochange swojego hasła, ponieważ ktoś inny ma dostęp do konta tootheir. 
   Zrzuty ekranu to obsługi są poniżej.
   
   ![Korygowanie](./media/active-directory-identityprotection-flows/111.png "korygowania")

## <a name="compromised-account-blocked"></a>Zagrożone Konto zablokowane
tooget użytkownika, który został zablokowany przez zasady zabezpieczeń użytkownika ryzyka odblokowany hello użytkownik musi skontaktować się administratora lub pomocy technicznej. Własnym odzyskiwanie przy rozwiązywaniu usługi Multi-Factor authentication nie jest opcją w tym przypadku.

![Korygowanie](./media/active-directory-identityprotection-flows/104.png "korygowania")

## <a name="reset-password"></a>Resetowanie hasła
Jeśli ze złamanymi zabezpieczeniami użytkownicy są blokowani logowanie, administrator może generować hasło tymczasowe dla nich. Witaj, użytkownicy będą mieli toochange swoje hasło podczas następnego logowania.

![Korygowanie](./media/active-directory-identityprotection-flows/160.png "korygowania")

## <a name="see-also"></a>Zobacz też
* [Ochronę tożsamości usługi Azure Active Directory](active-directory-identityprotection.md) 

