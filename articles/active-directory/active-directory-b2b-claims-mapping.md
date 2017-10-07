---
title: "mapowanie w usłudze Azure Active Directory oświadczeń użytkowników współpracy aaaB2B | Dokumentacja firmy Microsoft"
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
ms.date: 03/15/2017
ms.author: sasubram
ms.openlocfilehash: 9e26085e91a6004b2f11286ae9c1df133bd47341
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="b2b-collaboration-user-claims-mapping-in-azure-active-directory"></a>Mapowanie w usłudze Azure Active Directory oświadczeń użytkowników współpracy B2B

Dostosowywanie oświadczeń hello wydanych w tokenie SAML hello użytkowników współpracy B2B usługi Azure obsługuje usługi Active Directory (Azure AD). Podczas uwierzytelniania użytkownika aplikacji toohello, usługa Azure AD wystawia aplikacji toohello tokenu SAML, który zawiera informacje (lub oświadczenia) dotyczące hello użytkownika, który unikatowo identyfikuje je. Domyślnie w tym nazwę użytkownika, adres e-mail, imię i nazwisko użytkownika hello. Umożliwia wyświetlenie i edytowanie hello oświadczenia wysyłane w hello aplikacji toohello tokenu SAML hello karcie atrybutów.

Istnieją dwie możliwe przyczyny, dlaczego może być konieczne tooedit hello oświadczeń wydanych w tokenie SAML hello.

1. Aplikacja Hello została zapisana toorequire inny zestaw oświadczeń identyfikatorów URI lub wartości oświadczeń

2. Aplikacja wymaga hello NameIdentifier oświadczeń toobe inną niż nazwa główna użytkownika hello przechowywane w usłudze Azure Active Directory.

  ![Widok oświadczenia w tokenie SAML](media/active-directory-b2b-claims-mapping/view-claims-in-saml-token.png)

Aby informacji na temat sposobu tooadd i Edycja oświadczeń, zapoznaj się w tym artykule na dostosowanie oświadczenia, [Dostosowywanie oświadczeń wydanych w tokenie SAML hello wstępnie zintegrowanych aplikacji w usłudze Azure Active Directory](develop/active-directory-saml-claims-customization.md). Do współpracy B2B użytkowników mapowania NameID i UPN dzierżawy między będą mogły ze względów bezpieczeństwa.


## <a name="next-steps"></a>Następne kroki

Zobacz nasze inne artykuły dotyczące współpracy B2B w usłudze Azure AD:

* [Czym jest współpraca B2B w usłudze Azure AD?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Właściwości użytkownika współpracy B2B](active-directory-b2b-user-properties.md)
* [Dodawanie roli tooa użytkownika współpracy B2B](active-directory-b2b-add-guest-to-role.md)
* [Delegowanie B2bB współpracy zaproszenia](active-directory-b2b-delegate-invitations.md)
* [Grupami dynamicznymi i współpracy B2B](active-directory-b2b-dynamic-groups.md)
* [Kod współpracy B2B i przykłady środowiska PowerShell](active-directory-b2b-code-samples.md)
* [Konfigurowanie aplikacji SaaS do współpracy B2B](active-directory-b2b-configure-saas-apps.md)
* [Udostępnianie zewnętrzne w usłudze Office 365](active-directory-b2b-o365-external-user.md)
* [Tokeny użytkownika współpracy B2B](active-directory-b2b-user-token.md)
* [Bieżące ograniczenia współpracy B2B](active-directory-b2b-current-limitations.md)
