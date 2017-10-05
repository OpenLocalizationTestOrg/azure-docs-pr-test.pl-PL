---
title: "Często zadawane pytania dotyczące usługi Azure Active Directory | Microsoft Docs"
description: "Często zadawane pytania dotyczące usługi Azure Active Directory zawierają odpowiedzi na pytania związane z uzyskiwaniem dostępu do platformy Azure i usługi Azure Active Directory, zarządzaniem hasłami i uzyskiwaniem dostępu do aplikacji."
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
ms.openlocfilehash: 8d4460b3059558de2253c6f6a2d2fc8e7564d6d9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-faq"></a>Często zadawane pytania dotyczące usługi Azure Active Directory
Azure Active Directory (Azure AD) jest kompleksowym rozwiązaniem typu tożsamość jako usługa (IDaaS, Identity as a Service), które obejmuje wszystkie aspekty tożsamości, zarządzania dostępem i bezpieczeństwa.

Aby uzyskać więcej informacji, zobacz [Co to jest usługa Azure Active Directory?](active-directory-whatis.md).


## <a name="access-azure-and-azure-active-directory"></a>Uzyskiwanie dostępu do platformy Azure i usługi Azure Active Directory
**Pytanie: dlaczego otrzymuję błąd „Nie znaleziono żadnych subskrypcji” podczas próby dostępu do usługi Azure AD w klasycznej witrynie Azure Portal?**

**Odpowiedź:** aby uzyskać dostęp do klasycznej witryny Azure Portal, każdy użytkownik musi mieć uprawnienia w ramach subskrypcji platformy Azure. Jeśli korzystasz z płatnej licencji usługi Office 365 lub Azure AD, przejdź do strony [http://aka.ms/accessAAD](http://aka.ms/accessAAD), aby użyć jednorazowej aktywacji. W przeciwnym razie należy aktywować bezpłatne [konto platformy Azure](https://azure.microsoft.com/pricing/free-trial/) lub płatną subskrypcję.

Aby uzyskać więcej informacji, zobacz:

* [Jak subskrypcje platformy Azure są kojarzone z usługą Azure Active Directory](active-directory-how-subscriptions-associated-directory.md)
* [Zarządzanie katalogiem dla subskrypcji usługi Office 365 na platformie Azure](active-directory-manage-o365-subscription.md)

- - -
**Pytanie: jaka jest relacja między usługami Azure AD, Office 365 i platformą Azure?**

**Odpowiedź:** usługa Azure AD zawiera typowe funkcje związane z tożsamością i dostępem do wszystkich usług sieci Web. Niezależnie od tego, czy używasz usługi Office 365, Microsoft Azure, Intune lub innych, już używasz usługi Azure AD w celu umożliwienia logowania i zarządzania dostępem do tych wszystkich usług.

Wszyscy użytkownicy skonfigurowani do używania usług sieci Web są zdefiniowani jako konta użytkowników w co najmniej jednym wystąpieniu usługi Azure AD. Możesz skonfigurować te konta dla bezpłatnych funkcji usługi Azure AD, np. dostępu do aplikacji w chmurze.

Usługi płatne Azure AD, takie jak Enterprise Mobility + Security, uzupełniają inne usługi sieci Web, np. Office 365 i Microsoft Azure, zapewniając kompleksowe rozwiązania z zakresu skalowalnego zarządzania dla przedsiębiorstw i bezpieczeństwa.
- - -
**Pytanie: dlaczego mogę się zalogować w witrynie Azure Portal, ale nie w klasycznej witrynie Azure Portal?**

**Odpowiedź:** witryna Azure Portal nie wymaga ważnej subskrypcji, podczas gdy portal klasyczny wymaga posiadania ważnej subskrypcji.  Jeśli nie masz subskrypcji, zalogowanie się w portalu klasycznym nie jest możliwe.
- - -
**Pytanie: jaka jest różnica między administratorem subskrypcji a administratorem katalogu?**

**Odpowiedź:** domyślnie po utworzeniu konta na platformie Azure przypisywana jest do niego rola administratora subskrypcji. Administrator subskrypcji może używać konta Microsoft lub konta służbowego z katalogu, z którym została skojarzona subskrypcja platformy Azure.  Ta rola jest autoryzowana do zarządzania usługami w witrynie Azure Portal.

Jeśli inni użytkownicy potrzebują logować się i uzyskiwać dostęp do usług za pomocą tej samej subskrypcji, możesz dodać ich jako współadministratorów. Ta rola ma takie same uprawnienia dostępu jak administrator usługi, ale nie może zmieniać skojarzenia subskrypcji z katalogami platformy Azure.  Aby uzyskać dodatkowe informacje na temat administratorów subskrypcji, zobacz [How to add or change Azure administrator roles](../billing-add-change-azure-subscription-administrator.md) (Jak dodać lub zmienić role administratora platformy Azure) i [Jak subskrypcje platformy Azure są kojarzone z usługą Azure Active Directory](active-directory-how-subscriptions-associated-directory.md).


Usługa Azure AD ma inny zestaw ról administratora na potrzeby zarządzania katalogiem i funkcjami dotyczącymi tożsamości.  Ci administratorzy będą mieli dostęp do różnych funkcji w witrynie Azure Portal i klasycznej witrynie Azure Portal. Rola administratora określa, co może robić administrator, na przykład tworzyć lub edytować użytkowników, przypisywać role administracyjne innym osobom, resetować hasła użytkowników, zarządzać licencjami użytkowników oraz zarządzać domenami.  Aby uzyskać dodatkowe informacje na temat administratorów usługi Azure AD i ich ról, zobacz [Przypisywanie ról administratorów w usłudze Azure Active Directory](active-directory-assign-admin-roles.md).

Ponadto usługi płatne Azure AD, takie jak Enterprise Mobility + Security, uzupełniają inne usługi sieci Web, np. Office 365 i Microsoft Azure, zapewniając kompleksowe rozwiązania z zakresu skalowalnego zarządzania dla przedsiębiorstw i bezpieczeństwa.

- - -
**Pytanie: czy istnieje raport, który pokazuje, kiedy wygaśnie moja licencja użytkownika usługi Azure AD?**

**Odpowiedź:** Nie.  Taki raport nie jest obecnie dostępny.

- - -

## <a name="get-started-with-hybrid-azure-ad"></a>Wprowadzenie do hybrydowej usługi Azure AD


**Pytanie: jak opuścić dzierżawę, gdy dodano mnie do niej jako współpracownika?**

**Odpowiedź:** w przypadku dodania do dzierżawy innej organizacji jako współpracownika możesz przełączać się między dzierżawami za pomocą „przełącznika dzierżawy” w prawym górnym rogu.  Obecnie nie ma możliwości opuszczenia organizacji zapraszającej. Firma Microsoft pracuje nad dodaniem tej funkcji.  Do czasu udostępnienia tej funkcji rozwiązaniem może być poproszenie organizacji zapraszającej o usunięcie z dzierżawy.
- - -
**Pytanie: jak połączyć katalog lokalny z usługą Azure AD?**

**Odpowiedź:** możesz połączyć katalog lokalny z usługą Azure AD przy użyciu narzędzia Azure AD Connect.

Aby uzyskać więcej informacji, zobacz [Integrowanie tożsamości lokalnych z usługą Azure Active Directory](active-directory-aadconnect.md).

- - -
**Pytanie: jak skonfigurować logowanie jednokrotne (SSO) między katalogiem lokalnym i aplikacjami w chmurze?**

**Odpowiedź:** wystarczy skonfigurować logowanie jednokrotne (SSO) między katalogiem lokalnym i usługą Azure AD. Jeśli tylko uzyskujesz dostęp do aplikacji w chmurze poprzez usługę Azure AD, usługa automatycznie wymusza od użytkowników odpowiednie uwierzytelnianie przy użyciu ich lokalnych poświadczeń.

Implementowanie logowania jednokrotnego z pozycji lokalnej można z łatwością przeprowadzić przy użyciu rozwiązań federacyjnych, np. usług Active Directory Federation Services, lub przez skonfigurowanie synchronizacji skrótów haseł. Możesz z łatwością wdrożyć obie opcje, korzystając z kreatora konfiguracji programu Azure AD Connect.

Aby uzyskać więcej informacji, zobacz [Integrowanie tożsamości lokalnych z usługą Azure Active Directory](active-directory-aadconnect.md).

- - -
**Pytanie: czy usługa Azure AD zawiera samoobsługowy portal dla użytkowników w organizacji?**

**Odpowiedź:** tak, usługa Azure AD zapewnia [Panel dostępu usługi Azure AD](http://myapps.microsoft.com) do samoobsługi użytkowników i dostępu do aplikacji. Jeśli korzystasz z usługi Office 365, możesz znaleźć wiele tych samych funkcji w portalu usługi Office 365.

Aby uzyskać więcej informacji, zobacz [Wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).

- - -
**Pytanie: czy usługa Azure AD pomaga w zarządzaniu infrastrukturą lokalną?**

**Odpowiedź:** tak. Usługa Azure AD Premium zawiera program Azure AD Connect Health. Program Azure AD Connect Health pomaga monitorować i zdobywać informacje o lokalnej infrastrukturze do obsługi tożsamości oraz usługach synchronizacji.  

Aby uzyskać więcej informacji, zobacz [Monitorowanie lokalnej infrastruktury do obsługi tożsamości i usług synchronizacji w chmurze](active-directory-aadconnect-health.md).  

- - -
## <a name="password-management"></a>Zarządzanie hasłami
**Pytanie: czy można użyć funkcji zapisywania zwrotnego haseł usługi Azure AD bez synchronizacji haseł? (Czy w tym scenariuszu można użyć funkcji samoobsługowego resetowania haseł (SSPR) usługi Azure AD z zapisywaniem zwrotnym haseł bez przechowywania haseł w chmurze?)**

**Odpowiedź:** nie musisz synchronizować haseł usługi Active Directory z usługą Azure AD, aby korzystać z funkcji zapisywania zwrotnego. W środowisku federacyjnym logowanie jednokrotne usługi Azure AD opiera się na katalogu lokalnym w celu uwierzytelniania użytkownika. Ten scenariusz nie wymaga śledzenia lokalnego hasła w usłudze Azure AD.

- - -
**Pytanie: jak długo trwa zwrotne zapisanie hasła w lokalnym wystąpieniu usługi Active Directory?**

**Odpowiedź:** zapisywanie zwrotne haseł działa w czasie rzeczywistym.

Więcej informacji można znaleźć w temacie [Wprowadzenie do zarządzania hasłami](active-directory-passwords-getting-started.md)

- - -
**Pytane: czy mogę użyć funkcji zapisywania zwrotnego haseł wobec haseł zarządzanych przez administratora?**

**Odpowiedź:** tak, jeśli włączysz funkcję zapisywania zwrotnego haseł, operacje na hasłach wykonywane przez administratora będą zwrotnie zapisywane w środowisku lokalnym.  

Aby uzyskać więcej odpowiedzi na pytania związane z hasłami, zobacz [Często zadawane pytania dotyczące zarządzania hasłami](active-directory-passwords-faq.md).
- - -
**Pytanie: co zrobić, jeśli chcę zmienić hasło usługi Office 365/Azure AD, a nie pamiętam istniejącego hasła?**

**Odpowiedź:** w takiej sytuacji istnieje kilka opcji.  Użyj funkcji samoobsługowego resetowania haseł (SSPR), jeśli jest dostępna.  To, czy funkcja samoobsługowego resetowania haseł działa, zależy od tego, jak została skonfigurowana.  Aby uzyskać więcej informacji, zobacz [Jak działa portal resetowania haseł](active-directory-passwords-best-practices.md).

Jeśli jesteś użytkownikiem usługi Office 365, Twój administrator może zresetować hasło, wykonując kroki opisane w artykule [Resetowanie haseł użytkowników](https://support.office.com/en-us/article/Admins-Reset-user-passwords-7A5D073B-7FAE-4AA5-8F96-9ECD041ABA9C?ui=en-US&rs=en-US&ad=US).

W przypadku kont usługi Azure AD administratorzy mogą zresetować hasło w jeden z następujących sposobów:

- [Resetowanie kont w witrynie Azure Portal](active-directory-users-reset-password-azure-portal.md)
- [Resetowanie kont w portalu klasycznym](active-directory-create-users-reset-password.md)
- [Korzystanie z programu PowerShell](/powershell/module/msonline/set-msoluserpassword?view=azureadps-1.0)


- - -
## <a name="security"></a>Bezpieczeństwo
**Pytanie: czy konta są blokowane po określonej liczbie nieudanych prób, czy jest stosowana bardziej zaawansowana strategia?**</br>
Korzystamy z bardziej zaawansowanej strategii blokowania kont.  Jest ona oparta na adresie IP żądania i wprowadzonym haśle. Czas trwania blokady wydłuża się też w zależności od stopnia prawdopodobieństwa ataku.  

**Pytanie: niektóre (typowe) hasła są odrzucane i jest wyświetlany komunikat z informacją o tym, że hasło zostało użyte zbyt wiele razy. Czy dotyczy to haseł używanych w bieżącej usłudze Active Directory?**</br>
Dotyczy to typowych haseł występujących globalnie, takich jak różne odmiany ciągów „Hasło” i „123456”.

**Pytanie: czy żądanie logowania z podejrzanych źródeł (botnety, punkt końcowy sieci Tor) zostanie zablokowane w dzierżawie B2C, czy wymaga to dzierżawy w warstwie Podstawowa lub Premium?**</br>
Oferujemy bramę, która filtruje żądania i zapewnia ochronę przed botnetami. Jest ona stosowana we wszystkich dzierżawach B2C.

## <a name="application-access"></a>Dostęp do aplikacji
**Pytanie: gdzie mogę znaleźć listę aplikacji, które są wstępnie zintegrowane z usługą Azure AD i jej funkcjami?**

**Odpowiedź:** usługa Azure AD ma ponad 2600 wstępnie zintegrowanych aplikacji od firmy Microsoft, dostawców usług aplikacji i partnerów. Wszystkie wstępnie zintegrowane aplikacje obsługują logowanie jednokrotne. Logowanie jednokrotne umożliwia uzyskiwanie dostępu do aplikacji przy użyciu poświadczeń organizacji. Niektóre aplikacje obsługują również zautomatyzowaną aprowizację i cofanie aprowizacji.

Aby uzyskać pełną listę wstępnie zintegrowanych aplikacji, zobacz [Active Directory Marketplace](https://azure.microsoft.com/marketplace/active-directory/).

- - -
**Pytanie: co w przypadku, jeśli aplikacja, której potrzebuję, nie znajduje się w witrynie Azure AD Marketplace?**

**Odpowiedź:** przy użyciu usługi Azure AD Premium możesz dodać i skonfigurować dowolną aplikację. W zależności od możliwości aplikacji i preferencji możesz skonfigurować logowanie jednokrotne i automatyczną aprowizację.  

Aby uzyskać więcej informacji, zobacz:

* [Konfigurowanie logowania jednokrotnego do aplikacji, które nie znajdują się w galerii aplikacji Azure Active Directory](active-directory-saas-custom-apps.md)
* [Włączanie automatycznej aprowizacji użytkowników i grup z usługi Azure Active Directory do aplikacji przy użyciu SCIM](active-directory-scim-provisioning.md)

- - -
**Pytanie: jak użytkownicy logują się do aplikacji przy użyciu usługi Azure AD?**

**Odpowiedź:** usługa Azure AD oferuje użytkownikom kilka możliwości wyświetlania aplikacji i uzyskiwania do nich dostępu, np.:

* Panel dostępu usługi Azure AD
* Program uruchamiający aplikacje usługi Office 365
* Bezpośrednie logowanie do aplikacji federacyjnych
* Linki bezpośrednie do federacyjnych, opartych na hasłach lub istniejących aplikacjach

Aby uzyskać więcej informacji, zobacz [Wdrażanie zintegrowanych aplikacji usługi Azure AD dla użytkowników](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users).

- - -
**Pytanie: jakie są różne sposoby włączania uwierzytelniania i logowania jednokrotnego do aplikacji przez usługę Azure AD?**

**Odpowiedź:** usługa Azure AD obsługuje wiele standardowych protokołów uwierzytelniania i autoryzacji, takich jak SAML 2.0, OpenID Connect, OAuth 2.0 i WS-Federation. Usługa Azure AD obsługuje również archiwizowanie haseł i automatyczne logowanie do aplikacji, które obsługują wyłącznie uwierzytelnianie oparte na formularzach.  

Aby uzyskać więcej informacji, zobacz:

* [Scenariusze uwierzytelniania dla usługi Azure AD](active-directory-authentication-scenarios.md)
* [Protokoły uwierzytelniania usługi Active Directory](https://msdn.microsoft.com/library/azure/dn151124.aspx)
* [Jak działa logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md#how-does-single-sign-on-with-azure-active-directory-work)

- - -
**Pytanie: czy mogę dodać aplikacje uruchamiane lokalnie?**

**Odpowiedź:** serwer proxy aplikacji usługi Azure AD zapewnia prosty i bezpieczny dostęp do wybranych lokalnych aplikacji sieci Web. Dostęp do tych aplikacji można uzyskiwać w taki sam sposób jak w przypadku aplikacji typu oprogramowanie jako usługa (SaaS) w usłudze Azure AD. Nie ma potrzeby stosowania sieci VPN ani zmiany infrastruktury sieciowej.  

Aby uzyskać więcej informacji, zobacz [How to provide secure remote access to on-premises applications](active-directory-application-proxy-get-started.md) (Jak zapewnić bezpieczny zdalny dostęp do aplikacji lokalnych).

- - -
**Pytanie: jak wymagać uwierzytelniania wieloskładnikowego dla użytkowników uzyskujących dostęp do określonej aplikacji?**

**Odpowiedź:** przy użyciu dostępu warunkowego usługi Azure AD możesz przypisać unikatowe zasady dostępu dla każdej aplikacji. W zasadach możesz wymagać korzystania z uwierzytelniania wieloskładnikowego w każdym przypadku lub wtedy, gdy użytkownicy nie są połączeni z siecią lokalną.  

Aby uzyskać więcej informacji, zobacz [Zabezpieczanie dostępu do usługi Office 365 i innych aplikacji podłączonych do usługi Azure Active Directory](active-directory-conditional-access.md).

- - -
**Pytanie: co to jest automatyczna aprowizacja użytkowników dla aplikacji SaaS?**

**Odpowiedź:** usługa Azure AD umożliwia automatyzację tworzenia, obsługi i usuwania tożsamości użytkowników w wielu popularnych aplikacjach SaaS w chmurze.

Aby uzyskać więcej informacji, zobacz [Automate User Provisioning and Deprovisioning to SaaS Applications with Azure Active Directory](active-directory-saas-app-provisioning.md) (Automatyzacja aprowizacji i cofania aprowizacji użytkowników dla aplikacji SaaS przy użyciu usługi Azure Active Directory).

- - -
**Pytanie: czy mogę skonfigurować bezpieczne połączenie LDAP z usługą Azure AD?**

**Odpowiedź:** nie. Usługa Azure AD nie obsługuje protokołu LDAP.
