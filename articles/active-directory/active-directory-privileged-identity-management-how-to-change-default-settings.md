---
title: ustawienia aktywacji roli toomanage aaaHow | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toochange hello domyślne ustawienia dla tożsamości uprzywilejowanych z hello rozszerzenia usługi Azure Active Directory Privileged Identity Management."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: f6cbcb6a-8a89-4077-afd8-06c94a64f4aa
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: 453bb6f8f8e0fd2598cb073ef86c1dd55458dc72
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-role-activation-settings-in-azure-ad-privileged-identity-management"></a>Jak ustawienia aktywacji roli toomanage w usłudze Azure AD Privileged Identity Management
Administrator ról uprzywilejowanych można dostosować w usłudze Azure AD Privileged Identity Management (PIM) w organizacji, łącznie ze zmianą hello środowisko dla użytkownika, który jest aktywowanie przypisania roli kwalifikujących się.

## <a name="manage-hello-role-activation-settings"></a>Zarządzanie ustawieniami aktywacji roli hello
1. Przejdź toohello [portalu Azure](https://portal.azure.com) i wybierz hello **Azure AD Privileged Identity Management** aplikacji z hello pulpitu nawigacyjnego.
2. Wybierz **Zarządzanie ról uprzywilejowanych** > **ustawienia** > **ról uprzywilejowanych**.
3. Wybierz rolę hello, którego ustawienia chcesz toomanage.

Na stronie Ustawienia powitania dla każdej roli istnieje wiele ustawień, które można skonfigurować. Te ustawienia dotyczą tylko użytkownicy, którzy są kwalifikujących się Administratorzy, Administratorzy nie trwałych.

**Aktywacje**: hello czasu, w godzinach, które roli pozostaje aktywne, przed jego wygaśnięciem. Może to być w przedziale od 1 do 72 godzin.

**Powiadomienia**: można wybrać, czy hello system wysyła potwierdzenie, że ich uaktywniono rolę tooadmins wiadomości e-mail. Może to być przydatne do wykrywania nieautoryzowanego lub nielegalne aktywacji.

**Zdarzenie/żądania biletu**: można wybrać, czy toorequire tooinclude kwalifikujących się administratorów biletu numerów podczas aktywują ich roli. Może to być przydatne podczas wykonywania inspekcji dostępu do roli.

**Uwierzytelnianie wieloskładnikowe**: można wybrać, czy toorequire tooverify użytkowników tożsamości za pomocą usługi MFA aktywować ich ról. Tylko mają tooverify tego raz dla sesji, nie za każdym razem, gdy ich aktywowania roli. Istnieją dwa tookeep porady na uwadze, po włączeniu usługi MFA:

* Użytkownicy, którzy mają konta Microsoft do ich adresów e-mail (zazwyczaj @outlook.com, ale nie zawsze) nie można zarejestrować w usłudze Azure MFA. Chcesz tooassign toousers ról z kontami Microsoft, należy były administratorów trwałych lub Wyłącz uwierzytelnianie wieloskładnikowe dla tej roli.
* Nie można wyłączyć usługi MFA dla wysoko uprzywilejowane ról dla usługi Azure AD i usługi Office 365. Jest to zabezpieczenie, ponieważ te role powinny być starannie chronione:  
  
  * Administrator aplikacji
  * Administrator serwera Proxy aplikacji
  * Administrator rozliczeń  
  * Administrator zgodności  
  * Administrator programu CRM usługi
  * Osoba zatwierdzająca dostępu skrytki klienta
  * Składnik zapisywania katalogu  
  * Administrator programu Exchange  
  * Administrator globalny
  * Administrator usługi Intune
  * Skrzynki pocztowej administratora  
  * Obsługa tier1 partnera  
  * Obsługa tier2 partnera  
  * Administrator ról uprzywilejowanych   
  * Administrator zabezpieczeń  
  * Administrator programu SharePoint  
  * Administrator programu Skype dla firm  
  * Administrator konta użytkownika  

Aby uzyskać więcej informacji na temat przy użyciu usługi MFA w usłudze PIM zobacz [jak tooRequire MFA](active-directory-privileged-identity-management-how-to-require-mfa.md).

<!--PLACEHOLDER: Need an explanation of what hello temporary Global Administrator setting is for.-->

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Następne kroki
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

