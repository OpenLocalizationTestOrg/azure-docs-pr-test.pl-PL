---
title: "funkcje zabezpieczeń aaaAzure, które umożliwiają zarządzanie tożsamościami | Dokumentacja firmy Microsoft"
description: " Ten artykuł zawiera omówienie funkcji zabezpieczeń platformy Azure core hello, które ułatwiają zarządzanie tożsamościami. Pomocy firmy Microsoft tożsamościami i dostępem zarządzania rozwiązań IT ochronę tooapplications dostępu i zasobów na powitania firmowym centrum danych i w chmurze hello włączenie dodatkowe poziomy sprawdzania poprawności, takich jak uwierzytelnianie wieloskładnikowe i warunkowe zasady dostępu. "
services: security
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: TomSh
ms.assetid: 5aa0a7ac-8f18-4ede-92a1-ae0dfe585e28
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/09/2017
ms.author: terrylan
ms.openlocfilehash: f08e4f6cf2e48e455a16858b7fee08b53d5aa585
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-identity-management-security-overview"></a>Przegląd zabezpieczeń zarządzania tożsamość platformy Azure
Pomocy firmy Microsoft tożsamościami i dostępem zarządzania rozwiązań IT ochronę tooapplications dostępu i zasobów na powitania firmowym centrum danych i w chmurze hello włączenie dodatkowe poziomy sprawdzania poprawności, takich jak uwierzytelnianie wieloskładnikowe i warunkowe zasady dostępu. Monitorowania podejrzanych działań przez zaawansowane zabezpieczenia raportowania, inspekcji i alerty, pomaga ograniczyć potencjalne problemy. [Azure Active Directory Premium](../active-directory/active-directory-editions.md) zapewnia toothousands znak pojedynczego aplikacji w chmurze (SaaS) i uruchom lokalnie aplikacje tooweb dostępu.

Korzyści w zakresie zabezpieczeń dla usługi Azure Active Directory (AD) obejmują możliwość hello:

* Tworzenie i zarządzanie nimi jednej tożsamości dla każdego użytkownika w przedsiębiorstwie hybrydowego Synchronizacja użytkowników, grup i urządzeń
* Podaj dostępu rejestracji jednokrotnej tooyour aplikacji, w tym tysięcy wstępnie zintegrowanych aplikacji SaaS
* Włącz zabezpieczenia dostępu do aplikacji, wymuszając uwierzytelnianie wieloskładnikowe opartych na regułach, które zarówno lokalnie i aplikacji w chmurze
* Lokalne tooon bezpieczny dostęp zdalny należy sieci web aplikacji za pośrednictwem serwera Proxy aplikacji usługi Azure AD

Witaj celem tego artykułu jest tooprovide omówienie hello podstawowe zabezpieczeń platformy Azure funkcje, które ułatwiają zarządzanie tożsamościami. Firma Microsoft udostępnia również tooarticles łącza, które podać szczegóły dotyczące każdej funkcji, aby dowiedzieć się więcej.  

Witaj artykuł skupia się na powitania następujące możliwości zarządzania tożsamościami Azure rdzeni:

* Logowanie jednokrotne
* Zwrotny serwer proxy
* Uwierzytelnianie wieloskładnikowe
* Monitorowanie zabezpieczeń, alertów i raportów na podstawie learning maszyny
* Zarządzanie tożsamościami i dostępem klientów
* Rejestracja urządzenia
* Zarządzanie tożsamościami uprzywilejowanymi
* Ochrona tożsamości
* Hybrydowe Zarządzanie tożsamościami

## <a name="single-sign-on"></a>Logowanie jednokrotne
Rejestracji jednokrotnej (SSO) oznacza, że jest w stanie tooaccess wszystkich aplikacji hello i zasobów potrzebnych firm toodo, logując się tylko raz przy użyciu jednego konta użytkownika. Po zalogowaniu możesz uzyskać dostęp do wszystkich aplikacji hello należy nie jest wymagane tooauthenticate (na przykład wpisz hasło) po raz drugi.

W wielu organizacjach opierają się na oprogramowania jako aplikacje usługi (SaaS), takich jak Office 365, pole i Salesforce na produktywność użytkownika końcowego. W przeszłości tooindividually potrzebne personelu IT tworzenie i aktualizowanie kont użytkowników w każdej aplikacji SaaS, a użytkownicy mieli tooremember hasła dla każdej aplikacji SaaS.

Usługi Azure AD rozszerzenie lokalnych środowisk usługi Active Directory w chmurze hello włączenie toouse użytkowników ich podstawowego konta organizacyjnego toonot tylko logowania tootheir urządzeń przyłączonych do domeny i zasobów firmy, ale również wszystkich hello sieci web i aplikacji SaaS potrzebne do ich pracy.

Nie tylko użytkownicy bez toomanage wiele zestawów nazwy użytkowników i hasła, dostęp do aplikacji mogą być automatycznie udostępnione lub cofnąć elastycznie na podstawie grupy organizacyjne i ich stan jako pracownika. Usługi Azure AD wprowadzono zabezpieczeń i formantami ładu dostępu, które umożliwiają możesz toocentrally zarządzanie dostępem użytkowników do aplikacji SaaS.

Więcej informacji:

* [Omówienie logowania jednokrotnego](https://azure.microsoft.com/documentation/videos/overview-of-single-sign-on/)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](../active-directory/active-directory-appssoaccess-whatis.md)
* [Integrowanie usługi Azure Active Directory logowania jednokrotnego dla aplikacji SaaS](../active-directory/active-directory-sso-integrate-saas-apps.md)

## <a name="reverse-proxy"></a>Zwrotny serwer proxy
Serwera Proxy aplikacji usługi Azure AD umożliwia publikowanie aplikacji lokalnych, takich jak [SharePoint](https://support.office.com/article/What-is-SharePoint-97b915e6-651b-43b2-827d-fb25777f446f?ui=en-US&rs=en-US&ad=US) witryn, [aplikacji Outlook Web App](https://technet.microsoft.com/library/jj657718.aspx), i [IIS](http://www.iis.net/)— na podstawie aplikacji w sieci prywatnej i udostępnia toousers bezpieczny dostęp spoza sieci. Serwer Proxy aplikacji udostępnia dostępu zdalnego i rejestracji jednokrotnej (SSO) dla różnych typów lokalnych aplikacji sieci web z hello tysięcy aplikacji SaaS, które obsługuje usługę Azure AD. Pracownicy można rejestrować w aplikacjach tooyour z domu na ich własnych urządzeń i uwierzytelniania za pośrednictwem tego serwera proxy oparte na chmurze.

Więcej informacji:

* [Włączanie serwera Proxy aplikacji usługi Azure AD](../active-directory/active-directory-application-proxy-enable.md)
* [Publikowanie aplikacji przy użyciu serwera Proxy aplikacji usługi Azure AD](../active-directory/active-directory-application-proxy-publish.md)
* [Single-sign-on z serwerem Proxy aplikacji](../active-directory/active-directory-application-proxy-sso-using-kcd.md)
* [Praca z dostępu warunkowego](../active-directory/active-directory-application-proxy-conditional-access.md)

## <a name="multi-factor-authentication"></a>Uwierzytelnianie wieloskładnikowe
Usługa Azure Multi-Factor authentication (MFA) jest metoda uwierzytelniania, która wymaga użycia hello więcej niż jednej metody weryfikacji i dodaje kluczową drugą warstwę logowania toouser zabezpieczeń i transakcji. MFA ułatwia zabezpieczenie dostępu toodata i aplikacje spełniając zapotrzebowanie na prosty proces logowania. Zapewnia silne uwierzytelnianie za pomocą różnych opcji weryfikacji — połączenie telefoniczne, wiadomość tekstowa lub aplikacja mobilna weryfikacji lub powiadamiania o kodzie i innych firm tokenów OAuth.

Więcej informacji:

* [Multi-Factor Authentication](https://azure.microsoft.com/documentation/services/multi-factor-authentication/)
* [Co to jest usługa Multi-Factor Authentication platformy Azure?](../multi-factor-authentication/multi-factor-authentication.md)
* [Jak działa usługa Azure Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication-how-it-works.md)

## <a name="security-monitoring-alerts-and-machine-learning-based-reports"></a>Monitorowanie zabezpieczeń, alertów i raportów na podstawie learning maszyny
Monitorowanie zabezpieczeń i alertów i machine learning raportów na podstawie identyfikujące niespójne wzorce dostępu ułatwia ochronę firmy. Umożliwia dostęp do usługi Azure Active Directory i użycia raporty toogain widoczność hello integralności i bezpieczeństwa w katalogu organizacji. Dzięki tym informacjom administratora katalogu można lepiej określić, gdzie może znajdować się możliwe zagrożenia bezpieczeństwa, tak aby ich odpowiednio zaplanować toomitigate te zagrożenia.

W hello klasycznego portalu Azure raporty są podzielone na powitania następujące sposoby:

* Raporty anomalii — zawierają logowania czy znaleziono toobe nietypowe zdarzenia. Naszym celem jest toomake należy pamiętać o tych działań oraz pozwalające użytkownikowi toobe toomake możliwe określenie, czy jest podejrzane zdarzenia.
* Raporty aplikacji zintegrowanego — wgląd w sposób aplikacji w chmurze są używane w organizacji. Usługa Azure Active Directory oferuje integrację z tysiącami aplikacji w chmurze.
* Raporty o błędach — wskazują błędy, które mogą wystąpić podczas inicjowania obsługi administracyjnej kont tooexternal aplikacji.
* Raporty dotyczące użytkownika — wyświetlać urządzenia/symbol w dane o aktywności dla określonego użytkownika.
* Dzienniki aktywności — zawiera rekord wszystkich zdarzeń inspekcji w ramach hello ostatnich 24 godzinach, ostatnie 7 dni, lub ostatnich 30 dni i grupy działania zmiany oraz działania resetowania i rejestracji hasła.

Więcej informacji:

* [Wyświetlanie raportów dostępu i użycia](../active-directory/active-directory-view-access-usage-reports.md)
* [Wprowadzenie do korzystania z usługi Azure Active Directory raportowania](../active-directory/active-directory-reporting-getting-started.md)
* [Przewodnik po raportach usługi Azure Active Directory](../active-directory/active-directory-reporting-guide.md)

## <a name="consumer-identity-and-access-management"></a>Zarządzanie tożsamościami i dostępem klientów
Usługa Azure Active Directory B2C jest tożsamości wysokiej dostępności, globalnych, zarządzanie usługą w aplikacjach użytkownika która może obsłużyć toohundreds milionów tożsamości. Można ją łatwo integrować z platformami mobilnymi i platformami sieci Web. Użytkownicy mogą logować tooall aplikacji za pomocą środowiska można dostosować przy użyciu istniejących kont społecznościowych lub tworząc nowe poświadczenia.

W ciągu ostatnich hello deweloperów, którzy chciał toosign się i zalogować się w konsumentach napisanych w swoich aplikacjach, musieli napisać własny kod. I musieli korzystać z lokalnych baz danych lub systemów toostore nazwy użytkowników i hasła. Usługa Azure Active Directory B2C oferuje organizacji lepszą sposób toointegrate zarządzania tożsamością użytkowników do aplikacji za pomocą hello bezpiecznej, spełniającej standardy platformy i dużego zestawu rozszerzalnych zasad.

Gdy używasz usługi Azure Active Directory B2C użytkownicy mogą rejestrować dla aplikacji, przy użyciu istniejących kont społecznościowych (Facebook, Google, Amazon, LinkedIn) lub tworząc nowe poświadczenia (adres e-mail i hasło lub nazwa użytkownika i hasło).

Więcej informacji:

* [Co to jest Azure Active Directory B2C?](https://azure.microsoft.com/services/active-directory-b2c/)
* [Azure Active Directory B2C w wersji zapoznawczej: zarejestrować i logowanie użytkowników w twoich aplikacjach](../active-directory-b2c/active-directory-b2c-overview.md)
* [W wersji zapoznawczej usługi Azure Active Directory B2C: Typy aplikacji](../active-directory-b2c/active-directory-b2c-apps.md)

## <a name="device-registration"></a>Rejestracja urządzenia
Rejestracja urządzenia w usłudze Azure AD jest podstawą hello oparta na urządzeniach [dostępu warunkowego](../active-directory/active-directory-conditional-access-device-registration-overview.md) scenariuszy. Po zarejestrowaniu urządzenia rejestracji urządzeń usługi Azure Active Directory zapewnia hello urządzenia przy użyciu tożsamości, który jest używany tooauthenticate hello urządzenia po zalogowaniu użytkownika hello. urządzenie Hello uwierzytelniony i atrybuty hello hello urządzenia, można następnie tooenforce używane zasady dostępu warunkowego dla aplikacji, które znajdują się w chmurze hello i lokalnych.

W połączeniu z rozwiązania do zarządzania urządzeniami Przenośnymi urządzeniami przenośnymi, takie jak usługa Intune, dodatkowe informacje o urządzeniu hello są aktualizowane hello atrybuty urządzenia w usłudze Azure Active Directory. Dzięki temu można toocreate zasady dostępu warunkowego, które wymuszają dostęp z urządzeń toomeet standardy zabezpieczeń i zgodności.

Więcej informacji:

* [Wprowadzenie do rejestracji urządzeń usługi Azure Active Directory](../active-directory/active-directory-conditional-access-device-registration-overview.md)
* [Automatycznej rejestracji urządzeń z urządzeń dołączonych do domeny usługi Azure Active Directory dla systemu Windows](../active-directory/active-directory-conditional-access-automatic-device-registration.md)
* [Konfigurowanie automatycznej rejestracji systemu Windows przyłączone do domeny urządzenia z usługi Azure Active Directory](../active-directory/active-directory-conditional-access-automatic-device-registration-setup.md)

## <a name="privileged-identity-management"></a>Zarządzanie tożsamościami uprzywilejowanymi
Azure Active Directory (AD) Privileged Identity Management umożliwia zarządzanie, sterowanie i monitorowanie tożsamości uprzywilejowanych i tooresources dostępu w usłudze Azure AD, a także innych usług online firmy Microsoft, takich jak usługi Office 365 lub Microsoft Intune.

Czasami użytkownicy muszą toocarry operacje uprzywilejowane w zasobów platformy Azure lub usługi Office 365 lub innych aplikacji SaaS. Często oznacza to, organizacje mają toogive ich stałe uprzywilejowanego dostępu w usłudze Azure AD. Jest to zagrożenie bezpieczeństwa rosnącym zasobów hostowanych w chmurze, ponieważ organizacje wystarczająco nie można monitorować, co robią tych użytkowników, używając swoich uprawnień administratora. Ponadto w przypadku złamania zabezpieczeń konta użytkownika z dostępem uprzywilejowanym tego naruszenia co może mieć wpływ na ich ogólne bezpieczeństwo chmury. Azure AD Privileged Identity Management pomaga tooresolve to ryzyko.

Azure AD Privileged Identity Management umożliwia:

* Zobacz użytkowników, którzy są administratorami usługi Azure AD
* Włącz na żądanie "just in time" tooMicrosoft dostępu administracyjnego usług Online, takich jak Office 365 i Intune
* Uzyskaj raporty dotyczące historii dostępu administratora i zmian w przypisaniach administratora
* Uzyskiwanie alertów dotyczących ról uprzywilejowanych tooa dostępu

Więcej informacji:

* [Azure AD Privileged Identity Management](../active-directory/active-directory-privileged-identity-management-configure.md)
* [Role w usłudze Azure AD Privileged Identity Management](../active-directory/active-directory-privileged-identity-management-roles.md)
* [Azure AD Privileged Identity Management: Jak tooadd lub usunąć rolę użytkownika](../active-directory/active-directory-privileged-identity-management-how-to-add-role-to-user.md)

## <a name="identity-protection"></a>Ochrona tożsamości
Azure AD Identity Protection to usługa zabezpieczeń, która udostępnia skonsolidowany wgląd w zdarzenia o podwyższonym ryzyku i potencjalnych luk w zabezpieczeniach wpływających na tożsamości organizacji. Identity Protection wykorzystuje funkcje wykrywania anomalii istniejących Azure usługi Active Directory (dostępne za pośrednictwem usługi Azure AD nietypowe działanie raportów) i wprowadza nowe typy zdarzeń ryzyka, które można wykrywania anomalii w czasie rzeczywistym.

Więcej informacji:

* [Ochronę tożsamości usługi Azure Active Directory](../active-directory/active-directory-identityprotection.md)
* [Kanał 9: Usługi Azure AD i Pokaż tożsamości: Podgląd ochrony tożsamości](https://channel9.msdn.com/Series/Azure-AD-Identity/Azure-AD-and-Identity-Show-Identity-Protection-Preview)

## <a name="hybrid-identity-management"></a>Hybrydowe Zarządzanie tożsamościami
Firmy Microsoft podejście tooidentity obejmuje lokalnej i w chmurze hello, tworzenia tożsamością jednego użytkownika do uwierzytelniania i autoryzacji zasobów tooall, niezależnie od lokalizacji.

Więcej informacji:

* [Hybrydowe tożsamości oficjalny dokument](http://download.microsoft.com/download/D/B/A/DBA9E313-B833-48EE-998A-240AA799A8AB/Hybrid_Identity_White_Paper.pdf)
* [Azure Active Directory](https://azure.microsoft.com/documentation/services/active-directory/)
* [Blog zespołu usługi Active Directory](https://blogs.technet.microsoft.com/ad/)
