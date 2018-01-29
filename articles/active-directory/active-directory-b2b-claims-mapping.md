---
title: "Mapowanie w usłudze Azure Active Directory oświadczeń użytkowników współpracy B2B | Dokumentacja firmy Microsoft"
description: "mapowanie odwołania do usługi Azure Active Directory B2B współpracy oświadczeń"
services: active-directory
documentationcenter: 
author: sasubram
manager: mtillman
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
ms.openlocfilehash: 439219087d0a5027c729e9d0e0ecb90bd2a9de3c
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/11/2017
---
# <a name="b2b-collaboration-user-claims-mapping-in-azure-active-directory"></a>Mapowanie w usłudze Azure Active Directory oświadczeń użytkowników współpracy B2B

Dostosowywanie oświadczeń wydanych w tokenie SAML dla użytkowników współpracy B2B usługi Azure obsługuje usługi Active Directory (Azure AD). Podczas uwierzytelniania użytkownika do aplikacji, usługi Azure AD wystawia SAML token aplikacja, która zawiera informacje (lub oświadczenia) dotyczące użytkownika, który unikatowo identyfikuje je. Domyślnie w tym nazwę użytkownika, adres e-mail, imię i nazwisko użytkownika. Umożliwia wyświetlenie i edytowanie oświadczenia wysyłane w tokenie SAML do aplikacji na karcie atrybutów.

Istnieją dwie możliwe przyczyny, dlaczego konieczne może być Edycja oświadczeń wydanych w tokenie SAML.

1. Aplikacja została zapisana wymagają innego zestawu oświadczeń identyfikatorów URI lub wartości oświadczeń

2. Aplikacja wymaga oświadczeń NameIdentifier inny niż nazwa główna użytkownika przechowywane w usłudze Azure Active Directory.

  ![Widok oświadczenia w tokenie SAML](media/active-directory-b2b-claims-mapping/view-claims-in-saml-token.png)

Aby uzyskać informacje o tym, jak dodawać i edytować oświadczenia, zapoznaj się z tego artykułu na dostosowanie oświadczenia, [Dostosowywanie oświadczeń wydanych w tokenie SAML dla wstępnie zintegrowanych aplikacji w usłudze Azure Active Directory](develop/active-directory-saml-claims-customization.md). Do współpracy B2B użytkowników mapowania NameID i UPN dzierżawy między będą mogły ze względów bezpieczeństwa.


## <a name="next-steps"></a>Następne kroki

Zobacz nasze inne artykuły dotyczące współpracy B2B w usłudze Azure AD:

* [Czym jest współpraca B2B w usłudze Azure AD?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Właściwości użytkownika współpracy B2B](active-directory-b2b-user-properties.md)
* [Dodawanie do roli użytkownika współpracy B2B](active-directory-b2b-add-guest-to-role.md)
* [Delegowanie B2bB współpracy zaproszenia](active-directory-b2b-delegate-invitations.md)
* [Grupami dynamicznymi i współpracy B2B](active-directory-b2b-dynamic-groups.md)
* [Kod współpracy B2B i przykłady środowiska PowerShell](active-directory-b2b-code-samples.md)
* [Konfigurowanie aplikacji SaaS do współpracy B2B](active-directory-b2b-configure-saas-apps.md)
* [Udostępnianie zewnętrzne w usłudze Office 365](active-directory-b2b-o365-external-user.md)
* [Tokeny użytkownika współpracy B2B](active-directory-b2b-user-token.md)
* [Bieżące ograniczenia współpracy B2B](active-directory-b2b-current-limitations.md)
