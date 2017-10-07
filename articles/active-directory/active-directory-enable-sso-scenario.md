---
title: "aaaManaging aplikacji za pomocą usługi Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Ten artykuł hello zalet integracji z lokalnymi, chmurze i aplikacjami SaaS usługi Azure Active Directory."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 95b96f10-2d5c-4b78-8af8-d3657a24140f
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: asteen
ms.openlocfilehash: 0016f8b433e101d8a150bc6d9be3931851578241
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="managing-applications-with-azure-active-directory"></a>Zarządzanie aplikacjami przy użyciu usługi Azure Active Directory
Poza hello rzeczywiste przepływu pracy lub zawartości przedsiębiorstwa mają dwa podstawowe wymagania dotyczące wszystkich aplikacji:

1. wydajność tooincrease aplikacji powinno być łatwe toodiscover i dostępu
2. tooenable zabezpieczeń i nadzór nad hello organizacja musi kontroli i nadzoru, na który można i faktycznie uzyskuje dostęp do poszczególnych aplikacji

Witaj świecie najlepiej można to osiągnąć przy użyciu toocontrol tożsamości aplikacji w chmurze "*KTO jest dozwolone toodo co*".

W przypadku komputerów terminologią:

* *Kto* nosi nazwę *tożsamości* — Witaj zarządzania użytkownikami i grupami
* *Co* nosi nazwę *dostępu administracyjnego* — Witaj zarządzania zasobami tooprotected dostępu

Oba te składniki są ze sobą znane jako *tożsamości i dostępu do zarządzania (IAM)*, która jest zdefiniowana przez hello [Gartner](http://www.gartner.com/it-glossary/identity-and-access-management-iam) grupy jako "*hello dyscypliny zabezpieczeń, umożliwiający hello prawej osoby tooaccess hello odpowiednich zasobów na powitania kliknij prawym przyciskiem myszy razy hello prawej ze względu na*".

OK, co to jest hello problem? Jeśli jest IAM *niezarządzanych* w jednym miejscu z zintegrowanego rozwiązania:

* Tożsamość Administratorzy mają tooindividually tworzenie i aktualizowanie kont użytkowników we wszystkich aplikacjach oddzielnie, działanie nadmiarowe i czasochłonna.
* Użytkownicy mają toomemorize wiele poświadczeń tooaccess hello aplikacji potrzebnych im toowork z. W związku z tym użytkownicy często toowrite dół haseł lub użycie innych rozwiązań zarządzania hasła, które wprowadza inne zagrożenia dla bezpieczeństwa danych.
* Nadmiarowe, czasochłonne działania skrócić hello użytkowników i administratorów pracuje działalności, które zwiększają mierzenie Twojej firmy.

Tak co uniemożliwia zazwyczaj organizacje od przyjmowania zintegrowanego rozwiązania IAM?

* Najbardziej techniczne rozwiązania są oparte na platformy oprogramowania, które wymagają toobe wdrożone i dostosowane przez poszczególnych organizacji w celu ich własnych aplikacji.
* Aplikacje w chmurze są często stosowane poziomie wyższym niż organizacji IT można zintegrować z istniejącymi rozwiązaniami IAM.
* Monitorowanie narzędzi i zabezpieczeń wymagają dodatkowe dostosowanie i integracja z tooachieve kompleksowe E2E scenariusze.

## <a name="azure-active-directory-integrated-with-applications"></a>Usługa Azure Active Directory jest zintegrowany z aplikacjami
Azure Active Directory jest kompleksowe tożsamość firmy Microsoft jako rozwiązaniem Service (IDaaS) który:

* Włącza IAM jako usługa w chmurze 
* Umożliwia zarządzanie dostępu, jednokrotnego (SSO) i raportowania 
* Obsługuje zarządzanie zintegrowanego dostępu dla [tysięcy aplikacji](https://azure.microsoft.com/marketplace/active-directory/) w galerii aplikacji hello, w tym usług Salesforce, Google Apps, pole i Concur. 

Z usługą Azure Active Directory, wszystkie aplikacje publikowania dla partnerów i klientów (biznesowe lub klienta) ma hello takie same możliwości zarządzania tożsamościami i dostępem.<br> Ta umożliwia toosignificantly można zmniejszyć koszty operacyjne.

Co zrobić, jeśli potrzebna jest tooimplement aplikacji, która nie ma jeszcze w galerii aplikacji hello? Jest to nieco więcej czasu niż Konfigurowanie logowania jednokrotnego dla aplikacji z galerii aplikacji hello, usługa Azure AD zapewnia kreatora, który pomaga hello konfiguracji.

wartość Hello usługi Azure AD wykracza poza "tak" aplikacje w chmurze. Umożliwia także go z aplikacjami lokalnymi przez zapewnienie bezpiecznego dostępu zdalnego. Bezpiecznego dostępu zdalnego można wyeliminować konieczność hello hello sieci VPN lub innych implementacji zarządzania tradycyjnych dostępu zdalnego.

Zapewniając dostępu administracyjnego i logowania jednokrotnego (SSO) dla wszystkich aplikacji, usługi Azure AD zapewnia rozwiązanie hello danych głównych toohello problemy zabezpieczeń i wydajności.

* Użytkownicy mogą uzyskiwać dostęp do wielu aplikacji za pomocą jednego logowania nadanie więcej tooincome czasu generowania lub pracy działania operacje wykonywane.
* Tożsamość Administratorzy mogą zarządzać tooapplications dostępu w jednym miejscu.

korzyści Hello hello użytkownika i firmy jest oczywiste. Spójrzmy bliższe spojrzenie na hello korzyści dla administratora tożsamości i hello organizacji.

## <a name="integrated-application-benefits"></a>Korzyści zintegrowanej aplikacji
proces logowania jednokrotnego Hello obejmuje dwa kroki:

* Uwierzytelnianie, proces weryfikacji tożsamości użytkownika hello hello.
* Autoryzacji, hello decyzji tooenable lub blokowanie dostępu tooa zasobów przy użyciu zasad dostępu.

Podczas używania aplikacji toomanage usługi Azure AD i włączyć funkcję rejestracji Jednokrotnej:

* Uwierzytelnianie jest wykonywane na powitania użytkownika lokalnie (np. usługi AD) lub konto usługi Azure AD.
* Wykonuje autoryzacji na powitania usługi Azure AD przypisania ochrony zasad i zapewnienie spójności użytkownika końcowego i możliwość przypisania tooadd, lokalizacji i warunki MFA w dowolnej aplikacji, niezależnie od jej możliwości.

Ważne toounderstand, który hello sposób hello autoryzacji jest wprowadzany w aplikacji docelowej hello zależy w zależności od tego, jak aplikacja hello został zintegrowany z usługą Azure AD.

* **Aplikacje wstępnie zintegrowanych przez dostawcę usług** takich jak usługi Office 365 i Azure są to aplikacje wbudowane bezpośrednio w usłudze Azure AD i zależne dla ich kompleksowe funkcje zarządzania tożsamościami i dostępem. Uzyskiwać dostęp do aplikacji toothese jest włączona za pośrednictwem katalogu wystawiania informacji i tokenu.
* **Aplikacje wstępnie zintegrowanych przez firmę Microsoft i niestandardowych aplikacji** są to aplikacje w chmurze niezależne, które zależą od katalogu aplikacji wewnętrznych i może działać niezależnie od usługi Azure AD. Uzyskiwać dostęp do aplikacji toothese jest włączone przez wystawienie konto aplikacji tooan poświadczenie mapowane aplikacji. W zależności od możliwości aplikacji hello hello poświadczenie może być token Federacji lub nazwę użytkownika i hasło dla konta, które zostało wcześniej zainicjowane w aplikacji hello.
* **Aplikacje lokalne** aplikacji opublikowanych przy użyciu serwera proxy aplikacji hello Azure AD głównie Włączanie dostępu lokalnego tooon aplikacji. Te aplikacje polegają na katalog lokalny centralnej, takie jak Windows Server Active Directory. Aplikacje toothese dostępu jest włączana przez wyzwalania użytkownika końcowego toohello zawartości aplikacji hello hello proxy toodeliver, przy jednoczesnym zachowaniu lokalne powitania logowania jednokrotnego wymaganie.

Na przykład jeśli użytkownik nie przyłączy organizacji, należy toocreate konta dla użytkownika hello w usłudze Azure AD w operacjach hello głównej logowania jednokrotnego. Jeśli ten użytkownik wymaga dostępu tooa zarządzanych aplikacji, takie jak Salesforce, musisz również muszą toocreate konta dla tego użytkownika w usłudze Salesforce i połączyć ją toohello konta Azure toomake logowania jednokrotnego pracy. Gdy użytkownik hello opuszczenia organizacji, jest hello toodelete wskazane konto usługi Azure AD i magazyny IAM hello użytkownika ma dostęp do aplikacji hello hello wszystkich kontach odpowiednik w programie.

## <a name="access-detection"></a>Dostęp do wykrywania
W przedsiębiorstwach nowoczesnego działu IT często nie są znane wszystkich aplikacji hello chmury, które są używane. W połączeniu z usługi Cloud App Discovery usługi Azure AD zapewnia toodetect rozwiązanie tych aplikacji.

## <a name="account-management"></a>Zarządzanie kontami
Tradycyjnym zarządzania kontami w hello różnych aplikacji jest wykonywane przez proces ręczny IT lub obsługuje osobistych w organizacji hello. Usługi Azure AD pełni zautomatyzowanego zarządzania kontami przez wszystkie aplikacje dostawcy zintegrowane usługi i aplikacje, te wstępnie zintegrowanych przez firmę Microsoft obsługujący użytkownika automatycznego inicjowania obsługi administracyjnej lub SAML JIT.

## <a name="automated-user-provisioning"></a>Inicjowanie obsługi użytkowników automatycznych
Niektóre aplikacje Podaj interfejsów automatyzacji tworzenia i usuwania (lub dezaktywacji) kont. Jeśli dostawca oferuje takiego interfejsu, jest wykorzystywana przez usługę Azure AD. Zmniejsza koszty operacyjne, ponieważ zadania administracyjne odbywa się automatycznie i zwiększa bezpieczeństwo hello środowiska, ponieważ zmniejsza ryzyko hello nieautoryzowanego dostępu.

## <a name="access-management"></a>Zarządzanie dostępem
Używanie programu Azure AD można zarządzać dostępem do tooapplications za pomocą poszczególnych lub reguły zmiennych przypisania. Możesz również delegować dostęp do zarządzania toohello odpowiednich osób w hello organizacji zapewnienie hello najlepsze nadzoru i zmniejszenie obciążenia hello pomocy technicznej.

## <a name="on-premises-applications"></a>Aplikacje lokalne
wbudowany serwer proxy aplikacji Hello umożliwia toopublish użytkowników tooyour aplikacji lokalnej co zarówno spójne dostęp dzięki chmurze nowoczesnych aplikacji hello korzyści w zakresie i z usługi Azure AD monitorowania, raportowania i funkcji zabezpieczeń .

## <a name="reporting-and-monitoring"></a>Monitorowanie i raportowanie
Usługa Azure AD zapewnia wstępnie zintegrowanych raportowania i możliwości umożliwiających tooknow, kto ma dostęp do tooapplications i gdy rzeczywiście używane ich monitorowania.

## <a name="related-capabilities"></a>Funkcje pokrewne
Z usługą Azure AD można zabezpieczyć swoje aplikacje za pomocą zasad dostępu szczegółowego i wstępnie zintegrowane uwierzytelnianie wieloskładnikowe. więcej informacji na temat usługi Azure MFA, zobacz toolearn [usługi Azure MFA](https://azure.microsoft.com/services/multi-factor-authentication/).

## <a name="getting-started"></a>Wprowadzenie
tooget uruchomiona Integrowanie aplikacji z usługą Azure AD, Przyjrzyjmy się hello [przewodnik Wprowadzenie do integracji Azure Active Directory z aplikacjami pobierania](active-directory-integrating-applications-getting-started.md).

## <a name="see-also"></a>Zobacz też
[Indeks artykułów dotyczących zarządzania aplikacjami w usłudze Azure Active Directory](active-directory-apps-index.md)

