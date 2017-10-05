---
title: "Dostęp warunkowy w klasycznym portalu Azure | Dokumentacja firmy Microsoft"
description: "Wyszukuj określonych warunków podczas uwierzytelniania w celu uzyskania dostępu do aplikacji za pomocą kontroli dostępu warunkowego w klasycznym portalu Azure."
services: active-directory
keywords: "dostęp warunkowy do aplikacji, dostęp warunkowy przy użyciu usługi Azure AD, bezpieczny dostęp do zasobów firmy, zasady dostępu warunkowego"
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
ms.openlocfilehash: d96eeb07c4bf3944be82d9c54aea93d52b54a37a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="conditional-access-in-the-azure-classic-portal"></a>Dostęp warunkowy w klasycznym portalu Azure

Ten temat dotyczy dostępu warunkowego w klasycznym portalu Azure. Aby uzyskać najnowsze informacje dotyczące dostępu warunkowego w usłudze Azure Active Directory, zobacz [dostępu warunkowego w usłudze Azure Active Directory](active-directory-conditional-access-azure-portal.md).


Możliwości kontroli dostępu warunkowego w usłudze Azure Active Directory (Azure AD) oferują prosty sposobów zabezpieczania zasobów w chmurze i lokalnie. Zasady dostępu warunkowego, takich jak uwierzytelnianie wieloskładnikowe można zapewnić ochronę przed ryzyko kradzieży i phished poświadczeń. Inne zasady dostępu warunkowego można zabezpieczyć dane organizacji. Na przykład oprócz wymaganie poświadczeń, trzeba zasady że tylko urządzenia, które są zarejestrowane w systemie zarządzania urządzeniami przenośnymi, takie jak Microsoft Intune mogą uzyskiwać dostęp do poufnych usług w organizacji.

## <a name="prerequisites"></a>Wymagania wstępne
Azure AD dostęp warunkowy jest funkcją [Azure Active Directory Premium](http://www.microsoft.com/identity). Każdy użytkownik uzyskujący dostęp do aplikacji, która ma zasady dostępu warunkowego są stosowane musi mieć licencji usługi Azure AD Premium. Dowiedz się więcej na temat wymagań dotyczących licencji w [raport licencji użytkownika](https://aka.ms/utc5ix).

## <a name="how-is-conditional-access-control-enforced"></a>Jak jest wymuszana kontroli dostępu warunkowego
Przy użyciu kontroli dostępu warunkowego w miejscu, usługi Azure AD sprawdza określonych warunków, można ustawić, aby użytkownik mógł uzyskać dostęp do aplikacji. Po spełnieniu wymagań dostępu, użytkownik jest uwierzytelniony i dostęp do aplikacji.  

![Omówienie dostępu warunkowego](./media/active-directory-conditional-access/conditionalaccess-overview.png)

## <a name="conditions"></a>Warunki
Są to warunki, które można uwzględnić w zasadach dostępu warunkowego:

* **Członkostwa w grupie**. Kontrola dostępu użytkownika na podstawie członkostwa w grupie.
* **Lokalizacja**. Użycie lokalizacji użytkownika do uwierzytelniania wieloskładnikowego wyzwalacza i używanie formantów blok, gdy użytkownik nie znajduje się w zaufanej sieci.
* **Platformy urządzeń**. Użyj platformy urządzeń, takich jak systemu iOS, Android, Windows Mobile i Windows, jako warunek stosowania zasad.
* **Urządzenie włączone**. Stan urządzenia, czy włączać lub wyłączać, jest weryfikowane podczas oceny zasad urządzenia. Po wyłączeniu utraty lub kradzieży urządzenia w katalogu go nie spełnia wymagań zasad.
* **Ryzyko logowania i użytkownika**. Można użyć [Azure AD Identity Protection](active-directory-identityprotection.md) dla zasad dostępu warunkowego ryzyka. Zasady dostępu warunkowego ryzyka pomocy, nadaj ze względów bezpieczeństwa wcześniejszym organizacji na podstawie zdarzeń o podwyższonym ryzyku i nietypowych działań logowania.

## <a name="controls"></a>Kontrolki
Są to kontrolki, których można użyć do wymuszania zasad dostępu warunkowego:

* **Uwierzytelnianie wieloskładnikowe**. Możesz wymagać silnego uwierzytelniania za pośrednictwem usługi Multi-Factor authentication. Umożliwia uwierzytelnianie wieloskładnikowe Azure Multi-Factor Authentication lub za pomocą lokalnego dostawcy uwierzytelniania wieloskładnikowego, w połączeniu z usługi Active Directory Federation Services (AD FS). Przy użyciu usługi Multi-Factor authentication pomaga chronić zasoby z uzyskiwany przez nieautoryzowanego użytkownika, która może uzyska dostęp do poświadczeń prawidłowego użytkownika.
* **Blok**. Można stosować warunki, takie jak lokalizacja użytkownika w celu zablokowania dostępu użytkownika. Na przykład gdy użytkownik nie znajduje się w zaufanej sieci może zablokować dostęp.
* **Zgodne urządzenia**. Można ustawić zasady dostępu warunkowego na poziomie urządzeń. Można skonfigurować zasady, aby tylko komputery, które są przyłączone do domeny lub urządzeń przenośnych, które są zarejestrowane w aplikacji do zarządzania urządzeniami przenośnymi, mogą uzyskiwać dostęp do zasobów organizacji. Można na przykład sprawdzić zgodność urządzenia przy użyciu usługi Intune i zgłoś go do usługi Azure AD do wymuszania gdy użytkownik próbuje uzyskać dostęp do aplikacji. Aby uzyskać szczegółowe wskazówki dotyczące sposobu ochrona aplikacji i danych przy użyciu usługi Intune, zobacz [ochrona aplikacji i danych w usłudze Microsoft Intune](https://docs.microsoft.com/intune/deploy-use/protect-apps-and-data-with-microsoft-intune). Można również użyć Intune do wymuszania ochrony danych w przypadku utraty lub kradzieży urządzeń. Aby uzyskać więcej informacji, zobacz [pomocy lepszej ochrony danych dzięki pełnemu lub selektywnemu czyszczeniu przy użyciu programu Microsoft Intune](https://docs.microsoft.com/intune/deploy-use/use-remote-wipe-to-help-protect-data-using-microsoft-intune).

## <a name="applications"></a>Aplikacje
Można wymusić zasady dostępu warunkowego na poziomie aplikacji. Ustawienie poziomu dostępu dla aplikacji i usług w chmurze lub lokalnie. Zasady są stosowane bezpośrednio do witryny sieci Web lub usługi. Zasady są wymuszane uzyskać dostęp do przeglądarki i aplikacje, które uzyskują dostęp do usługi.

## <a name="device-based-conditional-access"></a>Dostępu warunkowego opartego na urządzeniu
Można ograniczyć dostęp do aplikacji z urządzeń zarejestrowanych w usłudze Azure AD i które spełniają określonych warunków. Dostępu warunkowego opartego na urządzeniu uniemożliwia użytkownika, który próbuje uzyskać dostęp do zasobów z zasobów organizacji:

* Nieznany lub niezarządzanego urządzenia.
* Urządzenia, które nie spełniają zasad zabezpieczeń organizacji, skonfigurować.

Można ustawić zasady na podstawie tych wymagań:

* **Urządzenia przyłączone do domeny**. Ustaw zasady, aby ograniczyć dostęp do urządzeń, które są przyłączone do domeny usługi Active Directory lokalnymi i które także są zarejestrowane w usłudze Azure AD. Ta zasada ma zastosowanie do komputerów stacjonarnych, laptopów i tabletów przedsiębiorstwa systemu Windows.
  Aby uzyskać więcej informacji dotyczących sposobu konfigurowania automatycznej rejestracji urządzeń przyłączonych do domeny z usługą Azure AD, zobacz [Konfigurowanie automatycznej rejestracji urządzeń z systemem Windows przyłączonych do domeny z usługą Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md).
* **Zgodne urządzenia**. Ustaw zasady, aby ograniczyć dostęp do urządzeń, które są oznaczone jako **zgodne** w katalogu systemu zarządzania. Ta zasada zapewnia, że tylko urządzenia, które są zgodne z zasadami zabezpieczeń, takie jak wymuszanie szyfrowania plików na urządzeniu mają prawo dostępu. Ta zasada służy do ograniczenia dostępu z następującymi urządzeniami:
  
  * **Urządzenia z systemem Windows przyłączonych do domeny**. Zarządzane przez System Center Configuration Manager (w wersji current branch) wdrożone w konfiguracji hybrydowego.
  * **Pracy systemu Windows 10 Mobile lub osobistych urządzeń**. Zarządzane przez usługę Intune lub za pomocą systemu zarządzania obsługiwanych urządzeń przenośnych innych firm.
  * **iOS i urządzeniach z systemem Android**. Zarządzane przez usługę Intune.

Użytkowników, którzy uzyskują dostęp do aplikacji, które są chronione przez oparty na urządzeniach, zasad urzędu certyfikacji musi uzyskać dostępu do aplikacji z urządzenia, które spełnia wymagania dotyczące tych zasad. Jeśli nastąpiła odmowa dostępu na urządzeniu, który nie spełnia wymagań zasad.

Aby uzyskać informacje o sposobie konfigurowania zasad oparta na urządzeniach urzędu certyfikacji w usłudze Azure AD, zobacz [ustawić zasady dostępu warunkowego opartego na urządzeniu aplikacje połączone usługi Azure Active Directory](active-directory-conditional-access-policy-connected-applications.md).

## <a name="resources"></a>Zasoby
Zapoznaj się z następujących kategorii zasobów i artykuły, aby dowiedzieć się więcej na temat ustawiania dostępu warunkowego dla Twojej organizacji.

### <a name="multi-factor-authentication-and-location-policies"></a>Zasady uwierzytelniania i lokalizacja wieloskładnikowego
* [Wprowadzenie do korzystania z dostępu warunkowego, aby aplikacje platformy Azure połączone AD na podstawie grupy, lokalizacji i zasady uwierzytelniania wieloskładnikowego](active-directory-conditional-access-azuread-connected-apps.md)
* [Aplikacje i przeglądarek, które są obsługiwane](active-directory-conditional-access-supported-apps.md)

### <a name="device-based-conditional-access"></a>Dostępu warunkowego opartego na urządzeniu
* [Ustaw zasady dostępu warunkowego opartego na urządzeniu do kontroli dostępu do aplikacji połączony z usługą Azure Active Directory](active-directory-conditional-access-policy-connected-applications.md)
* [Konfigurowanie automatycznej rejestracji systemu Windows przyłączone do domeny urządzenia z usługi Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md)
* [Rozwiązywanie problemów, dostęp do usługi Azure Active Directory](active-directory-conditional-access-device-remediation.md)
* [Łatwiejsza ochrona danych w przypadku utraty lub kradzieży urządzenia przy użyciu programu Microsoft Intune](https://docs.microsoft.com/intune/deploy-use/use-remote-wipe-to-help-protect-data-using-microsoft-intune)

### <a name="protect-resources-based-on-sign-in-risk"></a>Ochrona zasobów opartych na ryzyko logowania
* [Usługa Azure AD identity protection](active-directory-identityprotection.md)

### <a name="next-steps"></a>Następne kroki
* [Dostęp warunkowy — często zadawane pytania](active-directory-conditional-faqs.md)
* [Dokumentacja techniczna](active-directory-conditional-access-technical-reference.md)

