---
title: "uwierzytelnianie wieloskładnikowe toorequire aaaHow | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toorequire uwierzytelnianie wieloskładnikowe (MFA) dla uprzywilejowany tożsamości z hello rozszerzenia usługi Azure Active Directory Privileged Identity Management."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 1e3dc4ad-3a6a-4a52-8417-3ca4f84ae05c
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: c08fad9dc80c09a14a4bd7497da4942fa227c3ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toorequire-mfa-in-azure-ad-privileged-identity-management"></a>Jak toorequire MFA w usłudze Azure AD Privileged Identity Management
Firma Microsoft zaleca wymusić uwierzytelnianie wieloskładnikowe (MFA) dla wszystkich Administratorzy w Twojej organizacji. Zmniejszają one ryzyko hello ataku powodu hasła tooa naruszenia zabezpieczeń.

Możesz wymagać użytkownicy powinni wykonać żądanie uwierzytelniania MFA, po zalogowaniu. Witaj w blogu [MFA dla usługi Office 365 i uwierzytelniania Wieloskładnikowego na platformie Azure](https://blogs.technet.microsoft.com/ad/2014/02/11/mfa-for-office-365-and-mfa-for-azure/) porównuje dostępnych w ramach subskrypcji pakietu Office i usługi Azure, z funkcjami hello zawarte w hello oferta Microsoft Azure Multi-Factor Authentication.

Możesz również wymagać, że użytkownicy aktywują rola w programie Azure AD PIM, wykonać żądanie uwierzytelniania MFA. Dzięki temu, jeśli hello użytkownika nie została ukończona żądanie uwierzytelniania MFA, gdy są one podpisane, zostaną one toodo zostanie wyświetlony monit o tak przez usługi PIM.

## <a name="requiring-mfa-in-azure-ad-privileged-identity-management"></a>Wymagania uwierzytelniania Wieloskładnikowego w Azure AD Privileged Identity Management
W przypadku zarządzania tożsamościami w PIM jako administrator ról uprzywilejowanych, mogą pojawić się alerty, które zalecamy MFA do kont uprzywilejowanych. Kliknij kartę Zabezpieczenia hello alertu w pulpicie nawigacyjnym usługi PIM hello i nowy blok zostanie otwarty z listą kont administratora hello, które należy włączyć usługę MFA.  Uwierzytelniania MFA można wymagać, wybierając wiele ról, a następnie klikając polecenie hello **napraw** przycisku, lub kliknij przycisk Dalej ról tooindividual hello wielokropek można a następnie kliknij przycisk hello **napraw** przycisku.

> [!IMPORTANT]
> Kliknij prawym przyciskiem myszy obecnie działa tylko usługi Azure MFA z pracą lub konta służbowego, nie kont Microsoft (zazwyczaj konta osobistego używanej toosign w tooMicrosoft usług takich jak Skype, Xbox, Outlook.com, itp.). W związku z tym każda osoba, która za pomocą konta Microsoft nie może być administratorem kwalifikujących się nie mogą używać usługi MFA tooactivate ich ról. Jeśli Ci użytkownicy będą potrzebować toocontinue Zarządzanie obciążeń przy użyciu konta Microsoft, podniesienia uprawnień ich Administratorzy toopermanent teraz.
> 
> 

Ponadto hello wymaganie usługi MFA dla konkretnej roli można zmienić, klikając w hello ról części pulpitu nawigacyjnego PIM hello. Następnie kliknij **ustawienia** w bloku roli hello, a następnie wybierając **włączyć** w obszarze usługi Multi-Factor authentication.

## <a name="how-azure-ad-pim-validates-mfa"></a>Jak Azure AD PIM weryfikuje MFA
Dostępne są dwie opcje sprawdzania poprawności MFA, gdy użytkownik aktywuje roli.

najprostsza opcja Hello jest toorely na usługę Azure MFA dla użytkowników, którzy są Aktywacja ról uprzywilejowanych. toodo, pierwszy Sprawdź, czy Ci użytkownicy są licencjonowane w razie potrzeby i zarejestrowany dla usługi Azure MFA. Więcej informacji na temat sposobu toodo jest [wprowadzenie do korzystania z usługi Azure Multi-Factor Authentication w chmurze hello](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md). Jest zalecane, ale nie wymagane, skonfiguruj tooenforce usługi Azure AD MFA dla tych użytkowników, po zalogowaniu. Jest to spowodowane hello MFA kontroli będą wykonywane przez usługi Azure AD PIM samej siebie.

Alternatywnie użytkownicy są uwierzytelniani lokalnie może mieć odpowiedzialny za MFA dostawcy tożsamości. Na przykład, jeśli skonfigurowano uwierzytelnianie oparte na karty inteligentnej pakietu usługi federacyjnej AD toorequire przed uzyskaniem dostępu do usługi Azure AD [zabezpieczanie zasobów w chmurze Azure Multi-Factor Authentication i usług AD FS](../multi-factor-authentication/multi-factor-authentication-get-started-adfs-cloud.md) zawiera instrukcje w celu skonfigurowania usług AD FS toosend oświadczeń tooAzure AD. Gdy użytkownik próbuje tooactivate roli, Azure AD PIM będzie akceptować czy MFA została już sprawdzona dla użytkownika powitania po otrzymaniu hello odpowiednie oświadczenia.

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Następne kroki
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

