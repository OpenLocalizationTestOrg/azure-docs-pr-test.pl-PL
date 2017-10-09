---
title: "aaaAzure Active Directory — często zadawane pytania | Dokumentacja firmy Microsoft"
description: "Azure Active Directory — często zadawane pytania odpowiedzi na pytania dotyczące sposobu uzyskania dostępu tooaccess Azure i usługi Azure Active Directory, zarządzaniem hasłami i aplikacji."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: b8207760-9714-4871-93d5-f9893de31c8f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/16/2017
ms.author: markvi
ms.openlocfilehash: 63c30c4aeda4551bf02c6b968f98cded5a3b2c16
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-faq"></a>Często zadawane pytania dotyczące usługi Azure Active Directory
Azure Active Directory (Azure AD) jest kompleksowym rozwiązaniem typu tożsamość jako usługa (IDaaS, Identity as a Service), które obejmuje wszystkie aspekty tożsamości, zarządzania dostępem i bezpieczeństwa.

Aby uzyskać więcej informacji, zobacz [Co to jest usługa Azure Active Directory?](active-directory-whatis.md).


## <a name="access-azure-and-azure-active-directory"></a>Uzyskiwanie dostępu do platformy Azure i usługi Azure Active Directory
**Pytanie: Dlaczego otrzymuję błąd "nie znaleziono żadnych subskrypcji" podczas próby tooaccess usługi Azure AD w hello klasycznego portalu Azure?**

**Odpowiedź:** tooaccess hello klasycznego portalu Azure, każdy użytkownik potrzebuje uprawnień z subskrypcją platformy Azure. Jeśli masz płatną subskrypcję usługi Office 365 lub Azure AD, przejdź zbyt[http://aka.ms/accessAAD](http://aka.ms/accessAAD) kroku jednorazowej aktywacji. W przeciwnym razie trzeba będzie tooactivate bezpłatny [konta Azure](https://azure.microsoft.com/pricing/free-trial/) lub płatną subskrypcję.

Aby uzyskać więcej informacji, zobacz:

* [Jak subskrypcje platformy Azure są kojarzone z usługą Azure Active Directory](active-directory-how-subscriptions-associated-directory.md)
* [Zarządzanie hello katalogu dla subskrypcji usługi Office 365 na platformie Azure](active-directory-manage-o365-subscription.md)

- - -
**Pytanie: co to jest hello relacja między usługą Azure AD, Office 365 i Azure?**

**Odpowiedź:** usługi Azure AD zapewnia typowych możliwości tożsamościami i dostępem tooall usług sieci web. Czy używasz usługi Office 365, Microsoft Azure, Intune, lub inne osoby, możesz jest już przy użyciu usługi Azure AD toohelp włączyć zarządzanie logowania i dostępu dla tych usług.

Wszyscy użytkownicy, którzy są skonfigurowane usługi sieci web toouse są definiowane jako konta użytkowników w co najmniej jedno wystąpienie usługi Azure AD. Możesz skonfigurować te konta dla bezpłatnych funkcji usługi Azure AD, np. dostępu do aplikacji w chmurze.

Usługi płatne Azure AD, takie jak Enterprise Mobility + Security, uzupełniają inne usługi sieci Web, np. Office 365 i Microsoft Azure, zapewniając kompleksowe rozwiązania z zakresu skalowalnego zarządzania dla przedsiębiorstw i bezpieczeństwa.
- - -
**Pytanie: Dlaczego Zaloguj się w portalu Azure toohello ale nie hello klasycznego portalu Azure?**

**Odpowiedź:** hello portalu Azure wymaga ważnej subskrypcji i klasycznego portalu hello wymagają prawidłowej subskrypcji.  Jeśli nie masz subskrypcji, nie możesz zalogować w portalu klasycznym toohello.
- - -
**Pytanie: jakie są hello różnice między administratora subskrypcji i administratora katalogu?**

**Odpowiedź:** domyślnie mają przypisaną rolę subskrypcji powitania po utworzeniu konta platformy Azure. Administrator subskrypcji przy użyciu konta Microsoft lub służbowy lub konta służbowego z katalogu hello hello subskrypcji platformy Azure jest skojarzony z.  Ta rola jest toomanage autoryzowanych usług w hello portalu Azure.

Jeśli inne muszą toosign w, a dostęp do usług przez przy użyciu hello tej samej subskrypcji, możesz dodać je jako współadministratorzy. Ta rola ma hello same poziomy dostępu jako Witaj, Administratorze usługi, ale nie można zmienić skojarzenia hello katalogów tooAzure subskrypcji.  Aby uzyskać dodatkowe informacje na temat Administratorzy subskrypcji, zobacz [jak tooadd lub zmień role administratora platformy Azure](../billing-add-change-azure-subscription-administrator.md) i [jak subskrypcje platformy Azure są kojarzone z usługi Azure Active Directory](active-directory-how-subscriptions-associated-directory.md).


Usługa Azure AD ma inny zestaw katalogu hello toomanage ról administratora i funkcjami dotyczącymi tożsamości.  Te Administratorzy utracą funkcji toovarious dostępu w portalu Azure hello lub hello klasycznego portalu Azure. Rola administratora Hello określa sposób ich działania, takie jak tworzenie lub edytowanie użytkowników, Przypisz role administracyjne tooothers, resetowanie haseł użytkowników, zarządzanie licencjami użytkowników lub Zarządzanie domenami.  Aby uzyskać dodatkowe informacje na temat administratorów usługi Azure AD i ich ról, zobacz [Przypisywanie ról administratorów w usłudze Azure Active Directory](active-directory-assign-admin-roles.md).

Ponadto usługi płatne Azure AD, takie jak Enterprise Mobility + Security, uzupełniają inne usługi sieci Web, np. Office 365 i Microsoft Azure, zapewniając kompleksowe rozwiązania z zakresu skalowalnego zarządzania dla przedsiębiorstw i bezpieczeństwa.

- - -
**Pytanie: czy istnieje raport, który pokazuje, kiedy wygaśnie moja licencja użytkownika usługi Azure AD?**

**Odpowiedź:** Nie.  Taki raport nie jest obecnie dostępny.

- - -

## <a name="get-started-with-hybrid-azure-ad"></a>Wprowadzenie do hybrydowej usługi Azure AD


**Pytanie: jak opuścić dzierżawę, gdy dodano mnie do niej jako współpracownika?**

**Odpowiedź:** woluminowi dzierżawy organizacji tooanother jako współpracownika, można użyć hello "dzierżawy przełącznik" w górnym prawym tooswitch hello między dzierżawcami.  Obecnie nie istnieje żadne hello tooleave sposób zapraszanie organizacji i firma Microsoft pracuje udostępniać tę funkcjonalność.  Dopóki ta funkcja jest dostępna, możesz poprosić hello zapraszanie tooremove organizacji z swojej dzierżawy.
- - -
**Pytanie: jak połączyć tooAzure katalogu Moje lokalnej usługi AD?**

**Odpowiedź:** można połączyć z lokalnego katalogu tooAzure AD przy użyciu usługi Azure AD Connect.

Aby uzyskać więcej informacji, zobacz [Integrowanie tożsamości lokalnych z usługą Azure Active Directory](active-directory-aadconnect.md).

- - -
**Pytanie: jak skonfigurować logowanie jednokrotne (SSO) między katalogiem lokalnym i aplikacjami w chmurze?**

**Odpowiedź:** wystarczy tooset się rejestracji jednokrotnej (SSO) między katalogiem lokalnym i usługą Azure AD. Tak długo, jak możesz uzyskać dostęp do aplikacji w chmurze za pomocą usługi Azure AD, usługa hello automatycznie dyski toocorrectly uwierzytelniania przy użyciu poświadczeń lokalnych użytkowników.

Implementowanie logowania jednokrotnego z pozycji lokalnej można z łatwością przeprowadzić przy użyciu rozwiązań federacyjnych, np. usług Active Directory Federation Services, lub przez skonfigurowanie synchronizacji skrótów haseł. Obie te opcje można łatwo wdrożyć za pomocą Kreatora konfiguracji hello Azure AD Connect.

Aby uzyskać więcej informacji, zobacz [Integrowanie tożsamości lokalnych z usługą Azure Active Directory](active-directory-aadconnect.md).

- - -
**Pytanie: czy usługa Azure AD zawiera samoobsługowy portal dla użytkowników w organizacji?**

**Odpowiedź:** tak, usługa Azure AD zapewnia hello [Panel dostępu usługi Azure AD](http://myapps.microsoft.com) dla użytkownika samoobsługi i dostęp do aplikacji. W przypadku usługi Office 365, można znaleźć wiele hello takie same możliwości w portalu usługi Office 365 hello.

Aby uzyskać więcej informacji, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).

- - -
**Pytanie: czy usługa Azure AD pomaga w zarządzaniu infrastrukturą lokalną?**

**Odpowiedź:** tak. Hello Azure AD — wersja Premium zawiera program Azure AD Connect Health. Azure AD Connect Health pomaga monitorować i uzyskiwać wgląd w swoją tożsamość lokalnej infrastruktury i hello usług synchronizacji.  

Aby uzyskać więcej informacji, zobacz [monitorowanie lokalnej tożsamości infrastruktury i synchronizacji usług w chmurze hello](active-directory-aadconnect-health.md).  

- - -
## <a name="password-management"></a>Zarządzanie hasłami
**Pytanie: czy można użyć funkcji zapisywania zwrotnego haseł usługi Azure AD bez synchronizacji haseł? (W tym scenariuszu jest możliwe toouse usługi Azure AD samoobsługowego resetowania hasła (SSPR) przy użyciu hasła zapisu i nie magazynu haseł w chmurze hello?)**

**Odpowiedź:** nie ma potrzeby toosynchronize użytkownika usługi Active Directory hasła tooAzure AD tooenable zapisu. W środowisku federacyjnym usługi Azure AD rejestracji jednokrotnej (SSO) polega na powitania lokalnego katalogu tooauthenticate hello użytkownika. Ten scenariusz nie wymaga toobe hasło lokalne powitania śledzone w usłudze Azure AD.

- - -
**Pytanie: jak długo trwa dla toobe hasła, zapisywane tooActive katalogu lokalnego?**

**Odpowiedź:** zapisywanie zwrotne haseł działa w czasie rzeczywistym.

Więcej informacji można znaleźć w temacie [Wprowadzenie do zarządzania hasłami](active-directory-passwords-getting-started.md)

- - -
**Pytane: czy mogę użyć funkcji zapisywania zwrotnego haseł wobec haseł zarządzanych przez administratora?**

**Odpowiedź:** tak, jeśli masz hasło funkcję zapisywania zwrotnego hello hasła operacje wykonywane przez administratora będą zwrotnie zapisywane tooyour w środowisku lokalnym.  

Aby uzyskać więcej odpowiedzi pytania związane z toopassword, zobacz [Zarządzanie hasłami — często zadawane pytania](active-directory-passwords-faq.md).
- - -
**Pytanie: co można zrobić, jeśli w trakcie toochange hasła nie pamiętam istniejącego hasła Office 365/usługi Azure AD?**

**Odpowiedź:** w takiej sytuacji istnieje kilka opcji.  Użyj funkcji samoobsługowego resetowania haseł (SSPR), jeśli jest dostępna.  To, czy funkcja samoobsługowego resetowania haseł działa, zależy od tego, jak została skonfigurowana.  Aby uzyskać więcej informacji, zobacz [jak hello resetowania hasła portalu pracy](active-directory-passwords-best-practices.md).

W przypadku użytkowników usługi Office 365, administrator może zresetować hasło hello przy użyciu hello czynności opisane w temacie [resetowanie haseł użytkowników](https://support.office.com/en-us/article/Admins-Reset-user-passwords-7A5D073B-7FAE-4AA5-8F96-9ECD041ABA9C?ui=en-US&rs=en-US&ad=US).

Dla konta usługi Azure AD Administratorzy mogą resetować hasła przy użyciu jednej z następujących hello:

- [Resetuj konta w portalu Azure hello](active-directory-users-reset-password-azure-portal.md)
- [Resetuj konta w portalu klasycznym hello](active-directory-create-users-reset-password.md)
- [Korzystanie z programu PowerShell](/powershell/module/msonline/set-msoluserpassword?view=azureadps-1.0)


- - -
## <a name="security"></a>Bezpieczeństwo
**Pytanie: czy konta są blokowane po określonej liczbie nieudanych prób, czy jest stosowana bardziej zaawansowana strategia?**</br>
Używamy dokładniejsze kont toolock strategii.  To jest oparta na powitania IP hello żądania i hello hasła. czas trwania blokady hello Hello zwiększa także oparte na prawdopodobieństwo hello jest atak.  

**Komunikaty Q: niektórych odrzucone z hello hasła (typowe) "to hasło było używane toomany razy", czy to odnosi się toopasswords używane w hello, bieżącej usłudze active directory?**</br>
Odnosi się toopasswords, które są globalnie wspólne, takie jak warianty "Password" i "123456".

**Pytanie: czy żądanie logowania z podejrzanych źródeł (botnety, punkt końcowy sieci Tor) zostanie zablokowane w dzierżawie B2C, czy wymaga to dzierżawy w warstwie Podstawowa lub Premium?**</br>
Oferujemy bramę, która filtruje żądania i zapewnia ochronę przed botnetami. Jest ona stosowana we wszystkich dzierżawach B2C.

## <a name="application-access"></a>Dostęp do aplikacji
**Pytanie: gdzie mogę znaleźć listę aplikacji, które są wstępnie zintegrowane z usługą Azure AD i jej funkcjami?**

**Odpowiedź:** usługa Azure AD ma ponad 2600 wstępnie zintegrowanych aplikacji od firmy Microsoft, dostawców usług aplikacji i partnerów. Wszystkie wstępnie zintegrowane aplikacje obsługują logowanie jednokrotne. Logowania jednokrotnego pozwala korzystać z tooaccess poświadczeń w organizacji aplikacji. Niektórych aplikacji hello obsługują również zautomatyzowaną aprowizację i anulowanie obsługi.

Aby uzyskać pełną listę wstępnie zintegrowanych aplikacji hello Zobacz hello [Active Directory Marketplace](https://azure.microsoft.com/marketplace/active-directory/).

- - -
**Pytanie: co zrobić, jeśli hello potrzebnych w nie jest aplikacja hello Azure AD marketplace?**

**Odpowiedź:** przy użyciu usługi Azure AD Premium możesz dodać i skonfigurować dowolną aplikację. W zależności od możliwości aplikacji i preferencji możesz skonfigurować logowanie jednokrotne i automatyczną aprowizację.  

Aby uzyskać więcej informacji, zobacz:

* [Konfigurowanie jednego logowania jednokrotnego tooapplications, które nie znajdują się w galerii aplikacji hello Azure Active Directory](active-directory-saas-custom-apps.md)
* [Przy użyciu SCIM tooenable automatyczne Inicjowanie obsługi użytkowników i grup z usługi Azure Active Directory tooapplications](active-directory-scim-provisioning.md)

- - -
**Pytanie: jak użytkownicy logują się w tooapplications za pomocą usługi Azure AD?**

**Odpowiedź:** usługi Azure AD zapewnia kilka metod tooview użytkowników i dostępu do swoich aplikacji, takich jak:

* panel dostępu Hello Azure AD
* uruchamianie aplikacji Hello usługi Office 365
* Aplikacje toofederated bezpośredniego logowania
* Toofederated głębokiego łącza, oparte na hasłach lub istniejących aplikacjach

Aby uzyskać więcej informacji, zobacz [wdrażanie usługi Azure AD zintegrowane aplikacje toousers](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users).

- - -
**Pytanie: jakie są różne sposoby hello Azure AD umożliwia uwierzytelnianie i tooapplications rejestracji jednokrotnej?**

**Odpowiedź:** usługa Azure AD obsługuje wiele standardowych protokołów uwierzytelniania i autoryzacji, takich jak SAML 2.0, OpenID Connect, OAuth 2.0 i WS-Federation. Usługa Azure AD obsługuje również archiwizowanie haseł i automatyczne logowanie do aplikacji, które obsługują wyłącznie uwierzytelnianie oparte na formularzach.  

Aby uzyskać więcej informacji, zobacz:

* [Scenariusze uwierzytelniania dla usługi Azure AD](active-directory-authentication-scenarios.md)
* [Protokoły uwierzytelniania usługi Active Directory](https://msdn.microsoft.com/library/azure/dn151124.aspx)
* [Jak działa logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md#how-does-single-sign-on-with-azure-active-directory-work)

- - -
**Pytanie: czy mogę dodać aplikacje uruchamiane lokalnie?**

**Odpowiedź:** serwera Proxy aplikacji usługi Azure AD zapewnia prosty i bezpieczny dostęp tooon lokalnych aplikacji sieci web, które można wybrać. Można uzyskać dostępu do tych aplikacji w hello samo dostępu oprogramowanie jako usługa (SaaS) aplikacji w usłudze Azure AD. Nie istnieje potrzeba dla sieci VPN lub toochange infrastruktury sieci.  

Aby uzyskać więcej informacji, zobacz [jak tooprovide bezpiecznego dostępu zdalnego aplikacje lokalne tooon](active-directory-application-proxy-get-started.md).

- - -
**Pytanie: jak wymagać uwierzytelniania wieloskładnikowego dla użytkowników uzyskujących dostęp do określonej aplikacji?**

**Odpowiedź:** przy użyciu dostępu warunkowego usługi Azure AD możesz przypisać unikatowe zasady dostępu dla każdej aplikacji. W zasadach można wymagać uwierzytelniania wieloskładnikowego zawsze lub gdy użytkownicy nie są połączone toohello sieci lokalnej.  

Aby uzyskać więcej informacji, zobacz [zabezpieczanie dostępu tooOffice 365 i innych aplikacji połączone tooAzure usługi Active Directory](active-directory-conditional-access.md).

- - -
**Pytanie: co to jest automatyczna aprowizacja użytkowników dla aplikacji SaaS?**

**Odpowiedź:** tooautomate hello tworzenia, obsługi i usuwania tożsamości użytkowników w wiele aplikacji SaaS w chmurze popularnych użycia usługi Azure AD.

Aby uzyskać więcej informacji, zobacz [zautomatyzować użytkownika alokowania i anulowania alokowania tooSaaS aplikacji w usłudze Azure Active Directory](active-directory-saas-app-provisioning.md).

- - -
**Pytanie: czy mogę skonfigurować bezpieczne połączenie LDAP z usługą Azure AD?**

**Odpowiedź:** nie. Usługi Azure AD nie obsługuje protokołu LDAP hello.
