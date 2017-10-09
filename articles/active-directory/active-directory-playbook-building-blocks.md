---
title: "aaaAzure usługi Active Directory dowód bloków konstrukcyjnych podręcznika dotyczącego koncepcji | Dokumentacja firmy Microsoft"
description: "Eksploruj i szybkie rozpoczęcie scenariusze Zarządzanie tożsamościami i dostępem"
services: active-directory
keywords: "Usługa Azure active directory, podręcznika dotyczącego koncepcji, aby zapewnić"
documentationcenter: 
author: dstefanMSFT
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: dstefan
ms.openlocfilehash: e54148330a123baf27d7e0f73469ff2a24c0efcd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-proof-of-concept-playbook-building-blocks"></a>Azure Active Directory dowód podręcznikowym koncepcji: bloki konstrukcyjne

## <a name="catalog-of-roles"></a>Wykaz ról

| Rola | Opis | Weryfikacja koncepcji odpowiedzialności |
| --- | --- | --- |
| **Architektura tożsamości / zespół deweloperów** | Zespół ten jest zwykle hello jedną opracowywania rozwiązań hello, implementuje prototypy, dyski zatwierdzenia i na koniec przekazuje toooperations | Podaj hello środowisk i hello te oszacowania hello różnych scenariuszy z punktu widzenia działu hello możliwości zarządzania |
| **Zespół operacyjny tożsamości lokalnych** | Zarządza hello inną tożsamość źródła lokalnego: lasy usługi Active Directory, katalogów LDAP HR systemów i dostawców tożsamości federacyjnych. | Zapewniają dostęp do zasobów lokalnych tooon potrzebne hello scenariusze weryfikacji koncepcji.<br/>One powinny być wykonywane jak najmniejszy|
| **Właściciele technicznego aplikacji** | Techniczne właścicieli hello różnych usług w chmurze, aplikacji i usług, które zostanie zintegrowana z usługą Azure AD | Szczegółowe informacje dotyczące aplikacji SaaS (potencjalnie wystąpień do testowania) |
| **Administrator globalny usługi Azure AD** | Zarządza konfiguracją hello Azure AD | Podaj poświadczenia usługi synchronizacji hello tooconfigure. Zazwyczaj hello tego samego zespołu jako architektura tożsamości podczas fazy weryfikacji koncepcji, ale niezależnie w fazie operacji hello|
| **Zespół bazy danych** | Właściciele hello infrastruktury bazy danych | Podaj środowiska tooSQL dostępu (AD FS lub Azure AD Connect) dla danego scenariusza przygotowań.<br/>One powinny być wykonywane jak najmniejszy |
| **Zespół sieci** | Właściciele hello infrastruktury sieciowej | Podaj wymagane prawa dostępu na poziomie sieci hello synchronizacji hello tooproperly serwerów hello dostęp do źródła danych i usług w chmurze (reguły zapory, otwierane porty, reguły IPSec itp.) |
| **Zespół ds. zabezpieczeń** | Definiuje hello strategii zabezpieczeń analizuje raporty dotyczące zabezpieczeń z różnych źródeł i za pośrednictwem jest zgodna w wynikach. | Zabezpieczenia docelowy scenariusze oceny |

## <a name="common-prerequisites-for-all-building-blocks"></a>Typowe wymagania wstępne dotyczące wszystkie bloki konstrukcyjne

Poniżej przedstawiono niektóre wymagań wstępnych dla dowolnego fazy weryfikacji Koncepcji z usługą Azure AD Premium.

| Wymagania wstępne | Zasoby |
| --- | --- |
| Zdefiniowane za pomocą ważnej subskrypcji platformy Azure dzierżawą platformy Azure AD | [Jak dzierżawcy tooget usługi Azure Active Directory](active-directory-howto-tenant.md)<br/>**Uwaga:** Jeśli istnieje już środowisko o licencji Azure AD Premium, możesz uzyskać zero zakończenia subskrypcji, przechodząc toohttps://aka.ms/accessaad <br/>Dowiedz się więcej, zobacz: https://blogs.technet.microsoft.com/enterprisemobility/2016/02/26/azure-ad-mailbag-azure-subscriptions-and-azure-ad-2/ i https://technet.microsoft.com/library/dn832618.aspx |
| Domen zdefiniowany i weryfikacji | [Dodaj tooAzure nazwy domeny niestandardowej usługi Active Directory](active-directory-domains-add-azure-portal.md)<br/>**Uwaga:** niektórych obciążeń, takich jak usługi Power BI można elastycznie dzierżawy usługi azure AD w obszarze hello obejmuje. toocheck, jeśli danej domeny jest skojarzona tooa dzierżawy, przejdź toohttps://login.microsoftonline.com/ {domain}/v2.0/.well-known/openid-configuration. Jeśli uzyskać pomyślnej odpowiedzi, a następnie domeny hello jest już przypisany tooa dzierżawy i przejęcia mogą być wymagane. Jeśli tak, aby uzyskać dalsze informacje kontakt z firmą Microsoft. Dowiedz się więcej o opcjach przejęcia hello w: [czym jest rejestracja samoobsługowa na platformie Azure?](active-directory-self-service-signup.md) |
| Azure AD Premium lub pakietu EMS włączone wersji próbnej | [Azure Active Directory Premium wolnego przez jeden miesiąc](https://azure.microsoft.com/trial/get-started-active-directory/) |
| Przypisano licencje usługi Azure AD Premium lub pakietu EMS tooPoC użytkowników | [Licencja użytkownika, jak i użytkowników w usłudze Azure Active Directory](active-directory-licensing-get-started-azure-portal.md) |
| Poświadczenia usługi Azure AD administratora globalnego | [Przypisywanie ról administratorów w usłudze Azure Active Directory](active-directory-assign-admin-roles-azure-portal.md) |
| Opcjonalny, lecz zdecydowanie zalecane: środowiska laboratoryjnego równoległych jako rezerwowe | [Prerequisites for Azure AD Connect](./connect/active-directory-aadconnect-prerequisites.md) (Wymagania wstępne programu Azure AD Connect) |

## <a name="directory-synchronization---password-hash-sync-phs---new-installation"></a>Katalog synchronizacji — synchronizacja skrótów haseł (PHS, który) — nowa instalacja

Przybliżona godzina tooComplete: dopiero po godzinie mniej niż 1000 użytkowników fazy weryfikacji koncepcji

### <a name="pre-requisites"></a>Wymagania wstępne

| Wymagania wstępne | Zasoby |
| --- | --- |
| TooRun serwera Azure AD Connect | [Prerequisites for Azure AD Connect](./connect/active-directory-aadconnect-prerequisites.md) (Wymagania wstępne programu Azure AD Connect) |
| Użytkownicy fazy weryfikacji Koncepcji, w hello docelowi tej samej domenie i część grupy zabezpieczeń i jednostki Organizacyjnej | [Niestandardowa instalacja programu Azure AD Connect](./connect/active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering) |
| Funkcje platformy Azure AD Connect wymagane do weryfikacji Koncepcji są identyfikowane hello | [Połączenie usługi Active Directory z usługą Azure Active Directory — Konfigurowanie synchronizacji funkcji](./connect/active-directory-aadconnect.md#configure-sync-features) |
| Potrzeby poświadczeń dla lokalnych i środowisk w chmurze  | [Azure AD Connect: Accounts and permissions](./connect/active-directory-aadconnect-accounts-permissions.md) (Azure AD Connect: konta i uprawnienia) |

### <a name="steps"></a>Kroki

| Krok | Zasoby |
| --- | --- |
| Pobieranie najnowszej wersji hello programu Azure AD Connect | [Pobierz Microsoft Azure Active Directory Connect](https://www.microsoft.com/download/details.aspx?id=47594) |
| Instalowanie usługi Azure AD Connect przy użyciu Najprostsza ścieżka hello: Express <br/>1. Filtruj czas cyklu synchronizacji hello toominimize toohello docelowej jednostki Organizacyjnej<br/>2. Wybierz docelowy zbiór użytkowników, grupy lokalne powitania.<br/>3. Wdrożenie funkcji hello wymagane przez hello innymi motywów fazy weryfikacji Koncepcji | [Azure AD Connect: Instalacja niestandardowa: domenę i jednostkę Organizacyjną filtrowania](./connect/active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering) <br/>[Azure AD Connect: Instalacja niestandardowa: grupy na podstawie filtrowania](./connect/active-directory-aadconnect-get-started-custom.md#sync-filtering-based-on-groups)<br/>[Azure AD Connect: Integrowanie tożsamości lokalnych z usługą Azure Active Directory: Konfigurowanie funkcji synchronizacji](./connect/active-directory-aadconnect.md#configure-sync-features) |
| Otwórz hello Azure AD Connect interfejsu użytkownika i znaleźć hello systemem profile ukończone (Import, synchronizacji i eksportowanie) | [Synchronizacja programu Azure AD Connect: Harmonogram](./connect/active-directory-aadconnectsync-feature-scheduler.md) |
| Otwórz hello [portalu zarządzania usługi Azure AD](https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/UserManagementMenuBlade/), przejdź do bloku "Wszyscy użytkownicy" toohello, Dodaj kolumnę "Źródłowego urzędu" i zobacz, który pojawia się użytkowników hello, prawidłowo oznaczone jako pochodzący od "Windows Server AD" | [Portal zarządzania usługi Azure AD](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview) |

### <a name="considerations"></a>Zagadnienia do rozważenia

1. Przyjrzyj się hello zagadnienia dotyczące zabezpieczeń z synchronizacji skrótów haseł [tutaj](./connect/active-directory-aadconnectsync-implement-password-synchronization.md).  Jeśli synchronizacja skrótów haseł dla użytkowników pilotażowych produkcyjnych ostatecznie nie jest opcją, rozważ hello następujących alternatyw:
   * Utwórz użytkowników testowych w hello domeny produkcyjnej. Upewnij się, że nie Synchronizuj innego konta
   * Przenieś tooan UAT środowiska
2.  Chcąc toopursue federacyjnych, warto toounderstand hello koszty skojarzone federacyjnych rozwiązania z dostawcy tożsamości lokalnych poza hello fazy weryfikacji Koncepcji i szukasz miary, która przed hello przynosi korzyści, możesz:
    * Jest ścieżka krytyczne hello więc toodesign wysokiej dostępności
    * Jest to usługa lokalnych należy toocapacity planu
    * Jest to usługa lokalnych należy toomonitor/Obsługa/poprawki

Dowiedz się więcej: [tożsamości opis Office 365 i Azure Active Directory - tożsamości federacyjnych](https://support.office.com/article/Understanding-Office-365-identity-and-Azure-Active-Directory-06a189e7-5ec6-4af2-94bf-a22ea225a7a9#bk_federated)

## <a name="branding"></a>Znakowania.

Przybliżona godzina tooComplete: 15 minut

### <a name="pre-requisites"></a>Wymagania wstępne

| Wymagania wstępne | Zasoby |
| --- | --- |
| Zasoby (obrazy logo, itp.); Dla wizualizacji najlepsze upewnij się, że zasoby hello ma hello zalecane rozmiary. | [Dodaj firmowe tooyour strony logowania w hello Azure Active Directory](active-directory-branding-custom-signon-azure-portal.md) |
| Opcjonalnie: Jeśli hello środowiska pod kątem serwera usług AD FS, dostęp motyw sieci web toocustomize serwera toohello | [Usługi AD FS logowania dostosowaniem wprowadzanym przez użytkowników](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/ad-fs-user-sign-in-customization) |
| Środowisko logowania użytkownika końcowego tooperform komputera klienta |  |
| Opcjonalnie: Urządzenia przenośne toovalidate środowisko |  |

### <a name="steps"></a>Kroki

| Krok | Zasoby |
| --- | --- |
| Przejdź tooAzure AD portalu zarządzania | [Portal zarządzania usługi Azure AD — logo firmy](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/LoginTenantBranding) |
| Przekaż zasoby hello do strony logowania hello (bohater logo, małego logo, etykiety itp.). Opcjonalnie, jeśli masz usługi AD FS, Dopasuj hello zasoby tego samego ze strony logowania usług AD FS | [Dodaj firmowe logowania tooyour i strony panelu dostępu: elementy dostosowywalne](active-directory-add-company-branding.md) |
| Poczekaj kilka minut dla hello zmiany toofully zaczęły obowiązywać. |  |
| Zaloguj się z hello toohttps://myapps.microsoft.com poświadczeń użytkownika fazy weryfikacji Koncepcji |  |
| Potwierdź hello wygląd i działanie w przeglądarce | [Dodaj firmowe logowania tooyour i strony panelu dostępu](active-directory-add-company-branding.md) |
| Opcjonalnie można potwierdzić hello wyglądu i działania na innych urządzeniach |  |

### <a name="considerations"></a>Zagadnienia do rozważenia

Jeśli po dostosowaniu hello hello starego wyglądu i działania opróżnić pamięć podręczną klienta przeglądarki hello i ponów próbę wykonania operacji hello.

## <a name="group-based-licensing"></a>Oparta na grupy licencji

Przybliżona godzina tooComplete: 10 minut

### <a name="pre-requisites"></a>Wymagania wstępne

| Wymagania wstępne | Zasoby |
| --- | --- |
| Wszyscy użytkownicy w fazie weryfikacji Koncepcji należą do grupy zabezpieczeń (chmurze lub lokalnie) | [Utwórz grupy i Dodaj elementy członkowskie w usłudze Azure Active Directory](active-directory-groups-create-azure-portal.md) |

### <a name="steps"></a>Kroki

| Krok | Zasoby |
| --- | --- |
| Przejdź do bloku toolicenses w portalu zarządzania usługi Azure AD | [Portal zarządzania usługi Azure AD: licencjonowania](https://portal.azure.com/#blade/Microsoft_AAD_IAM/LicensesMenuBlade/Products) |
| Przypisz grupę zabezpieczeń toohello licencji hello użytkownikom fazy weryfikacji Koncepcji. | [Przypisz licencje tooa grupę użytkowników w usłudze Azure Active Directory](active-directory-licensing-group-assignment-azure-portal.md) |

### <a name="considerations"></a>Zagadnienia do rozważenia

W przypadku problemów, przejdź zbyt[scenariuszy, ograniczenia i znane problemy z przy użyciu grup toomanage Licencjonowanie w usłudze Azure Active Directory](active-directory-licensing-group-advanced.md)

## <a name="saas-federated-sso-configuration"></a>Konfiguracja federacyjną rejestracją Jednokrotną w modelu SaaS

Przybliżona godzina tooComplete: 60 minut

### <a name="pre-requisites"></a>Wymagania wstępne

| Wymagania wstępne | Zasoby |
| --- | --- |
| Testowanie środowiska hello dostępne dla aplikacji SaaS. W tym przewodniku używamy usługi ServiceNow jako przykład.<br/>Zdecydowanie zaleca się toouse tarcia toominimize wystąpienie testu, na nawigowanie po istniejących jakości danych i mapowania. | Przejdź toohttps://developer.servicenow.com/app.do#! / home toostart hello proces pobierania wystąpienia testu |
| Konsola zarządzania usługi ServiceNow toohello dostępu administratora | [Samouczek: Integracji Azure Active Directory z usługi ServiceNow](active-directory-saas-servicenow-tutorial.md) |
| Docelowy zestaw aplikacji hello tooassign użytkowników. Grupę zabezpieczeń zawierającą użytkowników fazy weryfikacji koncepcji hello jest zalecane. <br/>Tworzenie grupy hello nie jest realne, następnie Przypisz użytkowników hello toodirectly toohello aplikacji dla hello fazy weryfikacji koncepcji | [Przypisywanie użytkownikowi lub grupie tooan przedsiębiorstwa aplikacji w usłudze Azure Active Directory](active-directory-coreapps-assign-user-azure-portal.md) |

### <a name="steps"></a>Kroki

| Krok | Zasoby |
| --- | --- |
| Udostępnianie hello podmiotami tooall Samouczek Microsoft Documentation  | [Samouczek: Integracji Azure Active Directory z usługi ServiceNow](active-directory-saas-servicenow-tutorial.md) |
| Ustaw spotkania pracy, a następnie wykonaj kroki samouczka hello z każdym aktora. | [Samouczek: Integracji Azure Active Directory z usługi ServiceNow](active-directory-saas-servicenow-tutorial.md) |
| Przypisz grupę toohello aplikacji hello objęci hello wymagania wstępne. Jeśli hello fazy weryfikacji Koncepcji ma dostęp warunkowy w zakresie hello, można ponownie, które później i dodać uwierzytelnianie wieloskładnikowe i podobne. <br/>Należy pamiętać, że będzie to zaczną działać hello procesu udostępniania (jeśli jest skonfigurowane) |  [Przypisywanie użytkownikowi lub grupie tooan przedsiębiorstwa aplikacji w usłudze Azure Active Directory](active-directory-coreapps-assign-user-azure-portal.md) <br/>[Utwórz grupy i Dodaj elementy członkowskie w usłudze Azure Active Directory](active-directory-groups-create-azure-portal.md) |
| Użyj tooadd portalu zarządzania usługi Azure AD aplikacji usługi ServiceNow z galerii| [Usługa Azure AD management Portal: aplikacje dla przedsiębiorstw](https://portal.azure.com/#blade/Microsoft_AAD_IAM/StartboardApplicationsMenuBlade/Overview) <br/>[What's new in zarządzania aplikacjami przedsiębiorstwa w usłudze Azure Active Directory](active-directory-enterprise-apps-whats-new-azure-portal.md) |
| W bloku aplikacji usługi ServiceNow "Logowanie jednokrotne" Włącz "na podstawie SAML logowania" |  |
| Wypełnij pola "Zaloguj się na adres URL" i "Identyfikator" z adresem URL usługi ServiceNow<br/>Pole wyboru hello zbyt "Uaktywnij nowy certyfikat"<br/>i Zapisz ustawienia |  |
| Otwieranie bloku "Konfigurowanie usługi ServiceNow" na powitania dołu tooview panelu hello dostosowane instrukcje dla Ciebie tooconfigure usługi ServiceNow |  |
| Postępuj zgodnie z instrukcjami tooconfigure usługi ServiceNow |  |
| W bloku aplikacji usługi ServiceNow "Aprowizowanie" Włącz "Automatyczny" Inicjowanie obsługi administracyjnej | [Zarządzanie kontami użytkowników, inicjowanie obsługi administracyjnej dla aplikacji przedsiębiorstwa w hello nowego portalu Azure](active-directory-enterprise-apps-manage-provisioning.md) |
| Poczekaj kilka minut, podczas udostępniania.  W hello czasu, można sprawdzić na powitania inicjowania obsługi raportów |  |
| Zaloguj się w toohttps://myapps.microsoft.com/ jako użytkownika testowego, które ma dostęp | [Co to jest hello panelu dostępu?](active-directory-saas-access-panel-introduction.md) |
| Kliknij Kafelek hello aplikacji hello, która została właśnie utworzona. Potwierdź dostęp |  |
| Opcjonalnie można sprawdzić raporty użycia aplikacji hello. Należy pamiętać, że istnieje pewnego opóźnienia przesyłania, więc należy toowait pewien czas toosee hello ruch w raportach hello. | [Raporty aktywności logowania w portalu usługi Azure Active Directory hello: użycie aplikacji zarządzanej](active-directory-reporting-activity-sign-ins.md#usage-of-managed-applications)<br/>[Azure Active Directory report retention policies](active-directory-reporting-retention.md) (Zasady przechowywania raportów w usłudze Azure Active Directory) |

### <a name="considerations"></a>Zagadnienia do rozważenia

1. Powyżej [samouczek](active-directory-saas-servicenow-tutorial.md) odwołuje się możliwości zarządzania tooold usługi Azure AD. Jednak fazy weryfikacji koncepcji jest obliczana na podstawie [szybki start](active-directory-enterprise-apps-whats-new-azure-portal.md#quick-start-get-going-with-your-new-application-right-away) wystąpić.
2. Jeśli aplikacja docelowa hello nie jest obecny w galerii hello, następnie służy "Przynieś własne aplikacji". Dowiedz się więcej: [What's new in zarządzania aplikacjami przedsiębiorstwa w usłudze Azure Active Directory: Dodawanie niestandardowych aplikacji w jednym miejscu](active-directory-enterprise-apps-whats-new-azure-portal.md#add-custom-applications-from-one-place)

## <a name="saas-password-sso-configuration"></a>Konfiguracja rejestracji Jednokrotnej SaaS hasła

Przybliżona godzina tooComplete: 15 minut

### <a name="pre-requisites"></a>Wymagania wstępne

| Wymagania wstępne | Zasoby |
| --- | --- |
| Środowisko testowe dla aplikacji SaaS. Przykładem hasło rejestracji Jednokrotnej jest HipChat i Twitter. Dla żadnej innej aplikacji należy hello dokładny adres URL strony hello z formularza html logowania. | [Na platformie Microsoft Azure Marketplace w usłudze Twitter](https://azuremarketplace.microsoft.com/marketplace/apps/aad.twitter)<br/>[HipChat na platformie Microsoft Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/aad.hipchat) |
| Konta dla aplikacji hello testowe. | [Załóż konto usługi Twitter](https://twitter.com/signup?lang=en)<br/>[Załóż bezpłatne konto: HipChat](https://www.hipchat.com/sign_up) |
| Docelowy zestaw aplikacji hello tooassign użytkowników. Zaleca się użytkowników hello zawiera grupy zabezpieczeń. | [Przypisywanie użytkownikowi lub grupie tooan przedsiębiorstwa aplikacji w usłudze Azure Active Directory](active-directory-coreapps-assign-user-azure-portal.md) |
| Administrator lokalny dostępu tooa komputera toodeploy hello rozszerzenia Panel dostępu dla programu Internet Explorer, Chrome lub Firefox | [Rozszerzenia Panel dostępu dla programu Internet Explorer](https://account.activedirectory.windowsazure.com/Applications/Installers/x64/Access%20Panel%20Extension.msi)<br/>[Rozszerzenia Panel dostępu dla programu Chrome](https://go.microsoft.com/fwLink/?LinkID=311859&clcid=0x409)<br/>[Rozszerzenia Panel dostępu dla przeglądarki Firefox](https://go.microsoft.com/fwLink/?LinkID=626998&clcid=0x409) |

### <a name="steps"></a>Kroki

| Krok | Zasoby |
| --- | --- |
| Zainstaluj rozszerzenie przeglądarki hello | [Rozszerzenia Panel dostępu dla programu Internet Explorer](https://account.activedirectory.windowsazure.com/Applications/Installers/x64/Access%20Panel%20Extension.msi)<br/>[Rozszerzenia Panel dostępu dla programu Chrome](https://go.microsoft.com/fwLink/?LinkID=311859&clcid=0x409)<br/>[Rozszerzenia Panel dostępu dla przeglądarki Firefox](https://go.microsoft.com/fwLink/?LinkID=626998&clcid=0x409) |
| Skonfigurować aplikację z galerii | [What's new in zarządzania aplikacjami przedsiębiorstwa w usłudze Azure Active Directory: galerii nowych i ulepszonych aplikacji hello](active-directory-enterprise-apps-whats-new-azure-portal.md#improvements-to-the-azure-active-directory-application-gallery) |
| Skonfiguruj hasło logowania jednokrotnego | [Zarządzanie logowanie jednokrotne dla aplikacji przedsiębiorstwa w hello nowego portalu Azure: opartego na hasłach logowania](active-directory-enterprise-apps-manage-sso.md#password-based-sign-on) |
| Przypisz grupę toohello aplikacji hello objęci hello wymagania wstępne | [Przypisywanie użytkownikowi lub grupie tooan przedsiębiorstwa aplikacji w usłudze Azure Active Directory](active-directory-coreapps-assign-user-azure-portal.md) |
| Zaloguj się w toohttps://myapps.microsoft.com/ jako użytkownika testowego, które ma dostęp |  |
| Kliknij Kafelek hello aplikacji hello, która została właśnie utworzona. | [Co to jest hello panelu dostępu?: opartego na hasłach logowania jednokrotnego bez obsługi tożsamości](active-directory-saas-access-panel-introduction.md#password-based-sso-without-identity-provisioning) |
| Podaj poświadczenia aplikacji hello | [Co to jest hello panelu dostępu?: opartego na hasłach logowania jednokrotnego bez obsługi tożsamości](active-directory-saas-access-panel-introduction.md#password-based-sso-without-identity-provisioning) |
| Zamknij hello przeglądarki i zaloguj się za hello powtarzania. Go hello użytkownik powinien zobaczyć bezproblemowy dostęp toohello aplikacji. |  |
| Opcjonalnie można sprawdzić raporty użycia aplikacji hello. Należy pamiętać, że istnieje pewnego opóźnienia przesyłania, więc należy toowait pewien czas toosee hello ruch w raportach hello. | [Raporty aktywności logowania w portalu usługi Azure Active Directory hello: użycie aplikacji zarządzanej](active-directory-reporting-activity-sign-ins.md#usage-of-managed-applications)<br/>[Azure Active Directory report retention policies](active-directory-reporting-retention.md) (Zasady przechowywania raportów w usłudze Azure Active Directory) |

### <a name="considerations"></a>Zagadnienia do rozważenia

Jeśli aplikacja docelowa hello nie jest obecny w galerii hello, następnie służy "Przynieś własne aplikacji". Dowiedz się więcej: [What's new in zarządzania aplikacjami przedsiębiorstwa w usłudze Azure Active Directory: Dodawanie niestandardowych aplikacji w jednym miejscu](active-directory-enterprise-apps-whats-new-azure-portal.md#add-custom-applications-from-one-place)

 Należy pamiętać hello następujące wymagania:
   * Aplikacja powinna mieć adres URL logowania znane
   * Strona logowania Hello powinien zawierać formularza HTML, z jedną więcej pól tekstowych, które rozszerzenia przeglądarki hello można automatyczne wypełnianie. W minimalnej hello powinien zawierać nazwę użytkownika i hasło.

## <a name="saas-shared-accounts-configuration"></a>SaaS kont konfiguracji udostępnionej

Przybliżona godzina tooComplete: 30 minut

### <a name="pre-requisites"></a>Wymagania wstępne

| Wymagania wstępne | Zasoby |
| --- | --- |
| Witaj listy aplikacji docelowych i hello dokładne logowania adresy URL wcześniejsze. Na przykład można użyć usługi Twitter. | [Na platformie Microsoft Azure Marketplace w usłudze Twitter](https://azuremarketplace.microsoft.com/marketplace/apps/aad.twitter)<br/>[Załóż konto usługi Twitter](https://twitter.com/signup?lang=en) |
| Udostępnione poświadczenia dla tej aplikacji SaaS. | [Udostępnianie kont za pomocą usługi Azure AD](active-directory-sharing-accounts.md)<br/>[Hasło przerzucania dla usługi Facebook, Twitter i LinkedIn dostępna w wersji zapoznawczej usługi azure AD automatycznego! -Enterprise Mobility and Security Blog] (https://blogs.technet.microsoft.com/enterprisemobility/2015/02/20/azure-ad-automated-password-roll-over-for-facebook-twitter-and-linkedin-now-in-preview/) |
| Poświadczenia dla co najmniej dwóch członków zespołu, którzy będą uzyskiwać dostęp do hello tego samego konta. Należy do grupy zabezpieczeń. | [Przypisywanie użytkownikowi lub grupie tooan przedsiębiorstwa aplikacji w usłudze Azure Active Directory](active-directory-coreapps-assign-user-azure-portal.md) |
| Administrator lokalny dostępu tooa komputera toodeploy hello rozszerzenia Panel dostępu dla programu Internet Explorer, Chrome lub Firefox | [Rozszerzenia Panel dostępu dla programu Internet Explorer](https://account.activedirectory.windowsazure.com/Applications/Installers/x64/Access%20Panel%20Extension.msi)<br/>[Rozszerzenia Panel dostępu dla programu Chrome](https://go.microsoft.com/fwLink/?LinkID=311859&clcid=0x409)<br/>[Rozszerzenia Panel dostępu dla przeglądarki Firefox](https://go.microsoft.com/fwLink/?LinkID=626998&clcid=0x409) |

### <a name="steps"></a>Kroki

| Krok | Zasoby |
| --- | --- |
| Zainstaluj rozszerzenie przeglądarki hello | [Rozszerzenia Panel dostępu dla programu Internet Explorer](https://account.activedirectory.windowsazure.com/Applications/Installers/x64/Access%20Panel%20Extension.msi)<br/>[Rozszerzenia Panel dostępu dla programu Chrome](https://go.microsoft.com/fwLink/?LinkID=311859&clcid=0x409)<br/>[Rozszerzenia Panel dostępu dla przeglądarki Firefox](https://go.microsoft.com/fwLink/?LinkID=626998&clcid=0x409) |
| Skonfigurować aplikację z galerii | [What's new in zarządzania aplikacjami przedsiębiorstwa w usłudze Azure Active Directory: galerii nowych i ulepszonych aplikacji hello](active-directory-enterprise-apps-whats-new-azure-portal.md#improvements-to-the-azure-active-directory-application-gallery) |
| Skonfiguruj hasło logowania jednokrotnego | [Zarządzanie logowanie jednokrotne dla aplikacji przedsiębiorstwa w hello nowego portalu Azure: opartego na hasłach logowania](active-directory-enterprise-apps-manage-sso.md#password-based-sign-on) |
| Przypisz grupę toohello aplikacji hello objęci hello wymagań wstępnych podczas przypisywania do nich poświadczeń | [Przypisywanie użytkownikowi lub grupie tooan przedsiębiorstwa aplikacji w usłudze Azure Active Directory](active-directory-coreapps-assign-user-azure-portal.md) |
| Zaloguj się jako inny użytkownik, aplikacja dostępu jako hello **sam udostępnionego konta.**  |  |
| Opcjonalnie można sprawdzić raporty użycia aplikacji hello. Należy pamiętać, że istnieje pewnego opóźnienia przesyłania, więc należy toowait pewien czas toosee hello ruch w raportach hello. | [Raporty aktywności logowania w portalu usługi Azure Active Directory hello: użycie aplikacji zarządzanej](active-directory-reporting-activity-sign-ins.md#usage-of-managed-applications)<br/>[Azure Active Directory report retention policies](active-directory-reporting-retention.md) (Zasady przechowywania raportów w usłudze Azure Active Directory) |


### <a name="considerations"></a>Zagadnienia do rozważenia

Jeśli aplikacja docelowa hello nie jest obecny w galerii hello, następnie służy "Przynieś własne aplikacji". Dowiedz się więcej: [What's new in zarządzania aplikacjami przedsiębiorstwa w usłudze Azure Active Directory: Dodawanie niestandardowych aplikacji w jednym miejscu](active-directory-enterprise-apps-whats-new-azure-portal.md#add-custom-applications-from-one-place)

 Należy pamiętać hello następujące wymagania:
   * Aplikacja powinna mieć adres URL logowania znane
   * Strona logowania Hello powinien zawierać formularza HTML, z jedną więcej pól tekstowych, które rozszerzenia przeglądarki hello można automatyczne wypełnianie. W minimalnej hello powinien zawierać nazwę użytkownika i hasło.

## <a name="app-proxy-configuration"></a>Konfiguracja serwera Proxy aplikacji

Przybliżona godzina tooComplete: 20 minut

### <a name="pre-requisites"></a>Wymagania wstępne

| Wymagania wstępne | Zasoby |
| --- | --- |
| Basic usługi Microsoft Azure AD lub subskrypcję usługi premium i katalog usługi Azure AD, dla którego jesteś administratorem globalnym | [Wersje usługi Azure Active Directory](active-directory-editions.md) |
| Aplikacja sieci web hostowanej lokalnego chcieliby tooconfigure dostępu zdalnego |  |
| Serwer z systemem Windows Server 2012 R2 lub Windows 8.1 lub nowszym, na którym można zainstalować hello łącznika serwera Proxy aplikacji | [Zrozumienie łączniki serwera Proxy aplikacji usługi Azure AD](application-proxy-understand-connectors.md) |
| Jeśli w ścieżce hello jest zapora, upewnij się, czy jest otwarty, powitalne tego łącznika można wprowadzać HTTPS (TCP) żąda toohello serwera Proxy aplikacji | [Włącz serwer Proxy aplikacji w portalu Azure hello: wymagania wstępne serwera Proxy aplikacji](active-directory-application-proxy-enable.md#application-proxy-prerequisites) |
| Jeśli Twoja organizacja korzysta z serwera proxy serwerów tooconnect toohello Internetu, wykonaj spojrzeć na blogu hello post pracy z istniejących lokalnych serwerów proxy dla szczegółowych informacji na temat tooconfigure je | [Praca z istniejącym lokalnych serwerów proxy](application-proxy-working-with-proxy-servers.md) |


### <a name="steps"></a>Kroki

| Krok | Zasoby |
| --- | --- |
| Zainstaluj łącznik na powitania serwera | [Włącz serwer Proxy aplikacji w portalu Azure hello: Instalowanie i rejestrowanie hello łącznika](active-directory-application-proxy-enable.md#install-and-register-a-connector) |
| Publikowanie aplikacji lokalnych hello w usłudze Azure AD jako aplikacja serwera Proxy aplikacji | [Publikowanie aplikacji przy użyciu serwera Proxy aplikacji usługi Azure AD](application-proxy-publish-azure-portal.md) |
| Przypisywanie użytkowników testowych | [Publikowanie aplikacji przy użyciu serwera Proxy aplikacji usługi Azure AD: Dodaj użytkownika testowego](application-proxy-publish-azure-portal.md#add-a-test-user) |
| Opcjonalnie można skonfigurować pojedynczy jednokrotnego dla użytkowników | [Podaj rejestracji jednokrotnej z serwera Proxy aplikacji usługi Azure AD](application-proxy-sso-azure-portal.md) |
| Przetestuj aplikację po zarejestrowaniu się w portalu tooMyApps jako przypisany użytkownik | https://myapps.microsoft.com |

### <a name="considerations"></a>Zagadnienia do rozważenia

1. Zaleca się umieszczanie łącznika hello w sieci firmowej, powodują zgłoszenia spowoduje wyświetlenie lepszą wydajność umieszczenie go w chmurze hello. Dowiedz się więcej: [zagadnienia dotyczące topologii sieci, używając serwera Proxy usługi Azure Active Directory aplikacji](application-proxy-network-topology-considerations.md)
2. Dalsze szczegóły zabezpieczeń i jak szczególnie bezpieczny dostęp zdalny zapewnia rozwiązanie utrzymując tylko połączeń wychodzących dla: [zagadnienia dotyczące zabezpieczeń do uzyskiwania dostępu do aplikacji zdalnie przy użyciu serwera Proxy aplikacji usługi Azure AD](application-proxy-security-considerations.md)

## <a name="generic-ldap-connector-configuration"></a>Ogólny łącznik LDAP konfiguracji

Przybliżona godzina tooComplete: 60 minut

> [!IMPORTANT]
> Jest to Konfiguracja zaawansowana wymagające masz pewną znajomość programu FIM/MIM. Jeśli używane w środowisku produkcyjnym, zaleca się pytania dotyczące tej konfiguracji przejść przez [pomocy technicznej Premium](https://support.microsoft.com/premier).

### <a name="pre-requisites"></a>Wymagania wstępne

| Wymagania wstępne | Zasoby |
| --- | --- |
| Azure AD Connect zainstalowane i skonfigurowane | Bloków konstrukcyjnych: [synchronizacja katalogów — synchronizacja skrótów haseł](#directory-synchronization--password-hash-sync-phs--new-installation) |
| Wymagania dotyczące spotkań wystąpienia ADLDS | [Ogólny łącznik LDAP informacje techniczne: omówienie hello ogólny łącznik LDAP](./connect/active-directory-aadconnectsync-connector-genericldap.md#overview-of-the-generic-ldap-connector) |
| Lista obciążeń, które użytkownicy korzystają z i atrybuty skojarzone z tych obciążeń. | [Synchronizacja programu Azure AD Connect: atrybuty synchronizowane tooAzure usługi Active Directory](./connect/active-directory-aadconnectsync-attributes-synchronized.md) |


### <a name="steps"></a>Kroki

| Krok | Zasoby |
| --- | --- |
| Dodaj ogólny łącznik LDAP | [Ogólny łącznik LDAP informacje techniczne: Tworzenie nowego łącznika](./connect/active-directory-aadconnectsync-connector-genericldap.md#create-a-new-connector) |
| Tworzenie profilów uruchamiania dla utworzonego łącznika (pełny import, import zmian, pełnej synchronizacji, w ramach synchronizacji przyrostowej, eksport) | [Tworzenie profilu uruchamiania agenta zarządzania](https://technet.microsoft.com/library/jj590219(v=ws.10).aspx)<br/> [Za pomocą łączników o hello Azure AD Connect synchronizacji programu Service Manager](./connect/active-directory-aadconnectsync-service-manager-ui-connectors.md)|
| Pełny import profilu uruchamiania i sprawdź, czy istnieją obiekty w przestrzeni łącznika | [Wyszukiwania dla obiekt miejsca łącznika](https://technet.microsoft.com/library/jj590287(v=ws.10).aspx)<br/>[Za pomocą łączników o hello Menedżera usługi synchronizacji Azure AD Connect: przestrzeni łącznika wyszukiwania](./connect/active-directory-aadconnectsync-service-manager-ui-connectors.md#search-connector-space) |
| Tworzenie reguły synchronizacji tak, aby obiekty w magazynie Metaverse mają atrybuty niezbędne dla obciążeń | [Synchronizacja programu Azure AD Connect: najlepsze rozwiązania dotyczące zmieniania konfiguracji domyślnej hello: zmienia tooSynchronization reguły](./connect/active-directory-aadconnectsync-best-practices-changing-default-configuration.md#changes-to-synchronization-rules)<br/>[Synchronizacja programu Azure AD Connect: opis Aprowizacją deklaratywną](./connect/active-directory-aadconnectsync-understanding-declarative-provisioning.md)<br/>[Synchronizacja programu Azure AD Connect: opis deklaratywne wyrażenia inicjowania obsługi administracyjnej](./connect/active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md) |
| Uruchom pełną synchronizację cyklu | [Synchronizacja programu Azure AD Connect: harmonogramu: uruchamianie hello harmonogramu](./connect/active-directory-aadconnectsync-feature-scheduler.md#start-the-scheduler) |
| W przypadku problemów czy Rozwiązywanie problemów | [Rozwiązywanie problemów z obiektu, który nie jest synchronizowanie tooAzure AD](./connect/active-directory-aadconnectsync-troubleshoot-object-not-syncing.md) |
| Sprawdź, czy użytkownik LDAP można logowania i dostęp do aplikacji hello | https://myapps.microsoft.com |

### <a name="considerations"></a>Zagadnienia do rozważenia

> [!IMPORTANT]
> Jest to Konfiguracja zaawansowana wymagające masz pewną znajomość programu FIM/MIM. Jeśli używane w środowisku produkcyjnym, zaleca się pytania dotyczące tej konfiguracji przejść przez [pomocy technicznej Premium](https://support.microsoft.com/premier).

## <a name="groups---delegated-ownership"></a>Grupy - delegować prawa własności

Przybliżona godzina tooComplete: 10 minut

### <a name="pre-requisites"></a>Wymagania wstępne

| Wymagania wstępne | Zasoby |
| --- | --- |
| Aplikacja SaaS (federacyjnej usługi logowania jednokrotnego lub hasło logowania jednokrotnego) został już skonfigurowany | Bloków konstrukcyjnych: [SaaS Federacyjna usługa rejestracji Jednokrotnej w konfiguracji](#saas-federated-sso-configuration) |
| Określono grupy chmury, przypisany dostęp do aplikacji toohello w #1 | Bloków konstrukcyjnych: [SaaS Federacyjna usługa rejestracji Jednokrotnej w konfiguracji](#saas-federated-sso-configuration) <br/>[Utwórz grupy i Dodaj elementy członkowskie w usłudze Azure Active Directory](active-directory-groups-create-azure-portal.md) |
| Poświadczenia dla właściciela grupy hello są dostępne | [Zarządzanie tooresources dostępu za pomocą grup usługi Azure Active Directory](active-directory-manage-groups.md) |
| Wykryto poświadczenia hello informacji procesu roboczego uzyskiwaniu dostępu do hello aplikacji | [Co to jest hello panelu dostępu?](active-directory-saas-access-panel-introduction.md) |


### <a name="steps"></a>Kroki

| Krok | Zasoby |
| --- | --- |
| Identyfikator grupy hello, któremu udzielono dostępu toohello aplikacji i skonfigurować właściciela hello podanej grupy| [Zarządzaj ustawieniami hello grupy w usłudze Azure Active Directory](active-directory-groups-settings-azure-portal.md) |
| Zaloguj się jako właściciel grupy hello, zobacz hello członkostwa w grupie w grupach na karcie panelu dostępu | [Strony Zarządzanie grupami w usłudze Active Directory systemu Azure](https://account.activedirectory.windowsazure.com/r/#/groups) |
| Dodaj hello Pracownik przetwarzający informacje mają tootest |  |
| Zaloguj się jako pracownik przetwarzający informacje hello, upewnij się, że Kafelek hello jest dostępna | [Co to jest hello panelu dostępu?](active-directory-saas-access-panel-introduction.md) |

### <a name="considerations"></a>Zagadnienia do rozważenia

Aplikacja hello ma inicjowania obsługi administracyjnej włączone, może być konieczne toowait za kilka minut dla hello udostępniania toocomplete przed uzyskaniem dostępu do aplikacji hello jako hello Pracownik przetwarzający informacje.

## <a name="saas-and-identity-lifecycle"></a>SaaS i cyklem życia tożsamości

### <a name="pre-requisites"></a>Wymagania wstępne

| Wymagania wstępne | Zasoby |
| --- | --- |
| Aplikacja SaaS (federacyjnej usługi logowania jednokrotnego lub hasło logowania jednokrotnego) został już skonfigurowany | Bloków konstrukcyjnych: [SaaS Federacyjna usługa rejestracji Jednokrotnej w konfiguracji](#saas-federated-sso-configuration) |
| Określono grupy chmury, przypisany dostęp do aplikacji toohello w #1 | Bloków konstrukcyjnych: [SaaS Federacyjna usługa rejestracji Jednokrotnej w konfiguracji](#saas-federated-sso-configuration) <br/>[Utwórz grupy i Dodaj elementy członkowskie w usłudze Azure Active Directory](active-directory-groups-create-azure-portal.md) |
| Wykryto poświadczenia hello informacji procesu roboczego uzyskiwaniu dostępu do hello aplikacji | [Co to jest hello panelu dostępu?](active-directory-saas-access-panel-introduction.md) |


### <a name="steps"></a>Kroki

| Krok | Zasoby |
| --- | --- |
| Usuń użytkownika hello z aplikacji hello grupy hello jest przypisany zbyt| [Zarządzanie członkostwami grup użytkowników w dzierżawie usługi Azure Active Directory](active-directory-groups-members-azure-portal.md) |
| Poczekaj kilka minut, aż anulowanie obsługi. | [Automatyczne inicjowanie obsługi użytkowników aplikacji SaaS w usłudze Azure AD: jak działa automatycznego inicjowania obsługi administracyjnej?](active-directory-saas-app-provisioning.md#how-does-automated-provisioning-work) |
| Na sesję przeglądarki oddzielne zalogować się jako hello informacji procesu roboczego toomy aplikacje portalu i upewnij się, brak tego kafelka | http://myapps.microsoft.com |


### <a name="considerations"></a>Zagadnienia do rozważenia

Ekstrapolować tooleavers scenariusz weryfikacji koncepcji hello i/lub urlopu scenariuszy. Jeśli użytkownik hello pobiera wyłączony w lokalnej usłudze AD lub usunięty, nie będzie już toolog sposób w toohello aplikacji SaaS.

## <a name="self-service-access-tooapplication-management"></a>Samodzielnie tooApplication dostępu do usługi zarządzania

Przybliżona godzina tooComplete: 10 minut

### <a name="pre-requisites"></a>Wymagania wstępne

| Wymagania wstępne | Zasoby |
| --- | --- |
| Identyfikowanie użytkowników fazy weryfikacji Koncepcji, żądających toohello uzyskiwać dostęp do aplikacji, w ramach grupy zabezpieczeń hello | Bloków konstrukcyjnych: [SaaS Federacyjna usługa rejestracji Jednokrotnej w konfiguracji](#saas-federated-sso-configuration) |
| Wdrożona aplikacja docelowa | Bloków konstrukcyjnych: [SaaS Federacyjna usługa rejestracji Jednokrotnej w konfiguracji](#saas-federated-sso-configuration) |

### <a name="steps"></a>Kroki

| Krok | Zasoby |
| --- | --- |
| Przejdź do bloku aplikacji tooEnterprise w portalu zarządzania usługi Azure AD | [Portalu zarządzania usługi Azure AD: Aplikacje dla przedsiębiorstw](https://portal.azure.com/#blade/Microsoft_AAD_IAM/StartboardApplicationsMenuBlade/AllApps/menuId/) |
| Skonfiguruj aplikację z wstępne z samoobsługi | [What's new in zarządzania aplikacjami przedsiębiorstwa w usłudze Azure Active Directory: Konfigurowanie dostępu do aplikacji Sklep internetowy](active-directory-enterprise-apps-whats-new-azure-portal.md#configure-self-service-application-access) |
| Zaloguj się jako hello informacji procesu roboczego toomy aplikacje portalu | http://myapps.microsoft.com |
| Zwróć uwagę, "+ Dodaj aplikację" przycisk na op hello strony. Przy użyciu jego tooget dostępu toohello aplikacji |  |

### <a name="considerations"></a>Zagadnienia do rozważenia

Wybrany aplikacji Hello może być inicjowania obsługi wymagań, więc będzie natychmiast toohello aplikacji może spowodować błędy. Jeśli wybrana aplikacja hello obsługę z usługą azure ad i jest skonfigurowana, tej opcji można użyć jako okazji tooshow hello całego przepływu pracy tooend zakończenia. Zobacz hello blokiem [SaaS Federacyjna usługa rejestracji Jednokrotnej w konfiguracji](#saas-federated-sso-configuration) dla dalszego zalecenia

## <a name="self-service-password-reset"></a>Samodzielne resetowanie haseł

Przybliżona godzina tooComplete: 15 minut

### <a name="pre-requisites"></a>Wymagania wstępne

| Wymagania wstępne | Zasoby |
| --- | --- |
| Włącz zarządzanie samoobsługi hasła w dzierżawie. | [Azure Active Directory resetowania hasła dla administratorów IT](active-directory-passwords.md) |
| Włącz hasła toomanage zapisu haseł z lokalnej. Uwaga wymaga określonej usługi Azure AD Connect wersji | [Wymagania wstępne dotyczące funkcji zapisywania zwrotnego haseł](active-directory-passwords-writeback.md) |
| Zidentyfikuj użytkowników fazy weryfikacji koncepcji hello, które będą korzystać z tej funkcji i upewnij się, że są oni członkami grupy zabezpieczeń. Hello użytkownicy muszą mieć możliwość hello pokazy toofully z systemem innym niż administratorzy | [Dostosowanie: Zarządzanie hasłami AD platformy Azure: resetowanie toopassword ograniczenia dostępu](active-directory-passwords-writeback.md) |


### <a name="steps"></a>Kroki

| Krok | Zasoby |
| --- | --- |
| Przejdź tooAzure AD Management Portal: resetowania hasła | [Portalu zarządzania usługi Azure AD: Resetowanie hasła](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/PasswordReset) |
| Określa zasady resetowania hasła hello. Do celów weryfikacji Koncepcji można użyć połączenia telefonicznego i Q & A. Zalecane jest wymagane na logowania do panelu tooaccess toobe rejestracji tooenable |  |
| Wyloguj się i zaloguj się jako pracownik przetwarzający informacje |  |
| Podaj dane samoobsługowego resetowania hasła hello zgodnie z konfiguracją na krok 2 | http://aka.MS/ssprsetup |
| Zamknij hello przeglądarki |  |
| Zacznij od nowa proces logowania hello jako hello Pracownik przetwarzający informacje używane w kroku 4 |  |
| Resetowanie hasła hello | [Zaktualizuj własnego hasła: resetowania hasła](active-directory-passwords-update-your-own-password.md) |
| Spróbuj zalogować się przy użyciu Twoje nowe hasło tooAzure AD, a także tooon lokalnych zasobów |  |

### <a name="considerations"></a>Zagadnienia do rozważenia

1. Jeśli uaktualnianie hello Azure AD Connect będzie tarcia toocause, rozważ użycie go przed kontach w chmurze lub była pokaz oddzielne środowisku
2. Administratorzy Hello mają inne zasady i przy użyciu Witaj, Administratorze hasło do konta tooreset hello może skażenia hello fazy weryfikacji koncepcji i dezorientację. Upewnij się, że używasz operacje resetowania hello tootest zwykłego użytkownika konta


## <a name="azure-multi-factor-authentication-with-phone-calls"></a>Uwierzytelnianie wieloskładnikowe platformy Azure z połączeń telefonicznych

Przybliżona godzina tooComplete: 10 minut

### <a name="pre-requisites"></a>Wymagania wstępne

| Wymagania wstępne | Zasoby |
| --- | --- |
| Identyfikowanie użytkowników fazy weryfikacji Koncepcji, które będą korzystać z usługi MFA  |  |
| Telefon z dobrym odbioru dla żądania usługi MFA  | [Co to jest usługa Multi-Factor Authentication platformy Azure?](../multi-factor-authentication/multi-factor-authentication.md) |

### <a name="steps"></a>Kroki

| Krok | Zasoby |
| --- | --- |
| Przejdź do zbyt bloku "Użytkownicy i grupy" w portalu zarządzania usługi Azure AD | [Portalu zarządzania Azure AD: Użytkownicy i grupy](https://portal.azure.com/#blade/Microsoft_AAD_IAM/UserManagementMenuBlade/Overview/menuId/) |
| Wybierz blok "Wszyscy użytkownicy" |  |
| W hello górnym pasku, wybierz przycisk "Usługi Multi-Factor Authentication" | Bezpośredni adres URL do portalu usługi Azure MFA: https://aka.ms/mfaportal |
| W ustawieniach "Użytkownika" hello Wybierz użytkowników, aby zapewnić hello i włączyć je do usługi MFA | [Stany użytkowników w usłudze Azure Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication-get-started-user-states.md) |
| Zaloguj się jako użytkownik fazy weryfikacji koncepcji hello i przechodzenia przez proces hello dowód  |  |

### <a name="considerations"></a>Zagadnienia do rozważenia

1. Witaj fazy weryfikacji koncepcji czynnościach w ramach tego bloku konstrukcyjnego jawne ustawienie usługi MFA dla użytkownika na wszystkich identyfikatorów logowania. Brak innych narzędzi, takich jak dostęp warunkowy i ochronę tożsamości, które stosują usługę MFA na więcej określonych scenariuszach. Są to coś tooconsider przy przechodzeniu tooproduction fazy weryfikacji Koncepcji.
2. kroki weryfikacji koncepcji Hello w tym bloku konstrukcyjnego jawnie korzystają z połączeń telefonicznych jako hello metody MFA expedience. Korzystanie z fazy weryfikacji Koncepcji tooproduction, zaleca się przy użyciu aplikacji, takich jak hello [Microsoft Authenticator](../multi-factor-authentication/end-user/microsoft-authenticator-app-how-to.md) jako Twoje czynnika, jeśli to możliwe.
Dowiedz się więcej: [projekt NIST Special Publication 800-63B](https://pages.nist.gov/800-63-3/sp800-63b.html)

## <a name="mfa-conditional-access-for-saas-applications"></a>Dostęp warunkowy usługi MFA dla aplikacji SaaS

Przybliżona godzina tooComplete: 10 minut

### <a name="pre-requisites"></a>Wymagania wstępne

| Wymagania wstępne | Zasoby |
| --- | --- |
| Zidentyfikuj fazy weryfikacji koncepcji użytkowników tootarget hello zasad. Te użytkownicy powinni być w zasadach dostępu warunkowego hello tooscope grupy zabezpieczeń | [Konfiguracja federacyjną rejestracją Jednokrotną w modelu SaaS](#saas-federated-sso-configuration) |
| Aplikacja SaaS został już skonfigurowany |  |
| Aby zapewnić użytkownikom są już przypisane toohello aplikacji |  |
| Dostępne są poświadczenia toohello fazy weryfikacji Koncepcji użytkownika |  |
| Aby Zapewnić użytkownik jest zarejestrowany w usłudze MFA. Za pomocą telefonu z dobrym odbioru | http://aka.MS/ssprsetup |
| Urządzenia w sieci wewnętrznej hello. Adres IP skonfigurowany w zakresie wewnętrznym adresem hello | Znajdowanie adresu ip: https://www.bing.com/search?q=what%27s+my+ip |
| Urządzenia w sieci zewnętrznej hello (może to być telefon przy użyciu hello operator sieci komórkowej) |  |

### <a name="steps"></a>Kroki

| Krok | Zasoby |
| --- | --- |
| Przejdź tooAzure AD Management Portal: bloku dostępu warunkowego | [Portalu zarządzania usługi Azure AD: Warunkowy dostęp](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConditionalAccessBlade/Policies) |
| Tworzenie zasad dostępu warunkowego:<br/>-Użytkownicy fazy weryfikacji koncepcji docelowych w obszarze "Użytkownicy i grupy"<br/>— Aplikacja fazy weryfikacji koncepcji docelowa w obszarze "Aplikacje w chmurze"<br/>-Target wszystkich lokalizacji z wyjątkiem tych zaufanych "Warunkach" -> "W lokalizacji" **Uwaga:** listę zaufanych adresów IP są konfigurowane w [Portal usługi MFA](https://account.activedirectory.windowsazure.com/UserManagement/MfaSettings.aspx)<br/>-Wymusić uwierzytelnianie wieloskładnikowe w obszarze "Grant" | [Rozpoczynanie pracy z dostępu warunkowego w usłudze Azure Active Directory: kroki konfiguracji zasad](active-directory-conditional-access-azure-portal-get-started.md#policy-configuration-steps) |
| Dostęp do aplikacji z wewnątrz sieci firmowej | [Rozpoczynanie pracy z dostępu warunkowego w usłudze Azure Active Directory: testowanie hello zasad](active-directory-conditional-access-azure-portal-get-started.md#testing-the-policy) |
| Dostęp do aplikacji w sieci publicznej | [Rozpoczynanie pracy z dostępu warunkowego w usłudze Azure Active Directory: testowanie hello zasad](active-directory-conditional-access-azure-portal-get-started.md#testing-the-policy) |

### <a name="considerations"></a>Zagadnienia do rozważenia

Jeśli używasz federacyjnych, można użyć hello toocommunicate dostawcy tożsamości (IdP) lokalne powitania wewnętrznej/zewnętrznej stanu sieci firmowej z oświadczeniami. Można użyć tej metody bez konieczności toomanage hello lista adresów IP, które mogłyby być tooassess złożonych i zarządzanie w dużych organizacjach. W tej konfiguracji należy konta dla scenariusza "siecią roaming" hello (zalogowanie się użytkownika z sieci wewnętrznej hello oraz w trakcie przełączniki zalogowany na przykład w kawiarni) i upewnij się, że rozumiesz konsekwencje hello. Dowiedz się więcej: [zabezpieczanie zasobów w chmurze Azure Multi-Factor Authentication i usług AD FS: zaufanych adresów IP dla użytkowników federacyjnych](../multi-factor-authentication/multi-factor-authentication-get-started-adfs-cloud.md#trusted-ips-for-federated-users)

## <a name="privileged-identity-management-pim"></a>Zarządzanie tożsamościami uprzywilejowanymi (PIM)

Przybliżona godzina tooComplete: 15 minut

### <a name="pre-requisites"></a>Wymagania wstępne

| Wymagania wstępne | Zasoby |
| --- | --- |
| Zidentyfikuj hello Administrator globalny, który będzie częścią hello fazy weryfikacji Koncepcji PIM | [Rozpoczynanie korzystania z usługi Azure AD Privileged Identity Management](active-directory-privileged-identity-management-getting-started.md) |
| Zidentyfikuj hello Administrator globalny, który ma zostać hello Administrator zabezpieczeń | [Rozpoczynanie korzystania z usługi Azure AD Privileged Identity Management](active-directory-privileged-identity-management-getting-started.md)<br/> [Różne role administracyjne w usłudze Azure Active Directory PIM](active-directory-privileged-identity-management-roles.md) |
| Opcjonalnie: Upewnij się, jeśli hello Administratorzy globalni mają e-mail dostępu tooexercise powiadomienia e-mail w PIM | [Co to jest usługa Azure AD Privileged Identity Management?: Konfigurowanie ustawień aktywacji roli hello](active-directory-privileged-identity-management-configure.md#configure-the-role-activation-settings)


### <a name="steps"></a>Kroki

| Krok | Zasoby |
| --- | --- |
| Toohttps://portal.azure.com logowania jako administrator globalny (GA) i ładowania początkowego hello PIM bloku. Hello Administrator globalny, który wykonuje ten krok jest obsługiwany jako hello administratora zabezpieczeń.  Umożliwia wywołanie tego aktora GA1 | [Za pomocą Kreatora zabezpieczeń hello w usłudze Azure AD Privileged Identity Management](active-directory-privileged-identity-management-security-wizard.md) |
| Zidentyfikuj hello administratora globalnego i przenieść je z tooeligible trwałych. Powinno to być oddzielne administratora z hello używany w kroku 1 dla uzyskania przejrzystości. Umożliwia wywołanie tego aktora GA2 | [Azure AD Privileged Identity Management: Jak tooadd lub usunąć rolę użytkownika](active-directory-privileged-identity-management-how-to-add-role-to-user.md)<br/>[Co to jest usługa Azure AD Privileged Identity Management?: Konfigurowanie ustawień aktywacji roli hello](active-directory-privileged-identity-management-configure.md#configure-the-role-activation-settings)  |
| Teraz Zaloguj się jako GA2 toohttps://portal.azure.com i spróbuj zmienić "Ustawienia użytkownika". Zwróć uwagę, że niektóre opcje są wygaszone. | |
| Na nowej karcie w hello tej samej sesji zgodnie z kroku nr 3, przejdź teraz toohttps://portal.azure.com i dodać hello PIM bloku toohello w pulpicie nawigacyjnym. | [Jak tooactivate lub dezaktywować role w programie Azure AD Privileged Identity Management: Dodawanie aplikacji Privileged Identity Management hello](active-directory-privileged-identity-management-how-to-activate-role.md#add-the-privileged-identity-management-application) |
| Rola administratora globalnego toohello aktywacji żądania | [Jak tooactivate lub dezaktywować role w programie Azure AD Privileged Identity Management: aktywować rolę](active-directory-privileged-identity-management-how-to-activate-role.md#activate-a-role) |
| Należy pamiętać, że GA2 nigdy nie zarejestrowała się w usłudze MFA, rejestracji dla usługi Azure MFA będzie to konieczne |  |
| Przejdź wstecz karta toohello w kroku 3 i kliknij przycisk Odśwież hello w przeglądarce hello. Należy pamiętać, że masz teraz dostęp toochange "Ustawienia użytkownika" | |
| Opcjonalnie Jeśli Twoje Administratorzy globalni mają włączone poczty e-mail, można sprawdzić GA1 i GA2 w skrzynce odbiorczej i wyświetlone powiadomienie hello roli hello aktywowane |  |
| 8 Sprawdź hello Historia inspekcji i sprawdź, że hello raport tooconfirm hello podniesienie GA2 jest widoczny. | [Co to jest usługa Azure AD Privileged Identity Management?: Przejrzyj działania roli](active-directory-privileged-identity-management-configure.md#review-role-activity) |

### <a name="considerations"></a>Zagadnienia do rozważenia

Ta funkcja jest częścią usługi Azure AD Premium P2 i/lub EMS E5

## <a name="discovering-risk-events"></a>Wykrywanie zdarzenia ryzyka

Przybliżona godzina tooComplete: 20 minut

### <a name="pre-requisites"></a>Wymagania wstępne

| Wymagania wstępne | Zasoby |
| --- | --- |
| Urządzenia z przeglądarką Tor pobrane i zainstalowane | [Pobierz Tor przeglądarki](https://www.torproject.org/projects/torbrowser.html.en#downloads) |
| TooPOC użytkownika toodo hello logowania | [Azure podręcznikowym ochronę tożsamości w usłudze Active Directory](active-directory-identityprotection-playbook.md) |

### <a name="steps"></a>Kroki

| Krok | Zasoby |
| --- | --- |
| Otwórz tor przeglądarki | [Pobierz Tor przeglądarki](https://www.torproject.org/projects/torbrowser.html.en#downloads) |
| Zaloguj się za toohttps://myapps.microsoft.com z hello fazy weryfikacji Koncepcji konta użytkownika | [Azure Active Directory Identity Protection podręcznika dotyczącego: Symulowanie zdarzeń o podwyższonym ryzyku](active-directory-identityprotection-playbook.md#simulating-risk-events) |
| Zaczekaj 5-7 minut |  |
| Zaloguj się jako administrator globalny toohttps://portal.azure.com i otwarcie bloku Identity Protection hello | https://aka.MS/aadipgetstarted |
| Otwórz hello ryzyka zdarzenia bloku. Powinien zostać wyświetlony w obszarze "Logowania z anonimowych adresów IP"  | [Azure Active Directory Identity Protection podręcznika dotyczącego: Symulowanie zdarzeń o podwyższonym ryzyku](active-directory-identityprotection-playbook.md#simulating-risk-events) |

### <a name="considerations"></a>Zagadnienia do rozważenia

Ta funkcja jest częścią usługi Azure AD Premium P2 i/lub EMS E5

## <a name="deploying-sign-in-risk-policies"></a>Wdrażanie zasad logowania ryzyka

Przybliżona godzina tooComplete: 10 minut

### <a name="pre-requisites"></a>Wymagania wstępne

| Wymagania wstępne | Zasoby |
| --- | --- |
| Urządzenia z przeglądarką Tor pobrane i zainstalowane | [Pobierz Tor przeglądarki](https://www.torproject.org/projects/torbrowser.html.en#downloads) |
| Dostęp jako dziennik weryfikacji Koncepcji hello toodo użytkownika do testowania |  |
| Aby Zapewnić użytkownik jest zarejestrowany za pomocą usługi MFA. Upewnij się, że toouse telefonu z dobrym odbioru | Bloków konstrukcyjnych: [uwierzytelnianie wieloskładnikowe platformy Azure z połączeń telefonicznych](#azure-multi-factor-authentication-with-phone-calls) |


### <a name="steps"></a>Kroki

| Krok | Zasoby |
| --- | --- |
| Zaloguj się jako administrator globalny toohttps://portal.azure.com i otwórz hello bloku Identity Protection | https://aka.MS/aadipgetstarted |
| Włącz zasady logowania ryzyko w następujący sposób:<br/>-Przypisane do: fazy weryfikacji Koncepcji użytkownika<br/>— Warunki: Logowania ryzyka średnia lub nowszej (logowania z anonimowych lokalizacji jest traktowany jako poziom ryzyka średnia)<br/>-Formanty: Wymagają usługi MFA | [Azure Active Directory Identity Protection podręcznika dotyczącego: ryzyka logowania](active-directory-identityprotection-playbook.md#sign-in-risk) |
| Otwórz tor przeglądarki | [Pobierz Tor przeglądarki](https://www.torproject.org/projects/torbrowser.html.en#downloads) |
| Zaloguj się za toohttps://myapps.microsoft.com z hello fazy weryfikacji koncepcji konta użytkownika |  |
| Powiadomienie hello żądanie uwierzytelniania MFA | [Logowanie napotyka przy użyciu usługi Azure AD Identity Protection: ryzykowne odzyskiwania logowania](active-directory-identityprotection-flows.md#risky-sign-in-recovery)

### <a name="considerations"></a>Zagadnienia do rozważenia

Ta funkcja jest częścią usługi Azure AD Premium P2 i/lub EMS E5. toolearn można znaleźć więcej informacji na temat zdarzeń o podwyższonym ryzyku: [zdarzenia o podwyższonym ryzyku usługi Azure Active Directory](active-directory-reporting-risk-events.md)

## <a name="configuring-certificate-based-authentication"></a>Konfigurowanie uwierzytelniania opartego na certyfikatach

Przybliżona godzina toocomplete: 20 minut

### <a name="pre-requisites"></a>Wymagania wstępne

| Wymagania wstępne | Zasoby |
| --- | --- |
| Urządzenia z certyfikatu użytkownika udostępniane (z systemem Windows, iOS lub Android) z infrastruktury kluczy publicznych przedsiębiorstwa | [Wdrażanie certyfikatów użytkowników](https://msdn.microsoft.com/library/cc770857.aspx) |
| Sfederowane domenowych Azure AD przy użyciu usług AD FS | [Program Azure AD Connect a federacja](./connect/active-directory-aadconnectfed-whatis.md)<br/>[Usługi certyfikatów Active Directory — omówienie](https://technet.microsoft.com/library/hh831740.aspx)|
| Dla urządzeń z systemem iOS mieć zainstalowanej aplikacji Microsoft Authenticator | [Wprowadzenie do aplikacji Microsoft Authenticator hello](../multi-factor-authentication/end-user/microsoft-authenticator-app-how-to.md) |

### <a name="steps"></a>Kroki

| Krok | Zasoby |
| --- | --- |
| Włączyć "Uwierzytelnianie certyfikatu" w usługach AD FS | [Konfigurowanie zasad uwierzytelniania: tooconfigure uwierzytelniania podstawowego globalnie w systemie Windows Server 2012 R2](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/configure-authentication-policies#to-configure-primary-authentication-globally-in-windows-server-2012-r2) |
| Opcjonalnie: Włącz uwierzytelnianie certyfikatu w usłudze Azure AD dla klientów programu Exchange Active Sync | [Wprowadzenie do uwierzytelniania opartego na certyfikacie w usłudze Azure Active Directory](active-directory-certificate-based-authentication-get-started.md) |
| Przejdź do panelu tooAccess i uwierzytelniania za pomocą certyfikatu użytkownika | https://myapps.microsoft.com |

### <a name="considerations"></a>Zagadnienia do rozważenia

toolearn można znaleźć więcej informacji na temat ostrzeżenia tego wdrożenia: [usług AD FS: uwierzytelnianie certyfikatu z usługą Azure AD & usługi Office 365](https://blogs.msdn.microsoft.com/samueld/2016/07/19/adfs-certauth-aad-o365/)



> [!NOTE]
> Posiadanie certyfikatu użytkownika powinien być chroniony. Przy użyciu zarządzania urządzeniami lub kod PIN w przypadku kart inteligentnych.



[!INCLUDE [active-directory-playbook-toc](../../includes/active-directory-playbook-steps.md)]
