---
title: "aaaCompare B2B współpracy i B2C w usłudze Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Jaka jest różnica hello współpracy usługi Azure Active Directory B2B i usługi Azure AD B2C?"
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
ms.date: 03/15/2017
ms.author: sasubram
ms.openlocfilehash: 34d88b9a7d023e077568e8df3d5e1610ae05b361
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="compare-b2b-collaboration-and-b2c-in-azure-active-directory"></a>Porównaj współpracy B2B i B2C w usłudze Azure Active Directory

Zarówno współpracy B2B usługi Azure Active Directory (Azure AD) i usługi Azure AD B2C można toowork użytkownikom zewnętrznym w usłudze Azure AD. Jednak sposób ich porównanie?


Możliwości współpracy B2B |     Azure AD B2C autonomicznej oferty.
-------- | --------
Przeznaczony dla: organizacji, które użytkownicy mogą tooauthenticate toobe od organizacji będącej partnerem, niezależnie od dostawcy tożsamości. | Przeznaczony dla: zapraszanie klientów przenośnych i aplikacji sieci web, czy osoby, klienci użyteczności publicznej lub organizacji do usługi Azure AD.
Obsługiwane tożsamości: pracownikom pracy lub kont służbowych, partnerów z konta służbowego lub dowolnego adresu e-mail. Wkrótce toosupport bezpośredniego federacji.  | Obsługiwane tożsamości: konsumenta użytkownikom kont lokalnych aplikacji (wszystkie wiadomości e-mail adres lub użytkownika nazwę) lub dowolny obsługiwany społecznościowych tożsamość w usłudze federacyjnej bezpośredniego.
Które znajdują się w katalogu użytkowników z firm partnerskich hello: partnera użytkownicy z organizacji zewnętrznych hello są zarządzane w tym samym katalogu co pracowników, ale adnotacjami hello specjalnie. Mogą być zarządzane hello takie same sposób jako pracowników, może być dodany toohello tej samej grupy i tak dalej  | Które znajdują się w katalogu powitania klienta użytkownika jednostki: hello katalogu aplikacji. Zarządzana oddzielnie od hello pracowników i partnerów katalogu firmy (jeśli istnieje.
Pojedynczy tooall logowania jednokrotnego (SSO) usługi Azure AD połączonych aplikacji jest obsługiwana. Na przykład możesz zapewnić dostęp tooOffice 365 lub aplikacji lokalnych i aplikacji SaaS tooother, takie jak Salesforce lub produktu Workday.  |  Należy toocustomer logowania jednokrotnego do aplikacji w ramach dzierżaw usługi Azure AD B2C hello jest obsługiwana. Usługa rejestracji Jednokrotnej tooOffice 365 lub aplikacji firmy Microsoft i innych niż Microsoft SaaS tooother nie jest obsługiwane.
Cykl życia partnera: zarządza hello hosta/zapraszanie organizacji.  | Cykl życia klienta: zarządzane przez aplikacji hello lub Samoobsługa.
Zasady zabezpieczeń i zgodności: zarządza hello hosta/zapraszanie organizacji.  | Zasady zabezpieczeń i zgodności: zarządza aplikacji hello.
Znakowanie: Brand hosta/zapraszanie organizacji jest używany.  |    Znakowanie: Zarządzane przez aplikację. Zwykle zwykle produktu toobe marki z hello Znikająca organizacji w tle hello.
Aby dowiedzieć się więcej: [wpis w blogu](https://blogs.technet.microsoft.com/enterprisemobility/2017/02/01/azure-ad-b2b-new-updates-make-cross-business-collab-easy/), [dokumentacji](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-b2b-what-is-azure-ad-b2b)  | Aby dowiedzieć się więcej: [stronę produktu](https://azure.microsoft.com/en-us/services/active-directory-b2c/), [dokumentacji](https://docs.microsoft.com/en-us/azure/active-directory-b2c/)


### <a name="next-steps"></a>Następne kroki

Zobacz nasze inne artykuły dotyczące współpracy B2B w usłudze Azure AD:

* [Czym jest współpraca B2B w usłudze Azure AD?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Właściwości użytkownika współpracy B2B](active-directory-b2b-user-properties.md)
* [Dodawanie roli tooa użytkownika współpracy B2B](active-directory-b2b-add-guest-to-role.md)
* [Delegowanie zaproszenia współpracy B2B](active-directory-b2b-delegate-invitations.md)
* [Grupami dynamicznymi i współpracy B2B](active-directory-b2b-dynamic-groups.md)
* [Konfigurowanie aplikacji SaaS do współpracy B2B](active-directory-b2b-configure-saas-apps.md)
* [Tokeny użytkownika współpracy B2B](active-directory-b2b-user-token.md)
* [Oświadczenia użytkowników współpracy B2B mapowania](active-directory-b2b-claims-mapping.md)
* [Udostępnianie zewnętrzne w usłudze Office 365](active-directory-b2b-o365-external-user.md)
* [Bieżące ograniczenia współpracy B2B](active-directory-b2b-current-limitations.md)
* [Uzyskiwanie pomocy technicznej dla współpracy B2B](active-directory-b2b-support.md)
