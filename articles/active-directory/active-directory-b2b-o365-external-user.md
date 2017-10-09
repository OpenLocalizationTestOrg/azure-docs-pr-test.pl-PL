---
title: "aaaOffice 365 udostępnianie zewnętrzne i współpracy usługi Azure Active Directory B2B | Dokumentacja firmy Microsoft"
description: "mapowanie odwołania do usługi Azure Active Directory B2B współpracy oświadczeń"
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 05/24/2017
ms.author: sasubram
ms.openlocfilehash: 60452b27b328453eda729bd839c982b479cb6f1b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="office-365-external-sharing-and-azure-active-directory-b2b-collaboration"></a>Udostępnianie zewnętrzne usługi Office 365 i Azure Active Directory B2B współpracy

Zewnętrzne udostępnianie w usłudze Office 365 (OneDrive, SharePoint Online, Unified grup itp.) i B2B usługi Azure Active Directory (Azure AD) współpracy są technicznie hello sam element. Udostępnianie zewnętrzne wszystkich (oprócz OneDrive/usługi SharePoint Online), łącznie z gośćmi grupy usługi Office 365, używa już zaproszenia współpracy B2B usługi Azure AD hello interfejsów API do udostępniania.

OneDrive/usługi SharePoint Online ma menedżera oddzielne zaproszenia. Obsługa udostępnianie zewnętrzne w usłudze OneDrive/SharePoint Online zostało uruchomione przed jego obsługę opracowany usługi Azure AD. Wraz z upływem czasu OneDrive/usługi SharePoint Online udostępnianie zewnętrzne uzyskano kilka funkcji i milionów użytkowników, którzy korzystają produktu hello obiektu w — zbudowany udostępnianie wzorzec. Istnieją pewne niewielkie różnice między jak OneDrive/usługi SharePoint Online udostępnianie zewnętrzne działa i jak działa współpracy B2B usługi Azure AD:

- OneDrive/usługi SharePoint Online dodaje katalog toohello użytkowników po użytkowników zostały zrealizowane zaproszenia. Dlatego przed realizacji, nie widzisz hello użytkownika w portalu usługi Azure AD. Jeśli inna witryna zaprasza użytkownika w hello międzyczasie, generowany jest nowe zaproszenie. Użycie współpracy B2B usługi Azure AD, użytkownicy zostaną jednak dodane bezpośrednio na zaproszenia, tak aby pokazywały się wszędzie.

- środowisko realizacji Hello w usłudze OneDrive/usługi SharePoint Online wygląda inaczej niż hello środowisko współpracy B2B usługi Azure AD. Po użytkownika umarza zaproszenia, napotyka hello wyglądają podobnie.

- Azure AD B2B współpracy zaproszonych użytkowników mogą być pobierane z usługi OneDrive/usługi SharePoint Online udostępnianie okien dialogowych. OneDrive/SharePoint Online zaproszonych użytkowników również wyświetlane w usłudze Azure AD po ich zrealizować zaproszenia.

- toomanage zewnętrznych udostępnianie współpracy B2B usługi Azure AD w usłudze OneDrive/SharePoint Online, ustaw hello OneDrive/usługi SharePoint Online będzie zewnętrznych udostępnianie ustawienie zbyt**Zezwalaj tylko na udostępniania użytkownikom zewnętrznym już w katalogu hello**. Dla użytkowników tooexternally udostępnione Lokacje i pobranie z zewnętrznym współpracownikom, które hello admin został dodany. Witaj, Administratorze można dodać hello zewnętrznych współpracowników za pośrednictwem hello zaproszenia współpracy B2B interfejsów API.

![Witaj OneDrive/usługi SharePoint Online zewnętrznego współużytkuje](media/active-directory-b2b-o365-external-user/odsp-sharing-setting.png)

## <a name="next-steps"></a>Następne kroki

Zobacz nasze inne artykuły dotyczące współpracy B2B w usłudze Azure AD:

* [Czym jest współpraca B2B w usłudze Azure AD?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Właściwości użytkownika współpracy B2B](active-directory-b2b-user-properties.md)
* [Dodawanie roli tooa użytkownika współpracy B2B](active-directory-b2b-add-guest-to-role.md)
* [Delegowanie zaproszenia współpracy B2B](active-directory-b2b-delegate-invitations.md)
* [Grupami dynamicznymi i współpracy B2B](active-directory-b2b-dynamic-groups.md)
* [Kod współpracy B2B i przykłady środowiska PowerShell](active-directory-b2b-code-samples.md)
* [Konfigurowanie aplikacji SaaS do współpracy B2B](active-directory-b2b-configure-saas-apps.md)
* [Tokeny użytkownika współpracy B2B](active-directory-b2b-user-token.md)
* [Oświadczenia użytkowników współpracy B2B mapowania](active-directory-b2b-claims-mapping.md)
* [Bieżące ograniczenia współpracy B2B](active-directory-b2b-current-limitations.md)
