---
title: 'Licencjonowanie: Azure AD SSPR | Dokumentacja firmy Microsoft'
description: "Azure AD samoobsługowego resetowania hasła wymagania licencyjne"
services: active-directory
keywords: 
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
ms.openlocfilehash: 9cecaaac429165346f7082f1965dc8a21063fe7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="licensing-requirements-for-azure-ad-self-service-password-reset"></a>Wymagania dotyczące usługi Azure AD samoobsługi hasła licencjonowania resetowania

Aby Azure resetowania hasła AD toofunction możesz **musi mieć co najmniej jedną licencję przypisane w Twojej organizacji**. Firma Microsoft nie wymuszają licencjonowania na środowisko resetowania hasła hello na użytkownika. toomaintain zgodności z umowy licencyjnej firmy Microsoft, należy tooassign licencji tooany użytkowników korzystających z funkcji premium.

* **Tylko użytkownicy w chmurze** -usługi Office 365 (O365) żadnego płatnej SKU lub Azure AD podstawowa
* **Chmura** i/lub **lokalnych użytkowników** -Azure AD Premium P1 lub P2 pakietu Enterprise Mobility + Security (EMS) i Secure produktywności przedsiębiorstwa (p)

## <a name="licenses-required-for-password-writeback"></a>Licencjami wymaganymi do zapisywania zwrotnego haseł

Zapisywanie zwrotne haseł toouse, użytkownik musi mieć jeden z powitania od licencji przypisanych w dzierżawie.

* Usługa Azure AD — warstwa Premium P1
* Usługa Azure AD — warstwa Premium P2
* Enterprise Mobility + Security E3
* Enterprise Mobility + Security E5
* Secure Productive Enterprise E3
* Secure Productive Enterprise E5

> [!NOTE]
> Plany licencjonowania usługi Office 365 autonomiczny **nie obsługują funkcji zapisywania zwrotnego haseł** i wymagać hello poprzedzających plany toowork tej funkcji.

Dodatkowe informacje o licencji, wraz z kosztami znajduje się na powitania po stron

* [Usługi Azure site cennik usługi Active Directory](https://azure.microsoft.com/pricing/details/active-directory/)
* [Enterprise Mobility + Security](https://www.microsoft.com/cloud-platform/enterprise-mobility-security)
* [Bezpieczne produktywności Enterprise](https://www.microsoft.com/secure-productive-enterprise/default.aspx)

## <a name="enable-group-or-user-based-licensing"></a>Włącz grupy lub użytkownika na podstawie licencjonowania

Teraz usługi Azure AD obsługuje oparte na grupach licencjonowania, dzięki czemu administratorzy tooassign licencji w zbiorczego tooa grupy użytkowników, a nie przypisywanie pojedynczo. [Przypisać, sprawdź i rozwiąż problemy z licencjami](active-directory-licensing-group-assignment-azure-portal.md#step-1-assign-the-required-licenses)

Pewnych usług firmy Microsoft nie są dostępne we wszystkich lokalizacjach. Przed tooa użytkownika można przypisać licencji, hello administrator musi określać właściwość "Lokalizacji użytkowania" hello na powitania użytkownika. Można wykonać przypisania licencji użytkownika > Profil > w sekcji Ustawienia w hello portalu Azure. **Korzystając z przypisanie do grupy licencji, wszyscy użytkownicy bez użycia lokalizacji określonej dziedziczą hello lokalizację katalogu hello.**

## <a name="next-steps"></a>Następne kroki

Witaj następującego łącza znajdują się dodatkowe informacje dotyczące resetowania przy użyciu usługi Azure AD

* [**Szybki start**](active-directory-passwords-getting-started.md) — Przygotowywanie do pracy samoobsługowego zarządzania hasłami w usłudze Azure AD 
* [**Dane** ](active-directory-passwords-data.md) — zrozumieć dane hello jest wymagany i jak służy do zarządzania hasłami
* [**Wdrożenie** ](active-directory-passwords-best-practices.md) — planowanie i wdrażanie SSPR tooyour użytkowników przy użyciu wskazówek hello znaleźć tutaj
* [**Dostosowywanie** ](active-directory-passwords-customize.md) — Dostosowywanie hello wygląd i działanie hello SSPR środowisko firmy.
* [**Raportowanie**](active-directory-passwords-reporting.md) — Czy, kiedy i gdzie użytkownicy uzyskują dostęp do funkcji samoobsługowego resetowania haseł
* [**Nowości techniczne** ](active-directory-passwords-how-it-works.md) -przejdź za hello ściany toounderstand, jak to działa
* [**Często zadawane pytania**](active-directory-passwords-faq.md) — Jak? Dlaczego? Co? Gdzie? Kto? Kiedy? -Tooquestions tooask chciał zawsze odpowiada
* [**Rozwiązywanie problemów z** ](active-directory-passwords-troubleshoot.md) — Dowiedz się, jak tooresolve typowe problemy, widzimy z SSPR

