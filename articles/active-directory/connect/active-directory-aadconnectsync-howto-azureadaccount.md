---
title: "Synchronizacja programu Azure AD Connect: jak konto usługi toomanage hello Azure AD | Dokumentacja firmy Microsoft"
description: "W tym temacie omówiono, jak konto usługi toorestore hello Azure AD."
services: active-directory
keywords: "AADSTS70002, AADSTS50054, w jaki sposób tooreset hello hasło dla hello synchronizacji Azure AD Connect konta usługi łącznika"
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 6077043a-27f1-4304-a44b-81dc46620f24
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: e563518eae173de42a1d40bb5a76e63f29f9da42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-how-toomanage-hello-azure-ad-service-account"></a>Synchronizacja programu Azure AD Connect: jak konto usługi toomanage hello Azure AD
usługi toobe wolnego powinien Hello konto usługi używane przez hello łącznika usługi Azure AD. Jeśli potrzebujesz tooreset swoje poświadczenia, w tym temacie jest dla Ciebie. Na przykład, jeśli Administrator globalny ma przez pomyłkę resetowania hello hasło konta usługi hello przy użyciu programu PowerShell.

## <a name="reset-hello-credentials"></a>Resetowanie poświadczeń hello
Jeśli konto usługi hello zdefiniowane na powitania łącznika usługi Azure AD nie można skontaktować się z usługi Azure AD powodu tooauthentication problemów, można zresetować hasła hello.

1. Zaloguj się na serwerze synchronizacji Azure AD Connect toohello i uruchom program PowerShell.
2. Uruchom polecenie `Add-ADSyncAADServiceAccount`.  
   ![Addadsyncaadserviceaccount polecenia cmdlet programu PowerShell](./media/active-directory-aadconnectsync-howto-azureadaccount/addadsyncaadserviceaccount.png)
3. Podaj poświadczenia administratora globalnego usługi Azure AD.

To polecenie cmdlet resetuje hello hasło dla konta usługi hello i zaktualizować go, zarówno w usłudze Azure AD, jak i w hello aparatu synchronizacji.

## <a name="known-issues-these-steps-can-solve"></a>Znane problemy można rozwiązać te kroki
W tej sekcji znajduje się lista błędów zgłaszanych przez klientów, które zostały usunięte przez poświadczenia, zresetuj na powitania konta usługi Azure AD.

- - -
Zdarzenie 6900  
Witaj serwer napotkał nieoczekiwany błąd podczas przetwarzania powiadomienia o zmianie hasła:  
AADSTS70002: Błąd podczas sprawdzania poprawności poświadczeń. AADSTS50054: Stare hasło jest używany do uwierzytelniania.

- - -
Zdarzenie 659  
Błąd podczas pobierania konfiguracji synchronizacji zasad haseł. Microsoft.IdentityModel.Clients.ActiveDirectory.AdalServiceException:  
AADSTS70002: Błąd podczas sprawdzania poprawności poświadczeń. AADSTS50054: Stare hasło jest używany do uwierzytelniania.

## <a name="next-steps"></a>Następne kroki
**Tematy poglądowe**

* [Synchronizacja programu Azure AD Connect: zrozumienie i dostosowywanie synchronizacji](active-directory-aadconnectsync-whatis.md)
* [Integrowanie tożsamości lokalnych z usługą Azure Active Directory](active-directory-aadconnect.md)

