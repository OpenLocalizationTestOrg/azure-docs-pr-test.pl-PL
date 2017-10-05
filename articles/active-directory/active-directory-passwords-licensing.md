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
ms.openlocfilehash: 936134bddad19964f809a17f200ebbeed5aa853c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="licensing-requirements-for-azure-ad-self-service-password-reset"></a>Wymagania dotyczące usługi Azure AD samoobsługi hasła licencjonowania resetowania

Aby resetowania hasła programu Azure AD, funkcji możesz **musi mieć co najmniej jedną licencję przypisane w Twojej organizacji**. Firma Microsoft nie wymuszają licencjonowania na środowisku resetowania hasła użytkownika. Aby zachować zgodność z umowy licencyjnej firmy Microsoft, należy przypisać licencje do użytkowników korzystających z funkcji premium.

* **Tylko użytkownicy w chmurze** -usługi Office 365 (O365) żadnego płatnej SKU lub Azure AD podstawowa
* **Chmura** i/lub **lokalnych użytkowników** -Azure AD Premium P1 lub P2 pakietu Enterprise Mobility + Security (EMS) i Secure produktywności przedsiębiorstwa (p)

## <a name="licenses-required-for-password-writeback"></a>Licencjami wymaganymi do zapisywania zwrotnego haseł

Aby użyć funkcji zapisywania zwrotnego haseł, musi mieć jedną z poniższych licencji przypisane w dzierżawie.

* Usługa Azure AD — warstwa Premium P1
* Usługa Azure AD — warstwa Premium P2
* Enterprise Mobility + Security E3
* Enterprise Mobility + Security E5
* Secure Productive Enterprise E3
* Secure Productive Enterprise E5

> [!NOTE]
> Plany licencjonowania usługi Office 365 autonomiczny **nie obsługują funkcji zapisywania zwrotnego haseł** i muszą mieć jedną z powyższych planów ta funkcja działała.

Dodatkowe informacje o licencji, wraz z kosztami można znaleźć na następujących stronach

* [Usługi Azure site cennik usługi Active Directory](https://azure.microsoft.com/pricing/details/active-directory/)
* [Enterprise Mobility + Security](https://www.microsoft.com/cloud-platform/enterprise-mobility-security)
* [Bezpieczne produktywności Enterprise](https://www.microsoft.com/secure-productive-enterprise/default.aspx)

## <a name="enable-group-or-user-based-licensing"></a>Włącz grupy lub użytkownika na podstawie licencjonowania

Teraz usługi Azure AD obsługuje oparte na grupach licencjonowania, dzięki czemu administratorzy Aby przypisać licencje zbiorczo do grupy użytkowników, a nie przypisywanie pojedynczo. [Przypisać, sprawdź i rozwiąż problemy z licencjami](active-directory-licensing-group-assignment-azure-portal.md#step-1-assign-the-required-licenses)

Pewnych usług firmy Microsoft nie są dostępne we wszystkich lokalizacjach. Zanim można przypisać licencję do użytkownika, administrator musi określić właściwość "Lokalizacji użytkowania" użytkownika. Można wykonać przypisania licencji użytkownika > Profil > w sekcji Ustawienia w portalu Azure. **Korzystając z przypisanie do grupy licencji, wszyscy użytkownicy bez użycia lokalizacji określonej dziedziczą lokalizację katalogu.**

## <a name="next-steps"></a>Następne kroki

Poniższe linki dają dostęp do dodatkowych informacji dotyczących resetowania haseł za pomocą usługi Azure AD

* [**Szybki start**](active-directory-passwords-getting-started.md) — Przygotowywanie do pracy samoobsługowego zarządzania hasłami w usłudze Azure AD 
* [**Dane**](active-directory-passwords-data.md) — Omówienie wymaganych danych i sposobu ich wykorzystania w zarządzaniu hasłami
* [**Wdrażanie**](active-directory-passwords-best-practices.md) — Planowanie funkcji samoobsługowego resetowania haseł i jej wdrażanie dla użytkowników przy użyciu znajdujących się tu wytycznych
* [**Dostosowywanie**](active-directory-passwords-customize.md) — Dostosowywanie wyglądu i działania środowiska samoobsługowego resetowania haseł dla firmy
* [**Raportowanie**](active-directory-passwords-reporting.md) — Czy, kiedy i gdzie użytkownicy uzyskują dostęp do funkcji samoobsługowego resetowania haseł
* [**Szczegóły techniczne**](active-directory-passwords-how-it-works.md) — Informacje o tym, co dzieje się za kulisami tej funkcji i jak ona działa
* [**Często zadawane pytania**](active-directory-passwords-faq.md) — Jak? Dlaczego? Co? Gdzie? Kto? Kiedy? — Odpowiedzi na wszystkie nurtujące Cię pytania
* [**Rozwiązywanie problemów**](active-directory-passwords-troubleshoot.md) — Informacje o tym, jak rozwiązywać typowe problemy z samoobsługowym resetowaniem haseł

