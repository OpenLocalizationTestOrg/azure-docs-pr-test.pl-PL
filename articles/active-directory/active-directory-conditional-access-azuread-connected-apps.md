---
title: "Dostęp warunkowy dla aplikacji SaaS aaaAzure | Dokumentacja firmy Microsoft"
description: "Dostępu warunkowego w usłudze Azure AD pozwala na powitania możliwości tooblock dostęp i możesz tooconfigure uwierzytelnianie wieloskładnikowe dla poszczególnych aplikacji reguł dostępu dla użytkowników nie znajduje się w zaufanej sieci. "
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
ms.openlocfilehash: 69748014c0c8e266ba66562980c784aba4c68d80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-active-directory-conditional-access"></a>Wprowadzenie do korzystania z usługi Azure Active Directory dostępu warunkowego
Azure Active Directory dostępu warunkowego dla [SaaS](https://azure.microsoft.com/overview/what-is-saas/) aplikacje i usługi Azure AD połączone umożliwia aplikacji skonfigurowanie dostępu warunkowego na podstawie grupy, lokalizacji i czułości aplikacji. 

Przy użyciu dostępu warunkowego w oparciu czułości aplikacji można ustawić reguły dostępu do usługi Multi-Factor authentication (MFA) na aplikację. Uwierzytelnianie wieloskładnikowe na aplikację udostępnia hello możliwości tooblock dla użytkowników, którzy nie znajdują się w zaufanej sieci. Możesz zastosować MFA reguły tooall użytkowników, którzy są przypisane toohello aplikacji lub tylko dla użytkowników z określonych grup zabezpieczeń.  Użytkownicy mogą być wyłączone z hello wymaganie usługi MFA, jeśli uzyskują dostęp do aplikacji hello z adresu IP, który znajduje się w sieci organizacji hello.

Te funkcje będą dostępne toocustomers, który zakupionych licencji usługi Azure Active Directory Premium.

## <a name="scenario-prerequisites"></a>Warunki wstępne scenariusza
* Licencja usługi Azure Active Directory — wersja Premium
* Federacyjnych lub zarządzanego dzierżawcy usługi Azure Active Directory
* Dzierżaw federacyjnych wymaga włączenia uwierzytelniania wieloskładnikowego.

## <a name="configure-per-application-access-rules"></a>Konfigurowanie reguł dostępu dla poszczególnych aplikacji
W tej sekcji opisano, jak uzyskać dostęp do aplikacji tooconfigure reguły.

1. Zaloguj się toohello klasycznego portalu Azure przy użyciu konta administratora globalnego dla usługi Azure AD.
2. W okienku po lewej stronie powitania wybierz **usługi Active Directory**.
3. Na karcie katalogu hello wybierz swój katalog.
4. Wybierz hello **aplikacji** kartę.
5. Wybierz hello aplikacji hello reguły zostaną ustawione dla.
6. Wybierz hello **Konfiguruj** kartę.
7. Przewiń w dół do sekcji reguły dostępu toohello. Wybierz regułę dostępu do żądanego hello.
8. Określ użytkowników hello hello reguła będzie dotyczyć.
9. Włącz zasady hello wybierając **włączone toobe**.

## <a name="understanding-access-rules"></a>Opis reguł dostępu
W tej sekcji przedstawiono szczegółowy opis reguły dostępu hello obsługiwane w hello Azure warunkowego dostępu do aplikacji.

### <a name="specifying-hello-users-hello-access-rules-apply-to"></a>Określanie użytkowników hello hello dostępu, które mają zastosowanie reguły
Domyślnie hello zasady będą stosowane tooall użytkowników, którzy mają dostęp do aplikacji toohello. Jednak można również ograniczyć hello toousers zasad, które są członkami hello określonych grup zabezpieczeń. Witaj **Dodaj grupę** przycisk jest używane tooselect, jeden lub więcej grup z okna dialogowego wyboru grupy hello, które hello reguły dostępu będą stosowane do. To okno dialogowe może być również używane tooremove wybrane grupy. W przypadku reguł hello tooGroups tooapply wybranego hello reguły dostępu tylko zostaną wymuszone dla użytkowników, którzy należą tooone hello określone grupy zabezpieczeń.

Grup zabezpieczeń można również być jawnie wykluczony z zasad hello wybierając hello **z wyjątkiem** opcja i określenie co najmniej jedną grupę. Użytkownicy, którzy są członkami grupy w hello **z wyjątkiem** lista nie będzie wymagania dotyczące uwierzytelniania wieloskładnikowego toohello podmiotu, nawet jeśli należą do grupy tej reguły dostępu hello dotyczy.
reguły dostępu Hello pokazano poniżej wymaga wszyscy użytkownicy w hello menedżerów grupy toouse usługi Multi-Factor authentication podczas uzyskiwania dostępu do aplikacji hello.

![Ustawienie zasad dostępu warunkowego za pomocą usługi MFA](./media/active-directory-conditional-access-azuread-connected-apps/conditionalaccess-saas-apps.png)

## <a name="conditional-access-rules-with-mfa"></a>Zasady dostępu warunkowego za pomocą usługi MFA
Jeśli użytkownik został skonfigurowany przy użyciu funkcji uwierzytelniania wieloskładnikowego na użytkownika hello, to ustawienie na powitania użytkownika połączy się z zasadami uwierzytelniania wieloskładnikowego hello aplikacji hello. Oznacza to, że użytkownik, który został skonfigurowany dla poszczególnych użytkowników usługi Multi-Factor authentication będzie wymagane tooperform usługi Multi-Factor authentication, nawet jeśli zostały zwolnione z zasadami uwierzytelniania wieloskładnikowego aplikacji hello. Dowiedz się więcej o ustawieniach usługi Multi-Factor authentication i użytkownika.

### <a name="access-rule-options"></a>Opcje reguły dostępu
obsługiwane są następujące opcje Hello:

* **Wymagaj uwierzytelniania wieloskładnikowego**: hello użytkownicy mają zastosowanie reguły dostępu hello toowhom toocomplete wymagane uwierzytelnianie wieloskładnikowe zanim będą podczas uzyskiwania dostępu do aplikacji hello hello zasad dotyczy.
* **Wymagaj uwierzytelniania wieloskładnikowego, gdy nie w pracy**: użytkownika, które pochodzą z zaufanego adresu IP nie będzie wymagane tooperform usługi Multi-Factor authentication. Witaj zaufany, zakresów adresów IP można skonfigurować na stronie ustawień usługi Multi-Factor authentication hello.
* **Blokowanie dostępu, gdy nie w pracy**: użytkownik, który nie pochodzi z zaufanego adresu IP będą blokowane. Witaj zaufany, zakresów adresów IP można skonfigurować na stronie ustawień usługi Multi-Factor authentication hello.

### <a name="setting-rule-status"></a>Stan zasady ustawienia
Stan zasady dostępu umożliwia włączanie reguł hello lub wyłączanie. Gdy hello reguły dostępu są wyłączone, wymagania dotyczące uwierzytelniania wieloskładnikowego hello nie jest wymuszana.

### <a name="access-rule-evaluation"></a>Szacowanie reguły dostępu
Reguły dostępu są oceniane, gdy użytkownik uzyskuje dostęp do aplikacji federacyjnych, która używa protokołu OAuth 2.0, OpenID Connect, SAML i WS-Federation. Ponadto reguły dostępu są oceniane przy hello OAuth 2.0 OpenID Connect przy użyciu tokenu tooacquire odświeżenie tokenu dostępu. Jeśli ocena zasad nie powiedzie się, gdy jest używany token odświeżania, hello błąd **invalid_grant** zostaną zwrócone, oznacza to, użytkownik hello musi toore-uwierzytelniania toohello klienta.

### <a name="configure-federation-services-tooprovide-multi-factor-authentication"></a>Konfigurowanie uwierzytelniania wieloskładnikowego tooprovide usługi federacyjnej
W przypadku dzierżaw federacyjnych, uwierzytelnianie wieloskładnikowe może być wykonana przez usługi Azure Active Directory lub hello lokalnego serwera usług AD FS.

Domyślnie uwierzytelnianie wieloskładnikowe zostanie przeprowadzona na stronie hostowanej przez usługę Azure Active Directory. Witaj tooconfigure MFA lokalnymi, **— SupportsMFA** należy również ustawić właściwość**true** w usłudze Azure Active Directory, przy użyciu modułu hello Azure AD dla programu Windows PowerShell.

Witaj poniższy przykład przedstawia sposób tooenable lokalnej usługi MFA za pomocą hello [polecenia cmdlet Set-MsolDomainFederationSettings](https://msdn.microsoft.com/library/azure/dn194088.aspx) na powitania contoso.com dzierżawy:

    Set-MsolDomainFederationSettings -DomainName contoso.com -SupportsMFA $true

W toosetting dodanie tej flagi hello dzierżawy federacyjnych usług AD FS wystąpienie musi być skonfigurowany tooperform usługi Multi-Factor authentication. Wykonaj instrukcje hello [wdrażanie usługi Azure Multi-Factor Authentication lokalnymi](../multi-factor-authentication/multi-factor-authentication-get-started-server.md).

## <a name="related-articles"></a>Pokrewne artykuły
* [Zabezpieczanie dostępu tooOffice 365 i innych aplikacji połączone tooAzure usługi Active Directory](active-directory-conditional-access.md)
* [Indeks artykułów dotyczących zarządzania aplikacjami w usłudze Azure Active Directory](active-directory-apps-index.md)

