---
title: "aaaAzure AD samoobsługowego resetowania hasła omówienie | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 0efc291b1eeec0b7ae33ff5a7d9ed38e70c8be6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-self-service-password-reset-for-hello-it-professional"></a>Azure AD samodzielnego resetowania haseł dla specjalistów IT hello

"Samoobsługi" jest buzzword zgłoszony wokół wewnątrz wielu działów IT między hello world z różnymi znaczenie. rynek Hello jest przeciążony produktów, które pozwalają toomanage grup lokalnych, hasła lub profile użytkowników z hello chmurze lub lokalnie.

Azure Active Directory (Azure AD) samoobsługowego resetowania hasła (SSPR) ustawia się od siebie z łatwość użycia i wdrażania. Hasła usługi Azure AD Samoobsługowe Resetowanie łączy zestaw funkcji, które:

* Zezwalaj na używanie Twojego toomanage użytkowników własne hasła
  * Na dowolnym urządzeniu
  * W dowolnym miejscu
  * W dowolnym momencie
* Zachować zgodność z zasadami zdefiniowanych przez administratora

Gdy wszystko będzie gotowe, możesz rozpocząć pracę z usługi Azure AD SSPR za pomocą naszych [szybki start wskazówki](active-directory-passwords-getting-started.md) i szybko uzyskiwać Resetowanie własnych haseł użytkowników.

## <a name="what-is-possible"></a>Co to jest możliwe

* **Zmiana hasła samoobsługi** umożliwia użytkownicy końcowi lub Administratorzy toochange swoje hasła bez pomocy administratora
* **Odblokowywanie kont samoobsługi** umożliwia toounlock użytkownicy końcowi własne konto bez pomocy administratora
* **Samoobsługowego resetowania hasła** umożliwia użytkownicy końcowi lub Administratorzy tooreset haseł automatycznie bez pomocy administratora. Samoobsługowe Resetowanie hasła wymaga wersji Azure AD Premium lub podstawowa - [wersje usługi Azure Active Directory](active-directory-editions.md).
* **Resetowanie hasła inicjowanych przez administratora** umożliwia tooreset administratora hasło użytkownika końcowego lub inny administrator z poziomu hello [portalu Azure](https://docs.microsoft.com/azure/azure-portal-overview)
* **Raporty dotyczące działań zarządzania hasło** zapewnia administratorom wgląd w działanie resetowania i rejestracji hasła występujących w tej organizacji - [raporty zarządzania](active-directory-passwords-reporting.md)
* **Zapisywanie zwrotne haseł** umożliwia zarządzanie hasłami lokalnymi z chmury hello federacyjnych wszystkich poprzedzających hello scenariusze można wykonać przez lub w imieniu hello, lub użytkowników synchronizacji haseł. Zapisywanie zwrotne haseł wymaga [Azure AD Premium](active-directory-get-started-premium.md).

## <a name="why-choose-azure-ad-self-service-password-reset"></a>Dlaczego Azure AD samoobsługowego resetowania hasła

* **Obniżenie kosztów** jako pomoc techniczna i obsługuje resetowania hasła asystowaną jest zwykle spędzają na 20% organizacji IT
* **Poprawę środowiska użytkownika końcowego** i **zmniejszyć wolumin techniczną** , zapewniając tooresolve power hello użytkownicy końcowi zagadnienia hasło jednocześnie bez wywoływania pomocy technicznej lub otwarcia żądania pomocy technicznej.
* **Dysk mobilności** jak użytkownicy mogą resetować hasła w dowolnym miejscu.

## <a name="azure-ad-self-service-password-reset-availability"></a>Azure AD samoobsługowego resetowania hasła dostępności

Hasła usługi Azure AD Samoobsługowe resetowanie jest dostępne w trzech warstwach w zależności od subskrypcji.

* **Azure AD wolne** — tylko w chmurze, Administratorzy mogą resetować swoje hasła
* **Azure AD podstawowa** lub **płatnej subskrypcji programu Office 365** — tylko w chmurze użytkownicy i Administratorzy tylko do chmury można resetować swoje hasła
* **Azure AD Premium** — federacyjnych dowolnego użytkownika lub administratora, w tym trybie tylko do chmury, lub hasło synchronizowane użytkownicy, można resetować swoje hasła. Hasłami lokalnymi wymagają włączone toobe zapisywania zwrotnego haseł.

## <a name="azure-ad-self-service-password-reset-a-sum-of-hello-parts"></a>Azure AD samoobsługowego resetowania hasła, sumę hello części

Własnym resetowania haseł w usłudze Azure AD składa się z hello następujące składniki:

* **Portal konfiguracji zarządzania hasło** gdzie można kontrolować opcje dotyczące sposobu zarządzania hasła w dzierżawie za pośrednictwem hello portalu Azure
* **Portal rejestracji resetowania haseł** której użytkownicy mogą zarejestrować się samodzielnie do resetowania hasła
* **Portal resetowania haseł** podano gdzie użytkownicy mogą zresetować swoje hasło przy użyciu zdefiniowanych przez administratora hello wyzwania hello oraz hello odpowiedzi użytkowników
* **Portal zmiany hasła użytkowników** gdzie użytkownicy mogą zmieniać swoje hasła wprowadzenie starego hasła i podając nowe hasło
* **Raporty zarządzania hasło** gdzie Administratorzy można przeglądać i analizować działanie hasła raporty dla swoich dzierżaw w hello portalu Azure
* **Hasło zapisywania zwrotnego tooon lokalnie przy użyciu usługi Azure AD Connect** umożliwia możesz tooenable Zarządzanie lokalnymi, federacyjnych, lub hasło synchronizowane użytkowników z chmury hello

## <a name="azure-ad-pricing-sla-updates-and-roadmap"></a>Azure AD cennik, umowy SLA, aktualizacji i plan

Więcej szczegółów na temat tych tematów można znaleźć na powitania po stron

* [**Szczegóły cennika usługi Azure AD**](https://azure.microsoft.com/pricing/details/active-directory/)
* [**Cennik usługi Office 365**](https://products.office.com/compare-all-microsoft-office-products?tab=2)
* [**Umowy dotyczące poziomu usług platformy Azure**](https://azure.microsoft.com/support/legal/sla/)
* [**Umowa dotycząca poziomu usług Microsoft Online Services**](http://go.microsoft.com/fwlink/?LinkID=272026&clcid=0x409)
* [**Aktualizacje platformy Azure**](https://azure.microsoft.com/updates/)
* [**Plan platformy Azure**](https://www.microsoft.com/cloud-platform/roadmap-recently-available)

## <a name="next-steps"></a>Następne kroki

Witaj następującego łącza znajdują się dodatkowe informacje dotyczące resetowania przy użyciu usługi Azure AD

* [**Szybki start**](active-directory-passwords-getting-started.md) — Przygotowywanie do pracy samoobsługowego zarządzania hasłami w usłudze Azure AD 
* [**Licencjonowanie**](active-directory-passwords-licensing.md) — Konfigurowanie licencjonowania w usłudze Azure AD
* [**Dane** ](active-directory-passwords-data.md) — zrozumieć dane hello jest wymagany i jak służy do zarządzania hasłami
* [**Wdrożenie** ](active-directory-passwords-best-practices.md) — planowanie i wdrażanie SSPR tooyour użytkowników przy użyciu wskazówek hello znaleźć tutaj
* [**Dostosowywanie** ](active-directory-passwords-customize.md) — Dostosowywanie hello wygląd i działanie hello SSPR środowisko firmy.
* [**Raportowanie**](active-directory-passwords-reporting.md) — Czy, kiedy i gdzie użytkownicy uzyskują dostęp do funkcji samoobsługowego resetowania haseł
* [**Nowości techniczne** ](active-directory-passwords-how-it-works.md) -przejdź za hello ściany toounderstand, jak to działa
* [**Często zadawane pytania**](active-directory-passwords-faq.md) — Jak? Dlaczego? Co? Gdzie? Kto? Kiedy? -Tooquestions tooask chciał zawsze odpowiada
* [**Rozwiązywanie problemów z** ](active-directory-passwords-troubleshoot.md) — Dowiedz się, jak tooresolve typowe problemy, widzimy z SSPR

