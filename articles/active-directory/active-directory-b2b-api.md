---
title: "aaaAzure Active Directory B2B współpracy interfejsu API i dostosowywania | Dokumentacja firmy Microsoft"
description: "Współpraca z usługą Azure Active Directory B2B obsługuje relacji między firmami przez włączenie dostępu tooselectively partnerów biznesowych aplikacji firmowych"
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
ms.date: 04/11/2017
ms.author: sasubram
ms.openlocfilehash: 2609971ffa5d2ebc9466c61f4e4af11f5b045ecb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2b-collaboration-api-and-customization"></a>Dostosowywanie i Azure Active Directory B2B współpracy interfejsu API

Firma Microsoft zakończonej wielu klientów, poinformuj nas, czy chcą toocustomize hello zaproszenia procesu w taki sposób, który działa najlepiej w organizacji. O interfejsie API możesz to zrobić tylko. [https://Developer.microsoft.com/Graph/docs/API-Reference/V1.0/Resources/invitation](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation)

## <a name="capabilities-of-hello-invitation-api"></a>Możliwości zaproszenia hello interfejsu API
Witaj interfejsu API zapewniają hello następujące możliwości:

1. Zaproś użytkownika zewnętrznego z *żadnych* adres e-mail.

    ```
    "invitedUserDisplayName": "Sam"
    "invitedUserEmailAddress": "gsamoogle@gmail.com"
    ```

2. Dostosowywanie miejscu tooland Twojego użytkowników po zaakceptowaniu zaproszenia ich.

    ```
    "inviteRedirectUrl": "https://myapps.microsoft.com/"
    ```

3. Wybierz toosend hello standardowe zaproszeniu przez nas

    ```
    "sendInvitationMessage": true
    ```

  z adresata toohello komunikat, który można dostosować

    ```
    "customizedMessageBody": "Hello Sam, let's collaborate!"
    ```

4. I wybierz polecenie toocc: osób, które mają tookeep w hello pętli o tym współpracownika zaproszenie.

5. Lub całkowicie dostosować, wybierając nie toosend powiadomienia za pomocą usługi Azure AD Twojego zaproszenia i przepływ pracy dołączania.

    ```
    "sendInvitationMessage": false
    ```

  W takim przypadku wracając realizacji adres URL z hello interfejs API, który można osadzić w szablonu wiadomości e-mail, wiadomości Błyskawicznych lub innej metody dystrybucji wybranych przez użytkownika.

6. Ponadto jeśli jesteś administratorem, możesz tooinvite hello użytkownika jako element członkowski.

    ```
    "invitedUserType": "Member"
    ```


## <a name="authorization-model"></a>Modelu autoryzacji
Witaj interfejsu API mogą być uruchamiane w hello następujące tryby autoryzacji:

### <a name="app--user-mode"></a>Aplikacja + trybu użytkownika
W tym trybie, kto korzysta potrzeb hello interfejsu API toohave hello uprawnienia toobe Tworzenie zaproszeń do skorzystania z B2B.

### <a name="app-only-mode"></a>Tryb tylko do aplikacji
W kontekście tylko aplikacji hello aplikacja potrzebuje hello User.ReadWrite.All lub Directory.ReadWrite.All zakresów dla toosucceed zaproszenia hello.

Aby uzyskać więcej informacji, zapoznaj się: https://graph.microsoft.io/docs/authorization/permission_scopes


## <a name="powershell"></a>PowerShell
Łatwo jest teraz możliwe toouse środowiska PowerShell tooadd i zaprosić użytkowników zewnętrznych tooan organizacji. Utwórz zaproszenia przy użyciu polecenia cmdlet hello:

```
New-AzureADMSInvitation
```

Program hello następujące opcje:

* -InvitedUserDisplayName
* -InvitedUserEmailAddress
* -SendInvitationMessage
* -InvitedUserMessageInfo

Można również wyewidencjonować hello odwołanie zaproszenia interfejsu API w [https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation)

## <a name="next-steps"></a>Następne kroki

Zobacz nasze inne artykuły dotyczące współpracy B2B w usłudze Azure AD:

* [Czym jest współpraca B2B w usłudze Azure AD?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Jak Administratorzy usługi Azure Active Directory dodać użytkowników współpracy B2B?](active-directory-b2b-admin-add-users.md)
* [Jak pracownicy przetwarzający informacje dodać użytkowników współpracy B2B?](active-directory-b2b-iw-add-users.md)
* [elementy Hello hello wiadomość e-mail z zaproszeniem współpracy B2B](active-directory-b2b-invitation-email.md)
* [Realizacji zaproszenia współpracy B2B](active-directory-b2b-redemption-experience.md)
* [Azure licencjonowania współpracy B2B usługi AD](active-directory-b2b-licensing.md)
* [Rozwiązywanie problemów z współpracy usługi Azure Active Directory B2B](active-directory-b2b-troubleshooting.md)
* [Azure współpracy B2B usługi Active Directory — często zadawane pytania (FAQ)](active-directory-b2b-faq.md)
* [Usługa Multi-Factor Authentication dla użytkowników współpracy B2B](active-directory-b2b-mfa-instructions.md)
* [Dodawanie użytkowników współpracy B2B bez zaproszenia](active-directory-b2b-add-user-without-invite.md)
* [Indeks artykułów dotyczących zarządzania aplikacjami w usłudze Azure Active Directory](active-directory-apps-index.md)
