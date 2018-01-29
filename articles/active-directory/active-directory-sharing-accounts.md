---
title: "Udostępnianie kont za pomocą usługi Azure AD | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak Azure Active Directory umożliwia organizacjom bezpieczne udostępnianie kont dla aplikacji lokalnych i usług w chmurze konsumenta."
services: active-directory
documentationcenter: 
author: curtand
manager: mtillman
editor: 
ms.assetid: e2d77104-d978-46a3-bfea-03ffdf3b61e6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/13/2017
ms.author: curtand
ms.reviewer: jeffsta
ms.custom: it-pro
ms.openlocfilehash: 3b6a83d91ec5d8466669655d6c3bd7ae7b42dd2f
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/11/2017
---
# <a name="sharing-accounts-with-azure-ad"></a>Udostępnianie kont usługi Azure AD
## <a name="overview"></a>Omówienie
Czasami organizacji, należy użyć jednej nazwy użytkownika i hasło dla wielu osób, które zwykle odbywa się w obu przypadkach:

* Podczas uzyskiwania dostępu do aplikacji, które wymagają unikatowych logowania i hasło dla każdego użytkownika, czy aplikacjami lokalnymi lub odbiorcy usług w chmurze (na przykład kont firmowych mediów społecznościowych).
* Podczas tworzenia środowiska wielu użytkowników. Może mieć pojedynczy konto lokalne, mającego podniesione uprawnienia, który służy do podstawowe działania Instalatora, Administracja i odzyskiwania. Na przykład "globalny administrator lokalny" konto usługi Office 365 lub konta głównego w usłudze Salesforce.

Zazwyczaj te konta są współużytkowane przez dystrybucję poświadczeń (nazwy użytkownika i hasła) do prawej osób lub przechowywania ich w lokalizacji udostępnionej, gdzie wiele zaufanych agentów mogą uzyskiwać do nich dostęp.

Tradycyjnego modelu udostępniania ma kilka wady:

* Włączanie dostępu do nowych aplikacji należy rozpowszechnić poświadczenia dla wszystkich użytkowników, które musi mieć dostęp.
* Każda aplikacja udostępnionego może wymagać własny unikatowy zestaw poświadczeń udostępnionych wymaganie od użytkowników do zapamiętania wiele zestawów poświadczeń. Jeśli użytkownik ma do zapamiętania wiele poświadczeń, ryzyka zwiększa ich ponowne sortowanie do rozwiązania ryzykowne. (na przykład zapisywać hasła).
* Nie można sprawdzić, kto ma dostęp do aplikacji.
* Nie można sprawdzić, kto ma *dostępne* aplikacji.
* Jeśli chcesz usunąć dostęp do aplikacji, należy zaktualizować poświadczenia i rozpowszechnić je do wszystkich osób, które muszą mieć dostęp do tej aplikacji.

## <a name="azure-active-directory-account-sharing"></a>Udostępnianie Azure konta usługi Active Directory
Usługa Azure AD zapewnia nowe podejście do przy użyciu udostępnionego konta, aby wyeliminować te wady.

Skonfigurowane przez administratora usługi Azure AD, aplikacji, które użytkownik może uzyskać dostęp za pomocą panelu dostępu i wybierając typ najlepiej rejestracji jednokrotnej nadaje się do tej aplikacji. Jeden z tych typów *opartego na hasłach jednokrotnego*, umożliwia usługi Azure AD, które działają jako rodzaj "brokerze" podczas procesu logowania dla danej aplikacji.

W drugi raz z swoje konta organizacyjne logowania użytkowników. To konto jest taka sama jak używane regularnie uzyskiwać dostęp do swojego pulpitu lub poczty e-mail. Mogą odnajdywać i tylko te aplikacje, które są przypisane do dostępu. Z udostępnionego konta lista aplikacji może zawierać dowolną liczbę poświadczeń udostępnionych. Użytkownik końcowy nie trzeba pamiętać lub Zapisz różne konta, które mogą używać.

Udostępnionego konta nie tylko zwiększyć nadzoru i poprawić użyteczność, zapewniają również ze względów bezpieczeństwa. Użytkownicy z uprawnieniami, aby użyć poświadczeń nie widzisz wspólne hasło, ale raczej uzyskać uprawnienia do używania hasło jako część przepływu zorkiestrowana uwierzytelniania. Ponadto niektóre aplikacje logowania jednokrotnego hasła zapewnienia możliwości za pomocą usługi Azure AD, aby okresowo przerzucania (aktualizacja) hasła. System używa dużych, złożonych haseł, która zwiększa bezpieczeństwo konta. Administrator może łatwo przydzielić lub odwołać dostęp do aplikacji, wie, kto ma dostęp do konta i kto ma dostęp do niego w przeszłości.

Usługi Azure AD obsługuje udostępnionego konta Enterprise Mobility Suite (EMS), Premium lub Basic licencjonowani użytkownicy, wszystkich typów hasła pojedynczego logowania w aplikacji. Można udostępniać konta dla każdego tysięcy wstępnie zintegrowanych aplikacji w galerii aplikacji i dodać własne uwierzytelniania hasła aplikacji z [aplikacji niestandardowych logowania jednokrotnego](active-directory-enterprise-apps-manage-sso.md).

Azure AD funkcje, które umożliwiają udostępnianie konta:

* [Hasło logowania jednokrotnego](active-directory-appssoaccess-whatis.md#password-based-single-sign-on)
* Hasło jednego logowania jednokrotnego agenta
* [Przypisanie do grupy](active-directory-accessmanagement-self-service-group-management.md)
* Niestandardowe hasło aplikacji
* [Raporty pulpitu nawigacyjnego użycia aplikacji](active-directory-passwords-get-insights.md)
* Portale dostępu użytkownika końcowego
* [Serwer proxy aplikacji](active-directory-application-proxy-get-started.md)
* [Usługi Active Directory Marketplace](https://azure.microsoft.com/marketplace/active-directory/all/)

## <a name="sharing-an-account"></a>Udostępnianie kont
Aby udostępnić konta przy użyciu usługi Azure AD, musisz:

* Dodawanie aplikacji [galerii aplikacji](https://azure.microsoft.com/marketplace/active-directory/) lub [aplikacji niestandardowych](http://blogs.technet.com/b/ad/archive/2015/06/17/bring-your-own-app-with-azure-ad-self-service-saml-configuration-gt-now-in-preview.aspx)
* Konfigurowanie aplikacji dla hasła pojedynczego logowania jednokrotnego (SSO)
* Użyj [przypisywania na podstawie grupy](active-directory-accessmanagement-group-saasapps.md) i wybrać opcję wprowadzenia poświadczeń udostępnionych
* Opcjonalnie: w niektórych aplikacjach, takich jak Facebook, Twitter i LinkedIn, należy włączyć opcję dla [usługi Azure AD automatycznego przerzucania hasła](http://blogs.technet.com/b/ad/archive/2015/02/20/azure-ad-automated-password-roll-over-for-facebook-twitter-and-linkedin-now-in-preview.aspx)

Można również ustawić udostępnionego konta bardziej bezpieczne z usługi Multi-Factor Authentication (MFA) (Dowiedz się więcej o [zabezpieczanie aplikacji z usługą Azure AD](../multi-factor-authentication/multi-factor-authentication-get-started.md)) i delegować możliwości zarządzania, kto ma dostęp do aplikacji przy użyciu [ Azure AD samoobsługi](active-directory-accessmanagement-self-service-group-management.md) grupy zarządzania.

## <a name="related-articles"></a>Pokrewne artykuły:
* [Indeks artykułów dotyczących zarządzania aplikacjami w usłudze Azure Active Directory](active-directory-apps-index.md)
* [Ochrona aplikacji przy użyciu dostępu warunkowego](active-directory-conditional-access-azure-portal.md)
* [Zarządzanie grupami samoobsługi/SSAA](active-directory-accessmanagement-self-service-group-management.md)

