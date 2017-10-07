---
title: "aaaDelegate zaproszeń do współpracy usługi Azure Active Directory B2B | Dokumentacja firmy Microsoft"
description: "Właściwości użytkownika współpraca w usłudze Azure Active Directory B2B są konfigurowane"
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
ms.date: 05/23/2017
ms.author: sasubram
ms.openlocfilehash: c0122d6f60d494c6e251c41d947dc254ea887620
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="delegate-invitations-for-azure-active-directory-b2b-collaboration"></a>Delegowanie zaproszeń do skorzystania z usługi Azure Active Directory B2B współpracy

Ze współpracą między firmami (B2B) w usłudze Azure Active Directory (Azure AD) nie masz toobe zaproszenia toosend administratora globalnego. Zamiast tego można użyć zasad i delegować toousers zaproszenia, których role zezwolić im toosend zaproszeń do skorzystania z. Jest ważne nowy sposób toodelegate gościa użytkownika zaproszeń do skorzystania z za pomocą hello zapraszającej gościa roli.

## <a name="guest-inviter-role"></a>Rola zapraszającej gościa
Firma Microsoft można przypisać tooGuest użytkownika hello toosend zaproszeń do skorzystania z zapraszającej roli. Nie ma elementu członkowskiego toobe zaproszeń toosend roli administratora globalnego hello. Domyślnie normalnych użytkowników można także wywoływać interfejs API zaproszenia hello, chyba że administrator globalny wyłączone zaproszeń do normalnych użytkowników. Użytkownik może również wywołać hello interfejsu API przy użyciu hello portalu Azure lub programu PowerShell.

Oto przykład pokazujący sposób toouse PowerShell tooadd roli użytkownika gościa zapraszającej toohello:

```
Add-MsolRoleMember -RoleObjectId 95e79109-95c0-4d8e-aee3-d01accf2d47b -RoleMemberEmailAddress <RoleMemberEmailAddress>
```

## <a name="control-who-can-invite"></a>Formant, który można zaprosić

![Formant jak tooinvite](media/active-directory-b2b-delegate-invitations/control-who-to-invite.png)

Współpracy B2B usługi Azure AD administratora dzierżawy. można ustawić następujące zasady zaproszenia hello:

- Wyłącz zaproszenia
- Tylko administratorzy i użytkownicy w roli gościa zapraszającej hello można zaprosić
- Administratorzy, hello zapraszającej gościa roli i elementów członkowskich można zaprosić
- Wszyscy użytkownicy, w tym gości, można zaprosić

Dzierżawców są domyślnie zbyt #4. (Wszystkich użytkowników, w tym gości, można zaprosić użytkowników B2B).

## <a name="next-steps"></a>Następne kroki

Zobacz nasze inne artykuły dotyczące współpracy B2B w usłudze Azure AD:

* [Czym jest współpraca B2B w usłudze Azure AD?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Właściwości użytkownika współpracy B2B](active-directory-b2b-user-properties.md)
* [Dodawanie roli tooa użytkownika współpracy B2B](active-directory-b2b-add-guest-to-role.md)
* [Grupami dynamicznymi i współpracy B2B](active-directory-b2b-dynamic-groups.md)
* [Kod współpracy B2B i przykłady środowiska PowerShell](active-directory-b2b-code-samples.md)
* [Konfigurowanie aplikacji SaaS do współpracy B2B](active-directory-b2b-configure-saas-apps.md)
* [Tokeny użytkownika współpracy B2B](active-directory-b2b-user-token.md)
* [Oświadczenia użytkowników współpracy B2B mapowania](active-directory-b2b-claims-mapping.md)
* [Udostępnianie zewnętrzne w usłudze Office 365](active-directory-b2b-o365-external-user.md)
* [Bieżące ograniczenia współpracy B2B](active-directory-b2b-current-limitations.md)
