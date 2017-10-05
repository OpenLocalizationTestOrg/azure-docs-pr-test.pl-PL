---
title: "Azure AD samoobsługowego resetowania hasła omówienie | Dokumentacja firmy Microsoft"
description: "Co zrobić własnym resetowania haseł w usłudze Azure AD dla Twojej organizacji?"
services: active-directory
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: 3903c53b78e61b380bb812a9d3ade694655b5afb
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-self-service-password-reset-for-the-it-professional"></a>Azure AD samodzielnego resetowania haseł dla specjalistów IT

"Samoobsługi" jest buzzword zgłoszony wokół wewnątrz wielu działów IT w całym świecie z różnymi znaczenie. Rynek jest przeciążony produktów, które umożliwiają zarządzanie grupami lokalnymi, hasła lub profilów użytkowników w chmurze lub lokalnie.

Azure Active Directory (Azure AD) samoobsługowego resetowania hasła (SSPR) ustawia się od siebie z łatwość użycia i wdrażania. Hasła usługi Azure AD Samoobsługowe Resetowanie łączy zestaw funkcji, które:

* Zezwalaj użytkownikom na zarządzanie swoje hasła
  * Na dowolnym urządzeniu
  * W dowolnym miejscu
  * W dowolnym momencie
* Zachować zgodność z zasadami zdefiniowanych przez administratora

Gdy wszystko będzie gotowe, możesz rozpocząć pracę z usługi Azure AD SSPR za pomocą naszych [szybki start wskazówki](active-directory-passwords-getting-started.md) i szybko uzyskiwać Resetowanie własnych haseł użytkowników.

## <a name="what-is-possible"></a>Co to jest możliwe

* **Zmiana hasła samoobsługi** umożliwia użytkownicy końcowi lub administratorzy zmienić swoje hasła bez pomocy administratora
* **Odblokowywanie kont samoobsługi** umożliwia użytkownikom końcowym odblokować konto bez pomocy administratora
* **Samoobsługowego resetowania hasła** umożliwia użytkownicy końcowi lub Administratorzy na resetowanie haseł automatycznie bez pomocy administratora. Samoobsługowe Resetowanie hasła wymaga wersji Azure AD Premium lub podstawowa - [wersje usługi Azure Active Directory](active-directory-editions.md).
* **Resetowanie hasła inicjowanych przez administratora** administrator może zresetować hasło użytkownika końcowego lub inny administrator z poziomu [portalu Azure](https://docs.microsoft.com/azure/azure-portal-overview)
* **Raporty dotyczące działań zarządzania hasło** zapewnia administratorom wgląd w działanie resetowania i rejestracji hasła występujących w tej organizacji - [raporty zarządzania](active-directory-passwords-reporting.md)
* **Zapisywanie zwrotne haseł** umożliwia zarządzanie hasłami lokalnymi z chmury, więc wszystkie scenariusze poprzedzających można wykonać przez lub w imieniu, federacyjnych lub hasło synchronizowane użytkowników. Zapisywanie zwrotne haseł wymaga [Azure AD Premium](active-directory-get-started-premium.md).

## <a name="why-choose-azure-ad-self-service-password-reset"></a>Dlaczego Azure AD samoobsługowego resetowania hasła

* **Obniżenie kosztów** jako pomoc techniczna i obsługuje resetowania hasła asystowaną jest zwykle spędzają na 20% organizacji IT
* **Poprawę środowiska użytkownika końcowego** i **zmniejszyć wolumin techniczną** , zapewniając użytkownikom końcowym zasilania problemów własne hasło jednocześnie bez wywoływania pomocy technicznej lub otwarcia żądania pomocy technicznej.
* **Dysk mobilności** jak użytkownicy mogą resetować hasła w dowolnym miejscu.

## <a name="azure-ad-self-service-password-reset-availability"></a>Azure AD samoobsługowego resetowania hasła dostępności

Hasła usługi Azure AD Samoobsługowe resetowanie jest dostępne w trzech warstwach w zależności od subskrypcji.

* **Azure AD wolne** — tylko w chmurze, Administratorzy mogą resetować swoje hasła
* **Azure AD podstawowa** lub **płatnej subskrypcji programu Office 365** — tylko w chmurze użytkownicy i Administratorzy tylko do chmury można resetować swoje hasła
* **Azure AD Premium** — federacyjnych dowolnego użytkownika lub administratora, w tym trybie tylko do chmury, lub hasło synchronizowane użytkownicy, można resetować swoje hasła. Hasłami lokalnymi wymagają funkcji zapisywania zwrotnego haseł jest włączony.

## <a name="azure-ad-self-service-password-reset-a-sum-of-the-parts"></a>Azure AD samoobsługowego resetowania hasła, suma elementów

Własnym resetowania haseł w usłudze Azure AD składa się z następujących składników:

* **Portal konfiguracji zarządzania hasło** gdzie można kontrolować opcje dotyczące sposobu zarządzania hasła w dzierżawie za pośrednictwem portalu Azure
* **Portal rejestracji resetowania haseł** której użytkownicy mogą zarejestrować się samodzielnie do resetowania hasła
* **Portal resetowania haseł** gdzie użytkownicy mogą zresetować swoje hasło przy użyciu wyzwania zdefiniowanych przez administratora, a podano użytkowników odpowiedzi
* **Portal zmiany hasła użytkowników** gdzie użytkownicy mogą zmieniać swoje hasła wprowadzenie starego hasła i podając nowe hasło
* **Raporty zarządzania hasło** gdzie Administratorzy można przeglądać i analizować działanie hasła raporty dla swoich dzierżaw w portalu Azure
* **Zapisywanie zwrotne haseł do lokalnego za pomocą usługi Azure AD Connect** umożliwia włączenie zarządzania lokalnymi, federacyjnych, lub hasło synchronizowane użytkowników z chmury

## <a name="azure-ad-pricing-sla-updates-and-roadmap"></a>Azure AD cennik, umowy SLA, aktualizacji i plan

Więcej szczegółów na temat tych tematów można znaleźć na następujących stronach

* [**Szczegóły cennika usługi Azure AD**](https://azure.microsoft.com/pricing/details/active-directory/)
* [**Cennik usługi Office 365**](https://products.office.com/compare-all-microsoft-office-products?tab=2)
* [**Umowy dotyczące poziomu usług platformy Azure**](https://azure.microsoft.com/support/legal/sla/)
* [**Umowa dotycząca poziomu usług Microsoft Online Services**](http://go.microsoft.com/fwlink/?LinkID=272026&clcid=0x409)
* [**Aktualizacje platformy Azure**](https://azure.microsoft.com/updates/)
* [**Plan platformy Azure**](https://www.microsoft.com/cloud-platform/roadmap-recently-available)

## <a name="next-steps"></a>Następne kroki

Poniższe linki dają dostęp do dodatkowych informacji dotyczących resetowania haseł za pomocą usługi Azure AD

* [**Szybki start**](active-directory-passwords-getting-started.md) — Przygotowywanie do pracy samoobsługowego zarządzania hasłami w usłudze Azure AD 
* [**Licencjonowanie**](active-directory-passwords-licensing.md) — Konfigurowanie licencjonowania w usłudze Azure AD
* [**Dane**](active-directory-passwords-data.md) — Omówienie wymaganych danych i sposobu ich wykorzystania w zarządzaniu hasłami
* [**Wdrażanie**](active-directory-passwords-best-practices.md) — Planowanie funkcji samoobsługowego resetowania haseł i jej wdrażanie dla użytkowników przy użyciu znajdujących się tu wytycznych
* [**Dostosowywanie**](active-directory-passwords-customize.md) — Dostosowywanie wyglądu i działania środowiska samoobsługowego resetowania haseł dla firmy
* [**Raportowanie**](active-directory-passwords-reporting.md) — Czy, kiedy i gdzie użytkownicy uzyskują dostęp do funkcji samoobsługowego resetowania haseł
* [**Szczegóły techniczne**](active-directory-passwords-how-it-works.md) — Informacje o tym, co dzieje się za kulisami tej funkcji i jak ona działa
* [**Często zadawane pytania**](active-directory-passwords-faq.md) — Jak? Dlaczego? Co? Gdzie? Kto? Kiedy? — Odpowiedzi na wszystkie nurtujące Cię pytania
* [**Rozwiązywanie problemów**](active-directory-passwords-troubleshoot.md) — Informacje o tym, jak rozwiązywać typowe problemy z samoobsługowym resetowaniem haseł

