---
title: "aaaConditional dostępu w hello klasycznego portalu Azure | Dokumentacja firmy Microsoft"
description: "Użyj w hello Azure classic portal toocheck kontroli dostępu warunkowego dla określonych warunków uwierzytelniania dla tooapplications dostępu."
services: active-directory
keywords: "tooapps dostępu warunkowego, dostępu warunkowego z usługą Azure AD, bezpieczny dostęp do zasobów toocompany, zasady dostępu warunkowego"
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: da3f0a44-1399-4e0b-aefb-03a826ae4ead
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/07/2017
ms.author: markvi
ms.reviewer: calebb
ms.custom: oldportal
ms.openlocfilehash: 049bd3f6ec9e35479319ee7608b007b9a1e16647
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="conditional-access-in-hello-azure-classic-portal"></a>Dostęp warunkowy w hello klasycznego portalu Azure

Ten temat dotyczy dostępu warunkowego w hello klasycznego portalu Azure. Aby hello najnowsze informacje dotyczące dostępu warunkowego w hello Azure Active Directory, zobacz [dostępu warunkowego w usłudze Azure Active Directory](active-directory-conditional-access-azure-portal.md).


Witaj możliwości kontroli dostępu warunkowego w usłudze Azure Active Directory (Azure AD) oferują prosty toohelp bezpiecznych zasobów w chmurze hello i lokalnych. Zasady dostępu warunkowego, takich jak uwierzytelnianie wieloskładnikowe można zapewnić ochronę przed hello ryzyko kradzieży i phished poświadczeń. Inne zasady dostępu warunkowego można zabezpieczyć dane organizacji. Na przykład oprócz toorequiring poświadczenia, może zajść zasady że tylko urządzenia, które są zarejestrowane w systemie zarządzania urządzeniami przenośnymi, takie jak Microsoft Intune mogą uzyskiwać dostęp do poufnych usług w organizacji.

## <a name="prerequisites"></a>Wymagania wstępne
Azure AD dostęp warunkowy jest funkcją [Azure Active Directory Premium](http://www.microsoft.com/identity). Każdy użytkownik uzyskujący dostęp do aplikacji, która ma zasady dostępu warunkowego są stosowane musi mieć licencji usługi Azure AD Premium. Dowiedz się więcej na temat wymagań dotyczących licencji w [raport licencji użytkownika](https://aka.ms/utc5ix).

## <a name="how-is-conditional-access-control-enforced"></a>Jak jest wymuszana kontroli dostępu warunkowego
Przy użyciu kontroli dostępu warunkowego w miejscu usługi Azure AD sprawdza dotyczące określonych warunków hello należy ustawić dla tooaccess użytkownika aplikacji. Po spełnieniu wymagań dostępu hello użytkownik został uwierzytelniony i może uzyskać dostępu do aplikacji hello.  

![Omówienie dostępu warunkowego](./media/active-directory-conditional-access/conditionalaccess-overview.png)

## <a name="conditions"></a>Warunki
Są to warunki, które można uwzględnić w zasadach dostępu warunkowego:

* **Członkostwa w grupie**. Kontrola dostępu użytkownika na podstawie członkostwa w grupie.
* **Lokalizacja**. Użycie lokalizacji hello hello użytkownika tootrigger usługi Multi-Factor Authentication i używanie formantów blok, gdy użytkownik nie znajduje się w zaufanej sieci.
* **Platformy urządzeń**. Użyj hello platformy urządzeń, takich jak systemu iOS, Android, Windows Mobile i Windows, jako warunek stosowania zasad.
* **Urządzenie włączone**. Stan urządzenia, czy włączać lub wyłączać, jest weryfikowane podczas oceny zasad urządzenia. Po wyłączeniu utraty lub kradzieży urządzenia w katalogu hello go nie spełnia wymagań zasad.
* **Ryzyko logowania i użytkownika**. Można użyć [Azure AD Identity Protection](active-directory-identityprotection.md) dla zasad dostępu warunkowego ryzyka. Zasady dostępu warunkowego ryzyka pomocy, nadaj ze względów bezpieczeństwa wcześniejszym organizacji na podstawie zdarzeń o podwyższonym ryzyku i nietypowych działań logowania.

## <a name="controls"></a>Kontrolki
Są to kontrolki służy tooenforce zasady dostępu warunkowego:

* **Uwierzytelnianie wieloskładnikowe**. Możesz wymagać silnego uwierzytelniania za pośrednictwem usługi Multi-Factor authentication. Umożliwia uwierzytelnianie wieloskładnikowe Azure Multi-Factor Authentication lub za pomocą lokalnego dostawcy uwierzytelniania wieloskładnikowego, w połączeniu z usługi Active Directory Federation Services (AD FS). Przy użyciu usługi Multi-Factor authentication pomaga chronić zasoby z uzyskiwany przez nieautoryzowanego użytkownika, który może mieć uzyskał dostęp toohello poświadczenia prawidłowego użytkownika.
* **Blok**. Można stosować warunki, takie jak dostęp użytkownika tooblock lokalizacji użytkownika. Na przykład gdy użytkownik nie znajduje się w zaufanej sieci może zablokować dostęp.
* **Zgodne urządzenia**. Na poziomie urządzeń hello można ustawić zasady dostępu warunkowego. Można skonfigurować zasady, aby tylko komputery, które są przyłączone do domeny lub urządzeń przenośnych, które są zarejestrowane w aplikacji do zarządzania urządzeniami przenośnymi, mogą uzyskiwać dostęp do zasobów organizacji. Na przykład można użyć zgodności urządzeń toocheck usługi Intune i raportować ją tooAzure AD do wymuszania hello użytkownik próbujący tooaccess aplikacji. Szczegółowe wskazówki dotyczące sposobu toouse Intune tooprotect aplikacji i danych, zobacz [ochrona aplikacji i danych w usłudze Microsoft Intune](https://docs.microsoft.com/intune/deploy-use/protect-apps-and-data-with-microsoft-intune). Można też użyć do ochrony danych tooenforce usługi Intune w przypadku utraty lub kradzieży urządzeń. Aby uzyskać więcej informacji, zobacz [pomocy lepszej ochrony danych dzięki pełnemu lub selektywnemu czyszczeniu przy użyciu programu Microsoft Intune](https://docs.microsoft.com/intune/deploy-use/use-remote-wipe-to-help-protect-data-using-microsoft-intune).

## <a name="applications"></a>Aplikacje
Można wymusić zasady dostępu warunkowego na poziomie aplikacji hello. Ustaw poziomy dostępu dla aplikacji i usług w chmurze hello lub lokalnie. Witaj zasady są stosowane bezpośrednio toohello witryny sieci Web lub usługi. Witaj zasady są wymuszane dla przeglądarki toohello dostępu i tooapplications dostępnym hello usługi.

## <a name="device-based-conditional-access"></a>Dostępu warunkowego opartego na urządzeniu
Można ograniczyć tooapplications dostępu z urządzeń zarejestrowanych w usłudze Azure AD i które spełniają określonych warunków. Dostępu warunkowego opartego na urządzeniu uniemożliwia użytkownika, który próbuje tooaccess hello zasobów z zasobów organizacji:

* Nieznany lub niezarządzanego urządzenia.
* Urządzenia, które nie spełniają zasad zabezpieczeń hello Konfigurowanie organizacji.

Można ustawić zasady na podstawie tych wymagań:

* **Urządzenia przyłączone do domeny**. Ustaw zasady toorestrict dostępu toodevices, które są domeny usługi Active Directory tooan dołączonego do lokalnej, a które także są zarejestrowane w usłudze Azure AD. Ta zasada dotyczy tooWindows komputerów stacjonarnych, laptopów i tabletów przedsiębiorstwa.
  Aby uzyskać więcej informacji o tym, jak tooset się automatycznej rejestracji urządzeń przyłączonych do domeny z usługą Azure AD, zobacz [Konfigurowanie automatycznej rejestracji urządzeń z systemem Windows przyłączonych do domeny z usługą Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md).
* **Zgodne urządzenia**. Ustaw toodevices dostępu toorestrict zasad, które są oznaczone **zgodne** w katalogu systemu zarządzania hello. Ta zasada zapewnia, że tylko urządzenia, które są zgodne z zasadami zabezpieczeń, takie jak wymuszanie szyfrowania plików na urządzeniu mają prawo dostępu. Można użyć tego dostępu toorestrict zasad z hello następujące urządzenia:
  
  * **Urządzenia z systemem Windows przyłączonych do domeny**. Zarządzane przez System Center Configuration Manager (w wersji current branch hello) wdrożone w konfiguracji hybrydowego.
  * **Pracy systemu Windows 10 Mobile lub osobistych urządzeń**. Zarządzane przez usługę Intune lub za pomocą systemu zarządzania obsługiwanych urządzeń przenośnych innych firm.
  * **iOS i urządzeniach z systemem Android**. Zarządzane przez usługę Intune.

Użytkowników, którzy uzyskują dostęp do aplikacji, które są chronione przez oparty na urządzeniach, zasad urzędu certyfikacji musi uzyskać dostępu do aplikacji hello z urządzenia, które spełnia wymagania dotyczące tych zasad. Jeśli nastąpiła odmowa dostępu na urządzeniu, który nie spełnia wymagań zasad.

Aby uzyskać informacje o tooconfigure oparta na urządzeniach, zasad urzędu certyfikacji w usłudze Azure AD, zobacz temat [ustawić zasady dostępu warunkowego opartego na urządzeniu aplikacje połączone usługi Azure Active Directory](active-directory-conditional-access-policy-connected-applications.md).

## <a name="resources"></a>Zasoby
Zobacz hello następującego zasobu więcej o konfigurowaniu dostępu warunkowego dla Twojej organizacji toolearn kategorii i artykułów.

### <a name="multi-factor-authentication-and-location-policies"></a>Zasady uwierzytelniania i lokalizacja wieloskładnikowego
* [Wprowadzenie do korzystania z aplikacji połączonych AD tooAzure dostępu warunkowego na podstawie grupy, lokalizacji i zasady uwierzytelniania wieloskładnikowego](active-directory-conditional-access-azuread-connected-apps.md)
* [Aplikacje i przeglądarek, które są obsługiwane](active-directory-conditional-access-supported-apps.md)

### <a name="device-based-conditional-access"></a>Dostępu warunkowego opartego na urządzeniu
* [Ustawienie zasad dostępu warunkowego opartego na urządzeniu dla dostępu aplikacji połączone usługi Active Directory tooAzure formantu](active-directory-conditional-access-policy-connected-applications.md)
* [Konfigurowanie automatycznej rejestracji systemu Windows przyłączone do domeny urządzenia z usługi Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md)
* [Rozwiązywanie problemów, dostęp do usługi Azure Active Directory](active-directory-conditional-access-device-remediation.md)
* [Łatwiejsza ochrona danych w przypadku utraty lub kradzieży urządzenia przy użyciu programu Microsoft Intune](https://docs.microsoft.com/intune/deploy-use/use-remote-wipe-to-help-protect-data-using-microsoft-intune)

### <a name="protect-resources-based-on-sign-in-risk"></a>Ochrona zasobów opartych na ryzyko logowania
* [Usługa Azure AD identity protection](active-directory-identityprotection.md)

### <a name="next-steps"></a>Następne kroki
* [Dostęp warunkowy — często zadawane pytania](active-directory-conditional-faqs.md)
* [Dokumentacja techniczna](active-directory-conditional-access-technical-reference.md)

