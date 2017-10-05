---
title: "Azure dostępu warunkowego dla aplikacji SaaS | Dokumentacja firmy Microsoft"
description: "Dostęp warunkowy w usłudze Azure AD umożliwia konfigurowanie reguł dostępu do poszczególnych aplikacji usługi Multi-Factor authentication i możliwość blokowania dostępu dla użytkowników nie znajduje się w zaufanej sieci. "
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 51a1ee61-3ffe-4f65-b8de-ff21903e1e74
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/07/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: efaa70467346e910a78a63d182041029bb34b1cc
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="getting-started-with-azure-active-directory-conditional-access"></a>Wprowadzenie do korzystania z usługi Azure Active Directory dostępu warunkowego
Azure Active Directory dostępu warunkowego dla [SaaS](https://azure.microsoft.com/overview/what-is-saas/) aplikacje i usługi Azure AD połączone umożliwia aplikacji skonfigurowanie dostępu warunkowego na podstawie grupy, lokalizacji i czułości aplikacji. 

Przy użyciu dostępu warunkowego w oparciu czułości aplikacji można ustawić reguły dostępu do usługi Multi-Factor authentication (MFA) na aplikację. Uwierzytelnianie wieloskładnikowe na aplikację pozwala, aby blokowały dostęp dla użytkowników, którzy nie znajdują się w zaufanej sieci. Zasady MFA można stosować do wszystkich użytkowników, które są przypisane do aplikacji lub tylko dla użytkowników z określonych grup zabezpieczeń.  Użytkownicy mogą być wyłączone z wymaganie usługi MFA, jeśli uzyskują dostęp do aplikacji z adresu IP, który znajduje się w sieci organizacji.

Te funkcje będą dostępne do klientów, którzy kupili licencji usługi Azure Active Directory Premium.

## <a name="scenario-prerequisites"></a>Warunki wstępne scenariusza
* Licencja usługi Azure Active Directory — wersja Premium
* Federacyjnych lub zarządzanego dzierżawcy usługi Azure Active Directory
* Dzierżaw federacyjnych wymaga włączenia uwierzytelniania wieloskładnikowego.

## <a name="configure-per-application-access-rules"></a>Konfigurowanie reguł dostępu dla poszczególnych aplikacji
W tej sekcji opisano, jak skonfigurować zasady dostępu do poszczególnych aplikacji.

1. Zaloguj się do klasycznego portalu Azure przy użyciu konta administratora globalnego dla usługi Azure AD.
2. W lewym okienku wybierz pozycję **Active Directory**.
3. Na karcie Katalog wybierz swój katalog.
4. Wybierz **aplikacji** kartę.
5. Wybierz aplikację, która zostanie ustawiony reguły.
6. Wybierz kartę **Konfigurowanie**.
7. Przewiń w dół do sekcji reguły dostępu. Wybierz regułę żądany dostęp.
8. Określ użytkowników, których dotyczą reguły.
9. Włącz zasady, wybierając **włączone na**.

## <a name="understanding-access-rules"></a>Opis reguł dostępu
W tej sekcji przedstawiono szczegółowy opis reguły dostępu, obsługiwane w Azure warunkowego dostępu do aplikacji.

### <a name="specifying-the-users-the-access-rules-apply-to"></a>Określając użytkowników, zastosować reguły dostępu do
Domyślnie zasady będą stosowane do wszystkich użytkowników, którzy mają dostęp do aplikacji. Jednak można również ograniczyć zasad dla użytkowników, którzy są członkami określonych grup zabezpieczeń. **Dodaj grupę** przycisk służy do wybierania jednej lub kilku grup z okna dialogowego wyboru grupy, którego będzie dotyczyć reguła dostępu. W tym oknie dialogowym można również usunąć wybrane grupy. Po wybraniu opcji zasady stosowane do grupy, zasady dostępu tylko zostaną wymuszone dla użytkowników, którzy należą do jednej z określonych grup zabezpieczeń.

Grup zabezpieczeń może również być jawnie wykluczony z zasad, wybierając **z wyjątkiem** opcja i określenie co najmniej jedną grupę. Użytkownicy, którzy są członkami grupy w **z wyjątkiem** listy nie będą poddawani uwierzytelnianiu wymagania dotyczące uwierzytelniania wieloskładnikowego, nawet jeśli należą do grupy, która jest stosowana reguła dostępu do.
Reguły dostępu, pokazano poniżej wymaga wszyscy użytkownicy w grupie menedżerów uwierzytelniania wieloskładnikowego podczas uzyskiwania dostępu do aplikacji.

![Ustawienie zasad dostępu warunkowego za pomocą usługi MFA](./media/active-directory-conditional-access-azuread-connected-apps/conditionalaccess-saas-apps.png)

## <a name="conditional-access-rules-with-mfa"></a>Zasady dostępu warunkowego za pomocą usługi MFA
Jeśli użytkownik został skonfigurowany przy użyciu funkcji uwierzytelniania wieloskładnikowego na użytkownika, to ustawienie na użytkownika zostaną połączone z zasadami uwierzytelniania wieloskładnikowego aplikacji. Oznacza to, że użytkownik, który został skonfigurowany dla poszczególnych użytkowników usługi Multi-Factor authentication będą musieli wykonać uwierzytelnianie wieloskładnikowe, nawet wtedy, gdy zostały zwolnione z zasadami uwierzytelniania wieloskładnikowego aplikacji. Dowiedz się więcej o ustawieniach usługi Multi-Factor authentication i użytkownika.

### <a name="access-rule-options"></a>Opcje reguły dostępu
Obsługiwane są następujące opcje:

* **Wymagaj uwierzytelniania wieloskładnikowego**: użytkownicy, do których stosowane reguły dostępu, będą musieli pełną uwierzytelnianie wieloskładnikowe przed uzyskaniem dostępu do aplikacji, która dotyczy zasada.
* **Wymagaj uwierzytelniania wieloskładnikowego, gdy nie w pracy**: użytkownika, które pochodzą z zaufanego adresu IP nie będą wymagane do przeprowadzenia uwierzytelniania wieloskładnikowego. Zaufany zakresów adresów IP można skonfigurować na stronie Ustawienia usługi Multi-Factor authentication.
* **Blokowanie dostępu, gdy nie w pracy**: użytkownik, który nie pochodzi z zaufanego adresu IP będą blokowane. Zaufany zakresów adresów IP można skonfigurować na stronie Ustawienia usługi Multi-Factor authentication.

### <a name="setting-rule-status"></a>Stan zasady ustawienia
Stan zasady dostępu umożliwia włączanie reguł i wyłączanie. Gdy zasady dostępu są wyłączone, wymagania dotyczące uwierzytelniania wieloskładnikowego nie jest wymuszana.

### <a name="access-rule-evaluation"></a>Szacowanie reguły dostępu
Reguły dostępu są oceniane, gdy użytkownik uzyskuje dostęp do aplikacji federacyjnych, która używa protokołu OAuth 2.0, OpenID Connect, SAML i WS-Federation. Ponadto reguły dostępu są oceniane OAuth 2.0 i OpenID Connect używania token odświeżania, można uzyskać tokenu dostępu. Jeśli ocena zasad nie powiedzie się, gdy używany jest token odświeżania, błąd **invalid_grant** zostaną zwrócone, oznacza to, użytkownik musi ponownie uwierzytelniony do klienta.

### <a name="configure-federation-services-to-provide-multi-factor-authentication"></a>Konfigurowanie usług federacyjnych w celu zapewnienia uwierzytelniania wieloskładnikowego
W przypadku dzierżaw federacyjnych, uwierzytelnianie wieloskładnikowe może być wykonana przez usługi Azure Active Directory lub lokalnej serwera usług AD FS.

Domyślnie uwierzytelnianie wieloskładnikowe zostanie przeprowadzona na stronie hostowanej przez usługę Azure Active Directory. Aby skonfigurować uwierzytelnianie wieloskładnikowe w infrastrukturze lokalnej, **— SupportsMFA** musi mieć ustawioną właściwość **true** w usłudze Azure Active Directory, przy użyciu modułu Azure AD dla programu Windows PowerShell.

Poniższy przykład pokazuje, jak włączyć uwierzytelnianie wieloskładnikowe lokalnymi przy użyciu [polecenia cmdlet Set-MsolDomainFederationSettings](https://msdn.microsoft.com/library/azure/dn194088.aspx) dzierżawcy contoso.com:

    Set-MsolDomainFederationSettings -DomainName contoso.com -SupportsMFA $true

Oprócz ustawienia tej flagi, należy skonfigurować wystąpienie dzierżawy federacyjnej AD FS przeprowadzać uwierzytelnianie wieloskładnikowe. Postępuj zgodnie z instrukcjami dotyczącymi [wdrażanie usługi Azure Multi-Factor Authentication lokalnymi](../multi-factor-authentication/multi-factor-authentication-get-started-server.md).

## <a name="related-articles"></a>Pokrewne artykuły
* [Zabezpieczanie dostępu do usługi Office 365 i innych aplikacji podłączone do usługi Azure Active Directory](active-directory-conditional-access.md)
* [Indeks artykułów dotyczących zarządzania aplikacjami w usłudze Azure Active Directory](active-directory-apps-index.md)

