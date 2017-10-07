---
title: "aaaDynamic grup i współpracy usługi Azure Active Directory B2B | Dokumentacja firmy Microsoft"
description: "Azure współpracy B2B usługi Active Directory mogą być używane z grupami dynamicznymi w usłudze Azure AD"
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
ms.date: 06/27/2017
ms.author: curtand
ms.reviewer: sasubram
ms.openlocfilehash: b011298de5fd2c851c6d9caaf5c2b257807ef0a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="dynamic-groups-and-azure-active-directory-b2b-collaboration"></a>Grupami dynamicznymi i współpracy usługi Azure Active Directory B2B

## <a name="what-are-dynamic-groups"></a>Co to są grupami dynamicznymi?
Dynamicznej konfiguracji przynależności do grupy zabezpieczeń usługi Azure Active Directory (Azure AD) jest dostępna w [hello portalu Azure](https://portal.azure.com). Administratorzy mogą ustawiać zasady grupy toopopulate, które zostały utworzone w usłudze Azure Active Directory na podstawie atrybutów użytkownika (na przykład userType, działu lub kraju). Elementy Członkowskie mogą być automatycznie dodawane tooor usunięte z grupy zabezpieczeń na podstawie ich atrybutów. Te grupy może zapewnić dostęp do zasobów tooapplications lub w chmurze (witryny programu SharePoint, dokumenty) i tooassign licencje toomembers. Przeczytaj więcej na temat grup dynamicznych w [grup w usłudze Azure Active Directory w wersji dedykowanej](active-directory-accessmanagement-dedicated-groups.md).

Witaj odpowiednie [licencjonowania usługi Azure AD Premium P1 lub P2](https://azure.microsoft.com/pricing/details/active-directory/) jest wymagane toocreate i używania grup dynamicznych. Dowiedz się więcej informacji, zobacz artykuł hello [tworzenia reguł opartych na atrybutach dynamiczne członkostwo w grupie w usłudze Azure Active Directory](active-directory-groups-dynamic-membership-azure-portal.md).

## <a name="what-are-hello-built-in-dynamic-groups"></a>Co to są hello wbudowane grupy dynamiczne?
Witaj **wszyscy użytkownicy** grupa dynamiczna umożliwia toocreate Administratorzy dzierżawy kliknij zawierającego wszystkich użytkowników w dzierżawie powitalnych za pomocą jednej grupy. Domyślnie program hello **wszyscy użytkownicy** grupy należą wszyscy użytkownicy w katalogu hello, w tym elementów członkowskich i gości.
Witaj nowego portalu administracyjnego usługi Azure Active Directory, można wybrać tooenable hello **wszyscy użytkownicy** w hello wyświetlić ustawienia grupy.

![grupy wbudowane](media/active-directory-b2b-dynamic-groups/built-in-groups.png)

## <a name="hardening-hello-all-users-dynamic-group"></a>Ograniczanie funkcjonalności hello wszystkich Dynamiczna grupa użytkowników
Domyślnie program hello **wszyscy użytkownicy** grupa zawiera również użytkowników (Gość) współpracy B2B. Można dodatkowo zabezpieczyć Twoje **wszyscy użytkownicy** grupy przy użyciu reguły tooremove gości. Witaj poniższej ilustracji przedstawiono hello **wszyscy użytkownicy** modyfikacja grupy Goście tooexclude.

![Włącz wszystkie grupy użytkowników](media/active-directory-b2b-dynamic-groups/enable-all-users-group.png)

Można także znaleźć go przydatne toocreate nową grupę dynamicznych, zawierającą tylko gości, dzięki czemu można zastosować toothem zasad (np. zasady dostępu warunkowego AD Azure).
Jakie takiej grupy może wyglądać tak:

![Wyklucz gości](media/active-directory-b2b-dynamic-groups/exclude-guest-users.png)

## <a name="next-steps"></a>Następne kroki

Zobacz nasze inne artykuły dotyczące współpracy B2B w usłudze Azure AD:

* [Czym jest współpraca B2B w usłudze Azure AD?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Właściwości użytkownika współpracy B2B](active-directory-b2b-user-properties.md)
* [Dodawanie roli tooa użytkownika współpracy B2B](active-directory-b2b-add-guest-to-role.md)
* [Delegowanie zaproszenia współpracy B2B](active-directory-b2b-delegate-invitations.md)
* [Kod współpracy B2B i przykłady środowiska PowerShell](active-directory-b2b-code-samples.md)
* [Konfigurowanie aplikacji SaaS do współpracy B2B](active-directory-b2b-configure-saas-apps.md)
* [Tokeny użytkownika współpracy B2B](active-directory-b2b-user-token.md)
* [Oświadczenia użytkowników współpracy B2B mapowania](active-directory-b2b-claims-mapping.md)
* [Udostępnianie zewnętrzne w usłudze Office 365](active-directory-b2b-o365-external-user.md)
* [Bieżące ograniczenia współpracy B2B](active-directory-b2b-current-limitations.md)
