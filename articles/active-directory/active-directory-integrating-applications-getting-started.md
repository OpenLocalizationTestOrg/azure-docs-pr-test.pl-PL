---
title: "Rozpoczęto aaaGet Integrowanie usługi Azure AD z aplikacjami | Dokumentacja firmy Microsoft"
description: W tym artykule jest Przewodnik z wprowadzeniem do integracji z lokalnymi aplikacjami i aplikacje w chmurze Azure Active Directory (AD).
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: db6d210d-c970-49e9-bd20-36d984bcd1c3
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/31/2017
ms.author: markvi
ms.reviewer: asteen
ms.openlocfilehash: 5a7a851e8418083fee72ab58477a9cab75d0d4bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="integrating-azure-active-directory-with-applications-getting-started-guide"></a>Przewodnik Wprowadzenie do integracji Azure Active Directory z aplikacjami pobierania
## <a name="overview"></a>Omówienie
Ten temat jest zamierzone toogive możesz przewodnik integracji aplikacji z usługi Azure Active Directory (AD). Hello sekcjach poniżej zawiera krótkie podsumowanie bardziej szczegółowych tematów, więc można zidentyfikować części tego przewodnika pobierania, które są odpowiednie tooyou.  Wykonaj hello łącza do bardziej zgłębić temat na każdego tematu.

## <a name="before-you-begin-take-inventory"></a>Przed rozpoczęciem spis
Przed razu toointegrating aplikacji za pomocą usługi Azure AD jest tooknow ważne w przypadku, gdy użytkownik, a chcesz toogo.  Witaj następujące pytania są zamierzone toohelp, które zdaniem o projekcie integracji aplikacji usługi Azure AD.

### <a name="application-inventory"></a>Spis aplikacji
* Gdzie znajdują się wszystkie aplikacje? Kto jest właścicielem je?
* Jakiego rodzaju uwierzytelniania wymagane przez aplikacje
* Który musi uzyskiwać dostęp do aplikacji toowhich?
* Czy chcesz, aby toodeploy nową aplikację?
  * Zostanie skompiluj go wewnętrznych i wdrożyć go na wystąpienie obliczeń platformy Azure?
  * Zostanie użyty, jest dostępna w galerii aplikacji Azure hello?

### <a name="user-and-group-inventory"></a>Spis użytkowników i grup
* Gdy się kont użytkowników?
  * Lokalna usługa Active Directory
  * Azure AD
  * W ramach innej aplikacji bazy danych, którego jesteś właścicielem
  * W przypadku niezatwierdzonych aplikacji
  * Wszystkie powyższe hello
* Jakie uprawnienia i przypisania ról czy poszczególnych użytkowników aktualnie ma? Potrzebujesz tooreview ich dostęp, lub czy na pewno, że przypisania dostępu i role użytkowników są odpowiednie teraz?
* Grupy już istnieją w lokalnej usługi Active Directory?
  * Sposób organizowania grup
  * Które są elementami członkowskimi grupy hello?
  * Jakie przypisania uprawnień/ról grup hello aktualnie zainstalowanego?
* Należy określić tooclean zapasowe użytkownika/grupy baz danych przed zintegrowaniem?  (Jest to bardzo ważne pytania. Odzyskiwanie w pamięci out).

### <a name="access-management-inventory"></a>Dostęp do zarządzania spisu
* Jak można obecnie zarządzać tooapplications dostępu użytkownika? Czy który potrzebuje toochange?  Bierzesz pod uwagę inne sposoby toomanage dostępu, takich jak z [RBAC](role-based-access-control-configure.md) na przykład?
* Który musi toowhat dostępu?

Być może nie masz hello tooall odpowiedzi z tych pytań na początku, ale nie szkodzi.  Ten przewodnik może pomóc w odpowiedzi na niektóre z tych pytań i niektóre świadomych decyzji.

## <a name="prerequisites"></a>Wymagania wstępne
* Subskrypcja platformy Azure i katalogu usługi Azure Active Directory.  Jeśli nie masz jeszcze subskrypcji platformy Azure, Azure można Wypróbuj bezpłatnie przez 30 dni. [Wypróbuj](https://azure.microsoft.com/trial/get-started-active-directory/)

## <a name="application-integration-with-azure-ad"></a>Integracja aplikacji z usługą Azure AD
### <a name="finding-unsanctioned-cloud-applications-with-cloud-app-discovery"></a>Znajdowanie niezatwierdzona aplikacji w chmurze z usługi Cloud App Discovery
Jak wspomniano powyżej, może to być aplikacje, które nie zostały zarządzanych przez organizację do tej pory.  W ramach procesu spisu hello jest możliwe toofind niezatwierdzona aplikacji w chmurze. Zobacz [znajdowania aplikacji w chmurze niezatwierdzone z usługi Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md).

### <a name="authentication-types"></a>Typy uwierzytelniania
Poszczególnych aplikacji może być wymagania dotyczące różnych uwierzytelniania. Z usługą Azure AD certyfikaty podpisywania można z aplikacji, które używają SAML 2.0, WS-Federation, lub OpenID Connect protokoły oraz jak hasło rejestracji jednokrotnej. Aby uzyskać więcej informacji o aplikacji Zobacz typy uwierzytelniania do użycia z usługą Azure AD [Zarządzanie certyfikatów dla federacyjnych rejestracji jednokrotnej w usłudze Azure Active Directory](active-directory-sso-certs.md) i [hasła na podstawie jednokrotnego](active-directory-appssoaccess-whatis.md).

### <a name="enabling-sso-with-azure-ad-app-proxy"></a>Włączanie rejestracji Jednokrotnej z serwera Proxy aplikacji usługi Azure AD
Dzięki serwerowi Proxy aplikacji usługi AD Microsoft Azure musisz podać tooapplications dostępu znajdujących się w sieci prywatnej bezpiecznego, z dowolnego miejsca i na dowolnym urządzeniu. Po zainstalowaniu łącznika serwera proxy aplikacji w danym środowisku, można można łatwo skonfigurować z usługą Azure AD.

### <a name="integrating-applications-with-azure-ad"></a>Integrowanie aplikacji z usługą Azure AD
Witaj następujące artykuły omówiono w nim różne sposoby hello aplikacje integrują się z usługi Azure AD i niektóre wytyczne.

* [Określanie, które toouse usługi Active Directory](active-directory-administer.md)
* [Przy użyciu aplikacji w galerii aplikacji Azure hello](active-directory-appssoaccess-whatis.md)
* [Integrowanie listę samouczków aplikacji SaaS](active-directory-saas-tutorial-list.md)

## <a name="managing-access-tooapplications"></a>Zarządzanie tooapplications dostępu
Witaj następujące artykuły opisano sposoby można zarządzać tooapplications dostępu, gdy zostały zintegrowane z usługą Azure AD za pomocą łączników usługi Azure AD i Azure AD.

* [Zarządzanie tooapps dostępu za pomocą usługi Azure AD](active-directory-managing-access-to-apps.md)
* [Automatyzowanie z łączników usługi Azure AD](active-directory-saas-app-provisioning.md)
* [Przypisywanie użytkowników tooan aplikacji](active-directory-applications-guiding-developers-assigning-users.md)
* [Przypisywanie grup aplikacji tooan](active-directory-applications-guiding-developers-assigning-groups.md)
* [Udostępnianie kont](active-directory-sharing-accounts.md)

## <a name="integrating-custom-applications"></a>Integrowanie aplikacji niestandardowych
Jeśli pisania nowej aplikacji i deweloperów tooassist dzięki wykorzystaniu zasilania hello Azure AD, zobacz [deweloperzy Guiding](active-directory-applications-guiding-developers-for-lob-applications.md).

Jeśli chcesz tooadd Twojego toohello niestandardową aplikację galerii aplikacji Azure, zobacz ["Przynieś własne aplikacji" w konfiguracji usługi Azure AD samoobsługi SAML](http://blogs.technet.com/b/ad/archive/2015/06/17/bring-your-own-app-with-azure-ad-self-service-saml-configuration-gt-now-in-preview.aspx).

## <a name="see-also"></a>Zobacz też
* [Indeks artykułów dotyczących zarządzania aplikacjami w usłudze Azure Active Directory](active-directory-apps-index.md)

