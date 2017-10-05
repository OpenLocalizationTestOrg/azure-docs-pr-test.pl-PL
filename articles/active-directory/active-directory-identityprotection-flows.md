---
title: "Logowanie napotyka przy użyciu usługi Azure AD Identity Protection | Dokumentacja firmy Microsoft"
description: "Zawiera omówienie środowiska użytkownika, gdy ochronę tożsamości ma skorygowane lub skorygowane przez użytkownika lub uwierzytelnianie wieloskładnikowe jest wymagany przez zasady."
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
ms.openlocfilehash: e45936280b51fb2e54012a688fceddcc8dabe984
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="sign-in-experiences-with-azure-ad-identity-protection"></a>Logowanie, korzystając z usługi Azure AD Identity Protection
Za pomocą usługi Azure Active Directory Identity Protection można:

* Wymagaj rejestracji w usłudze Multi-Factor authentication użytkowników
* Obsługa ryzykowne logowania i użytkowników z naruszonymi zabezpieczeniami

Odpowiedź systemu te problemy ma wpływ na środowisko logowania użytkownika, ponieważ tylko bezpośrednio logowanie przez podanie nazwy użytkownika i hasło nie będzie możliwe już. Aby bezpiecznie uzyskać użytkownika są wymagane dodatkowe kroki do firm.

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
Najlepsze środowisko użytkownika w przypadku obu zagrożone konto przepływu odzyskiwania i ryzykowne przepływu logowania, jest, gdy użytkownik samodzielnie można odzyskać. Jeśli użytkownicy są zarejestrowani w usłudze Multi-Factor authentication, mają numer telefonu skojarzony z użyciem konta, który może służyć do przekazywania trudności. Pomoc techniczna lub administrator udziałów jest niezbędne do odzyskanie konta naruszenia. W związku z tym zdecydowanie zaleca się zachęcić użytkowników zarejestrowanych w usłudze Multi-Factor authentication. 

Administratorzy mogą:

* ustawienie zasad, która wymaga od użytkowników skonfigurować swoje konta dodatkowej weryfikacji zabezpieczeń. 
* umożliwia pomijanie usługi Multi-Factor authentication rejestracji przez maksymalnie 30 dni, w przypadku, gdy chcą, aby umożliwić użytkownikom okres prolongaty przed zarejestrowaniem.

**Rejestracja usługi Multi-Factor authentication ma trzy kroki:**

1. W pierwszym kroku użytkownik otrzymuje powiadomienie o konieczności Skonfiguruj konto dla usługi Multi-Factor authentication. 
   
    ![Korygowanie](./media/active-directory-identityprotection-flows/140.png "korygowania")
2. Aby skonfigurować uwierzytelnianie wieloskładnikowe, należy umożliwić wiedzieć, jaki ma zostać można skontaktować się z systemu.
   
    ![Korygowanie](./media/active-directory-identityprotection-flows/141.png "korygowania")
3. System przesyła żądanie do i możesz muszą odpowiadać.
   
    ![Korygowanie](./media/active-directory-identityprotection-flows/142.png "korygowania")

## <a name="risky-sign-in-recovery"></a>Ryzykowne odzyskiwania logowania
Jeśli administrator skonfigurował zasady logowania ryzyka, narażeni użytkownicy są powiadamiani o próby logowania. 

**Ryzykowne przepływu logowania ma dwa kroki:** 

1. Użytkownik jest informowany nietypowe zachowanie wykryto o ich logowania, takich jak logowanie nastąpiło z nowej lokalizacji, urządzenia lub aplikacji. 
   
    ![Korygowanie](./media/active-directory-identityprotection-flows/120.png "korygowania")
2. Użytkownik musi potwierdzić swoją tożsamość przy użyciu testu zabezpieczeń rozwiązywania. Jeśli użytkownik jest zarejestrowany w usłudze Multi-Factor authentication muszą wyrównana kod zabezpieczeń w celu jego numeru telefonu. Ponieważ jest to tylko ryzykowne logowania i zagrożone konto użytkownika nie będziesz mieć możliwość zmiany hasła w tym przepływie. 
   
    ![Korygowanie](./media/active-directory-identityprotection-flows/121.png "korygowania")

## <a name="risky-sign-in-blocked"></a>Ryzykowne logowania zablokowane
Administratorzy mogą wybrać także ustawić zasady logowania ryzyka, aby uniemożliwić użytkownikom na logowanie się w zależności od poziomu zagrożenia. Uzyskanie odblokowany, użytkowników końcowych musisz skontaktować się z administratorem lub pomocą techniczną lub próbują można logować się z lokalizacji znanych lub urządzenia. Własnym odzyskiwanie przy rozwiązywaniu usługi Multi-Factor authentication nie jest opcją w tym przypadku.

![Korygowanie](./media/active-directory-identityprotection-flows/200.png "korygowania")

## <a name="compromised-account-recovery"></a>Zagrożone konto odzyskiwania
Gdy skonfigurowano zasady zabezpieczeń użytkownika ryzyka, użytkowników, którzy spełniają użytkownika ryzyka poziom określonym w zasadach (i w związku z tym są uznawane za naruszenia zabezpieczeń) musi przejść przepływu odzyskiwania naruszenia użytkownika przed ich można logowania. 

**Przepływ odzyskiwania naruszenia użytkownik ma trzy kroki:**

1. Użytkownik jest informowany, że ich bezpieczeństwo konta jest zablokowana z powodu podejrzanej aktywności lub ujawnione poświadczenia.
   
    ![Korygowanie](./media/active-directory-identityprotection-flows/101.png "korygowania")
2. Użytkownik musi potwierdzić swoją tożsamość przy użyciu testu zabezpieczeń rozwiązywania. Jeśli użytkownik jest zarejestrowany w usłudze Multi-Factor authentication będą oni mogli samodzielnie odzyskiwać złamaniu. Należy wyrównana kod zabezpieczeń w celu jego numeru telefonu. 
   
   ![Korygowanie](./media/active-directory-identityprotection-flows/110.png "korygowania")
3. Ponadto użytkownik będzie zmuszony do zmiany hasła, ponieważ ktoś inny ma dostęp do swojego konta. 
   Zrzuty ekranu to obsługi są poniżej.
   
   ![Korygowanie](./media/active-directory-identityprotection-flows/111.png "korygowania")

## <a name="compromised-account-blocked"></a>Zagrożone Konto zablokowane
Aby uzyskać użytkownika, który został zablokowany przez zasady zabezpieczeń użytkownika ryzyka odblokowany, użytkownik musi skontaktować się z administratorem lub pomocą techniczną. Własnym odzyskiwanie przy rozwiązywaniu usługi Multi-Factor authentication nie jest opcją w tym przypadku.

![Korygowanie](./media/active-directory-identityprotection-flows/104.png "korygowania")

## <a name="reset-password"></a>Resetowanie hasła
Jeśli ze złamanymi zabezpieczeniami użytkownicy są blokowani logowanie, administrator może generować hasło tymczasowe dla nich. Użytkownicy mają do zmiany hasła podczas następnego logowania.

![Korygowanie](./media/active-directory-identityprotection-flows/160.png "korygowania")

## <a name="see-also"></a>Zobacz też
* [Ochronę tożsamości usługi Azure Active Directory](active-directory-identityprotection.md) 

