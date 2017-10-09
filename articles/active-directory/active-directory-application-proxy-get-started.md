---
title: "aaaHow tooprovide bezpieczny dostęp zdalny tooon lokalnej aplikacji"
description: "Opisano sposób toouse serwera Proxy aplikacji usługi Azure AD tooprovide bezpieczny dostęp zdalny tooyour lokalnej aplikacji."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: d5450da1-9e06-4d08-8146-011c84922ab5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 289e970ed0596fcd06ccf6b2ad92203366fbb494
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooprovide-secure-remote-access-tooon-premises-applications"></a>Jak tooprovide bezpiecznego dostępu zdalnego tooon lokalnej aplikacji

Dzisiaj żądają toobe produktywności w dowolnym miejscu w dowolnym momencie i na dowolnym urządzeniu. Chcą toowork na ich własnych urządzeń, czy są to tablety, telefony lub komputery przenośne. I oczekiwane tooaccess stanie toobe swoje aplikacje zarówno aplikacje firmowe, jak i aplikacji SaaS w chmurze hello lokalnymi. Zapewnianie dostępu lokalnego tooon aplikacji został użyty tradycyjnie wirtualnych sieci prywatnych (VPN) lub stref zdemilitaryzowaną (sieci DMZ). Nie tylko są bezpieczne toomake złożone i twardych te rozwiązania, ale są kosztowne tooset uruchomione i zarządzanie nimi.

Brak lepiej!

Nowoczesne pracowników w pierwszy mobile hello, world pierwszy chmury musi rozwiązanie nowoczesnych dostępu zdalnego. Serwer Proxy aplikacji usługi Azure AD to funkcja usługi Azure Active Directory, która oferuje dostępu zdalnego jako usługi. Oznacza to, że jest łatwe toodeploy, użyj i zarządzania.

[!INCLUDE [identity](../../includes/azure-ad-licenses.md)]

## <a name="what-is-azure-active-directory-application-proxy"></a>Co to jest serwer Proxy usługi Azure Active Directory aplikacji?
Serwer Proxy aplikacji usługi Azure AD zapewnia rejestracji jednokrotnej (SSO) i bezpieczny dostęp zdalny dla aplikacji sieci web hostowane lokalnie. Niektóre aplikacje byłaby wskazana toopublish obejmują witryn programu SharePoint, Outlook Web Access lub jakiekolwiek inne aplikacje sieci web LOB, które masz. Te lokalnej sieci web, które aplikacje są zintegrowane z usługą Azure AD, hello tej samej tożsamości i kontrola platformy, który jest używany przez usługi Office 365. Użytkownicy końcowi mają dostęp do sieci lokalnej aplikacji hello, taki sam sposób uzyskiwania dostępu do usług O365 i innych aplikacji SaaS zintegrowanych z usługą Azure AD. Nie należy infrastruktury sieciowej hello toochange lub wymagają tego rozwiązania tooprovide sieci VPN dla użytkowników.

## <a name="why-is-application-proxy-a-better-solution"></a>Dlaczego jest serwer Proxy aplikacji lepszym rozwiązaniem?
Serwera Proxy aplikacji usługi Azure AD zapewnia tooall rozwiązania proste, bezpieczną i ekonomicznego dostępu zdalnego aplikacji lokalnych.

Serwer Proxy aplikacji usługi Azure AD jest:

* **Proste**
   * Nie należy toochange lub zaktualizuj toowork Twojej aplikacji za pomocą serwera Proxy aplikacji. 
   * Użytkownicy pobierają obsługi uwierzytelniania zgodne. Odbiorca może użyć aplikacji SaaS tooboth hello MyApps tooget portalu rejestracji jednokrotnej w chmurze hello i aplikacjami lokalnymi. 
* **Bezpieczeństwo**
   * Podczas publikowania aplikacji przy użyciu serwera Proxy aplikacji usługi Azure AD można wykorzystasz formanty autoryzacji sformatowanego hello i analiza zabezpieczeń w systemie Azure. Otrzymasz skali chmury zabezpieczeń i funkcji zabezpieczeń platformy Azure, takich jak warunkowego dostępu i dwuetapowej weryfikacji.
   * Nie masz tooopen wszystkie połączenia przychodzące za pośrednictwem sieci toogive zapory użytkowników dostępu zdalnego. 
* **Ekonomiczne**
   * Serwer Proxy aplikacji działa w chmurze hello, można oszczędzić czas i pieniądze. Rozwiązania lokalnego zwykle wymagają tooset się i obsługa sieci DMZ, serwery krawędzi lub innych złożonych infrastruktury.  

## <a name="what-kind-of-applications-work-with-application-proxy"></a>Jakiego rodzaju aplikacje korzystają z serwera Proxy aplikacji?
Serwer Proxy aplikacji usługi Azure AD umożliwia dostęp do różnych typów wewnętrznych aplikacji:

* Aplikacje, które używają sieci Web [zintegrowane uwierzytelnianie systemu Windows](active-directory-application-proxy-sso-using-kcd.md) do uwierzytelniania  
* Aplikacje używające opartych na formularzach sieci Web lub [na podstawie nagłówka](application-proxy-ping-access.md) dostępu  
* Interfejsy API, które mają tooexpose toorich aplikacji na różnych urządzeniach w sieci Web  
* Aplikacje wymagające za [bramy usług pulpitu zdalnego](application-proxy-publish-remote-desktop.md)  
* Aplikacje klienta sformatowanego, które są zintegrowane z usługą hello Active Directory Authentication Library (ADAL)

## <a name="how-does-application-proxy-work"></a>Jak działa serwer Proxy aplikacji?
Istnieją dwa składniki należy toomake tooconfigure pracy serwera Proxy aplikacji: łącznika i zewnętrznego punktu końcowego. 

Łącznik Hello jest lekki agenta, która znajduje się w systemie Windows Server w sieci. Łącznik Hello ułatwia hello przepływ ruchu z hello usługi Serwer Proxy aplikacji hello chmury tooyour aplikacji w lokalnym programie. Funkcja ta używa tylko połączeń wychodzących, dlatego nie masz żadnych portów przychodzących tooopen lub umieść niczego w strefie DMZ hello. łączniki Hello są bezstanowych i pobierania informacji o chmurze hello odpowiednio do potrzeb. Aby uzyskać więcej informacji na temat łączników, takich jak jak one Równoważenie obciążenia i uwierzytelniania, zobacz [łączniki serwera Proxy aplikacji usługi AD zrozumieć Azure](application-proxy-understand-connectors.md). 

Hello zewnętrznego punktu końcowego jest, jak użytkownicy osiągnąć aplikacji znajduje się poza siecią. Może albo przejść bezpośrednio tooan zewnętrzny adres URL, który należy określić lub uzyskać dostęp do aplikacji hello za pośrednictwem portalu MyApps hello. Użytkownicy przejść tooone tymi punktami końcowymi, uwierzytelniania w usłudze Azure AD i następnie są wysyłane za pośrednictwem hello łącznika toohello lokalnej aplikacji.

 ![Diagram AzureAD serwera Proxy aplikacji](./media/active-directory-application-proxy-get-started/azureappproxxy.png)

1. Witaj użytkownik uzyskuje dostęp do aplikacji hello za pośrednictwem usługi Serwer Proxy aplikacji hello i jest tooauthenticate strony logowania usługi Azure AD toohello bezpośrednie.
2. Po pomyślnym zalogowaniu token jest i wysyłane toohello urządzenia klienckiego.
3. powitania klienta wysyła hello toohello tokenu usługi Serwer Proxy aplikacji, która pobiera hello nazwa główna użytkownika (UPN) i nazwy podmiotu zabezpieczeń (SPN) z tokenu hello następnie kieruje hello żądania toohello serwera Proxy aplikacji łącznika.
4. Jeśli skonfigurowano rejestracji jednokrotnej, łącznik hello wykonuje wszelkie dodatkowe uwierzytelnianie wymagane w imieniu użytkownika hello.
5. Łącznik Hello wysyła hello żądania toohello lokalnej aplikacji.  
6. odpowiedź Hello są wysyłane za pośrednictwem serwera Proxy aplikacji usługi i łącznik toohello użytkownika.

### <a name="single-sign-on"></a>Logowanie jednokrotne
Serwer Proxy aplikacji usługi Azure AD zapewnia tooapplications rejestracji jednokrotnej (SSO), które korzystają z zintegrowane uwierzytelnianie systemu Windows (IWA) lub aplikacje obsługujące oświadczenia. Jeśli aplikacja korzysta z funkcji IWA, serwer Proxy aplikacji personifikuje hello użytkownika przy użyciu tooprovide ograniczone delegowanie protokołu Kerberos logowania jednokrotnego. Jeśli masz aplikacji obsługującej oświadczenia, które ufają usłudze Azure Active Directory, logowania jednokrotnego działa, ponieważ hello użytkownik został już uwierzytelniony przez usługę Azure AD.

Aby uzyskać więcej informacji o protokole Kerberos, zobacz [wszystkie mają tooknow o protokołu Kerberos ograniczonego delegowania (KCD)](https://blogs.technet.microsoft.com/applicationproxyblog/2015/09/21/all-you-want-to-know-about-kerberos-constrained-delegation-kcd).

### <a name="managing-apps"></a>Zarządzanie aplikacjami
Co aplikacja została opublikowana z serwerem Proxy aplikacji, można nim zarządzać jak każda inna aplikacja przedsiębiorstwa w hello portalu Azure. Można za pomocą funkcji zabezpieczeń usługi Azure Active Directory, takie jak warunkowego dostępu i dwuetapowej weryfikacji, kontrolować uprawnienia użytkowników i dostosować hello znakowanie dla aplikacji. 

## <a name="get-started"></a>Rozpoczęcie pracy

Przed skonfigurowaniem serwera Proxy aplikacji upewnij się, że masz obsługiwaną [edition usługi Azure Active Directory](https://azure.microsoft.com/pricing/details/active-directory/) i katalog usługi Azure AD, dla którego jesteś administratorem globalnym.

Rozpoczynanie pracy z serwerem Proxy aplikacji w dwóch krokach:

1. [Włączanie serwera Proxy aplikacji i skonfigurować łącznik hello](active-directory-application-proxy-enable.md).    
2. [Publikowanie aplikacji](active-directory-application-proxy-publish.md) -Użyj tekst hello tooget szybkie i łatwe Kreatora aplikacji lokalnej opublikowanych i jest dostępny zdalnie.

## <a name="whats-next"></a>Co dalej?
Po opublikowaniu pierwszej aplikacji, istnieje wiele innych, które można wykonać przy użyciu serwera Proxy aplikacji:

* [Włączanie logowania jednokrotnego](active-directory-application-proxy-sso-using-kcd.md)
* [Publikowanie aplikacji przy użyciu własnej nazwy domeny](active-directory-application-proxy-custom-domains.md)
* [Więcej informacji na temat łączników serwera Proxy aplikacji usługi Azure AD](application-proxy-understand-connectors.md)
* [Praca z istniejących lokalnych serwerów Proxy](application-proxy-working-with-proxy-servers.md) 
* [Ustaw niestandardową stronę główną](application-proxy-office365-app-launcher.md)

Najnowsze wiadomości powitania i aktualizacji, zapoznaj się z hello [Blog dotyczący serwera Proxy aplikacji](http://blogs.technet.com/b/applicationproxyblog/)

