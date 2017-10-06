---
title: "aaaArticle indeksu do zarządzania aplikacjami w usłudze Azure Active Directory | Microsoft Azure"
description: "Dowiedz się, jak Data wygaśnięcia hello toocustomize certyfikaty federacyjnych i jak toorenew certyfikaty, które wkrótce wygaśnie."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 5321b8e4-2afa-4dfe-8d53-4add7abb5ec8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: markvi
ms.reviewer: asteen
ms.openlocfilehash: f8a584baa94dc50e279899074f50160978256559
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="article-index-for-application-management-in-azure-active-directory"></a>Indeks artykułów dotyczących zarządzania aplikacjami w usłudze Azure Active Directory
Ta strona zawiera pełną listę wszystkich dokumentów zapisywane o hello różnych funkcji związanych z aplikacji w usłudze Azure Active Directory (Azure AD).

Brak obszaru najważniejszych funkcji tooeach krótkie wprowadzenie, jak również wytyczne dotyczące tooread artykuły, które w zależności od tego, jakie informacje, których szukasz.

## <a name="overview-articles"></a>Artykuły — omówienie
Poniższe artykuły Hello są dobrym punkt wyjścia dla osób chcących po prostu krótki opis funkcji zarządzania aplikacjami w usłudze Azure AD.

| Przewodnik artykułu |  |
|:---:| --- |
| Wprowadzenie toohello aplikacji zarządzania problemy, które rozwiązuje usługa Azure AD |[Zarządzanie aplikacjami przy użyciu usługi Azure Active Directory (AD)](active-directory-enable-sso-scenario.md) |
| Omówienie hello różnych funkcji w usłudze Azure AD powiązane tooenabling logowania jednokrotnego, określające, kto ma dostęp do tooapps i jak użytkownicy uruchomią aplikacji |[Dostęp do aplikacji i logowanie jednokrotne w usłudze Azure Active Directory](active-directory-appssoaccess-whatis.md) |
| Obejrzyj hello inne czynności związane z integracji aplikacji usługi Azure AD |[Współdziałanie z aplikacjami usługi Azure Active Directory](active-directory-integrating-applications-getting-started.md)<br /><br />[Włączanie rejestracji jednokrotnej tooSaaS aplikacji](active-directory-sso-integrate-saas-apps.md)<br /><br />[Zarządzanie tooApps dostępu](active-directory-managing-access-to-apps.md) |
| Techniczne wyjaśnienie, w jaki aplikacje są reprezentowane w usłudze Azure AD |[Jak i dlaczego aplikacje są dodawane tooAzure AD](active-directory-how-applications-are-added.md) |

## <a name="troubleshooting-articles"></a>Rozwiązywanie problemów z artykułów
Ta sekcja zawiera szybki dostęp toorelevant przewodniki dotyczące rozwiązywania problemów. Więcej informacji na temat każdego obszaru funkcji można znaleźć na powitania pozostałej części tej strony.

| Obszar funkcji |  |
|:---:| --- |
| Federacyjne logowanie jednokrotne |[Rozwiązywanie problemów z systemem SAML logowania jednokrotnego](active-directory-saml-debugging.md) |
| Oparte na hasłach rejestracji jednokrotnej |[Rozwiązywanie problemów z hello rozszerzenia Panel dostępu dla programu Internet Explorer](active-directory-saas-ie-troubleshooting.md) |
| Serwer proxy aplikacji |[Przewodnik rozwiązywania problemów serwera Proxy aplikacji](active-directory-application-proxy-troubleshoot.md) |
| Logowanie jednokrotne między lokalnej usługi AD i Azure AD |[Rozwiązywanie problemów z synchronizacją haseł](connect/active-directory-aadconnectsync-implement-password-synchronization.md#troubleshoot-password-synchronization)<br /><br />[Rozwiązywanie problemów z zapisywaniem zwrotnym haseł](active-directory-passwords-troubleshoot.md#troubleshoot-password-writeback) |
| Członkostwa w grupach dynamiczne |[Rozwiązywanie problemów z członkostwa w grupach dynamiczne](active-directory-accessmanagement-troubleshooting.md) |

## <a name="single-sign-on-sso"></a>Logowanie jednokrotne
### <a name="federated-single-sign-on-sign-into-many-apps-using-one-identity"></a>Federacyjne logowanie jednokrotne: Logowania do wielu aplikacji przy użyciu jednej tożsamości
Logowanie jednokrotne umożliwia użytkownikom tooaccess różnych aplikacji i usług przy użyciu tylko jeden zestaw poświadczeń. Federacja znajduje się jedna metoda, za pomocą których można włączyć logowanie jednokrotne. Gdy użytkownicy próbują toosign do aplikacji federacyjnych, otrzyma organizacji przekierowanego tootheir oficjalnego strony logowania przez usługi Azure Active Directory i są następnie aplikacji przekierowanego toohello wstecz po pomyślnym uwierzytelnieniu.

| Przewodnik artykułu |  |
|:---:| --- |
| Wprowadzenie toofederation i inne typy logowania jednokrotnego |[Logowanie jednokrotne z usługą Azure AD](active-directory-appssoaccess-whatis.md) |
| Tysiące aplikacji SaaS, które są wstępnie zintegrowane z usługą Azure AD z uproszczony czynności konfiguracyjnych rejestracji jednokrotnej |[Wprowadzenie do korzystania z galerii aplikacji hello Azure AD](active-directory-appssoaccess-whatis.md#get-started-with-the-azure-ad-application-gallery)<br /><br />[Pełną listę wstępnie zintegrowanych aplikacji, które obsługują federacyjnego](http://aka.ms/aadfederatedapps)<br /><br />[Jak tooAdd aplikacji toohello galerii aplikacji Azure AD](active-directory-app-gallery-listing.md) |
| Więcej niż 150 samouczków aplikacji, w jaki sposób tooconfigure logowanie jednokrotne dla aplikacji takich jak [Salesforce](active-directory-saas-salesforce-tutorial.md), [ServiceNow](active-directory-saas-servicenow-tutorial.md), [usługi Google Apps](active-directory-saas-google-apps-tutorial.md), [produktu Workday](active-directory-saas-workday-tutorial.md)i o wiele więcej. |[Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md) |
| Jak toomanually Konfigurowanie i dostosowywanie jednej konfiguracji logowania jednokrotnego |[Jak tooConfigure tooApps federacyjne logowanie jednokrotne nie znajdują się w hello galerii aplikacji programu Azure Active Directory](active-directory-saas-custom-apps.md)<br /><br />[W jaki sposób tooCustomize oświadczenia wydane w hello tokenu SAML dla aplikacji Pre-Integrated](active-directory-saml-claims-customization.md) |
| Podręcznik rozwiązywania problemów dotyczących aplikacji federacyjnych, które używają protokołu SAML hello |[Rozwiązywanie problemów z systemem SAML logowania jednokrotnego](active-directory-saml-debugging.md) |
| Jak tooconfigure datę wygaśnięcia certyfikatu aplikacji, jak i toorenew certyfikatów |[Zarządzanie certyfikatami dla federacyjnego logowania jednokrotnego w usłudze Azure Active Directory](active-directory-sso-certs.md) |

Federacyjne logowanie jednokrotne jest dostępna dla wszystkich wersji programu Azure AD dla się tooten aplikacji dla poszczególnych użytkowników. [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/) obsługuje aplikacje nieograniczone. Jeśli Twoja organizacja ma [Azure AD podstawowa](https://azure.microsoft.com/pricing/details/active-directory/) lub [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/), wtedy będzie można [użycie grup aplikacji toofederated dostępu tooassign](#managing-access-to-applications).

### <a name="password-based-single-sign-on-account-sharing-and-sso-for-non-federated-apps"></a>Opartego na hasłach rejestracji jednokrotnej: udostępnianie kont i logowania jednokrotnego dla aplikacji niefederacyjnych
tooenable pojedynczego logowania jednokrotnego tooapplications które nie obsługują federacyjnych, funkcje zarządzania hasło oferty usługi Azure AD, które można bezpiecznie przechowywać haseł aplikacji tooSaaS i automatyczne logowanie użytkowników do tych aplikacji. Możesz łatwo rozpowszechnić poświadczenia dla nowo utworzonych kont i udostępniać konta team wiele osób. Użytkownicy nie muszą zawsze tooknow hello poświadczenia toohello konta, które są otrzymuje dostęp do.

| Przewodnik artykułu |  |
|:---:| --- |
| Wprowadzenie toohow opartego na hasłach logowania jednokrotnego działa i krótkie omówienie techniczne |[Oparte na hasłach logowanie jednokrotne z usługą Azure AD](active-directory-appssoaccess-whatis.md#password-based-single-sign-on) |
| Podsumowanie hello scenariusze związane z tooaccount udostępniania i jak te problemy można rozwiązać przez usługę Azure AD |[Udostępnianie kont usługi Azure AD](active-directory-sharing-accounts.md) |
| Automatyczna zmiana hasła hello w przypadku niektórych aplikacji w regularnych odstępach czasu |[Automatyczne Przerzucanie hasła (wersja zapoznawcza)](https://blogs.technet.microsoft.com/enterprisemobility/2015/02/20/azure-ad-automated-password-roll-over-for-facebook-twitter-and-linkedin-now-in-preview/) |
| Wdrażanie i rozwiązywanie problemów z przewodniki dotyczące wersji programu Internet Explorer hello hello rozszerzenie zarządzania hasła usługi Azure AD |[Jak tooDeploy hello rozszerzenia Panel dostępu dla programu Internet Explorer przy użyciu zasad grupy](active-directory-saas-ie-group-policy.md)<br /><br />[Rozwiązywanie problemów z hello rozszerzenia Panel dostępu dla programu Internet Explorer](active-directory-saas-ie-troubleshooting.md) |

Oparte na hasłach rejestracji jednokrotnej jest dostępna dla wszystkich wersji programu Azure AD dla się tooten aplikacji dla poszczególnych użytkowników. [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/) obsługuje aplikacje nieograniczone. Jeśli Twoja organizacja ma [Azure AD podstawowa](https://azure.microsoft.com/pricing/details/active-directory/) lub [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/), wtedy będzie można [użycie grupy tooapplications dostępu tooassign](#managing-access-to-applications). To hasło automatycznego przerzucania [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/) funkcji.

### <a name="app-proxy-single-sign-on-and-remote-access-tooon-premises-applications"></a>Serwer Proxy aplikacji: Aplikacje lokalne tooon jednego logowania i dostęp zdalny
Jeśli masz aplikacje w sieci prywatnej, wymagającym toobe dostępne dla użytkowników i urządzeń spoza sieci hello, można użyć serwera Proxy aplikacji usługi Azure AD tooenable bezpieczny, zdalny dostęp toothose aplikacji.

| Przewodnik artykułu |  |
|:---:| --- |
| Omówienie serwera Proxy aplikacji usługi Azure AD oraz sposób jej działania |[Zapewnianie bezpiecznego dostępu zdalnego do aplikacji lokalnych tooon](active-directory-application-proxy-get-started.md) |
| Samouczki dotyczące tooconfigure serwera Proxy aplikacji i w jaki sposób toopublish pierwszej aplikacji |[Jak tooSet się Proxy aplikacji Azure AD](active-directory-application-proxy-enable.md)<br /><br />[Jak zainstalować tooSilently hello łącznika serwera Proxy aplikacji](active-directory-application-proxy-silent-installation.md)<br /><br />[Jak tooPublish aplikacji przy użyciu serwera Proxy aplikacji](active-directory-application-proxy-publish.md)<br /><br />[Jak tooUse własną nazwę domeny](active-directory-application-proxy-custom-domains.md) |
| Jak tooenable pojedynczy logowania jednokrotnego i warunkowego dostępu do aplikacji opublikowane przy użyciu serwera Proxy aplikacji |[Single-sign-on z serwerem Proxy aplikacji](active-directory-application-proxy-sso-using-kcd.md)<br /><br />[Dostęp warunkowy i serwera Proxy aplikacji](active-directory-application-proxy-conditional-access.md) |
| Wskazówki dotyczące toouse serwera Proxy aplikacji dla hello następujące scenariusze |[Jak tooSupport natywnych aplikacji klienta](active-directory-application-proxy-native-client.md)<br /><br />[Jak tooSupport aplikacji obsługujących oświadczenia](active-directory-application-proxy-claims-aware-apps.md)<br /><br />[Jak aplikacje tooSupport opublikowane w odrębnych sieci i lokalizacje](active-directory-application-proxy-connectors.md) |
| Podręcznik rozwiązywania problemów dotyczących serwera Proxy aplikacji |[Przewodnik rozwiązywania problemów serwera Proxy aplikacji](active-directory-application-proxy-troubleshoot.md) |

Serwer Proxy aplikacji jest dostępna dla wszystkich wersji programu Azure AD dla się tooten aplikacji dla poszczególnych użytkowników. [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/) obsługuje aplikacje nieograniczone. Jeśli Twoja organizacja ma [Azure AD podstawowa](https://azure.microsoft.com/pricing/details/active-directory/) lub [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/), wtedy będzie można [użycie grupy tooapplications dostępu tooassign](#managing-access-to-applications).

Można go również zainteresowana [usług domenowych Azure AD](../active-directory-domain-services/active-directory-ds-overview.md), co pozwala toomigrate Twojego tooAzure aplikacji lokalnej spełniając nadal hello tożsamości wymaga tych aplikacji.

### <a name="enabling-single-sign-on-between-azure-ad-and-on-premises-ad"></a>Włączanie rejestracji jednokrotnej między usługą Azure AD i lokalnej usłudze AD
Jeśli organizacja ma Windows Server Active Directory lokalnie wraz z usługi Azure Active Directory w chmurze hello, a następnie prawdopodobnie będzie tooenable rejestracji jednokrotnej między tymi dwoma systemami. Azure AD Connect (narzędzie hello integrującą tych dwóch systemów razem) udostępnia wiele opcji konfigurowania rejestracji jednokrotnej: ustanowienia federacyjnej usług AD FS lub innego dostawcy federacyjnego lub włączanie synchronizacji haseł.

| Przewodnik artykułu |  |
|:---:| --- |
| Omówienie na powitania pojedynczego logowania jednokrotnego opcji oferowanych w Azure AD Connect, a także informacje na temat zarządzania środowisk hybrydowych |[Logowanie użytkownika na temat opcji w usłudze Azure AD Connect](active-directory-aadconnect-user-signin.md) |
| Ogólne wskazówki dotyczące zarządzania środowisk zarówno lokalnej usługi Active Directory i Azure Active Directory |[Zagadnienia dotyczące projektowania tożsamości hybrydowej usługi Azure AD](active-directory-hybrid-identity-design-considerations-overview.md)<br /><br />[Integrowanie tożsamości lokalnych z usługą Azure Active Directory](active-directory-aadconnect.md) |
| Wskazówki dotyczące używania tooenable synchronizacji haseł logowania jednokrotnego |[Implementowanie synchronizacji haseł w usłudze Azure AD Connect](active-directory-aadconnectsync-implement-password-synchronization.md)<br /><br />[Rozwiązywanie problemów z synchronizacją haseł](https://support.microsoft.com/en-us/kb/2855271) |
| Wskazówki dotyczące używania funkcji zapisywania zwrotnego haseł tooenable logowania jednokrotnego |[Wprowadzenie do zarządzania hasłami w usłudze Azure AD](active-directory-passwords-getting-started.md)<br /><br />[Rozwiązywanie problemów z zapisywaniem zwrotnym haseł](active-directory-passwords-troubleshoot.md#troubleshoot-password-writeback) |
| Wskazówki dotyczące używania tooenable dostawcy tożsamości innych firm logowania jednokrotnego |[Lista zgodne innych firm tożsamości dostawców czy można użyć tooEnable rejestracji jednokrotnej](https://aka.ms/ssoproviders) |
| Jak użytkownicy systemu Windows 10 można korzystać z hello zalet logowania jednokrotnego za pośrednictwem usługi Azure AD Join |[Rozszerzanie funkcji chmury tooWindows 10 urządzeń za pomocą usługi Azure Active Directory Join](active-directory-azureadjoin-overview.md) |

Azure AD Connect jest dostępna dla [wszystkie wersje usługi Azure Active Directory](https://azure.microsoft.com/pricing/details/active-directory/). Azure AD samoobsługowego resetowania hasła jest dostępna dla [Azure AD podstawowa](https://azure.microsoft.com/pricing/details/active-directory/) i [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/). Zapisywanie zwrotne haseł tooon — lokalny jest AD [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/) funkcji.

### <a name="conditional-access-enforce-additional-security-requirements-for-high-risk-apps"></a>Dostępu warunkowego: Dodatkowe wymagania dotyczące zabezpieczeń dla aplikacji o wysokim ryzyku wymuszenia
Po skonfigurowaniu aplikacji tooyour rejestracji jednokrotnej i zasobów można następnie dodatkowo zabezpieczyć aplikacji zawierających poufne dane przez wymuszenie specyficzne wymagania zabezpieczeń w każdej aplikacji toothat logowania. Na przykład można użyć toodemand usługi Azure AD, że wszystkie dostępu tooa danej aplikacji zawsze wymusić uwierzytelnianie wieloskładnikowe, niezależnie od tego, czy danej aplikacji innately obsługuje te funkcje. Inny typowy przykład dostępu warunkowego jest toorequire, że użytkownicy będą połączone toohello organizacji zaufanych sieci w kolejności tooaccess szczególnie poufnej aplikacji.

| Przewodnik artykułu |  |
|:---:| --- |
| Wprowadzenie toohello dostępu warunkowego możliwości oferowane przez usługi Azure AD, usługi Office 365 i Intune |[Zarządzanie ryzykiem przy użyciu dostępu warunkowego](active-directory-conditional-access.md) |
| Jak dostęp warunkowy tooenable hello następujące typy zasobów |[Dostęp warunkowy dla aplikacji SaaS](active-directory-conditional-access-azuread-connected-apps.md)<br /><br />[Dostęp warunkowy dla usługi Office 365](active-directory-conditional-access-device-policies.md)<br /><br />[Dostęp warunkowy do aplikacji lokalnych](active-directory-conditional-access.md)<br /><br />[Dostęp warunkowy do aplikacji lokalnych opublikowane za pośrednictwem serwera Proxy aplikacji usługi Azure AD](active-directory-application-proxy-conditional-access.md) |

| Jak tooregister urządzeń w usłudze Azure Active Directory w kolejności tooenable zasady dostępu warunkowego opartego na urządzeniach | [Omówienie rejestracji urządzeń usługi Azure Active Directory](active-directory-conditional-access-device-registration-overview.md)<br /><br />[Jak tooEnable automatycznej rejestracji urządzeń dla urządzeń z systemem Windows dołączonych do domeny](active-directory-conditional-access-automatic-device-registration.md)<br />— [Urządzeń kroki dla Windows 8.1](active-directory-conditional-access-automatic-device-registration-setup.md)<br />— [Urządzeń kroki dla systemu Windows 7](active-directory-conditional-access-automatic-device-registration-setup.md) |

| Jak toouse hello aplikacji Authenticator firmy Microsoft na potrzeby weryfikacji dwuetapowej | [Uwierzytelniania firmy Microsoft](../multi-factor-authentication/end-user/microsoft-authenticator-app-how-to.md) |

Dostęp warunkowy jest [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/) funkcji.

## <a name="apps--azure-ad"></a>Aplikacje i usługi Azure AD
### <a name="cloud-app-discovery-find-which-saas-apps-are-being-used-in-your-organization"></a>Usługa cloud App Discovery: Znajdowanie aplikacji SaaS, które są używane w organizacji
Usługa cloud App Discovery pomaga Dowiedz się, aplikacje SaaS, które są używane w całej organizacji hello działy IT. Go Mierz użycie aplikacji i popularność, którego nie można określić aplikacje, które będą korzystać hello najbardziej przed sterowane przez dział IT kontrolę i zostanie zintegrowanych z usługą Azure AD.

| Przewodnik artykułu |  |
|:---:| --- |
| Ogólne omówienie jak to działa |[Znajdowanie niezatwierdzona aplikacji w chmurze z usługi Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md) |
| Bardziej zgłębić temat do jej działania, z tooquestions odpowiedzi na prywatność |[Bezpieczeństwo i zagadnienia dotyczące ochrony prywatności](active-directory-cloudappdiscovery-security-and-privacy-considerations.md) |
| Często zadawane pytania |[Często zadawane pytania dotyczące Cloud App Discovery](http://social.technet.microsoft.com/wiki/contents/articles/24037.cloud-app-discovery-frequently-asked-questions.aspx) |
| Samouczki dotyczące wdrażania Cloud App Discovery |[Przewodnik dotyczący wdrażania zasad grupy](http://social.technet.microsoft.com/wiki/contents/articles/30965.cloud-app-discovery-group-policy-deployment-guide.aspx)<br /><br />[Przewodnik wdrażania programu System Center](http://social.technet.microsoft.com/wiki/contents/articles/30968.cloud-app-discovery-system-center-deployment-guide.aspx)<br /><br />[Instalowanie na serwerach Proxy z portami niestandardowe](active-directory-cloudappdiscovery-registry-settings-for-proxy-services.md) |
| Witaj zmiany w dzienniku agenta Cloud App Discovery toohello aktualizacji |[Dziennik zmian](http://social.technet.microsoft.com/wiki/contents/articles/24616.cloud-app-discovery-agent-changelog.aspx) |

Usługa cloud App Discovery jest [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/) funkcji.

### <a name="automatically-provision-and-deprovision-user-accounts-in-saas-apps"></a>Automatycznie udostępnić i anulowanie zastrzeżenia kont użytkowników w aplikacji SaaS
Zautomatyzować tworzenie hello, obsługi i usuwania tożsamości użytkowników w aplikacji SaaS, takich jak Dropbox, Salesforce, ServiceNow i inne. Zgodne i synchronizowanie istniejących tożsamości między usługą Azure AD i SaaS aplikacji i kontroli dostępu przez wyłączenie konta automatycznie, gdy użytkownicy opuszczają organizację hello.

| Przewodnik artykułu |  |
|:---:| --- |
| Więcej informacji na temat jej działania i odpowiedzi toocommon pytania |[Automatyzowanie Inicjowanie obsługi użytkowników & anulowania zastrzeżenia tooSaaS aplikacji](active-directory-saas-app-provisioning.md) |
| Skonfiguruj odwzorowania informacji między usługą Azure AD i aplikacji SaaS |[Dostosowywanie mapowań atrybutów](active-directory-saas-customizing-attribute-mappings.md)<br><br>[Tworzenie wyrażeń na potrzeby mapowań atrybutów](active-directory-saas-writing-expressions-for-attribute-mappings.md) |
| Jak tooenable automatycznego inicjowania obsługi administracyjnej aplikacji tooany, który obsługuje protokół SCIM hello |[Skonfiguruj automatyczne Inicjowanie obsługi użytkowników tooany SCIM-Enabled aplikacji](active-directory-scim-provisioning.md) |
| Jak tooreport na i rozwiązywać problemy dotyczące inicjowania obsługi użytkowników |[Raporty dotyczące użytkownika automatycznego inicjowania obsługi administracyjnej.](active-directory-saas-provisioning-reporting.md)<br><br>[Inicjowanie obsługi powiadomień](active-directory-saas-account-provisioning-notifications.md)<br><br>[Rozwiązywanie problemów z Inicjowanie obsługi użytkowników](active-directory-application-provisioning-content-map.md) |
| Limit, który pobiera elastycznie tooan aplikacji na podstawie ich wartości atrybutu |[Filtrami zakresów](active-directory-saas-scoping-filters.md) |

Inicjowanie obsługi użytkowników automatycznego jest dostępna dla wszystkich wersji programu Azure AD dla się tooten aplikacji dla poszczególnych użytkowników. [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/) obsługuje aplikacje nieograniczone. Jeśli Twoja organizacja ma [Azure AD podstawowa](https://azure.microsoft.com/pricing/details/active-directory/) lub [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/), a następnie możesz [Użyj toomanage grup użytkowników, którzy pobrania udostępniane](#managing-access-to-applications).

### <a name="building-applications-that-integrate-with-azure-ad"></a>Tworzenie aplikacji, które integrują się z usługą Azure AD
Jeśli Twoja organizacja jest tworzenie lub obsługa — biznesowych (LoB) aplikacji lub jeśli Deweloper aplikacji z klientami, którzy korzystają z usługi Azure Active Directory hello następujące samouczki zawierają informacje pomocne podczas integracji aplikacji z usługą Azure AD.

| Przewodnik artykułu |  |
|:---:| --- |
| Wskazówki dla informatyków i deweloperów aplikacji na integrowanie aplikacji z usługą Azure AD |[Witaj specjalistów IT w przewodniku opracowywanie aplikacji dla usługi Azure AD](active-directory-applications-guiding-developers-for-lob-applications.md)<br /><br />[Przewodnik dewelopera Hello usługi Azure Active Directory](active-directory-developers-guide.md) |
| Jak dodać dostawców tooapplication ich toohello aplikacji w galerii aplikacji Azure AD |[Wyświetlanie listy aplikacji hello galerii aplikacji programu Azure Active Directory](active-directory-app-gallery-listing.md) |
| Jak toomanage uzyskują dostęp do aplikacji toodeveloped przy użyciu usługi Azure Active Directory |[Jak tooEnable przypisanie użytkownika opracowanych aplikacji](active-directory-applications-guiding-developers-requiring-user-assignment.md)<br /><br />[Przypisywanie użytkowników tooyour aplikacji](active-directory-applications-guiding-developers-assigning-users.md)<br /><br />[Tooyour Przypisywanie grupy aplikacji](active-directory-applications-guiding-developers-assigning-groups.md) |

W przypadku tworzenia aplikacji dla użytkownika, może Cię zainteresować przy użyciu [usługi Azure Active Directory B2C](https://azure.microsoft.com/services/active-directory-b2c/) dzięki czemu nie trzeba toodevelop własne toomanage systemu tożsamości użytkowników. [Dowiedz się więcej](../active-directory-b2c/active-directory-b2c-overview.md).

## <a name="managing-access-tooapplications"></a>Zarządzanie tooApplications dostępu
### <a name="using-groups-and-self-service-toomanage-who-has-access-toowhich-apps"></a>Przy użyciu grup i toomanage samoobsługi, który ma dostęp do aplikacji toowhich
toohelp zarządzasz którzy powinni mieć dostęp do zasobów toowhich, Azure Active Directory umożliwia tooset przydziałów i uprawnień na dużą skalę przy użyciu grup. IT mogą wybrać tooenable funkcje samoobsługi, dzięki czemu użytkownicy mogą zażądać uprawnień po prostu, gdy są one wymagane.

| Przewodnik artykułu |  |
|:---:| --- |
| Omówienie funkcji zarządzania dostęp do usługi Azure AD |[Wprowadzenie tooManaging tooApps dostępu](active-directory-managing-access-to-apps.md)<br /><br />[Jak działa Zarządzanie dostępu w usłudze Azure AD](active-directory-manage-groups.md)<br /><br />[Jak tooUse grup tooManage tooSaaS dostępu do aplikacji](active-directory-accessmanagement-group-saasapps.md) |
| Włącz samoobsługowe zarządzanie aplikacji i grup |[Zarządzanie aplikacjami samoobsługi](active-directory-self-service-application-access.md)<br /><br />[Zarządzanie grupami samoobsługi](active-directory-accessmanagement-self-service-group-management.md) |
| Instrukcje dotyczące konfigurowania grup w usłudze Azure AD |[Jak tooCreate grup zabezpieczeń](active-directory-accessmanagement-manage-groups.md)<br /><br />[Jak tooDesignate właścicielami grupy](active-directory-accessmanagement-managing-group-owners.md)<br /><br />[Jak tooUse hello "wszyscy użytkownicy" grupy](active-directory-accessmanagement-dedicated-groups.md) |
| Użyj grup dynamicznych tooautomatically wypełnienia grupy przy użyciu reguł członkostwa na podstawie atrybutu |[Członkostwa w grupie dynamiczne: Zaawansowanych reguł](active-directory-accessmanagement-groups-with-advanced-rules.md)<br /><br />[Rozwiązywanie problemów z członkostwa w grupach dynamiczne](active-directory-accessmanagement-troubleshooting.md) |

Zarządzanie dostępem na podstawie grupy aplikacji jest dostępna dla [Azure AD podstawowa](https://azure.microsoft.com/pricing/details/active-directory/) i [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/). Samoobsługowe zarządzanie grupami, zarządzanie aplikacjami samoobsługi i grupami dynamicznymi [Azure AD Premium](https://azure.microsoft.com/pricing/details/active-directory/) funkcji.

### <a name="b2b-collaboration-enable-partner-access-tooapplications"></a>Współpraca B2B: Włącz tooapplications dostęp partnera
Jeśli firma współpracuje z innymi firmami, prawdopodobnie potrzebnych aplikacji firmowych dostępu tooyour toomanage partnera. Azure współpracy B2B Active Directory zapewnia prosty i bezpieczny sposób tooshare aplikacji z partnerami.

| Przewodnik artykułu |  |
|:---:| --- |
| Omówienie usługi Azure AD różnych funkcji, czy można uzyskać pomoc, takich jak zarządzanie użytkowników zewnętrznych partnerzy, klienci itd. |[Porównanie funkcji zarządzania w usłudze Azure AD tożsamości zewnętrznych](active-directory-b2b-compare-external-identities.md) |
| TooB2B wprowadzenie współpracy i sposób uruchamiania tooget |[Prosty bezpieczny, chmury partnera integracji z usługą Azure AD](active-directory-b2b-what-is-azure-ad-b2b.md)<br /><br />[Współpraca B2B usługi Azure Active Directory](active-directory-b2b-collaboration-overview.md) |
| Bardziej zgłębić temat do współpracy B2B usługi Azure AD i w jaki sposób toouse go |[Współpraca B2B: Jak to działa](active-directory-b2b-how-it-works.md)<br /><br />[Bieżące ograniczenia współpracy B2B usługi Azure AD](active-directory-b2b-current-limitations.md)<br /><br />[Szczegółowy przewodnik dotyczący użycia współpracy B2B usługi Azure AD](active-directory-b2b-detailed-walkthrough.md) |
| Odwołanie do artykułów z szczegółowe informacje techniczne dotyczące sposobu działania współpracy B2B usługi Azure AD |[Format pliku CSV do dodawania użytkowników z firm partnerskich](active-directory-b2b-references-csv-file-format.md)<br /><br />[Atrybuty użytkowników dotyczy współpracy B2B usługi Azure AD](active-directory-b2b-references-external-user-object-attribute-changes.md)<br /><br />[Format tokenu użytkownika dla użytkowników z firm partnerskich](active-directory-b2b-references-external-user-token-format.md) |

Współpraca B2B jest obecnie dostępna [wszystkie wersje usługi Azure Active Directory](https://azure.microsoft.com/pricing/details/active-directory/).

### <a name="access-panel-a-portal-for-accessing-apps-and-self-service-features"></a>Panel dostępu: Portal służący do uzyskiwania dostępu do aplikacji i funkcji samoobsługi
Witaj Panel dostępu usługi Azure AD jest, gdzie użytkownicy końcowi mogą uruchamianie ich aplikacji i hello Samoobsługowe funkcje dostępu, dzięki czemu toomanage ich aplikacji i członkostwa w grupach. Ponadto toohello panelu dostępu i inne opcje do uzyskiwania dostępu do aplikacji z włączoną obsługą rejestracji Jednokrotnej znajdują się w poniższej listy hello.

| Przewodnik artykułu |  |
|:---:| --- |
| Porównanie hello różne opcje dostępne podczas wdrażania aplikacji rejestracji jednokrotnej toousers |[Wdrażanie tooUsers zintegrowanych aplikacji usługi Azure AD](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users) |
| Omówienie hello panelu dostępu i jego przenośnych MyApps równoważne |[Wprowadzenie tooAccess Panel i MyApps](active-directory-saas-access-panel-introduction.md)<br />— [systemu iOS](https://itunes.apple.com/us/app/my-apps-azure-active-directory/id824048653?mt=8)<br />— [Systemu android](https://play.google.com/store/apps/details?id=com.microsoft.myapps) |
| Jak aplikacje tooaccess usługi Azure AD z hello witryny sieci Web usługi Office 365 |[Przy użyciu hello program uruchamiający aplikację pakietu Office 365](https://support.office.com/en-us/article/Meet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a) |
| Jak aplikacje tooaccess usługi Azure AD z hello aplikację mobilną Intune Managed Browser |[Intune Managed Browser](https://technet.microsoft.com/en-us/library/dn878029.aspx)<br />— [systemu iOS](https://itunes.apple.com/us/app/microsoft-intune-managed-browser/id943264951?mt=8)<br />— [Systemu android](https://play.google.com/store/apps/details?id=com.microsoft.intune.mam.managedbrowser) |
| Jak aplikacje tooaccess usługi Azure AD za pomocą linków bezpośrednich tooinitiate logowanie jednokrotne |[Pobieranie aplikacji tooYour linki bezpośrednie logowania jednokrotnego](active-directory-appssoaccess-whatis.md#direct-sign-on-links-for-federated-password-based-or-existing-apps) |

Panel dostępu jest dostępna dla [wszystkie wersje usługi Azure Active Directory](https://azure.microsoft.com/pricing/details/active-directory/).

### <a name="reports-easily-audit-app-access-changes-and-monitor-sign-ins-tooapps"></a>Raporty: Łatwo przeprowadzać inspekcję zmian dostępu do aplikacji i monitorowanie tooapps logowania
Azure Active Directory udostępnia kilka raportów i alerty toohelp monitorować tooapplications dostępu w organizacji. Możesz otrzymywać alerty w przypadku aplikacji tooyour nietypowe logowania, a można śledzić, kiedy i dlaczego aplikacja tooan dostępu użytkowników została zmieniona.

| Przewodnik artykułu |  |
|:---:| --- |
| Omówienie hello raportowania funkcji w usłudze Azure Active Directory |[Wprowadzenie do korzystania z raportów usługi Azure AD](active-directory-reporting-getting-started.md) |
| Jak toomonitor hello logowania i użycia aplikacji użytkowników |[Wyświetlanie dostępu oraz raporty użycia](active-directory-view-access-usage-reports.md) |
| Śledź zmiany toowho można uzyskać dostępu do konkretnej aplikacji |[Zdarzenia raportów inspekcji usługi Azure Active Directory](active-directory-reporting-audit-events.md) |
| Eksportowanie danych hello tych narzędzi tooyour preferowany raportów za pomocą hello interfejsu API raportowania |[Wprowadzenie do korzystania z hello Azure AD interfejsu API raportowania](active-directory-reporting-api-getting-started.md) |

Raporty, które są dołączone do różnych wersjach usługi Azure Active Directory, toosee [kliknij tutaj](active-directory-view-access-usage-reports.md).

## <a name="see-also"></a>Zobacz też
[Co to jest usługa Azure Active Directory?](active-directory-whatis.md)

[Azure Active Directory B2C](https://azure.microsoft.com/services/active-directory-b2c/)

[Usługi domenowe Azure Active Directory](https://azure.microsoft.com/services/active-directory-ds/)

[Uwierzytelnianie wieloskładnikowe platformy Azure](https://azure.microsoft.com/services/multi-factor-authentication/)
