---
title: "aaaAzure usługi Active Directory hybrydowego zagadnienia dotyczące projektowania tożsamości — określanie wymagań dotyczących uwierzytelniania wieloskładnikowego"
description: "Z kontroli dostępu warunkowego usługi Azure Active Directory sprawdza hello określonych warunków, można wybrać podczas uwierzytelniania użytkownika hello i przed zezwoleniem na dostęp toohello aplikacji. Gdy te warunki są spełnione, użytkownik hello uwierzytelniony i dozwolone dostępu toohello aplikacji."
documentationcenter: 
services: active-directory
author: femila
manager: billmath
editor: 
ms.assetid: 9c59fda9-47d0-4c7e-b3e7-3575c29beabe
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 49fa7b43772fb3a2d6664747477c60a34cddde2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="determine-multi-factor-authentication-requirements-for-your-hybrid-identity-solution"></a>Określić wymagania dotyczące rozwiązania z tożsamością hybrydową uwierzytelniania wieloskładnikowego
W tym świecie mobilności użytkownikom uzyskiwanie dostępu do danych i aplikacji w chmurze hello i na dowolnym urządzeniu zabezpieczanie informacji stał się podstawowym.  Codziennie jest nowy nagłówek o naruszenie zabezpieczeń.  Mimo że nie ma żadnej gwarancji przed takie naruszenia, uwierzytelnianie wieloskładnikowe, zapewnia dodatkową warstwę zabezpieczeń toohelp zapobiec tych naruszeń.
Rozpocznij od Trwa szacowanie wymagań organizacji hello uwierzytelnianie wieloskładnikowe. Co to jest toosecure w trakcie hello organizacji.  Tej oceny jest ważne toodefine hello wymagania techniczne dotyczące konfigurowania i umożliwienie użytkownikom organizacje hello uwierzytelnianie wieloskładnikowe.

> [!NOTE]
> Jeśli nie masz doświadczenia z usługami MFA i jakie operacje, zdecydowanie zaleca się przeczytanie artykułu hello [co to jest usługa Azure Multi-Factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md) toocontinue przed przeczytaniem tej części.
> 
> 

Upewnij się, że tooanswer hello następujące:

* Firma chce toosecure aplikacji firmy Microsoft? 
* Jak te aplikacje są publikowane?
* Firma oferuje dostępu zdalnego tooallow pracowników tooaccess lokalnej aplikacji?

Jeśli tak, jakiego typu dostępu zdalnego? Należy również tooevaluate, w której zostaną umieszczone hello użytkowników, którzy uzyskują dostęp do tych aplikacji. Tej oceny jest kolejną strategią odpowiednie uwierzytelnianie wieloskładnikowe, ważnym krokiem toodefine hello. Upewnij się, że hello tooanswer następujące pytania:

* Gdzie znajdują się użytkownicy hello przechodzi toobe?
* Mogą one znajdować się w dowolnym?
* Czy firma chce ograniczenia tooestablish zgodnie z lokalizacją użytkownika toohello?

Po zrozumieniu wymagań, ważne jest tooalso oceny wymagań dotyczących hello użytkownika usługi Multi-Factor Authentication. Tej oceny jest ważne, ponieważ będzie definiował hello wymagania dotyczące wdrażania usługi Multi-Factor authentication. Upewnij się, że hello tooanswer następujące pytania:

* Znasz hello użytkowników usługi Multi-Factor authentication?
* Niektóre zastosowania będzie tooprovide wymagane dodatkowe uwierzytelnianie?  
  * Jeśli tak, wszystkie hello czas, po wznowieniu z sieci zewnętrznych lub podczas uzyskiwania dostępu do określonych aplikacji lub w innych warunkach?
* Użytkownicy hello wymaga szkolenia dotyczące toosetup i wdrożenie usługi Multi-Factor authentication?
* Jakie są najważniejsze scenariusze hello, że firma chce tooenable uwierzytelnianie wieloskładnikowe dla użytkowników?

Po odpowiedzi na pytania wstecz hello, będzie możliwe toounderstand przypadku lokalne uwierzytelnianie wieloskładnikowe już zaimplementowany. Tej oceny jest ważne toodefine hello wymagania techniczne dotyczące konfigurowania i umożliwienie użytkownikom organizacje hello uwierzytelnianie wieloskładnikowe. Upewnij się, że hello tooanswer następujące pytania:

* Czy firma potrzebuje tooprotect uprzywilejowane konta za pomocą usługi MFA?
* Czy firma musi tooenable MFA dla niektórych aplikacji dla zachowania zgodności?
* Czy firma musi tooenable MFA dla wszystkich kwalifikujących się użytkowników z tych aplikacji lub tylko administratorzy
* Czy konieczne jest zawsze włączone uwierzytelnianie MFA lub tylko wtedy, gdy hello użytkownicy są zalogowani poza siecią firmową?

## <a name="next-steps"></a>Następne kroki
[Definiowanie strategii wdrażania tożsamości hybrydowej](active-directory-hybrid-identity-design-considerations-identity-adoption-strategy.md)

## <a name="see-also"></a>Zobacz też
[Omówienie zagadnień dotyczących projektowania](active-directory-hybrid-identity-design-considerations-overview.md)

