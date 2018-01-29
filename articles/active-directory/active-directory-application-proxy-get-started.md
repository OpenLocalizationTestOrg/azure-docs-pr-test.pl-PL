---
title: "Jak zapewnić bezpieczny zdalny dostęp do aplikacji lokalnych"
description: "Uwzględniono również sposób Użyj serwera Proxy aplikacji usługi Azure AD, aby zapewnić bezpieczny zdalny dostęp do aplikacji lokalnych."
services: active-directory
documentationcenter: 
author: daveba
manager: mtillman
ms.assetid: d5450da1-9e06-4d08-8146-011c84922ab5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: daveba
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 24def898f282c4e122ae53932ae86047e815595c
ms.sourcegitcommit: 3cdc82a5561abe564c318bd12986df63fc980a5a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/05/2018
---
# <a name="how-to-provide-secure-remote-access-to-on-premises-applications"></a>Jak zapewnić bezpieczny zdalny dostęp do aplikacji lokalnych

Obecnie pracownicy chcą produktywność w dowolnym miejscu w dowolnym momencie i na dowolnym urządzeniu. Chcą pracy na ich własnych urządzeń, czy są to tablety, telefony lub komputery przenośne. I ich oczekują mogły uzyskiwać dostęp do swoich aplikacji, obie aplikacje SaaS w chmurze i lokalne aplikacje firmowe. Zapewniając dostęp do aplikacji lokalnych tradycyjnie został użyty, wirtualnych sieci prywatnych (VPN) lub stref zdemilitaryzowaną (sieci DMZ). Nie tylko są tych rozwiązań, złożone i trudne do zwiększania bezpieczeństwa, ale są kosztowne do konfigurowania i zarządzania nią.

Brak lepiej!

Nowoczesne pracowników w pierwszym mobile, world pierwszy chmury musi rozwiązanie nowoczesnych dostępu zdalnego. Serwer Proxy aplikacji usługi Azure AD to funkcja usługi Azure Active Directory, która oferuje dostępu zdalnego jako usługi. Oznacza to, że jest łatwa do wdrożenia, użyj i zarządzanie nimi.

[!INCLUDE [identity](../../includes/azure-ad-licenses.md)]

## <a name="what-is-azure-active-directory-application-proxy"></a>Co to jest serwer Proxy usługi Azure Active Directory aplikacji?
Serwer Proxy aplikacji usługi Azure AD zapewnia rejestracji jednokrotnej (SSO) i bezpieczny dostęp zdalny dla aplikacji sieci web hostowane lokalnie. Niektóre aplikacje, które chcesz opublikować obejmują witryn programu SharePoint, Outlook Web Access lub jakiekolwiek inne aplikacje sieci web LOB, które masz. Te lokalnych aplikacji sieci web są zintegrowane z usługą Azure AD, w tej samej tożsamości i kontroli platformy, który jest używany przez usługi Office 365. Użytkownicy końcowi można uzyskać dostępu do aplikacji lokalnych taki sam sposób uzyskiwania dostępu do usług O365 i innych aplikacji SaaS zintegrowanych z usługą Azure AD. Nie trzeba zmienić infrastruktury sieciowej, lub wymagać sieci VPN do rozwiązaniem dla użytkowników.

## <a name="why-is-application-proxy-a-better-solution"></a>Dlaczego jest serwer Proxy aplikacji lepszym rozwiązaniem?
Serwer Proxy aplikacji usługi Azure AD zapewnia rozwiązanie proste, bezpieczną i ekonomicznego dostępu zdalnego do aplikacji lokalnych.

Serwer Proxy aplikacji usługi Azure AD jest:

* **Proste**
   * Nie ma potrzeby zmiany lub aktualizacji aplikacji do pracy z serwerem Proxy aplikacji. 
   * Użytkownicy pobierają obsługi uwierzytelniania zgodne. Będą mogli używać portalu MyApps, aby uzyskać rejestracji jednokrotnej do obu aplikacji SaaS w chmurze i aplikacjami lokalnymi. 
* **Bezpieczeństwo**
   * Podczas publikowania aplikacji przy użyciu serwera Proxy aplikacji usługi Azure AD, możesz można korzystać z formantów sformatowanego autoryzacji i analiza zabezpieczeń w usłudze Azure. Otrzymasz skali chmury zabezpieczeń i funkcji zabezpieczeń platformy Azure, takich jak warunkowego dostępu i dwuetapowej weryfikacji.
   * Nie masz otworzyć wszystkie połączenia przychodzące za zaporą, aby zapewnić użytkownikom dostęp zdalny. 
* **Ekonomiczne**
   * Serwer Proxy aplikacji działa w chmurze, więc można oszczędzić czas i pieniądze. Lokalnymi rozwiązaniami zwykle wymagają konfiguracji i utrzymania sieci DMZ, serwery krawędzi lub innych złożonych infrastruktury.  

## <a name="what-kind-of-applications-work-with-application-proxy"></a>Jakiego rodzaju aplikacje korzystają z serwera Proxy aplikacji?
Serwer Proxy aplikacji usługi Azure AD umożliwia dostęp do różnych typów wewnętrznych aplikacji:

* Aplikacje, które używają sieci Web [zintegrowane uwierzytelnianie systemu Windows](active-directory-application-proxy-sso-using-kcd.md) do uwierzytelniania  
* Aplikacje używające opartych na formularzach sieci Web lub [na podstawie nagłówka](application-proxy-ping-access.md) dostępu  
* Interfejsy API, które chcesz udostępnić do rozbudowanych aplikacji na różnych urządzeniach w sieci Web  
* Aplikacje wymagające za [bramy usług pulpitu zdalnego](application-proxy-publish-remote-desktop.md)  
* Aplikacje klienta sformatowanego, które są zintegrowane z Active Directory Authentication Library (ADAL)

## <a name="how-does-application-proxy-work"></a>Jak działa serwer Proxy aplikacji?
Istnieją dwa składniki, które trzeba skonfigurować, aby serwer Proxy aplikacji działa: łącznika i zewnętrznego punktu końcowego. 

Łącznik jest lekki agenta, która znajduje się w systemie Windows Server w sieci. Łącznik umożliwia przepływ ruchu z usługi Serwer Proxy aplikacji w chmurze do aplikacji lokalnej. Funkcja ta używa tylko połączeń wychodzących, dzięki czemu nie trzeba otworzyć żadnych portów przychodzących lub umieść niczego w strefie DMZ. Łączniki są bezstanowych i pobierania informacji o chmurze odpowiednio do potrzeb. Aby uzyskać więcej informacji na temat łączników, takich jak jak one Równoważenie obciążenia i uwierzytelniania, zobacz [łączniki serwera Proxy aplikacji usługi AD zrozumieć Azure](application-proxy-understand-connectors.md). 

Zewnętrznego punktu końcowego jest, jak użytkownicy osiągnąć aplikacji znajduje się poza siecią. Albo może przejść bezpośrednio do zewnętrznego adresu URL, który należy określić lub za pośrednictwem portalu MyApps one dostęp do aplikacji. Użytkownicy, przejdź do jednego z tych punktów końcowych, uwierzytelniania w usłudze Azure AD i następnie są kierowane za pośrednictwem łącznika do aplikacji lokalnych.

 ![Diagram AzureAD serwera Proxy aplikacji](./media/active-directory-application-proxy-get-started/azureappproxxy.png)

1. Użytkownik uzyskuje dostęp do aplikacji za pośrednictwem serwera Proxy aplikacji usługi i jest kierowany do strony logowania usługi Azure AD do uwierzytelniania.
2. Po pomyślnym zalogowaniu token jest wygenerowane i wysłane do urządzenia klienckiego.
3. Klient wysyła ten token do serwera Proxy aplikacji usługi, która pobiera głównej nazwy użytkownika (UPN) i nazwy podmiotu zabezpieczeń (SPN) z tokenu, a następnie przekierowuje żądanie do łącznika serwera Proxy aplikacji.
4. Jeśli skonfigurowano rejestracji jednokrotnej, łącznik wykonuje wszelkie dodatkowe uwierzytelnianie wymagane w imieniu użytkownika.
5. Łącznik wysyła żądanie do aplikacji lokalnych.  
6. Odpowiedź jest wysyłana za pośrednictwem serwera Proxy aplikacji usługi i łącznika do użytkownika.

### <a name="single-sign-on"></a>Logowanie jednokrotne
Serwer Proxy aplikacji usługi Azure AD zapewnia rejestracji jednokrotnej (SSO) do aplikacji używających zintegrowanego uwierzytelniania systemu Windows (IWA) lub aplikacje obsługujące oświadczenia. Jeśli aplikacja korzysta z funkcji IWA, serwer Proxy aplikacji personifikuje użytkownika przy użyciu ograniczone delegowanie protokołu Kerberos w celu zapewnienia logowania jednokrotnego. Jeśli masz aplikacji obsługującej oświadczenia, które ufają usłudze Azure Active Directory, logowania jednokrotnego działa, ponieważ został już uwierzytelniony przez usługę Azure AD.

Aby uzyskać więcej informacji o protokole Kerberos, zobacz [wszystkich chcesz wiedzieć o protokołu Kerberos ograniczonego delegowania (KCD)](https://blogs.technet.microsoft.com/applicationproxyblog/2015/09/21/all-you-want-to-know-about-kerberos-constrained-delegation-kcd).

### <a name="managing-apps"></a>Zarządzanie aplikacjami
Po opublikowaniu aplikacji za pomocą serwera Proxy aplikacji można zarządzać nim jak każda inna aplikacja przedsiębiorstwa w portalu Azure. Można za pomocą funkcji zabezpieczeń usługi Azure Active Directory, takie jak warunkowego dostępu i dwuetapowej weryfikacji, kontrolować uprawnienia użytkowników i Dostosuj znakowanie dla aplikacji. 

## <a name="get-started"></a>Rozpoczęcie pracy

Przed skonfigurowaniem serwera Proxy aplikacji upewnij się, że masz obsługiwaną [edition usługi Azure Active Directory](https://azure.microsoft.com/pricing/details/active-directory/) i katalog usługi Azure AD, dla którego jesteś administratorem globalnym.

Rozpoczynanie pracy z serwerem Proxy aplikacji w dwóch krokach:

1. [Włączanie serwera Proxy aplikacji i skonfigurować łącznik](active-directory-application-proxy-enable.md).    
2. [Publikowanie aplikacji](active-directory-application-proxy-publish.md) — Użyj Kreatora szybki i łatwy do pobrania aplikacji lokalnej opublikowanych i jest dostępny zdalnie.

## <a name="whats-next"></a>Co dalej?
Po opublikowaniu pierwszej aplikacji, istnieje wiele innych, które można wykonać przy użyciu serwera Proxy aplikacji:

* [Włączanie logowania jednokrotnego](active-directory-application-proxy-sso-using-kcd.md)
* [Publikowanie aplikacji przy użyciu własnej nazwy domeny](active-directory-application-proxy-custom-domains.md)
* [Więcej informacji na temat łączników serwera Proxy aplikacji usługi Azure AD](application-proxy-understand-connectors.md)
* [Praca z istniejących lokalnych serwerów Proxy](application-proxy-working-with-proxy-servers.md) 
* [Ustaw niestandardową stronę główną](application-proxy-office365-app-launcher.md)

Aby zapoznać się z najnowszymi informacjami i aktualizacjami, zobacz [blog dotyczący serwera proxy aplikacji](http://blogs.technet.com/b/applicationproxyblog/)

