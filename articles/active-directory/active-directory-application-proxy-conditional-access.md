---
title: "aplikacje lokalnych tooon dostępu aaaConditional — usługi Azure AD | Dokumentacja firmy Microsoft"
description: "Opisano, jak tooset dostępu warunkowego dla aplikacji można opublikować toobe dostęp zdalnie za pomocą serwera Proxy aplikacji usługi Azure AD."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 2e97722b-eb4e-4078-b607-9fed210d8a0f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/23/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro; oldportal
ms.openlocfilehash: 7bed25dd4ba17941e77d8c4b2b9ba4edcf0cf597
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-conditional-access-in-azure-ad-application-proxy"></a>Praca z dostępu warunkowego za pomocą serwera Proxy aplikacji usługi Azure AD

>[!NOTE]
>Ten artykuł dotyczy toohello klasycznego portalu Azure, która została wycofana. Zalecane jest użycie hello [portalu Azure](https://portal.azure.com). W portalu Azure hello aplikacje mają serwera Proxy aplikacji hello tej samej funkcji dostępu warunkowego jak wszystkie inne aplikacji SaaS. toolearn więcej informacji na temat dostępu warunkowego, zobacz [wprowadzenie dostępu warunkowego w usłudze Azure Active Directory](active-directory-conditional-access-azure-portal-get-started.md).

Dostęp można skonfigurować reguły toogrant dostępu warunkowego tooapplications opublikowane przy użyciu serwera Proxy aplikacji. Umożliwia to:

* Wymagaj uwierzytelniania wieloskładnikowego na aplikację
* Wymagaj uwierzytelniania wieloskładnikowego tylko wtedy, gdy użytkownicy nie są w miejscu pracy
* Uniemożliwić użytkownikom uzyskiwanie dostępu do aplikacji hello, jeśli nie są one w miejscu pracy

Te reguły mogą być zastosowane tooall użytkowników i grup lub tylko toospecific użytkowników i grup. Domyślnie hello reguła tooall użytkowników, którzy mają dostęp do aplikacji toohello. Jednak hello reguły może być również ograniczony toousers, które są członkami określonych grup zabezpieczeń.  

Reguły dostępu są oceniane, gdy użytkownik uzyskuje dostęp do aplikacji federacyjnych, która używa protokołu OAuth 2.0, OpenID Connect, SAML i WS-Federation. Ponadto reguły dostępu są oceniane przy OAuth 2.0 i OpenID Connect, gdy token odświeżania jest używane tooacquire tokenu dostępu.

## <a name="conditional-access-prerequisites"></a>Wymagania wstępne dostępu warunkowego
* Subskrypcja tooAzure Active Directory — wersja Premium
* Federacyjnych lub zarządzanego dzierżawcy usługi Azure Active Directory
* Dzierżaw federacyjnych wymusić uwierzytelnianie wieloskładnikowe (MFA)  
    ![Konfigurowanie reguł dostępu — wymusić uwierzytelnianie wieloskładnikowe](./media/active-directory-application-proxy-conditional-access/application-proxy-conditional-access.png)

## <a name="configure-per-application-multi-factor-authentication"></a>Konfigurowanie uwierzytelniania wieloskładnikowego dla każdej aplikacji
1. Zaloguj się jako administrator w hello klasycznego portalu Azure.
2. Przejdź tooActive katalog i wybierz katalog hello, w której ma zostać tooenable serwera Proxy aplikacji.
3. Kliknij przycisk **aplikacji** i przewiń w dół toohello **reguły dostępu** sekcji. sekcja reguły dostępu Hello jest wyświetlana tylko dla aplikacji publikowanych przy użyciu serwera Proxy aplikacji, które używają uwierzytelniania federacyjnego.
4. Włącz regułę hello wybierając **Włącz zasady dostępu** za**na**.
5. Określ hello użytkowników i grup toowhom powitalne Zastosuj reguły. Użyj hello **Dodaj grupę** przycisk tooselect co najmniej jedną grupę, do których jest stosowana reguła dostępu hello toowhich. To okno dialogowe może być również używane tooremove wybrane grupy.  W przypadku reguł hello toogroups tooapply wybranego hello reguły dostępu są wymuszane tylko w przypadku użytkowników, którzy należą tooone hello określony grup zabezpieczeń.  

   * Sprawdź tooexplicitly grup zabezpieczeń wykluczania z reguły hello **z wyjątkiem** i określ co najmniej jedną grupę. Użytkownicy, którzy są członkami grupy w hello z wyjątkiem listy nie są wymagane tooperform usługi Multi-Factor authentication.  
   * Jeśli użytkownik został skonfigurowany przy użyciu funkcji uwierzytelniania wieloskładnikowego na użytkownika hello, to ustawienie ma pierwszeństwo przed hello zasady uwierzytelniania wieloskładnikowego aplikacji. Użytkownik, który został skonfigurowany dla poszczególnych użytkowników usługi Multi-Factor authentication jest tooperform wymagane uwierzytelnianie wieloskładnikowe, nawet wtedy, gdy zostały zwolnione z aplikacji hello zasady uwierzytelniania wieloskładnikowego. Dowiedz się więcej o [ustawienia uwierzytelniania i dla poszczególnych użytkowników usługi Multi-Factor](../multi-factor-authentication/multi-factor-authentication.md).
6. Wybierz regułę dostępu hello, które chcesz tooset:

   * **Wymagaj uwierzytelniania wieloskładnikowego**: użytkownicy reguły dostępu toowhom stosowane są toocomplete wymagane uwierzytelnianie wieloskładnikowe, zanim podczas uzyskiwania dostępu do hello aplikacji toowhich hello reguła ma zastosowanie.
   * **Wymagaj uwierzytelniania wieloskładnikowego, gdy nie w pracy**: użytkownicy próby aplikacji hello tooaccess z zaufanych adresów IP nie są wymagane tooperform usługi Multi-Factor authentication. Witaj zaufany, zakresów adresów IP można skonfigurować na stronie ustawień usługi Multi-Factor authentication hello.
   * **Blokowanie dostępu, gdy nie w pracy**: próby tooaccess aplikacji hello spoza sieci firmowej użytkownicy nie będą mogli tooaccess aplikacji hello.

## <a name="configuring-mfa-for-federation-services"></a>Konfigurowanie uwierzytelniania MFA dla usług federacyjnych
W przypadku dzierżaw federacyjnych, uwierzytelnianie wieloskładnikowe (MFA) mogą być wykonywane przez usługę Azure Active Directory lub hello lokalnego serwera usług AD FS. Domyślnie uwierzytelnianie wieloskładnikowe jest przeprowadzana na każdej stronie hostowanej przez usługę Azure Active Directory. tooconfigure MFA lokalnie, uruchom środowisko Windows PowerShell i użyj hello SupportsMFA — właściwość tooset hello modułu Azure AD.

Witaj poniższy przykład przedstawia sposób tooenable lokalnej usługi MFA za pomocą hello [polecenia cmdlet Set-MsolDomainFederationSettings](https://msdn.microsoft.com/library/azure/dn194088.aspx) na powitania contoso.com dzierżawy:`Set-MsolDomainFederationSettings -DomainName contoso.com -SupportsMFA $true `

W toosetting dodanie tej flagi hello dzierżawy federacyjnych usług AD FS wystąpienie musi być skonfigurowany tooperform usługi Multi-Factor authentication. Wykonaj instrukcje hello [wdrażanie Microsoft Azure Multi-Factor authentication lokalnymi](../multi-factor-authentication/multi-factor-authentication-get-started-server.md).

## <a name="see-also"></a>Zobacz też
* [Praca z aplikacjami obsługującymi oświadczenia](active-directory-application-proxy-claims-aware-apps.md)
* [Publikowanie aplikacji przy użyciu serwera Proxy aplikacji](active-directory-application-proxy-publish.md)
* [Włączanie logowania jednokrotnego](active-directory-application-proxy-sso-using-kcd.md)
* [Publikowanie aplikacji przy użyciu własnej nazwy domeny](active-directory-application-proxy-custom-domains.md)

Najnowsze wiadomości powitania i aktualizacji, zapoznaj się z hello [Blog dotyczący serwera Proxy aplikacji](http://blogs.technet.com/b/applicationproxyblog/)
