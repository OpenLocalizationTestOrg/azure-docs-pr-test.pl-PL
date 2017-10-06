---
title: "aaaUsage scenariuszy i zagadnienia dotyczące wdrażania dla usługi Azure AD Join | Dokumentacja firmy Microsoft"
description: "W tym artykule wyjaśniono, jak Administratorzy mogą skonfigurować funkcję Azure AD Join dla użytkowników końcowych (pracowników, studentów, innych użytkowników). Zawiera omówienie również hello różnych rzeczywistych scenariusze korzystania z usługi Azure AD Join."
services: active-directory
documentationcenter: 
author: femila
manager: femila
editor: 
tags: azure-classic-portal
ms.assetid: 81d4461e-21c8-4fdd-9076-0e4991979f62
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: 7e57971481aa312ebf8a69999d194f9dcc3d4708
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="usage-scenarios-and-deployment-considerations-for-azure-ad-join"></a>Scenariusze użycia i zagadnienia dotyczące wdrażania dla usługi Azure AD Join
## <a name="usage-scenarios-for-azure-ad-join"></a>Scenariusze użycia dotyczące usługi Azure AD Join
### <a name="scenario-1-businesses-largely-in-hello-cloud"></a>Scenariusz 1: Firm głównie w chmurze hello
Azure Active Directory Join (Azure AD Join) mogą korzystać można obecnie działać i Zarządzanie tożsamościami dla Twojej firmy w chmurze hello lub przenosisz chmury toohello wkrótce. Można użyć konta, które zostały utworzone w usłudze Azure AD toosign w tooWindows 10. Za pomocą [hello pierwszego uruchomienia procesu obsługi (FRX)](active-directory-azureadjoin-user-frx.md), lub przez przyłączenie usługi Azure AD z [menu Ustawienia hello](active-directory-azureadjoin-user-upgrade.md), użytkowników można dołączyć ich tooAzure maszyny AD.  Użytkownicy mogą również korzystać z rejestracji jednokrotnej (SSO) dostęp do chmury za zasobów, takich jak usługi Office 365 w przeglądarce lub w aplikacjach pakietu Office.

### <a name="scenario-2-educational-institutions"></a>Scenariusz 2: Instytucji edukacyjnych
Instytucji edukacyjnych zwykle mają dwa typy użytkownika: pracowników i studentów. Elementy członkowskie nauczycieli lub wykładowców są traktowane jako członkowie dłuższy okres hello organizacji. Tworzenie lokalnych kont dla nich jest pożądane. Ale studenci są shorter-term członków organizacji hello i ich kont mogą być zarządzane w usłudze Azure AD. Oznacza to, może zostać umieszczony chmury toohello zamiast przechowywanego lokalnie katalog skali. Oznacza to również, że studentów będą mogli toosign w tooWindows z konta usługi Azure AD i uzyskać dostęp tooOffice 365 zasobów w aplikacjach pakietu Office.

### <a name="scenario-3-retail-businesses"></a>Scenariusz 3: Detaliczne firmy
Przedsiębiorstwa handlowe mają okresach pracowników i pracowników długoterminowej. Zazwyczaj tworzone konta lokalnego i komputerów przyłączonych do domeny na użytek długoterminowego pełnoetatowym pracownikom. Ale okresach pracownicy są shorter-term członków organizacji hello i jest pożądane toomanage swoje konta, na którym licencji użytkownika można łatwo przenosić wokół. Podczas tworzenia kont użytkowników w chmurze hello z licencjami usługi Office 365, ci użytkownicy uzyskiwać korzyści hello podpisywania w aplikacjach pakietu Office przy użyciu konta usługi Azure AD i tooWindows, gdy obsługa większą elastyczność i ich licencje po ich działania.

### <a name="scenario-4-additional-scenarios"></a>Scenariusz 4: Dodatkowe scenariusze
Wraz z wcześniejszym opisem korzyści hello możesz skorzystać z o użytkowników przyłączyć ich urządzeń tooAzure AD z powodu uproszczone środowisko łącząca, zarządzanie urządzeniami wydajne, rejestracji zarządzania automatyczne urządzeń przenośnych i tooAzure rejestracji jednokrotnej Usługi AD i zasobów lokalnych.  

## <a name="deployment-considerations-for-azure-ad-join"></a>Zagadnienia dotyczące wdrażania dla usługi Azure AD Join
### <a name="enable-your-users-toojoin-a-company-owned-device-directly-tooazure-ad"></a>Włącz toojoin Twojego użytkownicy urządzenia należące do firmy bezpośrednio tooAzure AD
Przedsiębiorstwa może zapewnić firm toopartner tylko w chmurze kont i organizacji. Partnerów te można następnie łatwo uzyskiwać dostęp do aplikacji firmowych i zasobów przy użyciu rejestracji jednokrotnej. W tym scenariuszu jest stosowane toousers, którzy uzyskują dostęp do zasobów głównie w przypadku hello chmury, takich jak usługi Office 365 lub SaaS aplikacje korzystające z usługi Azure AD na potrzeby uwierzytelniania.

### <a name="prerequisites"></a>Wymagania wstępne
**Na poziomie przedsiębiorstwa hello (administrator)**

* Subskrypcja platformy Azure w usłudze Azure Active Directory  

**Na poziomie użytkownika hello**

* Windows 10 (wersje Professional i Enterprise)

### <a name="administrator-tasks"></a>Zadania administratora
* [Konfigurowanie rejestracji urządzeń](active-directory-azureadjoin-setup.md)

### <a name="user-tasks"></a>Zadania użytkownika
* [Konfigurowanie nowego urządzenia systemu Windows 10 z usługą Azure AD podczas instalacji](active-directory-azureadjoin-user-frx.md)
* [Konfigurowanie urządzenia Windows 10 z usługą Azure AD z menu ustawień hello](active-directory-azureadjoin-user-upgrade.md)
* [Dołącz do osobistego organizacji tooyour urządzenia z systemem Windows 10](active-directory-azureadjoin-personal-device.md)

## <a name="enable-byod-in-your-organization-for-windows-10"></a>Włączyć model BYOD w organizacji dla systemu Windows 10
Można skonfigurować toouse Twojego użytkowników i pracowników, ich osobistych Windows urządzenia (BYOD) tooaccess aplikacji i zasobów firmy. Użytkownicy mogą dodawać ich usługi Azure AD kont (konta firmowego lub szkolnego) tooa osobistych Windows urządzenia tooaccess zasoby w sposób bezpieczny i być zgodne.

### <a name="prerequisites"></a>Wymagania wstępne
**Na poziomie przedsiębiorstwa hello (administrator)**

* Subskrypcja usługi Azure AD

**Na poziomie użytkownika hello**

* Windows 10 (wersje Professional i Enterprise)

### <a name="administrator-tasks"></a>Zadania administratora
* [Konfigurowanie rejestracji urządzeń](active-directory-azureadjoin-setup.md)

### <a name="user-tasks"></a>Zadania użytkownika
* [Dołącz do osobistego organizacji tooyour urządzenia z systemem Windows 10](active-directory-azureadjoin-personal-device.md)

## <a name="additional-information"></a>Dodatkowe informacje
* [System Windows 10 dla przedsiębiorstw hello: sposoby toouse urządzenia do pracy](active-directory-azureadjoin-windows10-devices-overview.md)
* [Rozszerzanie chmury możliwości tooWindows 10 urządzeniami za pomocą usługi Azure Active Directory Join](active-directory-azureadjoin-user-upgrade.md)
* [Uwierzytelnianie tożsamości bez hasła przy użyciu Microsoft Passport](active-directory-azureadjoin-passport.md)
* [Dowiedz się więcej na temat scenariuszy użycia funkcji Azure AD Join](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [Łączenie urządzeń przyłączonych do domeny tooAzure AD dla systemu Windows 10](active-directory-azureadjoin-devices-group-policy.md)
* [Konfigurowanie funkcji Azure AD Join](active-directory-azureadjoin-setup.md)

