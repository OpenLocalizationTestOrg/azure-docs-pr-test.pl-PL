---
title: "aaaSet urządzenia z systemem Windows 10 z usługą Azure AD z ustawień | Dokumentacja firmy Microsoft"
description: "W tym artykule wyjaśniono, jak użytkownicy mogą dołączać tooAzure AD za pomocą menu Ustawienia hello."
services: active-directory
documentationcenter: 
author: femila
manager: swadhwa
editor: 
tags: azure-classic-portal
ms.assetid: b844e1d9-ad43-4e4a-a398-5c4a43bf2f5c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: d6485228338db571cc01f913c99fbba49e0bb74a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-windows-10-device-with-azure-ad-from-settings"></a>Konfigurowanie urządzenia Windows 10 z usługą Azure AD z ustawień
Jeśli masz już przy użyciu systemu Windows 7 lub Windows 8 i komputera lub urządzenia został uaktualniony tooWindows 10, można dołączyć tooAzure usługi Active Directory (Azure AD) za pośrednictwem hello ustawień menu.

## <a name="toojoin-tooazure-ad-from-hello-settings-menu"></a>toojoin tooAzure AD z menu ustawień hello
1. Z hello **Start** menu, kliknij przycisk hello **ustawienia** panelu.
2. Z **ustawienia**, wybierz pozycję **systemu**->**o**->**usługi Azure AD Join**.
   
   <center>
   ![Dołącz do usługi Azure AD z menu ustawień hello](./media/active-directory-azureadjoin/active-directory-azureadjoin-settings.png)</center>
3. Kliknij przycisk **Kontynuuj** w hello Azure AD Join w oknie wiadomości.
   
   <center>
   ![W oknie wiadomości usługi Azure AD JOIN](./media/active-directory-azureadjoin/active-directory-azureadjoin-message.png)</center>
4. Podaj poświadczenia logowania. To środowisko logowania będzie zawierać wszystkie kroki hello, które są wymagane toocomplete uwierzytelniania. Jeśli należą federacyjnych dzierżawcy, administrator zapewnia środowisko federacyjnego hello jest obsługiwana przez organizację.
   <center>
   ![Podaj poświadczenia logowania](./media/active-directory-azureadjoin/active-directory-azureadjoin-sign-in.png)</center>
5. Jeśli w organizacji są skonfigurowane uwierzytelnianie wieloskładnikowe Azure łączenia tooAzure AD, podaj hello czynnika przed kontynuowaniem.
6. Kliknij przycisk **Akceptuj** na powitania **zezwolić tej toobe urządzenia zarządzane** ekranu.
7. Powinna zostać wyświetlona wiadomość hello "urządzenie jest teraz tooyour dołączonego do organizacji w usłudze Azure AD".

## <a name="additional-information"></a>Dodatkowe informacje
* [Dowiedz się więcej na temat scenariuszy użycia funkcji Azure AD Join](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [Łączenie urządzeń przyłączonych do domeny tooAzure AD dla systemu Windows 10](active-directory-azureadjoin-devices-group-policy.md)
* [Konfigurowanie funkcji Azure AD Join](active-directory-azureadjoin-setup.md)
* [Uwierzytelnianie tożsamości bez hasła przy użyciu Microsoft Passport](active-directory-azureadjoin-passport.md)

