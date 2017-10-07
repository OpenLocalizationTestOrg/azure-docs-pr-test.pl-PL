---
title: "aaaSharing kont za pomocą usługi Azure AD | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak Azure Active Directory umożliwia organizacjom toosecurely udostępnianie kont dla aplikacji lokalnych i usług w chmurze konsumenta."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: e2d77104-d978-46a3-bfea-03ffdf3b61e6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: 9f98bfa97a6c9ba1566d3f921c1b676d5f3c2a88
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="sharing-accounts-with-azure-ad"></a>Udostępnianie kont usługi Azure AD
## <a name="overview"></a>Omówienie
Czasami organizacje muszą toouse jednej nazwy użytkownika i hasło dla wielu osób. Ta sytuacja zwykle występuje w dwóch przypadkach:

* Podczas uzyskiwania dostępu do aplikacji, które wymagają Unikatowy identyfikator logowania i hasło dla każdego użytkownika, czy aplikacjami lokalnymi lub odbiorcy usług w chmurze (np. kont firmowych mediów społecznościowych).
* Podczas tworzenia środowiska wielu użytkowników. Może mieć pojedynczy konto lokalne, mającego podniesione uprawnienia i mogą być używane toodo core instalacji, Administracja i odzyskiwania działania (np. hello "globalny konta administratora lokalnego" dla konta głównego usługi Office 365 lub hello w usłudze Salesforce).

Tradycyjnie będzie można współużytkować tych kont przez dystrybucję hello poświadczeń (nazwy użytkownika i hasła) toohello prawo osób lub przechowywania ich w lokalizacji udostępnionej, gdzie wiele zaufanych agentów mogą uzyskiwać do nich dostęp.

tradycyjnego modelu udostępniania Hello ma kilka wady:

* Włączanie dostępu toonew aplikacji wymaga toodistribute tooeveryone poświadczenia, które wymagają dostępu.
* Każda aplikacja udostępnionego może wymagać własny unikatowy zestaw poświadczeń udostępnionych wymagające tooremember użytkowników wiele zestawów poświadczeń. Gdy użytkownicy mają tooremember wiele poświadczeń, ryzyka hello zwiększa ich powróci toorisky rozwiązania. (np. zapisanie hasła).
* Nie można sprawdzić, kto ma dostęp do aplikacji tooan.
* Nie można sprawdzić, kto ma *dostępne* aplikacji.
* Jeśli potrzebujesz tooremove dostępu tooan aplikacji hello tooupdate poświadczenia i ponownie przekazać je tooeveryone, który wymaga dostępu toothat aplikacji.

## <a name="azure-active-directory-account-sharing"></a>Udostępnianie Azure konta usługi Active Directory
Usługa Azure AD zapewnia nowe podejście toousing udostępnionego konta, które eliminuje te wady.

administrator usługi Azure AD Hello konfiguruje aplikacji, które użytkownik może uzyskać dostęp za pomocą hello panelu dostępu i wybierając typ hello rejestracji jednokrotnej najlepiej nadaje się do tej aplikacji. Jeden z tych typów *opartego na hasłach jednokrotnego*, umożliwia usługi Azure AD, które działają jako rodzaj "brokerze" procesie hello logowania dla danej aplikacji.

W drugi raz z swoje konta organizacyjne logowania użytkowników. Jest to hello tego samego konta, że regularnie korzystają z tooaccess pulpicie lub w wiadomości e-mail. Mogą odnajdywać i tylko te aplikacje, które są przypisane do dostępu. Z udostępnionego konta lista aplikacji może zawierać dowolną liczbę poświadczeń udostępnionych. użytkownik końcowy Hello nie wymagają tooremember lub Zapisz hello różnych kont, których może używać.

Udostępnionego konta nie tylko zwiększyć nadzoru i poprawić użyteczność, zapewniają również ze względów bezpieczeństwa. Użytkownicy z poświadczeniami hello toouse uprawnień nie będą widzieli hello wspólne hasło, ale raczej uzyskać uprawnienia toouse hello hasło jako część przepływu zorkiestrowana uwierzytelniania. Ponadto z niektórymi aplikacjami hasło logowania jednokrotnego, masz toohave opcji hello Azure AD okresowo hello przerzucania (aktualizacja) hasła przy użyciu dużych, złożonych haseł, zwiększenie hello konta zabezpieczeń. Hello administrator można łatwo udzielić lub odwołać dostęp do aplikacji tooan i także dowiedzieć się, kto ma dostęp do konta toohello i kto uzyskał do niego dostęp w przeszłości hello.

Usługi Azure AD obsługuje udostępnionego konta dla dowolnego Enterprise Mobility Suite (EMS), Premium lub podstawowa licencjonowani użytkownicy wszystkich typów jednego hasła logowania aplikacji. Można udostępniać konta dla każdego tysięcy wstępnie zintegrowanych aplikacji w galerii aplikacji hello i dodać własne uwierzytelniania hasła aplikacji z [aplikacji niestandardowych logowania jednokrotnego](active-directory-sso-integrate-saas-apps.md).

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
tooshare toouse usługi Azure AD konto należy do:

* Dodawanie aplikacji [galerii aplikacji](https://azure.microsoft.com/marketplace/active-directory/) lub [aplikacji niestandardowych](http://blogs.technet.com/b/ad/archive/2015/06/17/bring-your-own-app-with-azure-ad-self-service-saml-configuration-gt-now-in-preview.aspx)
* Konfigurowanie aplikacji hello hasła pojedynczego logowania jednokrotnego (SSO)
* Użyj [przypisywania na podstawie grupy](active-directory-accessmanagement-group-saasapps.md) i wybierz hello tooenter opcji poświadczeń udostępnionych
* Opcjonalnie: w niektórych aplikacjach, takich jak Facebook, Twitter i LinkedIn, można włączyć opcję hello [usługi Azure AD automatycznego przerzucania hasła](http://blogs.technet.com/b/ad/archive/2015/02/20/azure-ad-automated-password-roll-over-for-facebook-twitter-and-linkedin-now-in-preview.aspx)

Można również ustawić udostępnionego konta bardziej bezpieczne z usługi Multi-Factor Authentication (MFA) (Dowiedz się więcej o [zabezpieczanie aplikacji z usługą Azure AD](../multi-factor-authentication/multi-factor-authentication-get-started.md)) i delegować toomanage możliwości hello, kto ma dostęp do toohello aplikacji przy użyciu [Azure AD samoobsługi](active-directory-accessmanagement-self-service-group-management.md) grupy zarządzania.

## <a name="related-articles"></a>Pokrewne artykuły:
* [Indeks artykułów dotyczących zarządzania aplikacjami w usłudze Azure Active Directory](active-directory-apps-index.md)
* [Ochrona aplikacji przy użyciu dostępu warunkowego](active-directory-conditional-access.md)
* [Zarządzanie grupami samoobsługi/SSAA](active-directory-accessmanagement-self-service-group-management.md)

